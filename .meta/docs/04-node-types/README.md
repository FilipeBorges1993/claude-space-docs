# Node Types Reference

AgentBuilder uses **7 node types** to build AI agent systems. Each node serves a specific purpose in your agent's architecture.

---

## The 7 Node Types

| Node | Purpose | Example Use | Documentation |
|------|---------|-------------|---------------|
| 🤖 **[Agent](agent-node.md)** | Main agent configuration | System prompt, model selection, permissions | Core intelligence |
| 🛠️ **[Skills](skills-node.md)** | Agent capabilities | File operations, API calls, code execution | Tools and actions |
| 🧠 **[Memory](memory-node.md)** | Persistent knowledge | Conversation history, knowledge bases, RAG | Long-term context |
| ⚙️ **[Commands](commands-node.md)** | Custom slash commands | `/summarize`, `/review-pr`, `/deploy` | User shortcuts |
| 🔌 **[MCPs](mcps-node.md)** | External tool integrations | Context7 docs, databases, APIs | System connections |
| 🪝 **[Hooks](hooks-node.md)** | Lifecycle event handlers | PreToolUse, PostToolUse, SessionStart | Event triggers |
| 🎭 **[Sub-agents](subagents-node.md)** | Delegated specialized agents | Code reviewer, researcher, writer | Agent delegation |

---

## Node Anatomy

Every node in AgentBuilder has these components:

### Visual Appearance

[Diagram: Node structure showing icon, title, description, color]

```
┌─────────────────────────┐
│  🛠️  File System         │  ← Icon + Title
│  Reads and writes files │  ← Description
│                         │
│  [Configuration Panel]  │  ← Expandable settings
└─────────────────────────┘
```

**Components:**
- **Icon** - Emoji or custom image for quick identification
- **Title** - Node name (editable)
- **Description** - Brief explanation of purpose
- **Color** - Category-based (Skills=red, Memory=green, etc.)
- **Handles** - Connection points (top/bottom/sides)

### Connection Handles

Handles are small circles on node edges for creating connections.

**Handle Types:**
- **Input Handle** (top) - Receives connections FROM main agent
- **Output Handle** (bottom) - Not used (reserved for future features)

**Color Coding:**
- 🛠️ Red → Skills connections
- 🧠 Green → Memory connections
- 🔌 Blue → MCP connections
- ⚙️ Purple → Command connections
- 🪝 Yellow → Hook connections
- 🎭 Purple → Sub-agent connections

[Screenshot: Main agent card with all handles highlighted]

### Configuration Panel

Clicking a node opens its **configuration panel** on the right side.

**Panel Contents:**
- Node-specific settings (name, description, etc.)
- Configuration options (parameters, paths, etc.)
- Connection status
- Validation errors (if any)
- Delete button

[Screenshot: Configuration panel for a skill node]

---

## Connection Rules

### Valid Connections

**Only the main agent card can connect to other nodes.**

```
✅ Valid:
Main Agent → Skills
Main Agent → Memory
Main Agent → MCPs
Main Agent → Commands
Main Agent → Hooks
Main Agent → Sub-agents

❌ Invalid:
Skills → Memory          # Nodes can't connect to each other
Skills → Skills          # No node-to-node connections
Memory → Sub-agents      # Only main agent as source
```

### Connection Handles on Main Agent Card

The main agent card has **specialized handles** for each node type:

```
         [🪝 Hooks]
      (top-left handle)
              ↑
              │
[🧠 Memory] ← MAIN → [🛠️ Skills]
(bottom-left) (center) (right handle)
              ↓
      [🎭 Sub-agents]
   (bottom handle)

[🔌 MCPs]
(top-right handle - separate area)

[⚙️ Commands]
(configured via panel, not visual connection)
```

**Handle Locations:**
- **Right edge** → Skills
- **Bottom-left** → Memory
- **Bottom center** → Sub-agents
- **Top-left** → Hooks
- **Top-right** → MCPs
- **Panel config** → Commands (no visual connection)

[Screenshot: Main agent card with labeled handles]

### Creating Connections

**Step-by-step:**

1. **Hover** over main agent card
2. **Handles appear** on edges (small circles)
3. **Click and drag** from appropriate handle
4. **Drop** on target node
5. **Connection line** appears

[GIF: Animation showing connection being created]

**Rules:**
- Each handle can have **only one connection**
- Must connect **from main agent** to other nodes
- Can't connect nodes directly to each other
- Delete existing connection before making new one on same handle

---

## Quick Reference: When to Use Each Node

### 🤖 Agent (Main Card)
**Always present** - Every project has exactly one main agent card.

**Use for:**
- Defining agent personality and behavior
- Setting system prompt
- Choosing AI model (Opus/Sonnet/Haiku)
- Configuring permissions
- Sandbox settings

**Required:** Yes (1 per project)

[Learn more →](agent-node.md)

---

### 🛠️ Skills
**Add capabilities** - Tools and actions your agent can perform.

**Use when:**
- Agent needs to read/write files → **File System** skill
- Agent needs to run Python code → **Code Interpreter** skill
- Agent needs to call APIs → **HTTP Request** skill or custom
- Agent needs specific tool → Create custom skill

**Examples:**
- File operations (read, write, delete)
- Code execution (Python, JavaScript)
- API integrations (GitHub, Slack, database)
- Data processing (CSV parser, JSON transformer)

**Required:** Optional (0 to many per project)

[Learn more →](skills-node.md)

---

### 🧠 Memory
**Persistent knowledge** - Long-term information your agent remembers.

**Use when:**
- Agent needs domain knowledge → Add **knowledge base** markdown files
- Agent needs conversation context → Use **prime context** pattern
- Agent needs reference docs → Store as **memory files**
- Agent needs to recall past interactions → Enable **conversation history**

**Examples:**
- Company information and policies
- Team member contacts and roles
- Product documentation
- Customer interaction history
- Technical specifications

**Required:** Optional (0 to many per project)

[Learn more →](memory-node.md)

---

### ⚙️ Commands
**User shortcuts** - Custom slash commands for quick actions.

**Use when:**
- Repetitive workflows → Create `/command-name`
- Structured inputs needed → Define parameters
- Quick access to complex prompts → Template with variables
- User-facing features → Expose as commands

**Examples:**
- `/summarize` - Summarize document
- `/review-pr <number>` - Review GitHub PR
- `/deploy <env>` - Deploy to environment
- `/test <file>` - Run tests on file

**Required:** Optional (0 to many per project)

[Learn more →](commands-node.md)

---

### 🔌 MCPs (Model Context Protocol)
**External integrations** - Connect to databases, APIs, and external tools.

**Use when:**
- Agent needs documentation → **Context7** MCP (library docs)
- Agent needs database access → **PostgreSQL/MySQL** MCP
- Agent needs file system → **File System** MCP
- Agent needs custom integration → Configure custom MCP server

**Examples:**
- Context7 (documentation lookup)
- Database connections (PostgreSQL, MongoDB)
- Cloud services (AWS, GCP, Azure)
- Custom APIs (internal tools)

**Required:** Optional (0 to many per project)

[Learn more →](mcps-node.md)

---

### 🪝 Hooks
**Lifecycle events** - Scripts that run at specific points in agent execution.

**Use when:**
- Need to log tool calls → **PreToolUse** hook
- Need to transform outputs → **PostToolUse** hook
- Need to initialize session → **SessionStart** hook
- Need to enforce policies → **PermissionRequest** hook
- Need to track costs → **PostToolUse** hook (parse metadata)

**Event Types:**
- `PreToolUse` - Before tool execution
- `PostToolUse` - After tool execution
- `UserPromptSubmit` - On user input
- `PermissionRequest` - On permission check
- `SessionStart` / `SessionEnd` - Session lifecycle
- `Stop` / `SubagentStop` - Cancellation
- `Notification` - Status messages
- `PreCompact` - Before conversation compaction

**Required:** Optional (0 to many per project)

[Learn more →](hooks-node.md)

---

### 🎭 Sub-agents
**Specialized agents** - Delegate tasks to expert agents with different configurations.

**Use when:**
- Task needs specialized expertise → **Code Reviewer** sub-agent
- Task needs different model → **Haiku** for speed, **Opus** for reasoning
- Task needs isolation → Separate permissions/tools
- Parallel processing → Multiple sub-agents working together

**Examples:**
- Code Reviewer (strict code analysis)
- Researcher (web search + summarization)
- Writer (creative content generation)
- Tester (test case generation)

**Patterns:**
- **Coordinator + Specialists** - Main agent delegates to experts
- **Pipeline** - Sequential processing (planner → writer → reviewer)
- **Parallel** - Multiple sub-agents working simultaneously

**Required:** Optional (0 to many per project)

[Learn more →](subagents-node.md)

---

## Node Library vs. Canvas Nodes

Understanding the difference between library components and canvas instances:

### Node Library (Workspace-Level)

**Location:** Settings → Node Managers

**Purpose:** Reusable components shared across all projects

**Management:**
- Create once, use everywhere
- Edit in one place, updates available to all projects
- Delete from library → can still exist in project canvases

**Contains:**
- Skills (custom tools)
- MCPs (integration configs)
- Hooks (event scripts)
- Commands (slash command templates)
- Sub-agents (agent templates)
- Memory templates

**Example:**
```
Workspace Library:
  └── "GitHub API" skill
      ├── SKILL.md
      └── scripts/github_api.py
```

---

### Canvas Nodes (Project-Level)

**Location:** Project canvas

**Purpose:** Specific instances used in individual projects

**Behavior:**
- **Copy** from library when added to canvas
- **Customizable** per project (can modify without affecting library)
- **Independent** - Changes don't affect library or other projects

**Example:**
```
Project 1 Canvas:
  └── "GitHub API" instance
      └── Endpoint: api.github.com/repos/owner/repo1

Project 2 Canvas:
  └── "GitHub API" instance
      └── Endpoint: api.github.com/repos/owner/repo2
```

**Workflow:**
1. **Create** skill in Node Library (Settings)
2. **Drag** to canvas from left sidebar
3. **Configure** specific parameters for this project
4. **Connect** to main agent card
5. **Test** agent with this skill instance

---

## Node Categories and Organization

### Sidebar Organization

Nodes in the left sidebar are organized by category:

```
Left Sidebar:
├── 🛠️ Skills (Red)
│   ├── File System
│   ├── Code Interpreter
│   ├── HTTP Request
│   └── [Custom skills from library]
├── 🧠 Memory (Green)
│   ├── Knowledge Base
│   ├── Prime Context
│   └── [Custom memory from library]
├── 🔌 MCPs (Blue)
│   ├── Context7
│   ├── File System
│   └── [Custom MCPs from library]
├── ⚙️ Commands (Purple)
│   └── [Custom commands from library]
├── 🪝 Hooks (Yellow)
│   └── [Custom hooks from library]
└── 🎭 Sub-agents (Purple)
    └── [Custom sub-agents from library]
```

**Search:** Type in sidebar search bar to filter nodes by name

**Favorites:** Star frequently-used nodes to pin to top

---

## Common Patterns

### Pattern 1: Basic Agent with File Access

```
[🤖 Main Agent]
      ↓
[🛠️ File System Skill]
```

**Use case:** Agent that reads/writes files (e.g., document analyzer)

---

### Pattern 2: Agent with Memory

```
    [🤖 Main Agent]
         ↓
    [🧠 Knowledge Base]
```

**Use case:** Agent with domain knowledge (e.g., customer support with company info)

---

### Pattern 3: Multi-Capability Agent

```
         [🤖 Main Agent]
         ↙   ↓   ↘
[🛠️ Skills] [🧠 Memory] [🔌 MCPs]
```

**Use case:** Full-featured agent with tools, knowledge, and integrations

---

### Pattern 4: Multi-Agent System

```
      [🤖 Coordinator Agent]
              ↓
      [🎭 Sub-agents]
       ↙    ↓    ↘
   [Code] [Research] [Writer]
   [Review]
```

**Use case:** Complex workflows with specialized agents

---

### Pattern 5: Hooked Agent with Logging

```
   [🪝 PreToolUse Hook]
            ↑
      [🤖 Main Agent]
            ↓
       [🛠️ Skills]
```

**Use case:** Agent with audit logging of all tool calls

---

## Next Steps

**Deep dive into specific node types:**

- [🤖 Agent Node](agent-node.md) - Configure main agent (system prompt, model, permissions)
- [🛠️ Skills Node](skills-node.md) - Add custom capabilities and tools
- [🧠 Memory Node](memory-node.md) - Persistent knowledge and context
- [⚙️ Commands Node](commands-node.md) - Create slash commands
- [🔌 MCPs Node](mcps-node.md) - External integrations
- [🪝 Hooks Node](hooks-node.md) - Lifecycle event handlers
- [🎭 Sub-agents Node](subagents-node.md) - Specialized agents

**Learn workflow fundamentals:**

- [Canvas Workflow](../05-canvas-workflow.md) - Master the visual editor
- [Testing Agents](../06-testing-agents.md) - Use the chat interface
- [Exporting Agents](../07-exporting-agents.md) - Deploy to production

---

<div align="center">

**Ready to configure your agent?**

[Start with Agent Node →](agent-node.md)

</div>
