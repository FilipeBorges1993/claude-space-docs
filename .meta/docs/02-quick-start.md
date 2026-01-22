# Quick Start: Your First Agent in 10 Minutes

Build a fully functional "Email Summarizer" agent step-by-step.

---

## What You'll Build

An AI agent that:
- Reads email content from files
- Summarizes key points in 3 bullet points
- Identifies sender intent (question, request, FYI)
- Suggests appropriate reply actions

**Time:** 10 minutes
**Skill Level:** Beginner
**Prerequisites:** [ClaudeSpace installed](01-getting-started.md)

---

## Step 1: Create a Project (1 min)

### Launch ClaudeSpace

```bash
npm run dev
```

ClaudeSpace opens to the main dashboard.

### Create New Project

1. Click **"+ New Project"** button (center of dashboard)
2. **Project name:** `email-summarizer`
3. Click **"Create"**

[Screenshot: New project dialog with "email-summarizer" in the name field]

**What happens:**
- New project folder created in your workspace
- Canvas opens with main agent card in center
- Right panel shows agent configuration

✅ **Checkpoint:** Canvas displays with purple main agent card labeled "New Agent"

---

## Step 2: Configure Main Agent (3 min)

The **main agent card** is your agent's brain. Let's configure it.

### Set Basic Information

1. Click the **main card** (purple gradient card in center)
2. Right panel opens with configuration options
3. Fill in:

**Name:**
```
Email Summarizer
```

**Description:**
```
Analyzes emails and suggests appropriate responses
```

**Icon:** Click icon → Select 📧 (or any emoji you prefer)

[Screenshot: Agent configuration panel showing name, description, and icon fields filled in]

### Write System Prompt

Scroll down to **System Prompt** section and enter:

```
You are an email assistant. When given email content, analyze it and provide:

1. **Summary:** 3 bullet points of key information
2. **Intent:** Classify as Question, Request, FYI, or Complaint
3. **Suggested Action:** Recommend appropriate response

## Guidelines
- Be concise and actionable
- Identify urgency level (High/Medium/Low)
- Extract any deadlines mentioned
- Note if CC'd recipients need responses

## Output Format
📧 **Email Summary:**
• [Key point 1]
• [Key point 2]
• [Key point 3]

**Sender Intent:** [Classification]
**Urgency:** [Level]
**Suggested Action:** [Specific recommendation]
```

[Screenshot: System prompt editor with the above text]

**Why this works:**
- Clear role definition ("You are an email assistant")
- Specific output structure (numbered list)
- Explicit format example
- Actionable guidelines

✅ **Checkpoint:** Main card now displays "Email Summarizer" as title

---

## Step 3: Add a Skill (2 min)

Skills give your agent capabilities. Let's add file reading so it can access emails.

### Find File System Skill

1. Look at **left sidebar** (Skills section)
2. Scroll to find **"File System"** skill (or use search)
3. Skill shows icon 📁 with "File System" label

[Screenshot: Left sidebar showing Skills category with File System skill highlighted]

### Add to Canvas

1. **Drag** the File System skill from sidebar
2. **Drop** onto canvas (anywhere to the right of main card)
3. Skill node appears on canvas

[Screenshot: Canvas showing main agent card and File System skill node side-by-side]

### Connect to Main Agent

1. **Hover** over main agent card
2. **Connection handles** appear on edges (small circles)
3. **Click and drag** from the **right handle** (right edge of main card)
4. **Drop** on File System skill node
5. Blue connection line appears

[Screenshot: Connection being drawn from main card to skill node]

**Connection rules:**
- Only main agent card can connect to other nodes
- Right handle → Skills
- Each handle can have only one connection

✅ **Checkpoint:** Blue line connects main agent card to File System skill

---

## Step 4: Configure Claude Settings (2 min)

Set the AI model and permissions for your agent.

### Open Claude Settings

1. Click **main agent card** (if not already selected)
2. Scroll down in right panel to **"Claude Settings"** section
3. Expand if collapsed

[Screenshot: Claude Settings panel expanded]

### Configure Model

**Model:** Select `claude-sonnet-4-5`

**Why?** Balanced performance and cost for email summarization.

| Model | Best For | Speed | Cost |
|-------|----------|-------|------|
| claude-opus-4-5 | Complex reasoning | Slow | High |
| **claude-sonnet-4-5** | **General tasks** | **Medium** | **Medium** |
| claude-haiku-4-0 | Simple tasks | Fast | Low |

### Set Parameters

**Temperature:** `0.3`
- Lower = more consistent and focused
- Higher = more creative
- Email summarization needs consistency

**Max Tokens:** `2048`
- Sufficient for detailed summaries
- Not excessive for simple task

[Screenshot: Model dropdown and temperature slider configured]

### Configure Permissions

Scroll to **Permissions** section:

**Allow** (green checks):
- ✅ `read` - Agent can read files
- ✅ `list_allowed_directories` - Agent can browse folders

**Ask** (yellow question marks):
- ⚠️ `write` - Agent must ask before writing

**Deny** (red X):
- ❌ `execute` - Agent cannot run commands
- ❌ `delete` - Agent cannot delete files

[Screenshot: Permissions panel with checkboxes configured as above]

**Why these permissions?**
- Email reading only needs `read` access
- Writing is rare (ask first for safety)
- Execution and deletion are unnecessary

✅ **Checkpoint:** Claude Settings show sonnet-4-5, temperature 0.3, read permissions allowed

---

## Step 5: Test Your Agent (2 min)

Time to see your agent in action!

### Create Test Email

First, create a sample email file:

```bash
# Create test file in your workspace
cat > test-email.txt << 'EOF'
From: sarah.chen@techcorp.com
Subject: Q4 Budget Planning Meeting - Urgent

Hi Team,

I need to schedule our Q4 budget planning meeting ASAP. We have a hard deadline of Friday, Jan 17th to submit our proposals to finance.

Can everyone confirm availability for:
- Thursday, Jan 16th at 2:00 PM (Conference Room A)
- Alternative: Friday, Jan 17th at 10:00 AM

Please include Sarah Kim (VP Finance) and David Park (Ops Director) in the meeting invite.

Let me know by EOD today.

Thanks,
Sarah
EOF
```

### Open Chat Interface

1. Click **Chat icon** (speech bubble) in top-right toolbar
2. Chat panel slides in from right side
3. Agent dropdown shows "Email Summarizer"

[Screenshot: Chat interface with agent selector and message input]

### Send Test Message

Type in chat input:

```
Please read and analyze the file at test-email.txt
```

Press **Enter** or click **Send**.

### Watch Agent Work

The agent will:
1. **Think** - Shows reasoning process
2. **Request approval** - Asks to read file (you granted `ask` permission)
3. **Click "Allow"** to approve
4. **Execute** - Reads file
5. **Respond** - Provides analysis

[Screenshot: Chat showing agent thinking process and approval request]

### Expected Response

```
📧 Email Summary:
• Q4 budget meeting needs scheduling before Jan 17th deadline
• Two time slots proposed: Thu Jan 16 2pm or Fri Jan 17 10am
• Must include Sarah Kim (VP Finance) and David Park (Ops) in invite

**Sender Intent:** Request (scheduling + confirmation)
**Urgency:** High (needs response EOD, hard deadline Jan 17)
**Suggested Action:** Reply with availability confirmation and send calendar invite to all 5 attendees (team + 2 stakeholders)
```

✅ **Checkpoint:** Agent successfully analyzes email and provides structured summary

---

## Step 6: Save & Export (1 min)

Save your work and export for production use.

### Save Project

ClaudeSpace **auto-saves** every 5 seconds, but you can manually save:

**Keyboard:** `Cmd+S` (macOS) or `Ctrl+S` (Windows/Linux)

**Or:** Click **Save** button in top toolbar

[Screenshot: Top toolbar with Save button highlighted]

### Export to Production

Generate a `.claude` folder structure for use with Claude Code CLI:

1. Click **Export** button (top toolbar, next to Save)
2. **Export dialog** opens
3. **Destination:** Choose folder (e.g., `~/claude-agents/email-summarizer`)
4. Click **Export**

[Screenshot: Export dialog with destination folder picker]

### Exported Files

ClaudeSpace generates:

```
email-summarizer/
├── .claude/
│   ├── CLAUDE.md              # System prompt
│   ├── settings.json          # Agent configuration
│   ├── settings.local.json    # Runtime settings (model, permissions)
│   └── skills/
│       └── file-system/       # File System skill
│           └── SKILL.md
```

**Use with Claude Code CLI:**
```bash
cd ~/claude-agents/email-summarizer
claude chat
```

✅ **Complete!** You've built and exported your first agent.

---

## What You Learned

**Core Concepts:**
- ✅ Creating projects in workspaces
- ✅ Configuring the main agent card (name, system prompt)
- ✅ Adding and connecting skills to agents
- ✅ Setting Claude model, temperature, and max tokens
- ✅ Configuring permissions (allow/ask/deny)
- ✅ Testing agents with integrated chat interface
- ✅ Exporting production-ready `.claude` folders

**Skills Acquired:**
- Writing effective system prompts
- Choosing appropriate AI models
- Managing agent permissions
- Testing and iterating on agents

---

## Try These Next

Now that you've built your first agent, try enhancing it:

### Add Memory

Give your agent context about previous emails:

1. Drag **Memory** node from left sidebar
2. Connect to main agent card (bottom-left handle)
3. Add markdown files with company context, team info, etc.

**Learn more:** [Memory Node Documentation](04-node-types/memory-node.md)

### Add a Command

Create a `/summarize` command for quick access:

1. Drag **Command** node from left sidebar
2. Configure command name and parameters
3. Use in chat: `/summarize path/to/email.txt`

**Learn more:** [Commands Node Documentation](04-node-types/commands-node.md)

### Add More Skills

Enhance with additional capabilities:
- **Web Search** - Research mentioned topics
- **Calendar** - Check scheduling availability
- **Email Sender** - Draft and send replies

**Learn more:** [Skills Node Documentation](04-node-types/skills-node.md)

---

## Common Issues

### Agent doesn't respond in chat

**Problem:** Chat hangs or shows errors

**Solutions:**
1. **Check Claude authentication:**
   - Settings → General → Claude Configuration
   - Verify API key or CLI auth is set up
2. **Check permissions:**
   - Agent needs `read` permission for file access
   - Look for permission denials in chat
3. **Restart agent session:**
   - Click "Stop Session" in chat
   - Send message again to start new session

---

### Skill won't connect to main agent

**Problem:** Can't draw connection line

**Solutions:**
1. **Check handle location:**
   - Skills connect via **right handle** (right edge of main card)
   - Hover over main card until handles appear
2. **Delete existing connection:**
   - Each handle allows only one connection
   - Click existing connection → Delete key
   - Try connecting again
3. **Ensure node is a skill:**
   - Only compatible node types can connect
   - Skills = red icon/label

---

### Export fails or generates empty folder

**Problem:** Export produces no files or errors

**Solutions:**
1. **Save project first:**
   - `Cmd+S` or `Ctrl+S` before exporting
   - Wait for "Saved" confirmation
2. **Check destination folder:**
   - Must have write permissions
   - Path should not contain special characters
3. **Verify project has content:**
   - At minimum: main agent card with system prompt
   - Check canvas is not empty

---

### Agent gives generic responses

**Problem:** Agent doesn't follow system prompt format

**Solutions:**
1. **Lower temperature:**
   - Try 0.2-0.4 for more consistent outputs
   - Higher temperature = more variation
2. **Add explicit examples in system prompt:**
   ```
   ## Example Output
   📧 Email Summary:
   • [Specific format you want]
   ```
3. **Use stronger instructions:**
   - "You MUST use this exact format"
   - "Always begin with 📧"
   - "Never deviate from the template"

---

## Next Steps

**Master the fundamentals:**
- [Workspace Basics](03-workspace-basics.md) - Organize multiple projects
- [Node Types Overview](04-node-types/README.md) - Learn all 7 node types
- [Canvas Workflow](05-canvas-workflow.md) - Advanced graph building

**Deep dive into node types:**
- [Agent Node](04-node-types/agent-node.md) - Complete configuration reference
- [Skills Node](04-node-types/skills-node.md) - Add custom capabilities
- [Memory Node](04-node-types/memory-node.md) - Persistent knowledge

**Advanced topics:**
- [Testing Agents](06-testing-agents.md) - Master the chat interface
- [Exporting to Production](07-exporting-agents.md) - Deployment guide
- [Multi-Agent Systems](09-advanced/multi-agent-systems.md) - Build agent teams

---

## Example Variations

Try building these similar agents to practice:

### Resume Screener
**Purpose:** Analyze resumes against job requirements

**System Prompt:**
```
You are a resume screener. When given a resume and job description:
1. Match skills and experience to requirements
2. Rate fit as Strong/Good/Fair/Poor
3. List strengths and gaps
4. Recommend next steps (interview/reject/request info)
```

**Skills needed:** File System (read resumes)

---

### Code Reviewer
**Purpose:** Review code for bugs and style issues

**System Prompt:**
```
You are a code reviewer. When given code:
1. Check for security vulnerabilities
2. Identify performance issues
3. Flag style violations
4. Suggest improvements with examples

Focus on: SQL injection, XSS, auth bypasses, N+1 queries
```

**Skills needed:** File System (read code files)

---

### Meeting Note Summarizer
**Purpose:** Distill meeting notes into action items

**System Prompt:**
```
You are a meeting assistant. When given notes:
1. Extract action items with owners and deadlines
2. List key decisions made
3. Identify follow-up topics
4. Generate attendee summary

Format as Markdown with sections.
```

**Skills needed:** File System (read notes)

---

<div align="center">

**Congratulations on building your first agent! 🎉**

[Explore Node Types →](04-node-types/README.md) | [Build Multi-Agent Systems →](09-advanced/multi-agent-systems.md)

</div>
