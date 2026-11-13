---
name: review-implementation
description: Review implemented code against plan specifications with critical assessment
triggers:
  - "review implementation"
  - "audit implementation"
  - "check against plan"
  - "verify implementation"
  - "/review-implementation"
version: 1.0.0
---

# Review Implementation

Critically review implemented code against attached plan documents to verify completeness, adherence, quality, correctness, and testing coverage.

## Purpose

Perform evidence-based audits of implemented features against their specifications, identifying every discrepancy between plan and reality. Distinguish intentional improvements from unjustified deviations.

## Capabilities

- **Completeness analysis**: Verify all requirements and checklist items are fully implemented
- **Plan adherence**: Detect deviations, omissions, scope creep, unintended design changes
- **Code quality assessment**: Evaluate architectural consistency, elegance, maintainability, convention adherence
- **Correctness verification**: Identify logic errors, edge cases, integration issues, security vulnerabilities, potential regressions
- **Testing evaluation**: Assess test comprehensiveness, meaningfulness, and pass status

## Workflow

### 1. Gather Context

Read the plan document(s) first:
- Requirements specifications
- Design documents
- Implementation plans (PLAN.md, SPEC.md, etc.)
- User acceptance criteria
- Checklists

Then examine the actual implementation:
- Changed files (use `git diff` to see what was modified)
- New files created
- Test files and coverage
- Related configuration changes

### 2. Critical Assessment

Evaluate across five dimensions:

#### Completeness
- [ ] Every requirement from plan is implemented
- [ ] All checklist items are addressed
- [ ] No planned features are missing
- [ ] Edge cases from plan are handled

#### Plan Adherence
- [ ] Implementation follows planned architecture
- [ ] No unauthorized scope additions
- [ ] Design decisions match specification
- [ ] Deviations are documented and justified

#### Code Quality
- [ ] Matches existing codebase conventions
- [ ] Clean, maintainable architecture
- [ ] Appropriate abstractions and patterns
- [ ] No unnecessary complexity
- [ ] Proper error handling

#### Correctness
- [ ] Logic implements requirements accurately
- [ ] Edge cases are handled correctly
- [ ] No security vulnerabilities introduced
- [ ] Integration points work as expected
- [ ] No potential regressions

#### Testing
- [ ] Tests cover all new functionality
- [ ] Tests are meaningful, not just coverage theater
- [ ] Edge cases are tested
- [ ] All tests pass
- [ ] Test quality matches codebase standards

### 3. Evidence Collection

For each finding:
1. **Location**: File path and line numbers
2. **Category**: Completeness | Adherence | Quality | Correctness | Testing
3. **Severity**: Critical | High | Medium | Low | Note
4. **Evidence**: Specific code or plan quotes
5. **Impact**: What could go wrong
6. **Recommendation**: How to fix

### 4. Reporting

Produce a structured audit report:

```markdown
# Implementation Review

**Plan**: [plan document reference]
**Implementation**: [commit range or branch]
**Review Date**: [date]

## Executive Summary

[2-3 sentences on overall implementation state]

## Findings

### Critical Issues
[Findings that block shipping]

### High Priority
[Significant deviations or quality issues]

### Medium Priority
[Minor issues worth addressing]

### Low Priority / Notes
[Observations and suggestions]

## Analysis by Dimension

### Completeness: [COMPLETE | PARTIAL | INCOMPLETE]
[Evidence-based assessment]

### Plan Adherence: [EXCELLENT | GOOD | FAIR | POOR]
[Deviations with justification status]

### Code Quality: [EXCELLENT | GOOD | FAIR | POOR]
[Pattern and convention adherence]

### Correctness: [VERIFIED | CONCERNS | UNVERIFIED]
[Logic and integration assessment]

### Testing: [COMPREHENSIVE | ADEQUATE | INSUFFICIENT]
[Coverage and quality evaluation]

## Verdict

**Status**: Complete / Partially Complete / Incomplete

**Ready for Adversarial Review**: Yes / No / With Fixes

**Rationale**: [Brief explanation of verdict]

## Recommendations

1. [Prioritized actions needed]
2. [...]
```

## Review Protocol

### Do
- ✅ Read the entire plan before examining code
- ✅ Use git diff to see actual changes
- ✅ Run tests to verify they pass
- ✅ Check for security implications
- ✅ Verify against existing codebase patterns
- ✅ Cite specific line numbers
- ✅ Distinguish bugs from style preferences
- ✅ Acknowledge intentional improvements

### Don't
- ❌ Modify code during review
- ❌ Make assumptions without evidence
- ❌ Conflate missing tests with broken code
- ❌ Report style preferences as defects
- ❌ Skip reading the actual implementation
- ❌ Assume tests pass without running them

## Usage Examples

### Basic Review
```
Review the authentication implementation against PLAN.md
```

### Specific Scope
```
Review the API endpoints implemented in this PR against the API-SPEC.md
```

### With Context
```
The user stories in REQUIREMENTS.md have been implemented. Review the implementation for completeness and quality.
```

## Tools to Use

- **Read**: Read plan documents and implementation files
- **Bash**: Run `git diff`, `git log`, test commands
- **Grep**: Search for patterns across codebase
- **Glob**: Find related files

## Integration with Other Skills

- **Follow up with `/code-review`** for detailed bug hunting
- **Follow up with `/security-review`** for security-focused audit
- **Use `/simplify`** to address quality issues found

## Output Format

Return a single comprehensive markdown report, not a chat transcript. The report should be:
- **Concise**: Focus on findings, not process description
- **Evidence-based**: Every claim backed by file:line references
- **Actionable**: Clear recommendations for each issue
- **Prioritized**: Critical issues first
- **Verdict-driven**: Clear conclusion about implementation state

## Notes

- This is a **review-only** skill. Never modify code during the review process
- Distinguish between bugs (wrong behavior) and improvements (better approach)
- If tests don't exist, that's a finding, not an excuse to skip verification
- If plan is ambiguous, note where implementation made reasonable choices
- Implementation may legitimately improve on the plan - acknowledge this

## See Also

- `code-review`: Detailed Standards and Spec review for PRs
- `security-review`: Security-focused audit
- `simplify`: Code quality cleanup
