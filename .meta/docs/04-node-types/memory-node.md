# Memory Node

**Memory** gives your agent persistent knowledge and long-term context.

---

## Overview

**Purpose:** Store knowledge, conversation history, and reference information
**Connection:** Bottom-left handle of main agent card
**Color:** Green
**Icon:** 🧠
**Required:** Optional (0 to many)

---

## What is Memory?

Memory nodes contain markdown files that provide your agent with:
- Domain knowledge
- Company information
- Conversation context
- Reference documentation
- Historical data

---

## Memory Structure

Memory is organized as markdown files in folders:

```
memory-layer/
├── company-info.md
├── team-contacts.md
├── product-specs.md
└── faq.md
```

Each file contains knowledge in plain markdown format.

---

## Memory Types

### 1. Knowledge Base

**Purpose:** Domain-specific information

**Example: Company Knowledge Base**
```markdown
# TechCorp Company Information

## About Us
TechCorp is a software company specializing in...

## Products
- Product A: Cloud-based solution for...
- Product B: On-premise software for...

## Support Hours
Monday-Friday: 9am-6pm EST
```

**Use case:** Customer support agents with company context

---

### 2. Prime Context

**Purpose:** Always-available context included in every interaction

**Example: Agent Guidelines**
```markdown
# Agent Operating Guidelines

## Communication Style
- Professional but friendly
- Concise responses
- Always cite sources

## Restrictions
- Never share customer data
- Don't make promises about features
- Escalate billing issues to finance
```

**Use case:** Ensure consistent agent behavior

---

### 3. Conversation History

**Purpose:** Maintain context across sessions

**Example: Previous Interactions**
```markdown
# Customer: John Doe (ID: 12345)

## 2025-01-05 - Password Reset
Customer requested password reset. Issue resolved.

## 2025-01-08 - Billing Question
Asked about invoice #5678. Referred to finance team.
```

**Use case:** Personalized multi-session support

---

## Creating Memory

**Via Settings → Node Managers → Memory:**

1. Click "Add New Memory Layer"
2. Enter name (e.g., "Company KB")
3. Add markdown files
4. Write content in each file
5. Save to workspace library

**Memory layer appears in sidebar → drag to canvas → connect to main agent.**

---

## Configuration

**When clicked on canvas:**
- Add/edit markdown files
- Organize into subfolders
- Set priority (which files load first)
- Configure memory scope (always vs. contextual)

---

## Real-World Examples

### Example 1: Customer Support Knowledge Base

**Structure:**
```
customer-support-kb/
├── products.md          # Product catalog
├── policies.md          # Company policies
├── troubleshooting.md   # Common issues
└── contacts.md          # Team contacts
```

**products.md:**
```markdown
# Product Catalog

## TechCorp Cloud
- Pricing: $99/month
- Features: Unlimited storage, 24/7 support
- Trial: 14-day free trial

## TechCorp Enterprise
- Pricing: Custom
- Features: On-premise, dedicated support
- Contact sales for pricing
```

---

### Example 2: Code Review Style Guide

**Structure:**
```
code-review-guide/
├── style-guide.md       # Coding standards
├── security-checklist.md # Security best practices
└── examples.md          # Good/bad examples
```

**style-guide.md:**
```markdown
# Python Style Guide

## Naming Conventions
- Functions: snake_case
- Classes: PascalCase
- Constants: UPPER_SNAKE_CASE

## Imports
- Standard library first
- Third-party second
- Local imports last

## Example
\`\`\`python
import os
import sys

import requests

from .utils import helper
\`\`\`
```

---

## Memory Patterns

### Pattern 1: Layered Knowledge

```
[Main Agent]
     ↓
[General KB] + [Specialized KB] + [User History]
```

**Use case:** Agent with broad knowledge + domain expertise + personalization

---

### Pattern 2: RAG (Retrieval-Augmented Generation)

**Concept:** Agent retrieves relevant memory chunks based on user query

**Implementation:**
1. Store large knowledge base as memory
2. Agent searches relevant sections
3. Agent uses retrieved context for response

**Use case:** Documentation Q&A, technical support

---

## Best Practices

**✅ Do:**
- Use clear markdown headings
- Keep files focused (one topic per file)
- Update regularly
- Include examples and specifics
- Organize with folders

**❌ Don't:**
- Store huge files (split into smaller chunks)
- Include outdated information
- Use complex formatting (keep simple)
- Duplicate information across files

---

## Memory vs. System Prompt

| Feature | System Prompt | Memory |
|---------|---------------|--------|
| **When to use** | Instructions, behavior | Facts, knowledge |
| **Example** | "You are helpful" | "Company founded 2020" |
| **Changeable** | Rarely | Frequently |
| **Scope** | Every interaction | Contextual retrieval |

**Rule:** Instructions in prompt, facts in memory.

---

## Next Steps

- [Commands Node](commands-node.md) - Create slash commands
- [MCPs Node](mcps-node.md) - External integrations
- [Canvas Workflow](../05-canvas-workflow.md) - Build complex agents

---

<div align="center">

[← Skills Node](skills-node.md) | [Agent Node](agent-node.md) | [Commands Node →](commands-node.md)

</div>
