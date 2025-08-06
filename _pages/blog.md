---
layout: page
title: Blog
permalink: /blog/
---

# Security Research & Technical Articles

Welcome to my cybersecurity blog where I share technical insights, research findings, and practical tutorials on various aspects of information security.

<div class="grid grid-2" style="margin-top: 2rem;">

{% for post in site.posts %}
<article class="card">
  <h3 class="card-title">
    <a href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a>
  </h3>
  <div class="card-meta">
    {{ post.date | date: "%B %d, %Y" }}
    {% if post.categories.size > 0 %}
      • {{ post.categories | join: ', ' }}
    {% endif %}
  </div>
  <div class="card-excerpt">
    {{ post.excerpt | strip_html | truncatewords: 30 }}
  </div>
  <a href="{{ post.url | prepend: site.baseurl }}" class="card-link">Read More →</a>
</article>
{% endfor %}

</div>

## Blog Categories

### 🛠️ Tools & Development
Articles about building custom security tools, automation frameworks, and development best practices.

### 🔍 Vulnerability Research
Deep dives into specific vulnerabilities, exploitation techniques, and security research methodologies.

### 📚 Tutorials & How-To
Step-by-step guides for security testing, tool usage, and practical cybersecurity skills.

### 🏢 Enterprise Security
Insights on enterprise security strategies, compliance, and large-scale security implementations.

### 📊 Industry Analysis
Analysis of security trends, threat landscape evolution, and industry developments.

## Featured Series

### VAPT Automation Series
A comprehensive series on building automated vulnerability assessment and penetration testing frameworks.

### Modern Web Security
Exploring contemporary web application security challenges and solutions.

### Cloud Security Essentials
Practical guidance for securing cloud infrastructure and applications.

---

*Subscribe to stay updated with the latest posts and security insights. You can follow me on [Twitter](https://twitter.com/{{ site.twitter_username }}) or connect on [LinkedIn](https://linkedin.com/in/{{ site.linkedin_username }}) for real-time updates.*
