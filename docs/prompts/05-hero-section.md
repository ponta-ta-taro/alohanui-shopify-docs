# タスク: トップページヒーローセクション改善

## 📋 概要

**Phase**: 1  
**優先度**: 🔴 高  
**予想工数**: 4〜5時間  
**実装者**: 開発チーム

## 🎯 目的

トップページのヒーローセクション（ファーストビュー）を改善し、訪問者の興味を引き、サイト内を回遊してもらう。

### 改善の狙い
- わんこの笑顔で心を掴む
- ブランドの魅力を一瞬で伝える
- 明確な行動喚起（CTA）
- スクロールせずに重要情報が伝わる

### 期待される効果
- 直帰率 -20%
- サイト滞在時間 +30%
- 商品ページへの遷移率 +40%
- ブランド認知度向上

## 📂 対象ファイル

### 編集が必要なファイル
- `sections/hero-banner.liquid` または `sections/image-banner.liquid`
- `assets/section-hero.css` - ヒーローのスタイル
- `templates/index.json` - トップページテンプレート

### 確認が必要なファイル
- `sections/header.liquid` - ヘッダーとの視覚的バランス
- `sections/featured-collection.liquid` - 次のセクションとの繋がり

## 🎨 デザイン仕様

### レイアウト（デスクトップ）

```
┌──────────────────────────────────────────────┐
│                   Header                     │
├──────────────────────────────────────────────┤
│  ┌────────────────────────────────────────┐  │
│  │                                        │  │
│  │    [わんこの笑顔写真（背景）]         │  │
│  │                                        │  │
│  │    ┌──────────────────────────┐      │  │
│  │    │  愛犬に、ハワイの風を    │      │  │
│  │    │  手作りアロハシャツ      │      │  │
│  │    │  アロハ縫茅ヶ崎          │      │  │
│  │    │                          │      │  │
│  │    │  [商品を見る] [こだわり] │      │  │
│  │    └──────────────────────────┘      │  │
│  │                                        │  │
│  └────────────────────────────────────────┘  │
│  ↓ スクロール促進矢印                        │
└──────────────────────────────────────────────┘
```

### レイアウト（モバイル）

```
┌──────────────────────┐
│      Header          │
├──────────────────────┤
│  ┌────────────────┐  │
│  │                │  │
│  │  [わんこの     │  │
│  │   笑顔写真]    │  │
│  │                │  │
│  │  ┌──────────┐  │  │
│  │  │愛犬に、  │  │  │
│  │  │ハワイの風│  │  │
│  │  │を        │  │  │
│  │  │          │  │  │
│  │  │[商品を見る] │  │
│  │  └──────────┘  │  │
│  │                │  │
│  └────────────────┘  │
└──────────────────────┘
```

### コピー案

#### メインコピー（キャッチコピー）
```
愛犬に、ハワイの風を
```

#### サブコピー
```
職人が一枚一枚、心を込めて作る
わんこ専用アロハシャツ
```

#### CTA（行動喚起）
- 主CTA: 「商品を見る」
- 副CTA: 「こだわりを知る」

### カラースキーム

```css
/* ヒーローオーバーレイ（写真の上に半透明レイヤー） */
background: linear-gradient(
  135deg,
  rgba(255, 107, 107, 0.3) 0%,
  rgba(78, 205, 196, 0.3) 100%
);

/* テキスト */
color: #FFFFFF;
text-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);

/* CTAボタン */
.hero__cta-primary {
  background: linear-gradient(135deg, #FF6B6B 0%, #FF8E8E 100%);
  color: #FFFFFF;
}

.hero__cta-secondary {
  background: rgba(255, 255, 255, 0.2);
  backdrop-filter: blur(10px);
  border: 2px solid #FFFFFF;
  color: #FFFFFF;
}
```

### タイポグラフィ

```css
/* メインコピー */
.hero__heading {
  font-size: 56px;
  font-weight: 900;
  line-height: 1.2;
  letter-spacing: 0.02em;
}

/* サブコピー */
.hero__subheading {
  font-size: 20px;
  font-weight: 400;
  line-height: 1.6;
}

/* モバイル */
@media screen and (max-width: 749px) {
  .hero__heading {
    font-size: 32px;
  }
  
  .hero__subheading {
    font-size: 16px;
  }
}
```

### アニメーション

#### ページ読み込み時
1. 背景画像がふんわりズームイン（1秒）
2. テキストがフェードイン（0.5秒、0.3秒遅延）
3. CTAボタンがフェードイン（0.5秒、0.5秒遅延）

```css
@keyframes heroZoomIn {
  from {
    transform: scale(1.1);
    opacity: 0;
  }
  to {
    transform: scale(1);
    opacity: 1;
  }
}

@keyframes heroFadeInUp {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
```

## 💻 実装内容

### Gensparkマニュアルの該当部分

> **※重要**: `docs/genspark-manual.md` の「⑤トップページヒーロー改善」セクションを参照し、Gensparkの具体的な提案内容をここに転記してください。

---

### 1. Liquidテンプレート実装

`sections/hero-banner.liquid` を編集：

```liquid
{%- comment -%}
  ヒーローバナーセクション
  設定: 画像、見出し、サブ見出し、CTA
{%- endcomment -%}

<div class="hero-section">
  <div class="hero-section__background">
    {%- if section.settings.image -%}
      <img
        srcset="{{ section.settings.image | image_url: width: 375 }} 375w,
                {{ section.settings.image | image_url: width: 750 }} 750w,
                {{ section.settings.image | image_url: width: 1100 }} 1100w,
                {{ section.settings.image | image_url: width: 1500 }} 1500w,
                {{ section.settings.image | image_url: width: 1920 }} 1920w"
        src="{{ section.settings.image | image_url: width: 1500 }}"
        alt="{{ section.settings.image.alt | escape }}"
        class="hero-section__image"
        loading="eager"
        fetchpriority="high"
        width="{{ section.settings.image.width }}"
        height="{{ section.settings.image.height }}"
      >
    {%- else -%}
      {{ 'hero-apparel' | placeholder_svg_tag: 'hero-section__placeholder' }}
    {%- endif -%}
    
    {%- comment -%} グラデーションオーバーレイ {%- endcomment -%}
    <div class="hero-section__overlay"></div>
  </div>

  <div class="hero-section__content container">
    <div class="hero-section__text">
      {%- if section.settings.heading != blank -%}
        <h1 class="hero__heading">
          {{ section.settings.heading }}
        </h1>
      {%- endif -%}

      {%- if section.settings.subheading != blank -%}
        <p class="hero__subheading">
          {{ section.settings.subheading }}
        </p>
      {%- endif -%}

      {%- comment -%} CTAボタン {%- endcomment -%}
      <div class="hero__cta-group">
        {%- if section.settings.button_label_primary != blank -%}
          <a
            href="{{ section.settings.button_link_primary }}"
            class="button button--primary hero__cta-primary"
          >
            {{ section.settings.button_label_primary }}
          </a>
        {%- endif -%}

        {%- if section.settings.button_label_secondary != blank -%}
          <a
            href="{{ section.settings.button_link_secondary }}"
            class="button button--secondary hero__cta-secondary"
          >
            {{ section.settings.button_label_secondary }}
          </a>
        {%- endif -%}
      </div>
    </div>
  </div>

  {%- comment -%} スクロール促進矢印 {%- endcomment -%}
  <div class="hero__scroll-indicator">
    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
    </svg>
  </div>
</div>

{%- comment -%} セクション設定スキーマ {%- endcomment -%}
{% schema %}
{
  "name": "ヒーローバナー",
  "settings": [
    {
      "type": "image_picker",
      "id": "image",
      "label": "背景画像",
      "info": "推奨サイズ: 1920x800px"
    },
    {
      "type": "text",
      "id": "heading",
      "label": "メイン見出し",
      "default": "愛犬に、ハワイの風を"
    },
    {
      "type": "textarea",
      "id": "subheading",
      "label": "サブ見出し",
      "default": "職人が一枚一枚、心を込めて作る<br>わんこ専用アロハシャツ"
    },
    {
      "type": "text",
      "id": "button_label_primary",
      "label": "メインボタンのラベル",
      "default": "商品を見る"
    },
    {
      "type": "url",
      "id": "button_link_primary",
      "label": "メインボタンのリンク"
    },
    {
      "type": "text",
      "id": "button_label_secondary",
      "label": "サブボタンのラベル",
      "default": "こだわりを知る"
    },
    {
      "type": "url",
      "id": "button_link_secondary",
      "label": "サブボタンのリンク"
    }
  ],
  "presets": [
    {
      "name": "ヒーローバナー"
    }
  ]
}
{% endschema %}
```

### 2. CSS実装

`assets/section-hero.css` を新規作成：

```css
/* ヒーローセクション */
.hero-section {
  position: relative;
  width: 100%;
  min-height: 80vh;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
}

/* 背景画像 */
.hero-section__background {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 0;
}

.hero-section__image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  animation: heroZoomIn 1s ease;
}

/* グラデーションオーバーレイ */
.hero-section__overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(
    135deg,
    rgba(255, 107, 107, 0.3) 0%,
    rgba(78, 205, 196, 0.3) 100%
  );
  z-index: 1;
}

/* コンテンツエリア */
.hero-section__content {
  position: relative;
  z-index: 2;
  text-align: center;
  padding: 0 20px;
  max-width: 800px;
  margin: 0 auto;
}

.hero-section__text {
  animation: heroFadeInUp 0.8s ease 0.3s backwards;
}

/* メイン見出し */
.hero__heading {
  font-size: 56px;
  font-weight: 900;
  line-height: 1.2;
  letter-spacing: 0.02em;
  color: #FFFFFF;
  text-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
  margin-bottom: 20px;
}

/* サブ見出し */
.hero__subheading {
  font-size: 20px;
  font-weight: 400;
  line-height: 1.6;
  color: #FFFFFF;
  text-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
  margin-bottom: 32px;
}

/* CTAボタングループ */
.hero__cta-group {
  display: flex;
  gap: 16px;
  justify-content: center;
  flex-wrap: wrap;
  animation: heroFadeInUp 0.8s ease 0.5s backwards;
}

.hero__cta-primary {
  background: linear-gradient(135deg, #FF6B6B 0%, #FF8E8E 100%);
  color: #FFFFFF;
  padding: 18px 40px;
  font-size: 18px;
  font-weight: 700;
  border: none;
  border-radius: 50px;
  box-shadow: 0 4px 15px rgba(255, 107, 107, 0.3);
  transition: all 0.3s ease;
}

.hero__cta-primary:hover {
  background: linear-gradient(135deg, #FF5252 0%, #FF7575 100%);
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(255, 107, 107, 0.4);
}

.hero__cta-secondary {
  background: rgba(255, 255, 255, 0.2);
  backdrop-filter: blur(10px);
  border: 2px solid #FFFFFF;
  color: #FFFFFF;
  padding: 18px 40px;
  font-size: 18px;
  font-weight: 700;
  border-radius: 50px;
  transition: all 0.3s ease;
}

.hero__cta-secondary:hover {
  background: rgba(255, 255, 255, 0.3);
  transform: translateY(-2px);
}

/* スクロール促進矢印 */
.hero__scroll-indicator {
  position: absolute;
  bottom: 32px;
  left: 50%;
  transform: translateX(-50%);
  z-index: 2;
  animation: heroScrollBounce 2s infinite;
}

.hero__scroll-indicator svg {
  width: 32px;
  height: 32px;
  color: #FFFFFF;
  filter: drop-shadow(0 2px 4px rgba(0, 0, 0, 0.3));
}

/* アニメーション */
@keyframes heroZoomIn {
  from {
    transform: scale(1.1);
    opacity: 0;
  }
  to {
    transform: scale(1);
    opacity: 1;
  }
}

@keyframes heroFadeInUp {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes heroScrollBounce {
  0%, 20%, 50%, 80%, 100% {
    transform: translateX(-50%) translateY(0);
  }
  40% {
    transform: translateX(-50%) translateY(-10px);
  }
  60% {
    transform: translateX(-50%) translateY(-5px);
  }
}

/* モバイル対応 */
@media screen and (max-width: 749px) {
  .hero-section {
    min-height: 70vh;
  }
  
  .hero__heading {
    font-size: 32px;
  }
  
  .hero__subheading {
    font-size: 16px;
    margin-bottom: 24px;
  }
  
  .hero__cta-group {
    flex-direction: column;
    gap: 12px;
  }
  
  .hero__cta-primary,
  .hero__cta-secondary {
    width: 100%;
    padding: 16px 32px;
    font-size: 16px;
  }
  
  .hero__scroll-indicator {
    bottom: 20px;
  }
}

/* タブレット対応 */
@media screen and (min-width: 750px) and (max-width: 989px) {
  .hero__heading {
    font-size: 42px;
  }
  
  .hero__subheading {
    font-size: 18px;
  }
}
```

### 3. 画像素材の準備

#### 推奨仕様
- **サイズ**: 1920x800px（アスペクト比 2.4:1）
- **形式**: WebP（フォールバック用にJPG）
- **ファイルサイズ**: 300KB以下を目標
- **内容**: わんこがアロハシャツを着て笑顔の写真
  - 明るい、温かみのある雰囲気
  - わんこの表情がはっきり見える
  - 背景はシンプル（ビーチ、青空など）

#### 画像最適化
```bash
# 画像を最適化してアップロード
# Shopifyが自動でWebPに変換してくれます
```

## ✅ 確認ポイント

### デザイン面
- [ ] 背景画像が美しく表示されるか
- [ ] テキストが読みやすいか（オーバーレイの濃さ）
- [ ] CTAボタンが目立つか
- [ ] ブランドカラーが使われているか
- [ ] アニメーションがスムーズか

### 機能面
- [ ] CTAボタンのリンクが正しいか
- [ ] スクロール矢印が表示されるか
- [ ] 画像の読み込みが速いか（LCP 2.5秒以下）
- [ ] レスポンシブ対応ができているか

### モバイル
- [ ] テキストが小さすぎないか
- [ ] ボタンがタップしやすいサイズか（44x44px以上）
- [ ] 縦画面・横画面どちらでも見やすいか
- [ ] 画像の読み込みが速いか

### パフォーマンス
- [ ] Lighthouse スコア90以上
- [ ] LCP（最大コンテンツの描画）2.5秒以下
- [ ] CLS（レイアウトシフト）0.1以下

## 🧪 テスト手順

### 1. ローカルプレビュー
```bash
shopify theme dev --store alohanui-demo
```

### 2. 管理画面でセクションを設定
1. トップページ（`templates/index.json`）を開く
2. ヒーローバナーセクションを追加
3. 画像をアップロード
4. テキストを入力
5. CTAリンクを設定

### 3. 動作確認
- デスクトップ、タブレット、モバイルで表示確認
- アニメーションの動作確認
- CTAボタンのリンク確認

### 4. パフォーマンステスト
```bash
# Lighthouse でパフォーマンス測定
```

## 📝 実装後のアクション

### 1. 画像素材の準備
- [ ] クライアントに写真を依頼（わんこの笑顔）
- [ ] プロカメラマン撮影を検討
- [ ] 複数パターン用意してA/Bテスト

### 2. コピーの最適化
- [ ] キャッチコピーのA/Bテスト
- [ ] CTAボタンの文言テスト
- [ ] サブコピーの長さ調整

### 3. 効果測定
- [ ] 直帰率の変化
- [ ] スクロール率（どこまでスクロールされたか）
- [ ] CTAクリック率
- [ ] 商品ページへの遷移率

### 4. 季節対応
- [ ] 季節ごとに背景画像を変更
- [ ] セール時期のコピー変更
- [ ] 新商品発売時のCTA変更

## 🚨 注意事項

### やってはいけないこと
- ❌ 重すぎる画像（ページ読み込みが遅くなる）
- ❌ 読みにくいテキスト（背景とのコントラスト不足）
- ❌ 過度なアニメーション（酔ってしまう）
- ❌ 不明瞭なCTA（何をすればいいか分からない）

### 気をつけること
- ⚠️ 画像の著作権・肖像権
- ⚠️ モバイルでのテキストサイズ
- ⚠️ 読み込み速度（Core Web Vitals）
- ⚠️ アクセシビリティ（色のコントラスト、代替テキスト）

## 🔗 関連ドキュメント

- `docs/genspark-manual.md` - 元の改善提案
- `HANDOVER.md` - Phase 1の全体像
- `.cursorrules` - コーディング規約
- `docs/designs/` - 画像素材の管理

## 💡 追加のアイデア

- [ ] 動画背景（わんこが走っている映像）
- [ ] パララックス効果（スクロールで背景が動く）
- [ ] スライダー形式（複数の写真を切り替え）
- [ ] カウントアップアニメーション（「累計〇〇着販売」など）
- [ ] お客様の声をヒーロー下に表示
- [ ] Instagram投稿の埋め込み

---

**作成日**: 2026-02-14  
**実装予定**: Phase 1（1〜2週間以内）  
**ステータス**: 📋 未着手
