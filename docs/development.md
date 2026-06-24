# 開発ガイド

## 前提

- [mise](https://mise.jdx.dev/) によるツールバージョン管理（bun 1.3.14, node 24）
- bun をランタイム/パッケージマネージャとして使用
- biome 2.x によるリント/フォーマット
- lefthook による git hooks

## セットアップ

```sh
mise install
bun install
```

## コマンド

| コマンド | 内容 |
|---|---|
| `bun run fetch` | Google Docsからコンテンツを取得しMarkdownに変換 |
| `bun run check` | biomeによるリント/フォーマット（自動修正） |
| `bun run test` | vitestによるテスト実行 |
| `bun run validate` | Claude Codeプラグインのバリデーション |

## ディレクトリ構成

```
.
├── .claude-plugin/          # プラグイン/マーケットプレイス定義
│   ├── plugin.json
│   └── marketplace.json
├── .github/workflows/
│   ├── ci.yml               # push/PR時のテスト
│   └── sync-docs.yml        # 3日ごとのDocs同期
├── scripts/
│   ├── fetch-docs.mjs       # Docs取得エントリポイント
│   ├── html-to-markdown.mjs # HTML→Markdown変換ロジック
│   └── __tests__/           # テスト
├── skills/
│   └── conference-organizing-knowledge-skill/
│       ├── SKILL.md          # スキル定義
│       └── references/       # 自動生成されたMarkdown（直接編集不可）
└── docs/
    └── images/
```

## Docs同期の仕組み

1. Google Docsの公開エクスポートURLからHTMLを取得
2. styleタグ、imgタグ、class/style/id属性を除去
3. Google redirect URLを実際のURLにデコード
4. turndownでMarkdownに変換
5. 前回の内容と比較し、変更がある場合のみファイルを更新

環境変数`GOOGLE_API_KEY`を設定するとDrive API経由で取得する。未設定の場合は公開エクスポートURLを使用する。

## lefthook hooks

pre-commitで以下を並列実行する。

- plugin-validate: `claude plugin validate --strict .`
- biome-check: `bun run check`
- skill-md-exists: SKILL.mdの存在確認
- marketplace-json-valid: marketplace.jsonのJSON構文チェック

pre-pushでplugin-validateを実行する。
