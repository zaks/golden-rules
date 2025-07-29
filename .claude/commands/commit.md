# Commit changes

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
git commit -m "feat: add user profile component with avatar and bio display"

# Tests for the feature
git add tests/components/UserProfile.test.tsx
git commit -m "test: add comprehensive tests for UserProfile component"

# Documentation update
git add README.md
git commit -m "docs: update README with UserProfile component usage"
```

## Commit Message Format

### Structure - Conventional Commits

This project uses **conventional commit format** enforced by git hooks:

**Format:** `<type>[optional scope]: <description>`

**Types:**
- `feat`: A new feature
- `fix`: A bug fix  
- `docs`: Documentation only changes
- `style`: Changes that do not affect code meaning (white-space, formatting, etc)
- `refactor`: A code change that neither fixes a bug nor adds a feature
- `test`: Adding missing tests or correcting existing tests
- `chore`: Changes to the build process or auxiliary tools

**Rules:**
- **Use imperative mood** - "Add feature" not "Added feature"
- **Keep description under 50 characters**
- **No period at the end** of the description
- **Add detailed explanation if needed** in the body

### Good Examples

```
feat: add user authentication middleware
feat(auth): implement JWT token validation
fix: resolve memory leak in data processing pipeline
fix(calendar): correct date formatting for timezone handling
docs: update API documentation for event endpoints
style: format code according to ESLint rules
refactor: simplify database connection handling
test: add comprehensive tests for UserProfile component
chore: update dependency versions for security patches
```

### Bad Examples

```
fixes
updated stuff
minor changes
WIP
Add user authentication (missing type prefix)
feat: Added user authentication (wrong tense)
```

## File Selection Strategy

- **Review all staged files** with `git diff --cached` before committing
- **Use `git add -p`** for partial file commits when needed
- **Exclude unrelated files** even if they're in the same directory
- **Group related changes** that serve the same purpose

## Quality Checks

This project uses **automated pre-commit hooks** that handle all quality checks:

### Automated Pre-commit Hooks
- **ESLint** - Automatic code linting and style enforcement  
- **TypeScript** - Type checking to catch errors early
- **Build validation** - Ensures code compiles successfully

### Manual Checks (if needed)
- **Check for sensitive information** (API keys, passwords, etc.)
- **Review functionality** in browser if UI changes were made

**No manual linting or type checking required** - all automated via git hooks!
