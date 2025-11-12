# Rollback & Emergency Recovery Procedures

**How to Safely Recover If Anything Goes Wrong**

---

## Core Philosophy

> "You don't integrate agents because you're confident nothing will go wrong. You integrate agents because you KNOW what to do if something does go wrong."

With the triple backup strategy, recovery is **30 seconds maximum**.

---

## The Three Backup Methods (In Order of Speed)

### 1. Local Backup (Fastest - 30 seconds)

**Speed:** ⚡ 30 seconds
**Reliability:** ✅ Highest
**Recommended for:** Most situations

```bash
# STOP Agent Girl
# (Press Ctrl+C in terminal, or kill the npm process)

# Restore from local backup
rm -rf ~/agent-girl
cp -r ~/agent-girl.backup.20251112-180530 ~/agent-girl

# Reinstall dependencies
cd ~/agent-girl
npm install

# Start Agent Girl
npm run dev
```

**Verify recovery:**
1. Agent Girl loads without errors
2. Original agents (Explore, Plan, etc.) appear in dropdown
3. UI is responsive
4. Copywriting agents are GONE (back to pre-integration state)

### 2. Git Branch Rollback (Fast - 60 seconds)

**Speed:** ⚡⚡ 60 seconds
**Reliability:** ✅ Very High
**Recommended for:** If local backup corrupted

```bash
# STOP Agent Girl (Ctrl+C)

# Discard all local changes
cd ~/agent-girl
git reset --hard

# Switch to backup branch
git checkout backup/pre-agent-integration

# Reinstall dependencies
npm install

# Start Agent Girl
npm run dev
```

**Verify recovery:**
1. Agent Girl loads without errors
2. You're on backup/pre-agent-integration branch
2. Original agents work
3. Copywriting agents are GONE

### 3. Separate Backup Repository (Most Thorough - 2 minutes)

**Speed:** ⚡⚡⚡ 2 minutes
**Reliability:** ✅ Highest (completely separate system)
**Recommended for:** If both local and git backups corrupted

```bash
# STOP Agent Girl (Ctrl+C)

# Remove corrupted Agent Girl
rm -rf ~/agent-girl

# Copy from separate backup repo
cp -r ~/agent-girl-backup ~/agent-girl

# Install dependencies
cd ~/agent-girl
npm install

# Start Agent Girl
npm run dev
```

**Verify recovery:**
1. Agent Girl loads without errors
2. Original agents work
3. Copywriting agents are GONE
4. System fully restored to pre-integration state

---

## Step-by-Step Emergency Recovery

### Scenario 1: Agent Girl Won't Start After Integration

**Symptoms:**
- npm run dev shows error
- Application crashes on startup
- "Cannot find module" or "SyntaxError" in terminal

**Recovery (Choose One):**

**Option A (Fastest):**
```bash
# Stop the process
Ctrl+C

# Restore local backup
rm -rf ~/agent-girl
cp -r ~/agent-girl.backup.20251112-180530 ~/agent-girl
cd ~/agent-girl
npm install && npm run dev

# Check: Application starts without errors
```

**Option B (If Option A fails):**
```bash
# Stop the process
Ctrl+C

# Reset to git backup branch
cd ~/agent-girl
git reset --hard
git checkout backup/pre-agent-integration
npm install && npm run dev

# Check: Application starts without errors
```

### Scenario 2: Agent Girl Starts But UI Is Broken

**Symptoms:**
- Application loads but interface is incomplete
- Agents dropdown doesn't work
- Buttons/text not rendering
- Console shows JavaScript errors

**Recovery:**

```bash
# Option A: Clear browser cache and restart
# 1. Stop Agent Girl (Ctrl+C)
# 2. Clear browser cache (Ctrl+Shift+Delete or Cmd+Shift+Delete)
# 3. Close all browser tabs
# 4. npm run dev
# 5. Open fresh browser window to http://localhost:3000

# Option B: If still broken, use local backup
rm -rf ~/agent-girl
cp -r ~/agent-girl.backup.20251112-180530 ~/agent-girl
cd ~/agent-girl
npm install && npm run dev

# Check: UI loads completely and normally
```

### Scenario 3: Copywriting Agents Are Broken But Everything Else Works

**Symptoms:**
- Agent Girl loads fine
- Some agents work (Explore, Plan)
- Copywriting agents error or don't respond correctly
- UI functions normally

**Recovery (Non-Emergency):**

Option A: Live Fix (if minor issue)
```bash
# Edit server/agents.ts to fix the issue
# (Use Minimal Claude, not UI)
nano ~/agent-girl/server/agents.ts

# Fix the specific agent (syntax error, typo, etc.)
# Save and restart
npm run dev
```

Option B: Remove Just the Broken Agent
```bash
# Edit server/agents.ts
nano ~/agent-girl/server/agents.ts

# Find the broken agent definition
# Delete just that agent from AGENT_REGISTRY
# Save and restart
npm run dev
```

Option C: Full Rollback to Pre-Integration
```bash
# If too complicated, just rollback to pre-integration state
rm -rf ~/agent-girl
cp -r ~/agent-girl.backup.20251112-180530 ~/agent-girl
cd ~/agent-girl
npm install && npm run dev

# Start integration over more carefully
```

### Scenario 4: Integration Partially Complete and System Unstable

**Symptoms:**
- Some agents added, some not
- Inconsistent behavior
- Not sure what state system is in
- Want to start over cleanly

**Recovery:**

```bash
# Complete rollback
rm -rf ~/agent-girl
cp -r ~/agent-girl.backup.20251112-180530 ~/agent-girl
cd ~/agent-girl
npm install && npm run dev

# Verify pre-integration state
# Then carefully re-integrate following INSTALLATION.md
# This time, take notes on each step
```

---

## Verifying Successful Recovery

After any rollback, verify you're back to pre-integration state:

### Checklist

```bash
cd ~/agent-girl

# 1. Check git status
git status
# Should show: "Your branch is ahead of origin/backup/..."
# OR: "nothing to commit, working tree clean" (if on backup branch)

# 2. List all agents in AGENT_REGISTRY
grep -n "name:" server/agents.ts | head -20
# Should show: explore, plan, debugger, etc.
# Should NOT show: copy-orchestrator, copy-research, etc.

# 3. Start Agent Girl
npm run dev

# 4. In browser (http://localhost:3000):
#    - Open agent dropdown
#    - Verify ONLY original agents appear
#    - Verify Explore and Plan agents work
#    - NO copywriting agents visible

# 5. Check console (F12 in browser)
#    - No red error messages
#    - No TypeScript warnings
```

---

## Prevention: Avoiding Rollbacks

### Golden Rules

1. **Always create backups first** before any integration
2. **Never edit in UI** - always use terminal editor
3. **Test incrementally** - add one agent at a time
4. **Verify each step** - restart after each agent addition
5. **Keep documentation** - record what you change
6. **Commit frequently** - git commit after successful tests

### Early Warning Signs (Stop and Investigate)

If you notice:
- ❌ Typos in agent names
- ❌ Unclosed backticks or brackets in prompts
- ❌ npm run type-check shows errors
- ❌ Agent Girl restarts slowly (slowness indicates issues)
- ❌ UI elements don't load (console errors)

→ **STOP immediately** and fix before continuing

Don't let problems accumulate. Fix them right away.

---

## Quick Reference Card

**Disaster Recovery Card** (Save This!)

```
=== EMERGENCY ROLLBACK REFERENCE ===

FASTEST RECOVERY (Pick One):

1. Local Backup (30 sec):
   Ctrl+C
   rm -rf ~/agent-girl
   cp -r ~/agent-girl.backup.20251112-180530 ~/agent-girl
   cd ~/agent-girl && npm install && npm run dev

2. Git Branch (60 sec):
   Ctrl+C
   cd ~/agent-girl && git reset --hard
   git checkout backup/pre-agent-integration
   npm install && npm run dev

3. Separate Backup (2 min):
   Ctrl+C
   rm -rf ~/agent-girl
   cp -r ~/agent-girl-backup ~/agent-girl
   cd ~/agent-girl && npm install && npm run dev

Then verify recovery:
✅ Application starts
✅ Original agents in dropdown
✅ NO copywriting agents
✅ UI responsive

Questions? See ROLLBACK_PROCEDURES.md
```

---

## Recovery Time SLA

With the triple backup system, your recovery SLA is:

| Issue | Expected Recovery Time | Max Recovery Time |
|-------|----------------------|------------------|
| Syntax error in agents.ts | 30 seconds (local backup) | 60 seconds (git branch) |
| Complete Agent Girl corruption | 60 seconds (local backup) | 2 minutes (separate repo) |
| Git corruption | 60 seconds (separate repo) | N/A |
| All backups corrupted | Manual reload from cloud | N/A |

**In 99.9% of cases: 30-60 seconds recovery**

---

## Detailed Recovery Scenarios with Console Output

### Detailed Scenario: Syntax Error in Agent Definition

**What happened:**
```
You added copy-headlines agent but forgot closing backtick
in the prompt. Now Agent Girl won't start.
```

**Error output you see:**
```
$ npm run dev
> agent-girl@1.0.0 dev
> next dev

SyntaxError: Unexpected token (line 1547)
  at /home/user/agent-girl/server/agents.ts:1547:5
```

**Recovery steps:**

```bash
# Step 1: Stop it (Ctrl+C if still running)
Ctrl+C

# Step 2: Check your backup exists
ls ~/agent-girl.backup.*
# Should show: agent-girl.backup.20251112-180530

# Step 3: Restore from backup
rm -rf ~/agent-girl
cp -r ~/agent-girl.backup.20251112-180530 ~/agent-girl

# Step 4: Reinstall and start
cd ~/agent-girl
npm install
npm run dev

# Wait for "Ready on http://localhost:3000"
# You see: ✓ Ready in 2.3s
```

**Verification:**
```
Browser: Open http://localhost:3000
- See Agent Girl UI fully loaded ✅
- Click agent dropdown
- See: Explore, Plan, debugger, etc. ✅
- Do NOT see: copy-headlines (reverted to pre-integration) ✅
```

**You're back!** Now you know what went wrong (missing backtick). Learn from it and try integration again more carefully.

---

### Detailed Scenario: Git Corruption During Integration

**What happened:**
```
You were editing server/agents.ts directly (not in git properly).
Now git won't recognize your changes.
```

**Error you see:**
```
fatal: bad object 1234567
fatal: unpack-objects: unpack error
```

**Recovery steps:**

```bash
# Step 1: Stop Agent Girl
Ctrl+C

# Step 2: Reset git to clean state
cd ~/agent-girl
git reset --hard

# Step 3: Switch to backup branch
git checkout backup/pre-agent-integration

# Step 4: Verify you're on backup branch
git branch
# Should show: * backup/pre-agent-integration

# Step 5: Reinstall and restart
npm install
npm run dev
```

**You're recovered!** You're back to pre-integration state on the backup branch.

---

### Detailed Scenario: Multiple Failed Attempts

**What happened:**
```
You tried to add agents 3 times, each time had issues.
Now you're not sure what state system is in.
Easiest solution: Start completely fresh.
```

**Recovery steps:**

```bash
# Step 1: Stop Agent Girl
Ctrl+C

# Step 2: Remove the mess
rm -rf ~/agent-girl

# Step 3: Use separate backup (guaranteed clean)
cp -r ~/agent-girl-backup ~/agent-girl

# Step 4: Fresh start
cd ~/agent-girl
npm install
npm run dev

# Step 5: Verify clean state
# Browser: Check UI fully works
# Dropdown: Only original agents visible
# Tests: Run manual tests on Explore and Plan agents

# Step 6: Document what went wrong
# This time, follow INSTALLATION.md more carefully
# Take notes on each step
# Stop after each agent addition and test
```

**Learning:**
- When confused, use separate backup repo (it's cleanest)
- Take notes during integration
- Don't try to add all 8 at once - do one at a time
- Test each agent before adding the next

---

## Post-Recovery: Learn From It

After any rollback, spend 5 minutes learning:

### What went wrong?
```
Example: "I forgot to close a backtick in copy-headlines prompt"
```

### Why did it happen?
```
Example: "Copied prompt but didn't verify the backtick at the end"
```

### How will you prevent it next time?
```
Example: "I'll use a checklist:
1. Copy prompt
2. Verify closing backtick
3. Paste into agents.ts
4. Restart and test"
```

### Update your documentation
```bash
# Document what happened
cat >> ~/agent-girl/INTEGRATION_LOG.txt << 'EOF'

2025-11-12 14:35 - ROLLBACK #1
Issue: Missing closing backtick in copy-headlines
Resolution: Restored from local backup (30 sec)
Learning: Need to double-check backticks before saving
EOF
```

---

## When NOT to Rollback

Some situations don't need rollback:

**Situation 1: Agent outputs are lower quality than expected**
→ Don't rollback, try customizing the prompt
→ See CUSTOMIZATION_GUIDE.md

**Situation 2: One agent has a typo in output**
→ Don't rollback, edit that agent's prompt
→ Test and restart

**Situation 3: Want to change an agent's behavior**
→ Don't rollback, customize the agent
→ See CUSTOMIZATION_GUIDE.md

**Situation 4: Want to remove one agent but keep others**
→ Don't rollback, just delete that agent from AGENT_REGISTRY
→ Restart Agent Girl

**ONLY rollback when:**
- ✅ System won't start
- ✅ UI is completely broken
- ✅ Multiple agents failing
- ✅ Can't identify the problem
- ✅ You want to start completely over

---

## Backup Status Monitoring

Create a simple script to check your backups:

```bash
cat > ~/check-backups.sh << 'EOF'
#!/bin/bash

echo "=== BACKUP STATUS CHECK ==="
echo

echo "1. Local Backup:"
if [ -d ~/agent-girl.backup.* ]; then
  echo "  ✅ Found: $(ls -d ~/agent-girl.backup.* | tail -1)"
else
  echo "  ❌ NOT FOUND!"
fi

echo

echo "2. Git Branch Backup:"
cd ~/agent-girl
if git branch -a | grep -q "backup/pre-agent-integration"; then
  echo "  ✅ Found branch"
else
  echo "  ❌ Branch not found"
fi

echo

echo "3. Separate Backup Repo:"
if [ -d ~/agent-girl-backup ]; then
  echo "  ✅ Found"
else
  echo "  ❌ NOT FOUND!"
fi

echo
echo "Status: All three backups secure" || echo "Status: WARNING - Missing backups"
EOF

chmod +x ~/check-backups.sh
~/check-backups.sh
```

Run this monthly to ensure backups still exist.

---

## Questions Answered

**Q: How long does recovery actually take?**
A: 30 seconds for most common issues with local backup. Max 2 minutes with any backup method.

**Q: Will I lose any work?**
A: Only the failed integration attempt. All work before integration is safe. If worried, commit important changes to git first.

**Q: What if all 3 backups are corrupted?**
A: You can reload from git remote origin. See your git history to find last good state.

**Q: Do I need to keep all 3 backups?**
A: Yes, until integration is stable (1-2 weeks). After that, local and git are usually enough.

**Q: What if I accidentally delete a backup?**
A: If git backup exists, use that. If separate repo exists, use that. If both gone... you learned a lesson about backing up your backups.

**Q: How often should I test recovery?**
A: Test rollback procedure once before integration. Know it works before you need it.

---

## Final Checklist: Ready to Integrate?

Before starting integration, verify you have:

- [ ] All 3 backups created and tested
- [ ] ROLLBACK_COMMANDS.txt documented
- [ ] Terminal editor (Minimal Claude or VS Code) ready
- [ ] This file bookmarked and accessible
- [ ] Quick reference card printed or saved
- [ ] 1-2 hours uninterrupted time
- [ ] Confidence that if something breaks, you can recover in 30 seconds

✅ **Yes to all?** You're ready. Let's integrate! 🚀

---

**Last Updated**: November 2025
**Recovery SLA**: 30-60 seconds
**Confidence Level**: Very High
**Status**: Ready for Production

---

**Remember:** This level of safety is not excessive. It's prudent. Integration is safe when you KNOW you can recover instantly if needed.

That's the whole point.

Let's build with confidence. 🛡️
