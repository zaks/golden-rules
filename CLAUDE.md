### Critical Rules - DO NOT VIOLATE

- **NEVER create mock data or simplified components** unless explicitly told to do so

- **NEVER replace existing complex components with simplified versions** - always fix the actual problem

- **NEVER change code unrelated to the user's request** - maintain strict scope of changes

- **NEVER modify styling or interactions** unless explicitly requested by the user - preserve all existing UI/UX

- **ALWAYS work with the existing codebase** - do not create new simplified alternatives

- **ALWAYS find and fix the root cause** of issues instead of creating workarounds

- When debugging issues, focus on fixing the existing implementation, not replacing it

- When something doesn't work, debug and fix it - don't start over with a simple version

### TypeScript and Linting

- ALWAYS add explicit types to all function parameters, variables, and return types

- ALWAYS run `pnpm build` or appropriate linter command before considering any code changes complete

- Fix all linter and TypeScript errors immediately - don't leave them for the user to fix

- When making changes to multiple files, check each one for type errors

### Python Best Practices

- ALWAYS add type hints to all function parameters, variables, and return types

- Use `from typing import` for complex types like `List`, `Dict`, `Optional`, `Union`, `Callable`

- Use modern Python 3.9+ syntax when available (e.g., `list[str]` instead of `List[str]`)

- ALWAYS use type annotations for function definitions:
  ```python
  def process_data(items: list[str], max_count: int = 10) -> dict[str, int]:
      return {"processed": len(items)}
  ```

- Use `Optional[T]` or `T | None` for nullable parameters

- Add docstrings with parameter and return type documentation using Google or NumPy style

- ALWAYS run type checkers (`mypy`, `pyright`) before considering code complete

- ALWAYS run linting tools before considering code complete:
  - Use `black` for code formatting
  - Use `flake8` or `ruff` for style and error checking
  - Use `isort` for import sorting
  - Consider `pylint` for additional code quality checks

- Fix all linting and type checking errors immediately - don't leave them for the user to fix

- Use `dataclasses` or `pydantic` models for structured data instead of plain dictionaries

- Follow PEP 8 style guidelines consistently

- Use meaningful variable names and avoid single-letter variables except for short loops

### Directory Layout

Projects should follow this standard directory structure:

```
project-root/
├── bin/                    # Executable scripts and entry points
├── scripts/               # Development and build scripts
├── client/                # Frontend/client-side code
├── server/                # Backend/server-side code
├── docs/                  # Documentation
├── tests/                 # Test files
└── README.md
```

- **`bin/`** - Contains executable scripts, CLI tools, and main entry points
- **`scripts/`** - Development scripts, build tools, deployment scripts, and utilities
- **`client/`** - All frontend code, React components, styles, and client-side assets
- **`server/`** - Backend code, APIs, database models, and server-side logic
- Keep related files together within their respective directories
- Use consistent naming conventions within each directory

### Cleanup and Maintenance

- **ALWAYS delete temporary files and scripts** after debugging or testing is complete

- Remove any temporary debugging code, console.log statements, or print statements before finalizing

- Delete temporary scripts created for one-time tasks or debugging purposes

- Clean up any test files, mock data files, or experimental code that's no longer needed

- Remove commented-out code blocks unless they serve a specific documented purpose

- Keep the codebase clean - temporary files and debug scripts should not be committed to version control

- Use `.gitignore` to prevent accidental commits of temporary files and build artifacts

- **ALWAYS create and maintain a README.md file** with project overview, setup instructions, and usage examples

- **ALWAYS create and maintain specification files** and keep them synchronized with the codebase:
  - SQL schema files for database structure
  - API specification files (OpenAPI/Swagger)
  - Configuration schemas
  - Data model specifications
  - Any other relevant specification documents

- Update specification files immediately when making changes to the corresponding code

- Ensure specifications accurately reflect the current state of the implementation

### Code Organization and File Management

- **Keep files under 200 lines of code** whenever possible

- **Separate functionality into individual files** - each file should have a single, clear responsibility

- **Refactor files immediately** when they exceed 200 lines or become difficult to maintain

- Break large files into smaller, focused modules with clear interfaces

- Use meaningful file names that clearly indicate their purpose and contents

- Group related functionality into directories while keeping individual files small and focused

### Code Clarity and Comments

- **Use comments only when necessary** to understand complex logic or business rules

- **Rely on good naming conventions** to make code self-documenting:
  - Functions should clearly describe what they do: `calculateTotalPrice()` not `calc()`
  - Variables should describe what they contain: `userEmailAddress` not `email`
  - Classes should describe what they represent: `PaymentProcessor` not `Processor`

- **Prefer self-explanatory code over comments** - if you need a comment to explain what code does, consider refactoring for clarity

- When comments are necessary, explain *why* something is done, not *what* is being done

- Remove outdated or redundant comments that no longer match the code

- **ALWAYS add clear file-level docstrings** describing what the file does and its purpose

- Keep file docstrings synchronized with the actual functionality - update them when code changes

- File docstrings should include:
  - Brief description of the file's purpose
  - Key functionality or classes contained
  - Important usage notes or dependencies

### Development Philosophy

- **Prefer legibility over performance** - write clear, readable code first, optimize only when necessary

- **Optimize for fast development iterations**:
  - Set up auto-reloading for both frontend and backend
  - Use hot module replacement (HMR) for frontend development
  - Configure watch modes for backend services
  - Implement fast feedback loops for testing and debugging

### Production Build Rules

- **Production builds have different requirements** than development:
  - Enable all optimizations (minification, tree-shaking, compression)
  - Remove all debug code, console statements, and development-only features
  - Use production-specific configurations and environment variables
  - Implement proper error handling and logging for production
  - Enable security hardening and performance optimizations
  - Run full test suites before production deployment
  - Generate and validate production build artifacts

### Frontend Technology Stack

- **Use Next.js for frontend development** with the following boilerplate template:
  - Template: https://github.com/ixartz/Next-js-Boilerplate
  - Follow the established patterns and structure from this template

- **ALWAYS use TypeScript instead of JavaScript** for all frontend and backend code

- **Use Tailwind CSS for all styling** - no custom CSS unless absolutely necessary

### UI/UX Design Principles

- **Create compelling and elegant interfaces** that prioritize user experience

- **Avoid interface chrome overload**:
  - Keep interfaces clean and uncluttered
  - Use whitespace effectively
  - Minimize unnecessary visual elements
  - Focus on essential functionality and content
  - Prioritize readability and usability over decorative elements

- Design with accessibility and responsiveness in mind

- Maintain consistent design patterns throughout the application