[English](README.md) | [日本語](README.ja.md)

# Exif-Renamer

A macOS app that renames photos and videos by their capture date.
Drag and drop files or folders onto it, or open them with it from the Finder's "Open With",
and it renames them to the `YYYY.MM.DD_HH.MM.SS.ext` format.

## Installation (Homebrew)

```sh
brew install --cask EVAtiter/tap/exif-renamer
```

The cask installs the `exiftool` and `php` it depends on automatically.

> If Homebrew refuses to load the tap because it is not trusted,
> run `brew trust --cask EVAtiter/tap/exif-renamer` first.

For files without capture-date metadata, the fallback (reading the macOS creation date) uses `GetFileInfo` from the
Xcode Command Line Tools. If they are not installed, run the following
(not needed if all your files have capture-date metadata):

```sh
xcode-select --install
```

## Using it from the Terminal (since v1.3.0)

Installing with Homebrew also puts the `exif-renamer` command on your PATH.
It opens no window and writes its progress straight to standard output (for scripts and pipes).

```sh
exif-renamer <file_or_directory> [...]
```

It renames files exactly the same way as the app.

## Supported formats

- Images: JPEG / JPG / PNG / GIF / HEIC / HEIF / WEBP
- Videos: MOV / MP4 / M4V / AVI

## How it works

The date is chosen in this order:

1. Capture-date metadata (exiftool; `DateTimeOriginal` for images, `CreationDate` and others for videos)
2. The macOS creation date (`GetFileInfo`)
3. The file's modification date

When it falls back to 2 or 3, it writes that date back into the metadata of images.

## Requirements

- macOS 13 Ventura or later
- Apple Silicon (arm64) only
- Notarized by Apple

## License / Copyright

Copyright © 2026 EVA Titer. All rights reserved.
