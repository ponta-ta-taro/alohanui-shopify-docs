# タスク: 商品ページ購入ボタン改善

## 📋 概要

**Phase**: 1  
**優先度**: 🔴 高  
**予想工数**: 3〜4時間  
**実装者**: 開発チーム

## 🎯 目的

商品ページの購入ボタン（CTA: Call To Action）を改善し、コンバージョン率を向上させる。

### 改善の狙い
- 購入ボタンの視認性を高める
- クリックしたくなる訴求力を向上
- モバイルでの購入体験を改善（sticky対応）
- ホバー時のアニメーションで動的な印象を与える

### 期待される効果
- カート追加率 +40%
- 特にモバイルからの購入率向上
- ユーザーの迷いを減らし、購入までの時間短縮

## 📂 対象ファイル

### 編集が必要なファイル
- `sections/main-product.liquid` - 商品ページメインセクション
- `assets/component-product.css` または `assets/base.css` - スタイル定義
- 必要に応じて `snippets/buy-buttons.liquid`

### 確認が必要なファイル
- `layout/theme.liquid` - 全体のレイアウト
- `sections/header.liquid` - ヘッダーとの干渉確認

## 🎨 デザイン仕様

### カラースキーム
```css
/* メインボタン */
background: linear-gradient(135deg, #FF6B6B 0%, #FF8E8E 100%);
color: #FFFFFF;
border: none;
box-shadow: 0 4px 15px rgba(255, 107, 107, 0.3);

/* ホバー時 */
background: linear-gradient(135deg, #FF5252 0%, #FF7575 100%);
box-shadow: 0 6px 20px rgba(255, 107, 107, 0.4);
transform: translateY(-2px);

/* アクティブ時（クリック時） */
transform: translateY(0);
box-shadow: 0 2px 10px rgba(255, 107, 107, 0.3);
```

### サイズ・余白
```css
/* デスクトップ */
padding: 18px 40px;
font-size: 18px;
font-weight: 700;
border-radius: 50px;
min-height: 56px;

/* モバイル（750px未満） */
padding: 16px 32px;
font-size: 16px;
min-height: 52px;
width: 100%; /* 全幅 */
```

### アニメーション
```css
transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);

/* ホバー時のアニメーション */
@keyframes pulse {
  0% { box-shadow: 0 4px 15px rgba(255, 107, 107, 0.3); }
  50% { box-shadow: 0 6px 25px rgba(255, 107, 107, 0.5); }
  100% { box-shadow: 0 4px 15px rgba(255, 107, 107, 0.3); }
}
```

### モバイル対応（Sticky）
```css
/* モバイルでは画面下部に固定 */
@media screen and (max-width: 749px) {
  .product-form__submit--sticky {
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
    z-index: 10;
    margin: 0;
    border-radius: 0;
    padding: 16px;
    background: white;
    box-shadow: 0 -2px 10px rgba(0, 0, 0, 0.1);
  }
  
  .product-form__submit--sticky button {
    width: 100%;
  }
}
```

## 💻 実装内容

### Gensparkマニュアルの該当部分

> **※重要**: `docs/genspark-manual.md` の「①購入ボタン改善」セクションを参照し、Gensparkの具体的な提案内容をここに転記してください。

（以下はプレースホルダーです。実際のGenspark提案に置き換えてください）

---

### 1. ボタンのHTML構造改善

現在の構造を確認し、必要に応じて以下のように改善：

```liquid
<div class="product-form__submit">
  <button
    type="submit"
    name="add"
    class="product-form__cart-submit button button--primary button--full-width"
    {% if product.selected_or_first_available_variant.available == false %}
      disabled
    {% endif %}
  >
    <span>
      {% if product.selected_or_first_available_variant.available %}
        カートに追加
      {% else %}
        在庫切れ
      {% endif %}
    </span>
  </button>
</div>
```

### 2. CSS実装

`assets/component-product.css` に以下を追加：

```css
/* 購入ボタンのベーススタイル */
.product-form__cart-submit {
  background: linear-gradient(135deg, #FF6B6B 0%, #FF8E8E 100%);
  color: #FFFFFF;
  font-size: 18px;
  font-weight: 700;
  padding: 18px 40px;
  border: none;
  border-radius: 50px;
  min-height: 56px;
  box-shadow: 0 4px 15px rgba(255, 107, 107, 0.3);
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  cursor: pointer;
  position: relative;
  overflow: hidden;
}

/* ホバーエフェクト */
.product-form__cart-submit:hover:not(:disabled) {
  background: linear-gradient(135deg, #FF5252 0%, #FF7575 100%);
  box-shadow: 0 6px 20px rgba(255, 107, 107, 0.4);
  transform: translateY(-2px);
}

/* アクティブ状態 */
.product-form__cart-submit:active:not(:disabled) {
  transform: translateY(0);
  box-shadow: 0 2px 10px rgba(255, 107, 107, 0.3);
}

/* 在庫切れ時 */
.product-form__cart-submit:disabled {
  background: #CCCCCC;
  cursor: not-allowed;
  box-shadow: none;
}

/* モバイル対応 */
@media screen and (max-width: 749px) {
  .product-form__cart-submit {
    font-size: 16px;
    padding: 16px 32px;
    min-height: 52px;
    width: 100%;
  }
  
  /* Stickyバージョン（スクロールしても見える） */
  .product-form__submit--sticky {
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
    z-index: 10;
    margin: 0;
    padding: 12px 16px;
    background: white;
    box-shadow: 0 -2px 10px rgba(0, 0, 0, 0.1);
  }
}
```

### 3. JavaScript（Sticky機能）

必要に応じて、スクロール時にStickyクラスを追加：

```javascript
// Sticky購入ボタン
document.addEventListener('DOMContentLoaded', () => {
  const productForm = document.querySelector('.product-form__submit');
  const triggerHeight = 600; // スクロール量の閾値

  if (!productForm || window.innerWidth > 749) return; // デスクトップでは不要

  window.addEventListener('scroll', () => {
    if (window.scrollY > triggerHeight) {
      productForm.classList.add('product-form__submit--sticky');
    } else {
      productForm.classList.remove('product-form__submit--sticky');
    }
  });
});
```

## ✅ 確認ポイント

### デスクトップ（990px以上）
- [ ] ボタンがコーラル色のグラデーションになっているか
- [ ] ホバー時に浮き上がるアニメーションが動作するか
- [ ] クリック時に押し込まれる感じがあるか
- [ ] ボタンのサイズが適切か（大きすぎず小さすぎず）
- [ ] 在庫切れ時にグレーアウトするか

### モバイル（749px以下）
- [ ] ボタンが全幅で表示されるか
- [ ] スクロールすると画面下部に固定されるか（Sticky）
- [ ] Sticky時にヘッダーやフッターと干渉しないか
- [ ] タップしやすいサイズか（最小44x44px）
- [ ] スクロール中のパフォーマンスに問題ないか

### 全体
- [ ] フォント、色がブランドガイドラインに沿っているか
- [ ] アクセシビリティ（コントラスト比、フォーカス状態）は適切か
- [ ] 他のボタン（「今すぐ購入」など）との一貫性があるか
- [ ] ローディング中の状態表示があるか

## 🧪 テスト手順

### 1. ローカルでのプレビュー
```bash
shopify theme dev --store alohanui-demo
```

### 2. 各デバイスでの確認
- デスクトップ（Chrome、Edge、Firefox）
- モバイル（Chrome、Safari）
- タブレット

### 3. 動作テスト
1. 商品ページにアクセス
2. ボタンをホバー（デスクトップ）→ アニメーション確認
3. ボタンをクリック→ カート追加確認
4. 在庫切れ商品で確認→ ボタン無効化確認
5. スクロールテスト（モバイル）→ Sticky動作確認

### 4. パフォーマンステスト
- Chrome DevTools で Lighthouse 実行
- スクロール時のフレームレート確認

## 📝 実装後のアクション

### 1. 記録
`docs/implementation-log.md` に以下を記録：
- 実装日時
- 変更ファイル一覧
- 気づいた点や改善点

### 2. スクリーンショット
- Before/After のスクリーンショットを `docs/designs/` に保存
- モバイル版も撮影

### 3. 効果測定の準備
- Shopify Analytics でカート追加率を記録開始
- Google Analytics のイベントトラッキング設定（任意）

### 4. クライアント報告
- 実装内容をまとめて報告書作成
- デモ環境（alohanui-demo）のURLを共有

## 🚨 注意事項

### やってはいけないこと
- ❌ 本番環境（alohanui.jp）に直接push
- ❌ テストせずにデプロイ
- ❌ 過度なアニメーション（パフォーマンス低下）
- ❌ モバイルでのテストを省略

### 気をつけること
- ⚠️ 既存のJavaScriptとの競合
- ⚠️ Z-indexの管理（Stickyボタンが他要素に隠れないように）
- ⚠️ iOS Safariでの挙動（特にposition: fixed）
- ⚠️ アクセシビリティ（色のコントラスト、フォーカス状態）

## 🔗 関連ドキュメント

- `docs/genspark-manual.md` - 元の改善提案
- `HANDOVER.md` - Phase 1の全体像
- `.cursorrules` - コーディング規約
- `docs/implementation-log.md` - 実装記録

## 💡 追加のアイデア

実装しながら思いついた改善案があればメモ：

- [ ] カートに追加後の成功メッセージアニメーション
- [ ] 「残りX個」の在庫表示で緊急性を演出
- [ ] 「今すぐ購入」ボタン（Shopify Payments利用時）の追加検討
- [ ] ボタンクリック時のマイクロインタラクション強化

---

**作成日**: 2026-02-14  
**実装予定**: Phase 1（1〜2週間以内）  
**ステータス**: 📋 未着手
