# Race photos

Drop photos straight into this folder — the gallery at `/races/gallery/` picks
them up automatically at build time. No YAML to edit.

## Naming

Name files `YYYY-MM-DD-some-race-name.jpg` and the page derives both the date
and the caption from the filename:

    2025-10-26-clark-city-marathon.jpg   ->   Clark city marathon
                                              26 Oct 2025

Anything that doesn't start with a date still shows up — it just falls back to
the filename as its caption, and sorts by filename alongside everything else
(so an undated file will usually land above the dated ones). Prefixing the date
is what keeps the order sensible.

Supported: .jpg  .jpeg  .png  .webp  .avif  .gif

## Captions

To override a derived caption, add an entry to `_data/gallery.yml` keyed by the
exact filename:

    "2025-10-26-clark-city-marathon.jpg": "Final 2km at Clark — first sub-2:20 half"

## A note on file size

These ship as-is to every visitor; nothing resizes them. Straight-off-a-phone
photos are often 4–8 MB each, which makes the page slow. Aim for roughly
1600px on the long edge and under ~400 KB per image. On macOS:

    sips -Z 1600 *.jpg
