# Project Instructions

## Security & Privacy
- **Restricted Files**: Access to sensitive configuration files and secrets is strictly prohibited. This is enforced via `.geminiignore` and `.gemini/settings.json`.
- **Prohibited Patterns**:
  - `.env`, `.env.local`, `.env.*.local`
  - `appsettings.json`, `appsettings.*.json`
  - `**/secrets/**`, `**/.secrets/**`
- **Redaction**: Environment variable redaction is enabled for this project.

## Development Workflow
- Follow the established security patterns mirrored from `.claude/settings.json`.
