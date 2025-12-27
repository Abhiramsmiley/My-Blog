# 0xAbhiram Blog - Complete Project Manual

> **Version:** 1.0  
> **Last Updated:** December 27, 2025  
> **Framework:** Hexo v8.1.1  
> **Theme:** Hexploit (Custom Hacker Theme)

---

## Table of Contents

1. [Project Overview](#1-project-overview)
2. [Folder Structure](#2-folder-structure)
3. [Configuration Files](#3-configuration-files)
4. [Theme Structure](#4-theme-structure)
5. [Layout Templates](#5-layout-templates)
6. [CSS Files](#6-css-files)
7. [JavaScript Files](#7-javascript-files)
8. [Assets (Images, Fonts, Cursors)](#8-assets)
9. [Blog Posts](#9-blog-posts)
10. [Common Tasks](#10-common-tasks)
11. [Customization Guide](#11-customization-guide)
12. [Deployment](#12-deployment)
13. [Troubleshooting](#13-troubleshooting)

---

## 1. Project Overview

This is a **Hexo-based static blog** with a custom cybersecurity/hacker theme called "Hexploit". 

### Key Features:
- 🎬 **Boot Animation** - Cinematic loading screen (plays once per session)
- 🌐 **Matrix Rain Background** - Animated falling code effect
- 📱 **Responsive Design** - Works on desktop and mobile
- 🔍 **Search Functionality** - Client-side post search
- 📑 **Table of Contents** - Auto-generated for long posts
- 🎨 **Operation Brief Cards** - Military-style blog post cards
- 🖥️ **Terminal Aesthetic** - DOS font, green accents, hacker UI

### Tech Stack:
- **Static Site Generator:** Hexo 8.1.1
- **Template Engine:** EJS
- **CSS Framework:** Tailwind CSS + Custom CSS
- **Font:** Perfect DOS VGA 437
- **Hosting:** Netlify/Vercel

---

## 2. Folder Structure

```
my-blog-prod/
│
├── _config.yml              # Main Hexo configuration
├── package.json             # Node.js dependencies
├── db.json                  # Hexo database (auto-generated)
│
├── source/                  # YOUR CONTENT (Blog posts, pages)
│   ├── _posts/              # Blog posts (Markdown files)
│   ├── about/               # About page
│   ├── contact/             # Contact page
│   └── tags/                # Tags page
│
├── themes/                  # Theme files
│   └── hexploit/            # Custom hacker theme
│       ├── _config.yml      # Theme configuration
│       ├── layout/          # EJS templates
│       └── source/          # Theme assets (CSS, JS, images)
│
├── public/                  # Generated site (DO NOT EDIT)
│                            # This is rebuilt on every `hexo generate`
│
└── scaffolds/               # Templates for new posts
    ├── post.md              # Default post template
    ├── page.md              # Default page template
    └── draft.md             # Default draft template
```

---

## 3. Configuration Files

### 3.1 Main Config: `/_config.yml`

This is the **main Hexo configuration** file.

| Setting | Current Value | Purpose |
|---------|---------------|---------|
| `title` | `0xAbhiram` | Site title (shown in header) |
| `subtitle` | `Security Engineer Journal` | Tagline (shown in hero) |
| `author` | `Abhiram SS` | Author name |
| `url` | `https://0xabhiram-blogs.netlify.app` | Production URL |
| `permalink` | `:title/` | URL structure for posts |
| `theme` | `hexploit` | Active theme name |

**To change site title:**
```yaml
title: Your New Title
subtitle: 'Your New Tagline'
```

### 3.2 Theme Config: `/themes/hexploit/_config.yml`

Controls **navigation menu, sidebar widgets, and theme features**.

```yaml
menu:                        # Navigation menu items
  - name: Home
    url: /
  - name: About
    url: /about/
  - name: Tags
    url: /tags/
  - name: Contact
    url: /contact/

sidebar:
  enable: true
  widgets:                   # Sidebar widgets (desktop)
    - search
    - notice
    - categories
    - tags
    - links
  
  links: []                  # Social links (add GitHub, Twitter, etc.)

toc:
  enable: true               # Table of contents in posts
```

**To add a new menu item:**
```yaml
menu:
  - name: Blog
    url: /archives/
```

**To add social links:**
```yaml
sidebar:
  links:
    - name: GitHub
      url: https://github.com/yourusername
    - name: Twitter
      url: https://twitter.com/yourusername
```

---

## 4. Theme Structure

```
themes/hexploit/
│
├── _config.yml              # Theme settings
├── package.json             # Theme dependencies
├── tailwind.config.js       # Tailwind CSS config
│
├── layout/                  # EJS Templates
│   ├── index.ejs            # Homepage
│   ├── post.ejs             # Single blog post
│   ├── about.ejs            # About page
│   ├── contact.ejs          # Contact page
│   ├── tags.ejs             # All tags page
│   ├── tag.ejs              # Single tag page
│   ├── archive.ejs          # Archives page
│   ├── categories.ejs       # Categories page
│   │
│   └── _partial/            # Reusable components
│       ├── header.ejs       # Site header + mobile menu
│       ├── footer.ejs       # Site footer
│       ├── sidebar.ejs      # Desktop sidebar
│       ├── boot-screen.ejs  # Boot animation
│       └── operation-card.ejs # Blog post card
│
└── source/                  # Static assets
    ├── css/                 # Stylesheets
    ├── js/                  # JavaScript files
    ├── img/                 # Images
    ├── font/                # Fonts
    └── cursor/              # Custom cursors
```

---

## 5. Layout Templates

### 5.1 `index.ejs` - Homepage

**Location:** `/themes/hexploit/layout/index.ejs`

**What it contains:**
- Boot animation include
- Hero section with title and animated tagline
- Blog post grid (Operation Brief cards)
- Sidebar

**Key sections to modify:**
```ejs
<!-- Hero title comes from _config.yml subtitle -->
<h1><%= config.subtitle %></h1>

<!-- Animated tagline (hardcoded in JS) -->
<h2 id="animated-tagline"></h2>
```

### 5.2 `post.ejs` - Blog Post Page

**Location:** `/themes/hexploit/layout/post.ejs`

**What it contains:**
- Post header (title, date, categories, tags)
- Post content (Markdown rendered to HTML)
- Table of contents (sidebar)
- Share buttons

### 5.3 `_partial/header.ejs` - Site Header

**Location:** `/themes/hexploit/layout/_partial/header.ejs`

**What it controls:**
- Desktop navigation
- Mobile hamburger menu
- Search button
- Logo/site title link

**To change menu icons (mobile):**
```ejs
<% var menuIcons = { 
  'Home': 'fa-terminal', 
  'About': 'fa-user-secret', 
  'Tags': 'fa-tags', 
  'Contact': 'fa-envelope'
}; %>
```

### 5.4 `_partial/boot-screen.ejs` - Boot Animation

**Location:** `/themes/hexploit/layout/_partial/boot-screen.ejs`

**Features:**
- Plays only once per browser session (uses sessionStorage)
- Central orb with pulse rings
- Scan lines (horizontal, vertical, diagonal)
- Energy sweeps from edges
- "Welcome to 0xAbhiram Blogs" text

**To change boot text:**
```html
<div class="boot-text-main">Welcome to</div>
<div class="boot-text-sub">0xAbhiram Blogs</div>
```

**To change animation duration (currently 3 seconds):**
Edit the JavaScript setTimeout values:
```javascript
// Shake at 2400ms
setTimeout(function() { bootScreen.classList.add('shake'); }, 2400);

// Fade out at 2700ms
setTimeout(function() { bootScreen.classList.add('fade-out'); }, 2700);

// Remove at 3000ms
setTimeout(function() { bootScreen.parentNode.removeChild(bootScreen); }, 3000);
```

### 5.5 `_partial/footer.ejs` - Site Footer

**Location:** `/themes/hexploit/layout/_partial/footer.ejs`

Contains copyright, social links, and decorative elements.

---

## 6. CSS Files

All CSS is in `/themes/hexploit/source/css/`

| File | Purpose | Lines |
|------|---------|-------|
| `hacker.css` | **Main custom styles** - boot animation, mobile menu, cards, etc. | ~3000+ |
| `tailwind.css` | Compiled Tailwind utilities | Auto-generated |
| `styles.css` | Base styles, typography | ~200 |
| `highlight.css` | Code syntax highlighting | ~150 |
| `search.css` | Search overlay styles | ~100 |
| `toc.css` | Table of contents styles | ~100 |

### 6.1 `hacker.css` - Main Stylesheet

**This is where most customizations happen.**

**Key sections (search for these comments):**

| Line Range | Section |
|------------|---------|
| 1-400 | Boot Screen Animation |
| 400-600 | Mobile Menu Overlay |
| 600-700 | Mobile Post Fixes |
| 700-900 | Post Header Styles |
| 2200-2500 | Mobile Menu Drawer |
| 2500-2700 | Search Button |

**Important CSS Variables/Colors:**
```css
#2bbc8a          /* Primary green (hacker color) */
#0a0a0a          /* Dark background */
#030508          /* Boot screen background */
rgba(43,188,138) /* Green with transparency */
```

---

## 7. JavaScript Files

All JS is in `/themes/hexploit/source/js/`

| File | Purpose |
|------|---------|
| `matrix.js` | Matrix rain background animation |
| `menu.js` | Mobile menu toggle logic |
| `search.js` | Search functionality |
| `scroll.js` | Scroll effects |
| `toc.js` | Table of contents functionality |
| `floating-words.js` | Floating security terms animation |

### 7.1 `matrix.js` - Matrix Rain Effect

Controls the falling green characters in the background.

**To adjust speed/density:**
```javascript
// Find these values in the file
var fontSize = 14;        // Character size
var speed = 33;           // Lower = faster (milliseconds)
var opacity = 0.15;       // Background opacity
```

### 7.2 `search.js` - Search Functionality

Provides client-side search of blog posts.

**Data source:** `/search.json` (auto-generated by Hexo)

---

## 8. Assets

### 8.1 Images: `/themes/hexploit/source/img/`

| File | Usage |
|------|-------|
| `favicon.svg` | Browser tab icon |
| `my-photo.jpeg` | Profile photo (mobile menu) |
| `profilephoto.png` | Alternative profile photo |
| `cyber-bg.jpg` | Blog post thumbnail |
| `binary.svg` | Decorative binary pattern |

**To change profile photo:**
1. Add new image to `/themes/hexploit/source/img/`
2. Edit `/themes/hexploit/layout/_partial/header.ejs`:
```html
<img src="/img/your-new-photo.jpg" alt="Profile">
```

### 8.2 Font: `/themes/hexploit/source/font/`

| File | Usage |
|------|-------|
| `Perfect DOS VGA 437.ttf` | Main terminal font |

**Font is loaded in CSS:**
```css
@font-face {
  font-family: 'Perfect DOS VGA 437';
  src: url('/font/Perfect DOS VGA 437.ttf');
}
```

### 8.3 Cursors: `/themes/hexploit/source/cursor/`

| File | Usage |
|------|-------|
| `cursor.cur` | Default cursor |
| `link.cur` | Link hover cursor |
| `text.cur` | Text selection cursor |

---

## 9. Blog Posts

### 9.1 Creating a New Post

**Command:**
```bash
npx hexo new "Your Post Title"
```

**Creates:** `/source/_posts/Your-Post-Title.md`

### 9.2 Post Front Matter

Every post starts with YAML front matter:

```yaml
---
title: Your Post Title
date: 2025-12-27 10:00:00
tags:
  - Security
  - Tutorial
categories:
  - Security-Engineering
author: 0xAbhiram
risk: HIGH                    # For Operation Brief cards
summary: Brief description    # Card summary
vectors:                      # Attack vectors (optional)
  - Phishing
  - Malware
thumbnail: /img/cyber-bg.jpg  # Card thumbnail
---

Your post content here in Markdown...
```

### 9.3 Post Locations

| Type | Location |
|------|----------|
| Published posts | `/source/_posts/` |
| Drafts | `/source/_drafts/` |
| About page | `/source/about/index.md` |
| Contact page | `/source/contact/index.md` |
| Tags page | `/source/tags/index.md` |

---

## 10. Common Tasks

### 10.1 Development Commands

```bash
# Start development server
npx hexo server
# or
npx hexo s

# Generate static files
npx hexo generate
# or
npx hexo g

# Clean generated files
npx hexo clean

# Clean + Generate + Server (recommended)
npx hexo clean && npx hexo g && npx hexo s

# Create new post
npx hexo new "Post Title"

# Create new page
npx hexo new page "page-name"

# Create draft
npx hexo new draft "Draft Title"

# Publish draft
npx hexo publish "Draft Title"
```

### 10.2 Quick Reference

| Task | File to Edit |
|------|--------------|
| Change site title | `/_config.yml` → `title` |
| Change subtitle/tagline | `/_config.yml` → `subtitle` |
| Add menu item | `/themes/hexploit/_config.yml` → `menu` |
| Change boot animation text | `/themes/hexploit/layout/_partial/boot-screen.ejs` |
| Change boot animation duration | `/themes/hexploit/layout/_partial/boot-screen.ejs` (JS) + `/themes/hexploit/source/css/hacker.css` |
| Change profile photo | `/themes/hexploit/layout/_partial/header.ejs` |
| Modify mobile menu | `/themes/hexploit/layout/_partial/header.ejs` + `hacker.css` |
| Change colors | `/themes/hexploit/source/css/hacker.css` |
| Edit footer | `/themes/hexploit/layout/_partial/footer.ejs` |

---

## 11. Customization Guide

### 11.1 Changing the Primary Color

The primary green color is `#2bbc8a`. To change it:

1. Open `/themes/hexploit/source/css/hacker.css`
2. Find and replace: `#2bbc8a` → `#your-color`
3. Also replace: `rgba(43, 188, 138` → `rgba(r, g, b`
4. Regenerate: `npx hexo clean && npx hexo g`

### 11.2 Changing the Boot Animation Duration

**Current:** 3 seconds

**To change to X seconds:**

1. Edit `/themes/hexploit/layout/_partial/boot-screen.ejs`:
```javascript
// Change these values (in milliseconds)
setTimeout(..., X * 0.8 * 1000);   // Shake
setTimeout(..., X * 0.9 * 1000);   // Fade out
setTimeout(..., X * 1000);         // Remove
```

2. Edit `/themes/hexploit/source/css/hacker.css`:
   - Search for `boot-` animations
   - Adjust duration values proportionally

### 11.3 Disabling Boot Animation

To completely disable the boot animation:

1. Edit `/themes/hexploit/layout/index.ejs`
2. Remove or comment out: `<%- partial('_partial/boot-screen') %>`

### 11.4 Adding Social Links to Mobile Menu

1. Edit `/themes/hexploit/_config.yml`:
```yaml
sidebar:
  links:
    - name: GitHub
      url: https://github.com/yourusername
    - name: LinkedIn
      url: https://linkedin.com/in/yourusername
```

2. Icons are auto-mapped in header.ejs:
```javascript
var socialIcons = { 
  'GitHub': 'fa-github', 
  'Twitter': 'fa-twitter', 
  'LinkedIn': 'fa-linkedin'
};
```

### 11.5 Changing the Hero Animated Tagline

Edit `/themes/hexploit/layout/index.ejs`, find the script section:
```javascript
var phrases = [
  "Breaking Security...",
  "Analyzing Threats...",
  "Your Custom Text..."
];
```

---

## 12. Deployment

### 12.1 Build for Production

```bash
npx hexo clean && npx hexo generate
```

The `public/` folder contains the complete static site.

### 12.2 Deploy to Netlify

1. Push to GitHub
2. Connect repo to Netlify
3. Build command: `npx hexo generate`
4. Publish directory: `public`

### 12.3 Deploy to Vercel

1. Push to GitHub
2. Import project to Vercel
3. Framework preset: Other
4. Build command: `npx hexo generate`
5. Output directory: `public`

---

## 13. Troubleshooting

### Problem: Changes not showing

**Solution:**
```bash
npx hexo clean && npx hexo generate && npx hexo server
```

### Problem: Port 4000 already in use

**Solution:**
```bash
lsof -ti:4000 | xargs kill -9
npx hexo server
```

### Problem: Boot animation plays every time

**Check:** The sessionStorage logic in `boot-screen.ejs`

**Solution:** Clear browser cache or use incognito mode to test

### Problem: Images not loading

**Check:**
1. Image exists in `/themes/hexploit/source/img/`
2. Path in code starts with `/img/`
3. Run `npx hexo clean && npx hexo g`

### Problem: Mobile menu not working

**Check:**
1. JavaScript console for errors
2. `menu.js` is loaded
3. Mobile menu elements have correct IDs

---

## Quick File Reference

| What you want to change | File |
|-------------------------|------|
| Site title & metadata | `/_config.yml` |
| Navigation menu | `/themes/hexploit/_config.yml` |
| Homepage layout | `/themes/hexploit/layout/index.ejs` |
| Blog post layout | `/themes/hexploit/layout/post.ejs` |
| Header & mobile menu | `/themes/hexploit/layout/_partial/header.ejs` |
| Footer | `/themes/hexploit/layout/_partial/footer.ejs` |
| Boot animation | `/themes/hexploit/layout/_partial/boot-screen.ejs` |
| All custom CSS | `/themes/hexploit/source/css/hacker.css` |
| Matrix background | `/themes/hexploit/source/js/matrix.js` |
| Profile photo | `/themes/hexploit/source/img/` |

---

## Contact & Support

- **Author:** Abhiram SS (0xAbhiram)
- **Framework Docs:** https://hexo.io/docs/
- **Tailwind Docs:** https://tailwindcss.com/docs

---

*This manual was generated on December 27, 2025*
