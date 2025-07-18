# Lint code and documentation files

## Pre-Lint Checklist

- **ALWAYS run linting tools before considering code complete**
- **Fix all linting errors immediately** - don't leave them for later
- **Run type checking alongside linting** to catch both style and type issues
- **Use project-specific linting configurations** when available
- **When --fix is within $ARGUMENTS, automatically fix all fixable linting issues**

## Common Linting Commands by Language

### TypeScript/JavaScript (Node.js/Next.js)

```bash
# ESLint for code quality and style
npm run lint
# or
npx eslint . --ext .ts,.tsx,.js,.jsx

# When --fix is in $ARGUMENTS: automatically fix all fixable issues
npm run lint -- --fix
# or
npx eslint . --ext .ts,.tsx,.js,.jsx --fix

# TypeScript type checking
npm run type-check
# or
npx tsc --noEmit

# Prettier for code formatting (always auto-fixes)
npm run format
# or
npx prettier --write .
```

### Python

```bash
# Ruff for linting and formatting (replaces flake8, black, isort)
ruff check .
ruff format .

# When --fix is in $ARGUMENTS: automatically fix all fixable issues
ruff check . --fix
ruff format .

# mypy for type checking
mypy .

# pylint for additional code quality checks (optional)
pylint **/*.py
```

### CSS

```bash
# stylelint for CSS linting
npx stylelint "**/*.css"

# When --fix is in $ARGUMENTS: automatically fix all fixable issues
npx stylelint "**/*.css" --fix

# Prettier for CSS formatting (always auto-fixes)
npx prettier --write "**/*.css"
```

### HTML

```bash
# htmlhint for HTML linting
npx htmlhint "**/*.html"

# Prettier for HTML formatting
npx prettier --write "**/*.html"
```

### Markdown

```bash
# markdownlint for Markdown linting
npx markdownlint "**/*.md"

# When --fix is in $ARGUMENTS: automatically fix all fixable issues
npx markdownlint "**/*.md" --fix

# Prettier for Markdown formatting (always auto-fixes)
npx prettier --write "**/*.md"
```

## Linting Workflow

1. **Check for existing lint scripts** in package.json, Makefile, or project docs
2. **If --fix is within $ARGUMENTS, run auto-fix commands first**:
   - Code formatting (prettier, ruff format)
   - Auto-fixable style issues (eslint --fix, ruff check --fix, stylelint --fix, markdownlint --fix)
3. **Run linting tools in this order**:
   - Code formatting (prettier, ruff format)
   - Style checking (eslint, ruff check, stylelint, htmlhint, markdownlint)
   - Type checking (tsc, mypy)
4. **Fix remaining issues immediately** - don't proceed with broken linting
5. **Re-run linting** after fixes to ensure all issues are resolved

## Configuration Files to Look For

- `.eslintrc.*` - ESLint configuration
- `.prettierrc.*` - Prettier configuration
- `pyproject.toml` - Python project configuration (includes ruff config)
- `ruff.toml` - Ruff-specific configuration
- `.stylelintrc.*` - Stylelint configuration
- `.htmlhintrc` - HTMLHint configuration
- `.markdownlint.json` - Markdownlint configuration
- `tslint.json` - TypeScript linting (deprecated, use ESLint)

## Best Practices

- **Follow project conventions** - use existing linting configurations
- **Don't disable linting rules** without good reason
- **Add type annotations** when linting suggests them
- **Fix warnings, not just errors** - warnings often indicate code quality issues
- **Use IDE integration** for real-time linting feedback during development
- **When --fix is within $ARGUMENTS, always run auto-fix commands before manual inspection**
- **Auto-fix safely** - review changes made by auto-fix tools before committing

## Troubleshooting

- **Check project README** for specific linting instructions
- **Look for CI/CD configurations** that show required linting commands
- **Use `--help` flag** to understand linting tool options
- **Check for pre-commit hooks** that might run linting automatically
