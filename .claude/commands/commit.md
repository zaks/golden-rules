# Commit Guidelines

## Pre-Commit Checklist

- **ALWAYS run `git diff` before creating any commit** to review exactly what changes will be included
- **NEVER commit unrelated changes together** - keep commits focused on a single logical change
- **Use multiple commits to separate functionality** when working on complex features
- **Commit tests and code separately** to maintain clear separation of concerns

## Commit Organization

### Separate Commits for Different Types of Changes

1. **Code changes** - Implementation, bug fixes, refactoring
2. **Test changes** - New tests, test updates, test fixes
3. **Documentation changes** - README updates, inline documentation
4. **Configuration changes** - Build configs, environment settings
5. **Dependency changes** - Package updates, new dependencies

### Examples of Good Commit Separation

```bash
# Feature implementation
git add src/components/UserProfile.tsx
git commit -m "Add user profile component with avatar and bio display"

# Tests for the feature
git add tests/components/UserProfile.test.tsx
git commit -m "Add comprehensive tests for UserProfile component"

# Documentation update
git add README.md
git commit -m "Update README with UserProfile component usage"
```

## Commit Message Format

### Structure
- **Brief but complete** - explain what and why, not how
- **Use imperative mood** - "Add feature" not "Added feature"
- **Keep first line under 50 characters** when possible
- **Add detailed explanation if needed** in the body

### Good Examples
```
Add user authentication middleware

Fix memory leak in data processing pipeline

Update dependency versions for security patches

Refactor database connection handling for better error recovery
```

### Bad Examples
```
fixes
updated stuff
minor changes
WIP
```

## File Selection Strategy

- **Review all staged files** with `git diff --cached` before committing
- **Use `git add -p`** for partial file commits when needed
- **Exclude unrelated files** even if they're in the same directory
- **Group related changes** that serve the same purpose

## Quality Checks

- **Run linting and type checking** before committing
- **Ensure tests pass** before committing code changes
- **Verify build succeeds** for significant changes
- **Check for sensitive information** (API keys, passwords, etc.)