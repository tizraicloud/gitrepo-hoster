# CLAUDE.md — Sample Project Instructions

## Code Style
- Use TypeScript with strict mode enabled
- Prefer `const` over `let`; never use `var`
- Use named exports over default exports

## Testing
- Write tests for all new features
- Use Vitest as the test runner
- Aim for >80% coverage on critical paths

## Git
- Use conventional commits (feat:, fix:, chore:, docs:)
- Keep PRs focused — one feature or fix per PR
- Squash merge to main

## Architecture
- Follow the repository pattern for data access
- Keep business logic in service layers, not controllers
- Use dependency injection for testability
