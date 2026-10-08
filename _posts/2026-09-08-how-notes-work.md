---
title: How notes work
description: A throwaway post to confirm the build works. Delete it once you've posted a real one.
---

This is a test post. Delete the file once you've confirmed the notes page
works and you've written a real one.

## Adding a note

Create a file in `_posts/` named `YYYY-MM-DD-some-slug.md`. The date and the
slug both matter: the date orders the list, and the slug becomes the URL. This
file is `2026-09-08-how-notes-work.md`, so it lives at `/notes/how-notes-work/`.

The front matter at the top only needs a title:

    ---
    title: How notes work
    ---

Add a `description:` line too if you want control over the blurb that shows up
when you paste the link into Slack or iMessage. Without one it falls back to the
site description.

Then commit and push. GitHub builds it. There's no local build step.

## What Markdown gives you

Regular paragraphs, **bold**, *italic*, and [links](/) work as you'd expect.

- Bulleted lists
- Are fine
- As are numbered ones

> Blockquotes are styled, which is handy for quoting a script or a piece of
> direction you got.

Inline `code` and fenced blocks render too, though you probably won't need them
much on this particular site.

## The one gotcha

Because GitHub builds the site now, a broken post can fail the whole build, and
the site keeps serving the last good version until it's fixed. If a push doesn't
show up, check the **Actions** tab in the repo — the error will be there, and it's
almost always a typo in the front matter.
