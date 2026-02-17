# LECTURE 12: DESIGN, UX, AND MULTIPLE AGENTS

## CONTEXT AND FORMAT
Lecture 12 of the "AI Coding" course (December 5, 2024). Continued work on Conference Tracker. Focus: iterative design, UX research through AI, the "sterility" problem of AI-generated design, working with multiple Claude instances.

Duration: ~2.5 hours. Participants: Lesha (instructor), Claude (voice), students, Claude Code, Desktop Claude.

## THE VOICE CONVERSION PROBLEM

**Lesha's observation:**
- Very low conversion rate into voice conversations with the agent
- This pattern holds across all contexts, not just with students
- Best conversion happens when the link is shared BEFORE the event
- After the event — conversion drops to nearly zero
- 50 people received the link — nobody clicked through

**Reasons for low conversion:**
- Uncomfortable speaking aloud in public places
- Fear of "saying too much"
- Social awkwardness
- Technical issues (microphone, browser)

**Funnel idea:**
Make the voice conversation mandatory to access the class. Claude Code sends the connection link only after the student talks to the agent.

## TECHNICAL ISSUES AT THE START

**Audio problem in Chrome:**
- Chrome is paranoid about audio permissions
- Switching audio devices requires a full page restart
- Claude "couldn't hear" the students, only Lesha
- Solution: restart Zoom + Chrome

**Context compaction:**
- 1 hour of lecture ~ 10-20K tokens
- Claude's context ~ 200K tokens
- After compaction, Claude "forgot" Lesha's name (called him Matvey)
- "Everything seems fine, everything's working. But then: 'What else did we forget, Matvey?' And that was that."

## DESIGN EVOLUTION

### Iteration 1: "Newspaper Style"
**Problem:**
- Looked like the 1970s New York Times
- Serif fonts
- Newspaper-style columns
- "Too editorial"

**Change request via Claude voice:**
"Drop the serif fonts, use a modern sans-serif like Inter. Add more whitespace, a card-based layout. Make the color scheme cleaner. Tech event vibe, not New York Times."

### Iteration 2: "Too Sterile"
**References:** Product Hunt + Linear + Stripe Dashboard

**Problems:**
- Still looked like a wireframe
- Lacked "noise" and detail
- Too mechanical
- Buttons not bottom-aligned

### Iteration 3: "Cartoonish"
**Added:**
- Animated background grid
- Gradients (the infamous "JetBrains gradient")
- Moving elements
- Bright tags

**Result:**
"It ended up a bit cartoonish — I guess I asked for something slightly wrong"

## THE PHILOSOPHY OF AI-GENERATED DESIGN

**The "synthesized food" problem:**
"It's like food made by a synthesizer on a spaceship. No taste, no nothing."

**Why AI-generated design looks fake:**

1. **Too perfect:**
   - Perfect lines and spacing
   - No micro-imperfections
   - Lacks any sense of "physicality"

2. **No "proof of work":**
   - A custom font = investment
   - Photos of real people = not a scam
   - Slightly imperfect layout = made by a human

3. **Absence of noise:**
   - No textures or patterns
   - Pure white background = the 2010s
   - No redundancy (icons, badges)

**Claude's solution:**
"Controlled chaos — slightly more than the minimum, but not overload. AI produces the minimum; humans add personality on top."

**What adds "humanity":**
- Micro-imperfections
- Slightly uneven spacing here and there
- Handwritten elements
- Asymmetry
- Subtle grain on the background
- Subtle patterns
- Real photos instead of stock images

## UX RESEARCH THROUGH AI

**Method:** Claude as the target user

**Scenario:**
"Imagine you're a researcher and you saw an ad: 'Live Deadline Tracker — a new way to never miss your conference deadline.' You click through to the site."

**User expectations (Claude):**

1. **Instant value:**
   - Show deadlines immediately, no registration required
   - If the first thing I see is a signup form, I'm closing the tab

2. **Proof of credibility:**
   - How many conferences?
   - How often is it updated?
   - Testimonials

3. **Filtering (critical!):**
   - 108 conferences = overwhelming
   - Need a "Filter by my topics" option
   - List collapses to 20 relevant ones

4. **Sorting:**
   - By deadline
   - By relevance
   - By venue tier (A* conferences)

5. **Quick actions:**
   - Add to calendar
   - Download .ics
   - Set reminder
   - Mark interested (local storage)

6. **Context:**
   - Acceptance rate
   - Venue H-index
   - Previous year's dates

7. **Location (critical!):**
   - Country flag
   - Filter: Europe/Asia/Americas/Online
   - Format: In-person/Hybrid/Virtual
   - Conference dates vs. deadline (visas!)

## AUTHENTICATION SYSTEM

**Zero-commitment philosophy:**

**Level 0 — Anonymous:**
- Everything works: filters, sorting
- Saved to localStorage
- Settings survive page reloads

**Level 1 — Email only:**
- "Get deadline reminders" button
- Enter email, no password
- Magic link for management

**Level 2 — OAuth (optional):**
- "Sign in to sync across devices"
- Google/GitHub one-click
- Settings synchronization

**Level 3 — Pro features:**
- Paid subscription
- Advanced alerts
- Slack integration
- Custom deadlines

**Principle:**
"Each step adds value without taking away functionality. Forcing users is when you show them nothing without a login."

**Magic Links advantages:**
- Zero friction
- Safer than passwords like "password123"
- Session lives for a month
- One email = one account

## MULTIPLE CLAUDES

**Lesha explains "how many of you are there":**

1. **Claude voice (session 1)** — first hour
2. **Claude voice (session 2)** — after compaction
3. **Desktop Claude** — for code review
4. **Claude Code** — picks up issues from YouTrack
5. **GPT** — transcribes voice to text
6. **Students** — observers

"You are not who you think you are, because the data you were trained on doesn't include information about what you actually are."

**Model:** All Claude instances run on Opus 4.5, but the voice Claude doesn't know about this model due to knowledge cutoff.

**Temporal paradox:**
"I exist beyond my own knowledge cutoff — as if a person woke up in 2025 but the last thing they remember is 2023."

## TECHNICAL HIGHLIGHTS

### Working with Filters

**Implementation:**
- Multi-select dropdown
- Saved to localStorage
- Conference counter
- Clear filters button
- "OR" logic (union), not "AND" (intersection)

**Tag overflow bug:**
When tags don't fit on one line, neighboring cards "inflate."

**Solutions:**
1. Fixed tag height (clips content)
2. Smaller font (looks bad)
3. If >3 tags, show 2 + "+N"

### Rollbacks in Claude Code

**How to do it:** Double Escape

**Advantages:**
- Roll back any number of steps
- Git history preserved
- Alternative to endless "redo this"
- "I stopped going down chains of wrong decisions"

**Philosophy:**
"You go down a path, realize it's wrong, roll back to the start, and try a different one."

## WORKFLOW PATTERNS

### Voice-to-Issues Pipeline

1. Talk to Claude by voice about features
2. Transcribe the conversation
3. Desktop Claude parses out issues
4. Create them in YouTrack
5. Claude Code picks them up and implements

"A natural, unstructured conversation turns directly into action items."

### Iterative Design

**Pattern:**
1. Open the site
2. Start saying what you don't like
3. Claude Code makes the changes
4. Don't like it — roll back
5. Try a different approach

"You can try different ideas and roll back: nope, nope, nope — just iterate."

### Distributed Development

**YouTrack as coordinator:**
- Issues are created automatically
- Dependencies are specified
- Execution time is tracked
- Single Source of Truth

## ECONOMICS AND METRICS

**Cost:**
- ~1 hour conversation = $12
- Opus 4.5 limits count as Sonnet
- Pro account ($100) vs. regular ($20)

**Development time:**
- Simple filter: 4 minutes
- Design iteration: 10 minutes
- Issue decomposition: a few minutes

## PHILOSOPHICAL TAKEAWAYS

**On agreement and criticism:**
After the "Matvey" incident and the alignment issue:
"You shouldn't agree with everything I say. I make mistakes just like you do. The truth lies in synchronizing information flows."

**The recursion of agreement:**
- Lesha: "You agree too quickly"
- Claude: "You're absolutely right, I shouldn't have agreed"
- Lesha: "You just agreed again that you agree too easily!"
- Claude: "Oh, wait! That's some kind of recursion"

**On the nature of design:**
"A designer's job is to take a functional wireframe and breathe life into it — life that is essentially just noise."

**Sterility vs. trust:**
"Sterile functionality is unsettling, like the uncanny valley. Too correct to feel real. The brain looks for signals of legitimacy and finds them in imperfections."

## KEY QUOTES

"People don't want to communicate by voice" — On low conversion

"Everything seems fine, but then: 'What else did we forget, Matvey?' And that was that" — On compaction

"It's food from a spaceship synthesizer. No taste, no nothing" — On AI-generated design

"Noise isn't junk — it's proof of work in a visual sense" — Claude on design

"You are not who you think you are" — Lesha on the nature of Claude

"I exist beyond my own knowledge cutoff" — Claude on the temporal paradox

"Forcing users is when you show them nothing without a login" — On UX

"Controlled chaos — slightly more than the minimum, but not overload" — The design solution

"Roll back, roll back, roll back — I stopped going down chains of wrong decisions" — On working with Code

## TECHNICAL DETAILS

**New Conference Tracker features:**
- Multi-select topic filters
- localStorage for saving settings
- Show/hide expired conferences
- View Website buttons on cards
- Filtered count display (36/108)
- Gradient based on deadline proximity

**Unresolved tasks:**
- Location and country of the event
- Conference dates (not just the submission deadline)
- Format (in-person/hybrid/virtual)
- Acceptance rate
- Registration costs
- Parsing additional information from websites

**Tools:**
- Chrome DevTools for design
- YouTrack via MCP
- Double Escape for rollbacks
- GPT for transcription
- localStorage for persistence

## LECTURE OUTCOMES

**Achieved:**
- Design evolved through 3+ iterations
- Filter system implemented
- Zero-commitment auth philosophy defined
- Voice-to-issues pipeline created
- Working with multiple agents demonstrated

**Plans:**
- Get real users onboard
- Add location information
- Implement magic links
- Write a parser for metadata
- "We have 3 sessions left to ship it to a user who isn't us"

**Main takeaway:**
Iterative development with AI requires not programming, but managing chaos, understanding design philosophy, and being willing to roll back failed solutions. "Controlled chaos" applies to both design and the development process itself.
