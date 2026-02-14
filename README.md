# アロハ縫 Shopify リニューアルプロジェクト

わんこ用アロハシャツ専門店「アロハ縫茅ヶ崎」のShopify ECサイトリニューアルプロジェクトです。

## 🎯 プロジェクト概要

本番サイト: https://alohanui.jp/  
開発環境: alohanui-demo.myshopify.com

Genspark AIによる改善提案を基に、コンバージョン率向上とユーザー体験改善を目指します。

## 🚀 クイックスタート

### 前提条件
- Node.js v22.20.0
- npm 10.9.3
- Shopify CLI 3.90.1

### 初回セットアップ

```bash
# プロジェクトディレクトリに移動
cd C:\projects\alohanui-demo

# Shopify CLI でログイン
shopify auth login

# 開発サーバー起動
shopify theme dev --store alohanui-demo
```

ブラウザで `http://127.0.0.1:9292` にアクセスして確認できます。

### 日常的な開発

```bash
# 開発サーバー起動
shopify theme dev

# テーマをプル（最新状態を取得）
shopify theme pull --store alohanui-demo

# テーマをプッシュ（変更を反映）
shopify theme push --store alohanui-demo
```

## 📁 プロジェクト構造

```
alohanui-demo/
├── README.md                    # このファイル
├── HANDOVER.md                  # 引き継ぎドキュメント（最重要）
├── PROJECT_CONTEXT.md           # プロジェクト全体像
├── .cursorrules                 # Cursor AI用ルール
│
├── docs/                        # ドキュメント
│   ├── genspark-manual.md       # Gensparkの改善提案
│   ├── implementation-log.md    # 実装記録
│   ├── setup-log.md             # セットアップ記録
│   ├── decisions.md             # 意思決定ログ
│   │
│   ├── prompts/                 # 各機能の実装プロンプト
│   │   ├── 01-cta-button.md
│   │   ├── 02-photos.md
│   │   ├── 03-reviews.md
│   │   ├── 04-size-guide.md
│   │   └── 05-hero-section.md
│   │
│   └── designs/                 # デザイン素材
│       └── README.md
│
└── (Shopify テーマファイル群)
    ├── layout/
    ├── templates/
    ├── sections/
    ├── snippets/
    └── assets/
```

## 📚 重要ドキュメント

最初に読むべきドキュメント：

1. **[HANDOVER.md](./HANDOVER.md)** - プロジェクト引き継ぎ情報、進捗状況、次のステップ
2. **[PROJECT_CONTEXT.md](./PROJECT_CONTEXT.md)** - ビジネス背景、KPI、戦略
3. **[.cursorrules](./.cursorrules)** - コーディング規約とルール

## 🎨 実装フェーズ

### Phase 1: 最優先項目（1〜2週間）
- [ ] ①購入ボタン改善
- [ ] ②商品写真追加
- [ ] ③レビュー機能導入
- [ ] ④サイズガイド刷新
- [ ] ⑤トップページヒーロー改善

詳細は [HANDOVER.md](./HANDOVER.md) を参照してください。

## 🛠️ 開発ワークフロー

### 実装前
1. `HANDOVER.md` で現在の進捗を確認
2. `docs/prompts/` から該当プロンプトを読む
3. 対象ファイルを特定

### 実装中
1. `shopify theme dev` で開発サーバー起動
2. ファイルを編集（自動でリロード）
3. ブラウザでプレビュー確認

### 実装後
1. `docs/implementation-log.md` に作業内容を記録
2. プロンプトの確認ポイントをチェック
3. 問題なければ push

```bash
shopify theme push --store alohanui-demo
```

## ⚠️ 重要な注意事項

### 🚨 本番環境を触らない
- 本番ストア（alohanui.jp）には**絶対に直接編集しない**
- 必ず開発ストア（alohanui-demo）で検証
- 本番反映はクライアント承認後のみ

### 🔐 ストアの確認
コマンド実行前に必ず確認：
```bash
# 現在のストアを確認
shopify theme info
```

`alohanui-demo` または `bekffc-wz` であることを確認してください。

## 🎯 コーディング規約

### CSS（BEM方式）
```css
.product-card { }                /* Block */
.product-card__title { }         /* Element */
.product-card--featured { }      /* Modifier */
```

### Liquid
```liquid
{% comment %} 日本語でコメント OK {% endcomment %}
{% assign product_title = product.title %}
{{ product_title | escape }}
```

詳細は [.cursorrules](./.cursorrules) を参照してください。

## 🧪 テスト環境

| 環境 | ストア名 | URL | 用途 |
|------|---------|-----|------|
| 開発 | alohanui-demo | alohanui-demo.myshopify.com | 主な開発環境 |
| テスト | テストショップ | bekffc-wz.myshopify.com | 有料機能テスト |

## 📊 KPI

### 主要指標
- コンバージョン率: +30%改善目標
- カート追加率: +40%改善目標
- モバイル購入率: +50%増加目標

詳細は [PROJECT_CONTEXT.md](./PROJECT_CONTEXT.md) を参照してください。

## 🤝 コントリビューション

### 実装の進め方
1. Issue を作成（任意）
2. 該当プロンプトに従って実装
3. ローカルでテスト
4. `implementation-log.md` に記録

### 重要な決定事項
大きな方針変更は `docs/decisions.md` に記録してください。

## 🤖 Claude Projects との連携

このプロジェクトは Claude Projects と連携して、スレッド間で文脈を保持します。

### 初回セットアップ（1回のみ）

#### 1. GitHubリポジトリの準備
このリポジトリは既に公開されています：  
**https://github.com/ponta-ta-taro/alohanui-shopify-docs**

#### 2. Claude Projects の作成
1. Claude の左サイドバーから「Projects」をクリック
2. 「New Project」をクリック
3. プロジェクト名：`アロハ縫 Shopify`
4. 「Create Project」をクリック

#### 3. Project Knowledge へファイルを追加
1. プロジェクト画面で「Add content」→「From GitHub」をクリック
2. リポジトリを選択：`ponta-ta-taro/alohanui-shopify-docs`
3. 以下のファイルを**すべて**選択：
   - ✅ HANDOVER.md
   - ✅ PROJECT_CONTEXT.md
   - ✅ README.md
   - ✅ STATUS.md
   - ✅ .cursorrules
   - ✅ docs/ フォルダ（プロンプトファイル含む）
4. 「ファイルを追加」をクリック

### 日常的な使い方

#### 新しいチャットを開始する時
```
アロハ縫の続きやります。
今日はPhase 1-①のCTAボタン改善から。
```

Claude が自動的に Project Knowledge を参照し、文脈を理解した状態で応答します。

#### STATUS.md を更新した時
1. ローカルで STATUS.md を編集
2. Git コミット＆プッシュ：
```bash
git add STATUS.md
git commit -m "update: 作業進捗を更新"
git push origin main
```
3. Claude Projects で「Refresh」（自動同期の場合は不要）

### Project Knowledge に含まれる情報
- プロジェクト全体像（目的、KPI、戦略）
- 現在の進捗状況（STATUS.md）
- 実装ガイド（プロンプトファイル）
- コーディング規約（.cursorrules）
- 環境構成（HANDOVER.md）

### メリット
- ✅ 新しいチャットでも文脈が継続
- ✅ 毎回ファイルをアップロード不要
- ✅ ドキュメントが常に最新（Git経由）
- ✅ 複数人での作業に対応可能

## 🆘 トラブルシューティング

### Shopify CLI が動かない
```bash
shopify version
# 古い場合は更新
npm update -g @shopify/cli @shopify/theme
```

### ログインできない
```bash
shopify auth logout
shopify auth login
```

### 変更が反映されない
1. 開発サーバーを再起動
2. ブラウザのキャッシュをクリア
3. ストア管理画面でテーマを確認

## 📞 サポート

- **Shopify ドキュメント**: https://shopify.dev/docs
- **Liquid リファレンス**: https://shopify.dev/docs/themes/liquid/reference
- **Shopify コミュニティ**: https://community.shopify.com/

## 📝 ライセンス

このプロジェクトは「アロハ縫茅ヶ崎」の所有物です。

---

**プロジェクトスタート**: 2026-02-14  
**開発者**: ponta10sakura@gmail.com  
**ステータス**: 🟢 開発環境セットアップ完了

困ったときは [HANDOVER.md](./HANDOVER.md) に戻ってください！
