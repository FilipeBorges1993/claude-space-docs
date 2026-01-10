# AgentBuilder Documentation

Visual IDE for building Claude AI agents with drag-and-drop simplicity.

**Think Blender for agent workflows** — visual node graph, real-time testing, export to production config.

---

## Quick Navigation

### Getting Started (⏱️ 15 minutes)

New to AgentBuilder? Start here to get up and running quickly.

| Guide | Time | Description |
|-------|------|-------------|
| [Installation & Setup](01-getting-started.md) | 5 min | Get AgentBuilder running on your machine |
| [Your First Agent](02-quick-start.md) | 10 min | Build a working "Email Summarizer" agent step-by-step |
| [Workspace Basics](03-workspace-basics.md) | 5 min | Understand projects, folders, and organization |

---

### Core Concepts

Master the fundamentals of building AI agents visually.

#### Node Types Reference

Learn about the 7 node types that make up your agent systems:

| Node Type | Purpose | Documentation |
|-----------|---------|---------------|
| [🤖 Agent](04-node-types/agent-node.md) | Main agent configuration | System prompt, model, permissions |
| [🛠️ Skills](04-node-types/skills-node.md) | Agent capabilities | File operations, API calls, code execution |
| [🧠 Memory](04-node-types/memory-node.md) | Persistent knowledge | Conversation history, knowledge bases |
| [⚙️ Commands](04-node-types/commands-node.md) | Custom slash commands | `/summarize`, `/review-pr` |
| [🔌 MCPs](04-node-types/mcps-node.md) | External tool integrations | Context7 docs, databases, APIs |
| [🪝 Hooks](04-node-types/hooks-node.md) | Lifecycle event handlers | PreToolUse, PostToolUse, SessionStart |
| [🎭 Sub-agents](04-node-types/subagents-node.md) | Delegated specialized agents | Code reviewer, researcher |

**Start here:** [Node Types Overview](04-node-types/README.md)

#### Workflow Guides

- [Canvas Workflow](05-canvas-workflow.md) - Building visual agent graphs
- [Testing Agents](06-testing-agents.md) - Real-time chat testing interface
- [Exporting to Production](07-exporting-agents.md) - Generate `.claude` folders
- [Node Library](08-node-library.md) - Creating reusable components

---

### What You Can Build

AgentBuilder enables you to create sophisticated AI agent systems:

**Single-Purpose Agents**
- Email handler and summarizer
- Code reviewer with custom rules
- Document analyzer and reporter
- Customer support bot

**Multi-Agent Systems**
- Research coordinator with specialist sub-agents
- Code generation pipeline (planner → writer → reviewer)
- Customer service orchestrator (routing → specialist → escalation)

**Complex Workflows**
- Agents with custom lifecycle hooks
- Memory-enabled conversational agents
- Tool-augmented agents with MCP integrations
- Command-driven automation bots

---

## Architecture Overview

```
┌─────────────────────────────────────────┐
│         Electron Desktop App            │
├─────────────────────────────────────────┤
│  Vue 3 + TypeScript + Vite              │
│  ┌────────────┐  ┌──────────────────┐   │
│  │ Node Graph │  │  Chat Interface  │   │
│  │ (Vue Flow) │  │  (Agent Testing) │   │
│  └────────────┘  └──────────────────┘   │
├─────────────────────────────────────────┤
│  Pinia State Management                 │
├─────────────────────────────────────────┤
│  Claude Agent SDK Integration           │
└─────────────────────────────────────────┘
```

**Tech Stack:**
- Electron 28 - Desktop application framework
- Vue 3 - Modern UI framework with TypeScript
- Vue Flow - Node graph canvas
- Pinia - State management
- Claude Agent SDK - AI agent execution

---

## Why AgentBuilder?

### The Problem

Manually editing `.claude` configuration folders is error-prone and difficult to visualize:
- Hard to understand agent architecture at a glance
- Easy to misconfigure permissions and tool access
- Difficult to manage complex multi-agent systems
- No way to test changes in real-time

### The Solution

AgentBuilder provides a visual interface for building Claude AI agents:

**Visual Node Graph**
- Drag-and-drop canvas for building agent workflows
- Clear visualization of agent architecture
- Real-time validation and error checking

**Integrated Testing**
- Chat interface built right into the IDE
- Test agents as you build them
- See agent thinking process and tool calls

**Production-Ready Export**
- One-click export to `.claude` folder structure
- Generates all configuration files automatically
- Compatible with Claude Code CLI

**Full Ecosystem Management**
- Skills, Commands, MCPs, Sub-agents, Hooks
- All managed through intuitive GUI
- Reusable component library

---

## Quick Links

**New to AgentBuilder?**
→ Start with [Your First Agent](02-quick-start.md) (10 minutes)

**Need to install?**
→ See [Installation & Setup](01-getting-started.md) (5 minutes)

**Building complex agents?**
→ Explore [Node Types Reference](04-node-types/README.md)

**Ready to deploy?**
→ Learn about [Exporting to Production](07-exporting-agents.md)

---

## System Requirements

- **Node.js:** ≥18.19.9
- **Platform:** macOS, Windows, or Linux
- **RAM:** 4GB minimum, 8GB recommended
- **Disk Space:** 500MB for app + workspace storage

---

## Community & Support

**Found a bug?**
[Report an issue](https://github.com/FilipeBorges1993/ClaudeSpaceElectron/issues)

**Have questions?**
[Join our Discord](https://discord.gg/2tr2S7yw)

**Want to contribute?**
See our [GitHub repository](https://github.com/FilipeBorges1993/ClaudeSpaceElectron)

---

## License

MIT License - See [LICENSE](../../LICENSE)

---

<div align="center">

**AgentBuilder** - Making AI agent development visual, one node at a time.

```
⚡ Electron + Vue + Claude SDK = 🚀
```

</div>
