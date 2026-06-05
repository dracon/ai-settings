# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **reference implementation** for protecting sensitive files and credentials when using AI assistants. It demonstrates best practices for setting up security restrictions across multiple AI tools (Claude Code, GitHub Copilot, OpenCode, Gemini CLI, and Zed) to prevent accidental exposure of secrets, environment variables, and configuration files.

The project itself showcases how AI can generate and maintain its own security guardrails through configuration files in multiple formats.

## Key Files & Their Purpose

**Configuration Files** (auto-enforced, no special commands needed):
- `.claude/settings.json` — Permission rules that block AI access to sensitive files for Claude Code
- `opencode.json` — Security configuration for OpenCode AI assistant
- `.copilot-instructions` — Behavioral guidelines for GitHub Copilot
- `.gemini/settings.json` & `.geminiignore` — Security rules for Gemini CLI
- `.zed/settings.json` — Security configuration for Zed AI assistant
- `.gitignore` — Prevents accidental commits of secrets

**Documentation**:
- `README.md` — Comprehensive overview and setup instructions
- `AI_SECURITY_GUIDE.html` — Interactive guide for team members (view in browser)
- `GEMINI.md` — Gemini CLI specific instructions

## Protected File Patterns

These are blocked from AI read/write access:
- Environment files: `.env`, `.env.local`, `.env.*.local`
- Configuration files: `appsettings.json`, `appsettings.*.json`
- Secret directories: `secrets/`, `.secrets/`
- Private keys: `*.pem`, `*.key`, `*.pfx`, `*.p12`, `id_rsa*`, `id_ed25519*`
- Files with sensitive names: anything with "secret", "credentials", "password", "api_key", "token"

This is enforced via permission rules in `.claude/settings.json` — Claude Code will refuse access with a permission error if you try to read/write these files.

## Protected Commands

OpenCode also blocks bash commands that could expose environment variables or secrets:
- `env` and `env *` — Lists all environment variables
- `printenv` and `printenv *` — Prints environment variables
- `mise list` and `mise list *` — Lists Mise environment info

All other bash commands are allowed. This prevents accidental exposure of sensitive information through command output.

## Development Workflow

**To work with this project:**

1. **Understand the architecture**: Read `README.md` for the overall approach. The project uses a "defense-in-depth" model with multiple configuration file formats targeting different AI assistants.

2. **Modify configuration files**: All configuration files are JSON or text-based and designed to be human-editable:
   - Edit `.claude/settings.json` to change Claude Code restrictions
   - Edit `opencode.json` for OpenCode rules
   - Edit `.copilot-instructions` for Copilot guidelines
   - Update `.gitignore` to change Git protection patterns

3. **Generate documentation**: Use Claude Code to help maintain and regenerate documentation like the HTML guide, but reference the README and config files for structure.

4. **Testing restrictions**: Verify restrictions are working by attempting to read a `.env` file or accessing other protected patterns — you should see a permission denied error.

## Important Notes

- **No build system**: This is a configuration reference, not an application with tests, linting, or build steps.
- **Configuration format differences**: Each AI assistant has its own preferred format (JSON, text, etc.). When adding new restrictions, ensure they're applied consistently across all relevant config files.
- **Local overrides available**: Users can create `.claude/settings.local.json` to override restrictions for personal development, but this is not recommended.
- **All configurations are synced**: When updating protection patterns, ensure consistency across `.claude/settings.json`, `opencode.json`, `.copilot-instructions`, `.gemini/settings.json`, and `.gitignore`.

## Common Tasks

**Add a new protected file pattern:**
1. Add to `.claude/settings.json` under `permissions.deny` (both Read and Edit)
2. Add to `opencode.json` under `permission.read` and `permission.edit`
3. Add to `.copilot-instructions` under "Secret Files - DO NOT ACCESS"
4. Add to `.gitignore` to prevent commits
5. Add to `.geminiignore` for Gemini CLI
6. Update README.md with the new pattern in the "Protected File Patterns" section

**Add a new protected command (OpenCode only):**
1. Add to `opencode.json` under `permission.bash` with `"deny"` value
2. Include both the command and wildcard variants (e.g., `"cmd"` and `"cmd *"`)
3. Update CLAUDE.md "Protected Commands" section with explanation

**Update HTML guide:**
- The `AI_SECURITY_GUIDE.html` is generated content. You can ask Claude Code to regenerate it if you've made significant changes to the configuration, or edit it manually.

**Document changes:**
- Commit all configuration changes together with a descriptive message
- Update README.md if the approach or patterns change significantly
- Update CLAUDE.md to reflect new protection layers or configuration changes
