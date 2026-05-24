---
name: add-or-update-lint-rule
description: Workflow command scaffold for add-or-update-lint-rule in bloc.
allowed_tools: ["Bash", "Read", "Write", "Grep", "Glob"]
---

# /add-or-update-lint-rule

Use this workflow when working on **add-or-update-lint-rule** in `bloc`.

## Goal

Add a new lint rule or update an existing one in bloc_lint, including code, config, tests, and documentation.

## Common Files

- `packages/bloc_lint/lib/src/rules/*.dart`
- `packages/bloc_lint/lib/src/rules/rules.dart`
- `packages/bloc_lint/lib/all.yaml`
- `packages/bloc_lint/lib/recommended.yaml`
- `packages/bloc_lint/lib/bloc_lint.dart`
- `packages/bloc_lint/test/src/rules/*_test.dart`

## Suggested Sequence

1. Understand the current state and failure mode before editing.
2. Make the smallest coherent change that satisfies the workflow goal.
3. Run the most relevant verification for touched files.
4. Summarize what changed and what still needs review.

## Typical Commit Signals

- Implement or update the rule in lib/src/rules/ and lib/src/rules/rules.dart.
- Update all.yaml, recommended.yaml, and bloc_lint.dart to register the rule.
- Add or update tests in test/src/rules/.
- Update README.md and documentation in docs/src/components/lint-rules/ and docs/src/content/docs/lint-rules/.

## Notes

- Treat this as a scaffold, not a hard-coded script.
- Update the command if the workflow evolves materially.