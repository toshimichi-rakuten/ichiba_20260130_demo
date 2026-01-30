# Rakuten Design System - Component Reference for AI

このドキュメントは、楽天市場デザインシステムのHTMLコンポーネントを組み合わせて新規ページを作成する際に、AIが参照するためのガイドです。

## プロジェクト概要

- **プロジェクト名**: Rakuten Design System (Rakuma)
- **技術スタック**: 静的HTML、ECM (楽天共通フレームワーク) 3.28
- **目的**: 再利用可能なHTMLコンポーネントを組み合わせてキャンペーンページや商品ページを構築

## ECMフレームワーク

全てのページで以下のECMリソースを読み込む必要があります：

```html
<!-- ECM グローバルCSS -->
<link rel="stylesheet" href="https://r.r10s.jp/com/js/c/ecm/3.28/ecm-3.28.0.min.css">

<!-- ECM グローバルJS -->
<script src="https://r.r10s.jp/com/js/c/ecm/3.28/ecm-3.28.0.min.js"></script>
```

## デザイントークン

プロジェクト全体で使用する共通のCSS変数：

```css
:root {
  --white: #FFF;
  --crimson: #BF0000;
  --crimson-light: #d60000;
  --gray-900: #1a1a1a;
  --gray-700: #4a4a4a;
  --gray-500: #717171;
  --gray-300: #e5e5e5;
  --gray-100: #f5f5f5;
  --border-color: #D1D1D1;
  --shadow-sm: 0 1px 2px rgba(0, 0, 0, 0.05);
  --shadow-md: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
  --shadow-lg: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
  --radius-sm: 6px;
  --radius-md: 8px;
  --radius-lg: 12px;
}
```

## 利用可能なコンポーネント

### 1. 共通ヘッダー (`components/header.html`)

**用途**: 全ページの最上部に配置するグローバルヘッダー

**機能**:
- 楽天ロゴ
- 検索バー（商品検索機能）
- ユーザーアクションボタン（買い物かご、お知らせ、閲覧履歴、お気に入り、購入履歴、クーポン）
- ポイント表示エリア（会員情報、ポイント残高、倍率表示）

**主要クラス**:
- `.rakuten-header` - ヘッダーコンテナ
- `.search-bar` - 検索バー
- `.icon-button` - アイコンボタン
- `.badge` - 通知バッジ
- `.point-area` - ポイント表示エリア

**使用方法**:
```html
<!-- ページの<body>直後に配置 -->
<div class="rakuten-header">
  <!-- ヘッダーの内容をcomponents/header.htmlからコピー -->
</div>
```

**レスポンシブ対応**: 768px以下でモバイル最適化

---

### 2. エントリーボタン (`components/entry-button.html`)

**用途**: キャンペーン参加や特典エントリー用のアクションボタン

**機能**:
- キャンペーンへのエントリー機能
- メルマガ購読オプション（チェックボックス付き）
- ECMのJavaScriptコンポーネント（`rcEntryButton`）を使用

**必須リソース**:
```html
<script defer="defer" src="https://r.r10s.jp/com/js/c/ecm/1.1/entry_button-1.1.0.min.js"></script>
```

**使用方法**:
```html
<div
  class="rcEntryButton"
  layout="pc"
  settings='{
    "campaignCode": "/ic/your-campaign-code",
    "checkboxLabel": "<strong>エントリーしてメルマガを購読する</strong>",
    "checkboxText": "メルマガの説明文をここに記載",
    "ekey": "your-ekey-value"
  }'
></div>
```

**カスタマイズパラメータ**:
- `campaignCode`: キャンペーン識別コード
- `checkboxLabel`: チェックボックスのラベル
- `checkboxText`: メルマガ購読の詳細説明
- `ekey`: エントリーキー
- `layout`: "pc" または "sp"（モバイル）

---

### 3. 共通フッター (`components/footer.html`)

**用途**: 全ページの最下部に配置するグローバルフッター

**機能**:
- タブナビゲーション（特集・サービス、ジャンル）
- カテゴリー一覧（ファッション、グルメ、家電など）
- サービス紹介セクション（セキュリティ、安心、アクセシビリティ）
- リンク集（会員情報、楽天市場トップ、ランキングなど）
- 法的情報とコピーライト

**主要クラス**:
- `.rakuten-footer` - フッターコンテナ
- `.footer-tabs` - タブナビゲーション
- `.categories-grid` - カテゴリーグリッド（5列レイアウト）
- `.features-section` - サービス紹介セクション（3列レイアウト）
- `.links-section` - リンク集
- `.footer-bottom` - 下部エリア（ロゴ、コピーライト）

**使用方法**:
```html
<!-- ページの最下部、</body>の直前に配置 -->
<footer class="rakuten-footer">
  <!-- フッターの内容をcomponents/footer.htmlからコピー -->
</footer>
```

**レスポンシブ対応**: 
- 1024px以下: カテゴリー3列、リンク2列
- 768px以下: カテゴリー2列、縦並び最適化

---

### 4. キャンペーン詳細 (`components/campaign-detail.html`)

**用途**: キャンペーンのルール、期間、条件などの詳細情報を表示

**機能**:
- ページヘッダー（ステップインジケーター付き）
- キャンペーンタイトル入力フィールド
- ルール項目表示（2カラムレイアウト：ラベル + コンテンツ）
- タグ選択機能
- 注意事項セクション

**主要クラス**:
- `.campaign-detail` - コンテナ
- `.page-header` - ページヘッダー
- `.campaign-title-section` - タイトルセクション
- `.rules-section` - ルール一覧
- `.rule-item` - 個別ルール項目（グリッドレイアウト：180px + 1fr）
- `.tag-list` - タグリスト
- `.notes-section` - 注意事項エリア

**使用方法**:
```html
<div class="campaign-detail">
  <div class="page-header">
    <div class="page-header-icon">①</div>
    <h1 class="page-header-title">キャンペーンルール詳細</h1>
  </div>
  
  <div class="campaign-content">
    <!-- ルール項目 -->
    <div class="rules-section">
      <div class="rule-item">
        <div class="rule-label">項目タイトル</div>
        <div class="rule-content">
          <div class="rule-text">説明文</div>
        </div>
      </div>
    </div>
  </div>
</div>
```

**レスポンシブ対応**: 768px以下で1カラムレイアウトに切り替え

---

### 5. クーポンカード (`components/coupon-card.html`)

**用途**: 割引クーポンの表示と獲得機能

**機能**:
- クーポン金額表示（強調表示）
- 利用条件の表示
- 獲得ボタン
- 残数表示（先着〇〇回まで）
- ECMのクーポンスタイル（`.ecm-coupon`）を使用

**主要クラス**:
- `.ecm-coupon` - クーポンカードコンテナ
- `.ecm-coupon-body` - カード本体
- `.ecm-coupon-discount` - 割引額表示
- `.ecm-coupon-title` - 利用条件
- `.ecm-coupon-text` - 獲得ボタンテキスト
- `.ecm-coupon-note` - 注釈（残数など）

**使用方法**:
```html
<div class="ecm-coupon">
  <div class="ecm-coupon-body">
    <a class="ecm-coupon-link" href="#">
      <span class="ecm-coupon-discount"><em>500</em>円OFF</span>
      <span class="ecm-coupon-title">30,000円(税込)以上のご購入で利用可</span>
      <div class="ecm-coupon-text">
        <i class="ecm-icon-coupon-filled" aria-hidden="true"></i>
        クーポンを獲得する
      </div>
    </a>
  </div>
  <div class="ecm-coupon-note">※先着15,000回まで</div>
</div>
```

**レイアウト推奨**: グリッドレイアウトで複数配置（`grid-template-columns: repeat(auto-fit, minmax(320px, 1fr))`）

---

## ページ構造のベストプラクティス

### 基本的なページテンプレート

```html
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>ページタイトル - 楽天市場</title>

  <!-- ECM グローバルCSS -->
  <link rel="stylesheet" href="https://r.r10s.jp/com/js/c/ecm/3.28/ecm-3.28.0.min.css">

  <!-- ECM グローバルJS -->
  <script src="https://r.r10s.jp/com/js/c/ecm/3.28/ecm-3.28.0.min.js"></script>

  <!-- 必要に応じて追加のスクリプト -->
  <!-- エントリーボタンを使用する場合 -->
  <!-- <script defer="defer" src="https://r.r10s.jp/com/js/c/common/entry_button/1.1/entry_button-1.1.0.min.js"></script> -->

  <style>
    /* ページ固有のスタイル */
    :root {
      /* デザイントークン */
    }
    
    body {
      font-family: "Hiragino Kaku Gothic ProN", "Hiragino Sans", Meiryo, -apple-system, Roboto, Helvetica, sans-serif;
      background: #f5f5f5;
      margin: 0;
      padding: 0;
    }
    
    /* その他のスタイル */
  </style>
</head>
<body>

  <!-- 1. ヘッダー（グローバルナビゲーション） -->
  <div class="rakuten-header">
    <!-- components/header.htmlの内容 -->
  </div>

  <!-- 2. メインコンテンツ -->
  <main>
    <!-- ページ固有のコンテンツ -->
    <!-- コンポーネントを組み合わせる -->
  </main>

  <!-- 3. フッター（グローバルフッター） -->
  <footer class="rakuten-footer">
    <!-- components/footer.htmlの内容 -->
  </footer>

</body>
</html>
```

### キャンペーンページの例

```html
<!DOCTYPE html>
<html lang="ja">
<head>
  <!-- head要素は上記と同様 -->
  <script defer="defer" src="https://r.r10s.jp/com/js/c/common/entry_button/1.1/entry_button-1.1.0.min.js"></script>
</head>
<body>

  <!-- ヘッダー -->
  <div class="rakuten-header">...</div>

  <!-- メインコンテンツ -->
  <main>
    <!-- キャンペーンバナーエリア -->
    <section class="campaign-hero">
      <h1>キャンペーンタイトル</h1>
      <p>キャンペーン概要</p>
    </section>

    <!-- エントリーボタン -->
    <section class="entry-section">
      <div class="rcEntryButton" layout="pc" settings='{...}'></div>
    </section>

    <!-- クーポン一覧 -->
    <section class="coupon-section">
      <h2>お得なクーポン</h2>
      <div class="coupon-grid">
        <div class="ecm-coupon">...</div>
        <div class="ecm-coupon">...</div>
        <div class="ecm-coupon">...</div>
      </div>
    </section>

    <!-- キャンペーン詳細 -->
    <section>
      <div class="campaign-detail">...</div>
    </section>
  </main>

  <!-- フッター -->
  <footer class="rakuten-footer">...</footer>

</body>
</html>
```

## レスポンシブデザインガイドライン

### ブレークポイント

- **デスクトップ**: 1024px以上
- **タブレット**: 768px - 1023px
- **モバイル**: 767px以下

### メディアクエリの推奨記述

```css
/* タブレット */
@media (max-width: 1024px) {
  /* タブレット用のスタイル */
}

/* モバイル */
@media (max-width: 768px) {
  /* モバイル用のスタイル */
}
```

### レスポンシブグリッドレイアウト

```css
.grid-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 24px;
}

@media (max-width: 768px) {
  .grid-container {
    grid-template-columns: 1fr;
    gap: 16px;
  }
}
```

## スタイリング規約

### クラス命名規則

- **BEM風**: `.block__element--modifier`（ECMに準拠）
- **セマンティック**: 意味のある名前を使用（`.campaign-hero`, `.coupon-section`）
- **プレフィックス**: ECMコンポーネントは `.ecm-` プレフィックス、楽天共通は `.rakuten-` プレフィックス

### カラー使用ガイドライン

- **プライマリー**: `var(--crimson)` (#BF0000) - アクションボタン、強調要素
- **テキスト**: `var(--gray-900)` - メインテキスト
- **サブテキスト**: `var(--gray-500)` - 補足情報
- **ボーダー**: `var(--gray-300)` または `var(--border-color)`
- **背景**: `var(--gray-100)` または `var(--white)`

### タイポグラフィ

```css
/* 見出し */
h1 { font-size: 32px; font-weight: 700; }
h2 { font-size: 24px; font-weight: 700; }
h3 { font-size: 18px; font-weight: 700; }

/* 本文 */
body { font-size: 14px; line-height: 1.6; }
.small-text { font-size: 12px; }
.caption { font-size: 11px; }
```

## アクセシビリティ

- セマンティックHTMLを使用（`<header>`, `<main>`, `<footer>`, `<section>`, `<nav>`）
- 画像には`alt`属性を必ず付与
- フォームには適切な`<label>`を使用
- キーボードナビゲーションを考慮（`tabindex`、フォーカススタイル）
- ARIA属性の適切な使用（`aria-label`, `aria-hidden`など）

## パフォーマンス最適化

- ECMのCDNリソースを活用（キャッシュ効率）
- 画像の遅延読み込み（`loading="lazy"`）
- CSSは`<head>`内、JavaScriptは`<body>`終了タグ直前または`defer`属性使用
- 不要なスタイルの削除

## コンポーネントの組み合わせ例

### 商品ランディングページ

1. **ヘッダー** - 共通ヘッダー
2. **ヒーローセクション** - 商品画像とキャッチコピー
3. **クーポンセクション** - クーポンカード × 3-6個
4. **エントリーセクション** - エントリーボタン
5. **詳細情報** - キャンペーン詳細
6. **フッター** - 共通フッター

### キャンペーン告知ページ

1. **ヘッダー** - 共通ヘッダー
2. **キャンペーンバナー** - 期間、タイトル、ビジュアル
3. **特典紹介** - クーポンカード
4. **エントリーフォーム** - エントリーボタン
5. **ルール説明** - キャンペーン詳細
6. **FAQ** - よくある質問（カスタムセクション）
7. **フッター** - 共通フッター

### セール特集ページ

1. **ヘッダー** - 共通ヘッダー
2. **セールバナー** - セール情報のビジュアル
3. **目玉商品** - 商品カード（カスタム）
4. **クーポン配布** - クーポンカード × 複数
5. **カテゴリー別商品** - 商品グリッド（カスタム）
6. **フッター** - 共通フッター

## 新規ページ作成時のチェックリスト

- [ ] ECM CSS/JSの読み込み
- [ ] デザイントークンの定義（`:root`）
- [ ] 共通ヘッダーの配置
- [ ] レスポンシブ対応（メディアクエリ）
- [ ] 適切なセマンティックHTML
- [ ] アクセシビリティ対応（alt, label, aria）
- [ ] 共通フッターの配置
- [ ] ブラウザ互換性確認
- [ ] ページタイトルとメタタグの設定

## 参考リンク

- ECMドキュメント: https://r.r10s.jp/com/js/c/ecm/
- 楽天デザインガイドライン: 社内リソース参照
- コンポーネント一覧: `/components/` ディレクトリ
- プロジェクトトップ: `/index.html`

---

## AIへの指示

新規ページを作成する際は：

1. **ページの目的を明確化**: キャンペーン、商品紹介、セールなど
2. **必要なコンポーネントを選択**: 上記5つのコンポーネントから適切なものを選ぶ
3. **基本テンプレートから開始**: ヘッダー + メインコンテンツ + フッター
4. **コンポーネントのHTMLをコピー**: `components/` ディレクトリから必要な部分を抽出
5. **カスタマイズ**: コンテンツ、スタイル、パラメータを要件に合わせて調整
6. **レスポンシブ対応**: メディアクエリで各デバイスに最適化
7. **テスト**: 各ブレークポイントでの表示確認

**重要な注意点**:
- ECMのCDNリソースは必ず読み込む
- 既存のコンポーネントスタイルを上書きしない（独自のクラスを追加）
- デザイントークンを活用してカラーを統一
- セマンティックHTMLとアクセシビリティを常に意識
