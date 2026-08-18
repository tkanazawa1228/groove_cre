---
name: amazon-subimage-orchestrator
description: Coordinate the end-to-end Amazon sub-image planning workflow across product information, review analysis, competitor creative market research, claim risk checks, six-image structure planning, designer-ready wireframes, Figma output, and designer handoff briefs. Use when Codex is asked to produce or improve Amazon product sub-image concepts from spreadsheets, reviews, ASIN research, market patterns, product features, or existing creative analysis, especially when multiple Amazon creative skills must be sequenced.
---

# Amazon Subimage Orchestrator

Use this skill as the workflow controller. Do not replace the specialist skills; route to them, normalize their outputs, and make the final production decisions.

## Core Rule

Keep analysis and production as separate phases:

1. Product understanding
2. Review evidence
3. Market and competitor creative patterns
4. Appeal prioritization
5. Six-image information design
6. Six-image composition design
7. Compliance/copy risk check
8. Designer handoff wireframe
9. Designer brief

If a phase is missing, state the gap and use the best available evidence instead of inventing claims.

## Specialist Skill Routing

- Use `amazon-review-matrix` when review Excel files or review analysis outputs are provided.
- Use `amazon-creative-market-research` when ASINs, Amazon URLs, sub-image galleries, A+ content, or competitor creative patterns must be read.
- Use `amazon-subimage-structure` when turning analysis into six Amazon sub-image plans.
- Use `amazon-subimage-layout-pattern-library` when choosing distinct visual composition types.
- Use `amazon-compliance-copy-check` before finalizing copy or claim wording.
- Use `amazon-subimage-wireframe-quality-check` before handing off any wireframe.
- Use `amazon-designer-brief-generator` after the structure is approved or when a handoff document is requested.
- Use Google Sheets/Figma skills when the source or deliverable is a connected Sheet or Figma file.

## Required Workflow

### 1. Inventory Inputs

Record the exact sources:

- Product name, category, ASIN/URL if available
- Source spreadsheet/file/tab/range
- Review analysis source and sample size if available
- Competitor ASINs or market research source
- Supplied assets and unavailable assets
- Required claims, required exclusions, and brand tone
- Delivery target: text plan, Figma, brief, or all

### 2. Normalize Evidence

Produce a short evidence table:

| Evidence | Source | Strength | Use In Image | Risk |
|---|---|---|---|---|

Strength values: `strong`, `medium`, `weak`, `required-but-unsupported`.
Risk values: `low`, `needs-wording-care`, `avoid-main-claim`, `needs-official-confirmation`.

### 3. Decide Appeal Priority

Sort appeals into:

- Main differentiators
- Baseline category expectations
- Reassurance/support details
- Avoid or downplay

Do not let weak claims become first-image claims.

### 4. Create The Six-Image Strategy

For each image, define:

- Role in purchase journey
- Main claim
- Support claim
- Evidence source
- Layout pattern
- Main visual subject
- Required asset
- Risk/wording note

Use a distinct layout pattern for each image unless the user explicitly wants a standardized template.

### 5. Gate Before Figma

Before writing to Figma, verify:

- Six image roles do not duplicate each other
- At least four distinct layout patterns are used
- First image carries the strongest supported differentiator
- At least one image handles purchase anxiety
- At least one image handles usage scene or lifestyle fit
- All photo placeholders specify what the photo should show
- Risky claims are softened or removed

### 6. Figma Output

When producing a Figma wireframe:

- Preserve any prior page/version unless the user asks to replace it.
- Create 1600 x 1600 px frames for Amazon sub-images unless a different production size is specified.
- Put designer notes outside the artboard, not inside the final image frame.
- Separate editable text, photo placeholders, badges, cards, lines, and background shapes.
- Name frames by number and layout role, e.g. `image-01_product-hero`.

## Output Contract

When asked for a plan, use the contracts in `references/output-contracts.md`.
When asked for only guidance, summarize the current phase, gaps, and recommended next action.

## First-Pass Figma Template Delivery

When the user provides product information, review analysis, competitor or category research, and a Figma template for an Amazon six-sub-image plan, complete the full template in the first delivery whenever the required sources and target file are available.

1. Populate `素材`, `トンマナ`, `ムードボード`, and the `内容` and `使用画像` areas for images 1 through 6.
2. Select 5–8 moodboard references from the whole relevant Amazon category, not only provided competitor ASINs. If an image cannot be embedded, write its image name as a blue, underlined hyperlink in Figma.
3. Generate separate files for every required background, product image, and illustration/icon; do not use a combined material sheet as the only source asset.
4. Create a dynamically resolved Downloads subfolder named `<Figma file name>_画像` and save every generated asset there. Never hardcode a user name.
5. In each `使用画像` field, write the individual image filenames and only the notes that apply to that image. Use: `※〜は公式商品写真へ差し替える必要があります。` and `※〜は仕様の確認が必要です。`
6. Treat generated product, phone, and detail images as generic mocks unless official product assets were supplied. Never present a mock as the actual product.
7. Verify the source spreadsheet/Sheet, Figma text, generated-file count, filenames, and Downloads folder before reporting completion.
