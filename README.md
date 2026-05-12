# 助手くんやることリスト

毎日のこよ活をスタンプで記録するチェックリスト＋スタンプ帳。

## 機能

- 5項目のスタンプ式チェックリスト（「やること」タブ）
- 期間カレンダーのスタンプ帳（「スタンプ帳」タブ、2026/5/11〜6/14）
- 5個達成すると自動でスタンプ帳に切替＋今日のセルにスタンプが押される（ピンク）
- **過去日スタンプ機能**：スタンプ帳の過去日（未スタンプ）をタップ→確認モーダル→ピンクのスタンプが押せる（一度押すと取消不可）
- **JST 0時で毎日自動リセット**（タブ開きっぱなしでも自動切り替え）
- 過去にスタンプ帳に押された記録は永続保持
- ブラウザごとに状態保持（`localStorage`、ユーザー間同期なし）
- レスポンシブ対応（PC・スマホ両対応、最大幅 500px）
- 旧バージョン（v1）からの自動マイグレーション対応

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

`index.html` の冒頭 `<script>` 内に編集ポイントが集約されている：

```javascript
// ====== Config (edit here to change items or calendar range) ======
const ITEMS = [
  'こよの曲を聴く',
  // ... 追加・編集可
];
const START_DATE = '2026-05-11'; // 月曜日推奨
const END_DATE   = '2026-06-14'; // 日曜日推奨
const AUTO_SWITCH_DELAY_MS = 400; // 自動タブ切替までの遅延
```

- **スタンプ画像差し替え**: `stamp.png` を置き換えるだけ（透過 PNG、正方形、512px 以上推奨）
- **配色変更**: `index.html` 冒頭の `:root` CSS 変数を編集
- **カレンダー期間更新**: 上記 `START_DATE` / `END_DATE` を編集

## データ構造

localStorage に格納される v2 データ：

```json
{
  "v": 2,
  "date": "2026-05-11",
  "checked": [true, true, true, true, true],
  "switched": true,
  "calendar": {
    "2026-05-11": true,
    "2026-05-13": true,
    "2026-05-14": true
  }
}
```

- `checked`: 今日のチェック状況。日付が変わるとリセット
- `switched`: 今日達成済みフラグ。自動切替の再発火防止用。日付変更でリセット
- `calendar`: 達成日の永続記録（やることリスト5個達成・スタンプ帳からの手動押下のいずれも `true`）。日付変更でもクリアされない

旧バージョンデータは初回ロード時に自動的に v2 に変換される：

- v1 → v2 マイグレーション
- v1 で当日達成済みだった場合、カレンダー側に `true` 記録が引き継がれる
- `calendar` 内の予期しない値（文字列など）は読み込み時に破棄される

## 日付ロールオーバーの検出

- 30 秒間隔の interval ＋ visibilitychange イベントで日付変更を検出
- JST = UTC+9 固定（夏時間なし）として計算

## 免責事項

This is an unofficial fan-made site. Not affiliated with, endorsed by, or sponsored by Cover Corp. / hololive production / Hakui Koyori.

本サイトは非公式・非営利のファンメイドコンテンツです。カバー株式会社、ホロライブプロダクション、博衣こより氏とは一切関係ありません。

本サイトは、カバー株式会社の「二次創作ガイドライン」に基づいて制作されています。
[https://hololivepro.com/terms/](https://hololivepro.com/terms/)

掲載されている名称・画像・関連権利等は各権利者に帰属します。

## 使用フォント

* [M PLUS Rounded 1c](https://fonts.google.com/specimen/M+PLUS+Rounded+1c)

フォントは Google Fonts 経由で読み込まれます。
フォントの権利は制作者に帰属します。

## ライセンス

コードは [MIT License](./LICENSE) で配布。

`stamp.png` はリポジトリオーナーが用意した自作画像です。fork して使う場合は自分のスタンプに差し替えることを推奨します。
