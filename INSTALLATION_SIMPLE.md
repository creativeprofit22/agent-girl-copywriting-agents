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

Or use VS Code's built-in editor:
```bash
code server/agents.ts
```

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
1. Open file
2. Add agent prompt
3. Save
4. Restart
5. Test

If something breaks, Agent Girl restarts fine. Just fix the syntax and try again.

---

**Status**: Production Ready
**Time**: 1-2 hours for all 14 agents
**Difficulty**: Easy
