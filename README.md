# 助手くんやることリスト

毎日やることをスタンプで記録するチェックリストサイト。

## 機能

- 5項目のスタンプ式チェックリスト
- **JST 0時で毎日自動リセット**（タブ開きっぱなしでも自動切り替え）
- ブラウザごとに状態保持（`localStorage`、ユーザー間同期なし）
- レスポンシブ対応（PC・スマホ両対応、最大幅 500px）
- スタンプはタップで押す／もう一度タップで取り消し
- プライベートブラウジング等で localStorage が使えない環境では警告表示＋メモリ動作

## 公開 URL

`https://<your-github-username>.github.io/joshukun-todo/`

## デプロイ手順

1. このリポジトリを GitHub に作成（Public）
2. `index.html` / `stamp.png` / `README.md` / `LICENSE` をコミット
3. リポジトリの **Settings → Pages** を開く
4. **Source: Deploy from a branch** を選択し、`main` / `/ (root)` を指定して保存
5. 数分後、上記 URL でアクセス可能

## ファイル構成

```
joshukun-todo/
├── index.html   # 全部入り（HTML + CSS + JS）
├── stamp.png    # スタンプ画像（透過PNG）
├── README.md
└── LICENSE
```

## カスタマイズ

- **スタンプ画像差し替え**: `stamp.png`（透過 PNG、正方形、512px 以上推奨）を置き換えるだけ
- **項目変更**: `index.html` の `ITEMS` 配列を編集
- **配色変更**: `index.html` 冒頭の `:root` CSS 変数を編集

## 技術仕様

- 単一 HTML ファイル（依存パッケージなし、ビルド不要）
- 外部依存は Google Fonts (`M PLUS Rounded 1c`) のみ
- JavaScript はバニラ JS、IIFE 構成
- データ構造（localStorage）:
  ```json
  { "v": 1, "date": "2026-05-10", "checked": [true, false, false, true, false] }
  ```
- 日付ロールオーバー検出は 30 秒間隔の interval ＋ visibilitychange イベント

## 免責事項

This is an **unofficial fan-made site**. Not affiliated with, endorsed by, or sponsored by Cover Corp. / hololive production / Hakui Koyori.

本サイトは非公式・非営利のファンメイドコンテンツです。カバー株式会社、ホロライブプロダクション、博衣こより氏とは一切関係ありません。

## ライセンス

コードは [MIT License](./LICENSE) で配布。

`stamp.png` はリポジトリオーナーが用意した自作画像です。fork して使う場合は自分のスタンプに差し替えることを推奨します。
