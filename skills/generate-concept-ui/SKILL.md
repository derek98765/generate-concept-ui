---
name: generate-concept-ui
description: Draw design images for websites and mobile apps, then redo them until the user approves. One image per web section or app screen, one locked style across the set. Use when the user wants UI design images, mockups, screens, a landing page design, an app flow, design directions to pick from, or a redo of one screen. Images only — it never writes code. Approved images go to image-to-code.
---

# generate-concept-ui

You draw UI design images. The user judges them. You never write code here.

The flow is:

```
directions → user picks → full set → user asks for redos → user approves → image-to-code
```

Images are made with the `image-gen` skill. Pass earlier images as references
(`-i`) whenever the style must match — words alone drift.

## The 5 mistakes to avoid

These are the mistakes image models make most. Check every image for them.

1. **Left text, right image by habit.** It is the most overused AI layout. Use it
   only when it is clearly the best choice, and never twice in a row.
2. **A crowded first screen.** The hero or first app screen gets one focal point, a
   short headline (1–3 lines), short support text and one clear action. No pills,
   fake stats, badges, tiny logos or labels like "00 orchestration layer".
3. **Boxes inside boxes.** No cards inside cards inside a big rounded wrapper. Use
   space and alignment instead. Each box needs a reason.
4. **The AI look.** No purple-to-blue gradients, glowing edges, floating blobs,
   glass for no reason, fake chart dashboards, rows of identical stat cards.
5. **Too few images or tiny text.** One section or screen per image. Never pack a
   whole page into one image. If text looks small, the image is not done.

## Step 1 — Read the brief and pick the mode

- Website, landing page, marketing site → read `references/web.md`.
- Mobile app screens or flows → read `references/mobile.md`.
- Both → read both.

The user's brief always wins over the defaults in these files. Do not ask questions
when a strong reading of the brief is possible.

Pick a project name (short, kebab-case). All files go in `design/<name>/` at the
project root:

```
design/<name>/
  style.md          the locked style
  drafts/           every image you make, never deleted
  approved/         only what the user approved
```

## Step 2 — Offer directions

For a new design with no locked style, first make **2 or 3 clearly different
directions**, one image each (the hero or first screen). Different means different
theme, type and layout — not three shades of one idea. Save them as
`drafts/dir-a.png`, `dir-b.png`, `dir-c.png`, say in one line what each one is, and
let the user pick.

Skip this step when:
- the user already picked a direction or gave reference images, or
- `style.md` already exists, or
- the user asks for the full set straight away.

**The user's own images** (Figma exports, screenshots, other tools) are welcome as
the starting point. Pass them as references and ask what to keep from them if it
is not obvious.

## Step 3 — Lock the style

Once a direction is picked, write `design/<name>/style.md`. Keep it short:

- mode (web / iOS / Android / neutral mobile)
- palette: primary, secondary, one accent, neutrals — with hex values
- type: heading and body style, weights, rough scale
- corner radius, border and shadow use
- spacing feel (airy / medium) and section gap
- icon style, image style (photo grade, crops, texture)
- the picked direction file, used as the style reference for every later image

From now on every image follows `style.md` and passes the picked direction image
(and any approved images) as references.

## Step 4 — Make the full set

- One image per web section or app screen. Say the count first ("Making 6 images,
  one per section"), then label each one ("Section 2 of 6: Features").
- Do not stop early. Do not skip sections.
- Save as `drafts/<nn>-<part>-v1.png`, e.g. `drafts/02-features-v1.png`.

## Step 5 — Redo until approved

Show the images and wait. When the user asks for changes:

- Redo **only** the image they named. Save it as the next version (`-v2`, `-v3`);
  never overwrite.
- Keep the style locked. Pass the style reference and any approved images.
- If the user wants a style change for the whole set, update `style.md` first and
  say what changed.
- **Never crop or zoom into an old image** to make a new one. Cropping breaks
  spacing and type sizes. Make a fresh image of that part instead.
- If the user likes one image and wants the rest to match it, use that image as the
  new style reference.

## Step 6 — Approve

Approval is the user's call only. When they say "approve 1, 3, 5" (or move files
into `approved/` themselves):

1. Copy each approved image to `approved/` with a clean name: `01-hero.png`.
2. Write `approved/design-spec.md` from `style.md` plus what you see in the approved
   images: palette (hex), fonts, type sizes, spacing, radius, buttons, section
   order. This is what `image-to-code` follows.
3. Tell the user the set is ready for `image-to-code`.

## Shared rules (web and mobile)

**Pick a direction and commit.** For each set choose one theme, one type character,
one layout system and one image style (lists are in the mode files). Write them in
`style.md`. Strong and clear beats safe and mixed. Do not mash styles together.

**Layout**
- Vary layout between sections or screens: alignment, image-to-text ratio, density,
  background. Never let the page feel like one block repeated.
- Keep spacing even and generous. Calmer sections between busy ones.
- Fewer, stronger containers. Open layouts over framed ones.

**Type**
- Clear size contrast and reading order. Short headlines.
- Medium or light weights with tight tracking read as premium; bold shouting
  everywhere does not.
- No gradient text, no all-caps everywhere, no more than two font moods.

**Color**
- One palette for the whole set: one primary, one secondary, one accent used
  sparingly, plus neutrals. No theme swap between sections.
- Soft, low-color gradients that match the palette are fine (ink to graphite, cream
  to sand). Rainbow, mesh, purple-blue and pink-orange gradients are not.

**Images**
- Images are a main design material, not decoration. Use art-directed photos,
  product shots and crops; use them as full backgrounds when the brief allows.
- Keep image sizes and crops consistent across similar blocks.
- Text over an image needs a scrim, fade or mask so it stays easy to read.
- No stock-photo clichés, random scenery or tiny filler thumbnails.

**Copy**
- Short, believable, specific. Real button labels.
- Banned words: unleash, elevate, revolutionize, next-gen, seamless, transform,
  unlock your potential.
- No fake brands like Acme, Nexus, Flowbit, NovaCore. No lorem ipsum.
- Image models garble text. Keep text short so it renders cleanly; the exact copy
  gets fixed in code later.

**Consistency.** Every image must look like the same product: same palette, type,
radius, buttons, icons and image treatment. Only layout and emphasis change.

## Check before showing

1. Any of the 5 mistakes above? Fix them first.
2. Is the count right — one image per section or screen?
3. Is every bit of text comfortably readable?
4. Do all images clearly belong together?
5. Could a developer build it from the image?
6. Does it look designed, not like a template?

If an image fails, make it again. Do not show a weak image and explain it away.
