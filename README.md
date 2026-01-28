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

1. Create a new markdown file (e.g., `27-new-article.md`)
2. Add front matter:
   ```yaml
   ---
   layout: post
   title: Your Article Title
   permalink: /your-permalink
   ---
   ```
3. Add navigation at the bottom:
   ```html
   <nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
     <div>
       <a href="https://notes.sijokuruvilla.in/previous-article" style="text-decoration: none; color: #0366d6;">← Previous: Previous Title</a>
     </div>
     <div>
       <a href="https://notes.sijokuruvilla.in/" style="text-decoration: none; color: #0366d6;">Notes Home</a>
     </div>
   </nav>
   ```
4. Update `index.md` to include the new article link
5. Update the previous article's "Next" navigation

## DNS Configuration

The custom domain `notes.sijokuruvilla.in` is configured via:
- CNAME file in repository root
- DNS CNAME record pointing to `skgnotes.github.io`

## Last Updated

2026-01-28
