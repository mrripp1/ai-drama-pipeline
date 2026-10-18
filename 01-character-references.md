# Stage 1: Character Reference Sheets

Goal: a locked identity for each character that gets reused — never retype a character's description from scratch each scene; reference the locked sheet instead.

## Trait Lock format
Write one dense paragraph of specific, concrete traits per character. Vague traits ("tied back loosely") get reinterpreted inconsistently; specific traits ("sleek low ponytail, neatly tied at the nape, a few short strands loose at the front only") hold up.

Template:
> "[Age]-year-old [descent/ethnicity if relevant] [gender], [skin tone], [specific hair: color, style, length — be literal], [eye description], [1-2 distinguishing features: mole, scar, freckles], [signature wardrobe item or accessory], [build/posture note if relevant]."

## Two sheet types

**Turnaround sheet (body/angle):** one prompt, multi-panel grid, grey background, requesting front / 3-quarter / side / back views in one generation. This holds identity consistency far better than 4 separate generations, because the model isn't re-inferring the face from scratch each time.

**Expression sheet (emotional range):** same technique, multi-panel grid of the character's face showing the specific emotional beats needed for the season/episode (e.g., "determined," "shaken," "shocked"). Label each panel with the scene/beat name it's for.

Both should explicitly request: "plain grey background, numbered/labeled panels [or 'no panel numbers' if the user prefers clean panels], flat even studio lighting, photorealistic, identical lighting and proportions across all panels."

## If expression labels don't land
A vague expression ("determined") often renders as flat/neutral. Fix: make it more literal and intense ("intense furrowed focus, jaw set tight, eyebrows drawn down, unblinking direct stare — no softness in the expression"), same negative-constraint principle as elsewhere in this skill.

## Avoiding "prominent person" content-policy blocks
Photorealistic character generation occasionally lands close enough to a real person's likeness to trip identity-matching safety filters — ironically, generic/idealized "attractive lead" faces are *more* at risk than distinctive ones. If a character's reference image repeatedly triggers this block in later scenes (especially emotionally heavy ones):
1. First check whether it's actually a generation-mode issue (see troubleshooting.md) before assuming the face is the problem.
2. If it genuinely is the face, rebuild the trait lock with specific, unusual distinguishing features (an asymmetry, a small scar, an uneven feature) rather than just adding a "not a real person" disclaimer — the disclaimer alone is often not sufficient.

## When to build a new character's reference
Only when they're about to actually appear on screen — don't front-load reference sheets for a full season's supporting cast before they're needed, unless the show has a large ensemble cast appearing together early (in which case, lock the full ensemble before Episode 1 production begins).

## Consistency check after generating
For every reference sheet, check:
- Does the face/hair/wardrobe match the written trait lock, or did something drift (common: hair looser than specified, age reading older/younger than intended, accessory color changed)?
- Do the turnaround and expression sheets match *each other*, not just the text spec? (Two sheets generated separately can each individually look fine but subtly disagree with each other — check them side by side.)
- Is this character visually distinct enough from other characters in the cast to avoid confusion in multi-character scenes later?
