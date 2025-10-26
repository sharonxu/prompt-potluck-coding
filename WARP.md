# WARP.md

This file provides guidance to WARP (warp.dev) when working with code in this repository.

## Repository type
This is a content-first repository for sharing AI coding prompts, workflows, and templates from "Prompt Potluck @ Homebrew: Coding Edition." It primarily contains Markdown resources organized by topic, plus occasional self-contained examples.

## Commonly used commands

Clone and branch:
```bash
git clone https://github.com/sharonxu/prompt-potluck-coding.git
cd prompt-potluck-coding
git checkout -b feat/<short-topic-or-title>
```

Add a new resource using the template:
```bash
# Pick the right directory (see sections below), then:
cp TEMPLATE.md <topic-dir>/YYYY-MM-DD-<brief-title>-by-<your-handle>.md
git add <topic-dir>/YYYY-MM-DD-<brief-title>-by-<your-handle>.md
```

Add .gitkeep to any new directories you introduce:
```bash
mkdir -p <new-dir>
touch <new-dir>/.gitkeep
git add <new-dir>/.gitkeep
```

Preview structure (if `tree` is available):
```bash
tree -a -I .git
```

Git commit/push and open a PR:
```bash
git add .
git commit -m "feat(<topic>): add <brief title> by <your handle>"
git push -u origin HEAD
# If GitHub CLI is available:
gh pr create --fill
```

## Big-picture repo architecture

Top-level topics:
- **evals-and-observability** — Evaluation methods, observability dashboards/logging, continuous monitoring patterns.
- **best-practices** — Guardrails and workflows that maintain software quality during AI-assisted coding.
- **tool-specific** — Subfolders for particular tools:
  - claude-code
  - warp-terminal
  - cursor
  - roo-cline
- **debugging-strategies** — Tactics to reduce hallucinations, improve output quality, avoid agent loops.
- **system-prompts** — System prompts and templates (e.g., `.cursor/rules`, `CLAUDE.md`, project configs). Keep original filenames and add a short Markdown explainer for context.
- **production-apps** — Patterns for building production-ready, scalable web/mobile apps with AI-assisted coding.
- **frontend-design** — Practical guidance for attractive, maintainable UIs beyond "vibe-coded" designs.
- **llm-comparisons** — Prompt sets, evaluation notes, and observations comparing LLMs/VLMs with versions/dates.
- **examples** — Self-contained sample projects or code snippets. Each example should include a local README.md.

Authoring flow:
- Use TEMPLATE.md for new contributions.
- Keep assets (images, attachments) near the Markdown that references them and use relative links.
- For system prompts or tool rules (e.g., `.cursor/rules`, `CLAUDE.md`), commit the actual files and include a brief README section explaining how/where they're intended to be used.

Notes:
- There is no build, lint, or test pipeline for this repository by default; the primary workflow is content authoring and review via PRs.
