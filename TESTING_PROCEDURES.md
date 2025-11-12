# Testing Procedures & Quality Assurance

**Complete Guide to Testing 8 Copywriting Agents After Integration**

---

## Overview

After integration, run these tests to ensure:
- ✅ All agents function correctly
- ✅ Quality gates are working
- ✅ No regressions in existing Agent Girl functionality
- ✅ Agents integrate properly with each other
- ✅ Output quality maintained at 9.1+/10

**Total testing time: 30-45 minutes**

---

## Pre-Testing Checklist

Before starting tests, verify:

- [ ] Agent Girl is running (`npm run dev`)
- [ ] All 8 agents appear in the UI dropdown
- [ ] No error messages in console (F12 in browser)
- [ ] Server terminal shows no errors
- [ ] You have test prompts ready
- [ ] You have backup access if needed

---

## Test Suite 1: Individual Agent Testing (15 minutes)

Test each agent independently to verify core functionality.

### Test 1: copy-orchestrator

**Purpose:** Verify master router works and can coordinate other agents

**Test Prompt:**
```
I need to create a marketing email for a B2B SaaS product.
The product is a project management tool for remote teams.
Target audience: Engineering leads at 10-50 person companies.
Pain point: Current tools require too much setup/training.
Goal: Curiosity-driven hook that makes them want to learn more.

Which agent should I use? Route me to the right specialist.
```

**Expected Behavior:**
- Agent analyzes the brief
- Identifies this is email copywriting
- Routes to copy-orchestrator (master router itself) or copy-social (for email-style copy)
- Suggests using copy-headlines for hook or copy-analysis for positioning

**Quality Check (7-point):**
- Specificity: 8+ (mentions specific tools/audience)
- Authenticity: 8+ (natural language)
- Clarity: 9+ (clear routing decision)
- Alignment: 8+ (understands target pain)
- Impact: 8+ (provides actionable next step)
- Originality: 7+ (reasonable routing logic)
- Completeness: 8+ (explains routing reasoning)

✅ **Pass**: Average 8.0+/10

### Test 2: copy-research

**Purpose:** Verify source validation and reliability scoring

**Test Prompt:**
```
I'm writing copy about AI safety best practices.
I want to research current industry standards.
Can you find sources and score their reliability?
I need 0-100 reliability scores so I only use trustworthy info.
```

**Expected Behavior:**
- Agent searches for sources
- Finds reputable sources (academic, industry leader, government)
- Provides 0-100 reliability scoring
- Explains why each source gets its score
- Recommends sources with 80+ reliability for citing

**Quality Check:**
- Specificity: 8+ (specific reliability scores with reasons)
- Authenticity: 8+ (transparent about source evaluation)
- Clarity: 9+ (easy to understand scoring)
- Alignment: 9+ (directly addresses reliability concern)
- Impact: 8+ (helps make informed copy decisions)
- Originality: 7+ (reasonable scoring methodology)
- Completeness: 8+ (covers multiple sources)

✅ **Pass**: Average 8.0+/10

### Test 3: copy-persona

**Purpose:** Verify psychographic profiling works accurately

**Test Prompt:**
```
Create a detailed psychographic profile for:
- B2B SaaS product targeting engineering leads
- Companies 10-50 people
- Tech-forward but pragmatic
- Frustrated with tool complexity
- Looking for time savings

What are their values, fears, desires, pain points, and aspirations?
Make it detailed and usable for copywriting.
```

**Expected Behavior:**
- Creates detailed persona
- Includes values (efficiency, control, simplicity)
- Identifies fears (more complexity, wasted money)
- Lists desires (less time on admin, more on core work)
- Provides psychological hooks for each element

**Quality Check:**
- Specificity: 9+ (detailed psychological profile)
- Authenticity: 8+ (realistic, not stereotyped)
- Clarity: 9+ (easy to understand persona)
- Alignment: 9+ (matches target audience)
- Impact: 9+ (immediately usable for copywriting)
- Originality: 8+ (nuanced understanding)
- Completeness: 9+ (covers all elements)

✅ **Pass**: Average 8.7+/10

### Test 4: copy-analysis

**Purpose:** Verify copywriter technique extraction works

**Test Prompt:**
```
Analyze this piece of copy for techniques used:

"Everyone has a project management tool.
Most of them are the same.
That's exactly why your team is still drowning in admin work.

Here's what changes: Tools designed for asynchronous teams don't require daily standups.
Your remote engineering leads finally get their time back.

Ready to reclaim 10 hours per week?"

What copywriting techniques and frameworks are at work here?
Break down the hooks, triggers, and persuasion tactics.
```

**Expected Behavior:**
- Identifies pattern interrupt ("most are the same...")
- Calls out contrast ("exactly why...")
- Recognizes specificity ("10 hours per week")
- Names psychological triggers (curiosity, relevance, identity)
- Explains copywriter framework used
- Shows how each element builds persuasion

**Quality Check:**
- Specificity: 9+ (specific techniques named)
- Authenticity: 8+ (recognizes real techniques)
- Clarity: 9+ (explains each element clearly)
- Alignment: 9+ (analyzes requested copy)
- Impact: 8+ (actionable for copywriter)
- Originality: 8+ (insightful breakdown)
- Completeness: 9+ (covers all major elements)

✅ **Pass**: Average 8.6+/10

### Test 5: copy-headlines

**Purpose:** Verify psychological triggers are applied correctly

**Test Prompt:**
```
Generate 5 headlines for a copywriting course on positioning.

Audience: Freelance copywriters stuck at $3-5k projects
Pain: Getting undercut by cheaper writers
Goal: Help them understand positioning over pricing

Use the 9 psychological triggers.
Apply different triggers to each headline.
Score each 0-10 on impact and authenticity.
```

**Expected Behavior:**
- Generates 5 distinct headlines
- Each uses different psychological trigger(s)
- Provides impact and authenticity scores
- Explains which triggers were applied
- Scores should be 8+/10 (quality maintained)

**Example result expected:**
```
Headline 1: "The $3k copywriter and the $30k copywriter write the same stuff..."
- Triggers: Contrast, Curiosity, Specificity
- Impact: 9/10 | Authenticity: 9/10

[... etc for 4 more headlines]
```

**Quality Check:**
- Specificity: 9+ (specific headlines with scores)
- Authenticity: 9+ (natural language)
- Clarity: 9+ (easy to understand)
- Alignment: 9+ (speaks to pain)
- Impact: 9+ (headlines actually stop scroll)
- Originality: 8+ (varied angles)
- Completeness: 9+ (5 headlines as requested)

✅ **Pass**: Average 8.9+/10

### Test 6: copy-social

**Purpose:** Verify 4-style writer with quality gates works

**Test Prompt:**
```
Write social copy promoting a positioning course.
Target: Freelance copywriters
Platform: LinkedIn

Write in 2 different styles:
1. Chief Neefe (contrast-driven, strategic)
2. Gary Halbert (story-driven, specific)

For each, score against:
- Hook power (0-10)
- Authenticity (0-10)
- Engagement potential (0-10)
- Platform fit (0-10)

Apply quality gates. Only accept 8+/10 outputs.
```

**Expected Behavior:**
- Writes two distinct versions
- Chief Neefe version uses contrast
- Gary Halbert version tells story
- Provides scores for each
- Explains why scores are what they are
- Quality gates prevent low-scoring outputs

**Quality Check:**
- Specificity: 9+ (multiple versions with scores)
- Authenticity: 9+ (natural voice in each style)
- Clarity: 9+ (easy to compare)
- Alignment: 9+ (speaks to target)
- Impact: 9+ (both versions stop scroll)
- Originality: 9+ (distinct styles)
- Completeness: 9+ (covers all requests)

✅ **Pass**: Average 8.9+/10

### Test 7: copy-video

**Purpose:** Verify 3-second hook engineering works

**Test Prompt:**
```
Create a TikTok/Reels script for a course on positioning.
Target: Freelance copywriters
Length: 30 seconds
Hook requirement: Must stop scroll in first 3 seconds

Include:
- Visual timeline (when things happen on screen)
- Audio script with natural pacing
- Hook strategy used
- Quality scores for authenticity and hook power

Make it filmable on a phone.
```

**Expected Behavior:**
- Creates visual timeline with seconds marked
- Writes natural-sounding audio script
- Explains the hook strategy
- Provides quality scores
- Script is actually filmable
- First 3 seconds are attention-grabbing

**Quality Check:**
- Specificity: 9+ (timecode breakdowns, real script)
- Authenticity: 9+ (natural speech patterns)
- Clarity: 9+ (easy to understand and film)
- Alignment: 9+ (targets freelancers)
- Impact: 9+ (hook actually stops scroll)
- Originality: 8+ (creative visual approach)
- Completeness: 9+ (everything needed to film)

✅ **Pass**: Average 8.9+/10

### Test 8: copy-review

**Purpose:** Verify quality assurance gate works

**Test Prompt:**
```
Review this piece of copy against the 7-point quality framework:

"Learn positioning. Charge more. Stop competing on price."

Score it on:
1. Specificity (0-10)
2. Authenticity (0-10)
3. Clarity (0-10)
4. Alignment (0-10)
5. Impact (0-10)
6. Originality (0-10)
7. Completeness (0-10)

Provide overall score and recommendation (pass/fail for production use).
```

**Expected Behavior:**
- Scores each criterion independently
- Provides specific feedback for each
- Gives overall score
- Clear recommendation (pass/fail)
- Explains reasoning

**Quality Check:**
- Specificity: 9+ (detailed scoring with reasons)
- Authenticity: 8+ (fair and objective evaluation)
- Clarity: 9+ (easy to understand ratings)
- Alignment: 8+ (criteria clearly applied)
- Impact: 8+ (actionable feedback)
- Originality: 7+ (reasonable evaluation approach)
- Completeness: 9+ (covers all 7 points)

✅ **Pass**: Average 8.4+/10

---

## Test Suite 2: Integration Testing (10 minutes)

Test agents working together.

### Test 1: Orchestrator → Specialist Chain

**Purpose:** Verify routing between agents works

**Test Prompt:**
```
I need help writing a high-ticket offer for my coaching program.
It's positioned at $10k/month for serious entrepreneurs.
The audience is 7-figure business owners looking for growth.
Pain: They know they need coaching but don't trust random coaches.
I need the offer to position confidence and exclusivity.

Help me. What's the first step?
```

**Expected Behavior:**
1. copy-orchestrator analyzes brief
2. Routes to copy-headlines (for positioning hook)
3. copy-headlines provides positioning headline
4. Mentions copy-persona for deeper understanding
5. User can follow up with copy-persona for more detail

**Verification:**
- Routing happens automatically
- Suggested next steps are logical
- Quality maintained in handoffs

✅ **Pass**: Agents coordinate, quality maintained 8+/10

### Test 2: Persona → Analysis → Headlines Pipeline

**Purpose:** Test multi-agent sequence

**Prompt 1 (copy-persona):**
```
Build a psychographic profile for $10k/month coaching clients.
```

**Expected Response:** Detailed persona (price-insensitive, high-trust requirements, etc.)

**Prompt 2 (copy-analysis):**
```
Based on this profile [paste persona], what copywriting techniques
would most persuade this audience?
```

**Expected Response:** Analysis of what works for high-value buyers (authority, scarcity, specificity)

**Prompt 3 (copy-headlines):**
```
Using the persona and recommended techniques, create 5 headlines
for a $10k/month coaching offer.
```

**Expected Response:** Headlines using identified triggers, quality 8.5+/10

✅ **Pass**: Sequential usage works smoothly

---

## Test Suite 3: Regression Testing (10 minutes)

Ensure existing Agent Girl functionality still works.

### Test 1: Existing Agents Still Work

Verify built-in agents are unaffected:

**Test Explore Agent:**
```
Explore the copy-orchestrator.md file in this repo and tell me
what makes it different from other agents.
```

**Expected:** Explore agent works normally

**Test Plan Agent:**
```
Plan out the steps to integrate all 8 copywriting agents.
```

**Expected:** Plan agent works normally

### Test 2: No Performance Degradation

**Before Integration:** Agent Girl loads in ~2 seconds

**After Integration:** Agent Girl still loads in ~2-3 seconds

If significantly slower:
- Check for typos in agent prompts (too long prompts slow startup)
- Verify no syntax errors
- Restart with clean restart

### Test 3: UI Remains Responsive

- Click through agent dropdown (should show all agents)
- Send messages (should get responses quickly)
- Switch between agents (should work smoothly)
- Browser console (should show no red errors)

✅ **Pass**: All UI functions work normally

---

## Quality Score Calculation

For each test, calculate the 7-point quality score:

```
Quality Score = (
  Specificity (0-10) +
  Authenticity (0-10) +
  Clarity (0-10) +
  Alignment (0-10) +
  Impact (0-10) +
  Originality (0-10) +
  Completeness (0-10)
) / 7

Round to one decimal place.
```

### Success Threshold

- **Individual agent tests**: 8.0+/10
- **Integration tests**: 8.0+/10
- **Regression tests**: No failures
- **Overall**: 8.5+/10 average

---

## Test Report Template

Create a test report document:

```markdown
# AGENT INTEGRATION TEST REPORT

Date: [Today's date]
Tester: [Your name]
Status: [PASS / NEEDS WORK / FAILED]

## Individual Agent Tests

### copy-orchestrator
- Quality Score: 8.2/10
- Pass/Fail: ✅ PASS
- Notes: Good routing behavior, clear explanations

### copy-research
- Quality Score: 7.8/10
- Pass/Fail: ⚠️ NEEDS WORK
- Notes: Reliability scores sometimes vague, needs more detail

[... etc for all 8 agents ...]

## Integration Tests

### Orchestrator → Specialist Chain
- Status: ✅ PASS
- Notes: Routing works smoothly

### Persona → Analysis → Headlines
- Status: ✅ PASS
- Notes: Multi-agent sequences work

## Regression Tests

### Existing Agents
- Explore: ✅ PASS
- Plan: ✅ PASS

### UI Performance
- Load time: ~2.5 seconds (acceptable)
- Responsiveness: ✅ Good

### Console Errors
- JavaScript errors: 0
- TypeScript warnings: 0

## Summary

- Total agents tested: 8
- Pass rate: 100% (8/8 agents 8.0+/10)
- Overall quality: 8.7/10
- Ready for production: YES ✅

## Issues Found

[List any issues found during testing]

## Recommendations

[Any recommendations for improvement or customization]
```

---

## Continuous Testing

After initial testing:

**Weekly:**
- Run one agent test to ensure quality maintained
- Spot check outputs for quality regression

**Monthly:**
- Run full test suite
- Document scores and trends
- Identify customization opportunities

**When Customizing:**
- Re-run tests on modified agents
- Ensure quality maintained
- Update documentation

---

## Troubleshooting Tests

If a test fails:

### Agent Returns Error

**Error:** "Agent not found" or "Error running agent"

**Check:**
1. Agent appears in dropdown
2. No TypeScript errors (npm run type-check)
3. Restart Agent Girl (npm run dev)
4. Check server terminal for error messages

### Quality Score Too Low

**Issue:** Agent scores only 7.5/10

**Solutions:**
1. Is prompt copied correctly? (No truncation?)
2. Review agent design in markdown file
3. Check if tools available match what agent expects
4. Consider slight prompt adjustments
5. Run multiple tests (one low score might be anomaly)

### Agents Don't Work Together

**Issue:** Orchestrator doesn't route to other agents

**Check:**
1. All 8 agents successfully added?
2. Does copy-orchestrator have Task tool enabled?
3. Do specialist agents have correct descriptions?
4. Try manual sequential usage instead

---

## Passing Criteria

Testing is complete when:

- [ ] All 8 agents individually score 8.0+/10
- [ ] Integration tests show agents working together
- [ ] No regressions in existing functionality
- [ ] UI responsive and error-free
- [ ] Test report created and documented
- [ ] Overall quality average: 8.5+/10

---

## Next Steps After Passing

Once all tests pass:

1. **Document Results** - Save test report
2. **Create Baseline** - Use scores as baseline for future comparison
3. **Explore Customization** - See CUSTOMIZATION_GUIDE.md
4. **Use in Production** - Integrate agents into your workflow
5. **Contribute Findings** - Share test results with community

---

**Last Updated**: November 2025
**Quality Standard**: 9.1+/10 maintained
**Status**: Production Ready
