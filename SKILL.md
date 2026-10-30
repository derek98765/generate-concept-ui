---
name: generate-concept-ui
description: Generate a concept UI image of one mobile screen (402x874) or one desktop screen (1920x1080) from an explicit description of its layout and content, in plain text or an ASCII layout. Reads the current project's design guidelines (design.md, token CSS, component library) so the concept matches the real UI, and attaches relevant screenshots from the project's ref/ folder as image references. Saves to ref/output/. Use when the user wants a concept UI, mockup or screen design image. Images only, never code; approved images go to image-to-code. Requires the image-gen skill.
---

# generate-concept-ui

Draw one concept UI image of a screen, from a description the user gives, in the
look of the current project. Images only. You never write app code here.

**Requires the `image-gen` skill.** It drives the Codex or Grok CLI. Follow its
instructions to pick the CLI, write the command, pass references and verify the
file. This skill only decides *what* to draw.

**Never add things that are not in the description.** No extra sections, cards,
badges, stats or features. Where the description leaves a detail open, fill it
with the most plain, project-consistent choice.

## Step 1 — Get the screen description

The user gives an explicit description of the screen's layout and content, in
plain text or an ASCII layout. If it is missing, or too vague to tell what goes
where, ask for it. Do not invent a screen.

Also settle the **format**:

| Format | Size | Aspect |
|---|---|---|
| Mobile | 402 × 874 px | about 9:19.5 |
| Desktop | 1920 × 1080 px | 16:9 |

Take it from the description or the user's words ("mobile", "desktop", "iPhone").
If still unclear, ask. One screen per image. For several screens, make one image
per screen.

### Example 1 — plain text (mobile)

> Mobile. Order history screen. Top bar with a back arrow, the title "Orders"
> centered, and a filter icon on the right. Below, a segmented control with
> "Active" (selected) and "Past". Then a vertical list of order cards. Each card
> has a thumbnail on the left, the restaurant name, item count and total price in
> the middle, a status label ("Preparing") on the right, and a "Track order"
> button under the text. Bottom tab bar with Home, Orders (selected), Account.

### Example 2 — ASCII layout (desktop)

```
Desktop. Team settings page.

+--------------------------------------------------------------+
| Logo        Dashboard  Projects  [Team]  Billing      (avatar)|
+--------------------------------------------------------------+
| Team settings                                                |
| Manage members and roles.                  [ Invite member ] |
|                                                              |
| [ Members ] [ Roles ] [ Danger zone ]                        |
| ------------------------------------------------------------ |
| Name            Email                 Role         Status    |
| Jane Cooper     jane@acme.com         Admin        Active    |
| Cody Fisher     cody@acme.com         Member       Invited   |
| Esther Howard   esther@acme.com       Member       Active    |
|                                                              |
|                          < 1 2 3 >                           |
+--------------------------------------------------------------+
```

ASCII boxes show structure and position. Labels in them are the copy to use.

## Step 2 — Read the project's design guidelines

The concept must look like it belongs to the real product. Before drawing, find
and read what the project already defines:

- design docs: `design.md`, `DESIGN.md`, a design-system or style-guide doc,
  `CLAUDE.md` / `AGENTS.md` notes on UI
- tokens: CSS variables / token CSS files, the theme file, the Tailwind config
  (colors, type scale, font families, spacing, radius, shadows, borders)
- the component library: which components exist (buttons, inputs, cards, nav,
  tabs, tables, modals, badges) and how they look and are used

Write a short **style brief** for yourself, with real values: palette as hex, font
families and the type scale, radius, border and shadow style, spacing feel, icon
style, and the look of the components this screen needs. Use the project's actual
components for the parts of the screen. Do not invent a new style, and do not
fall back to a generic or "AI" look.

If the project has no design guidelines at all, say so and ask whether to proceed
from the ref images alone or from a style the user describes.

## Step 3 — Pick references from the ref folder

Look for a `ref/` folder at the project root. It may hold two kinds of images:

- **Project screenshots:** the current product's real screens. These are the style
  source of truth: copy their look (colors, type, radius, spacing, component
  look).
- **External references** (for example Airbnb or Venmo screens from Mobbin): use
  these for layout and interaction patterns only. Never copy their brand, colors,
  logos or copy into the concept.

Open the images and pick the **few that are relevant to this screen**, roughly 2
to 4: same kind of screen, same components, or a layout pattern the description
calls for. Prefer project screenshots of similar screens first, then external
ones. Skip anything unrelated. Do not attach the whole folder.

Attach the picks as image references following `image-gen`: `-i` for Codex, and
absolute paths in the prompt for Grok. In the prompt, say what each reference is
for, for example "image 1 is the app's current style; image 2 is a layout
reference only". Grok downscales references to about 768px, so small text in them
will not survive. Describe anything fine-grained in words.

No `ref/` folder, or nothing relevant in it: continue with the style brief from
Step 2 alone.

## Step 4 — Generate

1. **Prepare the output folder.** Create `ref/output/` if it does not exist. Make
   sure `ref/` is untracked (see below).
2. **Write the prompt** in prose, following `image-gen`'s order. Cover: the format
   and aspect ratio (mobile tall 9:19.5, desktop 16:9), a clean full-bleed UI
   screen with no device frame or surrounding background, the layout and every
   piece of content from the description, then the style brief with its real
   values and the role of each reference. Use the description's text as the copy.
   Where copy is needed but not given, use short, plain, believable text in the
   project's voice. No lorem ipsum, no fake brand names.
3. **Run it** with `image-gen`, from the project root, saving to
   `ref/output/<screen>-<mobile|desktop>-v1.png` (short kebab-case screen name).
4. **Check the size.** Neither CLI reliably hits an exact pixel size. If the ratio
   already matches (desktop 16:9, mobile about 9:19.5), resize to the exact size
   with `sips -z <H> <W> <file>`. If the ratio is off, regenerate once with the
   ratio stated more firmly. If it is still off, keep the file and report the
   actual size. Do not stretch an image of the wrong ratio.
5. **Look at it** and check against the list below. Regenerate once if it clearly
   fails. Do not show a weak image and explain it away.

### Keep `ref/` untracked

In the project's git repo:

1. `git ls-files ref` shows whether anything under `ref/` is tracked. If so, run
   `git rm -r --cached ref` to untrack it. This keeps the files on disk.
2. `git check-ignore -q ref` tells whether `ref/` is ignored. If not, add `ref/`
   to the project's `.gitignore`.
3. Do not commit. Tell the user the index changed so they can review and commit
   it.

If the project is not a git repo, skip this.

### Check before showing

1. Everything in the description is present, and nothing else is.
2. Labels and text are readable and spelled as given.
3. Colors, type, radius, shadows and components match the style brief and the
   project screenshots.
4. The format and size are right, with no device frame.
5. Could a developer build it from the image using the project's tokens and
   components?

## Step 5 — Hand over and redo

Report the saved path, the actual pixel size, which CLI made it, which ref images
were attached and why, and anything that is off.

When the user asks for changes, make a new version (`-v2`, `-v3`). Never overwrite
an earlier one, and never crop or zoom an old image to make a new one. Pass the
previous version as a reference, state exactly what changes and what stays, and
keep the style brief. If the user supplies a corrected description, start from
Step 1.

Approval is the user's call. Once they approve an image, it can go to
`image-to-code` as the reference for building the screen.
