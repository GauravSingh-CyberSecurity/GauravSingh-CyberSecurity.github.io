---
layout: page
title: About Me
permalink: /about/
---

<div class="hero" style="padding: 2rem 0;">
  <div class="hero-content">
    <img src="{{ '/images/profile.svg' | prepend: site.baseurl }}" alt="{{ site.author.name }}" class="hero-image">
    <h1 class="hero-title">About {{ site.title }}</h1>
    <p class="hero-tagline">{{ site.tagline }}</p>
  </div>
</div>

<div class="wrapper" style="max-width: 800px;">

## Professional Background

Hi, I'm Gaurav Singh (aka @singhggithub). I'm a Cybersecurity Engineer specializing in Vulnerability Assessment and Penetration Testing (VAPT), with hands-on experience in exploiting OWASP Top 10, Web, API, Android misconfigurations, and business logic flaws across enterprise applications.

Currently working as an Information Security Engineer at Harrier Information Systems PVT LTD, I'm proficient in discovering vulnerabilities related to authentication, authorization, injection flaws, business logic bypasses, server misconfigurations, and API-specific issues.

## What I Do

- **Black-box & Gray-box VAPT**: Comprehensive security assessments focusing on OWASP Top 10, API security flaws, and business logic vulnerabilities
- **Exploit Development**: Automating test cases and exploit development using Python, Bash, and JavaScript
- **Incident Response**: Leading end-to-end incident response and post-exploitation VAPT on web applications
- **Security Tool Development**: Creating custom offensive security tools and PoCs, including Burp Suite extensions
- **Red Team Operations**: Simulating advanced attacks including Kerberoasting, AS-REP Roasting, and Pass-the-Hash

## Experience & Expertise

### Technical Skills
- **Web/App Security**: Burp Suite Pro, Postman, OWASP ZAP, Nmap
- **Exploitation Tools**: SQLMap, Metasploit, Nikto, John the Ripper, Hashcat
- **Reconnaissance**: FFUF, Subfinder, Gobuster, Amass, WAFW00F
- **Programming Languages**: Python, JavaScript, Bash
- **Security Standards**: OWASP Top 10, MITRE ATT&CK, CVE
- **Attack Vectors**: SQLi, XSS, SSRF, RCE, IDOR, File Inclusion, Auth Bypass, XXE, Command Injection, API Misconfig, BOLA, Broken Auth, CSRF, Subdomain Takeover, Clickjacking, Session Fixation, CORS Misconfig, Insecure Deserialization

### Current Certifications & Training
- **Bug Bounty Hunter** - Hack The Box Academy (2025)
- **Practical Ethical Hacking – The Complete Course** - TCM Security (2024)
- **Intro to Bug Bounty Hunting and Web Application Hacking** - NahamSec (2025)

## Recent Projects

### BNHS Incident Response: Broken Auth to RCE Exploitation Chain
Led end-to-end incident response and conducted post-exploitation VAPT on Laravel, WordPress, and CodeIgniter applications. Successfully analyzed and reversed obfuscated PHP backdoors, removed SEO spam injections, and reinforced server entry vectors against RCE and web shell (Backdoor) attacks.

### Custom Burp Suite Extension Development
Created custom Burp Suite extension for detecting shell access patterns and automated exploit chains during black-box assessments, significantly improving the efficiency of vulnerability discovery.

### Red Team Attack Simulation
Simulated advanced red team attacks including Kerberoasting, AS-REP Roasting, and Pass-the-Hash using BloodHound and CrackMapExec for internal network reconnaissance and privilege escalation.

## Education & Training

**Bachelor of Engineering in Computer Science (Cyber Security)**  
Shri Ramdeobaba College of Engineering and Management (RCOEM) - 2024  
CGPA: 7.6 / 10.0

**Relevant Coursework**: Network Security, Operating Systems, Cryptography, Ethical Hacking, Web Application Security, Bug Bounty Hunting

I believe in continuous learning and regularly participate in security conferences, CTF competitions, and training programs. I also contribute to the security community through:

- **Tool Development**: Creating offensive security tools and PoCs in Python for buffer overflows, bind shells, SSH brute forcing, keyloggers, and hash cracking
- **Research**: Developing automated exploit chains and vulnerability assessment techniques
- **Professional Practice**: Delivering detailed technical reports with PoCs and remediation steps for enterprise applications
- **Mentoring**: Helping organizations strengthen their security posture through comprehensive VAPT assessments

## Personal Interests

When I'm not diving deep into security research, I enjoy:
- Participating in bug bounty programs
- Contributing to open-source security projects
- Playing capture-the-flag (CTF) competitions
- Reading about emerging technologies and their security implications

## Let's Connect

I'm always interested in discussing cybersecurity topics, sharing knowledge, and collaborating on interesting projects. Feel free to reach out through any of the channels below:

- **Email**: [{{ site.email }}](mailto:{{ site.email }})
- **LinkedIn**: [Connect with me](https://linkedin.com/in/{{ site.linkedin_username }})
- **GitHub**: [View my projects](https://github.com/{{ site.github_username }})
- **Twitter**: [Follow me](https://twitter.com/{{ site.twitter_username }})

</div>
