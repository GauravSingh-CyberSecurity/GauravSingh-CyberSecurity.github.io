# Placeholder Profile Image

This directory should contain your profile image named `profile.jpg` for the hero section.

**Recommended specifications:**
- Format: JPG or PNG
- Size: 400x400px (square aspect ratio)
- File size: < 500KB for optimal loading
- Professional headshot or avatar

**Alternative naming:**
If you use a different filename, update the reference in `index.md`:
```markdown
<img src="{{ '/images/your-image-name.jpg' | prepend: site.baseurl }}" alt="{{ site.author.name }}" class="hero-image">
```

**Image optimization tips:**
- Use tools like TinyPNG or ImageOptim to compress images
- Consider using WebP format for better compression
- Add appropriate alt text for accessibility
