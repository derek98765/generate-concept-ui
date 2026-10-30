# generate-concept-ui

A Claude Code skill that generates a concept UI image of one screen, from an
explicit description of its layout and content (plain text or an ASCII layout).
Images only. It never writes code.

- **Formats:** mobile 402 x 874 px, desktop 1920 x 1080 px.
- **Style:** read from the current project (design docs, token CSS, component
  library), so the concept matches the real UI.
- **References:** picks a few relevant screenshots from the project's `ref/`
  folder (its own screens, or external ones such as Mobbin) and attaches them to
  the image prompt.
- **Output:** `ref/output/<screen>-<mobile|desktop>-v1.png`. Creates the folder if
  needed and untracks `ref/` in git.

Approved images go to the `image-to-code` skill.

## Prerequisites

- The [`image-gen`](https://github.com/derek98765/image-gen) skill, which makes
  the images through the Codex CLI or the Grok CLI.

## Installation

Lives in the opstack repo as a submodule at `skills/generate-concept-ui`;
`~/.claude/skills` points at `opstack/skills`, so there is nothing to install. To
use it standalone, clone `https://github.com/derek98765/generate-concept-ui.git`
into `~/.claude/skills/generate-concept-ui`.
