# AIネイティブ開発 ドキュメントリポジトリ

「AIを使って開発する」のではなく、**AIを開発チームの構成員として構造的に組み込む開発手法**──
AIネイティブ開発の方法論・AIロールプロンプト・解説記事を管理するリポジトリです。

---

## リポジトリ構成

```
ai-native-dev-operation/
│
├── methodology/                         ← AIネイティブ開発の方法論
│   ├── INDEX.md                         ← ドキュメント索引・ロール別ドキュメントセット定義
│   │
│   ├── common/                          ← 共通知識（全ロールが参照）
│   │   ├── core-principles.md           ← 根源的原則・構造設計ルール・牽制関係
│   │   ├── phase-definitions.md         ← Phase 0〜8 の定義・ゲート条件・差し戻しルール
│   │   └── review-standards.md          ← コードレビュー4層構造・7視点・デシジョンツリー
│   │
│   ├── roles/                           ← 各AIロールのシステムプロンプト
│   │   ├── pm-scrum-master.md           ← PM・スクラムマスター
│   │   ├── coding-agent.md              ← コーディングエージェント
│   │   ├── code-reviewer.md             ← コードレビュアー
│   │   ├── system-auditor.md            ← システム監査官
│   │   └── user-ops-support.md          ← ユーザー・運用サポート
│   │
│   └── takahiro-gem-prompt.md           ← 著者の思考パターン再現Gem（独立利用）
│
├── guides/                              ← 人間向けガイド
│   ├── usage-guide.md                   ← ドキュメント活用ガイド（セットアップ・利用シーン別）
│   └── zenn-publishing-guide.md         ← Zenn投稿用メタデータ設定ガイド
│
├── articles/                            ← Zenn投稿用の個別記事（全8本）
│   └── ai-native-dev-{00-07}-*.md
│
├── books/                               ← Zenn Book（有料販売用・全8章）
│   └── ai-native-dev/
│       ├── config.yaml                  ← Book設定（タイトル・価格・チャプター順序）
│       └── *.md                         ← 各チャプター
│
├── HANDOVER.md                          ← AI間引継ぎドキュメント
├── package.json                         ← Node.js設定（zenn-cli依存）
└── .gitignore
```

## 5つのAIロール

| ロール | 責務 | 主要フェーズ |
|--------|------|-------------|
| PM・スクラムマスター | 進捗管理・要件整合性確認 | Phase 7-8 |
| コーディングエージェント | 実装の主体 | Phase 5以降 |
| コードレビュアー | 7視点の品質レビュー（品質ゲート） | Phase 7-8 |
| システム監査官 | 安全性・安定性・可用性の独立監査（安全ゲート） | Phase 7-8 |
| ユーザー・運用サポート | ペルソナベーステスト・UX検証 | Phase 6以降 |

## 使い方

詳しくは [`guides/usage-guide.md`](guides/usage-guide.md) を参照してください。
ドキュメントの索引とロール別の読み込みセットは [`methodology/INDEX.md`](methodology/INDEX.md) に定義されています。

## Zenn CLI

* [📘 How to use](https://zenn.dev/zenn/articles/zenn-cli-guide)
