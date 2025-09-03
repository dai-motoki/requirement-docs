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

## ケース別の実装方法

### 1. 新しいセクションを追加する場合

`data/sections.yaml` に新しいエントリを追加：

```yaml
- id: new-section
  category: 1
  category_name: カテゴリ名
  title: 新しいセクション
  content: |
    マークダウン形式のコンテンツ
    - リスト項目1
    - リスト項目2
```

### 2. 画像ギャラリーを追加する場合

```yaml
- id: gallery-section
  category: 2
  category_name: ギャラリー
  title: 画像ギャラリー
  content: ギャラリーの説明
  images:
    - path: /images/image1.png
      name: 画像1
    - path: /images/image2.png
      name: 画像2
```

### 3. Mermaid図を追加する場合

#### 単一のMermaid図
```yaml
- id: flow-section
  title: フロー図
  mermaid: |
    graph TD
      A[開始] --> B{条件分岐}
      B -->|Yes| C[処理1]
      B -->|No| D[処理2]
```

#### 複数のMermaid図
```yaml
- id: multi-diagram
  title: 複数の図
  additional_mermaid:
    - type: architecture
      content: |
        graph TB
          A --> B
    - type: sequence
      content: |
        sequenceDiagram
          A->>B: リクエスト
```

### 4. 動的テーブルを実装する場合

```yaml
- id: dynamic-table-section
  title: 動的テーブル
  dynamic_table:
    id: myTable
    headers:
      - 列1
      - 列2
      - 列3
    data_source: table-data
```

JavaScriptでデータを提供（`main.js`）：
```javascript
window.tableData = [
  { col1: "値1", col2: "値2", col3: "値3" },
  { col1: "値4", col2: "値5", col3: "値6" }
];
```

### 5. カスタムHTMLを埋め込む場合

```yaml
- id: custom-section
  title: カスタムセクション
  custom_html: |
    <div class="custom-container">
      <style>
        .custom-container {
          background: #f0f0f0;
          padding: 20px;
        }
        /* ダークモード対応 */
        [data-theme="dark"] .custom-container {
          background: #2a2a2a;
          color: #e0e0e0;
        }
      </style>
      <h3>カスタムコンテンツ</h3>
      <p>任意のHTMLを記述できます</p>
    </div>
```

### 6. カード形式のコンテンツを作成する場合

```yaml
- id: cards-section
  title: サービス一覧
  cards:
    - title: サービスA
      badges:
        - 新機能
        - おすすめ
      content: サービスAの説明
      details:
        料金: 月額1,000円
        利用制限: なし
    - title: サービスB
      badges:
        - 人気
      content: サービスBの説明
```

### 7. コードブロックを含める場合

```yaml
- id: code-section
  title: 実装例
  content: |
    以下のコードを使用してください：
    
    ```javascript
    function example() {
      console.log("Hello, KAMUI!");
    }
    ```
    
    Pythonの例：
    
    ```python
    def example():
        print("Hello, KAMUI!")
    ```
```

### 8. 条件付き表示を実装する場合

`layouts/index.html` で条件分岐を追加：

```html
{{ if eq .id "special-section" }}
  <!-- 特別な処理 -->
{{ else }}
  <!-- 通常の処理 -->
{{ end }}
```

### 9. インタラクティブな要素を追加する場合

YAMLでマークアップを定義：
```yaml
- id: interactive
  custom_html: |
    <div class="interactive-element">
      <button id="myButton">クリック</button>
      <div id="result"></div>
    </div>
```

JavaScriptで動作を実装（`main.js`）：
```javascript
document.addEventListener('DOMContentLoaded', () => {
  const button = document.getElementById('myButton');
  if (button) {
    button.addEventListener('click', () => {
      document.getElementById('result').textContent = 'クリックされました！';
    });
  }
});
```

### 10. レスポンシブ対応のレイアウトを作成する場合

```yaml
- id: responsive-section
  custom_html: |
    <style>
      .responsive-grid {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
        gap: 20px;
      }
      @media (max-width: 768px) {
        .responsive-grid {
          grid-template-columns: 1fr;
        }
      }
    </style>
    <div class="responsive-grid">
      <div>項目1</div>
      <div>項目2</div>
      <div>項目3</div>
    </div>
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
