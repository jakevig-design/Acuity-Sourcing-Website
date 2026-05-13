# Acuity Sourcing Website - Claude Code Update Instructions

## Overview
This guide shows how to use Claude Code to make updates to the Acuity Sourcing website. Claude Code allows you to ask for changes in natural language, and Claude will modify the HTML files directly.

## Quick Start

### 1. Open Claude Code
From your terminal:
```bash
cd ~/path/to/acuity-sourcing
claude code
```

This opens Claude Code with your project files. Claude can now see and edit:
- `acuity-homepage.html`
- `acuity-portfolio.html`

### 2. Make Updates via Chat
You can ask Claude to make changes in plain English. Examples below.

---

## Common Update Scenarios

### Update Hero Text
**Ask Claude:**
> Update the hero section headline to: "See the opportunity. Seize the value."

Claude will find the `<section class="hero">` block and update the `<h1>` tag.

### Change a Service Description
**Ask Claude:**
> Update the Advisory service card description. Change it to: "Your organization is scaling software spend and needs someone in the room who understands enterprise vendor playbooks and can negotiate from a position of strength."

Claude will locate the Advisory service card and update the paragraph text.

### Add a New Principle
**Ask Claude:**
> Add a fourth principle to the Three Principles section. Call it "Optionality Matters" with description: "Every platform decision should come with an exit strategy. Lock-in is a risk, not a feature."

Claude will add a new `.principle` div to the grid.

### Update Case Study
**Ask Claude:**
> In the Federal Reserve case study (Fintech and Emerging Technology...), update the Results to show "40%" instead of "30%" for the policy override reduction.

Claude will find the specific case study and update the number.

### Change Brand Colors
**Ask Claude:**
> Update the Navy color from #131F53 to #0F1A3C throughout the site.

Claude will find the CSS variables section and update all color definitions.

### Add New Case Study
**Ask Claude:**
> Add a new case study to the Advisory section. Here's the content:

Then paste in the Problem, Actions, Results, and Pattern. Claude will format it to match the existing case studies.

### Update Footer Information
**Ask Claude:**
> Update the footer to add a phone number: (610) 217-0420. Add it as a link after the email.

Claude will modify the footer section.

### Change Contact Email
**Ask Claude:**
> Replace all instances of jake@acuitysourcing.com with contact@acuitysourcing.com

Claude will find and replace throughout both files.

---

## More Complex Updates

### Restructure Services Section
**Ask Claude:**
> The services section currently has three cards. Let me add a fourth service called "Market Intelligence" for when organizations need competitive pricing benchmarks. Add it to the services grid with appropriate description and link to portfolio.

Claude will add the new card and adjust the grid layout.

### Customize Methodology
**Ask Claude:**
> I want to rename the three methodology phases. Change Phase 1 from "Define what good looks like" to "Establish Requirements and Context". Change Phase 2 from "Make a defensible recommendation" to "Model Scenarios and Decide". Change Phase 3 from "Make the win sustainable" to "Implement Governance and Monitor".

Claude will update all three phase names and descriptions.

### Add Internal Page
**Ask Claude:**
> Create a new page called acuity-about.html. It should have the same header and footer as the existing pages. The main content should explain the 20 years of experience across GE Vernova, BlackRock, Federal Reserve, Moody's, and Macmillan. Use the same brand styling.

Claude will generate the new HTML file with consistent design.

### Modify Styling
**Ask Claude:**
> The service cards currently have a gradient top border. Change them to have a solid teal left border instead, like the problem section.

Claude will update the `.service-card::before` CSS rule.

---

## Workflow: Making Updates Step-by-Step

### Step 1: Open Claude Code
```bash
claude code
```

### Step 2: Ask for Your Update
Be specific about what you want. Examples:

✓ **Good:** "Update the hero headline to 'Enterprise software procurement, done right.' and the subheading to 'You prepare systematically. They scramble to match it.'"

✗ **Not specific enough:** "Make the homepage better"

### Step 3: Review the Changes
Claude will show you the updated code. Read through it to make sure it's correct.

### Step 4: Ask for Refinements
If something isn't quite right:
> That's close, but change "systematically" to "with discipline" instead.

Claude will refine the change.

### Step 5: Test Locally
```bash
# Keep Claude Code open in one terminal
# In another terminal, run:
python3 -m http.server 8000
# Then visit http://localhost:8000
```

### Step 6: Deploy
Once you're happy with changes:
```bash
git add .
git commit -m "Update [description of change]"
git push origin main
# If using Vercel, it auto-deploys
# If using GoDaddy, upload via FTP
```

---

## Example: Full Update Session

Here's what a real update session looks like:

```
You: "I want to update the problem statement. Change it to: 'Enterprise software procurement is broken by design. Vendors extract information, shape requirements, and anchor prices — all before your procurement team walks in the room. By the time they arrive, the negotiation is already lost.'"

Claude: [Updates the problem section HTML]

You: "Good. Now update the Three Principles section. Keep the first two but change the third from 'Right Price, Not Low Price' to 'Timing is Everything' with description: 'Eighteen months of runway transforms a deal. Sixty days ends it. When you start determines what you can achieve.'"

Claude: [Updates the principle]

You: "Actually, let's keep 'Right Price, Not Low Price' but shorten the description to just: 'A 40% discount means you were 40% overcharged. Aim for correct structure from day one, not headline discounts.'"

Claude: [Refines the description]

You: "Perfect. Now let's add a new service card for 'Market Intelligence'. Here's the description: 'You need to understand what comparable organizations pay for equivalent capability, and you need it before the vendor conversation starts. Market benchmarking and competitive pricing intelligence.'"

Claude: [Adds the new service card to the grid]

You: "Great. Let me test this locally... [opens browser, checks site] All looks good. Let's deploy."

You: [Pushes to git, site deploys]
```

---

## Advanced: Creating Multiple Updates at Once

You can ask Claude to make several changes in one request:

**Ask Claude:**
> Make these three updates:
> 1. Change the problem section text to: [your text]
> 2. Update the Advisory service description to: [your text]
> 3. Add a new tag to the first case study: [new tag]

Claude will make all three changes and show you the updated files.

---

## Keeping Track of Changes

### Create a Change Log
Keep a `CHANGELOG.md` in your project:

```markdown
## May 15, 2026
- Updated hero headline and subheading
- Added fourth principle "Optionality Matters"
- Changed service card borders from gradient top to teal left
- Updated problem statement

## May 12, 2026
- Launched website
- Added five case studies
- Configured brand colors and typography
```

Then ask Claude to update it:
> Add today's date and changes to CHANGELOG.md

### Ask Claude to Review Changes
Before deploying:
> Summarize all the changes that have been made to the website since launch.

Claude will scan the files and give you a summary.

---

## Tips for Best Results

### Be Specific About Location
**Better:**
> In the Federal Reserve case study under Results, change "$200M+" to "$250M+"

**Less clear:**
> Update the monetary figure in a case study

### Ask for Styling Changes by Class/Section
**Better:**
> Update the `.service-card` CSS to add `border-radius: 8px` instead of `4px`

**Less clear:**
> Make the cards rounder

### Reference HTML Structure
**Better:**
> In the `<section class="cta">`, update the h2 text to say...

**Less clear:**
> Update the call-to-action

### Ask Claude to Validate
> Are there any broken links in the portfolio page? Check all hrefs in acuity-portfolio.html

Claude will scan and report any issues.

---

## Common Questions

**Q: Can I ask Claude to add images to the website?**
A: Yes, but you'll need to upload image files separately. Ask Claude to add an `<img>` tag with the correct path, then upload the image via FTP/git.

**Q: What if I don't like the change Claude made?**
A: Ask Claude to revert or refine it. You can always say "Change that back to the original" or "Try a different approach."

**Q: Can I create entirely new pages?**
A: Yes. Ask Claude to create a new HTML file (e.g., `acuity-services.html`) with the same header, footer, and styling as the existing pages.

**Q: How do I know if my changes will break anything?**
A: Ask Claude to review. Say: "Check for any broken links or CSS issues after these changes." Claude will scan the files.

**Q: Can I update both files at once?**
A: Yes. Claude can make changes across both `acuity-homepage.html` and `acuity-portfolio.html` in the same request.

---

## Deployment After Updates

### If Using Vercel (Auto-Deploy)
```bash
# After Claude makes changes:
git add acuity-homepage.html acuity-portfolio.html
git commit -m "Update [what changed]"
git push origin main
# Site deploys automatically in ~30 seconds
```

### If Using GoDaddy/FTP
```bash
# After Claude makes changes:
# Open FileZilla or FTP client
# Navigate to public_html
# Upload updated files
# Clear browser cache and verify
```

### Test the Live Site
After deploying, visit your domain and:
- [ ] Check that all links work
- [ ] Verify text displays correctly
- [ ] Test on mobile (resize browser or use phone)
- [ ] Clear cache if you see old version

---

## Emergency: Revert a Change

If something goes wrong:

```bash
# See recent commits
git log --oneline -5

# Revert to previous version
git revert HEAD
git push origin main

# Or go back to specific commit
git checkout [commit-hash] -- acuity-homepage.html
git add acuity-homepage.html
git commit -m "Revert to previous version"
git push origin main
```

Or ask Claude directly:
> Show me the previous version of acuity-homepage.html. The last update broke something.

Claude can help you restore previous content.

---

## Getting Help

**If Claude is confused:**
> Here's the exact HTML section I want to change: [paste the code block]. Update the text inside to: [your new text]

**If you want Claude to explain something:**
> Explain how the service card styling works. Why does it have a `::before` pseudo-element?

**If you want to understand a design decision:**
> Why did we use a gradient top border on the service cards instead of a solid color?

Claude can explain the design and reasoning.

---

## Summary: Quick Command Reference

| Task | Example |
|------|---------|
| Update text | "Change the hero headline to: [text]" |
| Add element | "Add a new principle called [name] with description [text]" |
| Update case study | "In the [case study name], update [field] to [new value]" |
| Change styling | "Update [class name] CSS to [change]" |
| Add new page | "Create a new page called [name].html with [description]" |
| Change color | "Update [color name] from [old hex] to [new hex]" |
| Check for issues | "Are there any broken links in the portfolio?" |
| Deploy | `git add . && git commit -m "message" && git push origin main` |

---

**Last Updated:** May 2026  
**Status:** Ready for Production Use  
**Claude Code Version:** Latest
