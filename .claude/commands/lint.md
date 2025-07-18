# Lint Guidelines

## Pre-Lint Checklist

- **ALWAYS run linting tools before considering code complete**
- **Fix all linting errors immediately** - don't leave them for later
- **Run type checking alongside linting** to catch both style and type issues
- **Use project-specific linting configurations** when available

## Common Linting Commands by Language

### TypeScript/JavaScript (Node.js/Next.js)
```bash
# ESLint for code quality and style
npm run lint
# or
npx eslint . --ext .ts,.tsx,.js,.jsx

# TypeScript type checking
npm run type-check
# or
npx tsc --noEmit

# Prettier for code formatting
npm run format
# or
npx prettier --write .
```

### Python
```bash
# Ruff for linting and formatting (replaces flake8, black, isort)
ruff check .
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

# Prettier for CSS formatting
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

# Prettier for Markdown formatting
npx prettier --write "**/*.md"
```

## Linting Workflow

1. **Check for existing lint scripts** in package.json, Makefile, or project docs
2. **Run linting tools in this order**:
   - Code formatting (prettier, ruff format)
   - Style checking (eslint, ruff check, stylelint, htmlhint, markdownlint)
   - Type checking (tsc, mypy)
3. **Fix issues immediately** - don't proceed with broken linting
4. **Re-run linting** after fixes to ensure all issues are resolved

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

## Troubleshooting

- **Check project README** for specific linting instructions
- **Look for CI/CD configurations** that show required linting commands
- **Use `--help` flag** to understand linting tool options
- **Check for pre-commit hooks** that might run linting automatically