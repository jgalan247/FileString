# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static HTML site for the **Edexcel GCSE Computer Science (1CP2) String Manipulation** unit. Six progressive lessons teach Python string functions and file handling, moving from fully scaffolded (Lesson 1) to fully independent (Lesson 6).

## Architecture

- **No build system, no framework** — plain HTML files served directly. Each lesson is a single self-contained `.html` file with inline `<style>` and `<script>` blocks.
- `index.html` — landing page with lesson grid; links to `lesson1.html` through `lesson6.html`. Contains branding for "Haute Vallee School - Dr Galan" in the title and hero section.
- Lessons share a consistent dark-theme design system via CSS custom properties duplicated in each file. **Note:** `index.html` uses `--accent1` through `--accent6`, while lesson files use shorthand names (`--accent`, `--accent2`, `--accent3`). Both share `--bg`, `--card`, `--text`, `--muted`, `--mono`, `--body`.
- Fonts loaded from Google Fonts: Space Mono (code/UI) and Nunito (body text).
- Code blocks use manual syntax-highlighting spans: `.kw` (keywords), `.fn` (functions), `.str` (strings), `.cm` (comments), `.num` (numbers), `.var` (variables).

## Lesson Structure

Each lesson HTML file follows the same pattern:
1. **Nav bar** — sticky, links to index and adjacent lessons
2. **Hero** — lesson badge, title, description, support level indicator
3. **Objectives** — checklist of learning goals
4. **Interactive activities** — mix of: match game, code blocks with copy button, fill-in-the-blanks, multiple-choice quiz, memory card game
5. **Bottom nav** — links back to index and to next lesson

All interactivity is vanilla JS within a `<script>` block at the bottom of each file. Activity types and their JS patterns:
- **Match game**: click term → click definition, `data-pair` attributes for pairing
- **Quiz**: `answer(el, qid, correct)` function with inline `onclick` handlers; correct answer indicated by `true` parameter
- **Fill-in-the-blanks**: `<input>` elements with `data-ans` attributes; `checkFill()` validates
- **Memory game**: dynamically built card grid from a `memPairs` array
- **Code blocks**: `copyCode(btn, id)` copies `<pre>` content to clipboard

## Scaffolding Progression

Lessons 1–2 provide full code; Lessons 3–4 have partial code with gaps/bugs; Lessons 5–6 provide minimal or no code. The support level is indicated by colored pills (green → yellow → red).

## Key Constraints

- **No shared CSS/JS files.** Every lesson duplicates styles and scripts. Changes to shared patterns (nav, quiz logic, memory game, code copy, color variables) must be applied to each affected file individually.
- `lesson6.html` exists in the file listing but may lack some interactive activity types present in earlier lessons (by design — minimal scaffolding).
- Quiz feedback messages are hardcoded per question per lesson. Each lesson's `answer()` function contains its own `msgs` object with feedback strings.
- Fill-in-the-blank answers support alternatives via the `alt` array in the `blanks` config.

## Development

Open `index.html` directly in a browser — no server required. To preview changes, refresh the browser.
