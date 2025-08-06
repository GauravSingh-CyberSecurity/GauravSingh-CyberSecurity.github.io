---
layout: page
title: CV
permalink: /cv/
---

<div class="hero" style="padding: 2rem 0;">
  <div class="hero-content">
    <img src="{{ '/images/profile.svg' | prepend: site.baseurl }}" alt="{{ site.author.name }}" class="hero-image">
    <h1 class="hero-title">Curriculum Vitae</h1>
    <p class="hero-tagline">{{ site.tagline }}</p>
  </div>
</div>

<div class="wrapper" style="max-width: 1000px;">

## Professional Resume

I embed a current version of my CV below. You can also [**download the PDF here**]({{ '/files/Gaurav_Security-Analyst_VAPT_2yrs_30days_np.pdf' | prepend: site.baseurl }}).

<div style="background: #f8f9fa; padding: 1.5rem; border-radius: 8px; margin: 2rem 0; text-align: center; border: 1px solid #ecf0f1;">
  <p style="margin: 0; color: #7f8c8d; font-size: 1rem;">
    <strong>{{ site.author.name }}</strong> • {{ site.email }} • 
    <a href="{{ site.url }}" target="_blank" style="color: #2c3e50; text-decoration: none;">{{ site.url | remove: 'https://' }}</a>
  </p>
  <div style="margin-top: 0.5rem;">
    <a href="https://github.com/{{ site.github_username }}" target="_blank" style="margin: 0 0.5rem; color: #2c3e50; text-decoration: none;">
      <i class="fab fa-github"></i> {{ site.github_username }}
    </a>
    <a href="https://linkedin.com/in/{{ site.linkedin_username }}" target="_blank" style="margin: 0 0.5rem; color: #2c3e50; text-decoration: none;">
      <i class="fab fa-linkedin"></i> LinkedIn
    </a>
  </div>
</div>

<div style="width: 100%; height: 800px; border: 1px solid #ecf0f1; border-radius: 8px; overflow: hidden; box-shadow: 0 8px 16px rgba(0, 0, 0, 0.1);">
  <iframe 
    src="{{ '/files/Gaurav_Security-Analyst_VAPT_2yrs_30days_np.pdf' | prepend: site.baseurl }}" 
    width="100%" 
    height="100%" 
    style="border: none;">
    <p>Your browser does not support PDFs. 
      <a href="{{ '/files/Gaurav_Security-Analyst_VAPT_2yrs_30days_np.pdf' | prepend: site.baseurl }}">Download the PDF</a> instead.
    </p>
  </iframe>
</div>

<div style="text-align: center; margin-top: 2rem;">
  <a href="{{ '/files/Gaurav_Security-Analyst_VAPT_2yrs_30days_np.pdf' | prepend: site.baseurl }}" 
     style="display: inline-block; padding: 12px 24px; background: #2c3e50; color: white; text-decoration: none; border-radius: 6px; font-weight: 500; margin: 0 1rem;">
    <i class="fas fa-download"></i> Download PDF
  </a>
  <a href="{{ '/contact/' | prepend: site.baseurl }}" 
     style="display: inline-block; padding: 12px 24px; background: transparent; color: #2c3e50; text-decoration: none; border: 2px solid #2c3e50; border-radius: 6px; font-weight: 500; margin: 0 1rem;">
    <i class="fas fa-envelope"></i> Contact Me
  </a>
</div>

## Professional Summary

**{{ site.author.bio }}**

Proficient in discovering vulnerabilities related to authentication, authorization, injection flaws, business logic bypasses, server misconfigurations, recon-based exposures, and API-specific issues. Experienced in automating test cases and exploit development using Python, Bash, and JavaScript in black-box and gray-box VAPT scenarios.

### Technical Skills

<div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(350px, 1fr)); gap: 2rem; margin: 2rem 0;">
  <div style="background: #f8f9fa; padding: 1.5rem; border-radius: 8px; border-left: 4px solid #2c3e50;">
    <h4 style="margin: 0 0 1rem 0; color: #2c3e50;">
      <i class="fas fa-shield-alt"></i> Web/App Security
    </h4>
    <p style="margin: 0; color: #555;">Burp Suite Pro, Postman, OWASP ZAP, Nmap</p>
  </div>
  
  <div style="background: #f8f9fa; padding: 1.5rem; border-radius: 8px; border-left: 4px solid #e74c3c;">
    <h4 style="margin: 0 0 1rem 0; color: #e74c3c;">
      <i class="fas fa-bug"></i> Exploitation
    </h4>
    <p style="margin: 0; color: #555;">SQLMap, Metasploit, Nikto, John the Ripper, Hashcat</p>
  </div>
  
  <div style="background: #f8f9fa; padding: 1.5rem; border-radius: 8px; border-left: 4px solid #3498db;">
    <h4 style="margin: 0 0 1rem 0; color: #3498db;">
      <i class="fas fa-search"></i> Reconnaissance
    </h4>
    <p style="margin: 0; color: #555;">FFUF, Subfinder, Gobuster, Amass, WAFW00F</p>
  </div>
  
  <div style="background: #f8f9fa; padding: 1.5rem; border-radius: 8px; border-left: 4px solid #f39c12;">
    <h4 style="margin: 0 0 1rem 0; color: #f39c12;">
      <i class="fas fa-code"></i> Scripting
    </h4>
    <p style="margin: 0; color: #555;">Python, JavaScript, Bash</p>
  </div>
  
  <div style="background: #f8f9fa; padding: 1.5rem; border-radius: 8px; border-left: 4px solid #9b59b6;">
    <h4 style="margin: 0 0 1rem 0; color: #9b59b6;">
      <i class="fas fa-book"></i> Standards
    </h4>
    <p style="margin: 0; color: #555;">OWASP Top 10, MITRE ATT&CK, CVE</p>
  </div>
  
  <div style="background: #f8f9fa; padding: 1.5rem; border-radius: 8px; border-left: 4px solid #e67e22;">
    <h4 style="margin: 0 0 1rem 0; color: #e67e22;">
      <i class="fas fa-crosshairs"></i> Attack Vectors
    </h4>
    <p style="margin: 0; color: #555;">SQLi, XSS, SSRF, RCE, IDOR, File Inclusion, Auth Bypass, XXE, Command Injection, API Misconfig, BOLA, CSRF, Subdomain Takeover</p>
  </div>
</div>

### Professional Experience

#### Information Security Engineer
**Harrier Information Systems PVT LTD** | *Jun 2024 – Present* | *Notice Period: 30 days*

- Performed black-box and gray-box Vulnerability Assessment and Penetration Testing (VAPT) across enterprise-grade web applications, focusing on OWASP Top 10, API security flaws, and business logic vulnerabilities
- Discovered critical issues such as SQLi, RCE, SSRF, IDOR, Broken Authentications and Access control and API misconfigurations; delivered detailed technical reports with PoCs and remediation steps
- **BNHS IR: Broken Auth to RCE Exploitation Chain**: Led end-to-end incident response and conducted post-exploitation VAPT on Laravel, WordPress, and CodeIgniter applications; analyzed and reversed obfuscated PHP backdoors, removed SEO spam injections, and reinforced server entry vectors against RCE and web shell (Backdoor)

#### Cyber Security Engineer
**GBJ Buzz | Virtually Testing Foundation** | *Jun 2023 – Jun 2024*

- Developed offensive security tools and PoCs in Python for buffer overflows, bind shells, SSH brute forcing, keyloggers, and hash cracking
- Simulated red team attacks including Kerberoasting, AS-REP Roasting, and Pass-the-Hash; used BloodHound and CrackMapExec for internal network recon and privilege escalation
- Created custom Burp Suite extension for detecting shell access patterns; automated exploit chains during black-box assessments

### Education

#### Bachelor of Engineering in Computer Science (Cyber Security)
**Shri Ramdeobaba College of Engineering and Management (RCOEM)** | *2024*
- **CGPA:** 7.6 / 10.0
- **Coursework:** Network Security, Operating Systems, Cryptography, Ethical Hacking, Web Application Security, Bug Bounty Hunting

### Courses and Certifications

- **Bug Bounty Hunter** - Hack The Box Academy (2025)
- **Practical Ethical Hacking – The Complete Course** - TCM Security (2024)  
- **Intro to Bug Bounty Hunting and Web Application Hacking** - NahamSec (2025)

---

*Last updated: {{ site.time | date: "%B %Y" }}*

</div>
