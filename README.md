# Exif-Renamer

撮影日時で写真・動画のファイル名を付け直す macOS アプリです。
ファイル/フォルダをドラッグ&ドロップするか、Finder の「このアプリケーションで開く」で起動すると、
`YYYY.MM.DD_HH.MM.SS.拡張子` 形式へリネームします。

> このリポジトリは**配布物（公証済み zip）の置き場**です。ソースコードは別リポジトリで管理しています。

## インストール（Homebrew）

```sh
brew install --cask EVAtiter/tap/exif-renamer
```

依存する `exiftool` / `php` は cask が自動で導入します。

撮影日時メタを持たないファイルのフォールバック（macOS 作成日時の取得）には
Xcode Command Line Tools の `GetFileInfo` を使います。未導入なら次を実行してください
（撮影日時メタがあるファイルだけなら不要です）:

```sh
xcode-select --install
```

## 対応形式

- 静止画: JPEG / JPG / PNG / GIF / HEIC / HEIF
- 動画: MOV / MP4 / M4V / AVI

## 仕組み

日時は次の優先順で決定します。

1. 撮影日時メタ（exiftool。静止画は `DateTimeOriginal`、動画は `CreationDate` 等）
2. macOS の作成日時（`GetFileInfo`）
3. ファイルの更新日時

2・3 にフォールバックした場合、静止画はその日時をメタへ書き戻します。

## ライセンス / 著作権

Copyright © 2026 EVA Titer. All rights reserved.
