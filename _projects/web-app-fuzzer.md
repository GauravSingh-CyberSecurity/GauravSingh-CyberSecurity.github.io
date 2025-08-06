---
layout: page
title: "Web Application Fuzzer"
tech: ["Python", "Web Security", "Fuzzing"]
excerpt: "An intelligent web application fuzzer that can discover hidden directories, files, and parameters."
---

# Web Application Fuzzer

An intelligent and efficient web application fuzzer designed for comprehensive web security testing and bug bounty hunting.

## Overview

This fuzzer combines traditional directory/file discovery with advanced parameter fuzzing capabilities. It's built to be fast, intelligent, and thorough in discovering hidden attack surfaces in web applications.

## Key Features

### 🎯 Comprehensive Discovery
- **Directory & File Fuzzing**: Discovers hidden paths and files
- **Parameter Discovery**: Finds hidden GET/POST parameters
- **Subdomain Enumeration**: Identifies subdomains and virtual hosts
- **Technology Detection**: Identifies web technologies and frameworks

### 🧠 Intelligent Fuzzing
- **Recursive Scanning**: Automatically explores discovered directories
- **Response Analysis**: Intelligent filtering of false positives
- **Custom Wordlists**: Support for multiple wordlist formats
- **Rate Limiting**: Configurable request rates to avoid detection

## Technical Architecture

```python
#!/usr/bin/env python3
"""
Intelligent Web Application Fuzzer
Author: Gaurav Singh
"""

import requests
import threading
import time
from urllib.parse import urljoin, urlparse
from concurrent.futures import ThreadPoolExecutor
import queue

class WebFuzzer:
    def __init__(self, target_url, wordlist_path, threads=50):
        self.target_url = target_url
        self.wordlist_path = wordlist_path
        self.threads = threads
        self.session = requests.Session()
        self.discovered_paths = []
        self.queue = queue.Queue()
        self.setup_session()
        
    def setup_session(self):
        """Configure session with proper headers and settings"""
        self.session.headers.update({
            'User-Agent': 'Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36',
            'Accept': 'text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8',
            'Accept-Language': 'en-US,en;q=0.5',
            'Accept-Encoding': 'gzip, deflate',
            'Connection': 'keep-alive',
        })
        
    def load_wordlist(self):
        """Load and prepare wordlist for fuzzing"""
        try:
            with open(self.wordlist_path, 'r') as f:
                wordlist = [line.strip() for line in f if line.strip()]
            return wordlist
        except FileNotFoundError:
            print(f"Wordlist file not found: {self.wordlist_path}")
            return []
    
    def make_request(self, url, method='GET', data=None):
        """Make HTTP request with error handling"""
        try:
            if method.upper() == 'GET':
                response = self.session.get(url, timeout=10)
            elif method.upper() == 'POST':
                response = self.session.post(url, data=data, timeout=10)
            else:
                return None
                
            return response
        except requests.exceptions.RequestException as e:
            return None
    
    def analyze_response(self, response, path):
        """Analyze response to determine if path is interesting"""
        if not response:
            return False
            
        # Skip common error responses
        if response.status_code in [404, 403, 500]:
            return False
            
        # Check for redirects to login or error pages
        if response.status_code == 302:
            location = response.headers.get('Location', '')
            if 'login' in location.lower() or 'error' in location.lower():
                return False
                
        # Analyze content length and type
        content_length = len(response.content)
        content_type = response.headers.get('Content-Type', '')
        
        # Skip very small responses (likely error pages)
        if content_length < 100:
            return False
            
        # Interesting status codes
        if response.status_code in [200, 301, 302, 401, 403]:
            return True
            
        return False
    
    def fuzz_directories(self, base_url, wordlist):
        """Fuzz directories and files"""
        discovered = []
        
        with ThreadPoolExecutor(max_workers=self.threads) as executor:
            futures = []
            
            for word in wordlist:
                # Test as directory
                dir_url = urljoin(base_url, word + '/')
                future = executor.submit(self.test_path, dir_url, word + '/')
                futures.append(future)
                
                # Test as file
                file_url = urljoin(base_url, word)
                future = executor.submit(self.test_path, file_url, word)
                futures.append(future)
                
                # Test common extensions
                for ext in ['.php', '.asp', '.aspx', '.jsp', '.html', '.txt']:
                    file_ext_url = urljoin(base_url, word + ext)
                    future = executor.submit(self.test_path, file_ext_url, word + ext)
                    futures.append(future)
            
            for future in futures:
                result = future.result()
                if result:
                    discovered.append(result)
                    
        return discovered
```

## Fuzzing Modes

### Directory Discovery
- **Common Directories**: Admin panels, config directories, backups
- **Technology-Specific**: Framework-specific paths (WordPress, Drupal, etc.)
- **Recursive Discovery**: Automatically explores found directories
- **Custom Extensions**: Tests multiple file extensions

### Parameter Fuzzing
- **GET Parameters**: Hidden query string parameters
- **POST Parameters**: Form field discovery
- **Header Fuzzing**: Custom header parameter testing
- **JSON/XML**: API parameter discovery

### Advanced Techniques
- **Virtual Host Discovery**: Finds virtual hosts on the same IP
- **HTTP Method Testing**: Tests different HTTP methods
- **Authentication Bypass**: Attempts to bypass authentication
- **Error Page Analysis**: Extracts information from error responses

## Smart Filtering

### Response Analysis
- **Content Length Filtering**: Filters based on response size
- **Status Code Analysis**: Intelligent status code handling
- **Content Similarity**: Detects and filters similar responses
- **Regex Patterns**: Custom pattern matching for interesting content

### False Positive Reduction
- **Baseline Establishment**: Creates response baselines
- **Dynamic Filtering**: Adapts to application behavior
- **Machine Learning**: Uses ML for response classification
- **Human Verification**: Flags responses for manual review

## Usage Examples

### Basic Directory Fuzzing
```bash
python web_fuzzer.py --url https://example.com --wordlist common.txt --threads 50
```

### Recursive Fuzzing
```bash
python web_fuzzer.py --url https://example.com --wordlist big.txt --recursive --depth 3
```

### Parameter Discovery
```bash
python web_fuzzer.py --url https://example.com/search --mode params --wordlist params.txt
```

### Subdomain Enumeration
```bash
python web_fuzzer.py --url example.com --mode subdomains --wordlist subdomains.txt
```

## Wordlist Management

### Built-in Wordlists
- **Common Directories**: Top 10,000 web directories
- **Technology-Specific**: CMS, framework-specific paths
- **File Extensions**: Common web file extensions
- **Parameters**: Common parameter names

### Custom Wordlists
- **Domain-Specific**: Industry-specific terminology
- **Technology-Based**: Framework and language specific
- **Historical Data**: Previously discovered paths
- **Crowd-Sourced**: Community-contributed wordlists

## Performance Optimization

- **Connection Pooling**: Reuses HTTP connections
- **Intelligent Threading**: Dynamic thread management
- **Memory Efficiency**: Streams large wordlists
- **Request Batching**: Groups similar requests

## Reporting Features

### Real-time Output
- **Live Discovery**: Shows findings as they're discovered
- **Progress Tracking**: Real-time progress indicators
- **Error Monitoring**: Tracks and reports errors
- **Rate Monitoring**: Shows current request rates

### Comprehensive Reports
- **HTML Reports**: Web-based interactive reports
- **JSON Output**: Machine-readable results
- **CSV Export**: Spreadsheet-compatible format
- **Integration**: Outputs compatible with other tools

## Integration Capabilities

- **Burp Suite**: Imports/exports Burp projects
- **OWASP ZAP**: Compatible with ZAP spider results
- **Custom Scripts**: Plugin system for custom checks
- **CI/CD Integration**: Automated testing in pipelines

## Security Features

- **Request Throttling**: Respects server resources
- **User-Agent Rotation**: Avoids blocking
- **Proxy Support**: Routes traffic through proxies
- **SSL/TLS Handling**: Proper certificate handling

## Advanced Configuration

```python
# Configuration example
config = {
    'threads': 100,
    'delay': 0.1,
    'timeout': 10,
    'follow_redirects': True,
    'max_depth': 3,
    'extensions': ['.php', '.asp', '.jsp'],
    'status_codes': [200, 301, 302, 403],
    'user_agents': ['Mozilla/5.0...', 'curl/7.68.0'],
    'proxy': 'http://127.0.0.1:8080'
}
```

## Future Enhancements

- **Machine Learning Integration**: AI-powered path prediction
- **Cloud-Native**: Support for cloud application testing
- **API Fuzzing**: Specialized REST/GraphQL fuzzing
- **Mobile App Testing**: Mobile application fuzzing

---

*This tool is designed for authorized security testing only. Always ensure proper authorization before testing web applications.*
