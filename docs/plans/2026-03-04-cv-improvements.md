# CV Improvements Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Restructure CV to showcase hybrid IC/manager value with compelling achievements and clear narrative

**Architecture:** Single unified CV (content/cv/index.md) restructured with new section order, consolidated skills, and impact-focused content. Maintains Hugo frontmatter and PaperMod theme compatibility.

**Tech Stack:** Hugo static site generator, PaperMod theme, Markdown

---

## Task 1: Backup Current CV

**Files:**

- Copy: `content/cv/index.md` → `content/cv/index.md.backup`

**Step 1: Create backup**

```bash
cp content/cv/index.md content/cv/index.md.backup
```

**Step 2: Verify backup exists**

Run: `ls -la content/cv/`
Expected: See both `index.md` and `index.md.backup`

**Step 3: Commit backup**

```bash
git add content/cv/index.md.backup
git commit -m "chore: backup current CV before restructuring"
```

---

## Task 2: Rewrite Frontmatter and Opening

**Files:**

- Modify: `content/cv/index.md:1-21`

**Step 1: Update frontmatter and add professional summary**

Replace lines 1-21 with:

```markdown
---
title: "CV for Morgan Roderick"
hidemeta: true
ShowBreadCrumbs: false
ShowPostNavLinks: false
ShowReadingTime: false
ShowShareButtons: false
ShowRssButtonInSectionTermList: false
---

## Contact

- **Email:** [morgan@roderick.dk](mailto:morgan@roderick.dk)
- **Location:** Berlin, Germany
- **LinkedIn:** [linkedin.com/in/morganroderick](https://linkedin.com/in/morganroderick)
- **GitHub:** [github.com/mroderick](https://github.com/mroderick)
- **Web:** [roderick.dk](https://roderick.dk)

_I prefer email over phone calls for most things._

## Professional Summary

Engineering leader with 25+ years experience building resilient software systems and high-performing teams. Currently leading 15 engineers across Payments at Pleo, with a track record of improving operational maturity and team practices. Equally effective as hands-on technical contributor and people manager—seeking Staff/Principal Engineer or Engineering Manager roles where I can combine technical depth with mentoring and organizational impact.
```

**Step 2: Verify rendering**

Run: `hugo server`
Expected: Site starts at http://localhost:1313
Action: Open http://localhost:1313/cv/ and verify new sections appear

**Step 3: Commit**

```bash
git add content/cv/index.md
git commit -m "feat(cv): add professional summary and streamline contact info"
```

---

## Task 3: Add Current Role Section

**Files:**

- Modify: `content/cv/index.md` (insert after Professional Summary)

**Step 1: Add Current Role section**

Insert after Professional Summary section:

```markdown
## Current Role

**Senior Engineering Manager, Payments Group** | Pleo (Nov 2024 – Present)  
**Engineering Manager, Payments Group** | Pleo (Apr 2022 – Nov 2024)

- **Team Leadership:** Grew and split team into two focused teams, improving delivery velocity and developer experience
- **Operational Excellence:** Reduced incident scope and frequency through systematic improvements in resilience and observability
- **Scale Efficiency:** Supported 3x growth in payments volume with same team size and modest hardware requirements
- **Technical Standards:** Implemented canonical log lines and circuit breaker patterns that are set to become organization-wide standards
```

**Step 2: Verify rendering**

Run: `hugo server` (if not running)
Action: Refresh http://localhost:1313/cv/ and verify Current Role section appears

**Step 3: Commit**

```bash
git add content/cv/index.md
git commit -m "feat(cv): add current role section with impact metrics"
```

---

## Task 4: Add Key Achievements Section

**Files:**

- Modify: `content/cv/index.md` (insert after Current Role)

**Step 1: Add Key Achievements section**

Insert after Current Role section:

```markdown
## Key Achievements

1. **Team Growth & Structure** — Grew and successfully split a team into two focused teams, improving delivery velocity and developer experience while maintaining system coherence

2. **Operational Excellence** — Reduced incident scope and frequency by systematically improving resilience patterns and observability practices at Pleo

3. **Scale Efficiency** — Supported 3x growth in payments volume with same team size and modest hardware requirements through architectural improvements and optimization

4. **Open Source Impact** — Core team member of Sinon.JS, a testing library with wide adoption and over 9M weekly downloads, demonstrating sustained technical leadership and community contribution
```

**Step 2: Verify rendering**

Run: `hugo server` (if not running)
Action: Refresh http://localhost:1313/cv/ and verify Key Achievements section appears

**Step 3: Commit**

```bash
git add content/cv/index.md
git commit -m "feat(cv): add key achievements section highlighting career wins"
```

---

## Task 5: Add Technical Skills Section

**Files:**

- Modify: `content/cv/index.md` (insert after Key Achievements)

**Step 1: Add Technical Skills section**

Insert after Key Achievements section:

```markdown
## Technical Skills & Practices

**Languages & Frameworks**  
JavaScript (expert), Go (learning), Python, Ruby, Node.js, Single Page Applications, Progressive Enhancement

**Architecture & Reliability**  
Distributed systems, microservices, circuit breakers, resilience patterns, observability (logging, metrics, tracing), SLO/SLI implementation

**Practices**  
Test-driven development, refactoring, code craft, pair programming, mentoring, engineering culture building

**Tools & Platforms**  
Git, CI/CD, cloud platforms (AWS/GCP), containerization

**Leadership**  
Team scaling (grew and split teams), DORA metrics improvement, incident reduction, operational maturity programs
```

**Step 2: Verify rendering**

Run: `hugo server` (if not running)
Action: Refresh http://localhost:1313/cv/ and verify Technical Skills section appears

**Step 3: Commit**

```bash
git add content/cv/index.md
git commit -m "feat(cv): add consolidated technical skills section"
```

---

## Task 6: Add Career Highlights Section

**Files:**

- Modify: `content/cv/index.md` (insert after Technical Skills)

**Step 1: Add Career Highlights section**

Insert after Technical Skills section:

```markdown
## Career Highlights

**Senior Engineering Manager** | Pleo (Nov 2024 – Present)  
**Engineering Manager** | Pleo (Apr 2022 – Nov 2024)

**Lead Engineer** | Kalo (Nov 2018 – Jan 2020)

**Senior Software Engineer** | Zalando SE (Jan 2017 – Nov 2018)

**Senior Software Engineer** | Apple - Maps Internal Tools (May 2015 – Nov 2016)

**Senior JavaScript Developer** | Nokia gate5 (Sep 2009 – Oct 2011)

**Independent Software Engineer** | Various clients (2001 – Present)  
Including: Brandwatch, AKQA, Atea, Imagine Easy Solutions, Bunch, and others through agencies 7N, Strand & Donslund, Equal Experts

_Earlier experience: Coop, ZYB, Semler IT, IT-Jobbank, Valtech, Software Innovation (1996 – 2001)_
```

**Step 2: Verify rendering**

Run: `hugo server` (if not running)
Action: Refresh http://localhost:1313/cv/ and verify Career Highlights section appears

**Step 3: Commit**

```bash
git add content/cv/index.md
git commit -m "feat(cv): add career highlights section with key companies"
```

---

## Task 7: Add Community & Open Source Section

**Files:**

- Modify: `content/cv/index.md` (insert after Career Highlights)

**Step 1: Add Community & Open Source section**

Insert after Career Highlights section:

```markdown
## Community & Open Source

**Open Source**

- **Sinon.JS** — Core team member, testing library with 9M+ weekly downloads
- Active contributor to JavaScript testing ecosystem

**Community Leadership**

- **codebar Berlin** — Volunteer coach and chapter organizer
- **CoderDojo Berlin** — Volunteer mentor for young programmers
- **CopenhagenJS** — Founder and organizer (18 months)
- **Conference Speaker** — Front Trends 2010, Reject.JS 2010
- **Meetup Speaker** — BerlinJS, CopenhagenJS, AsyncJS

**Volunteering**

- **Homeless Veggie Dinner Berlin** — Volunteer cook (~10 years)
```

**Step 2: Verify rendering**

Run: `hugo server` (if not running)
Action: Refresh http://localhost:1313/cv/ and verify Community section appears

**Step 3: Commit**

```bash
git add content/cv/index.md
git commit -m "feat(cv): add community and open source section"
```

---

## Task 8: Add Education and Final Sections

**Files:**

- Modify: `content/cv/index.md` (insert after Community)

**Step 1: Add Education, Languages, and References sections**

Insert after Community section:

```markdown
## Education

- **Datamatiker** (AP Degree in Computer Science) | Aarhus Business College (1996 – 1998)
- Object Oriented Development | Datanom (1999)
- Matematisk studenter eksamen | Thisted Gymnasium (1990 – 1993)

## Languages

Danish (Fluent), English (Fluent), Swedish (Some), German (~B1)

## References & Links

- **LinkedIn:** [linkedin.com/in/morganroderick](https://linkedin.com/in/morganroderick)
- **GitHub:** [github.com/mroderick](https://github.com/mroderick)
- **Website:** [roderick.dk](https://roderick.dk)
- Recommendations available on LinkedIn
```

**Step 2: Verify rendering**

Run: `hugo server` (if not running)
Action: Refresh http://localhost:1313/cv/ and verify all new sections appear

**Step 3: Commit**

```bash
git add content/cv/index.md
git commit -m "feat(cv): add education, languages, and references sections"
```

---

## Task 9: Remove Old Content

**Files:**

- Modify: `content/cv/index.md` (remove old sections)

**Step 1: Remove obsolete sections**

Remove these sections from the original CV:

- The old "Summary" section (replaced by Professional Summary)
- The old "Current role" section (replaced by new Current Role)
- The "Experience" → "Agents" section
- The "Experience" → "Employers/clients (selection)" section
- The old "Recommendations" section (consolidated into References)
- The old "Profiles" section (consolidated into Contact and References)
- The old "Spoken Languages" section (replaced by Languages)
- The old "Education and certifications" section (replaced by Education)
- The old "Community work" section (replaced by Community & Open Source)
- All the reference link definitions at the bottom (lines 116-163)

**Step 2: Verify rendering**

Run: `hugo server` (if not running)
Action: Refresh http://localhost:1313/cv/ and verify no duplicate sections

**Step 3: Commit**

```bash
git add content/cv/index.md
git commit -m "refactor(cv): remove obsolete sections and reference links"
```

---

## Task 10: Final Verification

**Files:**

- Verify: `content/cv/index.md`

**Step 1: Verify file structure**

Run: `cat content/cv/index.md`
Expected: See clean file with all new sections in order:

- Frontmatter
- Contact
- Professional Summary
- Current Role
- Key Achievements
- Technical Skills & Practices
- Career Highlights
- Community & Open Source
- Education
- Languages
- References & Links

**Step 2: Test Hugo build**

Run: `hugo`
Expected: Site builds successfully to `public/` directory

**Step 3: Verify rendered output**

Run: `hugo server`
Action: Open http://localhost:1313/cv/ and verify:

- Professional Summary visible in first screen
- Key Achievements easy to scan
- Skills consolidated
- Career progression clear
- No broken links or formatting issues

**Step 4: Mobile test**

Action: Resize browser to mobile width and verify readability

**Step 5: Final commit**

```bash
git add content/cv/index.md
git commit -m "feat(cv): complete CV restructuring with hybrid IC/manager positioning"
```

---

## Task 11: Clean Up Backup

**Files:**

- Remove: `content/cv/index.md.backup`

**Step 1: Remove backup file**

```bash
git rm content/cv/index.md.backup
```

**Step 2: Commit cleanup**

```bash
git commit -m "chore: remove CV backup file"
```

---

## Verification Commands

After all tasks complete:

```bash
# Verify Hugo builds
hugo

# Verify development server works
hugo server

# Check git status
git status

# View commit history
git log --oneline -15
```

## Success Criteria

- CV clearly positions Morgan as hybrid IC/manager ✓
- Key achievements visible within first 10 seconds ✓
- Career progression easy to understand ✓
- Skills consolidated and scannable ✓
- Compelling for both Staff/Principal and EM roles ✓
- Hugo builds successfully ✓
- Mobile-friendly formatting ✓
- Clean git history with logical commits ✓
