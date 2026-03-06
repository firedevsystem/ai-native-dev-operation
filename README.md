# AIネイティブ開発 ドキュメントリポジトリ

「AIを使って開発する」のではなく、**AIを開発チームの構成員として構造的に組み込む開発手法**──
AIネイティブ開発の方法論・システムプロンプト・解説記事を管理するリポジトリです。

---

## リポジトリ構成

```
ai-native-dev-operation/
│
├── methodology/                    ← コア方法論（システムプロンプト・フレームワーク）
│   ├── ai-native-dev-navigator.md  ← Phase 0〜8 開発ナビゲーター用システムプロンプト
│   ├── review-ruleset.md           ← コードレビュー判断体系（7視点・4層構造）
│   └── takahiro-gem-prompt.md      ← 著者の思考パターン再現用プロンプト
│
├── guides/                         ← セットアップ・運用ガイド
│   ├── CLAUDE-MD-SETUP-GUIDE.md    ← 3つのコアファイルのAIプラットフォームへの組み込み手順
│   └── zenn-publishing-guide.md    ← Zenn投稿用メタデータ・マークダウン設定ガイド
│
├── articles/                       ← Zenn投稿用の個別記事（全8本）
│   ├── ai-native-dev-00-introduction.md  ← 序章：AIネイティブ開発とは何か
│   ├── ai-native-dev-01-operator.md      ← 第1章：オペレーター
│   ├── ai-native-dev-02-ai-roles.md      ← 第2章：5つのAIロールと相互牽制
│   ├── ai-native-dev-03-phase0-2.md      ← 第3章：Phase 0〜2
│   ├── ai-native-dev-04-phase3-5.md      ← 第4章：Phase 3〜5
│   ├── ai-native-dev-05-phase6-8.md      ← 第5章：Phase 6〜8
│   ├── ai-native-dev-06-review-structure.md ← 第6章：レビューの3層構造
│   └── ai-native-dev-07-principles.md    ← 第7章：壁打ちの非対称性と横断的品質原則
│
├── books/                          ← Zenn Book（有料販売用・全8章）
│   └── ai-native-dev/
│       ├── config.yaml             ← Book設定（タイトル・価格・チャプター順序）
│       └── *.md                    ← 各チャプター（内容はarticlesと同一）
│
├── HANDOVER.md                     ← AI間引継ぎドキュメント
├── package.json                    ← Node.js設定（zenn-cli依存）
└── .gitignore
```

## コア方法論の3ファイル

```
takahiro-gem-prompt.md  ← 「人物」の再現（壁打ち・教育用）
    │ 内包する
    ├── review-ruleset.md           ← 技術判断の「How」（AIレビューエージェント用）
    └── ai-native-dev-navigator.md  ← 開発プロセスの「How」（案件進行のガイドレール）
```

各ファイルの詳しい使い方は [`guides/CLAUDE-MD-SETUP-GUIDE.md`](guides/CLAUDE-MD-SETUP-GUIDE.md) を参照してください。

## Zenn CLI

* [📘 How to use](https://zenn.dev/zenn/articles/zenn-cli-guide)
