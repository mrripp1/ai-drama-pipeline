---
name: ai-drama-pipeline
description: Produce AI-generated short-form drama/film content end-to-end — character reference sheets, Series Bibles, episode scripts, picture draft prompts, and video generation prompts, plus troubleshooting for common AI generation failures (identity drift, content-policy blocks, environment inconsistency). Use this skill whenever the user wants to create an AI drama series, write a Series Bible, build character reference sheets for consistency, write picture-draft or video-generation prompts for scene production, or troubleshoot AI image/video generation problems like hair/face drift, wrong branding appearing in generated UI, environment mismatches between scenes, or content-policy blocks on otherwise-fine content. Also trigger for requests to plan a multi-episode anthology, build a production schedule around image/video credit limits, or batch multiple scenes into fewer generations (grids, x4 variation workflows).
---

# AI Drama Production Pipeline

A complete workflow for producing AI-generated short-form drama series (Filipino micro-drama, Western teen drama, telenovela-style — genre-agnostic), from concept through ready-to-generate prompts. Built from real production experience across multiple shows, including the specific failures encountered and how they were fixed.

## The 6-Stage Pipeline

```
1. Character Reference Sheets  →  2. Script  →  3. Series Bible
            ↓                                        ↓
            └──────────────→ 4. Picture Drafts  ←────┘
                                   ↓
                         5. Video Generation
                                   ↓
                         6. Single-Shot Scenes
```

Stages 1–3 can run in parallel; they converge at Stage 4, which is the cheap checkpoint — catch a wrong outfit, wrong tone, or wrong blocking as a still image before spending video generation credits on it. Stages 5–6 should describe **only what changes** (motion, camera) since appearance/environment are already locked by the Stage 4 image.

Full templates and detailed guidance for each stage are in `references/`. Read the relevant reference file before generating content for that stage — don't rely on summarized knowledge of the stage, the reference files contain the exact prompt patterns that have been tested to work.

- `references/01-character-references.md` — building locked, consistent character reference sheets
- `references/02-03-script-and-bible.md` — script format and Series Bible template
- `references/04-picture-drafts.md` — picture draft prompting, including batch/grid/x4 techniques
- `references/05-06-video-generation.md` — video/motion prompting
- `references/troubleshooting.md` — **read this whenever a generation fails, drifts, or looks wrong** — covers the specific failure patterns and fixes below

## Quick-reference: common failures and fixes

These are the highest-value lessons from real production — see `references/troubleshooting.md` for full detail on each:

1. **Identity drift (hair, face, wardrobe changing between scenes)** → add an explicit **negative constraint** naming the specific failure ("do NOT show hair loose or windblown"), not just a positive instruction. Positive-only instructions get overridden by action/weather/emotion cues in the same prompt.
2. **Real brand names, platform logos, or real place names appearing in generated UI or backgrounds** → always fictionalize up front (invented app names, invented street/company names) and add explicit negative constraints ("NO real platform name or logo") since the model defaults to realistic/recognizable options when a detail is left open.
3. **Environment mismatch between scenes meant to be continuous** → feed the previous scene's actual output image in as a reference for the next scene, not just matching text description. Text-only matching is not reliable for environment continuity.
4. **Content-policy block that seems unrelated to the actual content** → first check whether the real cause is simpler than the content itself: wrong generation mode (image vs. video), or a flagged reference image (a face that happens to resemble a real person). Test by removing the reference image or splitting the shot (e.g., separate a sensitive line of dialogue from a visible face) before concluding the described content itself is the problem.
5. **A soft/vague instruction not landing** ("determined expression" reads as neutral) → make it more literal and intense, and pair it with a negative constraint ruling out the flat/neutral result.
6. **A multi-panel or multi-scene generation blends/confuses similar-looking characters** → give each character a distinct, specific, named visual anchor (hairstyle, accessory) and state explicitly in the prompt which panel/image belongs to which character and scene — don't assume positional ordering alone is enough.

## Workflow for a new show

1. Interview the user (or extract from conversation) on: genre/tone, target audience, episode count, platform/format constraints (e.g., episode duration, credit limits).
2. Write the Series Bible first (`references/02-03-script-and-bible.md`) — this anchors every later decision.
3. Build character reference sheets for all leads who appear in Episode 1 (`references/01-character-references.md`). Don't build references for characters who haven't appeared yet — build them when needed, same as the pipeline does for scripts.
4. Write Episode 1's compressed beat script (short logline per beat, not full screenplay prose — picture drafts are built directly from these beats).
5. Write picture draft prompts per beat (`references/04-picture-drafts.md`), choosing single-scene, batched, or grid format based on the user's generation tool and credit constraints.
6. Write video generation prompts per picture draft (`references/05-06-video-generation.md`), motion/camera only.
7. For episodes beyond the first, a compressed logline-level season outline is usually sufficient until the user is ready to produce that specific episode — don't fully script 20+ episodes in one pass unless explicitly asked.

## Tone for responses in this domain

Be a collaborative production partner, not just a prompt generator: flag inconsistencies the user might not have caught (wardrobe drift, environment mismatches, expressions not matching the written beat), explain *why* a fix works rather than just applying it, and be honest when something is genuinely unproven or a trade-off rather than presenting speculation as fact. When a generation fails, diagnose before re-prompting blindly — isolate the variable (reference image vs. wording vs. generation mode) rather than changing everything at once.
