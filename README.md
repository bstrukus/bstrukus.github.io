# benstrukus.com

A hand-written artist site. No framework, no dependencies, no monthly bill.
The homepage is one HTML file; Markdown notes are built by GitHub.

```
index.html          the homepage — plain HTML, NOT processed by Jekyll
assets/styles.css   all styling for every page
assets/             headshot, resume PDF, reels and gallery photos later
_config.yml         Jekyll settings (no theme — see below)
_layouts/           page shell + note template, used only by /notes/
_posts/             your notes, as YYYY-MM-DD-slug.md
notes/index.html    the notes listing page
CNAME               the custom domain: www.benstrukus.com
robots.txt          crawler rules
```

## Adding a note

Create `_posts/YYYY-MM-DD-some-slug.md`. The front matter needs only a title:

```markdown
---
title: What I learned about mic technique
description: Optional. Used for the link preview when you share it.
---

Write Markdown here.
```

That file lands at `benstrukus.com/notes/some-slug/` and appears at the top of
`/notes/`. Commit, push, done — the layout is applied automatically.

## Previewing locally

```bash
python -m http.server 8000
```

Then open <http://localhost:8000>. Ctrl+C to stop.

**This previews the homepage, not the notes.** The homepage is plain HTML, so
what you see locally is exactly what ships. The notes are built by Jekyll on
GitHub's servers, and rendering them locally would mean installing Ruby — which
isn't worth it for occasional posts. Preview a note's *content* in VS Code's
Markdown preview (Ctrl+Shift+V), then check the styled version on the live site
after pushing.

## Publishing

```bash
git add -A && git commit -m "Update site" && git push
```

GitHub rebuilds within a minute or two. Watch the **Actions** tab for the
green check if something seems stuck.

**One setting to verify:** in the repo's Settings → Pages, the source should be
**Deploy from a branch**, branch `main`, folder `/ (root)`. That's the default,
so it's probably already right.

---

## How Jekyll is used here (and how little)

GitHub Pages runs [Jekyll](https://jekyllrb.com) over the repo automatically.
It's on, but scoped to one job: turning `_posts/*.md` into pages under `/notes/`.

Two facts make that scoping possible, and they're worth knowing because most
Jekyll documentation buries them:

**1. Jekyll only processes files that begin with `---` front matter.** Every
other file is copied to the output byte-for-byte. `index.html` has no front
matter, so Jekyll treats it as a static asset — exactly like the headshot. It
cannot be altered by a template change, and it renders locally identically to
how it ships.

**2. There is no default theme.** Themes are opt-in via a `theme:` line in
`_config.yml`. This config deliberately has none, so Jekyll injects no CSS or
markup of its own. All styling comes from `assets/styles.css`, which you own.
(The Octocat look this repo shipped with originally came from a
`theme: jekyll-theme-minimal` line that used to be in that file.)

Templating is confined to `_layouts/`, and it's about a dozen lines of
[Liquid](https://shopify.github.io/liquid/) — `{{ content }}` marks where the
converted Markdown gets dropped.

### The one real cost

**A broken build fails the whole site, not just the notes.** Because GitHub now
runs a build on every push, a YAML typo in a post's front matter can stop the
deploy, and the live site keeps serving the last good version until it's fixed.

That's loud and recoverable, not silent: check the repo's **Actions** tab, where
the error will name the file and line. But it's the tradeoff that came with
Markdown notes, and it's worth knowing before you're confused about why a change
didn't appear.

---

## The contact form

GitHub Pages serves static files only. There's no server, no PHP, no place for
a form to POST to — so an HTML form on its own genuinely cannot send you email.
You need a third-party service to receive the submission and forward it.

The form is pre-wired for **[Formspree](https://formspree.io)** (free tier:
50 submissions/month, no credit card):

1. Sign up and create a new form.
2. Copy the form ID from the endpoint it gives you — the `xyzabcde` part of
   `https://formspree.io/f/xyzabcde`.
3. In `index.html`, find `YOUR_FORM_ID` and replace it.

Your email address lives in Formspree's dashboard, never in the page source, so
scrapers can't harvest it. That's the whole point.

The form also has a **honeypot**: a hidden `_gotcha` field that humans never see
and never fill in. Bots fill in every field they find. Formspree silently drops
any submission where that field has a value. It's not perfect, but it kills the
overwhelming majority of automated spam without making real people solve a
puzzle. Don't delete that block.

Alternatives if Formspree's limits pinch: [Web3Forms](https://web3forms.com)
(unlimited, free) or [Formspark](https://formspark.io) (one-time fee).

---

## About protecting the resume

Here's the honest version, because it's worth understanding rather than
cargo-culting a fix:

**Anything reachable by a public URL is public.** There is no way to put a file
on GitHub Pages and have it be downloadable by casting directors but not by
bots. No obfuscation, no JavaScript gate, no right-click blocker changes that —
they all still hand the file to anyone who asks. If a link works for a stranger
you want, it works for a stranger you don't.

So the real protection isn't access control. **It's controlling what's in the
file.** Your resume PDF should not contain:

- your home address
- your personal phone number
- your personal email
- your date of birth or age

None of those belong on a modern actor's resume anyway — industry practice
moved away from them a decade ago, precisely because resumes get forwarded and
posted. Use your agent's contact info, or a dedicated professional email that
forwards to your real one, or just point people at the contact form on this
site. A resume with no personal data on it is a resume you don't have to
protect.

`robots.txt` also asks search engines not to index the PDF, which keeps it out
of Google results. Respectable crawlers honor that. Scrapers ignore it
completely. Treat it as tidiness, not security.

**If you want a real gate**, the only approach that works is not publishing the
file at all: keep the PDF off the site, add a "Request resume" option to the
contact form (already in the dropdown), and email it to people who ask. That's
a real access control, and it has the side benefit of telling you who's
interested. The cost is friction, and some casting people won't bother. Your
call — the download button is there if you want the easy path, and deleting it
costs one line.

---

## Extending this later

For camera and stage work, the natural next steps are a video reel section
(embed Vimeo or YouTube — don't host video files in a git repo) and splitting
the resume into VO / Theatre / Film-TV credit tables. The `.credits` table
styling already handles multiple tables; you'd just duplicate the block.
