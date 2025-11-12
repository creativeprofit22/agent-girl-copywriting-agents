# Customization Guide

**How to Safely Customize Agents for Your Specific Needs**

---

## Overview

The agents are production-ready out of the box. But you might want to customize them for your:
- Specific industry
- Target audience
- Brand voice
- Company values
- Unique frameworks

This guide shows how to do that safely while maintaining quality.

---

## Golden Rule of Customization

> **Never modify the core prompt logic. Only add/customize the examples and context.**

The prompt structure is proven. Your industry-specific examples are the only thing that should change.

---

## Safe vs Unsafe Customizations

### ✅ SAFE Customizations

These maintain quality and don't break agents:

1. **Add industry examples**
   - "For SaaS copywriting, you might..."
   - "In legal writing, contrast looks like..."
   - "For e-commerce, specificity means..."

2. **Add brand voice guidelines**
   - "Use casual tone"
   - "Avoid jargon terms: [list]"
   - "Our brand voice emphasizes..."

3. **Add company context**
   - "You're writing for TechCorp"
   - "Our audience is engineering leads"
   - "Our positioning is: [statement]"

4. **Customize trigger examples**
   - Keep the 9 triggers, just add industry examples
   - "In legal writing, curiosity trigger looks like..."
   - Keep quality gate logic intact

5. **Add customization note**
   - "This customized version emphasizes..."
   - "Added SaaS-specific examples"
   - "Maintains 9.1+/10 quality standard"

### ❌ UNSAFE Customizations

These break agents or reduce quality:

- ❌ Changing the core trigger logic
- ❌ Removing quality gate criteria
- ❌ Changing tool usage
- ❌ Removing prompt sections
- ❌ Changing psychological framework fundamentals
- ❌ Adding conflicting instructions
- ❌ Removing safety guidelines

---

## Step-by-Step Customization Process

### Step 1: Choose Which Agent to Customize

Example: You want to customize `copy-headlines` for SaaS companies.

### Step 2: Open Agent File

```bash
# Edit the agent carefully
nano ~/agent-girl/server/agents.ts

# Or open in VS Code
code ~/agent-girl/server/agents.ts
```

### Step 3: Find the Agent Definition

Search for the agent in AGENT_REGISTRY. Example:

```typescript
const copy_headlines = {
  name: "copy-headlines",
  description: "...",
  tools: ["Task"],
  prompt: `
    [Full prompt here]
  `
}
```

### Step 4: Find Safe Customization Points

In the prompt, look for these sections to customize:

```
[SAFE] Add industry context here
[SAFE] Add company-specific examples here
[SAFE] Add voice guidelines here
[UNSAFE] Don't change core trigger logic
[SAFE] Add trigger examples specific to your industry
```

### Step 5: Make Your Changes

Example: Customizing copy-headlines for SaaS

**BEFORE:**
```
You are Agent Girl's headline generator, applying 9 psychological triggers...

Example 1: "The $3k copywriter..."
Example 2: "You're not a cheap writer..."
```

**AFTER:**
```
You are Agent Girl's headline generator, applying 9 psychological triggers...
Customized for SaaS copywriting and product launches.

For SaaS, specificity is critical (mention metrics, timeline, audience).
Contrast works well (old way vs new way, problem vs solution, price points).
Curiosity drives clicks on saturated platforms.

Example 1: "The $3k copywriter..." [ORIGINAL - good for all]
Example 2: "You're not a cheap writer..." [ORIGINAL - good for all]

SaaS-Specific Examples:
Example 3 (Contrast): "Your DevOps team spends 20 hours/week on deploys. Ours take 30 minutes."
Example 4 (Specificity): "Reduce CI/CD time from 45 min to 8 min. For 50-500 person teams."
Example 5 (Curiosity): "Why do fast-growing startups adopt this 60% faster than established companies?"
```

### Step 6: Test Your Customization

```bash
# Restart Agent Girl
Ctrl+C
npm run dev
```

**Test in UI:**
1. Select copy-headlines agent
2. Give it a SaaS-related request
3. Check that:
   - It uses SaaS-specific examples
   - Quality still 8.5+/10
   - Customization applied appropriately
   - Maintains original agent behavior

### Step 7: Verify Quality

Run through 7-point quality checklist:
- [ ] Specificity: 8+/10 (SaaS-specific metrics provided)
- [ ] Authenticity: 8+/10 (voice consistent with customization)
- [ ] Clarity: 9+/10 (customization makes it clearer)
- [ ] Alignment: 9+/10 (perfectly aligned to SaaS audience)
- [ ] Impact: 8+/10 (customization improves relevance)
- [ ] Originality: 8+/10 (SaaS examples original)
- [ ] Completeness: 9+/10 (fully customized for SaaS)

**Average must be 8.5+/10**

---

## Common Customizations

### Customization 1: Industry-Specific Agent

**Goal:** Adapt copy-social for legal services copywriting

**Changes:**
1. Add legal industry examples
2. Customize master copywriter applications to legal niche
3. Add legal-specific trigger examples
4. Include legal constraints (compliance, professional)

**Template:**
```
Original Agent
+ Legal-specific examples
+ Compliance notes
= Customized copy-social for legal

Same core logic, legal context added
```

### Customization 2: Company Voice

**Goal:** Make copy-social match your company's voice

**Changes:**
1. Add brand voice guidelines
2. Include brand examples
3. Exclude contradictory elements
4. Add company-specific audience insight

**Template:**
```
Agent
+ "Our voice is X"
+ "Our audience values Y"
+ "Use language Z, avoid language W"
= Branded agent
```

### Customization 3: Audience-Specific Agent

**Goal:** Customize copy-headlines for your specific customer

**Changes:**
1. Add specific audience context
2. Include audience pain points
3. Add audience-specific trigger examples
4. Emphasize most relevant triggers for this audience

**Template:**
```
Agent
+ "[Your customer] is..."
+ "[Their pain] is..."
+ "[Your solution] is..."
= Audience-customized agent
```

### Customization 4: Constraint-Based Agent

**Goal:** Customize agents for platform constraints

**Changes for TikTok:**
- Emphasize 3-second hook requirement
- Add short-form video emphasis
- Include vertical video notes
- Add platform-specific strategy

**Changes for LinkedIn:**
- Add professional tone notes
- Include thought-leadership framing
- Add 150-300 character line break notes
- Emphasize credibility/authority

---

## Advanced: Creating Variant Agents

Instead of modifying original agents, create variants.

### Why Variants?

- Original agents stay production-ready
- Easy to compare approaches
- Can A/B test variants
- Always have fallback

### How to Create Variants

**Step 1: Copy the agent**
```typescript
// Original
const copy_headlines = { ... }

// Variant for SaaS
const copy_headlines_saas = {
  name: "copy-headlines-saas",
  description: "Headline generation specialized for SaaS products",
  tools: ["Task"],
  prompt: `
    [Full prompt with SaaS customization]
  `
}

// Variant for Legal
const copy_headlines_legal = {
  name: "copy-headlines-legal",
  description: "Headline generation specialized for legal services",
  tools: ["Task"],
  prompt: `
    [Full prompt with legal customization]
  `
}
```

**Step 2: Add to AGENT_REGISTRY**
```typescript
AGENT_REGISTRY = {
  ...existing_agents,
  copy_headlines,        // Original
  copy_headlines_saas,   // Variant
  copy_headlines_legal,  // Variant
}
```

**Step 3: Use copy-orchestrator to route**
```
Brief: "I need a SaaS headline"
Orchestrator: "This is SaaS, routing to copy-headlines-saas"

Brief: "I need a legal services headline"
Orchestrator: "This is legal, routing to copy-headlines-legal"
```

---

## Best Practices

### ✅ DO

- ✅ Test extensively before using in production
- ✅ Keep detailed notes of what you changed
- ✅ Create variants instead of modifying originals
- ✅ Maintain the 7-point quality framework
- ✅ Use git to track customizations
- ✅ Document why you customized something
- ✅ Test multiple examples, not just one
- ✅ Compare customized version to original quality

### ❌ DON'T

- ❌ Change core prompt logic
- ❌ Remove quality gate sections
- ❌ Make vague customizations
- ❌ Use customized agents without testing
- ❌ Skip the 7-point quality check
- ❌ Modify agents you haven't read thoroughly
- ❌ Make assumptions about what will work
- ❌ Forget to restart Agent Girl after changes

---

## Customization Examples

### Example 1: SaaS Headlines

**Original** (generic):
```
You generate headlines applying 9 psychological triggers...
Example: "The $3k copywriter and $30k copywriter..."
```

**Customized** (SaaS):
```
You generate headlines for SaaS products, applying 9 psychological triggers...
For SaaS: Metrics are critical (users, speed, cost), competition is fierce (saturation), decision-makers want proof.

SaaS Customization Notes:
- Specificity trigger: Include metrics (X% faster, $Y savings, Z users)
- Contrast trigger: Old way (manual, slow, painful) vs New way (automated, fast, effortless)
- Relevance: B2B SaaS decision-makers (CTOs, VPs, founders) have specific pain points
- Authority: Include case studies, user counts, funded status
- Curiosity: "How do fast-growing companies..." creates intrigue

Example: "Deploys that take 45 minutes drop to 8 minutes. For 50-500 person engineering teams."
Example: "Most teams do CI/CD wrong. Here's how the fast-growing ones do it."
```

### Example 2: Legal Services Headlines

**Original** (generic):
```
You generate headlines applying 9 psychological triggers...
Example: "The $3k copywriter and $30k copywriter..."
```

**Customized** (Legal):
```
You generate headlines for legal services, applying 9 psychological triggers...
Important: Legal industry has compliance constraints. Headlines must be professional and factual.

Legal Customization Notes:
- Specificity trigger: Years of experience, case results (within ethical bounds), client types
- Relevance: Pain points are liability, cost, peace of mind, regulatory compliance
- Authority: Highly valued - credentials, bar association status, case wins matter
- Identity: Business owners, entrepreneurs, executives seeing themselves as needing legal protection
- Contrast: Unprotected vs Protected, risky vs Safe, expensive problem vs Cheap prevention
- Avoid: Exaggeration, unproven claims, competitive attacks on other lawyers

Example: "97% of 5-50 person companies are under-protected. Here's the one step that changes it."
Example: "You wouldn't run your business without insurance. So why run it without proper legal coverage?"
Example: "Most liability issues are preventable. Business owners who know this sleep better."
```

### Example 3: Consultant Headlines

**Customized** (Management Consulting):
```
You generate headlines for B2B consulting services, applying 9 psychological triggers...

Consultant Customization Notes:
- Authority: Emphasize methodology, frameworks, results, client logos
- Specificity: Revenue impact ($X increased, Y% improvement), timeline (6-month transformation)
- Identity: C-suite executives and founders see themselves as strategic leaders
- Contrast: Manual vs Automated, guessing vs Data-driven, struggling vs Thriving
- Relevance: Pain is: growth plateau, cash flow, team alignment, scalability
- Scarcity: Limited engagement slots, specific time window, exclusive framework
- Emotion: Frustration with slow growth, desire for breakthroughs, fear of being left behind

Example: "Your company can 3x revenue in 18 months. Here's how companies like yours are doing it."
Example: "Most scaling breaks at $10M. This framework prevents it."
```

---

## Troubleshooting Customizations

### Issue: Quality dropped after customization

**Solution:**
1. Compare customized to original version
2. Check if you accidentally changed core logic
3. Run 7-point quality evaluation
4. If below 8.5/10, revert and try different approach
5. Test with multiple examples, not just one

### Issue: Agent behaves differently

**Solution:**
1. Did you change the prompt logic?
2. Did you add conflicting instructions?
3. Did you remove tool definitions?
4. Revert to original and add customization more carefully

### Issue: Customization doesn't apply

**Solution:**
1. Did you save the file?
2. Did you restart Agent Girl (`npm run dev`)?
3. Is the customization in the right place in the prompt?
4. Did you add it before the example section?

---

## Documenting Customizations

Create a file documenting your customizations:

```markdown
# Customization Log

## copy-headlines-saas

**Date**: November 12, 2025
**Purpose**: SaaS product headline generation
**Changes**:
- Added SaaS-specific context (metrics-driven, competitive)
- Added metrics-focused examples
- Emphasized specificity and contrast triggers
- Added B2B decision-maker audience notes

**Testing**:
- Tested with 5 SaaS products
- Average quality score: 8.9/10
- Particularly strong on specificity (9.1/10) and relevance (9.0/10)
- Some impact scores lower (8.2/10) - may need revision

**Status**: Ready for production use

---

## copy-social-brand-voice

**Date**: November 12, 2025
**Purpose**: Social copy matching our brand voice
**Changes**:
- Added brand voice guidelines (conversational, direct)
- Removed corporate language examples
- Added company culture references
- Customized master copywriter styles to our voice

**Testing**:
- Team reviewed 10 outputs
- Unanimous: "Sounds like us"
- Quality scores 8.7+/10
- Authenticity score particularly high (9.3/10)

**Status**: Ready for production use
```

---

## When NOT to Customize

Some situations you shouldn't customize:

- ❌ Trying to "fix" a poor quality output (test more, agent works)
- ❌ Changing something you don't understand (read prompt first)
- ❌ Customizing because one output wasn't perfect (natural variation)
- ❌ Trying to add new triggers (framework is proven, don't change)
- ❌ Removing quality gates (they exist for a reason)

---

## Advanced: Building on the Framework

Once comfortable, you can:

1. **Create completely new agents** following the pattern
2. **Combine agent techniques** in new ways
3. **Create industry-specific agent suites**
4. **Build custom routing logic**

See `ADDING_NEW_AGENTS.md` for full guide.

---

## Getting Help

Customization not working?

1. Review this guide again
2. Check INSTALLATION.md (make sure setup correct)
3. Review agent examples in agents/ folder
4. Test without customization first
5. Ask in community channel

---

**Last Updated**: November 2025
**Customization Status**: Safe and Supported
