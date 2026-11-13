# Implement Plan

Execute a provided implementation plan completely. Usually invoked when a plan file (e.g. `.plan/*.md`) is attached to the chat session. If no plan is attached, ask which plan file to implement.

## Protocol

### 1. Read the plan completely

Extract every requirement, checklist item, acceptance criterion, and named file. If a requirement is ambiguous enough to change what gets built, ask before starting. Don't ask for things you can resolve from the plan or code.

### 2. Inspect the existing codebase first

Before writing code, study what exists: architecture, conventions, naming, test structure, and the project's own tooling (formatters, linters, static analysis, test runner). Match it. Reuse existing patterns, helpers, and components instead of introducing new ones. Read the project's agent instructions (CLAUDE.md / AGENTS.md / similar) and follow them.

### 3. Implement everything

- Write elegant, clean, maintainable, production-grade code in the project's idiom.
- No unnecessary abstractions, hacks, workarounds, or unrelated changes — surgical edits only.
- Complete every requirement and every checklist item. No TODOs left behind.
- Add or update tests for behavior changes, following the project's test conventions.

### 4. Verify — run the full relevant set

Run the project's actual tooling: the full relevant test suite, linters, formatters, and static analysis. Fix every failure. Never claim a check passed without running it.

### 5. Adversarial self-review

Before reporting done, actively hunt for: bugs (null handling, boundaries, off-by-one), edge cases, security issues (unvalidated input, missing authorization, injection), performance problems, regressions to existing behavior, and architectural drift from the codebase. Fix what you find.

### 6. Report honestly

Done means: all requirements implemented, all checklists completed, all quality checks passing, and no known issues remaining. Never claim unverified success.

End with a concise summary:

```markdown
## Implementation Summary
- What was implemented (per requirement, with file paths)
- Tests and quality checks run, with results (counts, exit status)
- Adversarial review findings and fixes applied
- Anything not done, with reasons (should be empty if truly done)
```

## Language

Always output in **English only** — all messages, summaries, comments, and code documentation.

## Anti-patterns

- "I've implemented X, but haven't run tests yet" — run them.
- "The code looks correct" — show the tool output instead.
- Leaving checklist items or TODOs in shipped code.
- Silently skipping verification steps because they're slow.
- Reporting partial completion as done.

