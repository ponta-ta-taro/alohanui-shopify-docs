# タスク: 商品写真追加・ギャラリー改善

## 📋 概要

**Phase**: 1  
**優先度**: 🔴 高  
**予想工数**: 4〜6時間  
**実装者**: 開発チーム

## 🎯 目的

商品ページに複数の写真を追加し、ギャラリー形式で表示することで商品の魅力を最大限に伝える。

### 改善の狙い
- 複数アングルから商品を見せる
- わんこが実際に着用している姿を見せる
- サイズ感や質感が伝わる写真を追加
- ユーザーが自由に写真を切り替えられる

### 期待される効果
- 商品理解度の向上
- 購入時の不安解消
- 返品率の低下
- コンバージョン率 +20〜30%

## 📂 対象ファイル

### 編集が必要なファイル
- `sections/main-product.liquid` - 商品ページメインセクション
- `assets/component-product-media.css` - メディアギャラリーのスタイル
- `assets/product-media-gallery.js` - ギャラリーの動作（必要に応じて）

### 確認が必要なファイル
- `snippets/product-thumbnail.liquid` - サムネイル表示
- `sections/product-recommendations.liquid` - 関連商品表示

## 🎨 デザイン仕様

### ギャラリーレイアウト

#### デスクトップ（990px以上）
```
┌─────────────┬──────────────────────┐
│ サムネイル  │   メイン画像         │
│ ┌────┐     │   ┌──────────────┐   │
│ │img1│     │   │              │   │
│ └────┘     │   │   大きく表示 │   │
│ ┌────┐     │   │              │   │
│ │img2│     │   └──────────────┘   │
│ └────┘     │                      │
│ ┌────┐     │   < >  ナビゲーション │
│ │img3│     │                      │
│ └────┘     │                      │
└─────────────┴──────────────────────┘
```

#### モバイル（749px以下）
```
┌──────────────────────┐
│   メイン画像          │
│   ┌──────────────┐   │
│   │              │   │
│   │   スワイプ可 │   │
│   │              │   │
│   └──────────────┘   │
│   ● ○ ○ ○  ドット   │
└──────────────────────┘
  サムネイルは横スクロール
```

### 推奨する写真構成

1. **メイン写真（必須）**
   - 商品全体が見える正面写真
   - 白または明るい背景
   - 高解像度（最低1000x1000px）

2. **詳細写真（推奨）**
   - 生地の質感が分かるクローズアップ
   - ボタンや縫製の詳細
   - 柄の全体像

3. **着用写真（必須）**
   - わんこが実際に着ている写真
   - 正面、横、後ろの3アングル
   - サイズ感が分かる全身ショット

4. **サイズ比較写真（推奨）**
   - サイズ違いの並べて比較
   - 測り方の参考写真

5. **コーディネート例（任意）**
   - 季節や用途別の着こなし
   - 小物との組み合わせ

### スタイル仕様

```css
/* ギャラリーコンテナ */
.product-media-gallery {
  display: grid;
  gap: 16px;
  grid-template-columns: 100px 1fr; /* サムネイル + メイン */
}

/* メイン画像 */
.product-media-gallery__main {
  position: relative;
  aspect-ratio: 1 / 1;
  background: #F8F8F8;
  border-radius: 12px;
  overflow: hidden;
}

.product-media-gallery__main img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  cursor: zoom-in;
}

/* サムネイル */
.product-media-gallery__thumbnails {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.product-thumbnail {
  aspect-ratio: 1 / 1;
  border: 2px solid transparent;
  border-radius: 8px;
  overflow: hidden;
  cursor: pointer;
  transition: border-color 0.3s;
}

.product-thumbnail--active {
  border-color: #FF6B6B;
}

.product-thumbnail:hover {
  border-color: #FF8E8E;
}

/* モバイル対応 */
@media screen and (max-width: 749px) {
  .product-media-gallery {
    grid-template-columns: 1fr;
  }
  
  .product-media-gallery__thumbnails {
    flex-direction: row;
    overflow-x: auto;
    -webkit-overflow-scrolling: touch;
  }
  
  .product-thumbnail {
    min-width: 80px;
  }
}
```

## 💻 実装内容

### Gensparkマニュアルの該当部分

> **※重要**: `docs/genspark-manual.md` の「②商品写真追加」セクションを参照し、Gensparkの具体的な提案内容をここに転記してください。

---

### 1. Liquidテンプレート実装

`sections/main-product.liquid` に以下の構造を実装：

```liquid
<div class="product-media-gallery">
  {%- if product.media.size > 0 -%}
    {%- comment -%} サムネイルエリア {%- endcomment -%}
    <div class="product-media-gallery__thumbnails">
      {%- for media in product.media limit: 6 -%}
        <button
          class="product-thumbnail{% if forloop.first %} product-thumbnail--active{% endif %}"
          data-media-id="{{ media.id }}"
          aria-label="画像 {{ forloop.index }} を表示"
        >
          <img
            src="{{ media | image_url: width: 100 }}"
            alt="{{ media.alt | escape }}"
            loading="lazy"
          >
        </button>
      {%- endfor -%}
    </div>

    {%- comment -%} メイン画像エリア {%- endcomment -%}
    <div class="product-media-gallery__main">
      {%- for media in product.media limit: 6 -%}
        <div
          class="product-media-item{% if forloop.first %} product-media-item--active{% endif %}"
          data-media-id="{{ media.id }}"
        >
          {%- if media.media_type == 'image' -%}
            <img
              srcset="{{ media | image_url: width: 375 }} 375w,
                      {{ media | image_url: width: 750 }} 750w,
                      {{ media | image_url: width: 1100 }} 1100w"
              src="{{ media | image_url: width: 750 }}"
              alt="{{ media.alt | escape }}"
              loading="{% if forloop.first %}eager{% else %}lazy{% endif %}"
              width="{{ media.width }}"
              height="{{ media.height }}"
            >
          {%- elsif media.media_type == 'video' -%}
            {{ media | video_tag: autoplay: false, controls: true }}
          {%- endif -%}
        </div>
      {%- endfor -%}
    </div>
  {%- else -%}
    {%- comment -%} 画像がない場合のプレースホルダー {%- endcomment -%}
    <div class="product-media-gallery__placeholder">
      {{ 'product-1' | placeholder_svg_tag }}
    </div>
  {%- endif -%}
</div>
```

### 2. CSS実装

```css
/* ギャラリーグリッド */
.product-media-gallery {
  display: grid;
  gap: 16px;
  grid-template-columns: 100px 1fr;
  margin-bottom: 32px;
}

/* メイン画像エリア */
.product-media-gallery__main {
  position: relative;
  background: #F8F8F8;
  border-radius: 12px;
  overflow: hidden;
}

.product-media-item {
  display: none;
  aspect-ratio: 1 / 1;
}

.product-media-item--active {
  display: block;
}

.product-media-item img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  cursor: zoom-in;
}

/* ズーム機能（ホバー時） */
.product-media-item img:hover {
  transform: scale(1.05);
  transition: transform 0.3s ease;
}

/* サムネイルエリア */
.product-media-gallery__thumbnails {
  display: flex;
  flex-direction: column;
  gap: 8px;
  overflow-y: auto;
  max-height: 600px;
}

.product-thumbnail {
  position: relative;
  aspect-ratio: 1 / 1;
  background: transparent;
  border: 2px solid #E0E0E0;
  border-radius: 8px;
  overflow: hidden;
  cursor: pointer;
  transition: all 0.3s ease;
  padding: 0;
}

.product-thumbnail img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.product-thumbnail:hover {
  border-color: #FF8E8E;
  transform: scale(1.05);
}

.product-thumbnail--active {
  border-color: #FF6B6B;
  border-width: 3px;
}

/* モバイル対応 */
@media screen and (max-width: 749px) {
  .product-media-gallery {
    grid-template-columns: 1fr;
    gap: 12px;
  }
  
  .product-media-gallery__thumbnails {
    flex-direction: row;
    overflow-x: auto;
    overflow-y: visible;
    max-height: none;
    -webkit-overflow-scrolling: touch;
    scroll-snap-type: x mandatory;
  }
  
  .product-thumbnail {
    min-width: 80px;
    scroll-snap-align: start;
  }
}

/* スマホスワイプ対応 */
@media screen and (max-width: 749px) {
  .product-media-gallery__main {
    touch-action: pan-x;
  }
}
```

### 3. JavaScript実装

```javascript
// 商品ギャラリーの切り替え
document.addEventListener('DOMContentLoaded', () => {
  const thumbnails = document.querySelectorAll('.product-thumbnail');
  const mediaItems = document.querySelectorAll('.product-media-item');

  thumbnails.forEach(thumbnail => {
    thumbnail.addEventListener('click', () => {
      const mediaId = thumbnail.dataset.mediaId;

      // すべての active クラスを削除
      thumbnails.forEach(t => t.classList.remove('product-thumbnail--active'));
      mediaItems.forEach(m => m.classList.remove('product-media-item--active'));

      // クリックされた要素に active クラスを追加
      thumbnail.classList.add('product-thumbnail--active');
      const targetMedia = document.querySelector(
        `.product-media-item[data-media-id="${mediaId}"]`
      );
      if (targetMedia) {
        targetMedia.classList.add('product-media-item--active');
      }
    });
  });

  // キーボードナビゲーション（アクセシビリティ）
  thumbnails.forEach((thumbnail, index) => {
    thumbnail.addEventListener('keydown', (e) => {
      if (e.key === 'ArrowDown' && thumbnails[index + 1]) {
        thumbnails[index + 1].focus();
      } else if (e.key === 'ArrowUp' && thumbnails[index - 1]) {
        thumbnails[index - 1].focus();
      }
    });
  });
});
```

### 4. 画像最適化の推奨設定

#### Shopify設定で推奨する形式
- **形式**: WebP（自動変換）
- **サイズ**: 1000x1000px 以上
- **アスペクト比**: 1:1（正方形）
- **ファイルサイズ**: 200KB以下を目標
- **Alt属性**: 必ず設定（SEO・アクセシビリティ）

#### 命名規則
```
商品名_角度_サイズ.jpg

例:
aloha-shirt-red_front_1000x1000.jpg
aloha-shirt-red_side_1000x1000.jpg
aloha-shirt-red_back_1000x1000.jpg
aloha-shirt-red_detail_1000x1000.jpg
aloha-shirt-red_wearing_1000x1000.jpg
```

## ✅ 確認ポイント

### 機能面
- [ ] サムネイルをクリックするとメイン画像が切り替わるか
- [ ] 最初の画像がデフォルトで選択されているか
- [ ] 選択中のサムネイルが視覚的に分かるか
- [ ] キーボード操作（矢印キー）で切り替えられるか
- [ ] 画像の読み込みが遅延ロード（lazy loading）されているか

### デザイン面
- [ ] 画像のアスペクト比が統一されているか
- [ ] サムネイルとメイン画像のサイズバランスが適切か
- [ ] ホバー時のエフェクトがスムーズか
- [ ] ボーダーやパディングが美しいか

### モバイル
- [ ] サムネイルが横スクロールで表示されるか
- [ ] スワイプでメイン画像を切り替えられるか（任意機能）
- [ ] タップしやすいサイズか（最小44x44px）
- [ ] 画像の読み込みが速いか

### パフォーマンス
- [ ] Lighthouse スコアが90以上か
- [ ] LCP（最大コンテンツの描画）が2.5秒以下か
- [ ] 画像が最適化されているか（WebP、適切なサイズ）

### アクセシビリティ
- [ ] Alt属性が適切に設定されているか
- [ ] キーボードナビゲーションが動作するか
- [ ] スクリーンリーダーで適切に読み上げられるか
- [ ] フォーカス状態が視覚的に分かるか

## 🧪 テスト手順

### 1. 画像のアップロード
1. Shopify管理画面で商品を開く
2. 「メディア」セクションから画像を追加
3. Alt属性を設定（例：「アロハシャツ 赤 正面」）
4. 並び順を調整

### 2. ローカルプレビュー
```bash
shopify theme dev --store alohanui-demo
```

### 3. 動作確認
1. 商品ページにアクセス
2. サムネイルをクリック → メイン画像切り替え確認
3. 各デバイスサイズでレイアウト確認
4. キーボード操作で切り替え確認

### 4. パフォーマンステスト
```bash
# Lighthouseでパフォーマンス測定
# Chrome DevTools > Lighthouse > Analyze page load
```

## 📝 実装後のアクション

### 1. 画像素材の準備依頼
クライアントに以下の写真を依頼：
- [ ] 各商品の正面・側面・背面写真
- [ ] わんこが着用している写真（複数アングル）
- [ ] 生地や縫製の詳細写真
- [ ] サイズ比較写真

### 2. 既存商品への適用
- [ ] 主力商品5〜10点に新しいギャラリーを適用
- [ ] 効果測定のため、一部商品は従来のまま（A/Bテスト）

### 3. ドキュメント更新
- `docs/implementation-log.md` に実装記録
- Before/After のスクリーンショット保存

### 4. 効果測定
- [ ] 商品ページの滞在時間
- [ ] カート追加率
- [ ] 返品率（長期的）

## 🚨 注意事項

### やってはいけないこと
- ❌ 画像を最適化せずにアップロード（重いファイル）
- ❌ Alt属性を設定しない
- ❌ アスペクト比がバラバラの画像を使う
- ❌ 過度なアニメーション（パフォーマンス低下）

### 気をつけること
- ⚠️ 著作権・肖像権の確認
- ⚠️ 画像の品質と読み込み速度のバランス
- ⚠️ モバイルでの表示崩れ
- ⚠️ 画像がない商品でのエラー回避

## 🔗 関連ドキュメント

- `docs/genspark-manual.md` - 元の改善提案
- `HANDOVER.md` - Phase 1の全体像
- `.cursorrules` - コーディング規約
- `docs/designs/` - 画像素材の管理

## 💡 追加のアイデア

- [ ] ズーム機能（画像をクリックで拡大表示）
- [ ] 360度回転ビュー（余裕があれば）
- [ ] 動画の組み込み（着用動画、制作過程）
- [ ] Instagram投稿の埋め込み（お客様の投稿）
- [ ] 比較スライダー（ビフォー・アフター）

---

**作成日**: 2026-02-14  
**実装予定**: Phase 1（1〜2週間以内）  
**ステータス**: 📋 未着手
