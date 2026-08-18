---
name: amazon-creative-market-research
description: Read Amazon.co.jp ASIN product image galleries, sub-images, A+ content, brand story modules, and other specified product-page creative content; extract each image/module's visible content, appeal, proof, structure, and compliance risks; compare a specified ASIN group to identify market creative patterns, category conventions, gaps, and reusable content strategy. Use when the user asks for ASIN-based creative market research, competitor sub-image analysis, A+ content analysis, appeal pattern extraction, Amazon image carousel research, market-winning creative structure discovery, or an Excel image inventory with the original Amazon gallery files embedded.
---

# Amazon Creative Market Research

## Purpose

Analyze Amazon creative content from user-specified ASINs and turn visual observations into reusable market patterns. Focus on what each image/module communicates, why it may exist in the purchase journey, and how the ASIN group converges or differs.

This skill is for market research and content planning. It does not replace legal review, medical/regulatory review, or Amazon Seller Central policy review.

## Required Inputs

Ask only for missing essentials. Continue with reasonable assumptions when possible.

- ASIN list or Amazon product URLs
- Target marketplace when ambiguous; default to `amazon.co.jp` for Japanese requests
- Content scope: product image gallery/sub-images, A+, brand story, comparison tables, video thumbnails, or all visible product-page creative
- Category and target product context, if known
- Desired output: quick summary, ASIN-by-ASIN matrix, pattern report, creative recommendations, or Figma/image-generation handoff

## Workflow

1. Confirm the research scope.
   - Normalize URLs to ASINs.
   - Separate target/self ASINs from competitor/reference ASINs when the user provides that distinction.
   - State if a page cannot be accessed, is unavailable, requires login, or has too few images.

2. Browse current product pages.
   - Use official Amazon product pages when available.
   - Because Amazon content changes over time, browse for every ASIN research task.
   - Capture product image gallery URLs, visible image thumbnails, A+ module images/text, brand story images/text, and visible product title/bullets.
   - If direct Amazon access is blocked or incomplete, use reliable secondary pages only to identify products; do not pretend they represent current Amazon sub-images.

3. Inspect image content.
   - For each image, identify visible product form, scene, layout, readable claims, icons, badges, tables, graphs, people, usage moments, and callouts.
   - Use the directly downloaded gallery media when visual content cannot be understood from DOM alt text.
   - Screenshots and page crops may be used only as temporary navigation evidence for non-gallery UI; never use them as the gallery image source or embed them in the deliverable.
   - Do not quote large amounts of text from images. Summarize visible claims and note exact short phrases only when necessary.

4. Extract appeal meaning.
   - Classify each image/module using `references/extraction-schema.md`.
   - Distinguish product facts, lifestyle usage, emotional reassurance, functional convenience, ingredient/nutrition proof, authority/research proof, comparison, instructions, and risk-reduction content.
   - Mark uncertain interpretations as inferred.

5. Build ASIN-level matrices.
   - List every observed image/module in order.
   - Include role, main appeal, support/proof, visual structure, compliance caution, and reusable insight.
   - Record missing content patterns, not just present ones.

6. Extract group patterns.
   - Identify repeated sequence patterns across the ASIN group.
   - Separate category conventions from standout differentiators.
   - Identify overused patterns, underused opportunities, and content gaps.
   - State confidence based on sample size and access quality.

7. Produce a usable report.
   - Include sources with Amazon URLs and date checked.
   - Include an observation matrix and pattern summary.
   - Include recommendations only after observations.
   - If the user will create Amazon images from the findings, include policy-sensitive wording cautions and image-generation handoff notes.

8. Build and verify an Excel image inventory whenever Excel is requested or created.
   - Create a worksheet named exactly `画像一覧` and include a column named exactly `画像`.
   - Resolve every gallery item's highest-quality original image URL from the current Amazon page. Prefer `hiRes`; otherwise use the largest gallery asset exposed for that item. Do not substitute thumbnails.
   - Download each image directly from its image URL. Browser page-asset export or an HTTP client is acceptable only when it saves the response bytes from that URL unchanged.
   - Do not use screenshots, screen crops, clipboard captures, recompression, format conversion, image editing, or pixel resizing. Do not pass the image through a canvas or an image-processing save operation.
   - Preserve the downloaded file bytes. Record ASIN, display order, image URL, local file, dimensions, byte size, and SHA-256 for every image.
   - Embed each original file in the corresponding `画像` cell. Scale only the Excel drawing frame with the aspect ratio locked and center it horizontally and vertically inside the cell; never alter the underlying image file.
   - Use `scripts/build_image_inventory_xlsx.ps1` to build the workbook and emit a verification JSON when running on PowerShell. On another runtime, implement the same OOXML guarantees and checks.
   - Before delivery, verify: source image count equals expected gallery count; embedded media count equals source image count; each embedded media SHA-256 equals its downloaded source SHA-256; and each Excel drawing width/height ratio matches the source pixel ratio within `0.0001` relative error.
   - Treat any missing image, download failure, duplicate or ambiguous gallery item, unsupported format, hash mismatch, count mismatch, or aspect-ratio mismatch as a delivery blocker. Do not report the workbook as complete until all checks pass.

## References

Read these only when needed:

- `references/extraction-schema.md`: use before structuring image/module observations.
- `references/amazon-creative-compliance-notes.md`: use before producing recommendations or image copy, especially for food, infant, supplement, health, cosmetic, or regulated categories.

## Optional Script

Use `scripts/summarize_patterns.py` when observations have been collected into JSON and a consistent markdown report is useful.

Use `scripts/build_image_inventory_xlsx.ps1` after original gallery files have been downloaded directly. Its JSON input contains an `images` array with `asin`, `product`, `order`, `content_type`, `image_url`, and `local_path`. The script writes the `画像一覧` workbook and a verification JSON, and fails if any integrity check fails.

Input shape:

```json
{
  "marketplace": "amazon.co.jp",
  "checked_date": "YYYY-MM-DD",
  "asins": [
    {
      "asin": "B000000000",
      "product": "Product name",
      "url": "https://www.amazon.co.jp/dp/B000000000",
      "items": [
        {
          "order": 1,
          "content_type": "gallery_image",
          "role": "first_impression",
          "appeal": "portable stick format",
          "visual_structure": "pack + sticks on white background",
          "proof": "visible product quantity",
          "cautions": "none",
          "notes": "shape recognition"
        }
      ]
    }
  ]
}
```

## Output Standards

- Lead with observed findings, then patterns, then recommendations.
- Preserve image/module order.
- Separate `observed` from `inferred`.
- Mention access limitations.
- Avoid claiming causality such as "this image increases CVR" unless external evidence is provided.
- Avoid turning competitor claims into recommended copy without checking whether the target product can substantiate them.
- For Amazon images, do not recommend review quotes, star-rating graphics, Amazon badges, ranking badges, shipping/Prime claims, seller-specific claims, or unsupported superlatives.
- When Excel contains a gallery inventory, report the expected image count, embedded count, hash result, aspect-ratio result, verification JSON path, and any access limitation.

## Moodboard Handoff for Amazon Sub-Image Templates

When the research feeds an Amazon six-sub-image Figma template, extend the research beyond supplied competitor ASINs and select 5–8 usable references from the relevant category as a whole. For each selected reference, record the image name, direct image or product-page URL, layout/tone rationale, and access status. When Figma embedding is unavailable, provide the image name as a hyperlink target; do not report an unverified external image as locally saved.
