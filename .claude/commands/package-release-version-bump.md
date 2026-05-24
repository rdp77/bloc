---
name: package-release-version-bump
description: Workflow command scaffold for package-release-version-bump in bloc.
allowed_tools: ["Bash", "Read", "Write", "Grep", "Glob"]
---

# /package-release-version-bump

Use this workflow when working on **package-release-version-bump** in `bloc`.

## Goal

Release a new version of a package by updating version, changelog, and sometimes README.

## Common Files

- `packages/*/CHANGELOG.md`
- `packages/*/pubspec.yaml`
- `packages/*/README.md`
- `packages/*/lib/src/version.dart`
- `extensions/vscode/CHANGELOG.md`
- `extensions/vscode/package.json`

## Suggested Sequence

1. Understand the current state and failure mode before editing.
2. Make the smallest coherent change that satisfies the workflow goal.
3. Run the most relevant verification for touched files.
4. Summarize what changed and what still needs review.

## Typical Commit Signals

- Update the CHANGELOG.md with release notes.
- Update the pubspec.yaml (or package.json/build.gradle.kts) with the new version.
- Optionally update README.md or version.dart (for Dart packages).

## Notes

- Treat this as a scaffold, not a hard-coded script.
- Update the command if the workflow evolves materially.