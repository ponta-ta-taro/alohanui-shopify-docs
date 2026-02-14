# セットアップログ

このドキュメントは、プロジェクトの環境構築手順と記録を保存します。

## 📅 セットアップ実施日

**2026-02-14**

---

## ✅ セットアップチェックリスト

### 前提環境

- [x] Windows 11 (10.0.26100)
- [x] PowerShell
- [x] インターネット接続

### 必須ツールのインストール

#### Node.js & npm
- [x] Node.js v22.20.0 インストール済み
- [x] npm 10.9.3 インストール済み

**確認方法**:
```powershell
node --version
# v22.20.0

npm --version
# 10.9.3
```

#### Shopify CLI
- [x] Shopify CLI 3.90.1 インストール済み

**確認方法**:
```powershell
shopify version
# 3.90.1
```

**インストール方法（参考）**:
```powershell
npm install -g @shopify/cli @shopify/theme
```

### Shopifyアカウント

#### パートナーアカウント
- [x] Shopifyパートナー登録完了
- **アカウント**: ponta10sakura@gmail.com
- **ダッシュボード**: https://partners.shopify.com/

#### 開発ストア
- [x] alohanui-demo 作成完了
- **URL**: alohanui-demo.myshopify.com
- **種別**: 無料開発ストア
- **用途**: メイン開発環境

#### テストストア
- [x] テストショップ（bekffc-wz）作成完了
- **URL**: bekffc-wz.myshopify.com
- **種別**: 有料ストア（月150円）
- **用途**: 有料機能のテスト

### プロジェクトディレクトリ

- [x] プロジェクトフォルダ作成
- **パス**: `C:\projects\alohanui-demo`

```powershell
# ディレクトリ作成
mkdir C:\projects\alohanui-demo
cd C:\projects\alohanui-demo
```

### ドキュメント整備

- [x] HANDOVER.md 作成
- [x] PROJECT_CONTEXT.md 作成
- [x] .cursorrules 作成
- [x] README.md 作成
- [x] docs/ フォルダ構造作成
- [x] docs/genspark-manual.md 作成
- [x] docs/implementation-log.md 作成
- [x] docs/setup-log.md 作成
- [x] docs/decisions.md 作成
- [x] docs/prompts/ 作成
- [x] docs/designs/ 作成

---

## 🔧 詳細セットアップ手順

### 1. Node.js インストール

1. https://nodejs.org/ から LTS版をダウンロード
2. インストーラーを実行
3. デフォルト設定でインストール
4. PowerShellを再起動
5. バージョン確認

### 2. Shopify CLI インストール

```powershell
# グローバルインストール
npm install -g @shopify/cli @shopify/theme

# バージョン確認
shopify version
```

### 3. Shopifyアカウント認証

```powershell
# 初回ログイン
shopify auth login

# ブラウザが開くので、パートナーアカウントでログイン
# ponta10sakura@gmail.com
```

### 4. 開発ストアの作成

パートナーダッシュボードから：
1. 「ストア」→「ストアを追加」
2. 「開発ストア」を選択
3. ストア名: alohanui-demo
4. 作成完了

### 5. テーマのローカルセットアップ（次回実施予定）

```powershell
cd C:\projects\alohanui-demo

# 既存テーマをpull（次回実施）
shopify theme pull --store alohanui-demo

# または新規テーマを作成
shopify theme init
```

---

## 🌐 環境情報まとめ

### ローカル環境

| 項目 | 値 |
|-----|-----|
| OS | Windows 11 (10.0.26100) |
| シェル | PowerShell |
| プロジェクトパス | C:\projects\alohanui-demo |
| Node.js | v22.20.0 |
| npm | 10.9.3 |
| Shopify CLI | 3.90.1 |

### Shopify環境

| 種別 | ストア名 | URL | 用途 |
|-----|---------|-----|------|
| 本番 | アロハ縫茅ヶ崎 | https://alohanui.jp/ | 本番環境（触らない） |
| 開発 | alohanui-demo | alohanui-demo.myshopify.com | メイン開発 |
| テスト | テストショップ | bekffc-wz.myshopify.com | 有料機能テスト |

---

## ⚙️ 環境変数（必要に応じて）

現時点では特に設定不要。将来的にAPI連携が必要になった場合は以下を検討：

```powershell
# 環境変数の設定例（将来用）
# $env:SHOPIFY_API_KEY = "your-api-key"
# $env:SHOPIFY_API_SECRET = "your-api-secret"
```

---

## 🔄 日常的なコマンド

### 開発サーバー起動
```powershell
cd C:\projects\alohanui-demo
shopify theme dev --store alohanui-demo
```

### テーマの同期
```powershell
# リモート→ローカル（最新を取得）
shopify theme pull --store alohanui-demo

# ローカル→リモート（変更を反映）
shopify theme push --store alohanui-demo
```

### ストア情報確認
```powershell
shopify theme info
```

---

## 🐛 トラブルシューティング

### Shopify CLI が認識されない

**症状**: `shopify: command not found`

**対処法**:
```powershell
# グローバルパスの確認
npm config get prefix

# 再インストール
npm install -g @shopify/cli @shopify/theme

# PowerShell再起動
```

### ログインできない

**症状**: 認証エラー

**対処法**:
```powershell
# ログアウト
shopify auth logout

# 再ログイン
shopify auth login
```

### テーマのpullができない

**症状**: ストアにアクセスできない

**対処法**:
1. ストア名が正しいか確認（alohanui-demo）
2. パートナーアカウントで該当ストアにアクセス権があるか確認
3. 開発ストアが有効か確認（無料開発ストアは90日で無効化される場合あり）

### ポートが使用中

**症状**: `Port 9292 is already in use`

**対処法**:
```powershell
# 別のポートを指定
shopify theme dev --port 9293
```

---

## 📝 セットアップ完了後の確認事項

- [x] Shopify CLI でログインできる
- [x] 開発ストアの管理画面にアクセスできる
- [ ] ローカルでテーマのプレビューができる（次回実施）
- [x] プロジェクトドキュメントが整備されている

---

## 🎯 次のステップ

### 今すぐやること
1. [ ] Gensparkマニュアルの内容を `docs/genspark-manual.md` に転記
2. [ ] 開発ストアのテーマをローカルにpull
3. [ ] 開発サーバーを起動してプレビュー確認

### コマンド
```powershell
cd C:\projects\alohanui-demo
shopify theme pull --store alohanui-demo
shopify theme dev
```

---

## 📚 参考資料

- **Shopify CLI ドキュメント**: https://shopify.dev/docs/themes/tools/cli
- **Shopify テーマ開発ガイド**: https://shopify.dev/docs/themes
- **Node.js 公式**: https://nodejs.org/
- **Shopify パートナープログラム**: https://partners.shopify.com/

---

**作成日**: 2026-02-14  
**最終更新**: 2026-02-14  
**次回更新予定**: テーマのローカルセットアップ完了時
