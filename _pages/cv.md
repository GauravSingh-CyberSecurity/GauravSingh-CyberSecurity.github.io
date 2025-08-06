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

<div class="cv-container" style="margin: 2rem 0;">
  <div class="cv-header" style="background: var(--bg-color-secondary); padding: 1rem; border-radius: 8px; margin-bottom: 1rem; text-align: center;">
    <p style="margin: 0; color: var(--text-color-secondary);">
      <strong>{{ site.author.name }}</strong> • {{ site.email }} • 
      <a href="{{ site.url }}" target="_blank">{{ site.url | remove: 'https://' }}</a>
    </p>
    <div style="margin-top: 0.5rem;">
      <a href="https://github.com/{{ site.github_username }}" target="_blank" style="margin: 0 0.5rem;">
        <i class="fab fa-github"></i> {{ site.github_username }}
      </a>
      <a href="https://linkedin.com/in/{{ site.linkedin_username }}" target="_blank" style="margin: 0 0.5rem;">
        <i class="fab fa-linkedin"></i> {{ site.linkedin_username }}
      </a>
    </div>
  </div>

  <div class="pdf-embed" style="width: 100%; height: 800px; border: 1px solid var(--border-color); border-radius: 8px; overflow: hidden;">
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

  <div class="cv-actions" style="text-align: center; margin-top: 2rem;">
    <a href="{{ '/files/Gaurav_Singh_resume_2025.pdf' | prepend: site.baseurl }}" 
       class="btn btn-primary" 
       style="display: inline-block; padding: 12px 24px; background: var(--accent-color); color: white; text-decoration: none; border-radius: 6px; font-weight: 500; margin: 0 1rem;">
      <i class="fas fa-download"></i> Download PDF
    </a>
    <a href="{{ '/contact/' | prepend: site.baseurl }}" 
       class="btn btn-secondary" 
       style="display: inline-block; padding: 12px 24px; background: transparent; color: var(--accent-color); text-decoration: none; border: 2px solid var(--accent-color); border-radius: 6px; font-weight: 500; margin: 0 1rem;">
      <i class="fas fa-envelope"></i> Contact Me
    </a>
  </div>

</div>

## Professional Summary

**{{ site.author.bio }}**

### Core Competencies

<div class="skills-grid" style="display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 2rem; margin: 2rem 0;">
  {% for skill in site.author.skills %}
  <div class="skill-item" style="background: var(--bg-color-secondary); padding: 1.5rem; border-radius: 8px; border-left: 4px solid var(--accent-color);">
    <h4 style="margin: 0 0 0.5rem 0; color: var(--accent-color);">
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

<style>
.cv-container {
  max-width: 100%;
}

.pdf-embed {
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

.btn:hover {
  transform: translateY(-2px);
  transition: transform 0.2s ease;
}

.btn-primary:hover {
  background: var(--accent-color-dark, #2980b9) !important;
}

.btn-secondary:hover {
  background: var(--accent-color);
  color: white !important;
}

.skills-grid .skill-item:hover {
  transform: translateY(-2px);
  transition: transform 0.2s ease;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

@media (max-width: 768px) {
  .pdf-embed {
    height: 600px;
  }
  
  .btn {
    display: block !important;
    margin: 1rem 0 !important;
    text-align: center;
  }
}
</style>
