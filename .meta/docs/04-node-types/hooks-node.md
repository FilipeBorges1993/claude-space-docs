# Hooks Node

**Hooks** run scripts at specific points in your agent's lifecycle.

---

## Overview

**Purpose:** Execute scripts on lifecycle events (before/after tool use, session start, etc.)
**Connection:** Top-left handle of main agent card
**Color:** Yellow
**Icon:** 🪝
**Required:** Optional (0 to many)

---

## What are Hooks?

Hooks are scripts (shell, Python, Node.js) that run automatically when events occur:
- Before tool execution (logging, validation)
- After tool execution (notifications, cleanup)
- On session start (initialization)
- On user input (filtering, preprocessing)

---

## Hook Types

### 10 Event Types

| Event | When It Runs | Use Case |
|-------|--------------|----------|
| **PreToolUse** | Before tool execution | Logging, validation, rate limiting |
| **PostToolUse** | After tool execution | Notifications, cleanup, metrics |
| **UserPromptSubmit** | On user input | Filter profanity, preprocess |
| **PermissionRequest** | On permission check | Custom approval logic |
| **SessionStart** | Agent session begins | Initialize connections, load context |
| **SessionEnd** | Agent session ends | Cleanup resources, save state |
| **Stop** | Agent stopped by user | Cancel operations, rollback |
| **SubagentStop** | Sub-agent stopped | Sub-agent cleanup |
| **Notification** | Status message | Log to external system |
| **PreCompact** | Before conversation trim | Archive conversation |

---

## Hook Structure

Hooks are shell scripts that receive event data via stdin:

```bash
#!/bin/bash
# pre-tool-use-logger.sh

# Read event data
read -r EVENT_DATA

# Parse tool name
TOOL=$(echo "$EVENT_DATA" | jq -r '.tool_name')

# Log to file
echo "[$(date)] Tool called: $TOOL" >> /var/log/agent-tools.log
```

---

## Creating Hooks

**Via Settings → Node Managers → Hooks:**

1. Click "Add New Hook"
2. Enter name (e.g., "Tool Logger")
3. Select event type (e.g., PreToolUse)
4. Write script (bash, Python, Node.js)
5. Save to workspace library

**Hook appears in sidebar → drag to canvas.**

---

## Hook Examples

### Example 1: Tool Call Logger (PreToolUse)

**Purpose:** Log all tool calls to file

```bash
#!/bin/bash
# log-tool-calls.sh

read -r EVENT

TOOL=$(echo "$EVENT" | jq -r '.tool_name')
TIMESTAMP=$(date +"%Y-%m-%d %H:%M:%S")

echo "[$TIMESTAMP] Tool: $TOOL" >> ~/agent-logs/tools.log
```

**Use case:** Audit trail of agent actions

---

### Example 2: Cost Tracker (PostToolUse)

**Purpose:** Track API costs per tool

```python
#!/usr/bin/env python3
# track-costs.py

import json
import sys

event = json.load(sys.stdin)
tokens = event.get('metadata', {}).get('tokens', 0)
cost_per_token = 0.00001

cost = tokens * cost_per_token

with open('costs.csv', 'a') as f:
    f.write(f"{event['tool_name']},{tokens},{cost}\n")
```

**Use case:** Monitor spending

---

### Example 3: Session Initializer (SessionStart)

**Purpose:** Load user preferences on session start

```bash
#!/bin/bash
# init-session.sh

USER_ID=$(echo "$1" | jq -r '.user_id')

# Load user preferences
PREFS=$(cat ~/users/$USER_ID/preferences.json)

# Set environment variables
export USER_PREFS="$PREFS"

echo "Session initialized for user $USER_ID"
```

**Use case:** Personalized agent behavior

---

### Example 4: Profanity Filter (UserPromptSubmit)

**Purpose:** Filter inappropriate user input

```python
#!/usr/bin/env python3
# filter-profanity.py

import json
import sys

event = json.load(sys.stdin)
message = event.get('message', '')

# Check for profanity (simple example)
profanity_list = ['badword1', 'badword2']

for word in profanity_list:
    if word in message.lower():
        # Replace with asterisks
        message = message.replace(word, '*' * len(word))

# Output filtered message
print(json.dumps({'message': message}))
```

**Use case:** Content filtering

---

## Event Data Structure

Each hook receives JSON event data:

### PreToolUse Event

```json
{
  "event": "pre_tool_use",
  "tool_name": "read_file",
  "parameters": {
    "file_path": "/path/to/file.txt"
  },
  "timestamp": "2025-01-10T10:30:00Z"
}
```

### PostToolUse Event

```json
{
  "event": "post_tool_use",
  "tool_name": "read_file",
  "result": "File content here...",
  "metadata": {
    "tokens": 150,
    "duration_ms": 250
  },
  "timestamp": "2025-01-10T10:30:01Z"
}
```

### SessionStart Event

```json
{
  "event": "session_start",
  "agent_id": "email-summarizer",
  "user_id": "user-123",
  "timestamp": "2025-01-10T10:30:00Z"
}
```

---

## Configuration

**When clicked on canvas:**
- Edit hook script
- Select event type
- Configure environment variables
- Test hook execution

---

## Best Practices

**✅ Do:**
- Keep hooks fast (< 100ms)
- Handle errors gracefully
- Log to files, not stdout (except results)
- Use async operations when possible
- Test hooks thoroughly

**❌ Don't:**
- Block agent execution with slow hooks
- Modify global state unexpectedly
- Ignore errors
- Use hooks for complex logic (use skills instead)

---

## Common Patterns

### Pattern 1: Audit Logging

```
[PreToolUse Hook] → Log tool call
[Agent executes tool]
[PostToolUse Hook] → Log result + duration
```

**Use case:** Compliance, debugging

---

### Pattern 2: Rate Limiting

```
[PreToolUse Hook] → Check rate limit
If exceeded: Cancel tool execution
If OK: Allow + increment counter
```

**Use case:** Prevent API abuse

---

### Pattern 3: Cost Control

```
[PostToolUse Hook] → Track token usage
If monthly budget exceeded: Alert user
```

**Use case:** Budget management

---

## Security Considerations

**⚠️ Important:**
- Hooks run with same permissions as agent
- Can access environment variables (including secrets)
- Validate hook scripts before use
- Avoid executing untrusted code
- Use hooks for read-only operations when possible

---

## Next Steps

- [Sub-agents Node](subagents-node.md) - Specialized agents
- [Testing Agents](../06-testing-agents.md) - Test hooks
- [Canvas Workflow](../05-canvas-workflow.md) - Build complex workflows

---

<div align="center">

[← MCPs Node](mcps-node.md) | [Agent Node](agent-node.md) | [Sub-agents Node →](subagents-node.md)

</div>
