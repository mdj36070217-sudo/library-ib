# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This repository contains a single static HTML file (`gemini-code-1777511425052.html`) — an IB (International Baccalaureate) learner profile quest board designed for a school library setting. The UI is in Korean.

## No Build System

There is no package manager, build step, or test suite. The file runs directly in any browser. To preview:

```
open gemini-code-1777511425052.html        # macOS
xdg-open gemini-code-1777511425052.html   # Linux
```

Or serve with any static file server if needed:

```
python3 -m http.server 8080
```

## Architecture

The entire application lives in one HTML file with three sections:

- **Styling**: Tailwind CSS loaded from CDN (`cdn.tailwindcss.com`) plus a small inline `<style>` block for the `.secret-msg` / `.show` animation.
- **HTML**: A card-based layout (max-w-md) showing rank/score, a hidden secret mission area, and a form to log reading quests.
- **JavaScript** (inline `<script>`): Vanilla JS with no dependencies. State is persisted via `localStorage` (`ibScore` key). Core functions:
  - `updateUI()` — reads `totalScore`, updates rank display and badge icon, and reveals the secret message at ≥ 500 pts.
  - `addQuest()` — validates form inputs, increments `totalScore` by 100, persists to localStorage, and prepends a new list item.

## Key Domain Details

- **IB Learner Profiles** (dropdown): 탐구하는 사람, 지식이 많은 사람, 생각하는 사람, 소통하는 사람, 원칙을 지키는 사람.
- **Rank thresholds**: 0–299 pt → 🐣 수습 사서 / 300–599 pt → 📚 숙련된 사서 / 600+ pt → 👑 전설의 사서.
- **Secret mission** unlocks at ≥ 500 pt (shows a hidden `<div>` with class `show`).
- Each quest submission awards exactly 100 points.
