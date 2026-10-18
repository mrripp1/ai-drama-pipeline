# Stage 4: Picture Drafts

Goal: generate one still image per scene/beat before any video generation — this is the cheapest point in the pipeline to catch a wrong outfit, wrong location mood, or wrong character positioning.

## Prompt template
> "[Character reference(s) — attach image and/or restate trait lock], [action/pose from the script beat], [environment], [visual style per the Series Bible: lighting, palette], [expression matching the beat's emotional register]."

Always feed the actual locked character reference **image** in alongside text, not text alone — text-only matching is noticeably less reliable for holding identity.

## Choosing a generation strategy

Several techniques exist; pick based on the tool's actual capabilities (test small before committing) and the user's credit/time constraints:

**One prompt per scene (most reliable, most generations needed):** full control per scene, easiest to debug when something's wrong, but doesn't scale well to many scenes under a tight generation budget.

**Multi-panel grid (one image, several panels):** works well for *spatially* combinable content — character reference sheets, or a handful of scenes that share the same location/characters. Tested limit before quality degrades is roughly 3-4 panels; pushing to 8-10 panels in one image is possible but risks lower per-panel detail and a harder consistency task for the model (more characters/locations to juggle at once) — test on a small batch before committing a whole episode to this approach.

**x4 / multi-variation generation (if the tool supports it):** generates several independent *takes* of the **same single prompt** — this is a quality-control tool, not a way to get multiple different scenes from one submission. Use it to generate 4 candidates of one scene and pick the strongest, rather than committing to the first result. Don't confuse this with the grid technique above; they solve different problems (variation count vs. scene count).

**Batching multiple scenes into one multi-variation submission:** some tools can be instructed ("Image 1 is X, Image 2 is Y...") to map each output slot to a different described scene instead of 4 variations of one scene — this is **not guaranteed to work**, since it depends on whether the specific tool respects per-slot instructions. Test it on 2 scenes first before assuming it'll scale to the whole episode; if the outputs come back as blended/similar rather than matching their assigned scene, fall back to one-prompt-per-scene.

## Compressing without losing scene count
If the user wants fewer generations without losing scene coverage, the safest compression is pairing **adjacent beats that share the same camera setup or location** into a single grid/multi-panel prompt, rather than trying to cram unrelated beats together. Don't force a location/tone-shift beat (e.g., a cliffhanger in a new setting) into the same batch as unrelated earlier beats just to hit a round number.
