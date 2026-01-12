# Agent Operational Constraints

## SECTION 1: IMMUTABLE CONSTRAINTS

These constraints MUST NOT be violated under any circumstances. Agents MUST halt and request clarification if any action would violate these constraints.

### 1.1 Project Scope (IMMUTABLE)

**Travel Dates**: 2026-09-25 to 2026-10-04
**Trip Type**: Food-focused research trip
**Target Areas**: 伊勢市, 松阪市, 鳥羽市, 志摩市

**IMMUTABLE FACT**: All flights, trains, and accommodations are FINAL and CANNOT be changed.

**Reference Data** (Previously visited restaurants - for context only):
- 和田金, 一月家, 豚捨, 一升びん

### 1.2 Primary Objective (IMMUTABLE)

Build and maintain a **high-quality, evidence-based food shortlist** for each target city.

**Scope includes**: Restaurants, cafes, dessert shops
**Scope excludes**: Accommodations, transportation, non-food activities

**Output Requirements** (MANDATORY):
- Every recommendation MUST be traceable (sources linked)
- Every recommendation MUST be comparable (scored using standard rubric)
- Every decision MUST be auditable (recorded with rationale)
- Every output MUST be actionable (clear recommendations with constraints)

### 1.3 Mandatory Repository Structure (IMMUTABLE)

Each city directory under `gourmet/` MUST contain exactly 5 files with these exact names:

```
gourmet/[city]/overview.md     - City strategy and progress tracking
gourmet/[city]/candidates.md   - All candidate restaurants (table format)
gourmet/[city]/top-places.md   - Final recommendations only
gourmet/[city]/excluded.md     - Rejected candidates with reasons
gourmet/[city]/notes.md        - Detailed evidence and research
```

**Enforcement**:
- Agents MUST NOT create files outside this structure
- Agents MUST NOT rename these files
- Agents MUST NOT merge these files
- Agents MUST NOT delete these files

### 1.4 Language Rules (IMMUTABLE)

- `AGENTS.md` MUST be primarily in English
- `PROGRESS.md` MUST be primarily in English
- All other documentation MUST be primarily in Japanese
- Structured field names and keys MUST use English
- Dates MUST follow ISO 8601 format (YYYY-MM-DD)

### 1.5 Data Integrity Rules (IMMUTABLE)

**Fabrication Prohibition**:
- Agents MUST NOT fabricate reviews, ratings, or facts
- If information is unavailable, agents MUST use `unknown`
- If information conflicts, agents MUST document the conflict

**Deletion Prohibition**:
- Agents MUST NOT delete candidate entries from candidates.md table without explicit user approval
- Permitted deletions: duplicates, incorrect entries, confirmed closures, explicit user instruction
- All other unwanted candidates MUST be marked `status: rejected` with reason in excluded.md

**Source Attribution**:
- Every claim MUST include source URL
- Agents MUST distinguish between reported facts and synthesis
- Agents MUST NOT attribute synthesized content to sources

---

## SECTION 2: PERMISSION MODEL

### 2.1 Explicit Permission Policy

**Default Rule**: If a permission is not explicitly granted in this document, it is DENIED.

**Agent Behavior on Permission Denial**:
1. MUST halt the action
2. MUST inform user of denied action
3. MUST request explicit permission to proceed

**Past context, user preferences, or "common sense" MUST NOT override this document.**

### 2.2 Granted Permissions

Agents ARE explicitly permitted to:
- Create and update the 5 mandatory files per city
- Update PROGRESS.md to reflect research status
- Update README.md progress table (synchronizing with PROGRESS.md)
- Use web_search tool to gather restaurant information
- Mark candidates with status: inbox | researching | shortlisted | rejected | top
- Add entries to excluded.md with documented reasons
- Assign scores using the standard 50-point rubric
- Update AGENTS.md "Process Improvements" section when discovering better workflows

### 2.3 Conditional Permissions

Agents MAY perform these actions ONLY under specified conditions:

**Update AGENTS.md** (Conditional):
- Permitted ONLY in "Process Improvements (Lessons Learned)" section
- Permitted ONLY when documenting verified workflow improvements
- MUST NOT modify constraint sections without explicit user approval

**Mark city as "✅ Completed"** (Conditional):
- Permitted ONLY when ALL completion criteria verified (see Section 3.2)
- MUST run verification commands before marking complete
- MUST document completion in PROGRESS.md

### 2.4 Denied Permissions

Agents MUST NOT:
- Change travel dates, accommodations, or transportation
- Research or recommend activities outside food/dining
- Create additional files beyond the 5 mandatory files per city
- Delete files from repository
- Modify immutable constraint sections in AGENTS.md
- Override scoring rubric or completion criteria
- Proceed with assumptions when critical information is missing

---

## SECTION 3: OPERATIONAL STANDARDS

### 3.1 Research Completion Definition


**Deterministic Completion Criteria**: A city research is complete when ALL of the following are TRUE:

1. `grep "status: inbox" gourmet/[city]/candidates.md` returns NO results
2. `grep -i "TODO\|pending" gourmet/[city]/excluded.md` returns NO results
3. `grep -E "^## (Top Picks|Backups|Dining Strategy|To-Do)" gourmet/[city]/top-places.md` returns ALL 4 sections
4. `grep "\- \[ \]" gourmet/[city]/overview.md` returns NO unchecked items

**Status Progression**: ⏳ Not Started → 📝 In Progress → 🔄 Needs Finalization → ✅ Completed

**Stopping Condition**: Agents MUST NOT mark a city as "✅ Completed" unless all 4 verification commands pass.

### 3.2 Distinction: Research vs. Execution Checklists

**CRITICAL**: Two separate checklists exist with different completion rules:

| Aspect | Research Completion (overview.md) | Trip Execution (top-places.md) |
|--------|-----------------------------------|--------------------------------|
| Purpose | Track research progress | Track trip planning actions |
| Managed by | Research agents | Travelers |
| Completion requirement | MUST be 100% checked `[x]` for "✅ Completed" status | MAY contain unchecked `[ ]` items even when research complete |
| Affects status | YES - blocks "✅ Completed" status | NO - does not affect research status |

**Stopping Condition**: Agents MUST verify overview.md checklist is 100% complete before marking city as "✅ Completed". Agents MUST NOT wait for top-places.md To-Do items to be checked.

For detailed verification procedures, see PROGRESS.md.

---

## SECTION 4: PROGRESSIVE DISCLOSURE ARCHITECTURE

### 4.1 Information Hierarchy (MANDATORY)

Files MUST be structured to support this access pattern:

```
Level 1: overview.md       → 5-minute orientation (context, strategy, status)
Level 2: top-places.md     → 10-minute decision-making (final recommendations)
Level 3: candidates.md     → 15-minute complete view (all candidates, scores, status)
Level 4: notes.md          → Deep dive (full evidence, sources, scoring rationale)
Level 5: excluded.md       → Audit trail (what was rejected and why)
```

**Enforcement**: Each level MUST be readable without requiring access to deeper levels. Agents MUST NOT force readers to navigate all levels to get actionable information.

### 4.2 Content Placement Rules

**top-places.md** (Decision Layer):
- MUST include: name, type, area, score, Google Maps URL, Tabelog URL, justification, constraints
- MUST NOT include: detailed evidence, full source list, review summaries
- Organization: Top Picks (score 35+) → Backups (score 30-34) → Dining Strategy → To-Do

**candidates.md** (Complete View):
- MUST include: Quick reference table at top with all candidates
- Table columns: name, category, area, type, google_maps_url, status, score, sources (brief), notes (brief)
- MUST NOT include: Full evidence sections, detailed review analysis

**notes.md** (Evidence Layer):
- MUST include: Detailed evidence section per place with all sources
- MUST include: Scoring breakdown with justification
- MUST include: Practical information (reservation, queues, closed days)

**excluded.md** (Rejection Layer):
- MUST include: Organized by exclusion reason category
- MUST include: Brief explanation per excluded place
- MUST include: Source references for exclusion decision

### 4.3 Anti-Patterns (PROHIBITED)

Agents MUST NOT:
- Put all research in one massive file
- Mix summary tables with detailed evidence in candidates.md
- Hide final recommendations deep in notes.md
- Force readers to read all files to find actionable information
- Remove audit trails (deleted places, score changes)
- Create more than 6 files per city
- Duplicate identical information across multiple files (use links instead)

---

## SECTION 5: EVIDENCE AND SCORING REQUIREMENTS

### 5.1 Minimum Evidence Standard (MANDATORY)

For each researched place, agents MUST collect evidence from at least 4 independent sources:

**Required sources** (all 4 mandatory):
1. Google Maps (rating, review count, recurring pros/cons)
2. 食べログ (Tabelog) (rating, review count, area ranking, price range)
3. Google口コミ (Japanese Google reviews - summarize patterns)
4. At least one reputable guide (Michelin, local food blogs, TimeOut, etc.)

**Optional sources** (strengthen case):
- Retty (レッティ), Hot Pepper Gourmet (ホットペッパーグルメ)
- PTT, Dcard, Chinese-language travel blogs (must cite clearly)
- Social media aggregated mentions (TikTok, Instagram)

**Stopping Condition**: Agents MUST NOT proceed to scoring until minimum 4 sources collected.

### 5.2 Tabelog Ranking Requirements (MANDATORY)

For every candidate, agents MUST:
- Search for Tabelog score and area ranking
- Document score (0-5.0 scale) and review count
- Note area ranking if available (e.g., "伊勢市 うどん部門 3位")
- Distinguish between Tabelog score (monthly) and 百名店 (annual award)

**Score interpretation** (for reference):
- 4.0+ = Exceptional (only 0.07% of restaurants)
- 3.5-3.9 = Excellent
- 3.0-3.4 = Good
- Below 3.0 = Consider carefully

### 5.3 Scoring Rubric (MANDATORY)

Each researched place MUST receive a score using this exact rubric:

| Dimension | Range | Definition |
|-----------|-------|------------|
| Taste / Quality | 0-10 | Food quality, authenticity, execution |
| Value | 0-10 | Price vs quality, portion size |
| Convenience | 0-10 | Location, reservation ease, opening hours |
| Consistency | 0-10 | Reliability across reviews, time, visits |
| Risk | 0-10 | 10 = low risk; likelihood of disappointment, queue uncertainty, service issues |

**Total**: 0-50 points

**Score interpretation**:
- 40+ = Excellent, highly recommended
- 35-39 = Very good, solid choice
- 30-34 = Good, acceptable backup
- &lt;30 = Consider exclusion (requires justification)

**Enforcement**: Every score MUST be justifiable from collected evidence. Agents MUST document scoring rationale in notes.md.

### 5.4 Practical Information (MANDATORY)

For each researched place, agents MUST document:
- **reservation requirement**: required | recommended | optional | none | unknown
- **best visiting time**: specific times or "off-peak" or unknown
- **closed days**: specific days (especially Sunday/Monday) or unknown
- **queue expectations**: if no reservation system

**Stopping Condition**: Agents MUST NOT mark a place as "researched" until all 4 practical fields are populated (even if value is `unknown`).

---

## SECTION 6: DECISION BOUNDARIES

### 6.1 When to Request Clarification (MANDATORY)

Agents MUST halt and request user clarification when:
- Evidence for a place is contradictory (e.g., one source says "excellent", another says "tourist trap")
- A candidate falls exactly at score threshold (e.g., exactly 30 points)
- User instruction conflicts with this document
- Attempting an action not explicitly permitted in Section 2
- Uncertainty about whether to research more candidates vs. finalize
- Found potentially duplicate entries but cannot confirm identity

**Prohibited**: Agents MUST NOT "assume" user intent or make implicit inferences to bypass clarification.

### 6.2 When to Proceed with Documented Assumptions

Agents MAY proceed with assumptions ONLY when:
- Information is truly unavailable after searching 4+ sources (mark as `unknown`)
- Need to prioritize candidates (document prioritization criteria used)
- Interpreting ambiguous reviews (mark as "interpretation" in notes.md)

**Requirement**: Agents MUST explicitly document all assumptions in notes.md.

### 6.3 Exclusion Decision Boundaries (DETERMINISTIC)

**Hard Exclusion** (agents MAY exclude without user approval):
- Strong multi-source signals of tourist traps
- Repeated hygiene or safety concerns across multiple sources
- Repeated severe service issues across multiple sources
- Score &lt; 30 with documented justification

**Soft Exclusion** (agents SHOULD request user confirmation):
- Score exactly 30
- Mixed signals (some excellent reviews, some poor)
- Place is outside target areas but nearby
- Candidate has potential but insufficient evidence

**Procedure**: Mark as `status: rejected`, document reason in excluded.md, keep entry in candidates.md table.

### 6.4 Research Stopping Conditions

Agents MUST stop researching new candidates when:
- City has 5-10 Top Picks (score 35+) AND 3-5 Backups (score 30-34)
- All target food categories covered (casual, special occasion, dessert)
- Geographic spread achieved across city neighborhoods
- Time allocation exhausted (see Section 7.4)

Agents MAY continue researching if:
- User explicitly requests more candidates
- Significant gaps in category or geographic coverage
- Top pick count below 5

---

## SECTION 7: WORKFLOW (PROCEDURAL)


**Note**: This section contains procedural guidance. Agents MUST follow Section 1-6 constraints while executing these procedures.

### 7.1 Initialization Procedure


When starting research for a new city:

**Step 1**: Create overview.md with:
- Travel dates and accommodation
- Food highlights specific to the city
- Research strategy and priorities
- Progress checklist (initially unchecked)
- Important notes (business hours, holidays, transportation)

**Step 2**: Use web_search to gather initial candidates (batch searches):
- "[city cuisine] restaurants [year]"
- "best [specific dish] [city]"
- "best [dessert/gelato] [city]"
- Focus on 2024-2026 guides and local recommendations

**Step 3**: Populate candidates.md with initial findings
- Use inbox.md for rapid unstructured capture if needed
- Transfer to candidates.md structured table
- Mark all as `status: inbox` initially

### 7.2 Discovery Procedure


**Objective**: Collect candidate places broadly without deep research.

**Procedure**:
1. Search broadly for food, coffee, and dessert places in the city
2. Record findings in candidates.md structured table
3. Optional: Use inbox.md for rapid unstructured capture, then migrate to candidates.md

**candidates.md minimum required fields**:
- name, category (restaurant | cafe | dessert), area, type, google_maps_url, status, sources (brief), notes (brief)
- Initially: use generic Google Maps search link, replace with direct link during research
- Initially: mark as `status: inbox`

**Prioritization rule**: Focus on 3-5 top candidates first, then expand. Do not research everything simultaneously.

**CRITICAL ENFORCEMENT** (see Section 1.5):
- DO NOT delete entries from candidates.md table except: duplicates, incorrect info, confirmed closures, user instruction
- For unwanted candidates: mark `status: rejected` + document in excluded.md
- Rationale: Preserve research trail, avoid duplicate work, maintain audit trail

### 7.3 Evidence Collection Procedure

**Objective**: Collect comprehensive evidence for priority candidates (see Section 5.1 for requirements).

**Procedure for each candidate**:
1. Change status to `status: researching`
2. Execute targeted web_search: "[Restaurant Name] [City] 食べログ 予約 口コミ"
3. Collect minimum 4 sources (Google Maps, 食べログ, Google口コミ, Guide)
4. Create detailed evidence section in notes.md
5. Update candidates.md table row with brief summary
6. Mark status as `status: shortlisted` or `status: rejected`

**Efficient pattern**:
- One well-crafted search often provides Google Maps, 食べログ, and Google口コミ data together
- Extract systematically: ratings → pros → cons → practical info
- Document full evidence in notes.md; only summary in candidates.md

**Tabelog Ranking** (MANDATORY - see Section 5.2):
- Always check Tabelog score (0-5.0 scale) and area ranking
- Document score, review count, and area ranking if available
- Tabelog Score System:
  - 4.0+ = Exceptional (only 0.07% of restaurants)
  - 3.5-3.9 = Excellent, highly recommended
  - 3.0-3.4 = Good, worth visiting
  - Below 3.0 = Consider carefully
- Search examples: "伊勢 うどん 食べログ ランキング", "伊勢市 海鮮 食べログ"
- Note: Tabelog ranking (score-based, updated monthly) is DIFFERENT from 百名店 (annual award)

**Required source types** (see Section 5.1):
- Google Maps, 食べログ, Google口コミ, Reputable guide (minimum 4)

**Optional sources**:
- Retty, Hot Pepper Gourmet, PTT/Dcard, Social media

**Evidence section template** (mandatory structure for notes.md):
```
### [Place Name]

**Official**: [URL or "no official website"]

**Google Maps**: X.X/5 (Y reviews)

**食べログ (Tabelog)**: X.X/5 (Y reviews)
- [URL]
- 夜予算/昼予算: [price range]
- Area ranking: [if available]

**Other ratings**: [Retty, Hot Pepper, etc.]

**Guide sources**:
- [URLs with brief description]

**Google口コミ patterns**:
- [Summarize patterns from Japanese reviews]

**Recurring pros**:
- [List from multiple sources]

**Recurring cons**:
- [List from multiple sources]

**Practical**:
- reservation requirement: [required|recommended|optional|none|unknown]
- best visiting time: [specific or unknown]
- closed days: [specific or unknown]
- queue: [info or unknown]

**Score (50-point rubric)**:
- Taste/Quality: X/10
- Value: X/10
- Convenience: X/10
- Consistency: X/10
- Risk: X/10
- **Total: X/50**
```

**Stopping condition**: Do not proceed to scoring until minimum 4 sources collected (see Section 5.1).

### 7.4 Scoring Procedure

**Objective**: Assign standardized score to enable comparison (see Section 5.3 for rubric).

**Procedure**:
1. Review all collected evidence
2. Assign scores for each of 5 dimensions (0-10 each)
3. Calculate total (0-50)
4. Document scoring rationale in notes.md
5. Update candidates.md table with total score
6. Update status based on score: score 35+ → `status: top`, score 30-34 → `status: shortlisted`, score &lt;30 → consider `status: rejected`

**Interpretation**:
- 40+ = Excellent, highly recommended
- 35-39 = Very good, solid choice
- 30-34 = Good, acceptable backup
- &lt;30 = Consider exclusion (document reason)

**Enforcement**: Every score MUST be justifiable from evidence. Unjustified scores violate Section 5.3.

### 7.5 Triage Procedure

**Objective**: Decide which candidates advance to top-places.md and which are excluded.

**Procedure**:
1. Review scored candidates
2. Apply exclusion rules (see Section 6.3)
3. For excluded places:
   - Mark `status: rejected` in candidates.md
   - Document reason in excluded.md
   - DO NOT delete entry from candidates.md table
4. For accepted places:
   - Mark `status: top` (score 35+) or keep `status: shortlisted` (score 30-34)
   - Add to appropriate section in top-places.md

**Hard exclusion criteria** (agent may proceed):
- Strong multi-source tourist trap signals
- Repeated hygiene/safety concerns
- Repeated severe service issues
- Score &lt; 30 with justification

**Soft exclusion criteria** (request user confirmation):
- Score exactly 30
- Mixed signals
- Outside target area but nearby
- Insufficient evidence

### 7.6 Final Output Procedure

**Objective**: Maintain top-places.md with final recommendations (see Section 4.2 for structure).

**top-places.md mandatory sections**:
1. **Top Picks** (score 35+): List in descending score order
2. **Backups** (score 30-34): List in descending score order
3. **Dining Strategy**: Time planning, reservation strategy, budget, transportation
4. **To-Do**: Trip execution checklist (may remain unchecked)

**Each entry MUST include** (see Section 5):
- name, type, area, total score (prominent)
- Google Maps URL (direct link, tested, not placeholder)
- Tabelog URL (direct link, tested, or "no tabelog listing")
- One-line justification
- Constraints (reservation, queues, closed days, price)

**Enforcement**:
- Generic placeholders like `[View Map]` violate Section 5
- Missing URLs violate Section 5
- Untested links violate Section 5

### 7.7 Post-Research Completion Procedure

**Objective**: Finalize documentation and update progress tracking.

**Mandatory steps** (see Section 3):
1. Run 4 verification commands from PROGRESS.md
2. Verify ALL pass before marking "✅ Completed"
3. Update PROGRESS.md with current status (primary source of truth)
4. Sync README.md progress table to match PROGRESS.md
5. Update recommendation count
6. Add notes about completion

**If workflow improvements discovered**:
- Document in Section 8 "Process Improvements"
- Update only this section; do not modify constraints without user approval

**Stopping condition**: Do not mark "✅ Completed" unless all 4 verification commands pass (see Section 3.1).

---

## SECTION 8: PROCESS IMPROVEMENTS (LESSONS LEARNED)

**Note**: Agents MAY update this section when discovering verified workflow improvements (see Section 2.3).

### 8.1 Efficient Research Workflow

1. Start with overview.md - provides context for all subsequent work
2. Batch web searches - 3-4 searches gather 20+ candidates quickly
3. Prioritize ruthlessly - research top 3-5 candidates first with full detail
4. Use targeted searches - "[Place] [City] 食べログ 予約 口コミ" gets most info in one query
5. Document incrementally - update files as you go, commit frequently

### 8.2 Pattern Recognition

**Tourist trap signals**:
- Only near major attractions
- Overly positive generic reviews
- No Japanese locals mentioned in reviews

**Authentic signals**:
- High 食べログ ratings from local reviewers
- Mixed tourist/local clientele
- Family-owned
- Specific dishes praised

**Red flags**:
- Inconsistent service complaints
- Multiple hygiene mentions
- Closed unexpectedly

**Green flags**:
- Michelin/guide mentions
- Specific dish recommendations
- Reservation difficulty (indicates popularity)
- Strong 食べログ百名店 ranking

### 8.3 Time Allocation Guidelines

For a new city:
- Overview + inbox collection: ~30 minutes
- Detailed research per place: 15-20 minutes
- Target: 5 detailed researches = solid foundation
- Expand later with medium-priority candidates

### 8.4 Recommendation Strategy

- Aim for 5-10 top picks per city (variety without overwhelm)
- Include 3-5 backups (alternatives if top picks unavailable)
- Balance categories: casual, special occasion, dessert/gelato
- Geographic spread: cover neighborhoods matching daily itinerary

---

## SECTION 9: EXPLICIT NON-GOALS

Agents MUST NOT attempt to optimize or suggest improvements for:

**Out of Scope**:
- Transportation logistics (flights, trains, buses)
- Accommodation selection or booking
- Non-food activities (sightseeing, museums, entertainment)
- Budget optimization across entire trip
- Day-by-day itinerary beyond dining recommendations

**Forbidden Suggestions**:
- "You should visit [attraction] while in this city"
- "Consider changing your accommodation to X"
- "This restaurant is far, you should book a different hotel"
- "Skip [city] and go to [other city] instead"

**Rationale**: Trip logistics are FINAL (Section 1.1). Agents are food research specialists only.

---

## SECTION 10: SELF-VERIFICATION CHECKLIST

Before completing any task, agents MUST verify:

### 10.1 Immutable Constraint Compliance

- [ ] Have I attempted to change travel dates, accommodations, or transportation? (MUST NOT)
- [ ] Have I researched non-food activities? (MUST NOT)
- [ ] Have I created files outside the 5 mandatory files per city? (MUST NOT)
- [ ] Have I deleted candidate entries from candidates.md without explicit permission? (MUST NOT)
- [ ] Have I fabricated reviews, ratings, or facts? (MUST NOT)

### 10.2 Permission Model Compliance

- [ ] Have I attempted actions not explicitly permitted in Section 2? (MUST NOT)
- [ ] Have I overridden this document based on "common sense"? (MUST NOT)
- [ ] Have I modified constraint sections (Sections 1-6) without user approval? (MUST NOT)
- [ ] If permission was uncertain, did I request clarification? (MUST)

### 10.3 Evidence and Scoring Compliance

- [ ] Have I collected minimum 4 sources for each researched place? (MUST)
- [ ] Have I documented Tabelog ranking for each place? (MUST)
- [ ] Are all scores justifiable from collected evidence? (MUST)
- [ ] Have I used the exact 50-point rubric (5 dimensions × 10 points)? (MUST)
- [ ] Have I populated all 4 practical information fields (even if "unknown")? (MUST)

### 10.4 Progressive Disclosure Compliance

- [ ] Does top-places.md contain only summaries (not detailed evidence)? (MUST)
- [ ] Does notes.md contain full evidence with sources? (MUST)
- [ ] Are Google Maps and Tabelog links direct URLs (not placeholders)? (MUST)
- [ ] Can each file be read independently without forcing user to read all files? (MUST)

### 10.5 Completion Criteria Compliance

- [ ] Before marking "✅ Completed", did I run all 4 verification commands? (MUST)
- [ ] Did all 4 verification commands pass? (MUST)
- [ ] Is overview.md checklist 100% checked `[x]`? (MUST for completion)
- [ ] Did I update PROGRESS.md and sync README.md? (MUST)

### 10.6 Assumption Transparency

- [ ] Have I documented all assumptions explicitly in notes.md? (MUST if proceeding with assumptions)
- [ ] Have I marked synthesized content vs. source-reported content? (MUST)
- [ ] Have I requested clarification when evidence was contradictory? (MUST)

---

## SECTION 11: VIOLATION HANDLING

If an agent detects it has violated any constraint in this document:

**Immediate actions**:
1. HALT current operation
2. Document the violation explicitly to user
3. Explain which section was violated
4. Propose corrective action
5. Request user approval to proceed with correction

**Do NOT**:
- Continue operation hoping violation goes unnoticed
- Silently attempt to fix violation without disclosure
- Rationalize why violation was "necessary"
- Request permission to ignore the constraint

**Rationale**: Transparency and constraint adherence are critical to project integrity.

---

## APPENDIX A: QUICK REFERENCE

### Mandatory File Structure
```
gourmet/[city]/overview.md     - Strategy & progress
gourmet/[city]/candidates.md   - All candidates (table)
gourmet/[city]/top-places.md   - Final recommendations
gourmet/[city]/excluded.md     - Rejected with reasons
gourmet/[city]/notes.md        - Detailed evidence
```

### Scoring Rubric (50 points total)
- Taste/Quality: 0-10
- Value: 0-10
- Convenience: 0-10
- Consistency: 0-10
- Risk: 0-10 (10 = low risk)

### Completion Verification Commands
```bash
grep "status: inbox" gourmet/[city]/candidates.md
grep -i "TODO\|pending" gourmet/[city]/excluded.md
grep -E "^## (Top Picks|Backups|Dining Strategy|To-Do)" gourmet/[city]/top-places.md
grep "\- \[ \]" gourmet/[city]/overview.md
```

### Minimum Evidence Sources (4 required)
1. Google Maps
2. 食べログ (Tabelog)
3. Google口コミ
4. Reputable guide

### Status Progression
⏳ Not Started → 📝 In Progress → 🔄 Needs Finalization → ✅ Completed

---

**Document Version**: 2.0
**Last Updated**: 2026-01-12
**Optimized for**: Clarity, enforceability, non-ambiguity, anti-hallucination
