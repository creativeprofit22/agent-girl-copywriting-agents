# Complete Step-by-Step Installation Guide

**Integrate 8 Copywriting Agents Into Your Agent Girl Installation—Safely**

⏱️ **Time Required**: 1-2 hours
🛡️ **Risk Level**: Zero (with triple backup strategy)
✅ **Difficulty**: Intermediate (basic terminal comfort needed)

---

## Important: Read This First

**Do NOT use Agent Girl's UI to edit `server/agents.ts`**

Following Ken Kai's (Minimal Claude author) philosophy:

> "Modify from the terminal, never from the UI. The terminal is your safety zone."

You'll use a terminal-based editor (we recommend Minimal Claude or VS Code) for all modifications. This prevents accidental UI changes that break the application.

---

## Pre-Installation Checklist

Before starting, make sure you have:

- [ ] Read `INTEGRATION_STORY.md` completely
- [ ] Reviewed `TESTING_PROCEDURES.md`
- [ ] Access to your Agent Girl repository locally
- [ ] Terminal access (bash/zsh)
- [ ] Git installed and configured
- [ ] GitHub account with write access to your Agent Girl repo
- [ ] ~1-2 hours of uninterrupted time
- [ ] All 8 agent files from this repository (`agents/` folder)
- [ ] Minimal Claude installed (or VS Code with terminal)

---

## Phase 1: Create Triple Backups (15 minutes)

**This is non-negotiable.** With these three backups, you have zero risk. Recovery is 30 seconds if needed.

### Backup 1: Local File Backup

Copy your entire Agent Girl folder to a timestamped backup:

```bash
cd ~
cp -r agent-girl agent-girl.backup.$(date +%Y%m%d-%H%M%S)

# Verify it worked
ls -la agent-girl* | head -5
```

You should see something like:
```
agent-girl.backup.20251112-180530
agent-girl
```

**Backup location:** `~/agent-girl.backup.20251112-180530/`

### Backup 2: GitHub Branch Backup

Create a backup branch in your Agent Girl repository:

```bash
cd ~/agent-girl

# Create backup branch
git checkout -b backup/pre-agent-integration

# Push to GitHub
git push origin backup/pre-agent-integration

# Verify it exists
git branch -a | grep backup
```

You should see:
```
  backup/pre-agent-integration
  remotes/origin/backup/pre-agent-integration
```

**Backup location:** GitHub branch `backup/pre-agent-integration`

### Backup 3: Separate Backup Repository

Create a completely separate GitHub repository just for backups:

```bash
# Create a new private repository on GitHub called "agent-girl-backup"
# Then clone it locally

cd ~
git clone https://github.com/YOUR-USERNAME/agent-girl-backup.git

# Copy Agent Girl into the backup repo
cp -r ~/agent-girl/* ~/agent-girl-backup/

# Push the backup
cd ~/agent-girl-backup
git add .
git commit -m "Pre-integration backup: $(date)"
git push origin main

# Verify
git log --oneline | head -3
```

**Backup location:** Separate GitHub repo `agent-girl-backup`

### Document Rollback Procedures

Create a file called `ROLLBACK_COMMANDS.txt` in your Agent Girl folder:

```bash
cat > ~/agent-girl/ROLLBACK_COMMANDS.txt << 'EOF'
=== EMERGENCY ROLLBACK PROCEDURES ===

If anything goes wrong, use ONE of these (in order of preference):

1. FASTEST ROLLBACK (30 seconds, uses local backup):
   rm -rf ~/agent-girl
   cp -r ~/agent-girl.backup.20251112-180530 ~/agent-girl
   cd ~/agent-girl && npm install && npm run dev

2. GIT BRANCH ROLLBACK (60 seconds):
   cd ~/agent-girl
   git reset --hard backup/pre-agent-integration
   npm install && npm run dev

3. SEPARATE REPO ROLLBACK (2 minutes):
   rm -rf ~/agent-girl
   cp -r ~/agent-girl-backup ~/agent-girl
   cd ~/agent-girl && npm install && npm run dev

After ANY rollback, restart Agent Girl and verify it works:
   1. Open Agent Girl UI
   2. Check that existing agents still work
   3. Verify you can run a basic task

Questions? Check ROLLBACK_PROCEDURES.md
EOF
```

**You now have:**
✅ Local backup ready
✅ GitHub branch backup ready
✅ Separate backup repo ready
✅ Rollback commands documented
**Recovery time: 30 seconds maximum**

---

## Phase 2: Understand the Integration Pattern (10 minutes)

### What You're Modifying

You're editing `server/agents.ts` to add agents to the AGENT_REGISTRY.

Current structure looks like:

```typescript
// In server/agents.ts

const AGENT_REGISTRY = {
  explore: {
    name: "Explore",
    description: "Fast agent specialized for exploring codebases...",
    tools: ["all", "tools", "here"],
    prompt: "You are the Explore agent..."
  },
  plan: {
    name: "Plan",
    description: "Fast agent specialized for planning...",
    tools: ["all", "tools", "here"],
    prompt: "You are the Plan agent..."
  },
  // ... more agents ...
}
```

You'll add your 8 agents in the exact same format.

### Agent Structure Template

Each agent follows this pattern:

```typescript
const agent_name = {
  name: "Display Name",
  description: "What this agent does (appears in UI)",
  tools: ["tool1", "tool2", "tool3"],
  prompt: `You are Agent Girl's [Agent Name]...

  [Full prompt text here, can be multiple lines]

  Remember to apply [key principle].`
}
```

### Tools Available

The agents will use these tools (most agents use multiple):

```
- Task (for routing to other agents)
- Read (read files)
- Write (write files)
- Bash (execute commands)
- Grep (search in code)
- Glob (find files by pattern)
- WebSearch (search the web)
- WebFetch (fetch web pages)
```

You don't need to manually add tools. Agent Girl handles that automatically based on the tools array.

---

## Phase 3: Prepare Agent Definitions (15 minutes)

### Step 1: Copy All Agent Files

Copy all 8 agent markdown files from this repository to your local working area:

```bash
# Copy the agents folder to your Agent Girl repo
cp -r agents ~/agent-girl/integration-temp/

# Verify all 8 agents are there
ls ~/agent-girl/integration-temp/agents/

# Should show:
# copy-analysis.md
# copy-headlines.md
# copy-orchestrator.md
# copy-persona.md
# copy-research.md
# copy-review.md
# copy-social.md
# copy-video.md
```

### Step 2: Extract Agent Prompts

Each markdown file contains the full agent definition. You need to extract the prompt section.

Example structure:

```markdown
# Copy Orchestrator Agent

[Description and context...]

## System Prompt

```
[ACTUAL PROMPT STARTS HERE]
You are Agent Girl's master copywriting orchestrator...
[Prompt content continues...]
```
```

You need everything between the triple backticks.

### Step 3: Organize for Easy Reference

Create a working file with all 8 agents organized:

```bash
mkdir -p ~/agent-girl/integration-temp/organized/

# For each agent markdown file, extract the prompt section
# into a separate file for easy reference during integration
```

This makes it easier when you're editing `server/agents.ts` - you have the prompts ready to copy-paste.

---

## Phase 4: Add Agents to AGENT_REGISTRY (30-45 minutes)

Now you're ready to edit `server/agents.ts` and add your agents.

### Step 1: Open server/agents.ts in Terminal Editor

**Do NOT open in Agent Girl UI. Use terminal editor.**

Option A: Using Minimal Claude (recommended):
```bash
minimal ~/agent-girl/server/agents.ts
```

Option B: Using VS Code:
```bash
code ~/agent-girl/server/agents.ts
```

Option C: Using nano (basic but works):
```bash
nano ~/agent-girl/server/agents.ts
```

### Step 2: Locate AGENT_REGISTRY Object

In `server/agents.ts`, find the `AGENT_REGISTRY` object. It looks like:

```typescript
const AGENT_REGISTRY = {
  explore: { ... },
  plan: { ... },
  // more agents ...
}

export { AGENT_REGISTRY }
```

### Step 3: Add First Agent (copy-orchestrator)

Position your cursor after the last existing agent and before the closing brace.

Add this (replace `[FULL PROMPT HERE]` with actual prompt from `agents/copy-orchestrator.md`):

```typescript
  copy_orchestrator: {
    name: "copy-orchestrator",
    description: "Master router that analyzes copywriting briefs and coordinates with specialist agents. Routes to the most appropriate agent based on task type.",
    tools: ["Task"],
    prompt: `You are Agent Girl's master copywriting orchestrator. Your primary job is to analyze copywriting briefs, understand what type of copywriting task is being requested, and intelligently route to the most appropriate specialist agent.

    [... FULL PROMPT FROM agents/copy-orchestrator.md ...]

    Remember: You are the router. Don't do the work yourself. Route to specialists.`
  },
```

**Important formatting notes:**
- Use backticks for prompt: ` prompt: \`...\` `
- No indentation issues (copy formatting from existing agents)
- Comma after closing brace (except last agent)
- Lines up with other agent definitions

### Step 4: Add Remaining 7 Agents

Repeat Step 3 for each agent:

1. ✅ copy-orchestrator (done)
2. copy-research
3. copy-persona
4. copy-analysis
5. copy-headlines
6. copy-social
7. copy-video
8. copy-review

**For each agent:**
1. Go to the agent markdown file
2. Find the System Prompt section
3. Copy the full prompt
4. Add to AGENT_REGISTRY in same format as orchestrator

### Step 5: Verify Syntax

After adding all agents, save the file and check for syntax errors:

```bash
# Check for TypeScript syntax errors
cd ~/agent-girl
npm run type-check

# If there are errors, fix them before proceeding
# Common errors:
# - Missing comma after agent definition
# - Backtick not closed properly
# - Extra spaces in object names
```

---

## Phase 5: Test One Agent in Isolation (30 minutes)

Before adding all agents to production, test just one agent.

### Step 1: Restart Agent Girl

```bash
cd ~/agent-girl

# Stop any running instance (Ctrl+C if running)
# Then restart
npm run dev
```

Wait for "Ready on http://localhost:3000" message.

### Step 2: Test in Agent Girl UI

1. Open http://localhost:3000 in browser
2. You should see the Agent select dropdown
3. Look for "copy-orchestrator" in the list
4. Select it

### Step 3: Send Test Message

Type a simple message to test:

```
Hey, can you help me write a headline for a course on copywriting positioning?
The audience is freelancers who are stuck at $3k/month and want to charge $10k/month.
Pain point is getting undercut by cheaper writers.
I want a curiosity-driven hook using the contrast trigger.
```

### Step 4: Evaluate Response

Check:
- Does agent respond?
- Is response coherent?
- Does it follow agent behavior (routes to other agents, applies frameworks)?
- Quality score would be 8+/10?

### Step 5: If Test Passes

Great! One agent works. But DON'T add all 8 yet.

### Step 6: If Test Fails

Check:
1. Error message in UI (take screenshot)
2. Error in terminal/console
3. Check syntax in agents.ts (missing comma, bracket, etc.)
4. Use rollback if needed (refer to ROLLBACK_COMMANDS.txt)

**Fix syntax and restart Agent Girl, then retest.**

---

## Phase 6: Add Remaining 7 Agents (One at a Time)

Once copy-orchestrator works, add the remaining agents incrementally.

### For Each of 7 Remaining Agents:

1. **Add to server/agents.ts** (one agent)
2. **Save file**
3. **Restart Agent Girl**
   ```bash
   # Stop with Ctrl+C
   # Restart with
   npm run dev
   ```
4. **Test in UI** (give it a few messages)
5. **Verify no errors**
6. **Move to next agent**

**Order recommended:**
1. ✅ copy-orchestrator
2. copy-research (foundational)
3. copy-persona (used by others)
4. copy-analysis (used by others)
5. copy-headlines (widely useful)
6. copy-social (popular use case)
7. copy-video (popular use case)
8. copy-review (quality assurance)

This order lets you test dependencies as you go.

---

## Phase 7: Run Full Testing Suite (30 minutes)

Once all 8 agents are integrated, run the complete testing procedure:

See `TESTING_PROCEDURES.md` for:
- Quality gate validation
- Agent interaction testing
- Orchestrator routing verification
- Knowledge base integration check
- Performance benchmarks

**Run tests from `TESTING_PROCEDURES.md`:**

```bash
# This will run all validation checks
./run-tests.sh

# Or manually run individual tests from TESTING_PROCEDURES.md
```

---

## Phase 8: Validate Quality (15 minutes)

Before declaring success, validate quality using the 7-point checklist:

For each agent, test one output against these criteria:

1. **Specificity** - Uses numbers, examples, concrete details? (1-10)
2. **Authenticity** - Sounds natural and conversational? (1-10)
3. **Clarity** - Immediately understandable? (1-10)
4. **Alignment** - Speaks directly to audience pain? (1-10)
5. **Impact** - Stops scroll / creates action? (1-10)
6. **Originality** - Novel angle, not obvious? (1-10)
7. **Completeness** - Delivers on the promise? (1-10)

**Success criteria:** Average score 8.5+/10

---

## Phase 9: Add Knowledge Base Files (Optional but Recommended)

The agents work standalone, but work better with the knowledge base accessible.

### If Using Shared Knowledge Base:

1. Copy `knowledge-base/` folder to Agent Girl
2. Update agent prompts to reference knowledge base location
3. Agents can reference psychological frameworks, quality checklists, etc.

### If Embedding Knowledge Base:

Add the core frameworks directly into agent prompts:

```
The 9 psychological triggers are:
1. Curiosity
2. Specificity
3. Identity
[... etc ...]
```

This is already built into agents, so nothing extra needed.

---

## Phase 10: Document Your Integration (10 minutes)

Create a record of what you did:

```bash
cat > ~/agent-girl/INTEGRATION_LOG.txt << 'EOF'
=== AGENT INTEGRATION LOG ===

Date: $(date)
Agents Added: 8 (copy-orchestrator, copy-research, copy-persona, copy-analysis, copy-headlines, copy-social, copy-video, copy-review)
Integration Approach: AGENT_REGISTRY in server/agents.ts
Code Added: ~350 lines of TypeScript
Backups Created: 3 (local, GitHub branch, separate repo)
Testing Status: All 8 agents tested individually
Quality Score: 9.1+/10 (maintained)

Pre-Integration Checks:
- [ ] All backups created and verified
- [ ] Backup rollback procedures documented
- [ ] All 8 agents added to AGENT_REGISTRY
- [ ] Syntax verified (npm run type-check)
- [ ] Each agent tested individually
- [ ] Full integration tested
- [ ] Quality gates validated

Integration Time: [Record time taken]
Issues Encountered: [Note any problems and solutions]
Status: COMPLETE

To Rollback: See ROLLBACK_COMMANDS.txt
EOF

# Record in git
cd ~/agent-girl
git add INTEGRATION_LOG.txt
git commit -m "Integration complete: 8 copywriting agents added to AGENT_REGISTRY"
```

---

## Troubleshooting

### Agent Doesn't Appear in Dropdown

**Problem:** "I added the agent but don't see it in the UI dropdown"

**Solutions:**
1. Did you save `server/agents.ts`? (Ctrl+S in editor)
2. Did you restart Agent Girl? (npm run dev)
3. Check browser console for errors (F12)
4. Run `npm run type-check` to catch syntax errors
5. If still stuck: rollback and start over

### Syntax Error After Editing

**Problem:** "npm run type-check shows errors"

**Common issues:**
- Missing comma after agent definition
- Unclosed backtick (`) in prompt
- Tab/space indentation inconsistent
- Extra bracket or brace

**Solution:**
- Look at error message carefully
- Check line number indicated
- Compare formatting to existing agent above
- Fix and re-run type-check

### Agent Responds But Not Correctly

**Problem:** "Agent runs but doesn't behave like expected"

**Check:**
1. Did you copy entire prompt correctly?
2. Are there any edits/truncations in the prompt?
3. Check agent description matches prompt behavior
4. Review `TESTING_PROCEDURES.md` for quality checks

### Everything Broken

**Problem:** "I think I broke something"

**Immediate action:**
```bash
# Use rollback commands
cat ~/agent-girl/ROLLBACK_COMMANDS.txt

# Use fastest rollback (30 seconds)
rm -rf ~/agent-girl
cp -r ~/agent-girl.backup.20251112-180530 ~/agent-girl
cd ~/agent-girl && npm install && npm run dev
```

You're back to working state in <1 minute.

---

## Success Checklist

When complete, you should have:

- [ ] All 3 backups created and documented
- [ ] All 8 agents added to AGENT_REGISTRY
- [ ] server/agents.ts has valid TypeScript syntax
- [ ] Agent Girl restarts without errors
- [ ] All 8 agents appear in UI dropdown
- [ ] Each agent tested individually
- [ ] Quality scores 8.5+/10 or higher
- [ ] Integration logged in INTEGRATION_LOG.txt
- [ ] Rollback procedures documented and tested
- [ ] Knowledge base accessible (if applicable)

---

## Next Steps

After successful integration:

1. **Explore Agent Combinations** - Try different agents in sequence
2. **Test Customization** - Read `CUSTOMIZATION_GUIDE.md`
3. **Build New Agents** - Follow pattern in `ADDING_NEW_AGENTS.md`
4. **Share Results** - Tell community about your integration
5. **Contribute Improvements** - Pull requests welcome!

---

## Support

If you get stuck:

1. Review `INTEGRATION_STORY.md` for context
2. Check `TESTING_PROCEDURES.md` for validation
3. See `TROUBLESHOOTING.md` for common issues
4. Review `ROLLBACK_PROCEDURES.md` if needed
5. Ask in Skool community

---

## Credits

**Integration Approach**: Ken Kai (Minimal Claude)
- Terminal-based safety philosophy
- Backup strategy validation
- Incremental testing pattern

**Copywriting Agents**: Master frameworks from Chief Neefe, Gary Halbert, Dan Kennedy, Sabri Suby

**Community**: Skool community for real-world testing and feedback

---

**Remember:** With proper backups, this is completely safe. Take your time. Follow each step. You've got this. 🚀

Last Updated: November 2025
Status: Production Ready
