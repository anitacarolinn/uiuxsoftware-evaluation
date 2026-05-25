# Figma MCP for Coding Agents — Blog Notes

> Reference notes for updating the design tools evaluation deck.
> Two related Figma blog posts about opening Figma to AI agents via MCP.

---

## Blog 1: "FigJam Is Now Your Coding Agent's Whiteboard Too"

- **URL:** https://www.figma.com/blog/figjam-your-coding-agents-whiteboard/
- **Author:** Caroline Okun (Software Engineer at Figma)
- **Date:** 2026-04-28

### Main Thesis

As coding agents accelerate development speed, teams need **visual collaboration tools** to handle architectural complexity and **maintain code quality through agent-assisted design reviews**.

> "Every agent-written PR we merge without deep human review adds confusion and hidden complexities to the codebase." — Caroline Okun

**Translation:** AI writes code incredibly fast, but if PRs get merged without serious review, the codebase silently rots. Solution = review using visual tools (FigJam), not just PR text.

### 6 Tools Released

| Tool | Function |
|---|---|
| `figma-use-figjam` | MCP skill — agents can read/write directly to FigJam boards |
| `generate_diagram` | Extended tool — generates complex architecture diagrams + ERDs |
| `generate-project-plan` | Workflow skill — converts specs + codebase into visual board |
| `use_figma` | (existing) — agents create/edit Figma designs |
| `create_new_file` | Agent can generate designs in a new Figma file |
| `get_figjam` | Retrieve FigJam board content back into the coding env |

### 9 Supported AI Clients

Augment, **Claude Code**, Codex CLI, Copilot CLI, Copilot in VS Code, **Cursor**, Factory, Kiro, Warp

### Pricing

- **Now:** Free during Beta (Figma still learning usage patterns)
- **Future:** Paid API, integrated into Figma's seat-based pricing model

### 3-Step Workflow: Research → Collaborate → Implement

**Step 1: Research, Plan & Visualize**
- Agent fetches MCP server docs + codebase context
- Identifies solutions + trade-offs
- Maps subtasks to stacked PRs
- Generates architecture diagrams + notes via `generate_diagram` & `figma-use-figjam`
- Result: wall of markdown → visual board the team can understand

**Step 2: Collaborate Before Coding**
- Team reviews FigJam board (not PR text)
- Comments/feedback directly on canvas (hover, drawing, sticky notes)
- Discusses implementation with remote teams on the same canvas
- Architecture decisions visualized BEFORE code is written

**Step 3: Implement**
- Developer uses `get_figjam` to extract board content into coding env
- Implements with full architectural context
- PR includes link to FigJam board → reviewer also has full context
- Not screenshot copying — agent reads board as **executable context**

### Technical Capabilities

- Architecture diagram generation from markdown specs
- ERD (Entity-Relationship Diagram) creation for database schemas
- Direct agent read/write access to FigJam collaborative spaces
- Code block + annotation embedding in visual boards
- Bidirectional workflow: agent generates → human reviews → agent consumes

### Use Cases

- Engineering critiques
- Tech specs
- Onboarding docs
- PRDs (Product Requirements Documents)
- Architecture planning for new tools
- Cross-functional collaboration (Engineer + PM + Designer + AI Agent)

### Conclusion

Tools are **foundational building blocks** for dev workflows. Teams encouraged to build custom skills on top of `figma-use-figjam` and `figma-generate-diagram` to match their processes.

---

## Blog 2: "Agents, Meet the Figma Canvas" (companion post, ~5 weeks earlier)

- **URL:** https://www.figma.com/blog/the-figma-canvas-is-now-open-to-agents/
- **Author:** Matt Colyer (Product Director at Figma)
- **Date:** 2026-03-24

### Main Thesis

Figma opens its Design canvas to AI agents via MCP server. Agents can write directly to Figma files using team's design system. Skills system (markdown-based instructions) lets teams encode conventions for the agent.

### Key Tools

- `use_figma` — agent writes directly to Figma files, creates/modifies design assets linked to design systems
- `generate_figma_design` — converts HTML from live apps into editable Figma layers (Code-to-Canvas flow)

### Skills System (NEW concept)

**Skills = Markdown-based instructions** that guide how agents build on the canvas. Encode team conventions as executable rules.

**9 Example Skills launched:**

| Skill | Function |
|---|---|
| `/figma-generate-library` | Creates components from codebases |
| `/figma-generate-design` | Generates designs using existing components |
| `/create-voice` | Generates screen reader specs (from Uber) |
| `/cc-figma-component` | Generates components from JSON contracts |
| `/apply-design-system` | Connects designs to system components |
| `/rad-spacing` | Applies hierarchical spacing with variables |
| `/edit-figma-design` | Orchestrates design workflows |
| `/sync-figma-token` | Syncs design tokens with drift detection |
| `/multi-agent` | Runs parallel workflows |

Plus foundational skill `/figma-use` for baseline understanding of Figma structure.

### Supported Clients (9, slightly different list)

Augment, Claude Code, Codex, Copilot CLI, Copilot in VS Code, Cursor, Factory, **Firebender** (vs Kiro in April post), Warp

### Key Quotes

> "Codex can find and use all the important design context in Figma to help us build higher quality products more efficiently." — Ed Bayes, Codex Design Lead, OpenAI

> "Skills teach Claude Code how to work directly in the design canvas, so you can build in a way that stays true to your team's intent and judgment." — Cat Wu, Head of Product for Claude Code, Anthropic

### Future Roadmap (per Matt Colyer)

- Image support
- Custom fonts
- Plugin API parity

---

## How the Two Blogs Connect

| March 24: Figma Canvas | April 28: FigJam |
|---|---|
| Opens Figma **Design** canvas to agents | Opens **FigJam** whiteboard to agents |
| Tools: `use_figma`, `generate_figma_design` + Skills | Tools: `generate_diagram`, `get_figjam`, `figma-use-figjam` |
| Goal: **execution** (build the design) | Goal: **planning + collaboration** (think before coding) |
| Use case: AI creates/edits UI designs | Use case: AI generates architecture diagrams, team plans visually |

**Complementary, not duplicate** — March 24 for producing designs, April 28 for planning architecture before coding. Both via MCP, both free during Beta.

---

## Implications for Design Tools Evaluation Deck

### New Figma Strengths to Add

1. **Skills system** — unique to Figma; lets teams encode conventions as markdown rules (no other tool has this)
2. **Code-to-Canvas + Canvas-to-Code full loop** — `generate_figma_design` (HTML → Figma) + `use_figma` (agent edits design)
3. **Agent infrastructure for full workflow** — planning (FigJam) + execution (Design canvas) + implementation (back to IDE)
4. **9-client AI ecosystem support** — works with Claude Code, Cursor, Copilot, Codex, Augment, etc.

### Updates Needed in Deck

- **Slide 5 (AI Feature Comparison)** — Figma's "MCP Server" cell currently says "Read + Write". Update to reflect the 6+ tools shipped (FigJam + Canvas), Skills system.
- **Slide 6 (Pros & Cons matrix)** — Add new Figma strength: "Skills system + agent workflow infrastructure"
- **Possibly new slide / section** — "AI Agent Integration" comparing all 5 tools' MCP capabilities (since Figma has now leapfrogged here)

### Re-evaluation Note

Previously framed Figma as "best collab + plugin ecosystem" — now also adds **strongest AI agent infrastructure** dimension. This shifts the evaluation: Figma isn't just for 美編 anymore — it's also a strong choice for vibe coders working with AI agents.

---

> Source: Figma official blog, 2026-03-24 and 2026-04-28
> Notes saved: 2026-04-30
