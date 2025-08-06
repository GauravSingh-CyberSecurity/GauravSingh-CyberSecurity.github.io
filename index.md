---
layout: default
class: home
---

<section class="hero">
  <div class="hero-content">
    <img src="{{ '/images/profile.jpg' | prepend: site.baseurl }}" alt="{{ site.author.name }}" class="hero-image">
    <h1 class="hero-title">{{ site.title }}</h1>
    <p class="hero-tagline">{{ site.tagline }}</p>
    <p class="hero-description">{{ site.author.bio }}</p>
    <div class="hero-buttons">
      <a href="{{ '/about/' | prepend: site.baseurl }}" class="btn btn-primary">About Me</a>
      <a href="{{ '/projects/' | prepend: site.baseurl }}" class="btn btn-secondary">View Projects</a>
    </div>
  </div>
</section>

<section class="wrapper">
  <div style="padding: 3rem 0;">
    <h2 class="text-center mb-4">Expertise & Skills</h2>
    <div class="skills-grid">
      {% for skill in site.author.skills %}
      <div class="skill-item">
        <div class="skill-icon">
          {% case skill %}
            {% when 'Vulnerability Assessment & Penetration Testing' %}
              <i class="fas fa-shield-alt"></i>
            {% when 'Security Research' %}
              <i class="fas fa-search"></i>
            {% when 'Incident Response' %}
              <i class="fas fa-ambulance"></i>
            {% when 'Compliance & Risk Assessment' %}
              <i class="fas fa-clipboard-check"></i>
            {% when 'Security Tool Development' %}
              <i class="fas fa-tools"></i>
            {% else %}
              <i class="fas fa-code"></i>
          {% endcase %}
        </div>
        <div class="skill-name">{{ skill }}</div>
      </div>
      {% endfor %}
    </div>
  </div>
</section>

<section class="wrapper">
  <div style="padding: 3rem 0;">
    <h2 class="text-center mb-4">Latest Blog Posts</h2>
    <div class="grid grid-2">
      {% for post in site.posts limit:4 %}
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
    <div class="text-center mt-4">
      <a href="{{ '/blog/' | prepend: site.baseurl }}" class="btn btn-secondary">View All Posts</a>
    </div>
  </div>
</section>

<section class="wrapper">
  <div style="padding: 3rem 0;">
    <h2 class="text-center mb-4">Featured Projects</h2>
    <div class="grid grid-2">
      {% for project in site.projects limit:4 %}
      <article class="card">
        <h3 class="card-title">
          <a href="{{ project.url | prepend: site.baseurl }}">{{ project.title }}</a>
        </h3>
        <div class="card-meta">
          {% if project.tech %}{{ project.tech | join: ', ' }}{% endif %}
        </div>
        <div class="card-excerpt">
          {{ project.excerpt | strip_html | truncatewords: 20 }}
        </div>
        <a href="{{ project.url | prepend: site.baseurl }}" class="card-link">View Project →</a>
      </article>
      {% endfor %}
    </div>
    <div class="text-center mt-4">
      <a href="{{ '/projects/' | prepend: site.baseurl }}" class="btn btn-secondary">View All Projects</a>
    </div>
  </div>
</section>
