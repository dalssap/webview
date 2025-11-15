# CLAUDE.md - AI Assistant Guide for webview Repository

**Last Updated:** 2025-11-15
**Repository:** dalssap/webview
**Status:** Initial Setup

---

## Overview

This document provides comprehensive guidance for AI assistants working with this codebase. It explains the project structure, development workflows, coding conventions, and key considerations for making effective contributions.

### Current State

**This repository is currently empty and in the initial setup phase.**

As the project develops, this document should be updated to reflect:
- Project architecture and technology stack
- Directory structure and organization
- Development workflows and processes
- Testing strategies and conventions
- Deployment procedures

---

## Table of Contents

1. [Project Information](#project-information)
2. [Codebase Structure](#codebase-structure)
3. [Technology Stack](#technology-stack)
4. [Development Workflow](#development-workflow)
5. [Coding Conventions](#coding-conventions)
6. [Testing Guidelines](#testing-guidelines)
7. [Common Tasks](#common-tasks)
8. [AI Assistant Best Practices](#ai-assistant-best-practices)
9. [Troubleshooting](#troubleshooting)

---

## Project Information

### Purpose
<!-- Update this section with project purpose and goals -->

**To be defined** - This section should describe:
- What problem the project solves
- Target users/audience
- Key features and capabilities
- Project goals and roadmap

### Architecture Overview
<!-- Update this section as architecture emerges -->

**To be defined** - This section should cover:
- High-level system architecture
- Key components and their interactions
- Data flow and processing pipelines
- External dependencies and integrations

---

## Codebase Structure

### Directory Organization

**To be defined** - Update this section when directories are created:

```
/
├── src/              # Source code (if applicable)
├── tests/            # Test files
├── docs/             # Documentation
├── config/           # Configuration files
├── scripts/          # Build and utility scripts
└── README.md         # Project documentation
```

### Key Files

**To be defined** - Document important files as they are created:

- **Entry Points:** List main application entry points
- **Configuration:** List key config files and their purposes
- **Build Files:** Document build and dependency management files

---

## Technology Stack

### Languages & Frameworks

**To be defined** - Update when technologies are chosen:

- **Primary Language:** TBD
- **Framework:** TBD
- **Build Tools:** TBD
- **Package Manager:** TBD

### Development Tools

**To be defined** - Document development tooling:

- **Version Control:** Git
- **CI/CD:** TBD
- **Code Quality:** Linters, formatters, etc. (TBD)
- **Testing:** Test frameworks and tools (TBD)

---

## Development Workflow

### Branch Strategy

**Current Development Branch:** `claude/claude-md-mhzu2wftxgweonxb-01SQehDVhGq8ggKWH385mMKa`

#### Branch Naming Convention

- `main` or `master` - Production-ready code
- `develop` - Integration branch for features
- `feature/*` - Feature branches
- `claude/*` - AI assistant development branches
- `bugfix/*` - Bug fix branches
- `hotfix/*` - Emergency production fixes

#### Git Workflow

1. **Create/Switch to Feature Branch**
   ```bash
   git checkout -b feature/your-feature-name
   ```

2. **Make Changes and Commit**
   ```bash
   git add .
   git commit -m "feat: descriptive commit message"
   ```

3. **Push to Remote**
   ```bash
   git push -u origin feature/your-feature-name
   ```

4. **Create Pull Request**
   - Use `gh pr create` or web interface
   - Include description of changes
   - Reference related issues

### Commit Message Convention

Follow conventional commits format:

```
<type>(<scope>): <subject>

<body>

<footer>
```

**Types:**
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Code style changes (formatting, etc.)
- `refactor`: Code refactoring
- `test`: Adding or updating tests
- `chore`: Maintenance tasks
- `perf`: Performance improvements

**Examples:**
```
feat(auth): add user authentication system
fix(api): resolve race condition in data fetch
docs(readme): update installation instructions
```

---

## Coding Conventions

### General Principles

1. **Code Clarity:** Write self-documenting code with clear variable/function names
2. **DRY Principle:** Don't Repeat Yourself - extract common logic
3. **SOLID Principles:** Follow object-oriented design principles
4. **Error Handling:** Always handle errors gracefully
5. **Security First:** Prevent common vulnerabilities (XSS, SQL injection, etc.)

### Style Guidelines

**To be defined** - Update based on chosen language/framework:

- **Indentation:** TBD (spaces vs tabs, size)
- **Line Length:** TBD (e.g., 80-120 characters)
- **Naming Conventions:** TBD (camelCase, snake_case, etc.)
- **Comments:** When and how to comment code
- **File Organization:** How to structure files/modules

### Code Review Checklist

Before committing code, verify:

- [ ] Code follows style guidelines
- [ ] No security vulnerabilities introduced
- [ ] Error handling is comprehensive
- [ ] Tests are included and passing
- [ ] Documentation is updated
- [ ] No commented-out code or debug statements
- [ ] No hardcoded credentials or secrets

---

## Testing Guidelines

### Test Strategy

**To be defined** - Document testing approach:

- **Unit Tests:** Test individual components/functions
- **Integration Tests:** Test component interactions
- **E2E Tests:** Test complete user workflows
- **Performance Tests:** Benchmark critical paths

### Running Tests

**To be defined** - Update with actual commands:

```bash
# Run all tests
npm test  # or equivalent

# Run specific test suite
npm test -- path/to/test

# Run with coverage
npm run test:coverage
```

### Writing Tests

**Best Practices:**

1. **AAA Pattern:** Arrange, Act, Assert
2. **Descriptive Names:** Test names should describe what they test
3. **Isolation:** Tests should be independent
4. **Coverage:** Aim for high coverage of critical paths
5. **Edge Cases:** Test boundary conditions and error cases

---

## Common Tasks

### Setting Up Development Environment

**To be defined** - Update with actual setup steps:

```bash
# 1. Clone repository
git clone <repository-url>
cd webview

# 2. Install dependencies
npm install  # or equivalent

# 3. Set up environment variables
cp .env.example .env
# Edit .env with your values

# 4. Run development server
npm run dev
```

### Building for Production

**To be defined** - Update with build process:

```bash
# Build production bundle
npm run build

# Run production build locally
npm run start
```

### Debugging

**To be defined** - Document debugging approaches:

- Debug configurations
- Logging strategies
- Common debugging tools
- Performance profiling

---

## AI Assistant Best Practices

### Understanding Context

When working with this codebase:

1. **Read First:** Always use Read tool to examine files before editing
2. **Search Strategically:** Use Grep/Glob to find relevant code
3. **Understand Dependencies:** Check how components interact
4. **Review Recent Changes:** Check git history for context

### Making Changes

1. **Minimize Changes:** Make focused, minimal changes
2. **Preserve Style:** Match existing code style and patterns
3. **Test Thoroughly:** Ensure changes don't break functionality
4. **Document Intent:** Use clear commit messages

### Communication

1. **Be Explicit:** Clearly state what changes are being made
2. **Explain Reasoning:** Describe why changes are necessary
3. **Highlight Risks:** Point out potential issues or side effects
4. **Ask When Uncertain:** Request clarification if requirements are unclear

### Security Considerations

**Always check for:**

- **Input Validation:** Sanitize all user inputs
- **Authentication/Authorization:** Verify access controls
- **Sensitive Data:** Never commit secrets, API keys, or passwords
- **Dependencies:** Check for known vulnerabilities
- **SQL Injection:** Use parameterized queries
- **XSS Prevention:** Sanitize output in web contexts
- **CSRF Protection:** Implement anti-CSRF tokens
- **Rate Limiting:** Prevent abuse of APIs

### Performance Considerations

- **Algorithmic Complexity:** Choose efficient algorithms
- **Database Queries:** Optimize queries and use indexes
- **Caching:** Implement appropriate caching strategies
- **Resource Usage:** Monitor memory and CPU usage
- **Lazy Loading:** Load resources only when needed

---

## Troubleshooting

### Common Issues

**To be defined** - Document common problems and solutions:

#### Issue 1: [Description]
**Symptoms:** What you observe
**Cause:** Why it happens
**Solution:** How to fix it

#### Issue 2: [Description]
**Symptoms:** What you observe
**Cause:** Why it happens
**Solution:** How to fix it

### Getting Help

- **Documentation:** Check README.md and docs/
- **Issue Tracker:** Search existing issues
- **Logs:** Check application logs for errors
- **Community:** Reach out to team members

---

## Maintenance

### Updating This Document

**This document should be updated when:**

- Project structure changes
- New conventions are adopted
- Technologies are added/changed
- Common issues are identified
- Development workflow evolves

**Update Process:**

1. Make changes to CLAUDE.md
2. Update "Last Updated" date at top
3. Commit with message: `docs(claude): update AI assistant guide`
4. Ensure all team members and AI assistants are aware

### Version History

| Date       | Changes                           | Updated By |
|------------|-----------------------------------|------------|
| 2025-11-15 | Initial template created          | Claude AI  |

---

## Quick Reference

### Essential Commands

**To be defined** - Add project-specific commands:

```bash
# Development
<command>  # Description

# Testing
<command>  # Description

# Building
<command>  # Description

# Deployment
<command>  # Description
```

### Important Paths

**To be defined** - List critical file paths:

- Configuration: `path/to/config`
- Environment Variables: `path/to/.env`
- Entry Point: `path/to/main`
- Tests: `path/to/tests`

### Key Contacts

**To be defined** - Add contact information:

- **Project Lead:** TBD
- **Tech Lead:** TBD
- **Repository:** dalssap/webview

---

## Appendix

### Glossary

Define project-specific terminology and acronyms.

### External Resources

- [Project Documentation](link-to-docs)
- [Team Wiki](link-to-wiki)
- [API Documentation](link-to-api-docs)

---

**Note to AI Assistants:** This document is a living guide. As you work with the codebase, if you notice missing or outdated information, suggest updates to keep it current and useful.
