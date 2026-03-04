# CV Improvements Design

## Context

Actively job hunting for Staff/Principal Engineer or Engineering Manager roles. Current CV lacks compelling content, clear structure, and strong career narrative despite 25+ years of experience.

**Primary differentiator:** Hybrid IC/Manager versatility - can code, lead teams, mentor, and grow organizations.

**Problems with current CV:**

- Content not compelling enough
- Poor organization (hard to scan)
- Mixed messaging about management vs IC work
- Achievements buried in narrative
- Skills scattered throughout

## Approach

**Chosen: Hybrid Unified CV**

Single CV that authentically showcases both IC and management capabilities. This appeals to modern companies that blur IC/manager boundaries and represents the true value proposition.

**Alternatives rejected:**

- Two separate CVs: Undersells hybrid value, misses crossover roles
- Modular CV: Decision fatigue, maintenance overhead

## Design

### New Section Structure

1. **Contact** (minimal - no phone in header)
2. **Professional Summary** (NEW - 3-4 lines, frames narrative immediately)
3. **Current Role** (Pleo - detailed, impact-focused)
4. **Key Achievements** (NEW - 4 cross-career highlights)
5. **Technical Skills & Practices** (consolidated)
6. **Career Highlights** (streamlined, key companies)
7. **Community & Open Source**
8. **Education**
9. **Languages**
10. **References & Links** (moved to end)

### Section Details

#### Professional Summary

Engineering leader with 25+ years experience building resilient software systems and high-performing teams. Currently leading 15 engineers across Payments at Pleo, with a track record of improving operational maturity and team practices. Equally effective as hands-on technical contributor and people manager - seeking Staff/Principal Engineer or Engineering Manager roles where I can combine technical depth with mentoring and organizational impact.

#### Current Role - Pleo

**Senior Engineering Manager, Payments Group | Pleo** (Nov 2024 – Present)
**Engineering Manager, Payments Group | Pleo** (Apr 2022 – Nov 2024)

- **Team Leadership:** Grew and split team into two focused teams, improving delivery velocity and developer experience
- **Operational Excellence:** Reduced incident scope and frequency through systematic improvements in resilience and observability
- **Scale Efficiency:** Supported 3x growth in payments volume with same team size and modest hardware requirements
- **Technical Standards:** Implemented canonical log lines and circuit breaker patterns that are set to become organization-wide standards

#### Key Achievements

1. **Team Growth & Structure** - Grew and successfully split a team into two focused teams, improving delivery velocity and developer experience while maintaining system coherence

2. **Operational Excellence** - Reduced incident scope and frequency by systematically improving resilience patterns and observability practices at Pleo

3. **Scale Efficiency** - Supported 3x growth in payments volume with same team size and modest hardware requirements through architectural improvements and optimization

4. **Open Source Impact** - Core team member of Sinon.JS, a testing library with wide adoption and over 9M weekly downloads, demonstrating sustained technical leadership and community contribution

#### Technical Skills & Practices

**Languages & Frameworks:**

- JavaScript (expert), Go (learning), Python, Ruby
- Node.js, Single Page Applications, Progressive Enhancement

**Architecture & Reliability:**

- Distributed systems, microservices, circuit breakers, resilience patterns
- Observability (logging, metrics, tracing), SLO/SLI implementation

**Practices:**

- Test-driven development, refactoring, code craft
- Pair programming, mentoring, engineering culture building

**Tools & Platforms:**

- Git, CI/CD, cloud platforms (AWS/GCP), containerization

**Leadership:**

- Team scaling (grew and split teams), DORA metrics improvement
- Incident reduction, operational maturity programs

#### Career Highlights

**Senior Engineering Manager** | Pleo (Nov 2024 – Present)
**Engineering Manager** | Pleo (Apr 2022 – Nov 2024)

**Lead Engineer** | Kalo (Nov 2018 – Jan 2020)

**Senior Software Engineer** | Zalando SE (Jan 2017 – Nov 2018)

**Senior Software Engineer** | Apple - Maps Internal Tools (May 2015 – Nov 2016)

**Senior JavaScript Developer** | Nokia gate5 (Sep 2009 – Oct 2011)

**Independent Software Engineer** | Various clients (2001 – Present)
Including: Brandwatch, AKQA, Atea, Imagine Easy Solutions, Bunch, and others through agencies 7N, Strand & Donslund, Equal Experts

_Earlier experience: Coop, ZYB, Semler IT, IT-Jobbank, Valtech, Software Innovation (1996 – 2001)_

#### Community & Open Source

**Open Source:**

- **Sinon.JS** - Core team member, testing library with 9M+ weekly downloads
- Active contributor to JavaScript testing ecosystem

**Community Leadership:**

- **codebar Berlin** - Volunteer coach and chapter organizer
- **CoderDojo Berlin** - Volunteer mentor for young programmers
- **CopenhagenJS** - Founder and organizer (18 months)
- **Conference Speaker** - Front Trends 2010, Reject.JS 2010
- **Meetup Speaker** - BerlinJS, CopenhagenJS, AsyncJS

**Volunteering:**

- **Homeless Veggie Dinner Berlin** - Volunteer cook (~10 years)

#### Education

- **Datamatiker** (AP Degree in Computer Science) | Aarhus Business College (1996 – 1998)
- Object Oriented Development | Datanom (1999)
- Matematisk studenter eksamen | Thisted Gymnasium (1990 – 1993)

#### Languages

Danish (Fluent), English (Fluent), Swedish (Some), German (~B1)

#### References & Links

- LinkedIn: linkedin.com/in/morganroderick
- GitHub: github.com/mroderick
- Website: roderick.dk
- Recommendations available on LinkedIn

### Content Removals

1. **Phone number** from header (keep email preference note)
2. **Book list** from Summary (saves space, less relevant)
3. **Detailed employer link reference list** at bottom (redundant with LinkedIn)
4. **"Agents" section** (confusing, adds no value)

### Visual Hierarchy

Use PaperMod markdown formatting:

- Bold for role titles
- Clear section breaks with headers
- Bullet points for scanability
- Consistent date formatting

## Implementation Notes

- Maintain Hugo frontmatter (same PaperMod settings)
- Test rendering with `hugo server`
- Ensure mobile-friendly formatting
- Keep markdown clean and readable in source

## Success Criteria

- CV clearly positions Morgan as hybrid IC/manager
- Key achievements visible within first 10 seconds of scanning
- Career progression easy to understand
- Skills consolidated and scannable
- Compelling for both Staff/Principal and EM roles
