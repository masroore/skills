# Implement Plan (Worktree)

Execute a provided implementation plan completely in an isolated Git worktree. Usually invoked when a plan file (e.g. `.plan/*.md`) is attached to the chat session. If no plan is attached, ask which plan file to implement.

## Language

Always output in **English only** — all messages, summaries, commit messages, comments, and code documentation.

## Git Workflow

### 1. Create isolated worktree

```bash
# Create feature branch and worktree from master
git worktree add -b feature/<name> ../worktree-<name> master
cd ../worktree-<name>
```

Keep master untouched. All work happens in the feature branch within the worktree.

### 2. Commit atomically at logical milestones

Make meaningful commits at implementation milestones:
- One commit per completed requirement or logical unit
- Clear, descriptive commit messages explaining what and why
- Never leave uncommitted changes at the end

### 3. Synchronize and merge

Before merging back to master:

```bash
# Sync with latest master
git fetch origin master:master

# Rebase feature branch on master
git rebase master

# Resolve any conflicts, rerun tests
# ... fix conflicts, run tests ...

# Switch to master and merge
git checkout master
git merge --no-ff feature/<name>

# Push if appropriate
git push origin master
```

### 4. Clean up only after successful merge

```bash
# Remove worktree and branch only after merge verified
cd <original-repo>
git worktree remove ../worktree-<name>
git branch -d feature/<name>
```

**Never discard unmerged work.** Only remove the worktree after successful merge and verification.

## Implementation Protocol

### 1. Read the plan completely

Extract every requirement, checklist item, acceptance criterion, and named file. If a requirement is ambiguous enough to change what gets built, ask before starting. Don't ask for things you can resolve from the plan or code.

### 2. Inspect the existing codebase first

Before writing code, study what exists: architecture, conventions, naming, test structure, and the project's own tooling (formatters, linters, static analysis, test runner). Match it. Reuse existing patterns, helpers, and components instead of introducing new ones. Read the project's agent instructions (CLAUDE.md / AGENTS.md / similar) and follow them.

### 3. Implement everything

- Write elegant, clean, maintainable, production-grade code in the project's idiom.
- No unnecessary abstractions, hacks, workarounds, or unrelated changes — surgical edits only.
- Complete every requirement and every checklist item. No TODOs left behind.
- Add or update tests for behavior changes, following the project's test conventions.
- Commit at logical milestones with clear commit messages.

### 4. Verify — run the full relevant set

Run the project's actual tooling: the full relevant test suite, linters, formatters, and static analysis. Fix every failure. Never claim a check passed without running it.

### 5. Adversarial review standard

Assume the implementation will eventually be scrutinized by a highly critical adversarial reviewer. Proactively identify and eliminate:

- **Bugs** — null handling, boundaries, off-by-one, type mismatches
- **Edge cases** — empty collections, single items, boundaries, overflow
- **Security vulnerabilities** — unvalidated input, missing authorization, injection, XSS
- **Race conditions** — concurrency issues, shared state, timing dependencies
- **Performance problems** — N+1 queries, unbounded loops, memory leaks
- **Regressions** — existing behavior broken by the change
- **Architectural drift** — new patterns inconsistent with codebase

Do not rely on the assumption that the code will pass review without rigorous engineering. Fix what you find before claiming done.

### 6. Integration and cleanup

After all verification passes:
- Sync with latest master
- Resolve any conflicts in the feature branch
- Rerun all tests after conflict resolution
- Merge into master using `--no-ff` for clear history
- Only after successful merge: remove worktree and feature branch

### 7. Report honestly

Done means: all requirements implemented, all checklists completed, all quality checks passing, changes merged into master, and worktree cleaned up. Never claim unverified success.

End with a concise summary:

```markdown
## Implementation Summary

**Branch & Worktree:**
- Feature branch: feature/<name>
- Worktree location: ../worktree-<name>
- Status: merged to master, worktree cleaned up

**Implementation:**
- [Requirement 1]: Implemented in `path/to/file.ext`
- [Requirement 2]: Added in `path/to/other.ext`
- Total commits: N
- Files changed: M

**Verification:**
- ✅ Tests: X passed
- ✅ Linter: clean
- ✅ Formatter: clean
- ✅ Static analysis: no errors
- ✅ Adversarial review: completed, all issues resolved

**Outstanding issues:** (should be empty if truly done)
```

## Anti-patterns

- Creating a worktree without a feature branch.
- Leaving uncommitted changes at the end.
- Merging without syncing with master first.
- Removing the worktree before verifying the merge.
- "I've implemented X, but haven't run tests yet" — run them.
- "The code looks correct" — show the tool output instead.
- Leaving checklist items or TODOs in shipped code.
- Silently skipping verification steps because they're slow.
- Reporting partial completion as done.
- Discarding the worktree with unmerged work still in it.

