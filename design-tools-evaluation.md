# Design Tools Evaluation 2026

> Figma Make vs Paper vs Stitch vs AI Studio vs Claude Design
> For Vibe Coders and Visual Designers (美編)

**Last updated:** 2026-05-01
**Slides:** 13

---

## 1. Overview — Five Tools, Five Philosophies

| Tool | Type | Maturity | Output | Best for | Desktop |
|---|---|---|---|---|---|
| **Figma Make** | AI Generative Design (Figma) | Built on Figma (10+ years) | React code + Figma design | 美編 | ✓ via Figma |
| **Paper** | Code-Native Design | Open alpha (Radix UI founder) | HTML / CSS / Tailwind | Vibe Coder | ✗ web only |
| **Stitch AI** | AI UI Generator | Google Labs (Gemini 2.5) | 7 frameworks + Figma | Both | ✗ web only |
| **AI Studio** | Full-Stack App Builder | GA, free IDE by Google | Full-stack web apps | Vibe Coder | ✗ web only |
| **Claude Design** | AI Design Workspace | Research preview (Anthropic) | Handoff → Claude Code | Both | ✗ web only |

---

## 2. Cost Comparison

| Tool | Free | Pro / Team | Enterprise | Notes |
|---|---|---|---|---|
| **Figma Make** | 3 files | $16/editor/mo | $55-90/editor/mo | 大團隊成本可觀 |
| **Paper** | 100 MCP calls/week | $16-20/user/mo | Coming soon | 免費版 MCP 額度不夠用 |
| **Stitch AI** | 350 std + 200 pro gen/mo | Coming soon | N/A | 目前完全免費，額度充裕 |
| **AI Studio** | 完全免費 | API token 計費 | Vertex AI | 部署到 Cloud Run 另計 |
| **Claude Design** | 無獨立免費版 | 含在 Pro/Max/Team 內 | 含在 Enterprise 內 | 獨立額度，無額外費用 |

---

## 3. How They Feel to Use (Editor Experience)

| Feature | Figma Make | Paper | Stitch | AI Studio | Claude Design |
|---|---|---|---|---|---|
| **Real-time Collab** | Share only<br>(live AI co-edit only in Figma Design) | Basic (alpha) | None | Share only | None |
| **Interactive Preview** | Advanced (interactions + animation) | Not yet | Page-to-page interactive flows | Live preview (runs the app) | AI-generated prototypes (hover/toggle) |
| **Component & Library** | No (need export to Figma Design) | Yes (via MCP) | Paste URL to extract site styles | None | Auto-reads from your codebase |
| **Built-in Code Export\*** | React code via Make/MCP | Native HTML/CSS | 7-framework dedicated buttons | Full-stack (+ download) | Handoff → Claude Code |
| **Other Export** | .fig + React code | HTML/CSS | Paste to Figma + Code export | Deploy to Cloud Run + Download as website | PDF / PPTX / Canva |

> **\*** Semua tools sebenarnya bisa output framework apapun via AI prompt, MCP, atau handoff. Row ini track **built-in dedicated export** yang langsung tersedia tanpa perlu prompt tambahan — bukan satu-satunya cara untuk dapat code.

---

## 4. AI Feature Comparison

| AI Feature | Figma Make | Paper | Stitch | AI Studio | Claude Design |
|---|---|---|---|---|---|
| **Text-to-Design** | First Draft | Via MCP | Core (5 screens) | Core (full app) | Core (conversation) |
| **Comment** | No | No | No | Click to comment/edit | Inline comments + edits |
| **MCP Server** | Read + Write | 24 tools | stitch-mcp | Gemini MCP | Via Claude Code |
| **Deploy** | No | No | No | Cloud Run + Download | Via Claude Code |

---

## 5. Methodology — Same Prompt, 5 Tools

I tested all 5 UI/UX tools using the **same detailed prompt** — apples-to-apples comparison so you can see how different tools interpret the same brief.

**Test scenario:** Disaster Relief Dashboard — same brief, same goal across all 5.

**Why same prompt:**
- Removes "I prompted differently" as excuse for output differences
- Reveals how each tool interprets the same brief
- Lets us compare quality, speed, and workflow fairly

---

## 6. Testing Notes — Figma Make

**Verdict:** Great for simple SPA + quick deploy. Skip for complex apps.

### Strengths
- **Publish site directly** from Figma Make — no separate hosting setup
- **GitHub + Supabase integrations** — auto-create repo, connect DB to Supabase
- **npm registry support** — install any npm package (`framer-motion`, `react-router`, `recharts`)
- **Connected domains** — use your own custom domain (GoDaddy/Namecheap/Cloudflare) instead of `.figma.site`
- **Favicon, title, metadata** editable directly in Figma Make settings
- **Direct code edit available** — engineer can edit `App.tsx` directly (note: contradicts pure vibe-coding flow)
- Good fit for **simple SPA** (single-page app)

### Weaknesses
- **No GUI canvas editing** — can't drag/click to fine-tune like Figma Design. Edit content (banner text, data, layout) only via prompt or direct code edit
- **No responsive preview toggle** — no built-in Mobile/Tablet/Desktop switcher. Must prompt "show mobile view" or verify after deploy
- **Export to Figma Design = one-way street** — manual edits in Figma Design don't sync back to Figma Make
- **Not great for multi-page + data-heavy sites** — better for simple sites only

### Links
- Live deployed site: https://stem-stand-02084533.figma.site/
- Figma Make project: https://www.figma.com/make/3p1G2MYQGBoIvHS8ZIwdDv/Disaster-Relief-Dashboard-Design?p=f&t=pEvCYrEibb7Iy6Iy-0

---

## 7. Testing Notes — Paper Design

**Verdict:** Clean UI output + GUI edit makes it my project go-to — just don't expect interactive UX or one-click deploy.

### Strengths
- **Connect via Claude MCP** — I use Claude (with Paper's MCP) to generate the design, then open in Paper to fine-tune
- **UI quality is clean** — my go-to tool for actual projects because the output looks polished
- **GUI editor for detail edits** — 美編 can drag/click to fine-tune (unlike Figma Make which is prompt-only)
- **Tailwind CSS native** — output uses utility classes ready to ship (engineer-friendly)

### Weaknesses
- **Pure UI only — no UX** — click a button, nothing happens. No popups, no interactions, no JS logic
- **No interactive preview** — can't simulate flows / click-through demos like Figma Design's prototyping mode
- **Separate subscription from Claude** — total cost ~$36-40/mo (Paper $16-20 + Claude Pro $20)

### Workflow
Claude (MCP) → generate design → open in Paper → fine-tune via GUI → generate code for website

### Links
- Paper project: https://app.paper.design/file/01KPMV40MNX7WF0B4VCVYYVR9T/1-0

---

## 8. Testing Notes — Stitch AI

**Verdict:** Free + 8 export paths make it the easiest "first-draft generator" — just don't expect interactive prototypes or GUI editing.

### Strengths
- **Free** — Google Labs, generous limits (350 standard + 200 pro generations/month)
- **Direct text editing** — click text in canvas to edit inline (the only thing you can edit without a prompt)
- **Design system / component library** — set color theme + font tokens, applied across the design
- **Output = pure HTML** — code is straightforward, easy to use anywhere
- **Tons of export options** — see breakdown below

### Weaknesses
- **Prompt-only editing** — no GUI editor for layout/elements. Only text can be edited inline
- **Very limited interactions** — only hover / active button states. Click button → *nothing happens*. No page navigation, no popups, no modals
- **Single version per prompt** — can't generate multiple style variants in one shot (vs Claude/AI Studio)
- **Future pricing unknown** — currently free as Google Labs experiment, may change

### Export Options (8 ways)
| Option | Description |
|---|---|
| **AI Studio** | Open in Google AI Studio |
| **Figma** | Paste with Auto Layout |
| **Jules** | Google's autonomous AI coding agent (jules.google) — sends design as task, Jules implements |
| **.zip** | Download HTML + CSS + assets |
| **Code to clipboard** | Raw HTML/CSS, paste anywhere |
| **MCP** | For AI agents (Claude Code / Cursor) to consume |
| **Project Brief** | Markdown spec doc for devs/AI |
| **Instant Prototype** | Live shareable preview link, no deploy needed |

### Workflow
Prompt → Stitch generate → iterate via prompt → export (Figma / .zip / Jules / etc.)

### Links
- Stitch project: https://stitch.withgoogle.com/projects/10574739860128708197

---

## 9. Testing Notes — Google AI Studio

**Verdict:** Best for "build something that works fast" — especially full-stack apps. Skip for fine visual design work.

### Strengths
- **Multiple style options at start** — pick from several layouts/styles before committing (vs single output tools)
- **Focused on full website / complete-flow** — generates working sites, not just static UI
- **GUI editor for color, font, size** — visual tweaks without prompt
- **Edit content: prompt OR direct code** — flexibility for both audiences
- **Remix button** — fork existing apps from App Gallery as starting point (like GitHub fork, but 1-click). Great for learning / templates
- **Integrations + Secrets** — connect API keys, GitHub repo
  - *Integrations* = pre-built connectors (1-click connect)
  - *Secrets* = raw env vars you manage yourself

### Weaknesses
- **UI quality less polished** — output is functional but not "designer pretty" like Figma Make / Paper
- **Not for fine visual design** — better at "make it work" than "make it beautiful"
- **No design system management** — can set basic styles via GUI but no reusable component library

### Publish — 2 paths
1. **Built-in publish** — deploy to Google Cloud Run 1-click. URL: `xxx.run.app`. Cloud Run = serverless, free tier available
2. **Download as website (.zip)** — export static files, deploy anywhere: Cloudflare Pages, Vercel, Netlify, GitHub Pages, AWS, dll

### Workflow
Pick style → AI generates full app → GUI tweak (colors/fonts) → prompt or code edit → publish (Cloud Run / .zip)

### Links
- AI Studio project: https://ai.studio/apps/57bb988c-4d21-4ddd-ba8a-1be79dffa5a3

---

## 10. Testing Notes — Claude Design

**Verdict:** Most polished interactive UX + most flexible editing (prompt+GUI+draw). Best fit if you already have Claude Pro.

### Strengths
- **Asks detailed questions first** — before generating, Claude clarifies direction (target audience, style, key features). Refines intent → better output
- **Built-in interactive UX** — click button → popup actually appears. Real interactions baked in, not just visual
- **Tweaks function** — select element → AI generates contextual drag sliders (padding, radius, font weight, color). Drag instead of typing prompts
- **GUI editor like Figma Design** — drag, resize, edit visually (not prompt-only)
- **Draw on canvas** — sketch rough wireframe with pencil, Claude reads your drawing & turns it into real design
- **Inline comments** — leave notes on design elements (like Google Docs comments)
- **Live preview site** — test interactions before exporting
- **Token separate from chat** — heavy Claude chat usage ≠ design quota burned. Independent quotas
- **No extra cost if already on Claude Pro** — included in subscription (vs Paper +$16-20/mo on top of Claude)

### Weaknesses
- **Weekly quota limit** — independent limit per week. Heavy use = wait for reset. Check current at `claude.ai/settings`
- **Browser-only (claude.ai)** — no desktop app, no offline mode. Internet drops = no work
- **Output quality depends on Q&A investment** — lazy answers to clarifying questions = mediocre output. Requires thoughtful input

### Workflow
Prompt → answer Q&A → Claude generates with interactions → tweak via GUI/draw/sliders → preview → export (PDF/PPTX/Canva or handoff to Claude Code)

### Links
- Claude Design project: https://claude.ai/design/p/decda9f3-7703-4882-a1bb-cf1b4430b3d4?file=dashboard.html&via=share

---

## 11. Late-Breaking Update — Figma Just Pivoted to AI Agents

Two Figma blog posts (March + April 2026) announced **MCP-based AI agent integration** — opening both Figma Design canvas *and* FigJam whiteboard to coding agents like Claude Code, Cursor, Copilot.

### Mar 24 — "Agents, Meet the Figma Canvas"
**Goal: execution** — AI builds the design

- `use_figma` — agent writes directly to Figma files
- `generate_figma_design` — HTML → editable Figma layers
- **Skills system** — markdown instructions encoding team conventions (9 example skills launched)
- Blog: https://www.figma.com/blog/the-figma-canvas-is-now-open-to-agents/

### Apr 28 — "FigJam Is Your Coding Agent's Whiteboard Too"
**Goal: planning** — think before code

- `generate_diagram` — architecture / ERD diagrams
- `figma-use-figjam` — agent reads/writes FigJam
- `get_figjam` — bring board context back to IDE
- **Workflow:** Research → Collaborate → Implement
- Blog: https://www.figma.com/blog/figjam-your-coding-agents-whiteboard/

### Key Facts
| | Detail |
|---|---|
| **Pricing** | Free during Beta, will become paid (integrated with Figma seat plans) |
| **9 supported clients** | Claude Code, Cursor, Copilot CLI/VS Code, Codex, Augment, Factory, Kiro/Firebender, Warp |
| **Total tools** | 6+ MCP tools + Skills system = most extensive AI agent infrastructure of any design tool |

### What this means for the evaluation
Previously framed Figma as "best for 美編 + plugin ecosystem." Now also adds **strongest AI agent infrastructure** — making Figma a serious option for vibe coders too, not just visual designers.

---

## 12. Conclusion — Each Tool Has Its Best-Fit Person

After testing all 5 tools with the same disaster-dashboard prompt, every tool has real strengths. Here's the role and scenario each one is best for.

| Tool | ★ Best for | Why | Scenario |
|---|---|---|---|
| 🎨 **Figma Make** | 美編 / designers already on Figma | Familiar Figma interface + AI generation. Full design tooling and plugin ecosystem already in workflow. | Team has a Figma workflow and wants to add AI generation |
| 📐 **Paper** | Designers + developers who care about code quality | Design *is* code — cleanest output. Drag-and-drop editing, most polished visuals. | Hi-quality prototype to hand off to engineers |
| ⚡ **Stitch AI** | Anyone who wants the fastest start | Fully free + fastest output + 7 framework exports. Lowest barrier. | Quick prototypes, concept validation, demos |
| 🚀 **Google AI Studio** | Vibe Coders who want a working site immediately | 5 style presets to pick + complete functional site + free + one-click Cloud Run deploy. | MVPs, internal tools, small deployable apps |
| ✨ **Claude Design** | Claude Pro users + interactive prototype needs | Asks scoping questions first + interactions actually work + 5 editing modes. Closed loop is most complete. | Interaction-heavy designs, handoff to Claude Code for production |

> Five tools, no "best" — just "best fit for you." The difference is whether you start from design, from code, or let AI think first.

### Live screenshots in deck
- **Slide 10**: Google AI Studio's design-preview picker (5 styles) — click to enlarge
- **Slide 12**: Claude Design's pre-build questions (scope, interactivity, realism) — click to enlarge

---

## 13. Hands-On Test — Claude Code Exercises All 3 Figma MCP Skills

**Live demo from this evaluation session.** Point Claude Code at a project folder, ask it to push the design *and* the team workflow *and* the system architecture into Figma. Three asks → three artifacts → three skills exercised.

### Input — 3 short asks
1. `read C:\...\disaster-dashboard, generate figma_design` — capture the live UI
2. `/figma-use-figjam — workflow for backend / frontend / data` — team work-assignment board
3. `/figma-generate-diagram — architecture` — future-state system diagram

### Figma MCP Tools Claude called (background, no `/` menu)
- `whoami` — fetch Figma plan key
- `create_new_file` — create blank Figma Design + FigJam files
- `generate_figma_design` — capture web page → editable Figma layers
- `use_figma` — Plugin API; build the workflow board (3 sections, 18 stickies)
- `generate_diagram` — Mermaid → architecture diagram (13 nodes, LR layout)
- `get_figjam` — verify the FigJam contents after construction

**Coverage of Apr 28 FigJam blog:** 5 of 6 named tools/skills exercised. The one not invoked — `/generate-project-plan` — was approximated manually via `use_figma` (the workflow-board construction).

### Figma MCP Skills loaded (via `/` slash menu)
- `/figma-use` — foundation skill for the `use_figma` plugin API
- `/figma-use-figjam` — FigJam-specific board patterns (sections, stickies, connectors)
- `/figma-generate-diagram` — Mermaid rules + architecture layout flag

> All three Figma skills mentioned in the Mar/Apr 2026 Figma blog posts are exercised in this single hands-on session.

### Results — 2 Figma files
| Type | Contents | URL |
|---|---|---|
| Figma Design | 4 frames captured from live dashboard (Dashboard, Events, Command, dark variant) | https://www.figma.com/design/EHogroXUZ2aq5yHfEcgE0w |
| FigJam | Workflow board (Backend / Frontend / Data, 6 stickies each) + system architecture diagram | https://www.figma.com/board/AykjSj3As1JTOmYh7ZqAkA |

### Key insight: Tool ≠ Skill
- **Tools** (`use_figma`, `generate_diagram`, `generate_figma_design`) — invoked by Claude in the background. Never appear in the `/` slash menu.
- **Skills** (`/figma-use`, `/figma-use-figjam`, `/figma-generate-diagram`) — markdown instruction files the user opens via `/`. They tell Claude *how* to use the tools properly.

This separation is why "search `/generate_figma_design`" returns nothing — it's a tool, not a skill.

---

## 14. Final Takeaway

| Tool | One-line Verdict |
|---|---|
| **Figma Make** | 美編首選。最完整的設計流程、協作和 plugin 生態。對 vibe coder 太重 |
| **Paper** | Code 品質首選。設計即程式碼，24 MCP tools。Alpha 階段，美編難獨立用 |
| **Stitch AI** | 最大公約數。兩種角色都能用，7 框架 export，免費且門檻最低 |
| **AI Studio** | App 生成器。Prompt 直接生成完整 app 並一鍵部署。完全免費 |
| **Claude Design** | 閉環最強。自動 design system，一鍵 handoff → Claude Code。零額外成本 |

### Best Combination

> **Claude Design / Stitch** *(generate)* → **Figma Make** *(refine)* → **Claude Code** *(ship)*

### Live Demos (Disaster Relief Dashboard)

| Tool | Link |
|---|---|
| Figma Make | https://www.figma.com/make/3p1G2MYQGBoIvHS8ZIwdDv/Disaster-Relief-Dashboard-Design?t=ZLtoBnV4ChImig7y-1 |
| Paper Design | https://app.paper.design/file/01KPMV40MNX7WF0B4VCVYYVR9T/1-0 |
| Stitch AI | https://stitch.withgoogle.com/projects/10574739860128708197 |
| AI Studio | https://ai.studio/apps/57bb988c-4d21-4ddd-ba8a-1be79dffa5a3 |
| Claude Design | https://claude.ai/design/p/decda9f3-7703-4882-a1bb-cf1b4430b3d4?file=dashboard.html&via=share |
