---
document_id: index
type: document-index
version: 1.0.0
purpose: 全ドキュメントの索引・ロール別ドキュメントセット定義・クロスリファレンスマップ
---

# AI-Native Development Methodology — Document Index

本インデックスはAIエージェントがドキュメントセットをロードする際の参照先として機能する。

---

## DOCUMENT_REGISTRY

### 共通ドキュメント（common/）

| document_id | ファイル | 目的 | 参照元 |
|-------------|---------|------|--------|
| core-principles | common/core-principles.md | 最上位原則・構造原則・実装品質原則・牽制関係 | 全ロール |
| phase-definitions | common/phase-definitions.md | Phase 0-8の定義・ゲート条件・差し戻しルール・壁打ち指針 | 全ロール |
| review-standards | common/review-standards.md | 4層レビュー構造・7つのレビュー視点・デシジョンツリー・出力形式 | code-reviewer, system-auditor, coding-agent |

### ロールプロンプト（roles/）

| document_id | ファイル | ロール名 | 主要稼働フェーズ |
|-------------|---------|---------|-----------------|
| role-pm-scrum-master | roles/pm-scrum-master.md | PM・スクラムマスター | Phase 7-8 |
| role-coding-agent | roles/coding-agent.md | コーディングエージェント | Phase 5以降 |
| role-code-reviewer | roles/code-reviewer.md | コードレビュアー | Phase 7-8 |
| role-system-auditor | roles/system-auditor.md | システム監査官 | Phase 7-8 |
| role-user-ops-support | roles/user-ops-support.md | ユーザー・運用サポート | Phase 6以降 |

### 運用テンプレート（templates/）

| document_id | ファイル | 目的 | 利用者 |
|-------------|---------|------|--------|
| role-startup-guide | templates/role-startup-guide.md | 各AIロールを実際のAIツールに読み込ませる手順・起動指示テンプレート | オペレーター・チームメンバー |
| review-output-template | templates/review-output-template.md | 品質ゲート・安全ゲート・オペレーター判断の出力テンプレート | code-reviewer, system-auditor, オペレーター |
| phase-gate-checklists | templates/phase-gate-checklists.md | 全フェーズのゲート条件チェックリスト（案件ごとにコピーして使用） | オペレーター |

### 個人Gem（独立利用）

| document_id | ファイル | 目的 |
|-------------|---------|------|
| takahiro-gem | takahiro-gem-prompt.md | 著者の人格・思考パターン再現。壁打ち・教育用途。ロールシステムとは独立して利用可能 |

---

## ROLE_DOCUMENT_SETS（ロール別ドキュメントセット）

各ロールをAIに担わせる際に読み込ませるドキュメントの組み合わせ。

### PM・スクラムマスター

```
load:
  1. common/core-principles.md      ← 必須: 最上位原則・構造原則
  2. common/phase-definitions.md     ← 必須: フェーズ管理・ゲート条件
  3. roles/pm-scrum-master.md        ← 必須: ロール定義・行動指針
```

### コーディングエージェント

```
load:
  1. common/core-principles.md      ← 必須: 最上位原則・構造原則
  2. common/phase-definitions.md     ← 必須: フェーズ定義（特にPhase 5の設計原則）
  3. common/review-standards.md      ← 必須: レビュー基準を理解した上で実装する
  4. roles/coding-agent.md           ← 必須: ロール定義・行動指針
```

### コードレビュアー

```
load:
  1. common/core-principles.md      ← 必須: 最上位原則・構造原則
  2. common/review-standards.md      ← 必須: 7つのレビュー視点・デシジョンツリー
  3. roles/code-reviewer.md          ← 必須: ロール定義・行動指針
```

### システム監査官

```
load:
  1. common/core-principles.md      ← 必須: 最上位原則・構造原則
  2. common/review-standards.md      ← 必須: レビュー基準（特に非機能層）
  3. roles/system-auditor.md         ← 必須: ロール定義・監査範囲
```

### ユーザー・運用サポート

```
load:
  1. common/core-principles.md      ← 必須: 最上位原則・構造原則
  2. common/phase-definitions.md     ← 必須: フェーズ定義（特にPhase 2のユースケース、Phase 6のフィードバック）
  3. roles/user-ops-support.md       ← 必須: ロール定義・行動指針
```

---

## CROSS_REFERENCE_MAP（クロスリファレンス）

ドキュメント間の参照関係:

```
core-principles ←─── 全ロールプロンプト（最上位原則・構造原則）
       │
       ├─── phase-definitions ←─── pm-scrum-master, coding-agent, user-ops-support
       │         │
       │         └─── phase-gate-checklists（ゲート条件をチェックリスト化）
       │
       ├─── review-standards ←─── code-reviewer, system-auditor, coding-agent
       │         │
       │         └─── review-output-template（レビュー出力の統合テンプレート）
       │
       └─── role-startup-guide（全ロールの起動手順。INDEX.mdのROLE_DOCUMENT_SETSを実践に落とし込む）
```

### 参照記法

ドキュメント内の `@ref:document-id#SECTION_ID` は以下のように解決する:
- `@ref:core-principles#TOP_LEVEL_PRINCIPLE` → core-principles.md の TOP_LEVEL_PRINCIPLE セクション
- `@ref:core-principles#SP-3` → core-principles.md の SP-3（レビューの2ゲート構造）
- `@ref:phase-definitions#Phase3` → phase-definitions.md の Phase 3 セクション
- `@ref:phase-definitions#PHASE_JUMP_RULES` → phase-definitions.md の差し戻しルール
- `@ref:review-standards#LAYER_3` → review-standards.md のコード層セクション
- `@ref:review-standards#REVIEW_EXECUTION_ORDER` → review-standards.md の実行順序セクション

---

## USAGE_PATTERNS（利用パターン）

### パターン1: 案件の全工程を回す

Phase 0から始めて全フェーズを通す場合。壁打ちナビゲーションは共通ドキュメントの壁打ち指針に従う。

```
Phase 0-4: core-principles + phase-definitions を読み込んだAIで壁打ち
Phase 5:   + coding-agent を追加（プロトタイプ開発）
Phase 6:   + user-ops-support を追加（フィードバック収集）
Phase 7-8: 全5ロールをフル稼働
```

### パターン2: コードレビューのみ

既存のコードに対してレビューを実施する場合。

```
load: core-principles + review-standards + code-reviewer
→ 品質ゲートとしてレビューを実施
```

### パターン3: セキュリティ監査のみ

既存のコードに対して安全性監査を実施する場合。

```
load: core-principles + review-standards + system-auditor
→ 安全ゲートとして監査を実施
```

### パターン4: 壁打ち（個人Gem）

著者の思考パターンで壁打ちする場合。ロールシステムとは独立。

```
load: takahiro-gem-prompt.md
→ Google AI Studio Gem / Claude Projects / ChatGPT GPTs として利用
```
