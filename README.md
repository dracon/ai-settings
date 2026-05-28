# AI Security Settings Project

## Project Purpose

This project demonstrates how to protect sensitive files and credentials when using AI assistants like **Claude Code** and **GitHub Copilot** in your projects. It provides a reference implementation for setting up security restrictions that prevent AI agents from accidentally reading, writing, or exposing sensitive configuration files and secrets.

The configuration files and security guidelines in this repository are **generated and managed through Claude Code**, showcasing best practices for AI-assisted development while maintaining strict security boundaries.

## Why This Matters

When using AI assistants for code development, there's a risk of accidentally exposing secrets through:
- Pasting `.env` files or configuration into AI chat
- Asking AI to read or edit files containing credentials
- Using AI to debug code that references sensitive data

This project provides a **defense-in-depth approach** using multiple layers of protection:

1. **Claude Code Permission Rules** - Hard blocks that prevent file access
2. **GitHub Copilot Custom Instructions** - Behavioral guidelines that guide responsible use
3. **Git Ignore Patterns** - Prevents secrets from being committed to version control

## What's Included

### Configuration Files (Generated with Claude Code)

All configuration files in this repository are created and maintained through Claude Code, demonstrating how AI can assist in implementing its own security guardrails.

#### `.claude/settings.json`
- **Purpose**: Permission-based security rules for Claude Code
- **Type**: Machine-readable JSON configuration
- **Effect**: Blocks Read, Write, and Edit operations on sensitive files
- **Scope**: Applied automatically to all users cloning the repository
- **Coverage**: Environment files, configs, secrets, keys, sensitive patterns

#### `.gemini/settings.json` & `.geminiignore`
- **Purpose**: Security policies and file ignoring for Gemini CLI
- **Type**: JSON configuration and text-based ignore patterns
- **Effect**: Blocks access to sensitive files and redacts environment variables
- **Scope**: Project-level security for Gemini CLI
- **Coverage**: Environment files, configs, secrets, keys, sensitive patterns
- **Features**: Includes environment variable redaction and mandatory ignore patterns

#### `.zed/settings.json`
- **Purpose**: Security permission rules for Zed AI assistant
- **Type**: Machine-readable JSON configuration with security schema
- **Effect**: Blocks Read, Edit, and Write operations on sensitive files
- **Scope**: Applied automatically when Zed operates in this project
- **Coverage**: Environment files, configs, secrets, keys, certificate patterns
- **Features**: Includes security blocklist with glob pattern matching for keys

#### `opencode.json`
- **Purpose**: Comprehensive security rules for OpenCode AI assistant
- **Type**: Structured JSON configuration with security metadata
- **Effect**: Blocks Read, Write, and Execute operations on sensitive files
- **Scope**: Applied to OpenCode when working in this project
- **Coverage**: Environment files, configs, secrets, keys, sensitive patterns
- **Features**: Includes detailed security layer documentation explaining why each pattern is protected

#### `.copilot-instructions`
- **Purpose**: Custom security instructions for GitHub Copilot
- **Type**: Human-readable guidelines
- **Effect**: Guides Copilot behavior when it encounters sensitive files
- **Scope**: Read by Copilot and applied within the GitHub editor

#### `.gitignore` (Updated)
- **Purpose**: Prevents accidental commits of sensitive files
- **Type**: Git configuration
- **Effect**: Blocks commits of secrets, credentials, and configuration files
- **Scope**: Applied to all git operations in the repository

#### `AI_SECURITY_GUIDE.html`
- **Purpose**: Interactive guide explaining the security setup
- **Type**: HTML documentation (view in browser)
- **Audience**: Team members, developers, and security teams

## Protected File Patterns

The configuration protects the following categories of sensitive files:

### Environment Files
- `.env` - Default environment variables
- `.env.local` - Local overrides
- `.env.*.local` - Environment-specific files (development, production, test)

### Configuration Files
- `appsettings.json` - Default configuration
- `appsettings.*.json` - Environment-specific configurations
- `appsettings.Development.json`
- `appsettings.Production.json`
- `appsettings.Staging.json`

### Secret Directories
- `secrets/` - Any files inside
- `.secrets/` - Any files inside

### Private Keys & Certificates
- `*.pem` - PEM certificates
- `*.key` - Private keys
- `*.pfx` - PKCS#12 certificates
- `*.p12` - PKCS#12 format
- `id_rsa*` - SSH keys
- `id_ed25519*` - Ed25519 SSH keys

### Sensitive Filename Patterns
- Files containing "secret" in the name
- Files containing "credentials" in the name
- Files containing "password" in the name
- Files containing "api_key" or "apikey" in the name
- Files containing "token" in the name

## How to Use This As a Template

To implement similar security in your own projects:

### 1. Copy Configuration Files

```bash
# Copy the Claude Code security settings
cp .claude/settings.json your-project/.claude/settings.json

# Copy the OpenCode security configuration
cp opencode.json your-project/opencode.json

# Copy the GitHub Copilot instructions
cp .copilot-instructions your-project/.copilot-instructions

# Review and merge the .gitignore patterns
cat .gitignore >> your-project/.gitignore
```

### 2. Customize for Your AI Assistants

Edit the configuration files to match your team's tools:
- **Claude Code**: Use `.claude/settings.json` if your team uses Claude Code
- **OpenCode**: Use `opencode.json` if your team uses OpenCode
- **GitHub Copilot**: Use `.copilot-instructions` if your team uses GitHub Copilot
- **Git**: Always include `.gitignore` patterns

### 3. Commit to Version Control

```bash
git add opencode.json .claude/settings.json .copilot-instructions .gitignore
git commit -m "Add AI security restrictions for secret file protection"
git push
```

### 4. Inform Your Team

Share the `AI_SECURITY_GUIDE.html` with your team to explain:
- What restrictions are in place
- How to work with the restrictions
- Best practices for secure development

## How Claude Code Generated These Files

This project demonstrates Claude Code's capability to create security configurations for multiple AI assistants:

### Claude Code & OpenCode Configurations
1. **Initial Setup**: The project was initialized with security requirements in mind
2. **Configuration Generation**: Claude Code created JSON configurations for:
   - Claude Code's permission system (`.claude/settings.json`)
   - OpenCode's permission model (`opencode.json`)
3. **Multi-Tool Approach**: Single security rules adapted across different AI assistants
4. **Documentation**: Claude Code generated comprehensive documentation explaining the setup
5. **HTML Guide**: Claude Code created an interactive HTML guide for team reference
6. **Validation**: All configurations were tested to ensure they work as intended

### OpenCode Configuration Features
The `opencode.json` file includes additional metadata:
- **Security Layers**: Documented descriptions of why each file pattern is protected
- **Structured Format**: JSON schema that OpenCode can parse and enforce
- **Extensible Design**: Easy to add new patterns or modify restrictions
- **Team Communication**: Built-in explanations that developers can reference

This showcases how AI can be used to implement security best practices, even when those practices restrict the AI itself. It demonstrates that consistent security policies can be applied across multiple AI assistants simultaneously.

## Security Features

### Claude Code Protection
- **Type**: Hard blocking at the file system level
- **Enforcement**: Immediate denial with error message
- **Message**: "File is in a directory that is denied by your permission settings."
- **Operations**: Read, Write, Edit
- **Scope**: Applied automatically to all users

### Gemini CLI Protection
- **Type**: Multi-layered protection (Ignore patterns + Settings)
- **Configuration**: `.geminiignore` for exclusion and `.gemini/settings.json` for security toggles
- **Enforcement**: Excludes files from discovery and redacts secrets in environment variables
- **Operations**: Read, Write, Discovery
- **Scope**: Project-level security for Gemini CLI

### OpenCode Protection
- **Type**: Structured permission-based blocking
- **Configuration**: Declarative JSON with security layer metadata
- **Enforcement**: Blocks access before operations are attempted
- **Operations**: Read, Write, Execute
- **Features**: 
  - Detailed explanation of why each file pattern is protected
  - Multi-layered security documentation
  - Easy integration with OpenCode AI assistant
- **Scope**: Applied when OpenCode is used in this project

### GitHub Copilot Protection
- **Type**: Behavioral guidance through custom instructions
- **Enforcement**: Copilot reads instructions and follows them
- **Guidance**: Won't suggest changes to protected files, won't complete secrets
- **Scope**: Code suggestions and chat interactions

### Git Protection
- **Type**: Repository-level file filtering
- **Enforcement**: Prevents commits of matched patterns
- **Scope**: All team members, all branches

## Testing the Security

You can verify these restrictions are working:

### Test Claude Code Access Blocking
```bash
# Create a test .env file
echo "SECRET=test123" > .env

# Try to use Claude Code to read it
# Expected: Permission denied error
```

### Test Gemini CLI Access Blocking
```bash
# Create a test .env file (if not already there)
echo "SECRET=test123" > .env

# Try to use Gemini CLI to list files or read it
# Expected: File is ignored and not visible to tools
```

### Test Git Protection
```bash
# Try to add a .env file
git add .env

# Expected: File is ignored by .gitignore
git status  # .env should not appear in staged changes
```

## Best Practices for Your Team

When using AI assistants with these restrictions in place:

### ✓ DO
- Reference environment variable names without showing values
- Ask about configuration patterns and structure
- Describe what needs to be configured without sharing secrets
- Handle `.env` files manually outside AI assistance
- Use AI for logic and code architecture, not secret management

### ✗ DON'T
- Paste `.env` files or configuration content into AI chat
- Ask AI to help debug secret values or credentials
- Expect AI to read or modify protected files
- Try to work around the restrictions
- Share secret content when asking for AI help

## Project Structure

```
ai-settings/
├── README.md                      # This file
├── AI_SECURITY_GUIDE.html         # Interactive guide for team members
├── .claude/
│   └── settings.json             # Claude Code security rules
├── .gemini/
│   └── settings.json            # Gemini CLI security rules
├── .geminiignore                 # Gemini CLI ignore patterns
├── .zed/
│   └── settings.json            # Zed AI security rules
├── opencode.json                 # OpenCode security configuration
├── .copilot-instructions         # GitHub Copilot guidelines
└── .gitignore                    # Git protection patterns
```

## AI Assistant Configuration Comparison

| Feature | Claude Code | Gemini CLI | Zed | OpenCode | GitHub Copilot | Git |
|---------|-------------|------------|-----|----------|----------------|-----|
| **Configuration File** | `.claude/settings.json` | `.gemini/settings.json`, `.geminiignore` | `.zed/settings.json` | `opencode.json` | `.copilot-instructions` | `.gitignore` |
| **Format** | JSON (permissions list) | JSON + Text | JSON (permissions + security schema) | JSON (structured) | Text (guidelines) | Text (patterns) |
| **Enforcement Level** | Hard block | Hard block (via ignore) | Hard block | Hard block | Soft guidance | Prevent commits |
| **Read Protection** | ✓ | ✓ | ✓ | ✓ | ✓ | N/A |
| **Write Protection** | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| **Execute Protection** | N/A | N/A | N/A | ✓ | N/A | N/A |
| **Team Scope** | All users | All users | All users | All users | All users | All users |
| **Metadata Support** | ✗ | ✗ | ✓ | ✓ | N/A | N/A |
| **File Patterns** | Glob patterns | Glob patterns | Glob patterns | Path patterns | Text references | Glob patterns |
| **Commitment Level** | Project-wide | Project-wide | Project-wide | Project-wide | Per-user setting | Project-wide |

## FAQ

**Q: Can I override these restrictions?**
A: Users can create `.claude/settings.local.json` for personal overrides, but this is not recommended for security reasons. Project-level settings apply to everyone.

**Q: Will this slow down my development?**
A: No. The restrictions are transparent. You simply use environment variables and configuration patterns, which are best practices anyway.

**Q: What if I need to work with secret files?**
A: Handle them manually outside of AI assistants using your code editor or terminal directly.

**Q: Can I see these restrictions in action?**
A: Yes! Try asking Claude Code to read the `.env` file. You'll see the permission denied error, which demonstrates the security is working.

## Security Considerations

These restrictions provide layered protection:

1. **Multiple Mechanisms**: Different tools (Claude Code, GitHub Copilot, Git) each provide a layer
2. **Defense in Depth**: If one layer fails, others still protect your secrets
3. **Automatic Application**: Settings are in the repository, so they apply automatically to all team members
4. **Team-Wide**: No individual setup required - clone and you're protected

## Contact & Support

- For security issues or concerns, contact your security team
- For questions about the setup, refer to the `AI_SECURITY_GUIDE.html`
- For modifications or customizations, edit the configuration files and test thoroughly

---

**Created**: May 2026  
**Project Type**: Security Configuration Template  
**Tools**: Claude Code, GitHub Copilot, Git  
**Status**: ✅ Active and Verified
