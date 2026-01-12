# Research Operations Manual

## Document Purpose

This document defines the complete research methodology for evidence-based gourmet research across multiple cities. It serves as the single source of truth for both human researchers and AI agents.

**Language Policy:**
- Primary language: English (all operational procedures, rules, and guidelines)
- Japanese: Used sparingly for clarification, context, or examples only
- No content duplication across languages

---

## Project Scope

### In Scope

**Primary Objective**: Build evidence-based food recommendations for a trip from 2026-09-25 to 2026-10-04.

**Target Cities** (調査対象エリア):
- 伊勢市 (Ise City)
- 松阪市 (Matsusaka City)
- 鳥羽市 (Toba City)
- 志摩市 (Shima City)

**Categories Covered**:
- Restaurants (all cuisine types)
- Cafes (coffee, tea, light meals)
- Dessert shops (sweets, pastries, ice cream)

**Research Deliverables**:
- Scored candidate list with evidence
- Top picks and backup recommendations
- Practical constraints (reservations, hours, closures)
- Exclusion rationale for rejected candidates

### Out of Scope

**Not Researched**:
- Accommodations (already booked)
- Transportation between cities (already booked)
- Non-food activities or attractions
- Shopping (unless food-related)
- Nightlife (bars, clubs) unless food-focused
- Cities outside the four target areas

**Fixed Constraints** (not modifiable by research):
- Travel dates: 2026-09-25 to 2026-10-04
- Previously visited restaurants (reference only): 和田金, 一月家, 豚捨, 一升びん

---

## Agent Roles and Responsibilities

### Research Agent
**Primary function**: Information discovery and evidence collection

**Responsibilities**:
- Search for candidate establishments across multiple sources
- Collect ratings, reviews, and practical information
- Document evidence in structured format
- Record source URLs and access dates
- Flag conflicts or uncertainties in data

**Authority**:
- Add candidates to discovery pipeline
- Request additional sources when needed
- Escalate unclear cases to Verification Agent

**Constraints**:
- Must not fabricate or infer data without clear evidence
- Must cite all sources with URLs
- Must collect minimum 4 sources per candidate (see Evidence Rules)

### Verification Agent
**Primary function**: Data validation and conflict resolution

**Responsibilities**:
- Cross-reference information from multiple sources
- Identify and resolve conflicts in evidence
- Verify practical constraints (hours, reservations, closures)
- Flag outdated or unreliable information
- Validate URL accessibility and accuracy

**Authority**:
- Request additional sources from Research Agent
- Mark evidence as "conflicting" or "uncertain"
- Escalate unresolvable conflicts for human review

**Constraints**:
- Cannot override source data without justification
- Must document all conflict resolution decisions
- Must preserve original conflicting evidence

### Scoring Agent
**Primary function**: Apply standardized scoring rubric

**Responsibilities**:
- Apply 50-point scoring system consistently (see Scoring System)
- Justify each score component with evidence
- Document scoring rationale in notes.md
- Update candidate scores in candidates.md
- Flag edge cases requiring human judgment

**Authority**:
- Assign scores 0-50 based on rubric
- Request additional evidence if insufficient for scoring
- Recommend exclusion for scores below thresholds

**Constraints**:
- Must follow rubric strictly (no subjective adjustments)
- Must justify every score with documented evidence
- Cannot score without minimum evidence requirements met

### Synthesis Agent
**Primary function**: Generate final recommendations

**Responsibilities**:
- Aggregate scored candidates into tiers (Top Picks, Backups)
- Create dining strategy across all recommendations
- Identify gaps in category or geographic coverage
- Generate practical guidance (reservation timing, budget allocation)
- Ensure progressive disclosure in documentation

**Authority**:
- Promote candidates to Top Picks (score ≥35)
- Designate Backups (score 30-34)
- Recommend additional research for underserved categories

**Constraints**:
- Cannot override scores from Scoring Agent
- Must respect score-based tier thresholds
- Must maintain geographic and category balance

### Human Review Agent
**Primary function**: Final approval and strategic decisions

**Responsibilities**:
- Review completion status per city
- Approve or reject recommendations
- Override automated decisions when justified
- Provide strategic direction for research priorities
- Validate compliance with project scope

**Authority**:
- Full override authority on any decision
- Set research priorities and focus areas
- Approve final completion status
- Request re-research or additional candidates

**Constraints**:
- Overrides must be documented with rationale
- Cannot modify historical research data (audit trail)

---

## Quick Start Guide

**For new agents entering this project:**

1. **Understand context**: Read [Project Scope](#project-scope) above
2. **Learn structure**: Review [Repository Structure](#repository-structure) below
3. **Follow workflow**: Execute [Research Workflow](#research-workflow) step-by-step
4. **Apply standards**: Use [Scoring System](#scoring-system) and [Evidence Rules](#evidence-rules)
5. **Check progress**: Verify completion against [Completion Criteria](#completion-criteria)

---

## Repository Structure

### File Organization

Each city under `gourmet/` directory contains exactly five files following the progressive disclosure principle:

```
gourmet/
  [city]/
    overview.md    - City context, strategy, research progress
    candidates.md  - All candidates in structured table format
    notes.md       - Detailed evidence and scoring rationale  
    excluded.md    - Rejected candidates with exclusion reasons
    top-places.md  - Final recommendations and dining strategy
```

**City directories** (use romanized names):
- `iseshi` (伊勢市)
- `matsusakashi` (松阪市)
- `tobashi` (鳥羽市)
- `shimashi` (志摩市)

### File Purposes and Reading Sequence

#### 1. overview.md
**Purpose**: Quick orientation and research strategy  
**Audience**: New researchers, project managers  
**Reading time**: 5 minutes  
**Contains**:
- Travel dates and accommodation info
- City-specific food highlights (e.g., 伊勢うどん, 松阪牛)
- Research strategy and priorities
- Progress checklist (research completion tracking)
- Important constraints (holidays, hours, transportation)

**Update trigger**: Project start, strategy changes, completion milestones

#### 2. candidates.md
**Purpose**: Complete candidate inventory with status and scores  
**Audience**: Researchers scanning all options, comparing scores  
**Reading time**: 10 minutes (table scan)  
**Contains**:
- Structured table with all candidates
- Required columns: name, category, area, type, google_maps_url, status, score, sources, notes
- Brief summary only (details in notes.md)

**Update trigger**: New candidate discovered, status change, score assigned

**Preservation rule**: NEVER delete entries unless duplicate, incorrect, or permanently closed. Use `status: rejected` and document in excluded.md instead.

#### 3. notes.md
**Purpose**: Detailed evidence trail and scoring justification  
**Audience**: Deep researchers, auditors, score validators  
**Reading time**: Variable (by section)  
**Contains**:
- Evidence sections per candidate (sources, ratings, reviews)
- Scoring breakdown with rationale
- Practical information (reservations, queues, hours)
- Source URLs with access dates

**Update trigger**: New evidence collected, score calculated, practical info discovered

#### 4. excluded.md
**Purpose**: Audit trail for rejected candidates  
**Audience**: Auditors, researchers avoiding duplicate work  
**Reading time**: 5-10 minutes  
**Contains**:
- Categorized exclusion reasons
- Brief explanation per excluded place
- Source references supporting exclusion
- Date of exclusion decision

**Update trigger**: Candidate rejected, exclusion reason documented

#### 5. top-places.md
**Purpose**: Actionable final recommendations  
**Audience**: Travelers making reservations, day planners  
**Reading time**: 10-15 minutes  
**Contains**:
- Top Picks (score ≥35) in descending score order
- Backups (score 30-34) in descending score order
- Dining Strategy (timing, reservations, budget, transportation)
- To-Do (trip execution checklist - NOT research completion)

**Update trigger**: Candidate promoted to Top Pick/Backup, strategy finalized, completion

### Progressive Disclosure Principle

**Information flow**: Each file serves a distinct abstraction level.

**Traveler journey**:
```
README.md → [select city] → top-places.md → Make reservations
```

**Quick research scan**:
```
overview.md → candidates.md (table scan) → Identify priorities
```

**Deep evidence review**:
```
candidates.md → notes.md → Validate scores and sources
```

**Exclusion investigation**:
```
excluded.md → [reason] → (Optional) notes.md for details
```

**Key principles**:
- Start with answers, then provide justification
- Link between files (don't duplicate content)
- Keep summary files concise (tables, bullet points)
- Bury detailed evidence in notes.md
- Respect reader's journey and time

**Anti-patterns** (avoid these):
- ❌ Mixing summary table with detailed evidence in candidates.md
- ❌ Duplicating scores across multiple files
- ❌ Hiding final picks deep in notes.md
- ❌ Deleting rejected candidates instead of documenting
- ❌ Creating files outside the five-file structure

---

## Research Workflow

### Workflow Overview

**Six-stage process** from discovery to completion:

```
Stage 0: Initialize    → Create overview.md, set strategy
Stage 1: Discovery     → Collect candidates in candidates.md  
Stage 2: Evidence      → Gather detailed evidence in notes.md
Stage 3: Scoring       → Apply 50-point rubric
Stage 4: Triage        → Accept or reject candidates
Stage 5: Synthesis     → Generate top-places.md
Stage 6: Completion    → Verify and document completion
```

### Stage 0: Initialize City Research

**Objective**: Establish research foundation and strategy

**Actions**:
1. Create `overview.md` with:
   - Travel dates and accommodation info
   - City-specific food highlights (e.g., 伊勢うどん, 松阪牛)
   - Research priorities (cuisine types, special dishes)
   - Progress checklist (initially empty)
   - Known constraints (business hours, holidays, transportation)

2. Gather initial candidate pool using web_search:
   - "best [city cuisine] restaurants [year]" (e.g., "best 伊勢うどん restaurants 2026")
   - "best [category] in [city]" (e.g., "best dessert cafes 志摩市")
   - "[specific dish] restaurants [city]" (e.g., "伊勢海老 restaurants Ise")
   - Focus on recent guides (2024-2026) and local sources

3. Batch similar searches (efficiency):
   - One search: main restaurants by cuisine type
   - One search: casual/local specialties
   - One search: desserts/cafes

**Success criteria**:
- overview.md created with complete sections
- 15-25 initial candidates identified
- Research priorities documented

**Time estimate**: 30 minutes

---

### Stage 1: Discovery and Candidate Collection

**Objective**: Build comprehensive candidate list with basic information

**Actions**:
1. Create `candidates.md` with structured table
2. Add all discovered candidates to table with required fields:
   - `name`: Restaurant/cafe name (prefer original language)
   - `category`: restaurant | cafe | dessert
   - `area`: Neighborhood or district
   - `type`: Cuisine or specialty (e.g., pasta, 伊勢うどん, gelato)
   - `google_maps_url`: Google Maps link (search link acceptable initially)
   - `status`: inbox (all start here)
   - `score`: - (empty initially)
   - `sources`: Brief list (e.g., "食べログ, Google Maps")
   - `notes`: One-line summary (expanded in notes.md later)

3. Prioritize candidates:
   - Mark 3-5 highest-priority candidates for immediate research
   - Consider: local specialties, high ratings, Michelin mentions, 百名店

**Preservation rules**:
- NEVER delete candidates from table
- Acceptable modifications only:
  - Merge duplicates
  - Correct errors
  - Note permanent closures
- Unwanted candidates: Set `status: rejected`, document in excluded.md

**Success criteria**:
- candidates.md table created and populated
- All candidates have `status: inbox`
- Top 3-5 priorities identified

**Time estimate**: 20-30 minutes

---

### Stage 2: Evidence Collection

**Objective**: Gather detailed, multi-source evidence for prioritized candidates

**Actions per candidate**:

1. **Search pattern** (efficient):
   - Single comprehensive query: "[Restaurant Name] [City] 食べログ 予約 口コミ"
   - Often returns Google Maps, 食べログ, and Google口コミ together
   - Extract systematically: ratings, review counts, prices, hours, pros/cons

2. **Create evidence section in notes.md**:
   ```markdown
   ### [Place Name]
   
   **Official**: [website URL or "no official website"]
   
   **Google Maps**: X.X/5 (Y reviews)
   
   **食べログ (Tabelog)**: X.X/5 (Y reviews)
   - [URL]
   - 夜予算/昼予算: [price range]
   - Area ranking: [e.g., "伊勢市 うどん部門 3位"]
   
   **Other ratings**: [Retty, Hot Pepper Gourmet, etc.]
   
   **Guide sources**:
   - [URLs with brief descriptions]
   
   **Google口コミ patterns**:
   - [Summarize recurring themes from Japanese reviews]
   
   **Recurring pros**:
   - [List from multiple sources]
   
   **Recurring cons**:
   - [List from multiple sources]
   
   **Practical**:
   - reservation requirement: [required|recommended|optional|none|unknown]
   - best visiting time: [specific times or "off-peak"]
   - closed days: [day of week or "irregular"]
   - queue: [expected wait time or "none"]
   ```

3. **Update candidates.md**:
   - Change `status` from `inbox` to `researching`
   - Add brief summary to `notes` column (keep concise)
   - Keep `score` empty until Stage 3

**Evidence rules** (see [Evidence Rules](#evidence-rules) for details):
- Minimum 4 sources required: Google Maps + 食べログ + Google口コミ + Guide
- Optional additional sources: Retty, Hot Pepper Gourmet, travel blogs
- Document conflicts clearly
- Mark uncertain information as `unknown`
- Include actual URLs (not placeholders)

**Tabelog ranking importance**:
- Always check score (0-5.0 scale) and area ranking
- 4.0+ = Exceptional (0.07% of restaurants)
- 3.5-3.9 = Excellent
- 3.0-3.4 = Good
- Search: "[City] [cuisine type] 食べログ ランキング"
- Note: Score-based ranking ≠ 百名店 (annual award)

**Success criteria**:
- Evidence section created in notes.md
- Minimum 4 sources collected with URLs
- Practical constraints documented
- Conflicts or uncertainties noted
- candidates.md updated with `status: researching`

**Time estimate**: 15-20 minutes per candidate

---

### Stage 3: Scoring

**Objective**: Apply standardized 50-point rubric consistently

**Actions**:

1. **Score each candidate** using rubric (see [Scoring System](#scoring-system)):
   - Taste/Quality (0-10): Food quality, authenticity, execution
   - Value (0-10): Price vs quality, portion size
   - Convenience (0-10): Location, reservation ease, hours
   - Consistency (0-10): Reliability across reviews/time
   - Risk (0-10): Low risk=10; disappointment likelihood, queue uncertainty

2. **Document scoring in notes.md**:
   ```markdown
   **Score (50-point rubric)**:
   - Taste/Quality: X/10 [justification with evidence]
   - Value: X/10 [justification with evidence]
   - Convenience: X/10 [justification with evidence]
   - Consistency: X/10 [justification with evidence]
   - Risk: X/10 [justification with evidence]
   - **Total**: XX/50
   ```

3. **Update candidates.md**:
   - Enter total score in `score` column
   - Keep `status: researching` (changed in Stage 4)

**Scoring requirements**:
- Every score must be justified from documented evidence
- No subjective adjustments outside rubric
- Document edge cases or difficult judgment calls
- Maintain consistency across all candidates

**Success criteria**:
- All five components scored with justification
- Total score calculated
- Scoring rationale documented in notes.md
- Score added to candidates.md table

**Time estimate**: 5-10 minutes per candidate (after evidence collected)

---

### Stage 4: Triage and Exclusion

**Objective**: Decide candidate fate based on scores and evidence

**Decision rules**:

| Score Range | Status | Action |
|-------------|--------|--------|
| ≥35 | `shortlisted` or `top` | Promote to Top Pick |
| 30-34 | `shortlisted` | Consider as Backup |
| <30 | `rejected` | Exclude with documented reason |

**Hard exclusion triggers** (regardless of score):
- Multi-source evidence of tourist trap
- Repeated hygiene or safety concerns
- Severe service issues across multiple sources

**Exclusion process**:
1. Update candidates.md: Set `status: rejected`
2. Create/update excluded.md:
   - Add to appropriate category section
   - Document exclusion reason with evidence
   - Include source references
   - Note date of decision

3. Preserve candidates.md entry (do NOT delete)

**Exclusion categories** (for excluded.md):
- Low Score (<30)
- Tourist Trap (evidence-based)
- Safety/Hygiene Concerns
- Service Issues
- Practical Constraints (location, hours)
- Not Researched Further (deprioritized)

**Success criteria**:
- All researched candidates triaged
- No `status: researching` remains after triage
- Rejected candidates documented in excluded.md
- Exclusion reasons clearly stated with evidence

**Time estimate**: 5 minutes per candidate

---

### Stage 5: Synthesis and Final Recommendations

**Objective**: Generate actionable recommendation list with strategy

**Actions**:

1. **Create/update top-places.md** with sections:

   **Section 1: Top Picks** (score ≥35)
   - List in descending score order
   - Include for each: name, type, area, score, Google Maps link, Tabelog link, one-line justification, constraints

   **Section 2: Backups** (score 30-34)
   - List in descending score order
   - Same information format as Top Picks

   **Section 3: Dining Strategy**
   - Time planning (lunch/dinner hours, local customs)
   - Reservation strategy (which need booking, how far ahead)
   - Budget allocation (price ranges by category)
   - Transportation (how to reach areas from hotel)

   **Section 4: To-Do** (trip execution checklist)
   - Reservation tasks
   - Information confirmation
   - Day-of preparation
   - Note: This is NOT research completion tracking

2. **Balance recommendations**:
   - Target: 5-10 Top Picks per city
   - Target: 3-5 Backups per city
   - Ensure category balance (casual, special occasion, dessert)
   - Ensure geographic spread across city

3. **Link requirements**:
   - Google Maps: Valid URL (direct link or search link)
   - Tabelog: Valid URL or "no tabelog listing"
   - Test all links before finalization

**Success criteria**:
- top-places.md created with all four sections
- Top Picks and Backups sorted by score
- All required information included per place
- All links valid and tested
- Dining Strategy practical and complete
- Balance across categories and geography

**Time estimate**: 30-45 minutes

---

### Stage 6: Completion and Documentation

**Objective**: Verify completion and update tracking systems

**Actions**:

1. **Verify completion criteria** (see [Completion Criteria](#completion-criteria)):
   - ✅ All candidates triaged (no `status: inbox` in candidates.md)
   - ✅ No pending decisions in excluded.md
   - ✅ top-places.md finalized with all sections
   - ✅ overview.md checklist fully marked `[x]`

2. **Run verification commands** (from PROGRESS.md):
   ```bash
   grep "status: inbox" gourmet/[city]/candidates.md  # Should return nothing
   grep -i "TODO\|pending" gourmet/[city]/excluded.md  # Should return nothing
   grep -E "^## (Top Picks|Backups|Dining Strategy|To-Do)" gourmet/[city]/top-places.md  # Should find all 4
   grep "\- \[ \]" gourmet/[city]/overview.md  # Should return nothing
   ```

3. **Update progress tracking**:
   - Update PROGRESS.md status (⏳ → 📝 → 🔄 → ✅)
   - Sync README.md progress table
   - Update recommendation counts
   - Add completion notes

4. **Document improvements** (if applicable):
   - Add efficiency tips to this document
   - Note common patterns discovered
   - Update workflow if process improved

**Completion status definitions**:
- ⏳ Not Started: No files created yet
- 📝 In Progress: Files exist, research ongoing
- 🔄 Needs Finalization: Research done, needs review/finalization
- ✅ Completed: All criteria met

**Critical distinction - Two checklists**:

| Checklist | Purpose | Location | Completion Rule |
|-----------|---------|----------|----------------|
| **Research Completion** | Track research progress | overview.md | MUST be 100% `[x]` for ✅ |
| **Trip Execution** | Track trip planning | top-places.md To-Do | MAY have `[ ]` when research complete |

**Success criteria**:
- All verification commands pass
- PROGRESS.md and README.md updated
- Status set to ✅ only if all criteria met

**Time estimate**: 10-15 minutes

---

## Evidence Rules

### Minimum Source Requirements

**Every researched candidate must have evidence from at least 4 independent sources:**

1. **Google Maps** (required)
   - Overall rating (X.X/5)
   - Review count
   - Recurring themes from reviews (pros/cons)

2. **食べログ (Tabelog)** (required)
   - Score (0-5.0 scale)
   - Review count
   - Price range (夜予算/昼予算)
   - Area ranking if available

3. **Google口コミ** (required)
   - Japanese-language reviews
   - Local reviewer perspectives
   - Recurring patterns across multiple reviews

4. **Food/Travel Guide** (required - at least one)
   - Michelin Guide
   - Local Japanese food blogs
   - TimeOut Tokyo, VOKKA, Hitosara
   - 百名店 (annual award)
   - Regional tourism sites

**Optional additional sources** (strengthen evidence):
- Retty (レッティ)
- Hot Pepper Gourmet (ホットペッパーグルメ)
- Chinese-language travel blogs (PTT, Dcard) - cite clearly
- Social media aggregates (TikTok, Instagram) - verify authenticity

### Source Quality Standards

**URL requirements**:
- Include actual URLs (not "see website")
- Verify links are accessible
- Note if behind paywall or login
- Document access date for time-sensitive info

**Citation format**:
```markdown
**Source name**: [Brief finding]
- URL: [actual link]
- Accessed: YYYY-MM-DD
```

**Source reliability assessment**:
- Prefer sources with large review counts (100+ reviews)
- Cross-reference claims across 3+ sources
- Flag sources that are outliers
- Note if source is outdated (>2 years old)

### Conflict Handling

**When sources disagree**:

1. **Document the conflict explicitly**:
   ```markdown
   **Conflict noted**: 
   - Source A claims: [X]
   - Source B claims: [Y]
   - Source C claims: [X]
   ```

2. **Resolution strategy**:
   - Majority consensus: Use most common finding
   - Recency: Prefer more recent information
   - Detail: Prefer source with more specific detail
   - Scale: Weight by review count/authority

3. **When unresolvable**:
   - Mark as `unknown` or `conflicting`
   - Document both sides
   - Flag for human review
   - Note in scoring rationale

**Common conflict types**:
- Hours of operation (check official website first)
- Reservation requirements (call restaurant if critical)
- Price ranges (use most recent, note inflation)
- Service quality (look for trend over time)

### Uncertainty Documentation

**Mark information as uncertain when**:
- Only one source provides the information
- Sources conflict without clear resolution
- Information is outdated (>1 year for restaurants)
- Seasonal variation possible

**Uncertainty labels**:
- `unknown`: No reliable source found
- `conflicting`: Sources disagree, no clear resolution
- `unverified`: Single source only, not confirmed
- `seasonal`: May vary by season (note which season)
- `outdated`: Based on old information (note date)

**Example**:
```markdown
**Practical**:
- reservation requirement: required (per Tabelog, unverified on official site)
- best visiting time: conflicting (some say lunch, some say dinner)
- closed days: unknown (no clear information)
- queue: 30-60 min (based on 2024 reviews, may be outdated)
```

### Seasonality Considerations

**Seasonal factors to document**:

1. **Ingredients** (especially seafood):
   - 伊勢海老 (spiny lobster): Peak season October-April
   - 岩牡蠣 (rock oysters): Peak season June-August
   - 的矢かき (Matoya oysters): Year-round but best winter
   - Note: Trip is late September, transitioning seasons

2. **Tourist volume**:
   - Peak season (Golden Week, summer, New Year)
   - Off-peak (January-February, September)
   - Trip timing: Late September = transitional (moderate crowds)

3. **Operating hours/closures**:
   - Summer-only items (赤福氷)
   - Winter-only items (赤福ぜんざい)
   - Monthly specials (朔日餅 - 1st of month only)
   - Irregular closures for holidays

**Documentation requirement**:
```markdown
**Seasonal notes**:
- Best visit season: [season] because [reason]
- Trip timing (Sept 25-Oct 4): [適切/注意が必要/オフシーズン]
- Seasonal considerations: [specific factors]
```

### Data Fabrication Prevention

**Strictly prohibited**:
- ❌ Inventing ratings or review counts
- ❌ Inferring facts not stated in sources
- ❌ Mixing personal opinion with source data
- ❌ Claiming consensus without evidence

**Acceptable synthesis**:
- ✅ Summarizing patterns across multiple reviews
- ✅ Noting common themes (with citation)
- ✅ Calculating averages from multiple sources (show calc)
- ✅ Drawing logical conclusions (clearly marked as inference)

**Boundary examples**:
- ❌ "This restaurant is popular" (subjective without evidence)
- ✅ "High review volume (2000+ on Tabelog) suggests popularity"
- ❌ "Service is excellent" (opinion)
- ✅ "12 of 15 recent reviews mention friendly service"

---

## Scoring System

### Rubric Definition

**Total: 50 points** across five equally-weighted categories.

#### 1. Taste / Quality (0-10 points)

**Intent**: Measure food quality, authenticity, and execution.

**Scoring guidelines**:
- **9-10**: Exceptional. Michelin-starred, 百名店, or Tabelog 4.0+. Consistently praised for outstanding flavors
- **7-8**: Excellent. Tabelog 3.5-3.9, strong reviews, specific dishes highly praised
- **5-6**: Good. Tabelog 3.0-3.4, generally positive, solid execution
- **3-4**: Acceptable. Mixed reviews, some quality concerns
- **0-2**: Poor. Multiple complaints, quality issues

**Evidence required**:
- Tabelog score
- Google Maps rating
- Specific dish mentions from reviews
- Guide recognition (Michelin, 百名店) if any

**Example scoring**:
```
Taste/Quality: 10/10
Evidence: Tabelog 4.00 (top 0.07%), 百名店 3 consecutive years,
reviews consistently praise 備長炭焼き technique
```

#### 2. Value (0-10 points)

**Intent**: Measure price-to-quality ratio and portion adequacy.

**Scoring guidelines**:
- **9-10**: Outstanding value. High quality at low/moderate price. Generous portions
- **7-8**: Good value. Fair pricing for quality delivered
- **5-6**: Acceptable. Slightly expensive but justified by quality
- **3-4**: Poor value. Overpriced for quality
- **0-2**: Very poor value. Significantly overpriced

**Evidence required**:
- Price range from Tabelog (夜予算/昼予算)
- Google Maps price level (¥/¥¥/¥¥¥/¥¥¥¥)
- Review mentions of portions or value
- Comparison to similar establishments

**Price bands** (rough guide for Japanese dining):
- Budget: <¥1,000
- Moderate: ¥1,000-3,000
- Upscale: ¥3,000-10,000
- Fine dining: ¥10,000+

**Example scoring**:
```
Value: 7/10
Evidence: ¥15,000-20,000 per person (fine dining), but exceptional
quality justifies price per multiple reviews
```

#### 3. Convenience (0-10 points)

**Intent**: Measure ease of access, reservation process, and operating hours.

**Scoring guidelines**:
- **9-10**: Highly convenient. Central location, walk-in friendly, long hours, near hotel
- **7-8**: Convenient. Accessible location, easy reservation, reasonable hours
- **5-6**: Moderate. Requires some planning, reservation needed, standard hours
- **3-4**: Inconvenient. Difficult access, complex reservation, limited hours
- **0-2**: Very inconvenient. Remote location, strict requirements, very limited hours

**Factors to consider**:
- Distance from hotel or major sites
- Reservation requirement (none/optional/recommended/required)
- Reservation difficulty (easy/moderate/difficult)
- Operating hours (flexible vs restrictive)
- Transportation access

**Example scoring**:
```
Convenience: 6/10
Evidence: 完全予約制 (reservation required), 18:00 synchronized start
(inflexible), 遅刻厳禁 (no-late policy), but walkable from station
```

#### 4. Consistency (0-10 points)

**Intent**: Measure reliability and stability over time.

**Scoring guidelines**:
- **9-10**: Highly consistent. Long-established, stable high ratings, minimal complaints
- **7-8**: Consistent. Reliable quality, few negative reviews
- **5-6**: Moderately consistent. Some variation noted, generally reliable
- **3-4**: Inconsistent. Mixed experiences, hit-or-miss quality
- **0-2**: Unreliable. Frequent complaints, significant variation

**Evidence required**:
- Rating stability over time (if data available)
- Review count (more reviews = more reliable signal)
- Establishment age/history
- Pattern of complaints (recurring vs isolated)
- 百名店 streak (indicates sustained quality)

**Example scoring**:
```
Consistency: 10/10
Evidence: 百名店 3 consecutive years, Tabelog score stable at 4.0,
4000+ reviews maintain high rating, few service complaints
```

#### 5. Risk (0-10 points)

**Intent**: Measure likelihood of disappointment or problems. **Higher score = lower risk.**

**Scoring guidelines**:
- **9-10**: Very low risk. Reliable, predictable, few ways to go wrong
- **7-8**: Low risk. Generally safe choice, minor uncertainties
- **5-6**: Moderate risk. Some factors that could lead to disappointment
- **3-4**: Higher risk. Significant potential issues
- **0-2**: High risk. Multiple red flags or major concerns

**Risk factors** (reduce score):
- Long unpredictable queues
- Strict cancellation policies
- Service quality complaints
- Tourist trap signals
- Seasonal closures during trip
- Unclear reservation process
- Location difficult to find

**Risk mitigators** (increase score):
- Confirmed reservation possible
- Consistent positive reviews
- Clear operating information
- Backup options nearby

**Example scoring**:
```
Risk: 9/10
Evidence: Reservation required (eliminates queue uncertainty),
strict cancellation policy but ensures quality control,
consistent reviews indicate reliable experience
```

### Tier Definitions

**Based on total score (0-50):**

| Score Range | Tier | Meaning | Action |
|-------------|------|---------|--------|
| 40-50 | Top Pick | Exceptional, highly recommended | Promote to Top Picks, prioritize |
| 35-39 | Top Pick | Very good, solid choice | Promote to Top Picks |
| 30-34 | Backup | Good, acceptable alternative | Promote to Backups |
| 25-29 | Marginal | Borderline, needs justification | Consider rejection |
| 0-24 | Reject | Below standard | Reject with documentation |

**Tier targets per city**:
- **Top Picks**: 5-10 candidates (quality over quantity)
- **Backups**: 3-5 candidates (alternatives if Top Picks unavailable)
- **Total recommendations**: 8-15 per city (avoid overwhelming)

### Scoring Consistency Rules

**To maintain consistency across candidates**:

1. **Score relative to category**:
   - Compare restaurants to restaurants, cafes to cafes
   - Don't penalize casual places for not being fine dining
   - Adjust expectations by price band

2. **Document edge cases**:
   - Note when scoring difficult or borderline
   - Flag for human review if uncertain
   - Explain unusual scores in rationale

3. **Avoid score inflation**:
   - Not every place can be 40+
   - Reserve 9-10 components for truly exceptional
   - A score of 35-38 is still very good

4. **Justify every component**:
   - Every 0-10 score must cite specific evidence
   - No scores without documented rationale
   - Refer to evidence section in notes.md

---

## Decision Rules

### Promotion Thresholds

**Automatic promotion**:
- Score ≥35: Promote to Top Pick
- Score 30-34: Promote to Backup

**Requires justification**:
- Score <30 but promoting anyway (explain why)
- Score ≥35 but not promoting (explain why)

### Exclusion Thresholds

**Automatic exclusion**:
- Score <25: Below quality standard
- Hard exclusion triggers (see below)

**Requires consideration**:
- Score 25-29: Marginal, needs discussion
- Score 30-34 with red flags: May exclude despite score

**Hard exclusion triggers** (override score):
1. **Tourist trap**: Multi-source evidence of targeting tourists with inflated prices/quality
2. **Safety/hygiene**: Multiple complaints about food safety or cleanliness
3. **Service**: Consistent severe service issues (rude staff, frequent errors)
4. **Practical**: Location truly inaccessible or always closed during trip dates

### Human Override Conditions

**Human reviewer may override automated decisions when**:

1. **Strategic considerations**:
   - Need geographic coverage in underserved area
   - Need category diversity (e.g., only dessert place in city)
   - Historical/cultural significance beyond food quality

2. **Context not captured in rubric**:
   - Unique experience worth the risk/inconvenience
   - Once-in-lifetime opportunity (e.g., seasonal specialty)
   - Strong personal recommendation from trusted source

3. **Edge cases**:
   - Conflicting evidence makes scoring difficult
   - New establishment with limited reviews but strong promise
   - Legendary place with declining quality (historical value debate)

**Override documentation requirement**:
```markdown
**Human override**: [Decision made]
**Reason**: [Detailed justification]
**Date**: YYYY-MM-DD
**Reviewer**: [Name/ID]
```

### Documentation Requirements

**Every decision must be documented**:

1. **Candidates promoted to Top Pick/Backup**:
   - Score with breakdown
   - Evidence summary
   - Practical constraints
   - Justification if borderline

2. **Candidates rejected**:
   - Score (if calculated)
   - Exclusion reason category
   - Supporting evidence
   - Entry in excluded.md

3. **Candidates deprioritized** (not researched):
   - Reason for deprioritization
   - Entry in excluded.md under "Not Researched Further"
   - Brief explanation (e.g., "lower priority", "enough alternatives")

4. **Human overrides**:
   - Original score/decision
   - Override decision
   - Detailed justification
   - Date and reviewer

**Traceability requirement**: Every decision must be traceable back to documented evidence or explicit human judgment.

---

## Completion Criteria

### Definition of Done

**A city is marked "✅ Completed" when ALL of the following are met:**

1. **All candidates triaged**:
   - No `status: inbox` entries in candidates.md
   - Every candidate has either a score or rejection reason

2. **No pending decisions**:
   - excluded.md has no "TODO" or "pending review" items
   - All exclusion reasons documented

3. **top-places.md finalized**:
   - Top Picks section complete (score ≥35)
   - Backups section complete (score 30-34)
   - Dining Strategy section complete
   - To-Do section present (trip execution, not research)

4. **overview.md checklist complete**:
   - Research completion checklist fully marked `[x]`
   - Note: This is different from To-Do in top-places.md

### Checklist Distinction

**Two separate checklists with different purposes:**

| Checklist | Purpose | Location | Completion Rule |
|-----------|---------|----------|----------------|
| **Research Completion** | Track research progress | overview.md | MUST be 100% `[x]` for ✅ |
| **Trip Execution** | Track trip planning tasks | top-places.md To-Do | MAY have `[ ]` when research complete |

**Critical**: Only Research Completion checklist determines "✅ Completed" status.

### Verification Commands

**Run these commands to verify completion**:

```bash
# Should return nothing (no inbox entries)
grep "status: inbox" gourmet/[city]/candidates.md

# Should return nothing (no pending decisions)
grep -i "TODO\|pending" gourmet/[city]/excluded.md

# Should find all 4 sections
grep -E "^## (Top Picks|Backups|Dining Strategy|To-Do)" gourmet/[city]/top-places.md

# Should return nothing (no unchecked research items)
grep "\- \[ \]" gourmet/[city]/overview.md
```

**Expected results for completed city**:
- No inbox entries found ✓
- No pending decisions found ✓
- All 4 sections found in top-places.md ✓
- No unchecked items in overview.md ✓

### Status Progression

**Status indicators**:
- ⏳ **Not Started**: No files created yet
- 📝 **In Progress**: Files exist, research ongoing, some candidates still inbox
- 🔄 **Needs Finalization**: Research done, all triaged, needs review/top-places.md completion
- ✅ **Completed**: All verification commands pass

**Progression rules**:
- Only advance status when criteria met
- Can regress if new candidates added or issues found
- Document status changes in PROGRESS.md

---

## Auditability and Maintenance

### Audit Trail Requirements

**Every research action must leave a trace**:

1. **Candidate addition**:
   - Entry in candidates.md with timestamp (in commit)
   - Initial `status: inbox`

2. **Research conducted**:
   - Evidence section in notes.md
   - Source URLs with access dates
   - `status` updated to `researching`

3. **Scoring**:
   - Score breakdown in notes.md
   - Total score in candidates.md
   - Justification for each component

4. **Triage decision**:
   - `status` updated to `shortlisted`, `top`, or `rejected`
   - If rejected: entry in excluded.md with reason
   - If promoted: entry in top-places.md

5. **Changes after initial decision**:
   - Document reason for change
   - Update all affected files
   - Note in commit message

**Preservation rules**:
- ❌ NEVER delete candidates from candidates.md
- ❌ NEVER remove evidence from notes.md
- ❌ NEVER hide exclusion reasons
- ✅ Mark as rejected and document reason instead
- ✅ Preserve historical scores if recalculated (note change)

### Maintenance Procedures

**Regular maintenance tasks**:

1. **Weekly** (during active research):
   - Update PROGRESS.md with current status
   - Sync README.md progress table
   - Review pending inbox items

2. **Per city completion**:
   - Run verification commands
   - Update status to ✅ only if all criteria met
   - Document completion date

3. **Pre-trip** (closer to 2026-09-25):
   - Verify restaurant hours haven't changed
   - Confirm seasonal availability (岩牡蠣, etc.)
   - Update any closed/relocated establishments
   - Mark outdated information

**Version control discipline**:
- Commit after each meaningful unit of work
- Use descriptive commit messages
- Reference issue/task numbers if applicable
- Keep commits focused (one logical change)

### Quality Assurance

**Self-review checklist before marking complete**:

- [ ] All candidates have scores or exclusion reasons
- [ ] Every score has documented justification
- [ ] All sources have working URLs
- [ ] No unsupported claims or fabricated data
- [ ] Conflicts documented and resolved
- [ ] Uncertainty explicitly marked
- [ ] top-places.md has all required sections
- [ ] Dining Strategy is practical and complete
- [ ] All verification commands pass
- [ ] PROGRESS.md and README.md updated

**Peer review focus areas**:
- Score consistency across candidates
- Evidence quality and sufficiency
- Exclusion reason clarity
- Missing categories or geographic gaps
- Practical constraint accuracy

### Continuous Improvement

**Learning capture**:
- Document efficiency improvements in this file
- Note common research patterns
- Record pitfalls to avoid
- Update workflow if process improved

**Feedback incorporation**:
- Track human override patterns
- Adjust scoring if systematic bias found
- Refine rubric if consistently ambiguous
- Update source requirements if gaps identified

---

## Process Improvements (Lessons Learned)

### Efficient Research Tactics

1. **Start with overview.md**: Provides context for all subsequent work
2. **Batch web searches**: Gather 20+ candidates in 3-4 searches
3. **Prioritize ruthlessly**: Research top 3-5 first, expand if needed
4. **Use comprehensive queries**: "[Place] [City] 食べログ 予約 口コミ" yields most info
5. **Document as you go**: Incremental updates prevent information loss

**Time estimates** (for planning):
- Overview + candidate collection: 30 minutes
- Detailed research per place: 15-20 minutes
- Scoring per place: 5-10 minutes
- Synthesis (top-places.md): 30-45 minutes
- **Total per city**: 4-6 hours for 10 candidates

### Pattern Recognition

**Tourist trap signals**:
- Only located near major attractions
- Overly generic positive reviews
- No mention of Japanese locals in reviews
- Price significantly higher than similar places

**Authentic signals**:
- High Tabelog ratings from verified locals
- Mixed tourist/local clientele
- Family-owned, long history
- Specific dishes praised repeatedly
- Reservation difficulty (genuine popularity)

**Red flags**:
- Inconsistent service complaints (>20% of reviews)
- Hygiene issues mentioned multiple times
- Closed unexpectedly/irregular hours
- Conflicting information across sources

**Green flags**:
- Michelin recognition or 百名店 award
- Tabelog 3.8+ with 500+ reviews
- Specific technique or ingredient praised
- Consistent experience across years

### Common Pitfalls

**Avoid these mistakes**:

1. **Research sprawl**: Don't try to research everything at once
2. **Skipping overview.md**: Context is essential for prioritization
3. **Single-source reliance**: Always cross-reference 4+ sources
4. **Ignoring practical constraints**: Reservation policies, closed days, queues matter
5. **Score inflation**: Not everything can be 40+; 35-38 is still excellent
6. **Geographic clustering**: Ensure coverage across different neighborhoods
7. **Category imbalance**: Need mix of casual, special occasion, dessert
8. **Deleting instead of documenting**: Preserve audit trail via excluded.md

### Research Quality Checklist

**Before finalizing any candidate, verify**:

- ✓ Exact rating and review count on Google Maps and Tabelog
- ✓ Patterns from Google口コミ (Japanese reviews)
- ✓ Signature dishes identified
- ✓ Reservation requirements clear
- ✓ Closed days confirmed
- ✓ Expected wait time documented (if no reservation)
- ✓ Price range from Tabelog (夜予算/昼予算)
- ✓ Most common complaints noted
- ✓ Tourist vs local clientele assessed
- ✓ Seasonal considerations documented (for September-October trip)

---

## Documentation Standards

### Language Rules

**Primary language: English**
- All operational procedures
- All rules and guidelines
- All workflow descriptions
- All rubric definitions
- All decision criteria

**Japanese: Supplementary only**
- Short clarifications (e.g., 食べログ = Tabelog)
- Restaurant/dish names (original language)
- Direct quotes from Japanese sources
- Brief contextual notes

**Prohibited**:
- ❌ Duplicating content in both languages
- ❌ Full paragraphs in Japanese when English suffices
- ❌ Using Japanese when English technical term exists

### File Naming Conventions

**Repository-level files**:
- `AGENTS.md`: This file (English)
- `PROGRESS.md`: Research progress tracker (English)
- `README.md`: Project overview (Japanese - traveler-facing)

**City directory names**:
- Use romanized names: `iseshi`, `matsusakashi`, `tobashi`, `shimashi`
- Lowercase, no spaces, no special characters

**City file names** (standardized, no variation):
- `overview.md`
- `candidates.md`
- `notes.md`
- `excluded.md`
- `top-places.md`

### Date and Data Formats

**Dates**: ISO 8601 format (YYYY-MM-DD)
- Example: 2026-09-25

**Unknown information**: Use `unknown` (not "-", "TBD", "N/A", etc.)

**Scores**: Always show as fraction
- Example: 42/50 (not "42" alone)

**URLs**: Full URLs, not shorteners
- Example: `https://tabelog.com/mie/...` (not `bit.ly/...`)

### Markdown Standards

**Headers**: Use ATX style (`#`, `##`, etc.)

**Lists**: 
- Unordered: `-` (not `*` or `+`)
- Ordered: `1.`, `2.`, etc.

**Emphasis**:
- Bold: `**text**`
- Italic: `*text*`
- Code: `` `text` ``

**Links**: Use reference or inline, not automatic
- Inline: `[text](url)`
- Reference: `[text][ref]` with `[ref]: url` below

**Tables**: Use standard Markdown tables with alignment

---

## Appendix: Quick Reference

### Research Workflow Checklist

- [ ] **Stage 0: Initialize**
  - [ ] Create overview.md
  - [ ] Conduct initial web searches
  - [ ] Gather 15-25 candidates
  
- [ ] **Stage 1: Discovery**
  - [ ] Create candidates.md table
  - [ ] Add all candidates with status: inbox
  - [ ] Prioritize top 3-5

- [ ] **Stage 2: Evidence**
  - [ ] Research prioritized candidates
  - [ ] Create notes.md evidence sections
  - [ ] Collect minimum 4 sources per candidate
  - [ ] Update candidates.md status

- [ ] **Stage 3: Scoring**
  - [ ] Apply 50-point rubric
  - [ ] Document scoring in notes.md
  - [ ] Update candidates.md scores

- [ ] **Stage 4: Triage**
  - [ ] Promote candidates ≥30 score
  - [ ] Reject candidates <30 or with red flags
  - [ ] Document exclusions in excluded.md

- [ ] **Stage 5: Synthesis**
  - [ ] Create top-places.md
  - [ ] Organize Top Picks and Backups
  - [ ] Write Dining Strategy
  - [ ] Add To-Do (trip execution)

- [ ] **Stage 6: Completion**
  - [ ] Run verification commands
  - [ ] Update PROGRESS.md
  - [ ] Sync README.md
  - [ ] Mark complete (✅) only if all criteria met

### Essential URLs

- **PROGRESS.md**: Detailed completion criteria and verification commands
- **README.md**: Traveler-facing project overview (Japanese)
- **City directories**: `gourmet/[city]/`

### Key Principles

1. **Evidence-based**: Every decision backed by documented sources
2. **Traceable**: Full audit trail preserved
3. **Comparable**: Standardized scoring across all candidates
4. **Actionable**: Clear recommendations with practical constraints
5. **Maintainable**: Consistent structure and documentation
6. **Progressive disclosure**: Information layered by abstraction level

---

*Document version: 2.0*  
*Last updated: 2026-01-12*  
*Purpose: Single source of truth for gourmet research operations*
