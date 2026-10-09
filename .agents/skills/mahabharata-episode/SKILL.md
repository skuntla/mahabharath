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

**Stage B — Illustration Director (only on explicit scene request):** Generate exactly **ONE** full-frame 3:4 illustration per tool invocation/request, from one scene entry in `scenes.json`. Never ask the generator to illustrate all scenes, a storyboard, grid, comic, contact sheet, or captioned panels. Include a negative instruction: 'single full-bleed illustration; no text, labels, numbers, frames, borders, inset panels, split screen, collage, or montage.' Check the image against the approved references and scene; record its status and only then proceed to another scene on user request. If generated image is wrong, don't silently generate another storyboard. Don't promise automatic binary GitHub upload without confirmed access to the image bytes and successful commit.

**New-character gate:** If Stage A identifies a new important character, create their profile and reference-sheet prompt and ask approval of the resulting reference sheet before Stage B scenes featuring them. Background unnamed extras are exempt.

**Reusable user commands:** 'Plan Mahabharata Day N' (Stage A), 'Approve Mahabharata Day N story and scenes', 'Illustrate Mahabharata Day N Scene M' (Stage B), 'Resume Mahabharata Day N', and 'Publish Mahabharata Day N' (only after verification).

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
- Ask for approval if user wants story-first review; otherwise proceed to visuals only if all cast references are approved.

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
If a day already exists, inspect its manifest and assets and resume from the first incomplete stage. Preserve approved story and images. Do not regenerate all eight merely because one failed.

## Important limitations
GitHub can store PNG/JPG/WebP, but retrieval of a GitHub image by a text connector does not guarantee it can be passed to the image generator. If the image is inaccessible in the generation context, ask the user to attach the approved image or use a supported retrieval path. Approval of a visual direction is not approval of every new character or scene.
