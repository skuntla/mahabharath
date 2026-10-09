---
name: mahabharata-episode
description: Produce continuity-safe, child-friendly Mahabharata episodes with approved recurring character references, new-character approval gates, individual illustrations, and GitHub delivery.
---

# Mahabharata Episode Production Skill

## Activation
Use when asked for "Day N", "next story", "Day N images", character design, revise an episode, or publish an episode in this repository. This is a reusable workflow, not an automatic background job. Do not claim an image was generated, uploaded, or committed unless verified.

## Source of truth (read before work)
1. `docs/SERIES-BIBLE.md`, `docs/STORY-GUIDELINES.md`, `docs/VISUAL-STYLE.md`, `docs/EPISODE-PLAN.md`.
2. `characters/README.md` and all profiles for today's cast; load actual approved image files, not just Markdown.
3. The previous 1–3 episodes and today's `episodes/day-NNN/manifest.json` if it exists.
4. This skill's `references/PRODUCTION-CHECKLIST.md`.
Do not infer episode completion from a README; verify required files and manifest.

## Two-stage workflow (mandatory)

**Stage A — Story Director (default for a new day):** Read continuity, identify cast, draft the story and decide the *story-driven* number of scenes (usually 5–10, not fixed at eight). Write `story.md`, `plan.md`, and `scenes.json` with one detailed prompt per scene. No image generation in this stage. Present story, scene list, new-character approvals, and a copyable next-command prompt. Wait for approval.

**Stage B — Illustration Director (one user approval for all scenes):** On 'Approved. Generate all Day N illustrations', process the approved scenes sequentially without requiring the user to send one message per scene. For each image-generation operation, request exactly **ONE** full-frame 3:4 illustration from exactly **ONE** scene entry in `scenes.json`; never combine scene prompts in a single image request. Do not ask the generator to make a storyboard, grid, comic, contact sheet, captioned panels, or multi-scene montage. Include: 'single full-bleed illustration; no text, labels, numbers, frames, borders, inset panels, split screen, collage, or montage.' Check each image against approved references and its scene before advancing; retry only the failed image when appropriate. Generate a separate cover only when planned. Continue through the remaining scenes within the same user request **when tool availability permits**. If tool limits, a failed call, or inability to supply essential character reference images prevents completion, stop, record the exact stage, and tell the user what remains. Never claim all images were generated or uploaded when they were not. Do not promise automatic binary GitHub upload without confirmed access to image bytes and a successful commit.

**New-character gate:** If Stage A identifies a new important character, create their profile and reference-sheet prompt and ask approval of the resulting reference sheet before Stage B scenes featuring them. Background unnamed extras are exempt.

**Primary two-message user flow:** (1) 'Plan Mahabharata Day N' → present story, cast, scene plan and any new-character approval requirements; (2) 'Approved. Generate all Day N illustrations' → generate each scene independently in sequence, review, save and publish what is technically possible. Optional commands: 'Illustrate Mahabharata Day N Scene M' for one-scene corrections, 'Resume Mahabharata Day N' for interruptions, and 'Publish Mahabharata Day N' after assets exist. Additional user approval is required only for important new characters or requested story changes.

## Episode planning
- Determine day number from the request. If "next", find latest approved/completed day; if ambiguous, ask.
- Establish exact narrative boundary: previous ending, today's single main event, tomorrow's teaser.
- Check chronology and primary-story fidelity. Separate later retelling variants from core account. Do not invent canonical facts.
- Identify all characters with visible or speaking roles; classify as recurring approved / existing unapproved / new / background.
- Create `episodes/day-NNN/plan.md` with cast, continuity notes, scene beats, and source/variant notes where relevant.

## Character gate — mandatory before final images
- For every recurring character, locate the approved master reference image and profile; use the actual reference image as input to image generation where supported. Do not claim a GitHub URL alone is automatically loaded into the image model.
- For each important NEW character: write `characters/<slug>/profile.md` (identity, approximate age, role, appearance, clothing, accessories, palette, expressions, relationships, age changes, forbidden drift); produce a character reference sheet with front/side/back views and expressions; save to `characters/<slug>/reference-v1.png`; mark `pending_approval`; request user approval before story-scene images featuring them.
- If a character exists but has no approved reference, treat as pending; don't silently improvise. Minor unnamed background figures need no individual reference unless recurring.
- When character ages change, create a linked age-specific approved reference and preserve recognizable facial structure.
- Do not overwrite approved character assets; version replacements and record approval.
- Canonical initial sheet (approved by user): `characters/file_00000000133081f583355f4f792cfb0d.png`, featuring Shantanu, Ganga, young Devavrata, adult Bhishma. See `docs/VISUAL-STYLE.md`. Individual portraits are optional until needed; sheet remains source of truth.

## Story
- Draft `episodes/day-NNN/story.md`: title, 450–650 word target / ~5–7 minutes spoken (adjust naturally), one principal event, vivid age-appropriate narration, clear emotional stakes, no graphic violence, one nuanced moral, two open-ended reasoning questions, next-day teaser.
- Avoid revealing future plot prematurely; do not introduce characters before their narrative entrance.
- Review for accuracy, timeline, name spelling, continuity, accessible vocabulary, pacing and respectful cultural framing.
- Always pause for story and scene-plan approval before Stage B. Do not start illustrations during Stage A.

## Visual production
- Produce a story-driven scene list of meaningful story beats (often 5–10). Each scene has unique composition, location, cast, emotion, action, lighting, and camera framing.
- 3:4 portrait, one distinct illustration per file, no collage, no text/watermark. Warm premium cinematic animated Indian mythology storybook style, believable anatomy.
- Load relevant approved image references as actual images whenever the tool permits; if not possible, disclose limitation and ask for the image rather than promising exact consistency.
- Create `cover.png` and `images/01.png` … up to the approved scene count, avoiding redundant regenerations. Generate each image independently.
- Inspect every image: identity, wardrobe, scene fidelity, anatomy, no text, framing, safety, duplicate detection. Regenerate only failed images.
- Do not mark images complete until actual image files are committed.

## Packaging and publishing
- Store `plan.md`, `story.md`, `manifest.json`, `cover.png`, `images/NN.png` in `episodes/day-NNN/`.
- Update `manifest.json` statuses: planned → character_pending → story_draft → story_approved → images_in_progress → review → complete. Do not skip gates or fabricate approvals.
- Manifest records cast reference paths, story scope, scene list and output paths, approvals, outstanding issues, and next-day handoff.
- Commit text and binary assets to GitHub only after confirming actual files exist; verify the commit and paths. Never claim an upload succeeded based only on an intention.
- Update `docs/EPISODE-PLAN.md` only for agreed changes; avoid spoilers in user-facing episode text.
- Return concise summary of what was completed, links, what needs approval, and next action.

## Recovery
If a day already exists, inspect its manifest and assets and resume from the first incomplete stage. Preserve approved story and images. Do not regenerate every scene merely because one failed.

## Important limitations
GitHub can store PNG/JPG/WebP, but retrieval of a GitHub image by a text connector does not guarantee it can be passed to the image generator. If the image is inaccessible in the generation context, ask the user to attach the approved image or use a supported retrieval path. Approval of a visual direction is not approval of every new character or scene.
