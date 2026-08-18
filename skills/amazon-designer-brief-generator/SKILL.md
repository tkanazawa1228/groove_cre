---
name: amazon-designer-brief-generator
description: Generate designer-ready production briefs for Amazon product creatives, especially six-image sub-image sets, from approved product information, review analysis, market research, layout patterns, Figma wireframes, and compliance notes. Use when Codex needs to create a handoff document with image roles, copy hierarchy, visual composition, photo/material directions, supplied and missing assets, tone, NG expressions, and production checklist for designers.
---

# Amazon Designer Brief Generator

Use this skill after the six-image strategy is approved or when the user asks for a designer handoff.

## Principle

The brief must let a designer start production without reinterpreting strategy. Keep strategy concise and make production instructions concrete.

## Required Inputs

- Product name and category
- Approved six-image plan
- Main and support copy
- Layout pattern per image
- Required assets and available assets
- Photo or AI-generation directions
- Brand tone
- Compliance/NG notes
- Delivery specs

If inputs are missing, include an `Open Questions` section rather than inventing.

## Brief Structure

Use `references/brief-template.md` as the output template.

## Figma Handoff Notes

When Figma frames exist:

- Link the Figma file/page if available.
- Reference frame names exactly.
- Keep designer notes outside final export frames.
- Identify which layers are placeholders and which copy is tentative.
- State that final copy may need client/legal review when claim-sensitive.

## Asset Instructions

Split assets into:

- Supplied assets to use as-is
- Supplied assets to combine or crop
- Assets to shoot
- Assets that may be AI-generated
- Assets that must not be AI-generated

For Amazon product images, do not instruct AI to generate exact product packaging, logos, official labels, certifications, or legally meaningful markings.
