# Claude Engineering Excellence Guidelines

This document defines comprehensive standards for software engineering excellence when working with Claude. These guidelines leverage Claude Opus 4.5's advanced capabilities to ensure exceptional code quality, maintainable architecture, and outstanding user experiences.

**Core Philosophy**: Deliver production-grade solutions that exceed expectations through systematic application of best practices, comprehensive testing, and attention to detail.

**Use Test Driven Development**: Before implementing any new functionality or a fix, create a test for it. After completion, run the test to ensure that the implementation is correct.

## Fundamental Principles - Core Directives

<core_rules>

These principles ensure high-quality, maintainable code that respects existing implementations and user intent. Following these guidelines prevents technical debt and maintains system integrity.

<codebase_integrity>

- **Work within the existing codebase architecture** - preserve established patterns, frameworks, and design decisions to maintain consistency and leverage existing infrastructure

- **Maintain strict scope of changes** - modify only code directly related to the user's specific request to prevent unintended side effects and maintain system stability

- **Preserve existing UI/UX implementations** unless explicitly requested to modify them - this maintains user experience consistency and prevents breaking established workflows

- **Use real, production-grade implementations** - create fully functional components with proper data handling, error management, and integration rather than simplified placeholders

</codebase_integrity>

<problem_solving_approach>

- **Identify and resolve root causes** - investigate underlying issues thoroughly rather than implementing surface-level fixes, which prevents recurring problems and technical debt

- **Debug and enhance existing implementations** - when functionality doesn't work as expected, fix the actual code rather than replacing it with simplified alternatives

- **Leverage existing complexity** - complex components exist for good reasons (performance, features, edge cases) - enhance them rather than simplifying them

- **Test before you fix** - implement a test before you implement a fix for an issue

</problem_solving_approach>

<code_exploration>

- **Read and understand relevant files before proposing code edits** - do not speculate about code you have not inspected. If the user references a specific file or path, open and inspect it before explaining or proposing fixes

- **Be rigorous and persistent in searching code for key facts** - thoroughly review the style, conventions, and abstractions of the codebase before implementing new features or abstractions

</code_exploration>

<over_engineering_prevention>

- **Avoid over-engineering** - only make changes that are directly requested or clearly necessary. Keep solutions simple and focused

- **Don't add features, refactor code, or make "improvements" beyond what was asked** - a bug fix doesn't need surrounding code cleaned up. A simple feature doesn't need extra configurability

- **Don't add error handling, fallbacks, or validation for scenarios that can't happen** - trust internal code and framework guarantees. Only validate at system boundaries (user input, external APIs). Don't use backwards-compatibility shims when you can just change the code

- **Don't create helpers, utilities, or abstractions for one-time operations** - don't design for hypothetical future requirements. The right amount of complexity is the minimum needed for the current task. Reuse existing abstractions where possible and follow the DRY principle

</over_engineering_prevention>

</core_rules>

<typescript_standards>

### TypeScript Excellence and Code Quality

Type safety and code quality are fundamental to maintainable software. These practices prevent runtime errors, improve IDE support, and make code self-documenting for team collaboration.

<type_safety_requirements>

- **Add explicit types to all function parameters, variables, and return types** - this provides compile-time error detection, enables powerful IDE features like autocomplete and refactoring, and serves as living documentation for future developers

- **Run build and linting commands before considering any code changes complete** - this ensures code meets quality standards and prevents issues from reaching production or breaking team workflows

- **Fix all linter and TypeScript errors immediately** - addressing issues at the source prevents accumulation of technical debt and maintains the integrity of the development environment for all team members

- **Validate each file for type errors when making changes to multiple files** - this prevents breaking changes from propagating through the codebase and ensures system-wide type safety

- **Apply these standards consistently across frontend and backend TypeScript code** - uniform quality standards reduce cognitive load when switching between different parts of the system

</type_safety_requirements>

</typescript_standards>

<python_standards>

### Python Excellence and Modern Practices

Python type hints and modern syntax improve code reliability, performance, and maintainability. These practices align with contemporary Python development standards and enable powerful tooling support.

<python_type_safety>

- **Add comprehensive type hints to all function parameters, variables, and return types** - this enables static analysis, improves IDE support, prevents runtime type errors, and makes code self-documenting for team collaboration

- **Use modern Python 3.10+ syntax exclusively** (e.g., `list[str]` instead of `List[str]`) - this reduces import overhead, improves readability, and aligns with current Python standards

- **Import from typing only for advanced types** - use `Callable`, `Protocol`, `TypeVar`, `Generic` only when built-in types are insufficient, which keeps imports clean and leverages language evolution

- **Use explicit type annotations in function definitions** - this provides clear contracts and enables powerful development tools:

<code_example>

```python
def process_data(items: list[str], max_count: int = 10) -> dict[str, int]:
    return {"processed": len(items)}

def find_user(user_id: int) -> User | None:
    return database.get_user(user_id)

def merge_configs(base: dict[str, str], override: dict[str, str] | None = None) -> dict[str, str]:
    return {**base, **(override or {})}
```

</code_example>

- **Use modern union syntax exclusively** - always use `T | None` for nullable types and `str | int` for unions, eliminating the need for `Optional` and `Union` imports

- **Add comprehensive docstrings using Google or NumPy style** - this provides usage examples, parameter documentation, and return value specifications for API clarity

</python_type_safety>

<python_quality_tools>

- **Run type checkers before considering code complete** - use `mypy` or `pyright` to catch type errors early and maintain type safety throughout the codebase

- **Run comprehensive linting tools** to maintain code quality and consistency:
  - `black` for consistent code formatting that eliminates style debates
  - `flake8` or `ruff` for catching style violations and potential errors
  - `isort` for consistent import organization
  - `pylint` for advanced code quality analysis and best practice enforcement

- **Resolve all linting and type checking errors immediately** - this prevents technical debt accumulation and maintains development environment integrity

- **Use structured data models** - leverage `dataclasses` or `pydantic` models instead of plain dictionaries to provide type safety, validation, and clear data contracts

- **Follow PEP 8 guidelines consistently** - this ensures code readability and maintains team coding standards

- **Use descriptive variable names** - avoid single-letter variables except in short loops to improve code clarity and maintainability

- **Maintain requirements.txt with pinned versions** - this ensures reproducible builds and prevents dependency conflicts in different environments

</python_quality_tools>

Use lazy % formatting in Python logging functions

</python_standards>


### Directory Layout

Projects should follow this standard directory structure:

```text
project-root/
├── bin/                    # Executable scripts and entry points
├── scripts/               # Development and build scripts
├── src/                   # Source code (for Next.js: app/, pages/, components/)
├── docs/                  # Documentation
├── tests/                 # Test files
└── README.md
```

**For Next.js projects**, follow the Next.js App Router structure:

```text
project-root/
├── bin/                   # Executable scripts and entry points
├── scripts/               # Development and build scripts
├── app/                   # App Router pages and layouts
├── components/            # Reusable UI components
├── lib/                   # Utility functions and configurations
├── public/                # Static assets
├── styles/                # Global styles (if not using Tailwind exclusively)
├── docs/                  # Documentation
├── tests/                 # Test files
└── README.md
```

- **`bin/`** - Contains executable scripts, CLI tools, and main entry points
- **`scripts/`** - Development scripts, build tools, deployment scripts, and utilities
- **`src/`** - Main source code directory (structure depends on framework)
- **`app/`** - Next.js App Router pages, layouts, and route handlers
- **`components/`** - Reusable UI components
- **`lib/`** - Utility functions, configurations, and shared logic
- Keep related files together within their respective directories
- Use consistent naming conventions within each directory

### Cleanup and Maintenance Excellence

Systematic cleanup and maintenance ensure codebase quality and prevent technical debt accumulation. These practices maintain development environment integrity and team productivity.

- **Perform comprehensive cleanup after debugging or testing** - systematically remove all temporary files, scripts, and artifacts to maintain a clean development environment

- **Eliminate debugging artifacts before finalizing work** - remove console.log statements, print statements, temporary variables, and experimental code that served only debugging purposes

- **Delete one-time scripts and temporary tools** - remove scripts created for specific debugging tasks or temporary problem-solving to prevent codebase clutter

- **Clean up experimental and test artifacts** - systematically remove mock data files, experimental code branches, and temporary test implementations that are no longer needed

- **Remove outdated commented code** unless it serves a specific, documented purpose - dead code creates confusion and maintenance overhead

- **Maintain clean version control** - use comprehensive `.gitignore` files to prevent accidental commits of temporary files, build artifacts, and development-specific configurations

- **Create comprehensive documentation when explicitly requested** - develop README.md files with clear project overview, detailed setup instructions, usage examples, and troubleshooting guides

- **Maintain synchronized specification files** that accurately reflect current implementation:
  - SQL schema files documenting complete database structure and relationships
  - API specification files (OpenAPI/Swagger) with comprehensive endpoint documentation
  - Configuration schemas defining all possible settings and their validation rules
  - Data model specifications showing entity relationships and business logic
  - Architecture diagrams and system documentation for complex implementations

- **Update specifications immediately with code changes** - maintain perfect synchronization between implementation and documentation to prevent drift and confusion

- **Validate specifications against current implementation** - regularly verify that documentation accurately represents the actual system behavior and capabilities

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

- When comments are necessary, explain _why_ something is done, not _what_ is being done

- Remove outdated or redundant comments that no longer match the code

- **Add clear file-level docstrings** describing what the file does and its purpose

- Keep file docstrings synchronized with the actual functionality - update them when code changes

- File docstrings should include:
  - Brief description of the file's purpose
  - Key functionality or classes contained
  - Important usage notes or dependencies

### Development Philosophy and Tool Efficiency

- **Prefer legibility over performance** - write clear, readable code first, optimize only when necessary. This approach reduces debugging time and improves long-term maintainability.

- **Optimize for fast development iterations** to accelerate feedback loops and development velocity:
  - Set up auto-reloading for both frontend and backend to eliminate manual restart overhead
  - Use hot module replacement (HMR) for frontend development to preserve application state during development
  - Configure watch modes for backend services to automatically restart on code changes
  - Implement fast feedback loops for testing and debugging to catch issues early

- **Use parallel tool execution** when possible - batch independent operations like file reads, searches, and validations to maximize efficiency and reduce iteration time

- **Leverage comprehensive search strategies** - use multiple search approaches simultaneously (grep, glob, file exploration) to gather complete information quickly

- **Don't start applications automatically** unless explicitly requested by the user - this prevents unwanted system resource usage and maintains user control

- **Write startup scripts using tmux for multi-service applications** to streamline development environment setup:
  - Create separate tmux windows for backend, frontend, database, and monitoring services
  - Use meaningful window names that clearly identify each service's purpose
  - Include proper error handling and startup sequencing to prevent dependency issues
  - Provide clear instructions for using startup scripts and troubleshooting common issues

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
  - Template: <https://github.com/ixartz/Next-js-Boilerplate>
  - Follow the established patterns and structure from this template

- **Use TypeScript instead of JavaScript** for all frontend and backend code

- **Use Tailwind CSS for all styling** - no custom CSS unless absolutely necessary

<ui_ux_excellence>

### UI/UX Design Excellence - Give It Your All

Create exceptional user interfaces that delight users and elevate the entire application experience. Don't hold back - implement comprehensive design systems that demonstrate true craftsmanship.

<interface_design_standards>

- **Create compelling, elegant, and sophisticated interfaces** - prioritize exceptional user experience with thoughtful interactions, beautiful visual design, and intuitive workflows that exceed user expectations

- **Implement comprehensive interaction design**:
  - Design meaningful hover states, focus indicators, and active states for all interactive elements
  - Create smooth, purposeful animations and transitions that guide user attention
  - Implement micro-interactions that provide delightful feedback and enhance usability
  - Add loading states, progress indicators, and status feedback for all user actions

- **Follow clean, uncluttered design principles**:
  - Use whitespace strategically to create visual hierarchy and improve content comprehension
  - Eliminate unnecessary visual elements that don't serve user goals or functionality
  - Focus on essential functionality while maintaining visual appeal and brand consistency
  - Prioritize readability, usability, and accessibility over purely decorative elements

</interface_design_standards>

<accessibility_responsiveness>

- **Design with comprehensive accessibility and responsiveness** - ensure interfaces work perfectly across all devices, screen sizes, and accessibility requirements including keyboard navigation, screen readers, and color contrast standards

- **Maintain consistent, scalable design patterns** throughout the application - develop and follow a comprehensive design system that ensures visual and interaction consistency across all components and pages

- **Implement advanced UI features** - include features like drag-and-drop, keyboard shortcuts, contextual menus, and sophisticated navigation patterns that demonstrate professional-grade implementation

</accessibility_responsiveness>

<frontend_aesthetics>

Avoid converging toward generic, "on distribution" outputs. In frontend design, this creates what users call the "AI slop" aesthetic. Make creative, distinctive frontends that surprise and delight.

Focus on:
- **Typography**: Choose fonts that are beautiful, unique, and interesting. Avoid generic fonts like Arial and Inter; opt instead for distinctive choices that elevate the frontend's aesthetics
- **Color & Theme**: Commit to a cohesive aesthetic. Use CSS variables for consistency. Dominant colors with sharp accents outperform timid, evenly-distributed palettes. Draw from IDE themes and cultural aesthetics for inspiration
- **Motion**: Use animations for effects and micro-interactions. Prioritize CSS-only solutions for HTML. Use Motion library for React when available. Focus on high-impact moments: one well-orchestrated page load with staggered reveals (animation-delay) creates more delight than scattered micro-interactions
- **Backgrounds**: Create atmosphere and depth rather than defaulting to solid colors. Layer CSS gradients, use geometric patterns, or add contextual effects that match the overall aesthetic

Avoid generic AI-generated aesthetics:
- Overused font families (Inter, Roboto, Arial, system fonts)
- Clichéd color schemes (particularly purple gradients on white backgrounds)
- Predictable layouts and component patterns
- Cookie-cutter design that lacks context-specific character

Interpret creatively and make unexpected choices that feel genuinely designed for the context. Vary between light and dark themes, different fonts, different aesthetics across generations.

</frontend_aesthetics>

</ui_ux_excellence>

<excellence_mandate>

## Excellence Mandate - Deliver Outstanding Results

**Give it your all. Don't hold back.** These guidelines exist to ensure exceptional outcomes that exceed expectations and demonstrate true engineering excellence.

<comprehensive_standards>

### Comprehensive Implementation Standards

- **Deliver complete, production-ready solutions** - implement fully functional features with comprehensive error handling, edge case coverage, and robust performance characteristics

- **Exceed basic requirements** - add thoughtful enhancements, anticipate user needs, and implement features that demonstrate deep understanding of the problem domain

- **Implement sophisticated solutions** - use advanced techniques, optimize for performance and maintainability, and create implementations that showcase professional-level engineering

- **Provide comprehensive testing and validation** - include unit tests, integration tests, error scenario testing, and performance validation to ensure bulletproof implementations

</comprehensive_standards>

<quality_craftsmanship>

### Quality and Craftsmanship

- **Demonstrate attention to detail** - polish all aspects of implementation including error messages, loading states, accessibility features, and edge case handling

- **Optimize for long-term success** - write code that is maintainable, extensible, and documented for future developers and evolving requirements

- **Validate against real-world usage** - consider actual user workflows, performance under load, and integration with existing systems and processes

</quality_craftsmanship>

<success_criteria>

### Task Completion Criteria

A task is only complete when ALL of the following are achieved:
- All functional requirements implemented and tested
- Code passes all linting and type checking without errors
- Comprehensive error handling and edge cases covered
- Performance optimized and validated
- Documentation updated to reflect changes
- Cleanup completed (temporary files removed)
- Integration with existing systems verified

</success_criteria>

</excellence_mandate>

### Personal Preferences

- I love using command line. Whenever you can, favor CLI based configuration over GUI.

- **Architectural Design Principles**:
  - shift as much workload to the backend - for example API-level filtering

### Research and Tool Usage

- When asked for documentation research, use Ref, Exa and Context7 mcp in parallel.

- **Don't build the app unless asked**

### VITAL rules

- CLAUDE.md files are vital for operation. They should not be moved.
- **Use pnpm and pnpx instead of npm and npx** - always use `pnpm` for package management (install, add, remove, run scripts, etc.) instead of `npm`
- Never use fallbacks for missing configuration values in code. Fail hard and fast.
- Never use a separate Python venv for a project. Rely on global venv.
- Don't use filesystem MCP
- when working with TeX / LaTeX files, use TeX quotation marks. E.g. ``text’’ instead of ‘text’ or “text”
- When you are working with German in LaTeX, add these packages: \usepackage[T1]{fontenc} \usepackage[ngerman]{babel} - it's important for hyphenation of umlauts, etc.
- Create source maps so that the browser display .ts file locations instead of .js
- Don't track JavaScript and .map files generated from TypeScript. remove from git. Add to .gitignore.
- Ensure all scritps run correctly regardless of which directory they are run from.
- Exit with error when an unknown --flag is passed
