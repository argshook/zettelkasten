---
title: About
date-modified: 2024-09-03
---

Hello and welcome to my digital garden.

This page is an unordered archive of notes, updated at random times.

All notes are markdown files and their source can be found on [github](https://github.com/argshook/zettelkasten). I'm happy to accept PRs with additions or fixes!

---

I enjoy taking notes. Over time I ironed out the note taking process pretty well, to the point where it is very simple and straighforward.

Wanted to share some of them, but there were problems:

- figure out what to share
- keep private and public notes separately
- actions of publishing always felt cumbersome

These few points were enough to prevent me from sharing.

What i wanted is to have ability to simply hit "save" and have the note published. No other actions at all, hit save and be done while notes automatically become available online.

Turns out just saving is a bit too often, so in the end i settled on a "publish" command. [Here's the source of it](https://github.com/argshook/dotfiles/blob/main/.argsdotfiles/vim/vim-zettel-public.lua)

After running `:Publish` in my editor, the note is formatted, saved,
committed, and pushed to a public Github repository, where a Github action notifies another (private) repository to run the build and deploy the note to the web.

For me it's instantaneous (just `:Publish` and `enter`) and the whole
build cycle takes about a minute. It takes longer for the cache to
update and the note to be available online. That's the CI/CD i always
dreamt of!

This is that page. A random collection of personal notes with links between them. It's not a blog, there are no posts or a timeline.

Notes are not well edited, sometimes unformatted or completely unfinished.

[Content is open sourced on github](https://github.com/argshook/zettelkasten)
