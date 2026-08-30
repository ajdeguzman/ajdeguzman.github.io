# Slide decks

PDFs for the talks listed on `/talks/`. Unlike the gallery, these aren't
auto-discovered — each one is referenced by name from `_data/talks.yml`:

    - date: 29 Jun 2023
      title: Kickstarting Career in Tech
      pdf: /assets/talks/2023-06-29-kickstarting-career-in-tech.pdf

The red PDF icon appears beside the title only when `pdf:` is set.

## Naming

Match the talk's date, then a kebab-case slug:

    YYYY-MM-DD-some-talk-title.pdf

Keep it lowercase with hyphens — no spaces or accents. The originals were
named things like `Writing Good Résumé.pdf`, which meant every link had to
carry `%20` and `%C3%A9` escapes and broke easily when edited by hand.

## A note on file size

These ship as-is; nothing compresses them. A deck over ~5 MB is a slow
download on a phone. If one is heavy, exporting at screen resolution rather
than print usually fixes it.
