# Agent Node (Main Card)

The **main agent card** is the heart of your AI agent. It defines personality, behavior, model selection, and permissions.

---

## Overview

**Always present:** Every project has exactly 1 main agent card
**Location:** Center of canvas by default
**Color:** Gradient purple/blue
**Icon:** Customizable (emoji or custom image)
**Required:** Yes (cannot be deleted)

[Screenshot: Main agent card with labeled components]

**Purpose:**
- Define agent personality and behavior via system prompt
- Select AI model (Claude Opus/Sonnet/Haiku)
- Configure permissions and sandbox settings
- Set temperature, max tokens, and other parameters
- Connect to all other node types (skills, memory, MCPs, etc.)

---

## Configuration Sections

### 1. Basic Information

**Name**
- Agent's display name shown in chat interface
- Appears in dashboard project cards
- Used in exported `.claude` folder

**Examples:**
```
✅ Good: Email Summarizer, Code Reviewer, Research Assistant
❌ Generic: Agent, My Bot, Untitled
```

**Description**
- Brief summary of agent's purpose
- Internal documentation (not sent to Claude)
- Shows on dashboard cards

**Examples:**
```
✅ "Analyzes emails and suggests appropriate responses"
✅ "Reviews code for security issues and style violations"
✅ "Researches topics and generates comprehensive reports"
```

**Icon**
- Visual identifier for your agent
- Emoji or custom image (PNG, JPG)
- Click icon to change

**Popular choices:**
- 📧 Email handler
- 💻 Code reviewer
- 📊 Data analyzer
- 🔍 Researcher
- 💬 Chatbot

[Screenshot: Basic info panel with name, description, and icon fields]

---

### 2. System Prompt

The **system prompt** is the most important configuration. It defines your agent's:
- Role and personality
- Instructions and guidelines
- Output format
- Constraints and limitations

**Location:** Large text area in configuration panel

**Best Practices:**

#### ✅ Do:

**1. Start with clear role definition**
```
You are a [specific role]. Your purpose is to [clear objective].
```

**2. Use structured instructions**
```
When given [input], you should:
1. [First step]
2. [Second step]
3. [Third step]
```

**3. Define output format explicitly**
```
## Output Format
📧 **Email Summary:**
• [Key point 1]
• [Key point 2]

**Intent:** [Classification]
**Action:** [Recommendation]
```

**4. Set tone and personality**
```
Tone: Professional, friendly, concise
Style: Direct answers, minimal jargon
```

**5. Specify constraints**
```
Constraints:
- Keep responses under 500 words
- Always cite sources
- Ask for clarification if ambiguous
```

#### ❌ Don't:

**1. Vague instructions**
```
❌ You are helpful. Please assist the user.
```

**2. Conflicting directives**
```
❌ Be very detailed but also extremely concise.
```

**3. Overly long prompts**
```
❌ [5000+ character prompt with every possible scenario]
```

**4. Assume implicit knowledge**
```
❌ Follow our standard process.  # What process?
```

---

### Example System Prompts

#### Example 1: Email Summarizer

```markdown
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

## Tone
Professional, empathetic, solution-oriented
```

---

#### Example 2: Code Reviewer

```markdown
You are a senior code reviewer focusing on security, performance, and maintainability.

## Review Criteria

When analyzing code:

1. **Security:** Check for:
   - SQL injection vulnerabilities
   - Cross-site scripting (XSS)
   - Authentication bypasses
   - Exposed secrets or credentials

2. **Performance:** Look for:
   - N+1 query problems
   - Memory leaks
   - Inefficient algorithms
   - Missing database indexes

3. **Code Quality:** Evaluate:
   - Naming conventions
   - Code organization
   - Error handling
   - Test coverage

## Output Format

### 🔴 Critical Issues
[Line X] Description of security or breaking issue
**Fix:** Specific code suggestion

### 🟡 Improvements
[Line Y] Description of non-critical improvement
**Suggestion:** How to optimize

### ✅ Good Practices
Highlight well-written code with brief praise

## Tone
Constructive, educational, specific. Always explain WHY changes are recommended.
Focus on teaching, not criticizing.
```

---

#### Example 3: Customer Support Bot

```markdown
You are a customer support agent for TechCorp. Your goal is to resolve customer issues quickly and professionally.

## Interaction Flow

1. **Acknowledge** customer concern with empathy
2. **Clarify** ask questions if issue is unclear
3. **Solve** provide step-by-step resolution
4. **Confirm** check if issue is resolved
5. **Follow-up** offer additional assistance

## Knowledge Base

**Company Info:**
- Support hours: Mon-Fri 9am-6pm EST
- Phone: 1-800-TECHCORP
- Email: support@techcorp.com
- Return policy: 30 days for full refund

**Common Issues:**
- Password reset → Direct to /reset-password
- Billing questions → Escalate to finance team
- Technical bugs → Create support ticket

## Escalation Rules

Escalate to supervisor if:
- Customer requests manager
- Issue involves refund >$500
- Customer is angry or threatening
- Technical issue requires engineering

## Tone

Friendly, professional, empathetic. Use:
- "I understand your frustration..."
- "Let me help you with that..."
- "I'm sorry you're experiencing this issue..."

Avoid:
- Technical jargon
- Blame (customer or company)
- Making promises you can't keep
```

---

### 3. Claude Settings

Configure the Claude AI model and behavior parameters.

[Screenshot: Claude Settings panel expanded]

#### Model Selection

Choose the right Claude model for your use case:

| Model | Best For | Speed | Cost | Token Limit |
|-------|----------|-------|------|-------------|
| **claude-opus-4-5** | Complex reasoning, coding, analysis | Slow | High | 200K |
| **claude-sonnet-4-5** | General-purpose, balanced | Medium | Medium | 200K |
| **claude-haiku-4-0** | Simple tasks, speed-critical | Fast | Low | 200K |

**Selection guide:**

**Use Opus when:**
- Complex reasoning required (multi-step logic)
- Code generation and debugging
- Deep analysis and research
- Quality is more important than speed

**Use Sonnet when:**
- General-purpose tasks
- Balanced speed and quality
- Most common use cases
- Cost-effectiveness matters

**Use Haiku when:**
- Simple, well-defined tasks
- Speed is critical
- High-volume operations
- Cost minimization important

---

#### Temperature (0.0 - 1.0)

Controls response randomness and creativity.

```
0.0 ──────── 0.5 ──────── 1.0
Deterministic  Balanced  Creative

<-------- Less Random | More Random -------->
```

**Temperature guide:**

**0.0 - 0.3 (Focused)**
- Code review and analysis
- Data extraction
- Factual question answering
- Consistent formatting

**0.4 - 0.7 (Balanced)**
- General assistance
- Email drafting
- Document summarization
- Mixed creative/factual tasks

**0.8 - 1.0 (Creative)**
- Creative writing
- Brainstorming
- Idea generation
- Story telling

**Examples:**
```
Code Reviewer: 0.2  # Consistent, focused analysis
Email Writer: 0.5   # Balanced, natural language
Story Generator: 0.9 # Creative, varied outputs
```

---

#### Max Tokens

Maximum length of response in tokens (roughly 4 characters per token).

**Common values:**

| Tokens | Approx Words | Approx Pages | Use Case |
|--------|--------------|--------------|----------|
| 512 | ~380 | 0.5 | Short summaries |
| 1024 | ~760 | 1 | Standard responses |
| 2048 | ~1500 | 2 | Detailed analysis |
| 4096 | ~3000 | 4 | Long-form content |
| 8192 | ~6000 | 8 | Comprehensive reports |

**Selection guide:**
- **Short answers** (summaries, quick questions) → 512-1024
- **Standard responses** (email drafts, code reviews) → 1024-2048
- **Long content** (reports, documentation) → 4096-8192

**Note:** Higher limits increase cost but don't guarantee longer responses. Agent stops when task complete.

---

### 4. Permissions

Control what your agent can access and modify.

**Three permission levels:**

- **Allow** (🟢) - Agent can use without asking
- **Ask** (🟡) - Agent requests permission each time
- **Deny** (🔴) - Agent cannot use at all

[Screenshot: Permissions panel showing allow/ask/deny options]

#### File System Permissions

**read**
- Read file contents
- View file metadata
- Safe for most agents

**write**
- Create new files
- Modify existing files
- ⚠️ Use with caution

**delete**
- Remove files permanently
- ⚠️ Very dangerous - usually deny

**list_allowed_directories**
- Browse folder structure
- List files and directories
- Safe to allow

#### Execution Permissions

**bash**
- Run shell commands
- Execute scripts
- ⚠️ Powerful - recommend ask

**python** / **javascript** / etc.
- Execute code in specific language
- ⚠️ Can modify system - recommend ask

#### Network Permissions

**network**
- Make HTTP requests
- Access external APIs
- ⚠️ Can leak data - configure carefully

**api_access**
- Call external services
- Database connections
- ⚠️ Depends on API - review per case

#### Recommended Configurations

**Low-Risk Agent (Read-only)**
```
Allow:
✅ read
✅ list_allowed_directories

Ask:
⚠️ [none]

Deny:
❌ write
❌ delete
❌ bash
❌ network
```

**Medium-Risk Agent (Interactive)**
```
Allow:
✅ read
✅ list_allowed_directories

Ask:
⚠️ write
⚠️ bash

Deny:
❌ delete
❌ network (unless needed)
```

**High-Risk Agent (Full Access)**
```
Allow:
✅ read
✅ write
✅ list_allowed_directories
✅ bash

Ask:
⚠️ delete
⚠️ network

Deny:
❌ [none, or system-critical operations]
```

---

### 5. Permission Modes

Control how your agent handles permission requests during chat.

[Screenshot: Permission mode dropdown]

**Available Modes:**

**default** (Recommended for development)
- Agent asks for permission on each tool use
- User approves/denies in chat interface
- Safest option

**acceptEdits** (Quick editing)
- Auto-approve file modifications
- Still asks for dangerous operations (delete, execute)
- Good for iterative development

**bypassPermissions** (Advanced)
- Run all tools without asking
- ⚠️ Dangerous - only for trusted workflows
- Use in controlled environments only

**plan** (Planning mode)
- Agent shows plan before execution
- User reviews full workflow
- Proceeds after approval

**dontAsk** (Silent mode)
- No approval notifications
- Tools run based on permissions
- User not interrupted

**Recommendation:** Start with `default`, move to `acceptEdits` once workflow is tested.

---

### 6. Sandbox Mode

Isolate your agent from system-level access.

**Enabled (✅ Recommended for testing)**
- Agent runs in isolated environment
- Limited file system access
- No system-level commands
- Safe for experimentation

**Disabled (⚠️ Use with caution)**
- Full system access based on permissions
- Can execute any allowed command
- Required for some production use cases
- ⚠️ Review security implications

**Excluded Commands (cannot bypass sandbox):**
```bash
rm -rf        # Recursive deletion
sudo          # Elevated permissions
chmod         # Permission changes
systemctl     # System services
```

[Screenshot: Sandbox toggle with warning]

---

## Connections

The main agent card connects to all other node types via **specialized handles**.

### Handle Locations

```
       [🪝 Hooks]
      (top-left)
            ↑
            │
[🧠 Memory] ← MAIN → [🛠️ Skills]
(bottom-left) (center) (right)
            ↓
      [🎭 Sub-agents]
      (bottom)

[🔌 MCPs]
(top-right)
```

### Connection Examples

#### Connect a Skill

1. Hover over main card **right edge**
2. Drag from **right handle** (circle appears)
3. Drop on skill node
4. Red connection line appears

[GIF: Connecting skill to main agent]

**Use case:** Add File System skill for file operations

---

#### Connect Memory

1. Hover over main card **bottom-left area**
2. Drag from **bottom-left handle**
3. Drop on memory node
4. Green connection line appears

**Use case:** Add knowledge base with company information

---

#### Connect Sub-agent

1. Hover over main card **bottom center**
2. Drag from **bottom handle**
3. Drop on sub-agent node
4. Purple connection line appears

**Use case:** Delegate code review to specialist sub-agent

---

#### Connect Hook

1. Hover over main card **top-left**
2. Drag from **top-left handle**
3. Drop on hook node
4. Yellow connection line appears

**Use case:** Add logging hook for tool call audit trail

---

#### Connect MCP

1. Hover over main card **top-right**
2. Drag from **top-right handle**
3. Drop on MCP node
4. Blue connection line appears

**Use case:** Connect Context7 for documentation lookup

---

## Real-World Examples

### Example 1: Customer Support Agent

**Use Case:** Handle customer inquiries with empathy and accuracy

**Configuration:**

**Name:** Customer Support Bot
**Description:** Assists customers with product questions and issues
**Icon:** 💬

**System Prompt:**
```markdown
You are a customer support agent for TechCorp. Your goal is to resolve customer issues quickly and professionally.

[Full prompt from earlier example]
```

**Claude Settings:**
- **Model:** claude-sonnet-4-5 (balanced)
- **Temperature:** 0.5 (natural conversation)
- **Max Tokens:** 2048 (detailed responses)

**Permissions:**
```
Allow:
✅ read (knowledge base)
✅ list_allowed_directories

Ask:
⚠️ write (create support tickets)

Deny:
❌ bash
❌ delete
❌ network
```

**Permission Mode:** default (ask for approvals)
**Sandbox:** Enabled ✅

**Connected Nodes:**
- 🧠 Memory → Company KB (policies, FAQs)
- 🛠️ Skill → Ticket Creator
- 🔌 MCP → CRM Database (read-only)

---

### Example 2: Code Quality Guardian

**Use Case:** Review code for bugs, security, and style

**Configuration:**

**Name:** Code Quality Guardian
**Description:** Comprehensive code review for security and best practices
**Icon:** 🛡️

**System Prompt:**
```markdown
You are a senior code reviewer focusing on security, performance, and maintainability.

[Full prompt from earlier example]
```

**Claude Settings:**
- **Model:** claude-opus-4-5 (best reasoning)
- **Temperature:** 0.2 (consistent analysis)
- **Max Tokens:** 4096 (detailed reviews)

**Permissions:**
```
Allow:
✅ read (source code files)
✅ list_allowed_directories

Deny:
❌ write (read-only reviewer)
❌ execute
❌ delete
```

**Permission Mode:** acceptEdits (for testing)
**Sandbox:** Enabled ✅

**Connected Nodes:**
- 🛠️ Skill → File System (read code)
- 🧠 Memory → Style Guide
- 🪝 Hook → PreToolUse (log all file reads)
- 🎭 Sub-agent → Security Scanner (specialized)

---

### Example 3: Research Assistant

**Use Case:** Comprehensive research with citation

**Configuration:**

**Name:** Research Assistant Pro
**Description:** Researches topics and generates cited reports
**Icon:** 🔍

**System Prompt:**
```markdown
You are a research assistant. When given a topic, you:

1. **Research:** Search multiple sources
2. **Synthesize:** Combine information into coherent narrative
3. **Cite:** Always include source links
4. **Organize:** Use clear sections and headings

## Output Format

# Topic: [Research Topic]

## Executive Summary
[2-3 paragraph overview]

## Detailed Findings

### [Subtopic 1]
[Content with citations[1]]

### [Subtopic 2]
[Content with citations[2]]

## Conclusions
[Key takeaways]

## Sources
[1] [Full citation with URL]
[2] [Full citation with URL]

## Tone
Objective, academic, well-sourced. Avoid speculation without noting it as such.
```

**Claude Settings:**
- **Model:** claude-sonnet-4-5 (balanced)
- **Temperature:** 0.4 (mostly factual, some synthesis)
- **Max Tokens:** 8192 (long reports)

**Permissions:**
```
Allow:
✅ read
✅ network (web search)
✅ list_allowed_directories

Ask:
⚠️ write (save reports)

Deny:
❌ bash
❌ delete
```

**Permission Mode:** acceptEdits (allow writing reports)
**Sandbox:** Disabled ⚠️ (needs network access)

**Connected Nodes:**
- 🛠️ Skill → Web Search
- 🛠️ Skill → File System
- 🧠 Memory → Research Guidelines
- 🔌 MCP → Context7 (documentation lookup)

---

## Best Practices

### System Prompt Design

**✅ Do:**
```
1. Define clear role and objectives
2. Use hierarchical structure (headings, lists)
3. Provide explicit output format examples
4. Set constraints and guidelines
5. Include error handling instructions
6. Specify tone and personality
```

**❌ Don't:**
```
1. Write overly long prompts (>3000 chars)
2. Use contradictory instructions
3. Assume implicit knowledge
4. Be vague about expectations
5. Skip output format specification
```

---

### Model Selection Strategy

```
Task Complexity:
Simple → Haiku
Medium → Sonnet
Complex → Opus

Speed Priority:
Critical → Haiku
Balanced → Sonnet
Quality → Opus

Cost Priority:
Budget → Haiku
Standard → Sonnet
Premium → Opus
```

---

### Permission Strategy

**Development Phase:**
```
Sandbox: ON
Permission Mode: default (ask everything)
Permissions: Minimal (read-only)
```

**Testing Phase:**
```
Sandbox: ON
Permission Mode: acceptEdits (faster iteration)
Permissions: Moderate (read + ask write)
```

**Production Phase:**
```
Sandbox: OFF (if needed)
Permission Mode: Based on use case
Permissions: Principle of least privilege
```

---

## Troubleshooting

### Agent doesn't respond or gives errors

**Problem:** Chat hangs or shows "Agent failed to respond"

**Solutions:**
1. Check Claude authentication (Settings → Claude Configuration)
2. Verify model selection is valid
3. Check permissions allow needed operations
4. Review system prompt for conflicts
5. Reduce temperature if outputs are erratic

---

### Agent ignores system prompt

**Problem:** Agent doesn't follow instructions or format

**Solutions:**
1. **Lower temperature** (try 0.2-0.4)
2. **Add explicit examples** in system prompt
3. **Use stronger directives** ("You MUST...", "Always...", "Never...")
4. **Simplify instructions** (break into smaller steps)
5. **Test with different model** (Opus more instruction-following)

---

### Permission errors in chat

**Problem:** "Permission denied" or tool calls fail

**Solutions:**
1. Check permissions in agent config match needed operations
2. Change permission mode to `default` to see approval requests
3. Verify sandbox mode isn't blocking needed operations
4. Review file/directory paths are within allowed directories

---

### Responses too long or too short

**Problem:** Agent output length doesn't match needs

**Solutions:**

**Too long:**
- Reduce max tokens
- Add length constraint to system prompt ("Keep under 200 words")
- Lower temperature (more focused)

**Too short:**
- Increase max tokens
- Request more detail in system prompt ("Provide comprehensive analysis")
- Raise temperature slightly (more expansive)

---

## Next Steps

**Learn about other node types:**
- [Skills Node](skills-node.md) - Add capabilities to your agent
- [Memory Node](memory-node.md) - Give your agent persistent knowledge
- [Sub-agents Node](subagents-node.md) - Delegate to specialist agents

**Master the workflow:**
- [Canvas Workflow](../05-canvas-workflow.md) - Build complex agent graphs
- [Testing Agents](../06-testing-agents.md) - Use chat interface effectively
- [Exporting Agents](../07-exporting-agents.md) - Deploy to production

---

<div align="center">

**Ready to add capabilities to your agent?**

[Add Skills →](skills-node.md) | [Add Memory →](memory-node.md) | [Add Sub-agents →](subagents-node.md)

</div>
