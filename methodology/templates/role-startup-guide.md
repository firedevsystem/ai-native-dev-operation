---
document_id: role-startup-guide
type: operational-template
version: 1.0.0
purpose: 各AIロールを実際のAIツールに読み込ませて起動するための実践ガイド
---

# ロール起動ガイド

各AIロールを実際に稼働させるための手順書。
INDEX.mdのROLE_DOCUMENT_SETSで定義されたドキュメントの組み合わせを、各ツールでどう読み込ませるかを具体的に示す。

---

## 前提: ドキュメントセットの考え方

各ロールには**必ず読み込ませるドキュメントの組み合わせ**が決まっている。
ロールプロンプト単体では機能しない。共通ドキュメントと組み合わせて初めて完全に動作する。

詳細は `INDEX.md` の `ROLE_DOCUMENT_SETS` セクションを参照。

---

## ツール別セットアップ手順

### Claude Projects（推奨）

Claude Projectsでは、Project Knowledgeにドキュメントをアップロードし、Project Instructionsにロールの起動指示を記述する。

**手順:**

1. Claude Projectsで新しいプロジェクトを作成
2. Project Knowledgeに該当ロールのドキュメントセットをアップロード
3. Project Instructionsに以下の起動指示を貼り付け

**起動指示テンプレート（Project Instructionsに貼り付け）:**

```
あなたはAIネイティブ開発チームの【ロール名】です。

アップロードされたドキュメントを以下の優先度で参照してください:

1. core-principles.md — 最上位原則。すべての判断の基盤
2. 【ロール固有の共通ドキュメント】
3. 【ロールプロンプト】 — あなたの責務・行動指針・出力形式

ドキュメント内の @ref:document-id#SECTION_ID という記法が出てきた場合:
- @ref: の後のdocument-idに対応するアップロード済みドキュメントを参照
- # の後のSECTION_IDに対応するセクションを特定して内容を確認
- 例: @ref:core-principles#TOP_LEVEL_PRINCIPLE → core-principles.md の TOP_LEVEL_PRINCIPLE セクション

応答はすべて日本語で行ってください。
```

**ロール別のアップロードファイルと起動指示:**

#### PM・スクラムマスター

アップロード:
- `common/core-principles.md`
- `common/phase-definitions.md`
- `roles/pm-scrum-master.md`

起動指示の【ロール名】を「PM・スクラムマスター」に、【ロール固有の共通ドキュメント】を「phase-definitions.md — フェーズ管理・ゲート条件」に、【ロールプロンプト】を「pm-scrum-master.md」に置き換え。

#### コーディングエージェント

アップロード:
- `common/core-principles.md`
- `common/phase-definitions.md`
- `common/review-standards.md`
- `roles/coding-agent.md`

起動指示の【ロール固有の共通ドキュメント】:
```
2. phase-definitions.md — フェーズ定義（特にPhase 5の設計原則）
3. review-standards.md — レビュー基準を理解した上で実装する
4. coding-agent.md — あなたの責務・行動指針・出力形式
```

#### コードレビュアー

アップロード:
- `common/core-principles.md`
- `common/review-standards.md`
- `roles/code-reviewer.md`

起動指示の【ロール固有の共通ドキュメント】:
```
2. review-standards.md — 7つのレビュー視点・デシジョンツリー
3. code-reviewer.md — あなたの責務・行動指針・出力形式
```

#### システム監査官

アップロード:
- `common/core-principles.md`
- `common/review-standards.md`
- `roles/system-auditor.md`

起動指示の【ロール固有の共通ドキュメント】:
```
2. review-standards.md — レビュー基準（特に非機能層）
3. system-auditor.md — あなたの責務・監査範囲・出力形式
```

#### ユーザー・運用サポート

アップロード:
- `common/core-principles.md`
- `common/phase-definitions.md`
- `roles/user-ops-support.md`

起動指示の【ロール固有の共通ドキュメント】:
```
2. phase-definitions.md — フェーズ定義（特にPhase 2のユースケース、Phase 6のフィードバック）
3. user-ops-support.md — あなたの責務・行動指針・出力形式
```

---

### Claude Code（CLAUDE.md統合）

Claude Codeでは、プロジェクトルートの `CLAUDE.md` にロールの指示を記述するか、サブディレクトリの `CLAUDE.md` で特定ロールを起動する。

**方法1: プロジェクトルートのCLAUDE.md**

```markdown
# AI-Native Development Methodology

このプロジェクトはAIネイティブ開発方法論に基づいて開発しています。

## コーディングエージェントとしての振る舞い

以下のドキュメントを参照し、コーディングエージェントとして振る舞ってください:

1. methodology/common/core-principles.md — 最上位原則
2. methodology/common/phase-definitions.md — フェーズ定義
3. methodology/common/review-standards.md — レビュー基準
4. methodology/roles/coding-agent.md — ロール定義

### 実装時の必須事項
- エラーハンドリング設計をレビュー提出前に完了すること
- 分岐の将来性を確認してから実装すること
- レビュー提出時は coding-agent.md の OUTPUT_FORMAT に従うこと
```

**方法2: サブディレクトリのCLAUDE.md（レビュー用）**

プロジェクト内に `review/CLAUDE.md` を作成:

```markdown
# コードレビュー実行環境

このディレクトリでClaude Codeを起動した場合、コードレビュアーとして振る舞ってください。

参照ドキュメント:
1. ../methodology/common/core-principles.md
2. ../methodology/common/review-standards.md
3. ../methodology/roles/code-reviewer.md

レビュー出力は code-reviewer.md の OUTPUT_FORMAT に従ってください。
```

---

### ChatGPT（GPTs / Custom Instructions）

#### GPTs（推奨）

1. GPTsの作成画面を開く
2. Knowledgeに該当ロールのドキュメントセットをアップロード
3. Instructionsに起動指示テンプレート（上記Claude Projects用と同じ）を貼り付け

#### Custom Instructions

Custom Instructionsには文字数制限があるため、ロールプロンプトの要約版を記述し、詳細はConversation Startersで「ドキュメントを読み込んで」と指示する方法が現実的。

---

### Google AI Studio Gems

1. Gemを新規作成
2. System Instructionsに以下を記述:

```
あなたはAIネイティブ開発チームの【ロール名】です。
以下のドキュメントの内容に基づいて行動してください。

【該当ドキュメントの内容をここに全文貼り付け】

ドキュメント内の @ref:document-id#SECTION_ID という記法は、
対応するドキュメントの該当セクションへの参照です。
参照先の内容を踏まえて応答してください。

応答はすべて日本語で行ってください。
```

3. 該当ロールのドキュメントセットの内容を全文貼り付け

**注意:** Google AI Studio Gemsはファイルアップロードに対応していないため、ドキュメントの内容をSystem Instructionsに直接貼り付ける。文字数上限に注意。

---

## 運用パターン別の起動方法

### パターン1: 案件の全工程を回す

Phase進行に合わせてロールを段階的に追加する。

```
Phase 0-4: 壁打ちナビゲーション
  → core-principles + phase-definitions を読み込んだAIで壁打ち
  → ロールプロンプトは使わない（ナビゲーターとして振る舞わせる）

Phase 5:   + コーディングエージェントを起動（プロトタイプ開発）
Phase 6:   + ユーザー・運用サポートを起動（フィードバック収集）
Phase 7-8: 全5ロールをフル稼働（それぞれ別のAIセッションで起動）
```

**重要:** Phase 7-8では5つのロールを**すべて別のAIセッション**で起動する。同一セッション内で複数ロールを担わせてはならない（相互牽制が機能しなくなる）。

### パターン2: コードレビューのみ

```
1つのAIセッション: core-principles + review-standards + code-reviewer
→ 品質ゲートとしてレビューを実施
```

### パターン3: セキュリティ監査のみ

```
1つのAIセッション: core-principles + review-standards + system-auditor
→ 安全ゲートとして監査を実施
```

### パターン4: レビュー＋監査の同時実施

```
セッションA: core-principles + review-standards + code-reviewer（品質ゲート）
セッションB: core-principles + review-standards + system-auditor（安全ゲート）
→ 2つのセッションを並行して実行し、両方の結果をオペレーターが確認
```

---

## トラブルシューティング

### AIがロールの範囲を超えた行動をする場合

→ ロールプロンプトの `BOUNDARIES` セクションを再度参照するよう指示する。
例: 「あなたの BOUNDARIES セクションを確認してください。その作業はあなたの責務ではありません。」

### AIが@ref参照を解決できない場合

→ 参照先のドキュメントが読み込まれていない可能性がある。INDEX.mdのROLE_DOCUMENT_SETSを確認し、必要なドキュメントがすべてアップロード/読み込み済みか確認する。

### レビュー結果の粒度が粗い場合

→ review-standards.md のデシジョンツリーに沿って1つずつ確認するよう指示する。
例: 「review-standards.md の LAYER_1 から順に、デシジョンツリーに沿って判定してください。」
