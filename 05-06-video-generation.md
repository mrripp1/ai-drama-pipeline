# Stages 5-6: Video Generation and Single-Shot Scenes

## Core principle
Every video prompt uses the matching picture draft as the **starting frame/reference image**. The prompt text should describe **only what changes** — motion, camera movement, action — never re-describe appearance, wardrobe, or environment, since those are already locked by the starting image. Re-describing them in the video prompt is redundant at best and reopens drift risk at worst.

## Prompt template
> "[Specific action/motion, described literally — not vague], [camera instruction: static / push-in / pan / handheld, pick one primary instruction not several], [any dialogue delivery note — mouth movement only if captions carry the actual text, see below]."

## Duration and compression reality
Video generation is **temporal, not spatial** — a single generation produces one continuous clip with a hard duration cap (commonly ~8 seconds, sometimes up to ~15 depending on the tool). Unlike picture drafts, there is no equivalent of "cram 10 scenes into one generation" for video — if the user asks for this, explain the constraint clearly rather than attempting it. The available compression is **grouping 2 adjacent beats that share a camera setup into one continuous clip** (e.g., an exchange of dialogue shown as one continuous shot-reverse-shot-free take) — this is real compression but trades generation *count* for generation *difficulty*: combined clips need the model to handle an internal transition, which usually needs more regeneration attempts than a single clean beat would.

## Dialogue without lipsync
For fast-paced short-form content, captions carrying the dialogue text (with mouth movement only, no synced audio) is often a better fit than full voice+lipsync — it's simpler to produce, avoids lipsync-matching failures, and is a well-established convention in the genre, not a downgrade. Reserve full voice/lipsync for scenes that specifically need vocal performance (a confrontation, a line where tone of voice matters more than the words alone).

## Motion complexity hierarchy (hardest to easiest for current video models)
1. **Hand/finger-specific motion** (typing, thumb-tapping, intricate gestures) — hardest, budget extra attempts.
2. **Walking/gait cycles** — a common failure point; use literal gait language ("even walking gait, both feet alternating naturally") plus a negative constraint against awkward mid-step poses if a first attempt looks stiff or wrong.
3. **Multi-character interaction** (physical contact, synchronized reactions) — moderate difficulty, test early in a sequence since it affects later shots.
4. **Single-character static/held emotional beats** — most reliable, good candidate for single-shot technique (below).
5. **UI/screen-only motion** (counters incrementing, notifications sliding in) — most reliable of all, no character physics involved.

## Single-shot technique (Stage 6)
For a contained, static beat (a phone-screen insert, a held emotional close-up, a line delivered to camera): no camera movement, no scene changes mid-shot, one character reference as anchor, one simple instruction. Resist over-directing these — simple instructions hold up far more reliably than layered cinematic language for a single continuous shot.
