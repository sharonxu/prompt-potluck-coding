# Prompt Potluck @ Homebrew: Coding Edition — AI Coding Prompts & Workflows

Share your favorite time-tested AI prompts and coding workflows from the Prompt Potluck @ Homebrew: Coding Edition. This repository collects prompts, templates, debugging tactics, evaluation approaches, system prompts, and real-world examples so attendees (and the wider community) can learn from each other.

Event page: https://luma.com/m5qrp9fq

## Who is this for?
- Attendees and community members who want to share AI coding prompts, workflows, and templates
- Practitioners comparing tools (Claude Code, Warp Terminal, Cursor, Roo Cline) and LLMs/VLMs
- Builders who want production-minded strategies for AI-assisted development

## How to contribute

We use a standard fork-and-PR workflow.

1) Fork the repo on GitHub to your account.

2) Clone your fork:
   ```bash
   git clone https://github.com/<your-username>/prompt-potluck-coding.git
   cd prompt-potluck-coding
   ```

3) Add the upstream remote (optional but recommended):
   ```bash
   git remote add upstream https://github.com/<upstream-owner>/prompt-potluck-coding.git
   git fetch upstream
   ```

4) Create a feature branch:
   ```bash
   git checkout -b feat/add-<short-topic-or-title>
   ```

5) Add your contribution using TEMPLATE.md:
   - Choose the best directory for your topic (see Directory structure below).
   - Copy the template and rename it using our naming convention:
     ```bash
     cp TEMPLATE.md <topic-dir>/YYYY-MM-DD-<brief-title>-by-<your-handle>.md
     ```
   - If you include images/assets, put them alongside your file (e.g., `<topic-dir>/images/`) and use relative links.

6) Commit and push:
   ```bash
   git add .
   git commit -m "feat(<topic>): add <brief title> by <your handle>"
   git push -u origin feat/add-<short-topic-or-title>
   ```

7) Open a Pull Request from your branch to the main repo.
   - Clearly describe the problem/use case, approach, and any model/tool versions.
   - Link to external references if applicable.

Tip: Keep one focused contribution per PR.

## Directory structure

- `/evals-and-observability/` — Agent evals, observability, and continuous monitoring patterns
- `/best-practices/` — Ensuring SD best practices during AI-assisted coding
- `/tool-specific/`
  - `/claude-code/` — Patterns, prompts, and workflows specific to Claude Code
  - `/warp-terminal/` — Terminal-centric AI workflows (Warp)
  - `/cursor/` — Cursor rules, workflows, and templates
  - `/roo-cline/` — Roo Cline workflows and patterns
- `/debugging-strategies/` — Reduce hallucinations, improve output quality, avoid loops
- `/system-prompts/` — System prompts, templates (.cursor/rules, CLAUDE.md, project configs)
- `/production-apps/` — Using AI-assisted coding for production-ready, scalable apps
- `/frontend-design/` — Creating visually appealing frontends that don't look "vibe-coded"
- `/llm-comparisons/` — Strengths and weaknesses of LLMs/VLMs (e.g., Sonnet 4.5, Opus 4.1, Gemini, Grok, ChatGPT, Qwen, DeepSeek-R1/V3)
- `/examples/` — Real-world code examples and sample projects

Each empty directory contains a `.gitkeep` to ensure it's tracked by Git.

## Contribution guidelines

### File naming
- Use kebab-case with a date prefix and your handle.
- Format: `YYYY-MM-DD-brief-title-by-your-handle.md`
- Example: `2025-10-26-reliable-code-refactors-by-alex.md`

### Content format
- Start from TEMPLATE.md and fill out all sections (Title, Author, Date, Topic(s), Problem/Use Case, Solution/Strategy, Example, Notes).
- Include model and tool versions explicitly (e.g., "Claude 3.5 Sonnet (2025-10), Cursor v0.45").
- For system prompts, include the exact prompt file and a short note on intended scope and limitations.
- For LLM comparisons, include prompts, versions/dates, and any evaluation method (manual notes or links to scripts).
- For debugging strategies, show the before/after and when to apply the tactic.
- For examples or sample projects, keep them self-contained under `/examples/<project-name>` with a local README.md.

### Assets
- Place images or attachments near your Markdown file (e.g., a sibling `images/` folder).
- Use relative links so previews work in GitHub UI.

### Attribution
- Add your name or handle in the Author field. If adapting others' work, credit and link to sources.

### Notes for agent/orchestration workflows
- If your example uses agent orchestration (e.g., crewai) or Dockerized MCP servers, add a brief "How to run" snippet and any environment constraints (e.g., Python 3.12) in the Example or Notes section.

## Event topics covered

- AI agent evals, observability, and continuous monitoring
- Methods to ensure best SD practices during AI-assisted coding
- Best practices for Claude Code, Warp Terminal, Cursor, Roo Cline
- Tactics to reduce hallucinations and improve output quality
- Debugging and avoiding loops
- System prompts and templates (.cursor/rules, CLAUDE.md, project configs)
- Production-ready, scalable web and mobile apps
- Frontend best practices beyond "vibe-coded" UIs
- LLM/VLM strengths and weaknesses: Sonnet 4.5, Opus 4.1, Gemini, Grok, ChatGPT, Qwen, DeepSeek-R1, DeepSeek-V3

---

Questions? Open an issue or start a discussion thread with context and examples.
