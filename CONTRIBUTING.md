# Contributing & Community Guidelines

**How to Contribute Improvements, Customizations, and New Agents**

---

## Welcome! 👋

This integration kit is built for and by the community. Your improvements, bug reports, and new agent ideas are welcome and valued.

---

## Ways to Contribute

### 1. Report Issues

Found a bug or something doesn't work right?

**Create an issue with:**
- What you tried to do
- What happened instead
- Error messages (if any)
- Your Agent Girl version
- Your environment (OS, Node version)

**Example:**
```
Title: copy-headlines agent not applying all triggers
Description:
- When I request 5 headlines, only 4 are generated
- Other agents working fine
- All other tests pass
- Error: [copy error message if present]
```

### 2. Improve Documentation

Docs unclear? Grammar errors? Missing information?

**You can improve:**
- README (make it clearer)
- INSTALLATION.md (add examples)
- TESTING_PROCEDURES.md (add test cases)
- Any README in subdirectories
- Fix typos anywhere

**How to contribute:**
1. Fork repository
2. Edit file
3. Submit pull request with description
4. We'll review and merge

### 3. Enhance Agents

Want to improve an existing agent?

**You can improve:**
- Prompt wording (make clearer)
- Add new trigger examples
- Better quality gate logic
- Handle edge cases
- Improve error messages

**Guidelines:**
- Don't change core prompt logic
- Maintain 9.1+/10 quality standard
- Test thoroughly before submitting
- Explain your improvement in PR

**Example PR:**
```
Title: copy-headlines - Add more trigger examples
Description:
- Added 3 more curiosity trigger examples
- All examples tested for 8.5+/10 quality
- Maintains quality gate standards
- No breaking changes
```

### 4. Add New Agents

Want to create an agent for a different use case?

**Follow the pattern in `customization/ADDING_NEW_AGENTS.md`**

**What we're looking for:**
- Clear, single-purpose agent
- Consistent with existing quality standards
- Tested thoroughly
- Documentation included
- Real use case examples

**Ideas:**
- Domain-specific research agents
- Niche copywriting agents (legal, medical, B2B tech)
- Language translation agents
- Format conversion agents
- Industry-specific frameworks

### 5. Add Examples

Want to share your integration experience?

**You can contribute:**
- Real-world usage examples
- Before/after quality scores
- Custom modifications and results
- Integration tips and tricks
- Video walkthroughs
- Blog posts or articles

**How to submit:**
1. Create examples/CUSTOM_EXAMPLES.md
2. Add your examples with context
3. Include quality scores if available
4. Include what you learned

### 6. Expand Knowledge Base

Want to add copywriting frameworks or techniques?

**You can add:**
- New master copywriter playbooks
- Industry-specific frameworks
- Trigger combination strategies
- Advanced techniques
- Case studies

**Location:** `knowledge-base/copywriter-techniques/`

**Guidelines:**
- Research-backed or proven in practice
- Clearly explained with examples
- Consistent with existing frameworks
- 500+ words for substantial additions

### 7. Share Improvements

Made a customization that works great?

**Create a PR with:**
- Your improvement
- Why you made it
- How it improves quality
- Real results (scores, metrics)
- Instructions for others

---

## Submission Process

### For Small Changes (Typos, Clarifications)

1. **Edit directly** on GitHub (click pencil icon)
2. **Write clear commit message**
3. **Submit pull request**
4. We'll review and merge quickly

### For Larger Changes (New Content, Agent Improvements)

1. **Fork the repository**
   ```bash
   # On GitHub, click "Fork"
   ```

2. **Clone your fork locally**
   ```bash
   git clone https://github.com/YOUR-USERNAME/agent-girl-copywriting-agents.git
   cd agent-girl-copywriting-agents
   ```

3. **Create a branch**
   ```bash
   git checkout -b improve/your-feature-name
   ```

4. **Make your changes**
   - Edit files
   - Test thoroughly
   - Verify quality

5. **Commit with clear message**
   ```bash
   git commit -m "Add: copy-legal agent for legal copywriting

   - Full system prompt for legal-specific copywriting
   - Tested to 9.1+/10 quality standard
   - Includes legal framework examples
   - Maintains compatibility with orchestrator"
   ```

6. **Push to your fork**
   ```bash
   git push origin improve/your-feature-name
   ```

7. **Create Pull Request**
   - On GitHub, click "New Pull Request"
   - Select your branch
   - Write clear description
   - Submit!

### For New Agents

1. Follow same fork/clone/branch process
2. Create new file in `agents/NEW_AGENT_NAME.md`
3. Follow pattern from existing agents
4. Test thoroughly in your Agent Girl instance
5. Add documentation explaining the agent
6. Include real examples
7. Submit PR with detailed explanation

---

## Quality Standards

When contributing, maintain our quality standards:

### For Agents
- **Minimum quality**: 8.5+/10 on all 7 criteria
- **Tested**: Must work reliably in Agent Girl
- **Documented**: Clear instructions for use
- **Examples**: Real working examples provided

### For Documentation
- **Clear writing**: Accessible to beginners
- **Accurate**: Technically correct
- **Complete**: All necessary context provided
- **Organized**: Proper structure and formatting

### For Customizations
- **Non-breaking**: Existing functionality preserved
- **Reversible**: Can undo if needed
- **Tested**: Works with existing agents
- **Documented**: Explain what changed and why

---

## Community Standards

Please follow these principles:

### Be Respectful
- Assume good intent
- Respond professionally to critique
- Acknowledge others' contributions
- Celebrate community wins

### Be Clear
- Explain your changes well
- Document your thinking
- Ask questions if unclear
- Help others understand

### Be Tested
- Don't submit untested changes
- Run full test suite before submitting
- Include quality scores
- Report any issues you find

### Be Community-Minded
- Your contribution helps others
- Future you will appreciate clear docs
- Community makes it better for all
- Share knowledge generously

---

## Review Process

### For Pull Requests

1. **Automated checks**
   - Files formatted correctly
   - No syntax errors
   - Quality standards maintained

2. **Manual review**
   - Does this add value?
   - Is it technically sound?
   - Does it maintain quality?
   - Is documentation clear?

3. **Discussion**
   - Questions from reviewers
   - Requests for changes
   - Suggestions for improvement
   - Collaborative refinement

4. **Approval & Merge**
   - Once approved
   - We merge to main
   - Thank you for contributing!

### Timeline

- **Small changes**: 2-3 days
- **Medium changes**: 3-5 days
- **New agents**: 5-7 days (more review needed)

---

## Recognition

Contributors are recognized in:
- **README.md** - Contributors section
- **CHANGELOG.md** - Your contribution listed
- **GitHub** - Your profile linked

### Types of Recognition

```markdown
## Contributors

**Agents**
- [Your Name](github.com/yourprofile) - copy-legal agent

**Documentation**
- [Your Name](github.com/yourprofile) - Expanded INSTALLATION.md

**Examples**
- [Your Name](github.com/yourprofile) - B2B SaaS examples

**Bug Fixes**
- [Your Name](github.com/yourprofile) - Fixed copy-headlines trigger logic
```

---

## Ideas for Contribution

### Agents We Need

These would be valuable additions:

1. **copy-legal** - Legal industry copywriting
2. **copy-medical** - Medical/health copywriting
3. **copy-b2b-tech** - B2B technology/SaaS copywriting
4. **copy-email-sequences** - Multi-email campaign creator
5. **copy-funnel** - Sales funnel copywriting
6. **copy-translation** - Translates copy maintaining triggers
7. **copy-ab-test** - Generates A/B variations

### Documentation Improvements

- **Video tutorials** for integration process
- **Domain-specific examples** (SaaS, agencies, etc.)
- **Troubleshooting guide** (common issues)
- **FAQ section**
- **Best practices guide**

### Knowledge Base Additions

- **SEO copywriting framework**
- **E-commerce copywriting framework**
- **B2B copywriting framework**
- **Advanced trigger combinations**
- **Cultural considerations in copywriting**

### Tools & Utilities

- **Quality score calculator** (spreadsheet)
- **Trigger identifier** (copy analyzer)
- **Agent tester** (batch testing tool)
- **Integration validator** (pre-check script)

### Community Feedback

Tell us:
- What's working great?
- What's confusing?
- What would help?
- What would you build?

---

## Contact & Questions

### Before You Contribute

Questions about:
- **Integration help**: Check INSTALLATION.md
- **Testing procedures**: Check TESTING_PROCEDURES.md
- **Customization**: Check CUSTOMIZATION_GUIDE.md
- **Technical details**: Check INTEGRATION_STORY.md

### Still Have Questions?

- **Ask in issues** - Start a discussion
- **Join the community** - Skool community channel
- **Share your work** - Show what you've built

---

## License & Rights

By contributing, you agree:
- Your contribution is free for the community
- Others can build on your work
- You retain credit/attribution
- No commercial restrictions

---

## Thank You! 🙏

Community is what makes this project thrive. Every contribution—big or small—makes it better for everyone.

You're awesome for being part of this.

Let's build amazing agents together! 🚀

---

**Last Updated**: November 2025
**Community Status**: Open and welcoming
