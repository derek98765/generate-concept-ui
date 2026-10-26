# generate-concept-ui

A Claude Code skill that draws UI design images for websites and mobile apps,
then redoes them until you approve. Images only — it never writes code.

- **Skill:** `generate-concept-ui` — offers 2–3 design directions, locks the one
  you pick in `style.md`, draws one image per web section or app screen, redoes
  only the images you name, and on approval copies them to `approved/` with a
  `design-spec.md` for the coding step.

## How it works

```
directions → you pick → full set → you ask for redos → you approve → code
```

Files go in `design/<name>/` at the project root:

```
design/<name>/
  style.md          the locked style
  drafts/           every image made, never deleted
  approved/         only what you approved, plus design-spec.md
```

Web rules live in `references/web.md` and mobile rules in `references/mobile.md`;
the skill reads only the one it needs.

## Prerequisites

- The [`image-gen`](https://github.com/derek98765/image-gen) skill, which makes
  the images through the Codex CLI or the Grok CLI.
- Optional: an `image-to-code` skill that builds the approved images in code.

## Installation

Claude Code loads skills from `~/.claude/skills/` (global, all projects) or
`.claude/skills/` (project-local). To install:

```bash
cp -r skills/generate-concept-ui ~/.claude/skills/
```

Or clone the repo and symlink the skill so `git pull` keeps it current:

```bash
git clone https://github.com/derek98765/generate-concept-ui.git ~/.claude/skills/.generate-concept-ui-repo
ln -s .generate-concept-ui-repo/skills/generate-concept-ui ~/.claude/skills/generate-concept-ui
```
