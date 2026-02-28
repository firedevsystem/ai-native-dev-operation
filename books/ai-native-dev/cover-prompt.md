# カバー画像生成プロンプト集

本書「AIネイティブ開発 実践ガイド」のカバー画像（500px × 700px）を生成するためのプロンプトです。
生成後、`cover.png` としてこのディレクトリに配置してください。

---

## 共通コンセプト

- **テーマ**: 人間（オペレーター）を中心に、5つのAIロールが相互牽制しながら開発を進める構造
- **キーカラー**: ディープブルー（信頼・構造）× アクセントにシアンやオレンジ
- **雰囲気**: テクノロジー感がありつつも、構造・秩序・設計思想を感じさせる
- **避けるべき要素**: テキスト（タイトルはZenn側で自動表示される）、写実的な人物の顔

---

## 1. ChatGPT (DALL-E 3) 用プロンプト

```
A minimalist technology book cover illustration, 500x700 pixels, portrait orientation.

Central concept: One human figure (abstract silhouette) stands at the center as a decision-maker,
surrounded by 5 distinct AI agent icons arranged in a pentagon formation.
Thin lines connect the agents to each other showing mutual checks and balances.

The background features a subtle blueprint-style grid with 9 horizontal phase layers,
suggesting a structured development pipeline from top to bottom.

Color palette: Deep navy blue background, cyan and electric blue for the AI agents,
warm amber/orange glow for the central human figure, white accent lines.

Style: Clean vector-like illustration, geometric shapes,
tech-minimal aesthetic similar to O'Reilly or Pragmatic Programmer book covers.
No text, no letters, no words anywhere in the image.
```

### バリエーション A（回路基板モチーフ）

```
Abstract book cover art, 500x700 pixels, portrait.

A circuit board pattern forms the background, but instead of electronic components,
the nodes represent 5 different AI roles (shown as distinct geometric shapes:
hexagon, diamond, circle, triangle, square) connected by clean pathways.

At the center intersection, a larger glowing node represents the human operator -
the decision point where all paths converge.

9 horizontal gate lines cross the board from left to right,
representing phase gates in a development process.

Color scheme: Dark indigo background, teal/cyan circuit paths,
golden-amber center node, subtle gradient from dark at edges to lighter at center.

Minimal, geometric, modern tech aesthetic. No text or letters.
```

### バリエーション B（オーケストラモチーフ）

```
Abstract minimalist book cover, 500x700 pixels, portrait orientation.

A conductor's podium viewed from above, with 5 sections of an orchestra
represented as abstract geometric clusters, each in a slightly different shade of blue.
The conductor (human operator) is shown as a single warm-colored point of light
at the center, with subtle conducting lines radiating outward.

The composition suggests harmony, structure, and coordinated collaboration
between multiple specialized units guided by a single decision-maker.

Deep blue to midnight purple gradient background.
Cyan, teal, and electric blue for the sections. Warm amber for the conductor.
Clean, modern, vector-style illustration. No text or letters anywhere.
```

---

## 2. Midjourney 用プロンプト

```
minimal tech book cover illustration, one central human silhouette surrounded by
five AI agent nodes in pentagon formation, connected by thin geometric lines showing
mutual checks and balances, blueprint grid background with nine horizontal phase layers,
deep navy blue background, cyan electric blue agents, warm amber human figure,
clean vector aesthetic, no text --ar 5:7 --style raw --s 200 --no text words letters
```

### バリエーション A

```
abstract circuit board art, five distinct geometric nodes connected by clean pathways,
central golden glowing intersection node, nine horizontal gate lines crossing the board,
dark indigo background, teal cyan paths, minimal geometric modern tech aesthetic,
book cover art --ar 5:7 --style raw --s 150 --no text words letters numbers
```

### バリエーション B

```
abstract orchestral formation viewed from above, five blue geometric clusters
surrounding one warm amber central point of light, conducting lines radiating outward,
deep blue to midnight purple gradient, harmony structure coordination theme,
clean modern vector illustration, book cover --ar 5:7 --style raw --s 200 --no text words letters
```

---

## 3. Stable Diffusion (SDXL / SD3) 用プロンプト

### Positive prompt

```
(minimalist tech book cover:1.3), (abstract geometric illustration:1.2),
central human silhouette as decision maker, five AI agent nodes in pentagon arrangement,
thin connecting lines showing mutual oversight, blueprint grid background,
nine horizontal phase layers, deep navy blue, cyan accents, amber warm glow center,
clean vector style, modern technology aesthetic, high contrast, sharp edges,
professional book cover design
```

### Negative prompt

```
text, letters, words, numbers, watermark, signature, realistic face, photograph,
blurry, noisy, low quality, deformed, cluttered, busy background, 3d render,
anime, cartoon style, childish
```

### 推奨設定

- サイズ: 512×720 → Upscale to 500×700
- Sampler: DPM++ 2M Karras
- Steps: 30-40
- CFG Scale: 7-8

---

## 4. Adobe Firefly 用プロンプト

```
Minimalist geometric book cover illustration.
An abstract pentagon formation of five distinct blue geometric shapes
connected by thin lines, surrounding a central warm amber glowing point.
Background is a deep navy blueprint grid with nine subtle horizontal lines.
Clean vector aesthetic, modern technology theme, professional and structured.
No text, no letters.
```

**スタイル設定**: グラフィック / ベクター
**カラー&トーン**: 高コントラスト、寒色系
**構図**: 中央配置

---

## 5. Canva AI (Magic Media) 用プロンプト

```
Minimalist tech book cover, abstract geometric design,
five blue shapes connected in a pentagon pattern around
a central glowing amber point, deep navy background
with subtle grid lines, clean modern vector style, no text
```

**カスタムサイズ**: 500 × 700 px

---

## 生成後のチェックリスト

- [ ] ファイル名: `cover.png` または `cover.jpeg`
- [ ] サイズ: 500px × 700px（推奨）
- [ ] テキストが含まれていないこと（タイトルはZennが自動表示）
- [ ] 配置先: `books/ai-native-dev/cover.png`
- [ ] 暗すぎず、サムネイルサイズでも視認性が良いこと
