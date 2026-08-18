---
name: amazon-review-matrix
description: Analyze Amazon review Excel files for a target product and competitors, create a source-grounded appeal matrix, and save the complete result as a formatted Excel workbook by default. Use for review comparison, positive and negative feature extraction, market baseline appeals, weaknesses, dissatisfaction, claim cautions, original-review evidence, and Amazon sub-image planning, including competitor-only analysis for a new product with no self reviews.
---

# Amazon Review Matrix

## Default outcome

Create one `.xlsx` workbook from the start as the standard deliverable whenever the user asks for Amazon review analysis. Do not stop at a chat summary and do not ask whether the user wants an Excel conversion. Produce chat-only, Markdown, JSON, or CSV output only when the user explicitly requests that format. Save the workbook in the current user's dynamically resolved `Downloads` directory unless the user explicitly specifies another destination, then return a clickable link plus only the most important conclusions.

Use the bundled scripts. Do not rewrite an Excel generator for each task.

## Inputs

- Accept zero or one self-product review `.xlsx` file.
- Accept one or more competitor review `.xlsx` files.
- Accept `food`, `beauty`, `daily`, `appliance`, `apparel`, `pet`, or `other` as the genre.
- Require a header row. Inspect unusual headers before analysis.
- When self reviews are absent, run competitor-only market mode. Mark self strengths and weaknesses as `新規商品のため未判定`; never infer them.

## Required workflow

1. Resolve a Node.js runtime without assuming a user-specific path. Prefer a configured workspace runtime or `node` on `PATH`; on Codex Desktop for Windows, the bundled launcher can locate the app runtime.
2. Unless the user explicitly selected another output format, keep `xlsx` as the format and resolve `Downloads` from the current runtime user. On Windows, honor a redirected Downloads known folder before falling back to `<current-user-profile>/Downloads`. Never hardcode a username.
3. Run `scripts/run_review_analysis.ps1` on Windows or invoke `scripts/analyze_reviews.mjs` with any available Node.js runtime.
4. Split each review into sentence or clause meaning units; do not use isolated word frequency as the result.
5. Classify each unit by aspect and `positive`, `negative`, `mixed`, or `neutral` sentiment.
6. Count distinct reviews separately from meaning units.
7. Keep self and competitor evidence separate. Preserve original excerpts, ASIN, star rating, and review number.
8. Distinguish purchaser impressions from claims usable in advertising. Treat safety, health, capacity, efficacy, and guaranteed-performance wording cautiously.
9. Reopen the generated workbook with the bundled validator. Confirm sheet names, row counts, Japanese text, and Open XML/ZIP integrity before delivery.

## Default command

```powershell
& "$skillRoot/scripts/run_review_analysis.ps1" `
  -Genre appliance `
  -Self "C:/path/self.xlsx" `
  -Competitors "C:/path/comp1.xlsx","C:/path/comp2.xlsx"
```

Omit `-Self` for a new product. The default filename is:

```text
Amazonレビュー分析_<商品ジャンル>_<YYYYMMDD>.xlsx
```

Direct Node usage:

```powershell
node scripts/analyze_reviews.mjs --genre appliance --self self.xlsx --competitors comp1.xlsx comp2.xlsx
```

Supported explicit alternatives are `--format md` and `--format json`. The default is `--format xlsx`.

## Required workbook sheets

Always create these sheets in this order:

1. `概要`
2. `商品情報`
3. `自社ポジティブ`
4. `自社ネガティブ`
5. `市場ポジティブ`
6. `市場ネガティブ`
7. `訴求マトリクス`
8. `ASIN別比較`
9. `評価軸集計`
10. `原文根拠`
11. `意味単位明細`

Include review counts, average rating, rating distribution, date range, verified-purchase count, Vine count, evidence cautions, and count definitions. Use frozen headers, filters on tabular sheets, wrapped text, readable column widths, and green/red/yellow styles for positive/negative/mixed or caution content. Keep the structure readable after Google Sheets import.

## Evidence rules

- Keep excerpts faithful; do not paraphrase text as an original quote.
- Include star rating and source ASIN when available.
- Mark weak or split evidence as `訴求注意`.
- Keep delivery or packaging complaints as operational issues, not product benefits.
- Never convert purchaser impressions into guaranteed safety, efficacy, health, legal, or capacity claims.

## Delivery

Return the workbook link and a compact summary. State that the file was saved in `Downloads`. Do not make the user request a second conversion step.

## Six-Sub-Image Handoff

When the analysis is used for an Amazon six-sub-image Figma template, deliver a concise handoff that separates supported priority appeals, review-derived anxieties, market baseline expectations, prohibited or unsupported claims, and facts requiring official specification confirmation. Mark every safety, capacity, output, compatibility, dimension, or material claim that must be confirmed before it is used in image copy or an illustration.
