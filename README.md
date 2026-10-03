# humanlike-browser · 拟人浏览器交互

![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)
![AI-ready](https://img.shields.io/badge/AI--ready-llms.txt%20%7C%20SKILL.md-brightgreen)

> **Pass Cloudflare / "Verify you are human" checks (and bot-flagged forms) by driving the browser like a person — irregular mouse motion, no teleporting, move-before-click, natural typing.**

A ready-to-use AI skill (opencode / Claude Code / Cursor compatible) that encodes the input behavior that human-verification widgets actually score.

## Why

Cloudflare Turnstile, "Verify you are human" widgets, and many forms score **recent pointer + timing behavior**. A cursor that teleports and clicks in one frame reads as a bot; a cursor that glides in with jitter and pauses before clicking reads as a human. This skill makes Playwright-driven sessions look human — so legitimate automation stops getting flagged.

## What's inside

- `SKILL.md` — when to use, the 8 rules that actually matter, a ready example, and the scope/ethics boundary.
- `references/human-mouse.mjs` — reusable helpers: `humanMove`, `humanClick`, `humanType`, `idleMoves`, `jitter`.

## The rules (short version)

1. Never teleport the cursor — always `page.mouse.move(x, y, { steps })` first.
2. Irregular motion — random steps + pixel jitter, never the same curve.
3. Move → pause (~120–400 ms) → click.
4. 2–3 idle moves across the page before interacting.
5. Type with per-character delays instead of instant fill.
6. Randomize timing; don't hammer on failure.

## Install

### opencode
```bash
git clone https://github.com/everest-an/humanlike-browser-skill.git .opencode/skills/humanlike-browser
```

### Claude Code / Cursor
```bash
git clone https://github.com/everest-an/humanlike-browser-skill.git ~/.claude/skills/humanlike-browser
```

### Any AI / manual
Point the model at `SKILL.md` + `references/`.

## Usage (Playwright MCP)
Paste the example from `SKILL.md` into a `browser_run_code_unsafe` call, or `import` `references/human-mouse.mjs` in a Playwright script.

## Scope & ethics

Use this for **your own legitimate actions** on services you're entitled to use — submitting your own form, testing your own site, accessibility/QA automation. **Do not** use it to bypass protections for scraping, abuse, or credential stuffing; passing a bot check is not permission to do what the check was guarding. Prefer official APIs.

## License

MIT © 2026 everest-an
