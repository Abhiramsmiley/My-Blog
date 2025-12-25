# Hexo Blog Codebase Map

## Project Structure Overview

```
my-blog/
├── _config.yml                    # Main Hexo config
├── source/                        # Your content (Markdown files)
│   ├── _posts/                    # Blog posts
│   ├── about/                     # About page
│   ├── contact/                   # Contact page
│   └── tags/                      # Tags index page
├── themes/hexploit/               # Theme files
│   ├── _config.yml                # Theme config (menu, sidebar)
│   ├── layout/                    # EJS templates
│   │   ├── index.ejs              # Home page
│   │   ├── post.ejs               # Blog post page
│   │   ├── tags.ejs               # Tags list page
│   │   ├── tag.ejs                # Individual tag archive
│   │   ├── archive.ejs            # Archives page
│   │   ├── about.ejs              # About page
│   │   ├── contact.ejs            # Contact page
│   │   ├── categories.ejs         # Categories page
│   │   └── _partial/              # Reusable components
│   │       ├── header.ejs         # Navigation header
│   │       ├── footer.ejs         # Site footer
│   │       └── sidebar.ejs        # Sidebar widget
│   └── source/                    # Theme assets
│       ├── css/                   # Stylesheets
│       │   ├── hacker.css         # Main custom styles
│       │   ├── tailwind.css       # Tailwind utilities
│       │   └── ...
│       ├── js/                    # JavaScript files
│       │   ├── matrix.js          # Matrix animation
│       │   ├── search.js          # Search functionality
│       │   └── floating-words.js  # Floating words effect
│       └── img/                   # Theme images
└── public/                        # Generated output (don't edit)
```

---

## 1. File Edit Guide by Task

### Creating a New Blog Post

| What | Where |
|------|-------|
| **File to create** | `source/_posts/your-post-name.md` |
| **Code type** | Markdown with YAML front-matter |
| **Command** | `npx hexo new post "Post Title"` |

**Example front-matter:**
```yaml
---
title: My Security Post
date: 2025-12-24 10:00:00
tags:
  - Red-Team
  - OSINT
categories:
  - Tutorials
description: A brief SEO description
---
```

---

### Editing an Existing Blog Post

| What | Where |
|------|-------|
| **File path** | `source/_posts/[post-slug].md` |
| **Existing posts** | `source/_posts/cybersecurity-101.md`, `python-for-hackers.md`, etc. |

---

### Adding Images Inside a Post

| What | Where |
|------|-------|
| **Image files** | `source/images/` (create this folder) OR `themes/hexploit/source/img/` |
| **Reference in Markdown** | `![Alt text](/images/screenshot.png)` |

**Best practice:** Create `source/images/` for post-specific images. They get copied to `public/images/` on generate.

---

### Changing Post Metadata

| Field | Location | Effect |
|-------|----------|--------|
| `title` | Post front-matter | Page title, card title |
| `date` | Post front-matter | Display date, archive sorting |
| `tags` | Post front-matter | Tag links, tag pages |
| `categories` | Post front-matter | Category grouping |
| `description` | Post front-matter | SEO meta, search.json |

---

### Adding New Tags

| What | Where |
|------|-------|
| **Action** | Just add to post front-matter |
| **No config needed** | Tags are auto-generated from posts |

```yaml
tags:
  - New-Tag-Name
```

---

### Controlling search.json

| What | Where |
|------|-------|
| **Generator config** | `_config.yml` (root) |
| **Content source** | All posts in `source/_posts/` |
| **Fields indexed** | `title`, `content`, `tags`, `path` |

```yaml
# In root _config.yml
search:
  path: search.json
  field: post
  content: true
```

---

### Editing Page Layouts

| Page | Template File | Code Type |
|------|---------------|-----------|
| **Home/Index** | `themes/hexploit/layout/index.ejs` | EJS + HTML |
| **Blog Post** | `themes/hexploit/layout/post.ejs` | EJS + HTML |
| **Tags List** | `themes/hexploit/layout/tags.ejs` | EJS + HTML |
| **Tag Archive** | `themes/hexploit/layout/tag.ejs` | EJS + HTML |
| **Archives** | `themes/hexploit/layout/archive.ejs` | EJS + HTML |
| **About** | `themes/hexploit/layout/about.ejs` | EJS + HTML |
| **Contact** | `themes/hexploit/layout/contact.ejs` | EJS + HTML |

---

### Editing Header/Navbar

| What | Where |
|------|-------|
| **Template** | `themes/hexploit/layout/_partial/header.ejs` |
| **Menu items** | `themes/hexploit/_config.yml` → `menu:` |
| **Styles** | `themes/hexploit/source/css/hacker.css` |

**Menu config:**
```yaml
menu:
  - name: Home
    url: /
  - name: Tags
    url: /tags
```

---

### Editing Footer

| What | Where |
|------|-------|
| **Template** | `themes/hexploit/layout/_partial/footer.ejs` |
| **Styles** | `themes/hexploit/source/css/hacker.css` (search: `.cyber-footer`) |

---

### Editing Global Styles (CSS)

| What | Where |
|------|-------|
| **Main custom styles** | `themes/hexploit/source/css/hacker.css` |
| **Tailwind utilities** | `themes/hexploit/source/css/tailwind.css` |
| **Code highlighting** | `themes/hexploit/source/css/highlight.css` |
| **Search dropdown** | `themes/hexploit/source/css/search.css` |
| **Table of contents** | `themes/hexploit/source/css/toc.css` |

**Key sections in `hacker.css`:**
- `.cyber-footer` - Footer styling
- `.contact-terminal` - Contact page
- `.info-widget` - Security widgets
- `.glass-card` - Blog cards
- `.tag-bubble` - Tag bubbles
- `.hero-section` - Home hero

---

### Editing Animations (JS)

| Animation | File |
|-----------|------|
| **Matrix rain** | `themes/hexploit/source/js/matrix.js` |
| **Floating words** | `themes/hexploit/source/js/floating-words.js` |
| **Search** | `themes/hexploit/source/js/search.js` |
| **Scroll effects** | `themes/hexploit/source/js/scroll.js` |
| **Table of contents** | `themes/hexploit/source/js/toc.js` |

---

## 2. What NOT to Touch

| Folder/File | Why |
|-------------|-----|
| `public/` | Auto-generated, overwritten on `hexo generate` |
| `db.json` | Hexo cache database |
| `node_modules/` | Dependencies |
| `themes/hexploit/source/css/tailwind.css` | Pre-compiled, edit `hacker.css` instead |

---

## 3. Content Workflow: New Blog Post

### Step 1: Create the post
```bash
cd /Users/abhiram.ss/my-blog
npx hexo new post "JWT Security Vulnerabilities"
```
Creates: `source/_posts/JWT-Security-Vulnerabilities.md`

### Step 2: Add front-matter
```yaml
---
title: JWT Security Vulnerabilities
date: 2025-12-24 14:00:00
tags:
  - Red-Team
  - Web-Security
  - Authentication
categories:
  - Tutorials
description: Common JWT vulnerabilities and how to exploit them
---
```

### Step 3: Add images
1. Create folder: `source/images/jwt-post/`
2. Add images there
3. Reference in post: `![JWT Structure](/images/jwt-post/structure.png)`

### Step 4: Write content
Use standard Markdown:
```markdown
## Introduction
JWT (JSON Web Tokens) are commonly used...

## Vulnerability 1: Algorithm Confusion
```

### Step 5: Generate and preview
```bash
npx hexo generate
npx hexo server
```

### Step 6: Verify
- Post appears on home page ✓
- Tags link to tag pages ✓
- Shows in search ✓
- SEO description in HTML `<meta>` ✓

---

## 4. Search System

### How search.json is generated

| Source | Config |
|--------|--------|
| **Generator plugin** | `hexo-generator-search` |
| **Config location** | Root `_config.yml` |
| **Output** | `public/search.json` |

### Front-matter fields that affect search

| Field | Indexed? |
|-------|----------|
| `title` | ✅ Yes |
| `content` | ✅ Yes (post body) |
| `tags` | ✅ Yes |
| `categories` | ✅ Yes |
| `description` | ❌ Not directly (but in content) |

### Search flow
1. `hexo generate` creates `search.json` with all posts
2. `search.js` fetches and parses it
3. User types → JS filters matches → displays results

---

## 5. Tag System

### How tags are created
- **Source:** Post front-matter
- **No manual config:** Tags auto-generate from posts

```yaml
# In any post
tags:
  - OSINT
  - Red-Team
```

### How tag pages are rendered

| Page Type | Template | URL |
|-----------|----------|-----|
| **All tags list** | `layout/tags.ejs` | `/tags/` |
| **Single tag archive** | `layout/tag.ejs` | `/tags/Red-Team/` |

### Template responsibilities

**`tags.ejs`** - Shows all tags as bubbles:
```ejs
<% site.tags.each(function(tag) { %>
  <a href="<%- url_for(tag.path) %>" class="tag-bubble">
    <%= tag.name %> (<%= tag.length %>)
  </a>
<% }) %>
```

**`tag.ejs`** - Shows posts for one tag:
```ejs
<h1><%= page.tag %></h1>
<% page.posts.forEach(function(post) { %>
  <!-- Blog card -->
<% }) %>
```

### Tag styling
- **CSS location:** `hacker.css` → `.tag-bubble`
- **Colors:** Green cyber theme (#2bbc8a)

---

## 6. Quick Reference Card

| Task | Primary File |
|------|--------------|
| New post | `source/_posts/new-post.md` |
| Edit home page | `themes/hexploit/layout/index.ejs` |
| Edit post layout | `themes/hexploit/layout/post.ejs` |
| Edit navbar | `themes/hexploit/layout/_partial/header.ejs` |
| Edit footer | `themes/hexploit/layout/_partial/footer.ejs` |
| Edit menu links | `themes/hexploit/_config.yml` |
| Edit CSS | `themes/hexploit/source/css/hacker.css` |
| Edit animations | `themes/hexploit/source/js/*.js` |
| Site title/author | Root `_config.yml` |

---

## 7. Commands Cheatsheet

```bash
# Create new post
npx hexo new post "Title"

# Generate static files
npx hexo generate

# Start dev server
npx hexo server

# Clean cache (if issues)
npx hexo clean

# Full rebuild
npx hexo clean && npx hexo generate
```
