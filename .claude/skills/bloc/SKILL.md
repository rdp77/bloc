```markdown
# bloc Development Patterns

> Auto-generated skill from repository analysis

## Overview
This skill teaches you the core development patterns, coding conventions, and common workflows used in the `bloc` repository. The codebase is primarily TypeScript (with some Dart and Kotlin in subprojects), and it focuses on maintainable, modular code for state management, linting, and IDE extension tooling. You'll learn how to contribute code, manage releases, update dependencies, and extend the project with new features or rules, following established conventions and workflows.

## Coding Conventions

- **File Naming:**  
  Use `camelCase` for file names.  
  _Example:_  
  ```
  installBlocTools.ts
  myExampleFile.ts
  ```

- **Import Style:**  
  Use relative imports.  
  _Example:_  
  ```typescript
  import { myFunction } from './utils/myFunction';
  ```

- **Export Style:**  
  Use named exports.  
  _Example:_  
  ```typescript
  export function myFunction() { ... }
  export const MY_CONSTANT = 42;
  ```

- **Commit Messages:**  
  Follow [Conventional Commits](https://www.conventionalcommits.org/) with prefixes:  
  `chore`, `refactor`, `docs`, `feat`, `fix`  
  _Example:_  
  ```
  feat: add support for custom lint rules
  fix: correct typo in README.md
  ```

## Workflows

### Package Release Version Bump
**Trigger:** When releasing a new version of a package  
**Command:** `/release-package`

1. Update the `CHANGELOG.md` with release notes.
2. Update the version in `pubspec.yaml`, `package.json`, or `build.gradle.kts`.
3. Optionally update `README.md` or `version.dart` (for Dart packages).
4. Commit changes with a conventional message (e.g., `chore: release vX.Y.Z`).
5. Push and create a release PR.

_Files involved:_  
- `packages/*/CHANGELOG.md`
- `packages/*/pubspec.yaml`
- `packages/*/README.md`
- `packages/*/lib/src/version.dart`
- `extensions/vscode/CHANGELOG.md`
- `extensions/vscode/package.json`
- `extensions/vscode/package-lock.json`
- `extensions/intellij/intellij_generator_plugin/build.gradle.kts`
- `extensions/intellij/intellij_generator_plugin/src/main/resources/META-INF/plugin.xml`

---

### Add or Update Lint Rule
**Trigger:** When introducing or modifying a lint rule in `bloc_lint`  
**Command:** `/add-lint-rule`

1. Implement or update the rule in `lib/src/rules/` and register in `rules.dart`.
2. Update `all.yaml`, `recommended.yaml`, and `bloc_lint.dart` to register the rule.
3. Add or update tests in `test/src/rules/`.
4. Update documentation in `README.md` and `docs/src/components/lint-rules/` and `docs/src/content/docs/lint-rules/`.

_Example Dart rule registration:_
```dart
// lib/src/rules/rules.dart
export 'my_new_rule.dart';
```

---

### Dependency Bump via Dependabot
**Trigger:** When a new dependency version is released and Dependabot creates a PR  
**Command:** `/bump-dependency`

1. Update `package.json` and/or `package-lock.json` (or other lock/config files).
2. Commit with a message referencing the dependency and version bump.
3. Merge after CI passes.

_Example commit message:_  
```
chore(deps): bump typescript from 4.9.5 to 5.0.0
```

---

### Example App Addition or Major Update
**Trigger:** When adding a new example app or making a significant update  
**Command:** `/add-example-app`

1. Create or update files under `examples/` (Dart, assets, configs).
2. Update or add `README.md` for the example.
3. Add or update `pubspec.yaml` and other config files.
4. Add assets (images, gifs, icons) if needed.

---

### Update Extension to Use Latest bloc_tools
**Trigger:** When `bloc_tools` is updated and extensions need to use the new version  
**Command:** `/update-extension-bloc-tools`

1. Update `bloc_tools` version in extension source/config files.
2. Update `package-lock.json` or `build.gradle.kts` as needed.
3. Update `plugin.xml` (IntelliJ) or `install-bloc-tools.ts` (VSCode) if necessary.
4. Optionally update `CHANGELOG.md`.

---

## Testing Patterns

- **Test File Pattern:**  
  Test files are named with the `.test.ts` suffix.  
  _Example:_  
  ```
  myFunction.test.ts
  ```

- **Testing Framework:**  
  Not explicitly specified, but likely uses a standard TypeScript/JavaScript test runner (e.g., Jest, Mocha).

- **Test Example:**  
  ```typescript
  import { myFunction } from './myFunction';

  describe('myFunction', () => {
    it('should return true for valid input', () => {
      expect(myFunction('valid')).toBe(true);
    });
  });
  ```

## Commands

| Command                      | Purpose                                                      |
|------------------------------|--------------------------------------------------------------|
| /release-package             | Release a new version of a package                           |
| /add-lint-rule               | Add or update a lint rule in bloc_lint                       |
| /bump-dependency             | Update dependencies via Dependabot or manually                |
| /add-example-app             | Add a new example app or make a major update to an example   |
| /update-extension-bloc-tools | Update IDE extensions to use the latest bloc_tools version    |
```
