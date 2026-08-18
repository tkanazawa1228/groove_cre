---
name: amazon-subimage-wireframe-quality-check
description: Audit Amazon sub-image concepts, six-image wireframes, Figma outputs, and designer handoff drafts for production readiness. Use when Codex needs to review whether Amazon creative wireframes are more than information blocks, have distinct compositions, clear visual hierarchy, concrete photo/material directions, compliant copy, editable Figma layers, and enough specificity for a designer to execute.
---

# Amazon Subimage Wireframe Quality Check

Use this skill before sending Amazon sub-image plans or Figma wireframes to a designer.

## Review Stance

Be strict. A pass means a designer can start production without guessing the composition, visual priority, or required assets.

## Minimum Checks

1. Six-image strategy
2. Composition diversity
3. Visual hierarchy
4. Photo/material specificity
5. Copy hierarchy
6. Evidence and claim support
7. Compliance risk
8. Figma editability
9. Handoff clarity

Read `references/rubric.md` for the scoring rubric.

## Workflow

1. Inspect the submitted plan, document, or Figma output.
2. Score each image independently.
3. Score the six-image sequence as a set.
4. Lead with blocking issues.
5. Provide concrete fixes, not abstract advice.
6. If using Figma, inspect screenshots or metadata when available.

## Pass/Fail Rule

Fail the wireframe if any of these are true:

- Four or more images use the same layout skeleton.
- Photo placeholders say only `photo`, `image`, or `scene` without subject, angle, or use context.
- The first image does not communicate a supported differentiator.
- Copy and visual priority are unclear.
- The Figma output is a flat raster or not practically editable.
- Risky copy appears as a main claim without mitigation.
- Designer notes are mixed into the final artboard in a way that could be exported accidentally.

## Output Format

```markdown
# Wireframe QC

## Verdict
- Result: pass / needs-fix / blocked
- Main reason:

## Blocking Issues
| Severity | Image | Issue | Why It Matters | Required Fix |
|---|---|---|---|---|

## Image Scores
| Image | Role Clarity | Composition | Visual Hierarchy | Asset Direction | Copy Risk | Handoff Ready |
|---|---:|---:|---:|---:|---:|---:|

## Sequence Review
- Duplicated patterns:
- Missing purchase-stage coverage:
- Strongest improvement:

## Recommended Fix Plan
1.
2.
3.
```
