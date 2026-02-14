# デザイン素材管理

このフォルダには、プロジェクトで使用するデザイン素材を保存します。

## 📁 フォルダ構成

```
docs/designs/
├── README.md                    # このファイル
├── screenshots/                 # 実装前後のスクリーンショット
│   ├── before/                  # Before画像
│   └── after/                   # After画像
├── wireframes/                  # ワイヤーフレーム
├── mockups/                     # モックアップ
├── assets/                      # 画像素材（アイコン、イラストなど）
│   ├── icons/
│   ├── illustrations/
│   └── photos/
└── brand/                       # ブランドガイドライン関連
    ├── logo/
    └── colors/
```

## 🎨 ブランドカラー

プロジェクトで使用する色は以下の通りです：

### メインカラー

```css
/* コーラル（購入ボタン、重要な要素） */
--color-coral: #FF6B6B;
--color-coral-light: #FF8E8E;
--color-coral-dark: #FF5252;

/* オーシャン（アクセント、リンク） */
--color-ocean: #4ECDC4;
--color-ocean-light: #5FD9D0;
--color-ocean-dark: #44B3AA;

/* ウォームベージュ（背景） */
--color-warm: #FFF4E6;
--color-warm-light: #FFF9F2;
```

### ニュートラルカラー

```css
/* テキスト */
--color-text-primary: #2C3E50;
--color-text-secondary: #555555;
--color-text-light: #999999;

/* 背景・ボーダー */
--color-background: #FFFFFF;
--color-border: #E0E0E0;
--color-border-light: #F0F0F0;
```

### 機能カラー

```css
/* 成功 */
--color-success: #4CAF50;

/* エラー */
--color-error: #F44336;

/* 警告 */
--color-warning: #FFC107;

/* 情報 */
--color-info: #2196F3;
```

## 📐 画像仕様

### 商品写真

#### 必須写真
1. **メイン写真** - 商品全体、正面
   - サイズ: 1000x1000px以上
   - 形式: JPG（Shopifyが自動でWebPに変換）
   - 背景: 白または明るいグレー

2. **詳細写真** - 生地、ボタン、縫製のクローズアップ
   - サイズ: 1000x1000px以上
   - 形式: JPG
   - 背景: 白または商品に合わせて

3. **着用写真** - わんこが実際に着ている写真
   - サイズ: 1000x1000px以上
   - 形式: JPG
   - 背景: 自然光、屋外推奨

#### 推奨写真
4. **サイズ比較** - 複数サイズを並べた写真
5. **コーディネート例** - 季節や用途別の着こなし
6. **制作工程** - 職人が作っている様子

#### 命名規則
```
商品名_角度_サイズ_バージョン.jpg

例:
aloha-shirt-red_front_1000x1000_v1.jpg
aloha-shirt-red_side_1000x1000_v1.jpg
aloha-shirt-red_back_1000x1000_v1.jpg
aloha-shirt-red_detail-fabric_1000x1000_v1.jpg
aloha-shirt-red_wearing-chihuahua_1000x1000_v1.jpg
```

### ヒーローバナー画像

- **サイズ**: 1920x800px（アスペクト比 2.4:1）
- **形式**: JPG（Shopifyが自動でWebPに変換）
- **ファイルサイズ**: 300KB以下を目標
- **内容**: わんこがアロハシャツを着て笑顔の写真
  - 明るい、温かみのある雰囲気
  - わんこの表情がはっきり見える
  - 背景はシンプル（ビーチ、青空など）
  - テキストを重ねることを考慮した構図

#### 命名規則
```
hero-[テーマ]-[サイズ]-[バージョン].jpg

例:
hero-summer-1920x800-v1.jpg
hero-winter-1920x800-v1.jpg
hero-main-1920x800-v2.jpg
```

### アイコン・イラスト

#### サイズガイドイラスト
- **サイズ**: 300x300px
- **形式**: PNG（透過背景）
- **スタイル**: 手描き風、温かみのある線画
- **必要な種類**:
  - `size-guide-neck.png` - 首回りの測り方
  - `size-guide-chest.png` - 胴回りの測り方
  - `size-guide-length.png` - 着丈の測り方

#### アイコン
- **サイズ**: 24x24px、32x32px、48x48px（複数サイズ）
- **形式**: SVG（推奨）またはPNG
- **スタイル**: シンプル、線画または塗りつぶし

## 📸 スクリーンショット管理

### Before/After

実装の効果を視覚的に記録するため、以下のタイミングでスクリーンショットを撮影：

#### 撮影タイミング
- 実装前（Before）
- 実装後（After）
- デスクトップ版
- モバイル版

#### 保存場所
```
docs/designs/screenshots/
├── before/
│   ├── 01-cta-button-desktop.png
│   ├── 01-cta-button-mobile.png
│   ├── 02-photos-desktop.png
│   └── ...
└── after/
    ├── 01-cta-button-desktop.png
    ├── 01-cta-button-mobile.png
    ├── 02-photos-desktop.png
    └── ...
```

#### 命名規則
```
[番号]-[機能名]-[デバイス].png

例:
01-cta-button-desktop.png
01-cta-button-mobile.png
02-photos-desktop.png
03-reviews-mobile.png
```

#### 推奨ツール
- **デスクトップ**: Windows標準スクリーンショット（Win + Shift + S）
- **モバイル**: Chrome DevTools のデバイスモード
- **全画面**: Full Page Screen Capture 拡張機能

## 🖼️ ワイヤーフレーム・モックアップ

### ワイヤーフレーム

簡易的な設計図。レイアウトや要素の配置を決める段階で作成。

#### ツール例
- Figma（推奨）
- Adobe XD
- 手書き → スキャン

#### 保存形式
- PDF（印刷・共有用）
- PNG（ドキュメント埋め込み用）
- Figmaリンク（編集可能な形式）

### モックアップ

実際のデザインに近い見た目の設計図。色、フォント、画像を含む。

#### 命名規則
```
[ページ名]-[セクション]-[バージョン].png

例:
homepage-hero-v1.png
homepage-hero-v2.png
product-page-cta-button-v1.png
```

## 🎯 画像最適化ガイド

### 最適化の重要性
- ページ読み込み速度の向上
- Core Web Vitals の改善
- モバイル体験の向上

### 最適化手順

#### 1. リサイズ
適切なサイズに縮小（不要に大きな画像は使わない）

#### 2. 圧縮
画質を保ちながらファイルサイズを削減

#### 3. 形式変換
- 写真: JPG → WebP（Shopifyが自動変換）
- イラスト/アイコン: PNG → SVG（可能な場合）

### 推奨ツール

#### オンラインツール
- **TinyPNG**: https://tinypng.com/ - PNG/JPG圧縮
- **Squoosh**: https://squoosh.app/ - 高度な画像最適化
- **SVGOMG**: https://jakearchibald.github.io/svgomg/ - SVG最適化

#### デスクトップツール
- Adobe Photoshop
- GIMP（無料）

#### コマンドラインツール（高度）
```bash
# ImageMagick でリサイズ・圧縮
convert input.jpg -resize 1000x1000 -quality 85 output.jpg
```

## 📋 素材チェックリスト

### Phase 1 で必要な素材

#### ①購入ボタン改善
- [ ] なし（CSSのみ）

#### ②商品写真追加
- [ ] 各商品の正面・側面・背面写真
- [ ] わんこが着用している写真（複数アングル）
- [ ] 生地や縫製の詳細写真
- [ ] サイズ比較写真

#### ③レビュー機能導入
- [ ] なし（Judge.meアプリ使用）

#### ④サイズガイド刷新
- [ ] 首回りの測り方イラスト
- [ ] 胴回りの測り方イラスト
- [ ] 着丈の測り方イラスト

#### ⑤トップページヒーロー改善
- [ ] わんこの笑顔写真（1920x800px）
- [ ] 季節別の複数バージョン（任意）

## 🤝 素材の依頼方法

### クライアントへの依頼

#### 依頼テンプレート
```
件名: 【アロハ縫】サイトリニューアル用の写真素材のお願い

アロハ縫茅ヶ崎 ご担当者様

お世話になっております。
Shopifyサイトリニューアルに使用する写真素材についてお願いがございます。

【必要な写真】
1. 商品写真（各商品3〜5枚）
   - 正面、側面、背面
   - 生地のクローズアップ
   - わんこが着用している写真

2. ヒーローバナー用写真（1枚）
   - わんこがアロハシャツを着て笑顔の写真
   - 明るい背景（ビーチ、青空など）

【仕様】
- サイズ: できるだけ大きく（1000px以上）
- 形式: JPG、PNG
- 明るく、ピントが合っている写真

お手数ですが、○月○日までにご提供いただけますと幸いです。

よろしくお願いいたします。
```

## 💡 Tips

### 写真撮影のコツ
1. **自然光を使う** - 明るい時間帯、窓際で撮影
2. **シンプルな背景** - わんこと商品に焦点を当てる
3. **複数枚撮影** - 表情や角度のバリエーション
4. **スマホでもOK** - 最近のスマホカメラは高品質

### 画像選びのポイント
1. **わんこの表情** - 笑顔、楽しそうな様子
2. **商品の見やすさ** - 柄や色が分かりやすい
3. **ストーリー性** - 使用シーンが想像できる
4. **季節感** - ターゲット時期に合った雰囲気

### 著作権・肖像権
- ⚠️ フリー素材の場合、ライセンスを確認
- ⚠️ わんこの飼い主様に掲載許可を取る
- ⚠️ プロカメラマン撮影の場合、使用権を確認

## 🔗 参考リソース

### デザインインスピレーション
- **Dribbble**: https://dribbble.com/ - デザイン事例
- **Behance**: https://www.behance.net/ - ポートフォリオサイト
- **Pinterest**: https://pinterest.com/ - ビジュアル検索

### 画像素材サイト（商用可）
- **Unsplash**: https://unsplash.com/
- **Pexels**: https://www.pexels.com/
- **Pixabay**: https://pixabay.com/

### アイコン素材
- **Heroicons**: https://heroicons.com/ - SVGアイコン（無料）
- **Font Awesome**: https://fontawesome.com/
- **Material Icons**: https://fonts.google.com/icons

## 📝 変更履歴

| 日付 | 変更内容 | 変更者 |
|------|---------|--------|
| 2026-02-14 | 初版作成 | プロジェクトチーム |

---

**作成日**: 2026-02-14  
**最終更新**: 2026-02-14

素材に関するご質問は `docs/implementation-log.md` または `HANDOVER.md` に記録してください。
