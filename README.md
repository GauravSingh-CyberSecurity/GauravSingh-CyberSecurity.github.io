# Gaurav Singh - Cybersecurity Portfolio

A professional cybersecurity portfolio website showcasing my expertise in vulnerability assessment, penetration testing, and security research.

## 🚀 Live Site

Visit the live portfolio at: [https://singhggithub.github.io/cybersecurity-portfolio/](https://singhggithub.github.io/cybersecurity-portfolio/)

## 📋 Features

- **Modern Design**: Clean, professional layout inspired by industry leaders
- **Responsive**: Optimized for desktop, tablet, and mobile devices
- **Fast Loading**: Optimized assets and efficient Jekyll setup
- **SEO Friendly**: Proper meta tags and structured data
- **Blog Integration**: Technical articles and security research posts
- **Project Showcase**: Detailed project descriptions and case studies

## 🛠️ Built With

- **Jekyll**: Static site generator
- **GitHub Pages**: Hosting platform
- **Sass/SCSS**: CSS preprocessing
- **Font Awesome**: Icons
- **Google Fonts**: Typography (Inter font family)

## 📁 Structure

```
cybersecurity-portfolio/
├── _includes/          # Reusable HTML components
├── _layouts/           # Page templates
├── _pages/            # Static pages (About, Projects, etc.)
├── _posts/            # Blog posts
├── _projects/         # Project details
├── _sass/             # Sass stylesheets
├── css/               # Compiled CSS
├── js/                # JavaScript files
├── images/            # Image assets
├── files/             # Downloadable files
├── _config.yml        # Jekyll configuration
└── index.md           # Homepage
```

## 🎨 Design Features

### Color Scheme
- Primary: #2c3e50 (Dark blue-gray)
- Secondary: #3498db (Bright blue)
- Accent: #e74c3c (Red)
- Background: #ffffff (White)
- Alt Background: #f8f9fa (Light gray)

### Typography
- Primary Font: Inter (Google Fonts)
- Monospace: Fira Code
- Responsive font scaling
- Optimized line heights and spacing

### Components
- Hero section with profile image
- Card-based layouts
- Grid systems for responsive design
- Smooth animations and transitions
- Mobile-friendly navigation

## 📱 Responsive Design

The portfolio is fully responsive with breakpoints at:
- Mobile: 480px and below
- Tablet: 768px and below
- Desktop: 1024px and above
- Wide: 1200px and above

## 🔧 Local Development

### Prerequisites
- Ruby 2.7+
- Bundler gem
- Jekyll gem

### Setup
```bash
# Clone the repository
git clone https://github.com/singhggithub/cybersecurity-portfolio.git
cd cybersecurity-portfolio

# Install dependencies
bundle install

# Run locally
bundle exec jekyll serve

# View at http://localhost:4000
```

### Build for Production
```bash
bundle exec jekyll build
```

## 📝 Content Management

### Adding Blog Posts
Create new files in `_posts/` with the format:
```
YYYY-MM-DD-title-slug.md
```

Example front matter:
```yaml
---
layout: post
title: "Your Post Title"
date: 2025-01-01 10:00:00 +0530
categories: [Security, Tools]
---
```

### Adding Projects
Create new files in `_projects/` with:
```yaml
---
layout: page
title: "Project Name"
tech: ["Technology", "Stack"]
excerpt: "Brief description"
---
```

### Updating Pages
Edit files in `_pages/` directory:
- `about.md` - About page content
- `projects.md` - Projects listing
- `research.md` - Research activities
- `contact.md` - Contact information

## 🎯 SEO Optimization

- Semantic HTML structure
- Meta descriptions and titles
- Open Graph tags for social sharing
- Structured data markup
- XML sitemap generation
- Optimized images with alt text

## 🚀 Deployment

The site is automatically deployed to GitHub Pages when changes are pushed to the main branch.

### Manual Deployment
```bash
# Build the site
bundle exec jekyll build

# The _site directory contains the built site
# Deploy _site contents to your web server
```

## 📊 Performance

- **Lighthouse Score**: 95+ on all metrics
- **Page Load Time**: < 2 seconds
- **Mobile Friendly**: 100% mobile usability
- **Core Web Vitals**: All metrics in green

## 🔒 Security Features

- HTTPS enforced
- Content Security Policy headers
- No inline scripts or styles
- Sanitized user-generated content
- Regular dependency updates

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test locally
5. Submit a pull request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 📞 Contact

- **Email**: gs.cyber.red@gmail.com
- **LinkedIn**: [Connect with me](https://linkedin.com/in/your-linkedin-username)
- **GitHub**: [singhggithub](https://github.com/singhggithub)

## 🙏 Acknowledgments

- Design inspiration from Jason Haddix's portfolio
- Jekyll community for excellent documentation
- GitHub Pages for free hosting
- Font Awesome for beautiful icons
- Google Fonts for typography

---

⭐ If you found this portfolio helpful, please consider giving it a star!
