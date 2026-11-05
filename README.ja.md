[English](README.md) | [日本語](README.ja.md)

# Exif-Renamer

撮影日時で写真・動画のファイル名を付け直す macOS アプリです。
ファイル/フォルダをドラッグ&ドロップするか、Finder の「このアプリケーションで開く」で起動すると、
`YYYY.MM.DD_HH.MM.SS.拡張子` 形式へリネームします。

## インストール（Homebrew）

```sh
brew install --cask EVAtiter/tap/exif-renamer
```

依存する `exiftool` / `php` は cask が自動で導入します。

> Homebrew が信頼していない tap として読み込みを拒否する場合は、
> 先に `brew trust --cask EVAtiter/tap/exif-renamer` を実行してください。

撮影日時メタを持たないファイルのフォールバック（macOS 作成日時の取得）には
Xcode Command Line Tools の `GetFileInfo` を使います。未導入なら次を実行してください
（撮影日時メタがあるファイルだけなら不要です）:

```sh
xcode-select --install
```

## ターミナルから使う（v1.3.0 から）

Homebrew でインストールすると、`exif-renamer` コマンドも PATH に置かれます。
ウインドウを開かず、進捗をそのまま標準出力に出します（スクリプト・パイプ向け）。

```sh
exif-renamer <file_or_directory> [...]
```

リネームの処理はアプリと同じです。

## 対応形式

- 静止画: JPEG / JPG / PNG / GIF / HEIC / HEIF / WEBP
- 動画: MOV / MP4 / M4V / AVI

## 仕組み

日時は次の優先順で決定します。

1. 撮影日時メタ（exiftool。静止画は `DateTimeOriginal`、動画は `CreationDate` 等）
2. macOS の作成日時（`GetFileInfo`）
3. ファイルの更新日時

2・3 にフォールバックした場合、静止画はその日時をメタへ書き戻します。

## 動作環境

- macOS 13 Ventura 以降
- Apple Silicon（arm64）専用
- Apple 公証済み（Notarized by Apple）

## ライセンス / 著作権

Copyright © 2026 EVA Titer. All rights reserved.
