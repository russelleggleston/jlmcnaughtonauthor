# jlmcnaughtonauthor.com

Source for the author site at **https://jlmcnaughtonauthor.com**.
Built with [Hugo](https://gohugo.io/) and the [PaperMod](https://github.com/adityatelange/hugo-PaperMod) theme. Hosted on GitHub Pages.

## Day-to-day editing

All content lives under `content/`:

| File / folder                         | What it controls                                        |
|---------------------------------------|---------------------------------------------------------|
| `content/_index.md`                   | Home page text (under the profile photo + buttons)      |
| `content/about.md`                    | About page                                              |
| `content/books/_index.md`             | Intro text on the Books list page                       |
| `content/books/<slug>/index.md`       | One book — front matter + description                   |
| `content/books/<slug>/cover.jpg`      | That book's cover image                                 |
| `static/profile.jpg`                  | Home-page author photo                                  |
| `hugo.toml`                           | Site title, social links, menu, theme settings          |

### Add a new book

```powershell
hugo new content books/your-book-slug/index.md
```

Then drop `cover.jpg` next to the new `index.md`, edit the front matter (title, date, summary, buy links), and set `draft: false` when ready.

### Preview locally

Install Hugo extended once (Windows):

```powershell
winget install Hugo.Hugo.Extended
```

Then from this directory:

```powershell
hugo server -D
```

Open http://localhost:1313 in a browser. The `-D` flag shows drafts.

### Publish

Commit and push to `main`:

```powershell
git add .
git commit -m "Update bio"
git push
```

The GitHub Action in `.github/workflows/deploy.yml` will build the site and deploy it to GitHub Pages. Watch progress at https://github.com/russelleggleston/jlmcnaughtonauthor/actions.

## One-time setup (already done locally; complete the remote half)

### 1. Push to GitHub

```powershell
gh repo create russelleggleston/jlmcnaughtonauthor --public --source=. --remote=origin --push
```

### 2. Enable GitHub Pages

On github.com → **Settings → Pages**:
- **Source:** GitHub Actions
- **Custom domain:** `jlmcnaughtonauthor.com`
- Check **Enforce HTTPS** (once the cert provisions; can take a few hours after DNS).

### 3. DNS records (at your domain registrar)

| Type  | Host  | Value                            |
|-------|-------|----------------------------------|
| A     | @     | 185.199.108.153                  |
| A     | @     | 185.199.109.153                  |
| A     | @     | 185.199.110.153                  |
| A     | @     | 185.199.111.153                  |
| CNAME | www   | `russelleggleston.github.io.`    |

Propagation typically takes minutes to a few hours. Check with `nslookup jlmcnaughtonauthor.com` or [dnschecker.org](https://dnschecker.org).

## Theme updates

PaperMod is included as a git submodule. To pull theme updates:

```powershell
git submodule update --remote themes/PaperMod
git add themes/PaperMod
git commit -m "Update PaperMod theme"
git push
```

## TBD before launch

- [ ] Replace `content/_index.md` placeholder tagline
- [ ] Write `content/about.md` bio
- [ ] Add author photo at `static/profile.jpg` (square, ~440x440 px recommended)
- [ ] Add a favicon at `static/favicon.ico`
- [ ] Add first real book under `content/books/` (delete `sample-book/`)
- [ ] Add any additional social icons in `hugo.toml` under `[[params.socialIcons]]` (Goodreads, Amazon author page, Bluesky, Instagram, etc.)
