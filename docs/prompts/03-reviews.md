# タスク: レビュー機能導入

## 📋 概要

**Phase**: 1  
**優先度**: 🔴 高  
**予想工数**: 3〜4時間  
**実装者**: 開発チーム

## 🎯 目的

商品ページにレビュー機能を導入し、お客様の声を目立つ形で表示することで信頼性を高め、購入の後押しをする。

### 改善の狙い
- 社会的証明（Social Proof）による信頼性向上
- 購入者のリアルな声で不安解消
- 写真付きレビューで商品イメージを強化
- レビュー投稿を促進し、UGC（ユーザー生成コンテンツ）を増やす

### 期待される効果
- コンバージョン率 +20〜30%
- 初回購入のハードル低下
- レビューによるSEO効果
- リピート購入率向上

## 📂 対象ファイル

### インストールするアプリ
- **Judge.me** - レビューアプリ（推奨）
  - 写真付きレビュー対応
  - 無料プランあり
  - カスタマイズ性高い

### 編集が必要なファイル（アプリ導入後）
- `sections/main-product.liquid` - レビュー表示エリアの追加
- `assets/component-reviews.css` - レビューのスタイル調整
- `sections/product-template.liquid` - レビュースキーマの追加

### 確認が必要なファイル
- `layout/theme.liquid` - Judge.meのスクリプト読み込み
- `sections/footer.liquid` - レビューバッジの表示

## 🎨 デザイン仕様

### レビュー表示位置

商品ページの構成：
```
1. 商品画像ギャラリー
2. 商品名・価格
3. バリエーション選択
4. 購入ボタン
5. 商品説明
6. 📌 レビューセクション ← ここに配置
7. サイズガイド
8. 配送・返品情報
```

### レビューセクションのレイアウト

#### 概要エリア
```
┌────────────────────────────────────┐
│ ⭐️⭐️⭐️⭐️⭐️ 4.8 (125件のレビュー)  │
│                                    │
│ ⭐️⭐️⭐️⭐️⭐️ 80件                  │
│ ⭐️⭐️⭐️⭐️   35件                  │
│ ⭐️⭐️⭐️     8件                   │
│ ⭐️⭐️       2件                   │
│ ⭐️         0件                   │
│                                    │
│ [📝 レビューを書く]               │
└────────────────────────────────────┘
```

#### 個別レビュー
```
┌────────────────────────────────────┐
│ ⭐️⭐️⭐️⭐️⭐️                       │
│ 「うちの子にぴったり！」           │
│                                    │
│ サイズもちょうどよく、生地も       │
│ しっかりしていて大満足です。       │
│                                    │
│ [📷写真1] [📷写真2]                │
│                                    │
│ 太郎ママ さん                      │
│ 購入商品: アロハシャツ 赤 M        │
│ 投稿日: 2026年1月15日              │
│                                    │
│ ✅ 購入者確認済み                  │
└────────────────────────────────────┘
```

### スタイル指定

```css
/* レビューセクション */
.product-reviews {
  margin-top: 48px;
  padding: 32px;
  background: #FFFFFF;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.05);
}

.product-reviews__header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 24px;
}

.product-reviews__summary {
  display: flex;
  align-items: center;
  gap: 12px;
  font-size: 24px;
  font-weight: 700;
}

.product-reviews__stars {
  color: #FFD700; /* ゴールド */
}

.product-reviews__count {
  font-size: 16px;
  color: #666666;
}

/* 個別レビュー */
.review-item {
  padding: 24px 0;
  border-bottom: 1px solid #E0E0E0;
}

.review-item:last-child {
  border-bottom: none;
}

.review-item__header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: 12px;
}

.review-item__author {
  font-weight: 700;
  color: #2C3E50;
}

.review-item__date {
  font-size: 14px;
  color: #999999;
}

.review-item__stars {
  color: #FFD700;
  margin-bottom: 8px;
}

.review-item__title {
  font-size: 18px;
  font-weight: 700;
  margin-bottom: 8px;
  color: #2C3E50;
}

.review-item__body {
  line-height: 1.6;
  color: #555555;
  margin-bottom: 12px;
}

.review-item__images {
  display: flex;
  gap: 8px;
  margin-top: 12px;
}

.review-item__image {
  width: 100px;
  height: 100px;
  object-fit: cover;
  border-radius: 8px;
  cursor: pointer;
  transition: transform 0.3s;
}

.review-item__image:hover {
  transform: scale(1.05);
}

.review-item__verified {
  display: inline-flex;
  align-items: center;
  gap: 4px;
  font-size: 14px;
  color: #4ECDC4;
  margin-top: 8px;
}

/* レビュー投稿ボタン */
.review-button {
  background: linear-gradient(135deg, #4ECDC4 0%, #44B3AA 100%);
  color: #FFFFFF;
  padding: 12px 24px;
  border: none;
  border-radius: 50px;
  font-weight: 700;
  cursor: pointer;
  transition: all 0.3s;
}

.review-button:hover {
  background: linear-gradient(135deg, #44B3AA 0%, #3A9A92 100%);
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(78, 205, 196, 0.3);
}

/* モバイル対応 */
@media screen and (max-width: 749px) {
  .product-reviews {
    padding: 20px 16px;
    margin-top: 32px;
  }
  
  .product-reviews__header {
    flex-direction: column;
    align-items: flex-start;
    gap: 16px;
  }
  
  .review-item__images {
    overflow-x: auto;
  }
}
```

## 💻 実装内容

### Gensparkマニュアルの該当部分

> **※重要**: `docs/genspark-manual.md` の「③レビュー機能導入」セクションを参照し、Gensparkの具体的な提案内容をここに転記してください。

---

### 1. Judge.meアプリのインストール

#### ステップ1: アプリをインストール
1. Shopifyアプリストアで「Judge.me」を検索
2. 「アプリを追加」をクリック
3. 開発ストア（alohanui-demo）にインストール

#### ステップ2: 初期設定
1. Judge.meダッシュボードにアクセス
2. 言語設定を日本語に変更
3. メール通知テンプレートをカスタマイズ
4. レビュー収集の自動化を設定

#### ステップ3: テーマへの組み込み
Judge.meが自動でテーマにコードを挿入しますが、手動で調整が必要な場合：

```liquid
{%- comment -%} sections/main-product.liquid に追加 {%- endcomment -%}

<div class="product-reviews">
  <div id="judgeme_product_reviews"></div>
  
  {%- comment -%} Judge.meウィジェット {%- endcomment -%}
  <div 
    class="jdgm-widget jdgm-review-widget"
    data-product-id="{{ product.id }}"
  >
    {{ product.metafields.judgeme.badge }}
  </div>
</div>
```

### 2. レビュー表示位置の調整

`sections/main-product.liquid` に以下を追加：

```liquid
{%- comment -%} 商品説明の後、サイズガイドの前 {%- endcomment -%}

<div class="product__reviews-section" id="reviews-section">
  <h2 class="product__reviews-heading">お客様の声</h2>
  
  {%- comment -%} Judge.meバッジ（星評価の概要） {%- endcomment -%}
  <div class="jdgm-widget jdgm-preview-badge" 
       data-id="{{ product.id }}">
    {{ product.metafields.judgeme.badge }}
  </div>
  
  {%- comment -%} Judge.meレビューリスト {%- endcomment -%}
  <div id="judgeme_product_reviews" 
       class="jdgm-widget jdgm-review-widget"
       data-id="{{ product.id }}">
    {{ product.metafields.judgeme.widget }}
  </div>
</div>
```

### 3. スタイルのカスタマイズ

Judge.meのデフォルトスタイルを上書き：

```css
/* assets/component-reviews.css */

/* Judge.meウィジェットのカスタマイズ */
.jdgm-widget {
  font-family: 'Hiragino Sans', 'Hiragino Kaku Gothic ProN', sans-serif;
}

/* 星の色をブランドカラーに */
.jdgm-star {
  color: #FFD700 !important;
}

/* レビュー投稿ボタン */
.jdgm-rev-widg__write-btn {
  background: linear-gradient(135deg, #4ECDC4 0%, #44B3AA 100%) !important;
  border: none !important;
  border-radius: 50px !important;
  padding: 12px 24px !important;
  font-weight: 700 !important;
  transition: all 0.3s !important;
}

.jdgm-rev-widg__write-btn:hover {
  background: linear-gradient(135deg, #44B3AA 0%, #3A9A92 100%) !important;
  transform: translateY(-2px);
}

/* レビュー画像 */
.jdgm-rev__pics .jdgm-rev__pic {
  border-radius: 8px !important;
  overflow: hidden;
}

/* 購入者確認バッジ */
.jdgm-verified-badge {
  color: #4ECDC4 !important;
}
```

### 4. レビュー収集の自動化

#### メール設定
Judge.meダッシュボードで以下を設定：

1. **レビュー依頼メール**
   - 商品発送後7日で自動送信
   - 件名: 「【アロハ縫】ご購入ありがとうございます！レビューをお願いします」
   - 本文: 温かみのある文章、写真投稿の特典を案内

2. **リマインダーメール**
   - 最初のメールから14日後に再送
   - 写真付きレビューの場合の特典を強調

#### インセンティブ設定
- 写真付きレビューで次回使える500円クーポン
- レビュー投稿で100円クーポン

### 5. トップページへのレビュー表示（任意）

```liquid
{%- comment -%} sections/featured-products.liquid {%- endcomment -%}

<div class="product-card__reviews">
  <div class="jdgm-widget jdgm-preview-badge"
       data-id="{{ product.id }}">
    {{ product.metafields.judgeme.badge }}
  </div>
</div>
```

## ✅ 確認ポイント

### 機能面
- [ ] 商品ページにレビューセクションが表示されるか
- [ ] 星評価が正しく表示されるか
- [ ] レビュー投稿ボタンがクリックできるか
- [ ] 写真付きレビューが表示されるか
- [ ] レビューが新しい順/評価順に並び替えられるか

### デザイン面
- [ ] ブランドカラーに合っているか
- [ ] フォントが統一されているか
- [ ] レビュー画像が美しく表示されるか
- [ ] レスポンシブ対応ができているか

### レビュー収集
- [ ] 自動メールが送信されるか
- [ ] メールのデザインがブランドに合っているか
- [ ] クーポンコードが正しく発行されるか
- [ ] レビュー投稿フォームが使いやすいか

### SEO・構造化データ
- [ ] Google検索結果に星評価が表示されるか（要確認）
- [ ] 構造化データ（Schema.org）が適切か

## 🧪 テスト手順

### 1. インストールとセットアップ
```bash
# Judge.meアプリをShopifyアプリストアからインストール
# 開発ストア（alohanui-demo）にインストール
```

### 2. テストレビューの作成
1. Judge.meダッシュボードで「テストレビュー」を作成
2. 星5つ、写真付きのレビューを追加
3. 商品ページで表示を確認

### 3. レビュー投稿フローのテスト
1. テスト注文を作成
2. 注文完了メールを確認
3. レビュー依頼メールを確認（設定により数日後）
4. レビュー投稿フォームから投稿
5. 投稿したレビューが表示されるか確認

### 4. モバイル確認
- iOS Safari
- Android Chrome
- レビュー画像のスワイプ操作

## 📝 実装後のアクション

### 1. 初期レビューの準備
- [ ] 既存顧客にレビュー依頼メールを送信
- [ ] SNSで写真付きレビューを依頼
- [ ] 最初の10件は手動で収集も検討

### 2. レビュー投稿の促進策
- [ ] 購入完了ページにレビュー投稿の案内
- [ ] 梱包物にレビュー依頼のカードを同封
- [ ] SNSキャンペーン（#アロハ縫レビュー）

### 3. 効果測定
- [ ] レビュー数の推移
- [ ] 写真付きレビューの割合
- [ ] レビューありの商品とない商品のCVR比較
- [ ] Google検索での星評価表示確認

### 4. 定期的なメンテナンス
- [ ] 週1回、新規レビューに返信
- [ ] ネガティブレビューへの真摯な対応
- [ ] レビュー投稿率の分析と改善

## 🚨 注意事項

### やってはいけないこと
- ❌ サクラレビューの投稿
- ❌ ネガティブレビューの削除（正当な理由なく）
- ❌ レビュー依頼の過剰な頻度
- ❌ 不適切なインセンティブ（高額な特典など）

### 気をつけること
- ⚠️ ネガティブレビューへの誠実な対応
- ⚠️ 個人情報の保護（レビューに含まれる場合）
- ⚠️ 写真の著作権・肖像権
- ⚠️ Judge.meアプリの料金プラン（無料の範囲を確認）

### Judge.me 無料プランの制限
- レビュー数: 無制限
- 写真付きレビュー: 対応
- 自動メール: 月50通まで
- カスタマイズ: 基本的なもののみ

→ 有料プラン検討の目安：月50件以上の注文

## 🔗 関連ドキュメント

- `docs/genspark-manual.md` - 元の改善提案
- `HANDOVER.md` - Phase 1の全体像
- `.cursorrules` - コーディング規約
- Judge.me公式ドキュメント: https://judge.me/support

## 💡 追加のアイデア

- [ ] レビューハイライト（優良レビューを商品ページ上部に表示）
- [ ] Instagram連携（ハッシュタグ投稿を自動収集）
- [ ] Q&A機能（Judge.meのQ&A機能を活用）
- [ ] レビューランキング（月間ベストレビュー表彰）
- [ ] 動画レビュー対応（余裕があれば）

---

**作成日**: 2026-02-14  
**実装予定**: Phase 1（1〜2週間以内）  
**ステータス**: 📋 未着手
