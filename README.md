# Suno 行単位 SRT ブックマークレット

Suno の曲ページ（`/song/` または `/edit/`）から、タイミング付き歌詞 API を使って **SRT ファイル**をダウンロードするブックマークレットです。

- `[Intro]` や `[Verse]` など **`[...]` タグ行は除去**
- **歌詞 1 行 = SRT 1 ブロック**（行単位の字幕）
- 出力ファイル名: `{曲ID}-lines.srt`

> **非公式ツールです。** Suno とは無関係です。API の仕様変更で動かなくなる可能性があります。

## インストール

GitHub の README 上では `javascript:` リンクが使えないため、**インストール用ページ（GitHub Pages）** から登録してください。

### 方法 1: ドラッグ（推奨）

1. **[インストールページ](https://kuwa2005.github.io/suno-line-srt-bookmarklet/)** を開く
2. ブックマークバーを表示（Chrome: `Ctrl+Shift+B`）
3. **「Suno 行SRT 取得」** ボタンをブックマークバーへドラッグ

### 方法 2: 手動登録

1. [インストールページ](https://kuwa2005.github.io/suno-line-srt-bookmarklet/) を開く
2. 「URL をコピー」をクリック
3. ブックマークマネージャで新規ブックマークを作成
   - **名前:** `Suno 行SRT 取得`
   - **URL:** コピーした 1 行をそのまま貼り付け

> URL を貼るとブラウザが percent-encoding して `SyntaxError` になることがあります。可能なら **ドラッグ登録** を使ってください。

## 使い方

1. [Suno](https://suno.com/) にログイン
2. 対象曲の `/song/{id}` または `/edit/{id}` を開く
3. ブックマークバーの **Suno 行SRT 取得** をクリック
4. `{曲ID}-lines.srt` がダウンロードされ、行数が alert で表示されます

## うまくいかないとき

| メッセージ | 対処 |
|-----------|------|
| song/edit ページで実行してください | 曲ページ以外では動きません |
| ログインが必要です | Suno にログインして再実行 |
| APIエラー | ページを再読み込みして再実行 |
| SyntaxError: Unexpected end of input | 古いブックマークを削除し、インストールページから入れ直す |

## 仕組み

1. 現在の URL から曲 ID を取得
2. ログイン Cookie（`__session`）で `aligned_lyrics/v2` API を呼び出し
3. タグ行を除去して SRT 形式に変換
4. Blob ダウンロードで `.srt` を保存

## ライセンス

MIT
