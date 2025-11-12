# Simple Installation Guide

**Using Claude Minimal (Terminal Editor) in VS Code**

---

## The Easy Way (5 Minutes)

### Prerequisites
- Agent Girl project open in VS Code
- Claude Code extension installed (with terminal access)
- This repository cloned or files available

### Step 1: Open Terminal in Agent Girl

In VS Code, open the terminal:
```bash
cd ~/path/to/agent-girl
```

### Step 2: Open server/agents.ts in Minimal Claude

```bash
minimal server/agents.ts
```

**Important:** Minimal Claude will open a chat interface and ask you questions about what you're trying to do. Be specific:

- "I'm adding copywriting agents to AGENT_REGISTRY"
- "I have agent prompts from GitHub that need to be added"
- "I want to add the copy-commander agent first"

Minimal Claude will use these answers to help you do it better. Just answer naturally - it's there to assist.

Or use VS Code's built-in editor directly:
```bash
code server/agents.ts
```

**What to Expect:**
When you run `minimal server/agents.ts`, Claude will:
- Ask what you're working on
- Ask which agent you want to add
- Ask where the prompts are located
- Offer to help you format and add the code correctly
- Guide you through the process step-by-step

Just let it know you're adding copywriting agents and it will handle the details. You're not alone in this - Claude is helping!

### Step 3: Locate AGENT_REGISTRY

Find the `AGENT_REGISTRY` object in the file. It looks like:

```typescript
const AGENT_REGISTRY = {
  explore: { ... },
  plan: { ... },
  // existing agents here
}
```

### Step 4: Add Agent Prompt

After the last existing agent, add your agent. Example (copy-commander):

```typescript
const copy_commander = {
  name: "copy-commander",
  description: "Master copywriting orchestrator that routes briefs to appropriate specialist agents",
  tools: ["Task"],
  prompt: `[COPY FULL PROMPT FROM agents/copy-commander/prompt.md HERE]`
},
```

### Step 5: Save & Restart

1. Save file (Ctrl+S or Cmd+S)
2. Stop Agent Girl (Ctrl+C in terminal)
3. Restart: `npm run dev`
4. Check UI - agent should appear in dropdown

### Step 6: Repeat for Other Agents

Add remaining agents (copy-social, copy-research, etc.) one at a time, testing each.

---

## That's It!

No complex procedures. No multiple phases. Just:
1. Open file with Minimal Claude (it asks questions to help)
2. Answer Claude's questions about what you're doing
3. Let Claude guide you through adding the agent
4. Save & restart
5. Test in Agent Girl UI

---

## The Magic: Minimal Claude Asks Questions

The beauty of this approach is that **Minimal Claude isn't just a dumb editor** - it's an AI that understands what you're doing:

✅ You say: "I want to add the copy-social agent"
✅ Claude asks: "Do you have the prompt file? Should I help format it?"
✅ You say: "It's in agents/copy-writers/social/prompt.md"
✅ Claude: "I'll help you add it correctly to AGENT_REGISTRY"

**It's a conversation, not a manual process.** Claude does the heavy lifting.

---

If something breaks, Agent Girl restarts fine. Just fix the syntax and try again.

---

**Status**: Production Ready
**Time**: 1-2 hours for all 14 agents
**Difficulty**: Easy (Claude handles most of it)
**Experience**: Interactive (Minimal Claude asks questions to help you)
