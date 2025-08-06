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

I embed a current version of my CV below. You can also [**download the PDF here**]({{ '/files/Gaurav_Singh_resume_2025.pdf' | prepend: site.baseurl }}).

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
    src="{{ '/files/Gaurav_Singh_resume_2025.pdf' | prepend: site.baseurl }}" 
    width="100%" 
    height="100%" 
    style="border: none;">
    <p>Your browser does not support PDFs. 
      <a href="{{ '/files/Gaurav_Singh_resume_2025.pdf' | prepend: site.baseurl }}">Download the PDF</a> instead.
    </p>
  </iframe>
</div>

<div style="text-align: center; margin-top: 2rem;">
  <a href="{{ '/files/Gaurav_Singh_resume_2025.pdf' | prepend: site.baseurl }}" 
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

### Core Competencies

<div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 2rem; margin: 2rem 0;">
  {% for skill in site.author.skills %}
  <div style="background: #f8f9fa; padding: 1.5rem; border-radius: 8px; border-left: 4px solid #2c3e50;">
    <h4 style="margin: 0 0 0.5rem 0; color: #2c3e50;">
      <i class="fas fa-shield-alt"></i> {{ skill }}
    </h4>
  </div>
  {% endfor %}
</div>

### Professional Experience Highlights

- **15+ years** of experience in cybersecurity and VAPT
- **Security Assessment**: Led comprehensive security assessments for enterprise applications
- **Compliance**: Extensive experience with ISO 27001, PCI DSS, and other security frameworks
- **Research**: Active security researcher with focus on web application vulnerabilities
- **Tool Development**: Created automated security testing frameworks and tools

### Certifications & Training

- Security Assessment methodologies (OWASP, NIST)
- Vulnerability Assessment & Penetration Testing
- Incident Response & Digital Forensics
- Risk Assessment & Compliance Auditing

---

*Last updated: {{ site.time | date: "%B %Y" }}*

</div>
