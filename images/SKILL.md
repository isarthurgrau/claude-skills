---
name: images
description: Decode, convert, inspect, and extract text from image files (HEIC, PNG, JPG, WebP, TIFF, SVG). Use when the user asks to read, convert, resize, OCR, or get info about an image, or when a file won't open because of its format.
---

# Images

Claude reads PNG, JPG, GIF, and WebP natively with the Read tool — just Read the file and describe or extract what's needed. This skill covers everything the Read tool can't do alone.

## Inspect metadata

```bash
sips -g all photo.jpg            # dimensions, color space, DPI, EXIF basics (built into macOS)
mdls photo.heic                  # Spotlight metadata: GPS, capture date, camera
```

## Convert formats

`sips` ships with macOS — no install needed. Use it first.

```bash
sips -s format png photo.heic --out photo.png      # HEIC → PNG (Read can't open HEIC directly)
sips -s format jpeg image.tiff --out image.jpg     # TIFF → JPEG
sips -Z 1200 big.png --out small.png               # resize to max dimension 1200px, keep aspect
```

For formats sips can't handle (AVIF, some WebP encodes, SVG rasterization), check for ImageMagick (`magick input.avif out.png`) — suggest `brew install imagemagick` if missing, but don't install it unprompted.

Converted copies of a user's image go in the scratchpad directory unless the user wants the file kept.

## OCR (text extraction)

1. First try just Reading the image — Claude transcribes text in images directly, including handwriting. This is usually all you need.
2. For bulk/scriptable OCR, check for tesseract: `tesseract scan.png out.txt`. Suggest `brew install tesseract` if missing.

## PDFs pretending to be images

A scanned PDF is a stack of images. Use the pdf skill for splitting; for a single page, `sips` won't help — render with `qlmanage -t -s 1600 -o . file.pdf` (page 1 thumbnail) or ask about installing poppler (`pdftoppm`).

## Notes

- Never bulk-read a directory of images (see the user's mind skill: grep the index instead).
- HEIC is the iPhone default — expect it whenever the user says "a photo from my phone."
