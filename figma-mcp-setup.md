# Figma MCP Setup Guide

> Quick guide to connect Figma to Claude Code (or Cursor / Copilot CLI / etc.) so AI agents can read/write Figma files and FigJam boards via MCP.

---

## Prerequisites

- ✅ A Figma account (free or paid — both work)
- ✅ Claude Code installed (or Cursor / Copilot CLI / Codex / etc.)
- ✅ Node.js installed (for `npx` to run the MCP server)

---

## Setup Steps

### 1. Generate Figma Personal Access Token

1. Login to [figma.com](https://figma.com)
2. Click your avatar (top-right) → **Settings**
3. Scroll to **Security** section
4. Click **Personal access tokens** → **Generate new token**
5. Name it: `Claude Code MCP` (or any descriptive name)
6. Set **expiration** if available (90 days recommended)

### 2. Set Minimal Scopes (5 required)

Check **only these 5 scopes** for safe minimal access:

| Section | Scope | Purpose |
|---|---|---|
| **Users** | ☑ Read current user's name, email, profile image | Identify you to MCP |
| **Files** | ☑ Read the contents of and render images from files | Core read access (FigJam + Design files) |
| **Files** | ☑ Read metadata of files | List/navigate files |
| **Design systems** | ☑ Read variables in accessible files | Read design tokens for consistency |
| **Design systems** | ☑ Read data about individual components and styles | Use existing components when generating |

**Skip everything else** unless you have a specific need (see "Advanced scopes" below).

### 3. Copy the Token

- Token format: `figd_xxxxxxxxxxxxxxxxx`
- ⚠️ **Token only shown once** — save it somewhere safe (password manager)

### 4. Configure Claude Code

Edit your Claude Code config file:

- **Mac**: `~/Library/Application Support/Claude/claude_desktop_config.json`
- **Windows**: `%APPDATA%\Claude\claude_desktop_config.json`

Add Figma MCP server entry:

```json
{
  "mcpServers": {
    "figma": {
      "command": "npx",
      "args": ["-y", "@figma/mcp-server"],
      "env": {
        "FIGMA_ACCESS_TOKEN": "figd_xxxxxxxxxxxxxxxxx"
      }
    }
  }
}
```

> ⚠️ Exact package name (`@figma/mcp-server`) may vary — check official Figma MCP docs for the current package.

### 5. Restart Claude Code & Verify

- Close Claude Code completely
- Re-open it
- Prompt: `What Figma MCP tools/skills are available?`

You should see tools like:
- `use_figma`
- `generate_figma_design`
- `generate_diagram`
- `figma-use-figjam`
- `get_figjam`
- `create_new_file`
- `generate-project-plan`

---

## How to Use the Skills

### Generate an Architecture Diagram on FigJam

```
Generate a FigJam architecture diagram of this codebase.
Show all services, database connections, and external APIs.
```

Claude calls `generate_diagram` → new FigJam board appears in your Figma account.

### Convert a Live Website to Figma

```
Convert https://example.com/landing to an editable Figma design.
```

Claude calls `generate_figma_design` → fetches HTML → creates editable Figma file.

### Create a Design from Scratch

```
Use Figma to create a landing page design for product X.
Use my brand colors (read from existing variables).
```

Claude calls `use_figma` → design appears in your Figma account.

### Pull FigJam Context Back to Code

```
Read the FigJam board at [URL] and implement the architecture
in src/services/.
```

Claude calls `get_figjam` → reads board content → implements code with full context.

### Update an Existing FigJam Board

```
Update the FigJam board at [URL] — add a Redis queue between
the API and the worker service.
```

Claude calls `figma-use-figjam` → modifies the board.

---

## Workflow: Research → Collaborate → Implement

This is the workflow Figma proposes in their April 2026 blog:

```
1. Research / Plan
   You: "Generate FigJam diagram of feature X"
   AI:   calls generate_diagram → new board

2. Collaborate
   You: share board with team
   Team: comments + suggestions on FigJam
   You: "Update the board with team's feedback"

3. Implement
   You: "Pull FigJam context, then implement feature X"
   AI:   calls get_figjam → reads board → writes code
   You: PR includes link to FigJam board for reviewers
```

---

## Pricing

- **Now**: Free during Beta period (Figma still learning usage patterns)
- **Future**: Paid API, integrated into Figma's seat-based pricing model

---

## Advanced Scopes (Optional)

Add these only if needed:

| Scope | When to add |
|---|---|
| Files: Read comments | If AI should read team feedback from boards |
| Files: Create/modify comments | If AI should leave comments/responses |
| Projects: Read team project structure | If you want AI to navigate team file hierarchy |
| Development: Read dev resources | If linking designs to code files |
| Development: Write component code | Only if using **Code Connect** (Figma↔code mapping) |
| Design systems: Create/modify variables | ⚠️ Risky on Team plan — affects everyone's tokens |
| Design systems: Read team library | If AI should use shared component library |

---

## Security Tips

1. **Set token expiration** — 30-90 days recommended, regenerate periodically
2. **Don't commit token to git** — keep config files in `.gitignore`
3. **If token leaks**: Revoke immediately at Figma → Settings → Personal access tokens
4. **Team/Org plan**: Consider creating a separate Figma account just for AI experiments to limit blast radius
5. **Principle of least privilege**: Only enable scopes you actually use

---

## Troubleshooting

| Problem | Likely cause | Fix |
|---|---|---|
| MCP tools not showing in Claude Code | Config syntax error | Validate JSON, check for trailing commas |
| "Unauthorized" errors | Wrong token / expired | Regenerate token |
| "Can't write to file" | Missing scope | Add required scopes (write capability is granted by Figma's MCP server) |
| FigJam board not appearing | Wrong account | Check you're logged into Figma with same account as token |

---

## References

- Figma Blog (Mar 24, 2026): [Agents, Meet the Figma Canvas](https://www.figma.com/blog/the-figma-canvas-is-now-open-to-agents/)
- Figma Blog (Apr 28, 2026): [FigJam Is Your Coding Agent's Whiteboard Too](https://www.figma.com/blog/figjam-your-coding-agents-whiteboard/)
- Figma MCP docs: figma.com/developers/mcp (check for latest)

---

> Last updated: 2026-05-01
