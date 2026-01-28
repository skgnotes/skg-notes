# skg-notes

Notes and writings by Sijo Kuruvilla George.

## Live Site

**URL**: https://notes.sijokuruvilla.in/

## Tech Stack

- **Static Site Generator**: Jekyll
- **Theme**: Minima
- **Hosting**: GitHub Pages
- **Branch**: `gh-pages`

## Repository

- **GitHub**: https://github.com/skgnotes/skg-notes
- **Account**: skgnotes

## Project Structure

```
skg-notes/
├── _config.yml          # Jekyll configuration
├── _layouts/            # HTML templates
├── index.md             # Notes listing page
├── 01-books.md          # Article: Books
├── 02-rbooks.md         # Article: Books that made me Rethink
├── ...                  # More articles (01-26)
├── 26-singapore.md      # Article: Singapore trip
├── CNAME                # Custom domain config
└── Gemfile              # Ruby dependencies
```

## Articles

| # | Permalink | Title |
|---|-----------|-------|
| 01 | /books | Books |
| 02 | /rbooks | Books that made me Rethink |
| 03 | /batch | Allow things to pile up |
| 04 | /email | Common email productivity mistakes |
| 05 | /ask | Asking for favours & Ben Franklin effect |
| 06 | /projects | Projects worth pursuing |
| 07 | /cnh | Calvin & Hobbes |
| 08 | /done | Almost done |
| 09 | /compliment | Compliment people |
| 10 | /search | Search, not sort |
| 11 | /productivity | Make decisions about productivity |
| 12 | /ignore | Ignore them both |
| 13 | /moment | Rich Dad Poor Dad moment |
| 14 | /possible | Never said it was easy. Said it was possible. |
| 15 | /slowly | Read slowly |
| 16 | /jit | Just in time information |
| 17 | /work | Parkinson Law |
| 18 | /braindump | Braindump |
| 19 | /reduce | Bring down cost of experimentation |
| 20 | /slay | Slaying hoaxes |
| 21 | /priorities | Priorities |
| 22 | /import-substitution | Rethinking import substitution |
| 23 | /boardgames | Board games |
| 24 | /signature | Story of my signature |
| 25 | /name | What does your name mean? |
| 26 | /singapore | I once travelled to Singapore on a 1 dollar ticket |

## Related Sites

| Site | Repository | Domain |
|------|------------|--------|
| Main | sijokuruvilla/skg_blog | www.sijokuruvilla.in |
| Notes (this) | skgnotes/skg-notes | notes.sijokuruvilla.in |

## Local Development

```bash
# Install dependencies
bundle install

# Run local server
bundle exec jekyll serve

# Site available at http://localhost:4000
```

## Deployment

Changes pushed to the `gh-pages` branch are automatically deployed via GitHub Pages.

```bash
git add .
git commit -m "Your message"
git push origin gh-pages
```

## Adding a New Article

### Files to Modify

| File | Action |
|------|--------|
| `27-new-article.md` | Create new article file |
| `index.md` | Add link to new article |
| `26-singapore.md` | Add "Next" navigation to link to new article |

### Step 1: Create the Article File

Create `27-new-article.md` with the following structure:

```markdown
---
layout: post
title: Your Article Title
permalink: /your-slug
---

Your article content goes here...

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="https://notes.sijokuruvilla.in/singapore" style="text-decoration: none; color: #0366d6;">← Previous: I once travelled to Singapore on a 1 dollar ticket</a>
  </div>
  <div>
    <a href="https://notes.sijokuruvilla.in/" style="text-decoration: none; color: #0366d6;">Notes Home</a>
  </div>
</nav>
```

### Step 2: Update index.md

Add the new article link at the end of `index.md`.

**IMPORTANT**: Each link must end with TWO SPACES for proper line breaks.

```markdown
[I once travelled to Singapore on a 1 dollar ticket](singapore)
[Your Article Title](your-slug)
```

Without the two trailing spaces, all links will appear on a single line.

### Step 3: Update Previous Article Navigation

Edit `26-singapore.md` to add a "Next" link in its navigation:

```html
<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="https://notes.sijokuruvilla.in/name" style="text-decoration: none; color: #0366d6;">← Previous: "What does your name mean?"</a>
  </div>
  <div>
    <a href="https://notes.sijokuruvilla.in/your-slug" style="text-decoration: none; color: #0366d6;">Next: Your Article Title →</a>
  </div>
  <div>
    <a href="https://notes.sijokuruvilla.in/" style="text-decoration: none; color: #0366d6;">Notes Home</a>
  </div>
</nav>
```

### Step 4: Commit and Deploy

```bash
cd "/Users/sijokuruvilla/Documents/All Projects/SKG Notes/skg-notes"
git add .
git commit -m "Add article: Your Article Title"
git push
```

The site will auto-deploy via GitHub Pages in ~30 seconds.

## DNS Configuration

The custom domain `notes.sijokuruvilla.in` is configured via:
- CNAME file in repository root
- DNS CNAME record pointing to `skgnotes.github.io`

## Last Updated

2026-01-28
