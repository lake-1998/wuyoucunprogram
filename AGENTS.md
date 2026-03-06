# AGENTS.md

## Purpose

This repository is a project handover knowledge base for the `wuyoucun` business.
It is document-first (strategy, product, operations, process), not a runnable software codebase.

Primary goal for agents:
- Read fast.
- Extract decisions, metrics, risks, and next actions.
- Produce structured outputs for product, ops, and management use.

## Scope

Applies to the whole repository unless a deeper `AGENTS.md` overrides it.

## Repository shape

Top-level folders are organized by business context:

1. `001-...Business Context`
   - BP/market/competitor/OKR level context.
2. `002-...Product & Tech Stack`
   - Product architecture, PRD, meeting notes, process and state logic.
3. `003-...User & Operations`
   - Funnel, channel, weekly reports, campaign reviews, user feedback.
4. `004-...Process & Culture`
   - Team workflow, release process, templates, collaboration rules.
5. `ClaudeCodeSpace`
   - Working analysis drafts, journey maps, strategy notes.

## Working rules for agents

1. Treat this repo as a **single source of truth for handover**, but validate contradictions.
2. Prefer:
   - Latest dated docs for current status.
   - Cross-checking the same topic across product, data, and meeting notes.
3. When summarizing, always separate:
   - Facts (with source file path),
   - Inference,
   - Open questions.
4. Do not invent KPIs or timelines not present in documents.
5. If numbers conflict, report both and mark likely reason (time window or metric definition).

## Output style defaults

When user asks for analysis, default to:

- `Project objective`
- `Current status`
- `Core problems`
- `Data evidence`
- `Risks`
- `Priority actions (30/60/90 days)`

For every key claim, attach at least one repository file path.

## Commands and validation

There is no standard build/test pipeline in this repo.

Recommended checks for document work:
- Ensure referenced paths exist.
- Ensure dates and metric windows are explicit.
- Ensure no confidential credentials are exposed in outputs.

## Editing conventions

1. Keep edits minimal and targeted.
2. Preserve original source documents unless user requests direct modification.
3. Prefer creating new synthesis docs in a clearly named file, for example:
   - `ClaudeCodeSpace/analysis-YYYYMMDD-topic.md`
4. Use plain Markdown.

## Security and sensitive data

Assume docs may contain internal business data.
- Do not copy large raw sensitive tables into responses unless requested.
- Prefer aggregated summaries.

