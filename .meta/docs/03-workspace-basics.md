# Workspace Basics

Learn how AgentBuilder organizes your agents, projects, and workspaces.

---

## Workspace Hierarchy

AgentBuilder uses a three-level organization system:

```
📁 My-Agents-Workspace/          ← Workspace (root folder)
├── 📁 email-summarizer/          ← Project folder
│   ├── workflow.json             ← Visual graph data
│   ├── agent.json                ← Agent metadata
│   ├── .claude/                  ← Claude Code config
│   │   ├── CLAUDE.md             ← System prompt
│   │   ├── settings.json         ← Agent definitions
│   │   ├── settings.local.json   ← Runtime settings
│   │   ├── skills/               ← Skill implementations
│   │   └── memory/               ← Memory files
│   └── context/                  ← Context files
├── 📁 code-reviewer/             ← Another project
│   └── ...
└── 📁 research-assistant/        ← Another project
    └── ...
```

---

## Core Concepts

### Workspace

A **workspace** is a folder containing multiple related projects.

**Purpose:**
- Organize agents by category or use case
- Share reusable components (skills, MCPs, hooks)
- Manage multiple projects from one location

**Example Workspaces:**
```
~/Documents/AgentBuilder-Workspaces/
├── work-agents/           ← Workspace 1: Work-related agents
│   ├── email-handler/
│   ├── meeting-scheduler/
│   └── doc-generator/
├── personal-projects/     ← Workspace 2: Personal agents
│   ├── recipe-assistant/
│   └── fitness-tracker/
└── experiments/           ← Workspace 3: Testing new ideas
    └── prototype-agent/
```

**Storage:**
- Workspace path stored in AgentBuilder settings
- Recent workspaces list for quick switching
- Workspace metadata (icon, title, description)

---

### Project

A **project** is a single agent system with its visual workflow and configuration.

**Contains:**
- **Visual workflow** - Node graph (canvas state)
- **Agent configuration** - System prompt, settings, permissions
- **Skills** - Custom capabilities and tools
- **Memory** - Knowledge base files
- **Commands** - Slash command definitions
- **Hooks** - Lifecycle event handlers
- **Sub-agents** - Specialized delegated agents
- **Context files** - Documents and references

**Lifecycle:**
1. **Created** - New project initialized with main agent card
2. **Developed** - Nodes added, configured, connected
3. **Tested** - Agent run via chat interface
4. **Exported** - `.claude` folder generated for production
5. **Deployed** - Used with Claude Code CLI

**Metadata stored in `agent.json`:**
```json
{
  "name": "Email Summarizer",
  "created": "2025-01-10T10:30:00Z",
  "modified": "2025-01-10T15:45:00Z",
  "iconImage": "icons/email.png",
  "description": "Analyzes emails and suggests responses"
}
```

---

### Node Library

The **Node Library** contains reusable components shared across all projects in a workspace.

**Location:** `<workspace>/.library/`

**Contains:**
- **Skills** - Custom tools and capabilities
- **MCP Servers** - External tool integrations
- **Hooks** - Lifecycle event scripts
- **Commands** - Reusable slash commands
- **Sub-agents** - Shared agent templates
- **Memory Templates** - Knowledge base structures

**How it works:**
1. Create components in **Settings → Node Managers**
2. Components saved to workspace library
3. **Drag from sidebar** to add to any project
4. Each project gets its own **instance** (can customize)
5. Edit library item → **all projects can use updated version**

**Example:**
```
Workspace Library:
  ├── "GitHub API" skill (shared)

Project 1 Canvas:
  └── "GitHub API" skill instance (endpoint: api.github.com/repos)

Project 2 Canvas:
  └── "GitHub API" skill instance (endpoint: api.github.com/users)
```

---

## Creating and Managing Workspaces

### Create Your First Workspace

**At first launch:**

1. AgentBuilder opens with **"Select Workspace Folder"** dialog
2. Click **"Choose Folder"**
3. Navigate to desired location:
   ```
   ~/Documents/AgentBuilder-Workspace     # macOS/Linux
   C:\Users\YourName\AgentBuilder         # Windows
   ```
4. Create new folder or select existing empty folder
5. Click **"Select"**

[Screenshot: Workspace selection dialog]

**What happens:**
- AgentBuilder initializes workspace
- Creates `.library/` folder for shared components
- Opens main dashboard (empty project list)

✅ **Checkpoint:** Dashboard shows "No projects yet" with "+ New Project" button

---

### Switching Workspaces

**To work with a different workspace:**

1. Click **workspace dropdown** (top-left corner)
2. Shows current workspace name and icon
3. Select **"Switch Workspace"** from menu
4. Choose different folder
5. AgentBuilder loads new workspace

[Screenshot: Workspace dropdown menu with "Switch Workspace" option]

**Recent Workspaces:**
- AgentBuilder remembers last 5 workspaces
- Quick access from dropdown menu
- Click name to instantly switch

---

### Customizing Workspaces

**Access:** Settings (⚙️) → General Tab → Workspace Customization

**Customize:**
- **Icon** - Emoji or image for visual identification
- **Title** - Display name (different from folder name)
- **Description** - Purpose or category notes

[Screenshot: Workspace customization panel]

**Example:**
```
Folder name: ~/work-agents
Icon: 💼
Title: "Work Projects"
Description: "Production agents for company workflows"
```

---

## Managing Projects

### Create New Project

**From dashboard:**

1. Click **"+ New Project"** button
2. Enter project name: `my-agent`
3. Click **"Create"**

**What gets created:**
```
<workspace>/my-agent/
├── workflow.json       # Empty canvas with main card
├── agent.json          # Metadata (timestamps, icon)
└── .claude/            # Empty config folders
    ├── skills/
    ├── memory/
    ├── commands/
    └── hooks/
```

[Screenshot: New project dialog]

**Naming guidelines:**
```
✅ Descriptive: email-summarizer, github-pr-reviewer
✅ Lowercase with hyphens: my-agent-name
✅ No special chars: avoid spaces, quotes, slashes

❌ Generic: agent1, test, new-agent
❌ Special chars: my agent!, reviewer/v2
```

---

### Open Existing Project

**From dashboard:**

1. **Project cards** display all workspace projects
2. Each card shows:
   - Project name
   - Icon
   - Description (if set)
   - Last modified date
3. **Click card** to open in canvas

[Screenshot: Dashboard with multiple project cards]

**Alternative access:**
- **Recent Projects** - Top of dashboard (last 3 opened)
- **Search** - Filter projects by name

---

### Delete Project

**⚠️ Warning:** Deletion is permanent and cannot be undone.

**Steps:**

1. **Right-click project card** on dashboard
2. Select **"Delete Project"** from context menu
3. **Confirmation dialog** appears
4. Type project name to confirm
5. Click **"Delete Permanently"**

[Screenshot: Delete confirmation dialog]

**What gets deleted:**
- All project files (`workflow.json`, `agent.json`)
- `.claude/` configuration folder
- Skills, memory, commands, hooks
- Cannot be recovered

**Best practice:** **Export project** before deleting to keep backup.

---

### Duplicate Project

**Create a copy of existing project:**

1. **Right-click project card**
2. Select **"Duplicate Project"**
3. Enter new name: `my-agent-copy`
4. Click **"Duplicate"**

**What gets copied:**
- Complete visual workflow (all nodes and connections)
- Agent configuration (system prompt, settings)
- Skills, memory files, commands, hooks
- Context files

**Use cases:**
- Test variations without affecting original
- Create similar agents with modifications
- Backup before major changes

---

## File Structure Deep Dive

### Project Files

**`workflow.json` - Visual Graph Data**

Stores the canvas state (nodes, connections, positions):

```json
{
  "version": "1.0",
  "name": "Email Summarizer",
  "visual": {
    "nodes": [
      {
        "id": "main-card",
        "type": "agent",
        "position": { "x": 400, "y": 300 },
        "data": { "name": "Email Summarizer", ... }
      },
      {
        "id": "skill-1",
        "type": "skill",
        "position": { "x": 700, "y": 300 },
        "data": { "name": "File System", ... }
      }
    ],
    "edges": [
      {
        "id": "edge-1",
        "source": "main-card",
        "target": "skill-1",
        "sourceHandle": "skills"
      }
    ]
  }
}
```

**Purpose:** Reconstructs canvas when project opens

---

**`agent.json` - Project Metadata**

```json
{
  "name": "Email Summarizer",
  "description": "Analyzes emails and suggests responses",
  "created": "2025-01-10T10:30:00Z",
  "modified": "2025-01-10T15:45:00Z",
  "iconImage": "data:image/png;base64,..."
}
```

**Purpose:** Dashboard display, search, sorting

---

**`.claude/` Folder Structure**

Generated when you export or test agent:

```
.claude/
├── CLAUDE.md                 # System prompt (main agent)
├── settings.json             # Agent definitions
├── settings.local.json       # Runtime config
├── .mcp.json                 # MCP servers (at project root)
├── agents/                   # Sub-agent definitions
│   ├── code-reviewer.md
│   └── researcher.md
├── skills/                   # Skill implementations
│   ├── file-system/
│   │   ├── SKILL.md
│   │   └── scripts/
│   └── github-api/
│       ├── SKILL.md
│       └── references/
├── memory/                   # Knowledge base files
│   ├── company-info.md
│   └── team-contacts.md
├── commands/                 # Slash command definitions
│   ├── summarize.md
│   └── review.md
└── hooks/                    # Lifecycle event scripts
    ├── pre-tool-use.sh
    └── post-tool-use.sh
```

**Purpose:** Claude Code CLI compatibility, version control

---

### Workspace Files

**`.library/` - Shared Components**

```
<workspace>/.library/
├── skills/
│   ├── custom-api-v1/
│   ├── data-processor/
│   └── email-sender/
├── mcps/
│   ├── postgres-db.json
│   └── redis-cache.json
├── hooks/
│   ├── logging.sh
│   └── rate-limiter.sh
├── commands/
│   ├── deploy.md
│   └── test.md
└── memory/
    └── templates/
```

**Purpose:** Reusable across all projects in workspace

---

## Best Practices

### Workspace Organization

**✅ Do:**
```
Group by purpose:
  ~/work-agents/           # Company projects
  ~/personal-agents/       # Personal use
  ~/experiments/           # Prototypes

Use descriptive names:
  customer-support-bot     # Clear purpose
  github-pr-reviewer       # Specific use case

Regular exports:
  Weekly backup to .claude folders
  Version control with git
```

**❌ Don't:**
```
Mix unrelated agents:
  ~/all-agents/            # Too broad

Use generic names:
  agent1, test, new        # Not descriptive

Forget to backup:
  No exports = no recovery
```

---

### Project Naming

**✅ Good Names:**
```
email-summarizer         # Descriptive action
code-quality-checker     # Clear purpose
meeting-scheduler        # Specific task
customer-support-v2      # Version indicated
```

**❌ Bad Names:**
```
agent                    # Too generic
my_project               # Underscores, not hyphens
test123                  # Temporary name kept
New Agent (1)            # Spaces and parens
```

---

### Library Management

**✅ Do:**
```
Create reusable skills:
  - Generic "HTTP Request" vs project-specific
  - Parameterized for flexibility

Share MCPs across projects:
  - Database connections
  - API integrations

Document library items:
  - Add descriptions in Settings
  - Include usage examples
```

**❌ Don't:**
```
Duplicate similar skills:
  - github-api-v1, github-api-v2, github-api-final
  - Instead: Update single library item

Accumulate unused items:
  - Delete deprecated skills
  - Clean library regularly
```

---

### File Management

**Version Control:**

```bash
# Initialize git in workspace
cd ~/my-workspace
git init

# Add .gitignore
cat > .gitignore << 'EOF'
node_modules/
dist/
*.log
.DS_Store
EOF

# Commit projects
git add .
git commit -m "Initial agent projects"

# Push to remote
git remote add origin <repo-url>
git push -u origin main
```

**Backup Strategy:**

```bash
# Export all projects weekly
# Create backup script

#!/bin/bash
WORKSPACE=~/my-workspace
BACKUP=~/backups/agents-$(date +%Y%m%d)

mkdir -p "$BACKUP"
cp -r "$WORKSPACE" "$BACKUP/"
tar -czf "$BACKUP.tar.gz" "$BACKUP"
echo "Backup complete: $BACKUP.tar.gz"
```

---

## Importing Existing Projects

**Import `.claude` folder from another source:**

1. **Copy `.claude` folder** to workspace:
   ```bash
   cp -r ~/existing-agent/.claude ~/my-workspace/imported-agent/
   ```

2. **Create minimal project files:**
   ```bash
   cd ~/my-workspace/imported-agent

   # Create agent.json
   cat > agent.json << 'EOF'
   {
     "name": "Imported Agent",
     "created": "2025-01-10T00:00:00Z",
     "modified": "2025-01-10T00:00:00Z"
   }
   EOF

   # Create workflow.json
   cat > workflow.json << 'EOF'
   {
     "version": "1.0",
     "name": "Imported Agent",
     "visual": { "nodes": [], "edges": [] }
   }
   EOF
   ```

3. **Open AgentBuilder** → Project appears on dashboard

4. **Open project** → Manually recreate visual workflow (nodes + connections)

**Why manual recreation?**
- Visual graph not stored in `.claude` folder
- AgentBuilder needs to build canvas representation
- Settings auto-detected from `.claude` files

---

## Workspace Settings

**Access:** Settings (⚙️) → General Tab

### Workspace Selection

- **Current Workspace:** Shows active workspace path
- **Switch Workspace:** Change to different folder
- **Recent Workspaces:** Quick access to last 5

### Workspace Customization

- **Icon:** Emoji or custom image
- **Title:** Display name (overrides folder name)
- **Description:** Notes about workspace purpose

### Storage Location

AgentBuilder stores workspace preferences in:
- **macOS/Linux:** `~/.config/agentbuilder/workspaces.json`
- **Windows:** `%APPDATA%\agentbuilder\workspaces.json`

```json
{
  "current": "/Users/name/my-workspace",
  "recent": [
    { "path": "/Users/name/work-agents", "icon": "💼", "title": "Work" },
    { "path": "/Users/name/personal", "icon": "🏠", "title": "Personal" }
  ]
}
```

---

## Troubleshooting

### Workspace won't load

**Symptoms:**
- Empty dashboard despite projects existing
- "Failed to load workspace" error

**Solutions:**

1. **Check folder permissions:**
   ```bash
   ls -la ~/my-workspace
   # Should have read/write access
   ```

2. **Verify folder structure:**
   ```bash
   # Workspace should contain project folders
   ~/my-workspace/
   ├── project-1/
   └── project-2/
   ```

3. **Reset workspace cache:**
   ```bash
   # macOS/Linux
   rm -rf ~/.config/agentbuilder/cache

   # Windows
   del %APPDATA%\agentbuilder\cache
   ```

4. **Re-select workspace:**
   - Settings → Switch Workspace
   - Choose same folder again

---

### Projects not appearing on dashboard

**Symptoms:**
- Project folders exist but don't show in dashboard

**Solutions:**

1. **Check for required files:**
   ```bash
   # Each project needs these files
   cd ~/my-workspace/my-project
   ls -la
   # Should see: workflow.json, agent.json
   ```

2. **Create missing files:**
   ```bash
   # If files missing, create minimal versions
   echo '{"version":"1.0","visual":{"nodes":[],"edges":[]}}' > workflow.json
   echo '{"name":"My Project"}' > agent.json
   ```

3. **Refresh dashboard:**
   - Press `Cmd+R` (macOS) or `Ctrl+R` (Windows/Linux)

---

### Can't delete project

**Symptoms:**
- Delete confirmation fails
- "Permission denied" error

**Solutions:**

1. **Close project if open:**
   - Switch to dashboard first
   - Then attempt delete

2. **Check file permissions:**
   ```bash
   chmod -R u+w ~/my-workspace/my-project
   ```

3. **Manual deletion:**
   ```bash
   rm -rf ~/my-workspace/my-project
   # Refresh dashboard in AgentBuilder
   ```

---

## Next Steps

**Continue learning:**
- [Node Types Overview](04-node-types/README.md) - Learn all 7 node types
- [Canvas Workflow](05-canvas-workflow.md) - Build visual graphs
- [Node Library](08-node-library.md) - Create reusable components

**Build more agents:**
- [Quick Start Tutorial](02-quick-start.md) - Build another agent
- [Testing Agents](06-testing-agents.md) - Master chat interface
- [Exporting to Production](07-exporting-agents.md) - Deploy agents

---

<div align="center">

**Ready to build complex agent systems?**

[Explore Node Types →](04-node-types/README.md)

</div>
