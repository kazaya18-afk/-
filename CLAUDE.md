# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Single-file static HTML demo for a Japanese bank's online address change procedure (住所変更手続き). No build system, no dependencies, no package manager — open `index.html` directly in a browser.

## Architecture

Everything lives in `index.html` as one self-contained file: CSS in `<style>`, markup in `<body>`, and JS in `<script>`.

### 4-screen wizard flow

Navigation is controlled by `goTo(n)` — it hides all `.screen` divs and shows `#screen-{n}`, then calls `updateSteps(n)` to sync the progress indicator.

| Screen | ID | Purpose |
|--------|----|---------|
| 1 | `#screen-1` | Personal info input (本人情報入力) |
| 2 | `#screen-2` | JPKI identity verification (マイナンバーカード読取) |
| 3 | `#screen-3` | Confirmation & submission (確認・送信) |
| 4 | `#screen-4` | Completion (申請完了) |

### JPKI simulation (Screen 2)

`startJPKI()` simulates the My Number Card read with a 2.2s `setTimeout`, then reveals `#jpki-result` (identity confirmed + new address retrieved). `resetJPKI()` hides the result panel for demo replay.

### CSS conventions

- Brand blue: `#0D3B8C`
- Success green: `#16A34A`
- All layout via CSS Grid (`field-grid`) and Flexbox
- `.filled` class on inputs = pre-populated demo data (blue tint)
- Responsive breakpoint at 480px: single-column grid, reduced padding

## Deployment

Hosted via GitHub Pages. No build step needed — `index.html` is served as-is.
