# タスク: サイズガイド刷新

## 📋 概要

**Phase**: 1  
**優先度**: 🔴 高  
**予想工数**: 4〜5時間  
**実装者**: 開発チーム

## 🎯 目的

商品ページに分かりやすいサイズガイドを追加し、購入時の不安（サイズ選び）を解消する。

### 改善の狙い
- サイズ選びの不安を解消
- 返品・交換率の低下
- カート放棄率の低下
- 測り方の具体的な説明で自信を持って購入できる

### 期待される効果
- カート放棄率 -30%
- 返品率 -20%
- サイズ問い合わせの減少
- コンバージョン率 +15%

## 📂 対象ファイル

### 編集が必要なファイル
- `sections/main-product.liquid` - サイズガイドの表示位置
- `snippets/size-guide-modal.liquid` - サイズガイドのモーダル
- `assets/component-size-guide.css` - スタイル定義
- `assets/size-guide.js` - モーダルの開閉動作

### 確認が必要なファイル
- `sections/product-recommendations.liquid` - 関連商品との配置バランス

## 🎨 デザイン仕様

### サイズガイドの表示位置

商品ページの構成：
```
1. 商品画像ギャラリー
2. 商品名・価格
3. バリエーション選択（サイズ選択）
   └ 📌 [📏 サイズガイドを見る] ← ここにリンク
4. 購入ボタン
5. 商品説明
6. レビュー
```

### モーダルウィンドウのレイアウト

```
┌────────────────────────────────────────┐
│  📏 サイズガイド              [✕]     │
├────────────────────────────────────────┤
│                                        │
│  🐕 正しい測り方                      │
│  [イラスト付き説明]                    │
│  1. 首回り: 首の付け根を一周測る      │
│  2. 胴回り: 前足の後ろを一周測る      │
│  3. 着丈: 首の付け根から尻尾の前まで  │
│                                        │
│  📐 サイズ表                          │
│  ┌─────┬──────┬──────┬──────┐  │
│  │サイズ│首回り│胴回り│着丈  │  │
│  ├─────┼──────┼──────┼──────┤  │
│  │ SS  │20-24 │28-32 │18-22 │  │
│  │ S   │24-28 │32-38 │22-26 │  │
│  │ M   │28-32 │38-45 │26-30 │  │
│  │ L   │32-36 │45-52 │30-34 │  │
│  │ LL  │36-40 │52-60 │34-38 │  │
│  └─────┴──────┴──────┴──────┘  │
│                                        │
│  💡 サイズ選びのコツ                  │
│  • ゆったり着せたい場合は1サイズ上   │
│  • 測定値が2サイズにまたがる場合は   │
│    大きい方を選択                      │
│                                        │
│  ❓ サイズでお困りですか？            │
│  [お問い合わせ]                        │
│                                        │
└────────────────────────────────────────┘
```

### イラスト素材

#### 測り方イラスト（3種類必要）
1. **首回りの測り方**
   - わんこの首の付け根にメジャーを当てている図
   - 「ここを測ります」の矢印付き

2. **胴回りの測り方**
   - 前足の後ろ、胸の一番太い部分
   - 「ゆとりを持たせて測ります」の注釈

3. **着丈の測り方**
   - 首の付け根から尻尾の付け根まで
   - 背骨に沿って測る図

#### 推奨イラストスタイル
- 温かみのある手描き風
- 分かりやすいシンプルな線画
- ブランドカラー（コーラル・オーシャン）を使用

### スタイル指定

```css
/* サイズガイドリンク */
.size-guide-link {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  color: #4ECDC4;
  font-size: 14px;
  font-weight: 600;
  text-decoration: underline;
  cursor: pointer;
  margin-top: 8px;
  transition: color 0.3s;
}

.size-guide-link:hover {
  color: #44B3AA;
}

.size-guide-link svg {
  width: 16px;
  height: 16px;
}

/* モーダルオーバーレイ */
.size-guide-modal {
  display: none;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  z-index: 999;
  overflow-y: auto;
}

.size-guide-modal--active {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20px;
}

/* モーダルコンテンツ */
.size-guide-modal__content {
  background: #FFFFFF;
  border-radius: 16px;
  max-width: 700px;
  width: 100%;
  max-height: 90vh;
  overflow-y: auto;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.2);
  animation: modalSlideIn 0.3s ease;
}

@keyframes modalSlideIn {
  from {
    opacity: 0;
    transform: translateY(-20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* モーダルヘッダー */
.size-guide-modal__header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 24px;
  border-bottom: 1px solid #E0E0E0;
}

.size-guide-modal__title {
  font-size: 24px;
  font-weight: 700;
  color: #2C3E50;
}

.size-guide-modal__close {
  background: none;
  border: none;
  font-size: 32px;
  color: #999999;
  cursor: pointer;
  padding: 0;
  width: 32px;
  height: 32px;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: color 0.3s;
}

.size-guide-modal__close:hover {
  color: #333333;
}

/* モーダルボディ */
.size-guide-modal__body {
  padding: 24px;
}

/* 測り方セクション */
.size-guide-section {
  margin-bottom: 32px;
}

.size-guide-section__title {
  font-size: 18px;
  font-weight: 700;
  color: #2C3E50;
  margin-bottom: 16px;
  display: flex;
  align-items: center;
  gap: 8px;
}

.size-guide-section__title svg {
  width: 24px;
  height: 24px;
  color: #FF6B6B;
}

/* 測り方イラスト */
.size-guide-measurements {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 16px;
  margin-bottom: 24px;
}

.measurement-item {
  text-align: center;
  padding: 16px;
  background: #F8F8F8;
  border-radius: 12px;
}

.measurement-item__image {
  width: 100%;
  max-width: 150px;
  margin: 0 auto 12px;
}

.measurement-item__label {
  font-weight: 700;
  color: #2C3E50;
  margin-bottom: 4px;
}

.measurement-item__description {
  font-size: 14px;
  color: #666666;
}

/* サイズ表 */
.size-guide-table {
  width: 100%;
  border-collapse: collapse;
  margin: 16px 0;
  font-size: 14px;
}

.size-guide-table th {
  background: #FF6B6B;
  color: #FFFFFF;
  padding: 12px;
  text-align: left;
  font-weight: 700;
}

.size-guide-table td {
  padding: 12px;
  border-bottom: 1px solid #E0E0E0;
}

.size-guide-table tr:hover {
  background: #FFF4E6;
}

.size-guide-table__size {
  font-weight: 700;
  color: #2C3E50;
}

/* ヒントセクション */
.size-guide-tips {
  background: #E8F9F8;
  padding: 16px;
  border-radius: 12px;
  border-left: 4px solid #4ECDC4;
}

.size-guide-tips__title {
  font-weight: 700;
  color: #2C3E50;
  margin-bottom: 8px;
}

.size-guide-tips ul {
  margin: 0;
  padding-left: 20px;
}

.size-guide-tips li {
  margin-bottom: 8px;
  color: #555555;
}

/* モバイル対応 */
@media screen and (max-width: 749px) {
  .size-guide-modal__content {
    max-height: 100vh;
    border-radius: 16px 16px 0 0;
  }
  
  .size-guide-measurements {
    grid-template-columns: 1fr;
  }
  
  .size-guide-table {
    font-size: 12px;
  }
  
  .size-guide-table th,
  .size-guide-table td {
    padding: 8px;
  }
}
```

## 💻 実装内容

### Gensparkマニュアルの該当部分

> **※重要**: `docs/genspark-manual.md` の「④サイズガイド刷新」セクションを参照し、Gensparkの具体的な提案内容をここに転記してください。

---

### 1. サイズガイドリンクの追加

`sections/main-product.liquid` のサイズ選択の近くに追加：

```liquid
{%- comment -%} バリエーション選択エリア {%- endcomment -%}
<div class="product-form__input product-form__input--variant">
  <label for="product-select-{{ section.id }}">サイズ</label>
  <select id="product-select-{{ section.id }}" name="id">
    {%- for variant in product.variants -%}
      <option value="{{ variant.id }}">{{ variant.title }}</option>
    {%- endfor -%}
  </select>
  
  {%- comment -%} サイズガイドリンク {%- endcomment -%}
  <button
    type="button"
    class="size-guide-link"
    data-size-guide-trigger
    aria-label="サイズガイドを開く"
  >
    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M7 21h10a2 2 0 002-2V9.414a1 1 0 00-.293-.707l-5.414-5.414A1 1 0 0012.586 3H7a2 2 0 00-2 2v14a2 2 0 002 2z" />
    </svg>
    📏 サイズガイドを見る
  </button>
</div>
```

### 2. モーダルスニペットの作成

`snippets/size-guide-modal.liquid` を新規作成：

```liquid
{%- comment -%}
  サイズガイドモーダル
  使い方: {% render 'size-guide-modal' %}
{%- endcomment -%}

<div class="size-guide-modal" data-size-guide-modal>
  <div class="size-guide-modal__content">
    {%- comment -%} ヘッダー {%- endcomment -%}
    <div class="size-guide-modal__header">
      <h2 class="size-guide-modal__title">📏 サイズガイド</h2>
      <button
        class="size-guide-modal__close"
        data-size-guide-close
        aria-label="閉じる"
      >
        ×
      </button>
    </div>

    {%- comment -%} ボディ {%- endcomment -%}
    <div class="size-guide-modal__body">
      {%- comment -%} 測り方セクション {%- endcomment -%}
      <section class="size-guide-section">
        <h3 class="size-guide-section__title">
          <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
          </svg>
          🐕 正しい測り方
        </h3>
        
        <div class="size-guide-measurements">
          <div class="measurement-item">
            <img
              src="{{ 'size-guide-neck.png' | asset_url }}"
              alt="首回りの測り方"
              class="measurement-item__image"
              loading="lazy"
            >
            <div class="measurement-item__label">1. 首回り</div>
            <div class="measurement-item__description">
              首の付け根を一周測ります。<br>
              指2本分のゆとりを持たせてください。
            </div>
          </div>

          <div class="measurement-item">
            <img
              src="{{ 'size-guide-chest.png' | asset_url }}"
              alt="胴回りの測り方"
              class="measurement-item__image"
              loading="lazy"
            >
            <div class="measurement-item__label">2. 胴回り</div>
            <div class="measurement-item__description">
              前足の後ろ、胸の一番太い部分を一周測ります。
            </div>
          </div>

          <div class="measurement-item">
            <img
              src="{{ 'size-guide-length.png' | asset_url }}"
              alt="着丈の測り方"
              class="measurement-item__image"
              loading="lazy"
            >
            <div class="measurement-item__label">3. 着丈</div>
            <div class="measurement-item__description">
              首の付け根から尻尾の付け根まで、<br>
              背骨に沿って測ります。
            </div>
          </div>
        </div>
      </section>

      {%- comment -%} サイズ表 {%- endcomment -%}
      <section class="size-guide-section">
        <h3 class="size-guide-section__title">📐 サイズ表（単位：cm）</h3>
        
        <table class="size-guide-table">
          <thead>
            <tr>
              <th>サイズ</th>
              <th>首回り</th>
              <th>胴回り</th>
              <th>着丈</th>
              <th>参考犬種</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td class="size-guide-table__size">SS</td>
              <td>20-24</td>
              <td>28-32</td>
              <td>18-22</td>
              <td>チワワ、ヨーキー</td>
            </tr>
            <tr>
              <td class="size-guide-table__size">S</td>
              <td>24-28</td>
              <td>32-38</td>
              <td>22-26</td>
              <td>トイプードル、ポメラニアン</td>
            </tr>
            <tr>
              <td class="size-guide-table__size">M</td>
              <td>28-32</td>
              <td>38-45</td>
              <td>26-30</td>
              <td>ミニチュアダックス、シーズー</td>
            </tr>
            <tr>
              <td class="size-guide-table__size">L</td>
              <td>32-36</td>
              <td>45-52</td>
              <td>30-34</td>
              <td>柴犬、コーギー</td>
            </tr>
            <tr>
              <td class="size-guide-table__size">LL</td>
              <td>36-40</td>
              <td>52-60</td>
              <td>34-38</td>
              <td>ボーダーコリー、柴犬(大)</td>
            </tr>
          </tbody>
        </table>
      </section>

      {%- comment -%} ヒントセクション {%- endcomment -%}
      <section class="size-guide-section">
        <div class="size-guide-tips">
          <div class="size-guide-tips__title">💡 サイズ選びのコツ</div>
          <ul>
            <li>ゆったり着せたい場合は、1サイズ上をお選びください</li>
            <li>測定値が2サイズにまたがる場合は、大きい方がおすすめです</li>
            <li>伸縮性のある生地なので、少し小さめでもフィットします</li>
            <li>初めてお買い求めの方は、お気軽にお問い合わせください</li>
          </ul>
        </div>
      </section>

      {%- comment -%} お問い合わせボタン {%- endcomment -%}
      <section class="size-guide-section">
        <h3 class="size-guide-section__title">❓ サイズでお困りですか？</h3>
        <p style="margin-bottom: 12px; color: #666;">
          わんちゃんのサイズに不安がある方は、お気軽にお問い合わせください。<br>
          測定値をお知らせいただければ、最適なサイズをご提案いたします。
        </p>
        <a href="/pages/contact" class="button button--secondary">
          お問い合わせ
        </a>
      </section>
    </div>
  </div>
</div>
```

### 3. JavaScript実装

`assets/size-guide.js` を新規作成：

```javascript
// サイズガイドモーダルの開閉
document.addEventListener('DOMContentLoaded', () => {
  const triggers = document.querySelectorAll('[data-size-guide-trigger]');
  const modal = document.querySelector('[data-size-guide-modal]');
  const closeBtn = document.querySelector('[data-size-guide-close]');

  if (!modal) return;

  // モーダルを開く
  triggers.forEach(trigger => {
    trigger.addEventListener('click', () => {
      modal.classList.add('size-guide-modal--active');
      document.body.style.overflow = 'hidden'; // スクロール無効化
    });
  });

  // モーダルを閉じる
  const closeModal = () => {
    modal.classList.remove('size-guide-modal--active');
    document.body.style.overflow = ''; // スクロール有効化
  };

  closeBtn.addEventListener('click', closeModal);

  // オーバーレイクリックで閉じる
  modal.addEventListener('click', (e) => {
    if (e.target === modal) {
      closeModal();
    }
  });

  // ESCキーで閉じる
  document.addEventListener('keydown', (e) => {
    if (e.key === 'Escape' && modal.classList.contains('size-guide-modal--active')) {
      closeModal();
    }
  });
});
```

### 4. イラスト素材の準備

以下の画像を `assets/` フォルダにアップロード：
- `size-guide-neck.png` - 首回りの測り方
- `size-guide-chest.png` - 胴回りの測り方
- `size-guide-length.png` - 着丈の測り方

**推奨サイズ**: 300x300px、透過PNG

## ✅ 確認ポイント

### 機能面
- [ ] 「サイズガイドを見る」リンクが表示されるか
- [ ] リンクをクリックするとモーダルが開くか
- [ ] ×ボタンでモーダルが閉じるか
- [ ] オーバーレイクリックで閉じるか
- [ ] ESCキーで閉じるか
- [ ] モーダル表示中は背景がスクロールしないか

### デザイン面
- [ ] イラストが分かりやすいか
- [ ] サイズ表が読みやすいか
- [ ] ブランドカラーが使われているか
- [ ] モバイルでも見やすいか

### 内容
- [ ] サイズ表が正確か（実際の商品と一致）
- [ ] 測り方の説明が分かりやすいか
- [ ] 参考犬種が適切か
- [ ] ヒントが役立つか

### アクセシビリティ
- [ ] キーボードで操作できるか
- [ ] スクリーンリーダーで読み上げられるか
- [ ] aria属性が適切に設定されているか

## 🧪 テスト手順

### 1. ローカルプレビュー
```bash
shopify theme dev --store alohanui-demo
```

### 2. 動作確認
1. 商品ページにアクセス
2. サイズ選択エリアの「サイズガイドを見る」をクリック
3. モーダルが開くことを確認
4. 各セクションの表示を確認
5. 閉じるボタン、ESCキー、オーバーレイクリックで閉じることを確認

### 3. モバイル確認
- iOS Safari、Android Chrome
- モーダルがスクロールできるか
- 表が横スクロールせず見やすいか

## 📝 実装後のアクション

### 1. イラスト素材の作成依頼
- [ ] デザイナーorクライアントに測り方イラストを依頼
- [ ] 温かみのあるイラストスタイルを指定
- [ ] 実際のわんこの写真を参考に

### 2. サイズ表の正確性確認
- [ ] 実際の商品のサイズを測定
- [ ] サイズ表と一致するか確認
- [ ] 必要に応じて調整

### 3. ドキュメント更新
- `docs/implementation-log.md` に記録
- スクリーンショット保存

### 4. 効果測定
- [ ] サイズに関する問い合わせ件数
- [ ] 返品・交換の理由（サイズ間違い）
- [ ] カート放棄率

## 🚨 注意事項

### やってはいけないこと
- ❌ 不正確なサイズ表
- ❌ 分かりにくいイラスト
- ❌ モーダルが開かない・閉じられない
- ❌ モバイルで見づらい表

### 気をつけること
- ⚠️ サイズ表は実測値に基づくこと
- ⚠️ イラストの著作権
- ⚠️ モーダルのパフォーマンス（アニメーション）
- ⚠️ Z-indexの管理

## 🔗 関連ドキュメント

- `docs/genspark-manual.md` - 元の改善提案
- `HANDOVER.md` - Phase 1の全体像
- `.cursorrules` - コーディング規約

## 💡 追加のアイデア

- [ ] AIサイズ推奨機能（質問に答えると最適サイズを提案）
- [ ] 動画での測り方ガイド
- [ ] サイズ交換無料キャンペーン
- [ ] オーダーメイド対応（サイズオーダー）
- [ ] サイズ比較機能（2サイズを並べて表示）

---

**作成日**: 2026-02-14  
**実装予定**: Phase 1（1〜2週間以内）  
**ステータス**: 📋 未着手
