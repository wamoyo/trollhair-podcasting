# Troll Hair Podcast - Customer Discovery System

This podcast serves as a customer discovery tool for Troll Hair (carbon nanotube manufacturing). Guests should be potential customers OR well-networked with target customers who can make referrals.

---

## Pipeline Overview

```
PROSPECTING
┌─────────────────────────────────────────────────────┐
│ 1. Search via matrix → identify prospects           │
│ 2. User approves/rejects                            │
│ 3. Deep research + draft outreach                   │
│    ↓ (user sends manually)                          │
└─────────────────────────────────────────────────────┘

BOOKING
┌─────────────────────────────────────────────────────┐
│ 4. They accept → user pastes their response         │
│ 5. Prep user for the 30-min prep call               │
└─────────────────────────────────────────────────────┘

PREP CALL
┌─────────────────────────────────────────────────────┐
│ 6. User runs prep call → drops transcript file      │
│ 7. Generate questions/plan for recording            │
│ 8. User vets, then records podcast                  │
└─────────────────────────────────────────────────────┘

POST-PRODUCTION
┌─────────────────────────────────────────────────────┐
│ 9. User drops transcript + impressions              │
│ 10. Generate episode page code                      │
│ 11. Create clip list with timestamps for editor     │
└─────────────────────────────────────────────────────┘

FOLLOW-UP
┌─────────────────────────────────────────────────────┐
│ 12. Add to CRM + nurture activities                 │
│ 13. Thank you package to guest (TBD)                │
└─────────────────────────────────────────────────────┘
```

---

## Status Flow

```
identified → approved → researched → outreach_sent →
accepted → prepped → recorded → published → nurturing
         ↘ declined (archive)
```

### Status Definitions

| Status | Meaning |
|--------|---------|
| `identified` | Found in search, basic profile captured |
| `approved` | User said yes, ready for deep research |
| `researched` | Deep dive done, outreach message drafted |
| `outreach_sent` | Message sent (manually by user) |
| `accepted` | They responded positively |
| `declined` | They said no or ignored (archived) |
| `prepped` | Prep call completed, questions generated |
| `recorded` | Podcast recorded, transcript received |
| `published` | Episode page generated, clips identified |
| `nurturing` | Added to CRM with follow-up activities |

---

## Directory Structure

```
/Troll Hair/Podcasting/
├── CLAUDE.md                    # This file
├── .gitignore
│
├── prospects/
│   ├── pipeline.json            # Master list: name, status, slug
│   ├── search-matrix.json       # Search combinations (TBD)
│   ├── search-history.json      # Completed searches log
│   └── [slug]/                  # One folder per prospect
│       ├── profile.md           # Basic info from search
│       ├── deep-dive.md         # Deep research (approved ones)
│       └── outreach.md          # Draft outreach message
│
├── episodes/
│   └── [slug]/
│       ├── acceptance.md        # Their response when they accept
│       ├── prep-notes.md        # Prep for the prep call
│       ├── prep-transcript.md   # User drops this file
│       ├── questions.md         # Generated interview plan
│       ├── transcript.md        # User drops this file
│       ├── impressions.md       # User's notes post-recording
│       ├── clips.md             # Timestamped clip suggestions
│       └── page.pug             # Generated episode page
│
├── templates/
│   ├── outreach.md              # Outreach message template
│   └── episode-page.pug         # Website page template (TBD)
│
└── viewer/                      # Optional Deno web app (TBD)
    └── server.ts
```

---

## Workflow Details

### Step 1: Search & Identify Prospects

Use `search-matrix.json` to systematically find prospects. For each search:
1. Run web search (LinkedIn, Google, industry sites)
2. Identify potential guests
3. Create `prospects/[slug]/profile.md` with basic info
4. Add entry to `pipeline.json` with status `identified`
5. Log search in `search-history.json`

### Step 2: User Approval

Present identified prospects to user. User says yes/no.
- If yes: update status to `approved`
- If no: update status to `declined`

### Step 3: Deep Research & Outreach Draft

For approved prospects:
1. Conduct deep research
2. Create `prospects/[slug]/deep-dive.md`
3. Draft personalized outreach in `prospects/[slug]/outreach.md`
4. Update status to `researched`

User reviews, edits if needed, sends manually.
Update status to `outreach_sent`.

### Step 4: Handle Acceptance

When user reports acceptance:
1. Create `episodes/[slug]/` directory
2. Save their response in `episodes/[slug]/acceptance.md`
3. Update status to `accepted`

### Step 5: Prep Call Preparation

Create `episodes/[slug]/prep-notes.md` with:
- Key topics to explore
- Questions about their business/role
- Customer discovery angles to probe
- Background context for user

### Step 6: Receive Prep Transcript

User runs prep call and drops transcript at:
`episodes/[slug]/prep-transcript.md`

User tells Claude when transcript is ready.

### Step 7: Generate Interview Plan

Analyze prep transcript and create `episodes/[slug]/questions.md`:
- Intro script
- Main questions (in logical flow)
- Follow-up prompts
- Customer discovery questions woven in naturally

User vets and approves.

### Step 8: Recording

User records podcast, drops transcript at:
`episodes/[slug]/transcript.md`

User also provides impressions in `episodes/[slug]/impressions.md`.
Update status to `recorded`.

### Step 9-11: Post-Production

1. Generate `episodes/[slug]/page.pug` from template
2. Create `episodes/[slug]/clips.md` with:
   - Timestamp ranges
   - Suggested titles
   - Why each clip is compelling
3. Update status to `published`

### Step 12: CRM Integration

Add prospect to Troll Hair CRM (when available) with:
- Contact info
- Company details
- Nurture follow-up activities

### Step 13: Thank You

TBD - Thank you package for guests.

---

## File Formats

### pipeline.json

```json
{
  "prospects": [
    {
      "name": "Jane Smith",
      "slug": "[slug]",
      "company": "Aerospace Corp",
      "status": "identified",
      "date_added": "2025-01-15",
      "last_updated": "2025-01-15"
    }
  ],
  "stats": {
    "total": 0,
    "by_status": {
      "identified": 0,
      "approved": 0,
      "researched": 0,
      "outreach_sent": 0,
      "accepted": 0,
      "declined": 0,
      "prepped": 0,
      "recorded": 0,
      "published": 0,
      "nurturing": 0
    }
  }
}
```

### search-history.json

```json
{
  "searches": [
    {
      "query": "...",
      "date": "2025-01-15",
      "prospects_found": 3,
      "notes": "..."
    }
  ],
  "stats": {
    "total_searches": 0,
    "total_prospects_found": 0
  }
}
```

### profile.md (Basic)

```markdown
# [Name]

**Company**:
**Title**:
**Location**:
**LinkedIn**:
**Email**: (if found)

## Why They're a Fit

[Brief notes on why they could be a customer or connector]

## Source

[How they were found - which search query]
```

### deep-dive.md

```markdown
# [Name] - Deep Dive

## Background
[Career history, education, notable achievements]

## Current Role
[What they do, company details, responsibilities]

## Company Details
[Size, industry, products, potential CNT use cases]

## Network & Influence
[Who they know, speaking engagements, publications]

## Customer Discovery Angles
[Questions to ask, pain points to probe, use cases to explore]

## Podcast Topics
[What would make a compelling episode]
```

### outreach.md

```markdown
# Outreach Draft for [Name]

## Email Version

**Subject**: [subject line]

[body]

## LinkedIn Version

[shorter version for LinkedIn message]

## Notes

[any personalization notes or timing considerations]
```

---

## Search Matrix (TBD)

To be refined based on:
- Target industries (aerospace, automotive, electronics, etc.)
- Target roles (R&D directors, materials engineers, product managers)
- Connector types (industry associations, professors, consultants)
- Geographic focus

---

## Coding Standards

Follow conventions from global CLAUDE.md:
- Use `var`/`let`, no `const`
- Regular functions for multi-line, arrows only for single-line returns
- Space between function name and opening parenthesis
- No semicolons except where required
- Pure functions with documented inputs/outputs
- Comments describing each function's purpose
