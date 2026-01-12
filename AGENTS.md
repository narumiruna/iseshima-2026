# Instructions for Agents

## Main Purpose (Immutable)

- The main purpose of this project is to plan a trip from 2026-09-25 to 2026-10-04, especially focusing on food.
- All flights, trains, and accommodations have already been booked and are FINAL.
- 調査対象エリア：
  - 伊勢市
  - 松阪市
  - 鳥羽市
  - 志摩市
- 過去に訪問したことのあるレストラン（参考情報）：
  - 和田金
  - 一月家
  - 豚捨
  - 一升びん

## Agent Mission

Build and maintain a **high-quality, evidence-based food shortlist** for each city, covering:
- Restaurants
- Cafes
- Dessert shops

All recommendations must be:
- Traceable (sources linked)
- Comparable (shared scoring rubric)
- Auditable (decisions and exclusions recorded)
- Actionable (clear top picks and backups)

---

## Research Completion Standard

For detailed completion criteria, status definitions, and verification checklists, see [PROGRESS.md](PROGRESS.md).

**Quick Reference:**
- A city is marked "✅" when ALL of the following are met:
  1. All candidates triaged (no `status: inbox` in candidates.md)
  2. No pending decisions in excluded.md
  3. top-places.md finalized (Top Picks, Backups, Dining Strategy, To-Do)
  4. overview.md checklist fully checked `[x]`

**Status Indicators:**
- ⏳ Not Started → 📝 In Progress → 🔄 Needs Finalization → ✅ Completed

---

## Required Repository Structure (Per City)

```
gourmet/ - City food research data
  [city]/overview.md - City food strategy and progress
  [city]/candidates.md - Candidate restaurants and ratings
  [city]/top-places.md - Final recommendation list
  [city]/excluded.md - Excluded places and reasons
  [city]/notes.md - Detailed evidence and research notes
```

Each city directory under `gourmet/` (e.g., `iseshi`, `matsusakashi`, `tobashi`, `shimashi`) MUST contain:

- overview.md - City food strategy and progress
- candidates.md - Candidate restaurants and ratings
- top-places.md - Final recommendation list
- excluded.md - Excluded places and reasons
- notes.md - Detailed evidence and research notes

Agents MUST respect this structure and naming.

**All documentation must follow the Progressive Disclosure Principle** (see dedicated section below for details).

---

## Progressive Disclosure Principle

**Progressive disclosure** is a design principle where information is revealed gradually, showing only what's necessary at each stage while providing paths to deeper detail when needed.

### Why This Matters

In this project:
- **Travelers need quick answers** (e.g., "What are the top 3-5 places for dinner?")
- **But decisions require justification** (e.g., "Why did you exclude Restaurant X?")
- **Research depth varies** (quick scan → detailed investigation → deep dive)

Progressive disclosure prevents:
- ❌ Overwhelming users with all details upfront
- ❌ Hiding critical information too deeply
- ❌ Making quick decisions difficult
- ❌ Losing traceability of research rationale

### How We Apply It

#### File Structure (Layered Information)

```
overview.md       ← START HERE: Context, strategy, progress at a glance
    ↓
top-places.md     ← ACTIONABLE: Final recommendations with scores
    ↓
candidates.md     ← COMPLETE: All candidates with scores and status
    ↓
notes.md          ← EVIDENCE: Detailed research evidence and scoring rationale
    ↓
excluded.md       ← REJECTED: What was considered and why it was excluded
```

**Each file serves a distinct purpose**:
- **overview.md**: Quick orientation (5-minute read) - City food strategy and progress
- **top-places.md**: Decision-making (10-minute read, includes dining strategy) - Final recommendation list
- **candidates.md**: Complete research (shows all candidates with scores and status) - Candidate restaurants and ratings
- **notes.md**: Detailed evidence (research trail with sources, scoring rationale) - Detailed evidence and research notes
- **excluded.md**: Audit trail (transparency, prevents re-research) - Excluded places and reasons

#### Within-Document Disclosure

**In candidates.md**:
1. **Quick reference table at top** (name, category, area, type, google_maps_url, status, score) → quick scan
2. **Brief summary in notes column** → high-level overview per place

**In notes.md**:
1. **Detailed evidence sections per place** → full research trail with sources
2. **Scoring rationale** → justification for each score component
3. **Practical information** → reservation, queues, closed days, etc.

**In top-places.md**:
1. **Top Picks** first (35+ scores) → immediate action
2. **Backups** second (30-34 scores) → alternatives if needed
3. **Dining Strategy** → logistics and planning
4. **To-Do items** → execution checklist

**In overview.md**:
1. **Travel info** → immediate context
2. **Food highlights** → city-specific focus
3. **Strategy** → research approach
4. **Progress checklist** → current status

**In excluded.md**:
1. **Exclusion reason categories** → organized by reason type
2. **Brief explanation per place** → why it was excluded
3. **Source references** → evidence for exclusion decision

### Guidelines for Agents

When creating or updating documentation:

1. **Start with the answer, then justify**
   - ✅ "Top Pick: Restaurant X (42/50) - Exceptional pasta, reliable service"
   - ❌ "After reviewing 15 sources and analyzing 200 reviews... Restaurant X"

2. **Use visual hierarchy**
   - Headers, scores, and key facts should stand out
   - Details should be scannable (bullets, short paragraphs)
   - Full evidence goes in expandable sections or separate files

3. **Link, don't duplicate**
   - overview.md references top-places.md
   - top-places.md links to candidates.md for quick scan
   - candidates.md table rows can reference notes.md for detailed evidence
   - Avoid copying the same information into multiple files

4. **Respect the reader's journey**
   - Someone planning their day → starts at top-places.md
   - Someone wanting a quick overview → checks candidates.md table
   - Someone questioning a score → digs into notes.md for evidence
   - Someone auditing research → checks excluded.md

5. **Maintain traceability without overwhelming**
   - Every score must be justifiable (in notes.md)
   - Every top pick must have evidence (sources in notes.md)
   - But candidates.md and top-places.md stay concise with summary info only

### Anti-Patterns to Avoid

- ❌ Putting all research in one massive file
- ❌ Mixing summary tables with detailed evidence in candidates.md
- ❌ Hiding final recommendations deep in notes
- ❌ Forcing readers to read everything to find actionable info
- ❌ Removing audit trails (deleted places, score changes)
- ❌ Creating too many layers (more than 6 files per city)

### Example Flow

**Quick Trip Planning (5 minutes)**:
```
README.md → [select city] → top-places.md → Done
```

**Quick Candidate Scan (10 minutes)**:
```
candidates.md → Scan table with scores and status → Identify priorities
```

**Reservation Planning (15 minutes)**:
```
top-places.md → Check constraints → Make reservations → Update To-Do
```

**Deep Research Review (1 hour)**:
```
overview.md → top-places.md → candidates.md → notes.md → Check all sources → Validate scores
```

**Investigating an Exclusion (5 minutes)**:
```
excluded.md → Find place → Read reason → (Optional: check notes.md for full details)
```

---

## Workflow (Must Follow)

### 0 Initialize City Research

When starting research for a new city:

1. **Create overview.md first** with:
   - Travel dates and accommodation
   - Food highlights specific to the city (e.g., Roman pasta, Viennese schnitzel)
   - Research strategy and priorities
   - Current progress checklist
   - Important notes (business hours, holidays, transportation from hotel)

2. **Use web_search to gather initial candidates**:
   - Search for "best [city cuisine] restaurants [year]"
   - Search for specific dishes (e.g., "best carbonara Rome")
   - Search for "best pizza/gelato/dessert in [city]"
   - Focus on recent guides (2024-2026) and local recommendations

3. **Batch similar searches** to save time:
   - Do one search for restaurants
   - One search for pizza/casual dining
   - One search for desserts/gelato

---

### 1 Discovery — Candidate Collection

- Search broadly for food, coffee, and dessert places in the city.
- Record raw findings in:
  - inbox.md (unstructured, fast capture with quick notes)
  - and/or candidates.md (structured table)

**inbox.md structure recommendation**:
```
## カテゴリー (e.g., すき焼き)
1. **店舗名**
   - 所在地：エリア
   - 特徴：代表的な料理／独自の特徴
   - 注意点：制約事項
   - 情報源：情報源の種類
```

Minimum fields per candidate in candidates.md table:
- name
- category (restaurant | cafe | dessert)
- area / neighborhood
- type (e.g., pasta, steak, espresso, gelato)
- google_maps_url (use search link initially, replace with exact link when researched)
- status: inbox | researching | shortlisted | rejected | top
- sources (brief: e.g., "食べログ, Google Maps, Michelin")
- notes (brief summary)

**Prioritization**: Focus on 3-5 top candidates first, then expand. Don't try to research everything at once.

**⚠️ CRITICAL: Preserving candidates.md Table Entries**

**DO NOT delete or remove entries from the candidates.md summary table** unless absolutely necessary for one of the following reasons:

**Acceptable reasons to modify/remove table entries:**
1. **Duplicate entries**: Same restaurant appears multiple times in table (merge into one entry with combined information)
2. **Incorrect information**: Restaurant name, location, or category is wrong and needs correction
3. **Restaurant permanently closed**: Confirmed closure (must note in excluded.md)
4. **Explicit instruction**: User specifically requests removal

**NEVER remove entries because:**
- ❌ They are not yet researched (keep as `status: inbox`)
- ❌ They seem lower priority (move to excluded.md with reason instead)
- ❌ There are already enough candidates (document decision in excluded.md)
- ❌ You think they won't be needed (let user decide; move to excluded.md if appropriate)

**Correct workflow for unwanted candidates:**
1. Keep entry in candidates.md table with `status: rejected`
2. Add detailed reason to excluded.md under "Not Researched Further" or similar section
3. Explain why it was not researched (e.g., "already have enough recommendations", "lower priority", "location too far")

**Why this matters:**
- Preserves research trail and avoids duplicate work
- Maintains audit trail of all candidates considered
- Prevents accidental loss of potentially valuable options
- Allows user to see full scope of research

**When recovering deleted entries:**
- If entries were accidentally deleted, restore them to the table
- Add detailed research sections if available
- Update excluded.md to remove them from "Not Researched Further" if they are now researched

---

### 2 Evidence Collection — Per Place

For each candidate promoted to research:
- Add a detailed evidence section in `notes.md` (keep it skimmable; link sources).
- Update the candidates.md table row with brief summary in notes column.
- Summarize evidence from multiple independent sources.

**Efficient research pattern**:
1. Use web_search with specific queries: "[Restaurant Name] [City] 食べログ 予約 口コミ"
2. One search often provides Google Maps rating, 食べログ reviews, and Google口コミ together
3. Extract key information systematically
4. Document full evidence in notes.md, update candidates.md table with status and brief summary

**Tabelog Ranking Search**:
- **Always check for Tabelog rankings**: Search for "食べログ百名店 [cuisine type] [city/prefecture]" or "[Restaurant Name] 食べログ百名店"
- **百名店 (Hyakumeiten)**: Tabelog's annual "Top 100" lists by category (e.g., うどん百名店, 海鮮百名店, カフェ百名店)
  - Being listed indicates exceptional quality and local/expert recognition
  - Lists are updated annually, so check for the most recent year
  - Example searches: "食べログ百名店 うどん 三重", "食べログ百名店 海鮮 伊勢"
- **How to use this information**:
  - 百名店 status is a strong positive signal (add points in Taste/Quality and Consistency)
  - Note the ranking year in your evidence (e.g., "2024年百名店")
  - If a restaurant is consistently listed across multiple years, that's an even stronger signal
  - Not being listed doesn't mean it's bad - many excellent places don't make the list

Required source types:
- Google Maps (rating, review count, recurring pros/cons)
- 食べログ (Tabelog) (rating, review count, detailed scoring)
- Google口コミ (Google Reviews in Japanese; summarize patterns from local reviewers)
- One or more reputable food or travel guides (Michelin Guide, local Japanese food blogs, TimeOut Tokyo)

Optional sources:
- Retty (レッティ) - another Japanese restaurant review platform
- Hot Pepper Gourmet (ホットペッパーグルメ)
- PTT / Dcard / Chinese-language travel blogs (cite clearly if used)
- Social media mentions (TikTok, Instagram) if aggregated

Rules:
- Do NOT fabricate facts or reviews
- Clearly distinguish:
  - What sources report (use bullet points with source citations)
  - Your synthesis or inference (clearly marked)
- Include actual URLs in sources section
- Note if information is unavailable (use `unknown`)

**Evidence section template (for notes.md)**:
```
### [Place Name]

**Official**: [website URL or "no official website"]

**Google Maps**: X.X/5 (Y reviews)

**食べログ (Tabelog)**: X.X/5 (Y reviews)
- [URL]
- 夜予算/昼予算: [price range]
- 百名店: [e.g., "2024年うどん百名店" or "not listed"]

**Other ratings**: [Retty, Hot Pepper Gourmet, etc.]

**Guide sources**:
- [URLs with brief description]

**Google口コミ patterns**:
- [Summarize patterns from Japanese Google reviews]

**Recurring pros**:
- [List from multiple sources]

**Recurring cons**:
- [List from multiple sources]

**Practical**:
- reservation requirement: 
- best visiting time: 
- closed days:
- queue:

**Score (50-point rubric)**:
- [breakdown]
```

---

### 3 Scoring — Standard Rubric

Each researched place MUST include a 50-point total score:

- Taste / Quality (0–10): Food quality, authenticity, execution
- Value (0–10): Price vs quality, portion size
- Convenience (0–10): Location, ease of reservation/access, opening hours
- Consistency (0–10): Reliability across reviews, time, visits
- Risk (0–10; 10 = low risk): Likelihood of disappointment, queue uncertainty, service issues

**Scoring guidelines**:
- 40+ = excellent, highly recommended
- 35-39 = very good, solid choice
- 30-34 = good, acceptable backup
- <30 = consider exclusion

Also record:
- reservation requirement (required | recommended | optional | none | unknown)
- best visiting time (specific times or "off-peak", etc.)
- closed days (especially Sunday/Monday)
- queue expectations (if no reservation)

---

### 4 Triage — Exclusion with Reasons

- Do NOT delete entries silently.
- Mark excluded places with:
  - status: rejected
  - a documented reason

Record exclusions in:
- excluded.md (primary location for all exclusion reasons)
- Update candidates.md table with `status: rejected`

Hard exclusion triggers:
- Strong multi-source signals of tourist traps
- Repeated hygiene or safety concerns
- Repeated severe service issues

Soft exclusion trigger:
- Total score < 30 / 50 (justification required)

---

### 5 Final Output — Top Picks

Maintain top-places.md with:
- Top Picks (high-confidence, score 35+)
- Backups (good alternatives, score 30-34)
- Researching (in-progress candidates)

**Organization by score**:
- List in descending score order within each section
- Clearly show total score for each place

Each entry MUST include:
- name
- type
- area
- total score (prominently displayed)
- google maps link
- tabelog link
- one-line justification (why recommended)
- constraints (reservation, queues, closed days, price level)

**Google Maps Link Requirement**:
- Every place in top-places.md MUST have a valid, working Google Maps link
- Links MUST be actual URLs (not placeholders or generic text)
- Acceptable formats:
  - Direct Google Maps links: `https://maps.app.goo.gl/...`
  - Search API links: `https://www.google.com/maps/search/?api=1&query=[Place+Name+City]`
  - Place links: `https://www.google.com/maps/place/[Place+Name]`
- Links MUST be tested/verified to point to the correct location
- Generic placeholders like `[View Map]` without proper URLs are NOT acceptable

**Tabelog Link Requirement**:
- Every place in top-places.md MUST have a valid, working Tabelog (食べログ) link
- Links MUST be actual URLs (not placeholders or generic text)
- Acceptable format:
  - Direct Tabelog links: `https://tabelog.com/[prefecture]/[area]/[area_code]/[restaurant_id]/`
  - Example: `https://tabelog.com/mie/A2403/A240301/24000009/`
- Links MUST be tested/verified to point to the correct restaurant
- If a restaurant is not listed on Tabelog, note as "no tabelog listing" instead of omitting the field

**Additional sections to include**:
- Dining Strategy:
  - Time planning (lunch/dinner hours, local customs)
  - Reservation strategy (which places need booking, how far in advance)
  - Budget allocation (price ranges per category)
  - Transportation from hotel (how to reach different areas)
- To-Do:
  - Confirm closed days
  - Make reservations (with timing)
  - Plan daily dining schedule

---

### 6 Post-Research Updates — Documentation Maintenance

**After completing research for a city, MUST do the following**:

1. **Verify Research Completion Standard** (see [PROGRESS.md](PROGRESS.md)):
   - ✅ All candidates triaged (no `status: inbox` remaining)
   - ✅ No pending decisions in excluded.md
   - ✅ top-places.md finalized with Top Picks and Dining Strategy
   - ✅ overview.md checklist fully marked `[x]`
   - Run the verification commands from PROGRESS.md

2. **Update progress tracking**:
   - Update PROGRESS.md with current status (primary source of truth)
   - Sync README.md progress table to match PROGRESS.md
   - Use accurate status icon based on completion criteria:
     - ⏳ Not Started → 📝 In Progress → 🔄 Needs Finalization → ✅ Completed
   - Only use ✅ when ALL completion criteria are met
   - Update recommendation count
   - Add relevant notes about research completion

3. **Update AGENTS.md if workflow improved**:
   - If you discovered a more efficient research method, document it in "Process Improvements (Lessons Learned)"
   - If you found common patterns or pitfalls, add them to relevant sections
   - Keep the workflow documentation current with actual practices

**Why this matters**:
- PROGRESS.md serves as the project progress dashboard - it must reflect current reality
- README.md provides a quick overview that syncs with PROGRESS.md
- Completion standards ensure consistency across all cities
- AGENTS.md captures institutional knowledge - improvements benefit future research
- Consistent updates prevent confusion and duplicate work

---

## Process Improvements (Lessons Learned)

### Efficient Research Workflow

1. **Start with overview.md** - gives context for all other work
2. **Batch web searches** - do 3-4 searches to gather 20+ candidates quickly
3. **Prioritize ruthlessly** - research top 3-5 candidates first with full detail
4. **Use targeted searches** - "[Place] [City] 食べログ 予約 口コミ" gets most info in one query
5. **Document as you go** - update files incrementally and commit frequently

### Common Patterns to Look For

When researching restaurants:
- **Tourist trap signals**: Only near major attractions, overly positive generic reviews, no Japanese locals mentioned in reviews
- **Authentic signals**: High 食べログ ratings from local reviewers, mixed tourist/local clientele, family-owned, specific dishes praised
- **Red flags**: Inconsistent service complaints, hygiene issues mentioned multiple times, closed unexpectedly
- **Green flags**: Michelin/guide mentions, specific dish recommendations, reservation difficulty (shows popularity), strong 食べログ百名店 ranking

### Time Allocation

For a new city:
- Overview + inbox collection: 30 minutes
- Detailed research per place: 15-20 minutes each
- Target: 5 detailed researches = solid foundation
- Can expand later with medium-priority candidates

### Top-places.md Strategy

- **Aim for 4-6 top picks** per city (enough variety, not overwhelming)
- **Include 2-3 backups** (alternatives if top picks unavailable)
- **Balance categories**: At least one casual option, one special occasion, one dessert/gelato
- **Geographic spread**: Cover different neighborhoods to match daily itinerary

---

## Documentation & Naming Rules

- `AGENTS.md` and `PROGRESS.md` MUST be primarily in English.
- Other documents in this repo MUST be primarily in Japanese.
- Use English for structured fields and keys
- Dates must follow ISO format (YYYY-MM-DD)
- Unknown information must be labeled as `unknown`
- Place filenames MUST follow the format: `<city>-<normalized-place-name>.md`

---

## Quality Bar

- Prefer fewer, higher-confidence picks
- Avoid relying on a single platform
- Preserve traceability at all times
- **Aim for evidence from 4+ sources per place** (Google Maps + 食べログ + Google口コミ + Guide)
- **Every score must be justifiable** from the evidence collected
- **Document uncertainty** - if information conflicts or is unavailable, note it

## Common Pitfalls to Avoid

1. **Don't research everything at once** - focus on top candidates first
2. **Don't skip overview.md** - context is crucial for prioritization
3. **Don't rely on single sources** - cross-reference at least 3-4 sources
4. **Don't forget practical constraints** - reservation policies, closed days, queue times matter
5. **Don't over-optimize scores** - a 35-40 range is realistic for good places; not everything is 45+
6. **Don't neglect geographic distribution** - consider travel time from hotel

## Research Questions Checklist

For each researched place, ensure you can answer:
- ✓ What is the exact rating and review count on Google Maps and 食べログ?
- ✓ What do Google口コミ (Japanese reviews) say about it?
- ✓ What are the signature dishes?
- ✓ Do I need a reservation? How far in advance?
- ✓ When is it closed? (day of week)
- ✓ What is the expected wait time without reservation?
- ✓ What is the approximate price range (食べログ 夜予算/昼予算)?
- ✓ What are the most common complaints?
- ✓ Is it touristy or more local?
