# Kobozo Plugins for OpenCode

This directory contains all Kobozo plugins restructured for **OpenCode** compatibility.

## What is OpenCode?

[OpenCode](https://opencode.ai) is an AI coding agent built for the terminal. It's similar to Claude Code but with a different architecture and configuration system.

## Directory Structure

```
opencode/
├── opencode.json          # Main configuration file
├── agent/                 # 71 specialized agents
│   ├── ui-analyzer.md
│   ├── bug-analyzer.md
│   ├── code-reviewer.md
│   └── ... (68 more)
├── command/               # 45 custom commands
│   ├── ui-check.md
│   ├── fix-bug.md
│   ├── brainstorm.md
│   └── ... (42 more)
├── plugin/                # Custom JavaScript/TypeScript plugins (empty for now)
└── README.md              # This file
```

## Installation

### Option 1: Symbolic Link (Recommended for Testing)

Create a symbolic link from your OpenCode config directory to this folder:

```bash
# Navigate to your home directory
cd ~

# Create the .config/opencode directory if it doesn't exist
mkdir -p ~/.config/opencode

# Create symbolic link to this directory
ln -s /path/to/kobozo-plugin/opencode ~/.config/opencode

# Or if you want to link individual directories:
ln -s /path/to/kobozo-plugin/opencode/agent ~/.config/opencode/agent
ln -s /path/to/kobozo-plugin/opencode/command ~/.config/opencode/command
ln -s /path/to/kobozo-plugin/opencode/opencode.json ~/.config/opencode/opencode.json
```

**Replace `/path/to/kobozo-plugin`** with the actual path to this repository.

### Option 2: Copy Files

Copy the contents to your OpenCode config directory:

```bash
# Copy all agents
cp -r opencode/agent/* ~/.config/opencode/agent/

# Copy all commands
cp -r opencode/command/* ~/.config/opencode/command/

# Copy configuration (merge with existing if needed)
cp opencode/opencode.json ~/.config/opencode/opencode.json
```

### Option 3: Per-Project Installation

You can also use these plugins on a per-project basis:

```bash
# In your project root
mkdir -p .opencode

# Create symbolic links
ln -s /path/to/kobozo-plugin/opencode/agent .opencode/agent
ln -s /path/to/kobozo-plugin/opencode/command .opencode/command
ln -s /path/to/kobozo-plugin/opencode/opencode.json .opencode/opencode.json
```

## Available Agents (71)

Agents are specialized AI assistants for specific tasks. Invoke them with `@agent-name`:

### UI & Design
- `ui-analyzer` - Analyze UI screenshots against style guides
- `playwright-tester` - Automate UI testing with Playwright
- `component-generator` - Generate React components
- `style-guide-builder` - Create comprehensive style guides
- `design-system-manager` - Manage design systems

### Development & Debugging
- `bug-analyzer` - Deep bug analysis
- `fix-implementer` - Implement bug fixes
- `test-validator` - Validate fixes with tests
- `code-explorer` - Explore codebase patterns
- `code-reviewer` - Review code quality

### Testing
- `test-generator` - Generate unit/integration tests
- `coverage-analyzer` - Analyze test coverage
- `playwright-auth-generator` - Generate auth tests
- `page-object-builder` - Build page objects

### Security
- `auth-reviewer` - Review authentication
- `code-security-analyzer` - Analyze security vulnerabilities
- `dependency-scanner` - Scan dependency vulnerabilities
- `gdpr-compliance-checker` - Check GDPR compliance

### Performance
- `performance-analyzer` - Analyze performance
- `bundle-optimizer` - Optimize bundle size
- `query-optimizer` - Optimize database queries

### Architecture
- `architecture-mapper` - Map architecture
- `dependency-analyzer` - Analyze dependencies
- `documentation-generator` - Generate docs
- `solution-architect` - Design solutions

### And 47 more specialized agents!

## Available Commands (45)

Commands are shortcuts for common tasks. Use them with `/command-name`:

### UI Commands
- `/ui-check [page]` - Check UI against style guide
- `/create-component [name]` - Create React component
- `/create-style-guide` - Generate style guide
- `/setup-design-system` - Setup Tailwind design system

### Development Commands
- `/fix-bug [description]` - Fix bugs systematically
- `/feature-dev [description]` - Develop features
- `/brainstorm [idea]` - Research and architect ideas
- `/code-expert [query]` - Deep code research

### Testing Commands
- `/generate-tests` - Generate test suites
- `/coverage-report` - Analyze coverage
- `/generate-playwright-e2e` - Generate E2E tests
- `/generate-playwright-auth-tests` - Generate auth tests

### Security Commands
- `/security-audit` - Comprehensive security audit
- `/dependency-check` - Check dependencies
- `/privacy-audit` - GDPR compliance check

### Performance Commands
- `/profile-performance` - Profile performance
- `/optimize-bundle` - Optimize bundle

### Documentation Commands
- `/api-docs` - Generate API docs
- `/document-this [subject]` - Create documentation

### And 25 more commands!

## MCP Servers Configuration

The `opencode.json` includes several MCP (Model Context Protocol) servers:

### Enabled by Default
- **playwright** - UI testing automation
- **context7** - Documentation search (requires `CONTEXT7_API_KEY`)

### Disabled by Default (Enable as Needed)
- **nano-banana** - Gemini image generation (requires `GEMINI_API_KEY`)
- **dalle** - DALL-E image generation (requires `OPENAI_API_KEY`)
- **chunkhound** - Deep code analysis
- **docker** - Docker/Podman container management

### Environment Variables

Set these environment variables for MCP servers:

```bash
export CONTEXT7_API_KEY=your_context7_api_key
export GEMINI_API_KEY=your_gemini_api_key
export OPENAI_API_KEY=your_openai_api_key
```

### Enable/Disable MCP Servers

Edit `opencode/opencode.json`:

```json
{
  "mcp": {
    "chunkhound": {
      "enabled": true  // Change to true to enable
    }
  }
}
```

## Usage Examples

### Using Commands

```bash
# Check UI compliance
/ui-check dashboard

# Fix a bug
/fix-bug "Payment processing fails with invalid discount codes"

# Research a feature
/brainstorm "Real-time notification system with WebSockets"

# Generate tests
/generate-tests

# Security audit
/security-audit
```

### Using Agents

```bash
# Invoke an agent directly
@ui-analyzer please analyze the login page screenshot

# Use in conversation
Can you help me with performance? @performance-analyzer

# Multiple agents in workflow
@bug-analyzer find the root cause, then @fix-implementer apply the fix
```

### Switching Between Build and Plan Mode

OpenCode has built-in agents:
- **build** - Full development with all tools (default)
- **plan** - Analysis only, no file changes

Use **Tab** key to switch between them during a session.

## Differences from Claude Code

| Feature | Claude Code | OpenCode |
|---------|-------------|----------|
| Config Location | `.claude-plugin/` | `.opencode/` |
| Main Config | `plugin.json` | `opencode.json` |
| Agent Location | `agents/` in plugin | `.opencode/agent/` |
| Command Location | `commands/` in plugin | `.opencode/command/` |
| MCP Config | In `plugin.json` | In `opencode.json` |
| Plugin System | Marketplace-based | Direct file placement |
| Multi-Plugin | Yes (separate plugins) | No (flat structure) |

## Troubleshooting

### Commands/Agents Not Found

1. Verify the symbolic link exists:
   ```bash
   ls -la ~/.config/opencode
   ```

2. Check OpenCode is using the right config:
   ```bash
   opencode --version
   ```

3. Try restarting OpenCode

### MCP Servers Not Working

1. Check environment variables are set:
   ```bash
   echo $CONTEXT7_API_KEY
   ```

2. Verify MCP server is enabled in `opencode.json`

3. Check MCP server timeout (increase if needed):
   ```json
   {
     "mcp": {
       "playwright": {
         "timeout": 15000
       }
     }
   }
   ```

### Too Many Tools Warning

OpenCode may warn about context size if too many MCP servers are enabled. Disable unused MCP servers in `opencode.json`.

## Technical Notes

### Agent Frontmatter Format

All agents have been converted to OpenCode's frontmatter format:

**Supported fields:**
- `description` (required) - Brief description of the agent
- `tools` (object) - Tools the agent can use (e.g., `bash: true`)
- `mode` (string) - Agent mode: primary/subagent/all
- `temperature` (number) - 0.0-1.0
- `disable` (boolean) - Disable the agent
- `permission` (object) - Tool permissions

**Removed from Claude Code format:**
- ❌ `name` - Filename is used as agent name
- ❌ `color` - Not supported
- ❌ `model` shortcuts - Use full provider/model format in opencode.json

## Contributing

This directory is auto-generated from the main plugin repository. To add or modify plugins:

1. Edit plugins in `plugins/` or `claude/plugins/` directories
2. The `opencode/` directory will be regenerated
3. Keep both structures in sync

## Support

- **OpenCode Docs**: https://opencode.ai/docs
- **Repository Issues**: https://github.com/kobozo/kobozo-plugin
- **Author**: Yannick De Backer (yannick@kobozo.eu)

## License

Custom plugin collection for Kobozo development.

---

**Total Agents**: 71
**Total Commands**: 45
**MCP Servers**: 6
**Last Updated**: 2025-11-13
