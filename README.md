# KAMUI CODE ドキュメント - Hugo版

元のHTMLファイルと同じ見た目・機能を保ちながら、Hugoで管理できるように移行したプロジェクトです。

## 概要

KAMUI CODE は、MCP（Model Context Protocol）に準拠した複数のサーバー群を統合的に提供するソリューションのドキュメントサイトです。このプロジェクトは、単一のHTMLファイルから、Hugoの静的サイトジェネレーターを使用した管理しやすい構造に移行されました。

## プロジェクト構成

```
requirement-docs/
├── config.yaml              # Hugo設定ファイル（YAML形式）
├── content/
│   └── _index.md           # ホームページのフロントマター
├── data/
│   ├── sections.yaml       # 全セクションのコンテンツデータ
│   ├── kamui-doc-menus.json
│   ├── mcp_catalog.json
│   ├── mcp_playlists.json
│   └── pages.yaml

├── themes/kamui-docs/      # カスタムテーマ
│   ├── theme.yaml         # テーマ設定
│   ├── layouts/
│   │   ├── _default/
│   │   │   └── baseof.html  # ベースレイアウト
│   │   ├── index.html        # ホームページテンプレート
│   │   └── partials/         # 再利用可能なパーシャル
│   │       ├── sidebar.html
│   │       ├── header.html
│   │       ├── modals.html
│   │       ├── table.html
│   │       ├── image-grid.html
│   │       ├── mermaid.html
│   │       ├── cards.html
│   │       ├── code.html
│   │       ├── dynamic-table.html
│   │       ├── flow-diagram.html
│   │       ├── mcp-section.html
│   │       ├── dynamic-cards.html
│   │       ├── gantt.html
│   │       ├── mermaid-with-caption.html
│   │       ├── design-specs.html
│   │       └── client-samples.html
│   └── static/
│       ├── css/
│       │   └── main.css      # 全てのスタイル
│       └── js/
│           └── main.js       # 全てのJavaScript
├── static/
│   ├── images/             # 全ての画像ファイル
│   │   ├── journey-discover.png
│   │   ├── journey-explore.png
│   │   ├── journey-compare.png
│   │   ├── journey-trial.png
│   │   ├── journey-purchase.png
│   │   └── ... (その他の画像)
│   └── data/              # JSONデータファイル
│       ├── kamui-doc-menus.json
│       ├── mcp_catalog.json
│       ├── mcp_playlists.json
│       └── menus.json
└── public/                   # ビルド出力ディレクトリ
```

## 実装された機能

元のHTMLファイルにあった全ての機能が移行されています：

### 1. UI/UX機能
- ✅ **ダーク/ライトテーマ切り替え** - LocalStorageで保存
- ✅ **サイドバーナビゲーション** - 折りたたみ可能な章構成
- ✅ **クイックリンク** - 主要セクションへのジャンプ
- ✅ **検索機能** - ヘッダーの検索バー
- ✅ **表示切り替え** - カード/リスト表示の切り替え
- ✅ **レスポンシブデザイン** - モバイル対応
- ✅ **カスタマージャーニーマップ** - KAMUI CODE利用時のユーザー体験を可視化

### 2. インタラクティブ要素
- ✅ **UI遷移図** - ズーム可能なインタラクティブフロー図
- ✅ **動的テーブル** - JSONデータから自動生成される表
- ✅ **MCPプレイリスト/カタログ** - カテゴリ別に切り替え可能
- ✅ **動的カード生成** - サーバーカタログ、パッケージ一覧
- ✅ **画像モーダル** - クリックで拡大表示
- ✅ **右クリックメニュー** - 画像の相対パスコピー機能

### 3. ビジュアル要素
- ✅ **Mermaid図** - 複数のフロー図、ガントチャート
- ✅ **デザイン要件定義** - カラーパレット、タイポグラフィ、レイアウト仕様
- ✅ **カテゴリ別グラデーション** - クリエイティブ/開発/ビジネス
- ✅ **コードハイライト** - 見やすいコード表示

### 4. データ管理
- ✅ **YAML形式のデータ** - `data/sections.yaml`で全コンテンツを管理
- ✅ **JSONフォールバック** - オフライン時のローカルデータ表示
- ✅ **動的コンテンツ生成** - JavaScriptによる動的要素
- ✅ **MCP仕様書リンク** - Model Context Protocol公式仕様書への参照

## 使い方

### 開発サーバーの起動

```bash
# 開発サーバーを起動（ライブリロード付き）
hugo server

# 別のポートで起動
hugo server -p 8080

# ドラフトも含めて表示
hugo server --buildDrafts
```

### ビルド

```bash
# 本番用ビルド
hugo

# ビルドされたファイルは public/ ディレクトリに出力されます
```

### コンテンツの編集

1. **セクションの編集**: `data/sections.yaml` を編集
2. **画像の追加**: `static/images/` に配置
3. **新しいセクションの追加**: `sections.yaml` に新しいエントリを追加

#### sections.yaml の構造例

```yaml
- id: section-id
  category: 1
  category_name: カテゴリ名
  title: セクションタイトル
  content: |
    マークダウン形式のコンテンツ
  images:
    - path: /images/example.png
      name: 画像名
  mermaid: |
    graph TD
      A --> B
  cards:
    - title: カードタイトル
      badges:
        - バッジ1
      content: カード内容
```

## 特殊な機能の使い方

### 動的テーブル
```yaml
dynamic_table:
  id: tableId
  headers:
    - ヘッダー1
    - ヘッダー2
  data_source: json-data-source
```

### Mermaid図（複数）
```yaml
additional_mermaid:
  - type: system_architecture
    content: |
      graph TB
        A --> B
```

### カスタムHTML
```yaml
custom_html: |
  <div class="custom-content">
    <!-- カスタムHTMLコンテンツ -->
  </div>
```

### デザイン仕様
```yaml
design_specs:
  colors:
    - group: グループ名
      swatches:
        - name: 色名
          color: "#000000"
```

## デプロイ

### GitHub Pages

1. リポジトリの Settings > Pages
2. Source を "Deploy from a branch" に設定
3. Branch を main、フォルダを `/public` に設定
4. ビルドしてコミット：

```bash
hugo
git add public/
git commit -m "Build site"
git push
```

### Netlify / Vercel

Hugo対応の設定で自動デプロイが可能です。

## 最新の更新内容

### 2025年9月3日
- ✅ カスタマージャーニーマップを追加（UI・UXセクション）
  - 矢印型のフェーズデザイン
  - KAMUI CODE利用時のユーザー体験を可視化
  - 各アクションにアイコン画像を配置
- ✅ 付録にMCP公式仕様書へのリンクを追加
- ✅ メニュー一覧テーブルの動的生成を実装
- ✅ メイン画像を `kamui-gradient-soft-2.png` に設定
- ✅ 特定の画像の表示制御を実装

## 注意事項

- 画像パスは `/images/` から始まる絶対パスを使用
- Mermaid図は自動的に初期化されます
- JavaScriptの動的機能は `main.js` に集約
- CSSは `main.css` に全スタイルを記載
- JSONデータは `static/data/` ディレクトリに配置
- カスタムHTMLは `custom_html` フィールドで直接記述可能

## ライセンス

MIT License

## 作成者

KAMUI CODE プロジェクトチーム
