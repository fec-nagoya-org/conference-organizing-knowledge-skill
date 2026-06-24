# Conference Organizing Knowledge Skill

Google Docsとして公開されている[カンファレンス開催ノウハウ](https://docs.google.com/document/d/1b0GAEADYCefXw4GZNTO6mktZDhZ-hno7QIziqh54W4I/edit?usp=sharing)をClaudeのSkillとして提供するプラグイン。
GitHub Actionsにより3日ごとにDocsの内容を自動同期しています。

## Skillの導入

```zsh
# マーケットプレイスの追加
claude plugin marketplace add fec-nagoya-org/conference-organizing-knowledge

# プラグインのインストール
claude plugin install 

# skillの使用
conference-organizing-knowledge-skill@conference-organizing-knowledge-skill
```

## カンファレンス開催ノウハウとは

カンファレンスを開催する上で注意すべき点を有志でまとめ、主にこれからイベントを主催するスタッフの間で共有できることを目的に作成されたドキュメント。

<img src="./docs/images/pages_list.png" width="500px">

## 開発Docs

このリポジトリの開発に関するドキュメントは[こちら](./docs/development.md)
