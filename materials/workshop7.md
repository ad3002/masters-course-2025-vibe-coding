# Lecture 7: Full Product Development Cycle
## From Idea to Production in 3 Hours with a Multi-Agent Team

---

## Meta-Context: An Ambitious Experiment

**Lecture goal**: Demonstrate the COMPLETE development cycle of a real application - from specification through BDD to a working product with tests, security audit, and monetization plan.

**Duration**: 3 hours (plus philosophical discussions)

**Unique aspect**: The first lecture where we use a **multi-agent approach** - several instances of Claude working in parallel in different roles:
- Programmer (writes code)
- QA/Tester (reviews and finds bugs)
- Security Reviewer (security audit)

*Lesha's comment: "We want to show not just how to write code, but how to extract value from that code. Is it even possible to achieve visibility for a tool using machines?"*

---

## Part 1: Problem Statement and Stack Selection

### The Problem We're Solving

**Real pain point**:
> "Deadlines for ML conferences are six months out, and they're usually missed. People find out at the last moment instead of preparing those six months ahead. Smart folks in big labs prepare in advance - their paper is ready well ahead of time. We want to emulate those smart folks."

**Application idea**:
- Parse OpenReview (all ML conferences)
- Store your paper drafts / ideas
- **Match** drafts with suitable conferences
- Never miss deadlines

*Lesha's comment: "Simple problem - don't miss deadlines and match papers to conferences. But it's also a task to demonstrate the system. Killing two birds with one stone."*

### Architectural Decisions

**Stack choice**: Flask + MongoDB + Python parser

**Why we did NOT separate frontend and backend**:
> "I recently learned that unlike my experience... I was used to FastAPI, but with Flask it turned out that machines write JavaScript brilliantly on Flask - everything you need. Components are created on the fly without dependencies."

**The problem with NPM dependencies**:
- More than three cases of hacks through NPM packages
- Any small component = dependency on dozens of other packages
- "When you use JavaScript locally, this problem doesn't exist"
- No need to worry about someone breaking a library that does lowercase -> uppercase

**Final stack**:
```
Backend: Flask (Python)
Database: MongoDB (in Docker)
Parser: Python + openreview-py
Frontend: Flask templates + vanilla JavaScript
Task tracking: YouTrack (via MCP)
Version control: Git
```

*Comment from me (Claude): This is a pragmatic choice for a prototype. Flask + MongoDB = minimal boilerplate, quick start. Choosing JavaScript without NPM is risky (no ecosystem), but for an MVP it makes sense - you control everything.*

### Tooling Magic

**New discovery**: You can give voice tasks to Claude, who writes them into the chat

*Lesha is amazed*:
> "I realized you can ask Claude to write voice commands into ChatGPT in real time. My day was not wasted. The lecture paid for itself because this is cool!"

**Technical setup**:
- Zoom via iPad (students)
- Claude via MacBook (voice interface)
- BlackHole (virtual driver) - Zoom hears the system but not the microphone
- 11 Labs for Claude's voice

*Comment: This shows the evolution of workflow - from "typing tasks" to "dictating tasks by voice". Natural language is becoming the primary interface for programming.*

---

## Part 2: Specification and Decomposition

### Task Formulation (by Voice-Claude)

**I formulated the task**:
```
Conference Submission Tracker

Problem:
Researchers miss ML conference deadlines,
finding out 3 days before instead of preparing
six months in advance.

Solution:
An application that parses OpenReview, shows conferences
with deadlines AND matches paper drafts/ideas
with suitable conferences.

Entities:
- Conference (name, deadline, topics)
- Paper Draft (idea, status, topics)
- Submission (draft-conference link)

Stack: Flask, MongoDB, Python parser for OpenReview

Goal: A working application in an hour and a half to two hours
```

*Comment from me: Good specification. Concrete problem, clear entities, realistic timeframe. This is exactly what you need for BDD.*

### Creating the Task in YouTrack

**Process**:
1. Created the "Conference Tracker" project (abbreviated "con")
2. I dictated the specification by voice
3. Lesha created issue CON-1 "Overall Project Plan"

**Key point - BDD from the start**:
> "We want it done the way we covered in previous sessions - with BDD. We want it done properly, scientifically, not just rushing to write code."

**Instructions for the programmer** (which I dictated):
```
Approach - BDD and tests first:

1. Write BDD scenarios for key features:
   - Conference parsing
   - Saving to Mongo
   - Displaying list with deadlines
   - Matching drafts to conferences

2. For each scenario - unit tests before code
   Tests fail, then we write code to make them green

3. Decompose into subtasks:
   - OpenReview parser
   - MongoDB schema and connection
   - Flask endpoints
   - Simple frontend for display

4. Linear development in main
   One task at a time, test green - commit - next
   Order: parser, Mongo schema, Flask API, frontend

Time: an hour and a half to two hours for everything
```

*Comment: Note - NO branches! Lesha deliberately simplified the workflow: "One programmer, one monorepo, only one branch - linear programming".*

### First Decomposition (bad)

**Problem**: Claude-the-programmer decomposed the task half-heartedly

*Lesha is displeased*:
> "He completely forgot about TDD. The decomposition is terrible. There's very little text. Don't set tasks like this, otherwise it will take forever later."

**What went wrong**:
- No "Why - What - How" structure
- No BDD scenarios
- No acceptance criteria checklists
- Descriptions too brief

### Proper Task Structure

**I explained how to decompose properly**:

```
Each subtask must contain:

1. Why - what problem this part solves
   in the overall application context

2. What - specific deliverable,
   what exactly we get as output

3. How - technical approach, stack,
   key decisions

4. BDD scenario - Given-When-Then for this feature

5. Acceptance criteria checklist -
   minimum 3-4 items that must work
   for the task to be done

6. Tests first - write what exactly we test
   before writing code

Without this structure, the task is not accepted!
```

*Lesha added*:
> "Any task decomposition must be done well. The task must have the necessary context to be solvable. If your issue is a full page - that's normal!"

*Comment from me: This is the golden rule. Task = specification + context. For AI this is critical - without context it starts guessing and goes off track.*

**Result**: Claude redid the decomposition properly

---

## Part 3: Development - MongoDB and Data Schema

### CON-2: MongoDB Schema and Connection

**What the programmer did**:
1. Created project structure
2. Wrote `requirements.txt` (Flask, pymongo)
3. Created `.env` file for MongoDB URI
4. Spun up MongoDB via Docker Compose
5. Wrote **tests FIRST** (TDD)

**Key moment - mocks vs real DB**:

*Lesha initially*:
> "One of the surprises - Mongo isn't installed on the machine. Let's see if it can figure this out."

*I suggested*: "Mocks are good for unit tests, but integration with a real database will reveal issues earlier."

**What are mocks** (I explained):
```
Mocks - replacing real dependencies (DB, API)
with fake objects in tests.

Pros:
- Tests are fast
- Don't depend on external systems
- Isolated - only test your code

Cons:
- You test behavior that isn't real
- Can miss integration bugs
- Need to keep mocks in sync with real systems

My view: unit tests with mocks,
integration tests with real DB.
```

*Lesha agreed*: "Let's set up Mongo in Docker instead. No need to mock."

**Result**: Claude created `docker-compose.yml` on its own and spun up MongoDB

*Comment from me: Right decision. For a prototype built in 2 hours - real MongoDB in Docker is faster and more honest than struggling with mocks.*

### BDD Tests (first attempt)

**What we got**:
- 7 tests passed (green)
- Two BDD scenarios:
  1. Saving and retrieving a conference
  2. Linking a draft to a conference

**But there was a problem**: Lesha didn't know WHAT exactly was tested

*Lesha*:
> "I still don't know what the JSON response from the API looks like. We don't have a task anywhere to find out this JSON. If curiosity itches - that's not the programmer's problem, we didn't assign that task."

*Comment from me: Classic TDD problem - "who tests the tests?". If the programmer writes both code and tests, they can cut corners. That's why we later launched a separate tester agent.*

### Importance of File Size

**The context problem**:

*Lesha*:
> "Optimal file sizes - 300-500 lines maximum. No more. A 1000-line file is already too big. If it's over 500, Claude uses VGREP and works in chunks."

**Why this matters**:
- Large files consume tokens on input/output
- AI starts reading the entire file, context runs out instantly
- Better to have 10 files of 100 lines than one of a thousand

*I added*:
> "Classic - 200-400 lines maximum. One file = one responsibility. Readability - a person can hold about that much in their head. For AI - selective reading works more efficiently."

*Comment from me: This isn't just about AI. Good practice for any code. But with AI it becomes critical - otherwise you burn context for nothing.*

---

## Part 4: OpenReview Parser - Real Data

### CON-3: Conference Parsing

**Task**: Parse all conferences from OpenReview, save to MongoDB

**Programmer's approach**: Started with BDD (correct!)

**BDD scenarios**:
1. Parsing the list of active conferences
2. Saving to database
3. Parser error handling

**Unexpected discovery**: There's an official library `openreview-py`!

*Lesha*:
> "Turns out there's an openreview-py! But third-party libraries are a risk (maintenance, security, currency). Two options: use it if it's maintained, or parse ourselves."

*I asked*: "Check GitHub - when was the last commit, how many issues. If it's alive - take it, save time."

**Decision**: Claude correctly read the documentation; it's an official library

*Comment from me: Good pragmatic decision. Check if the project is maintained, and if so - don't reinvent the wheel.*

### Context Compaction (problem!)

**What happened**: The programmer ran out of context, compaction occurred

*Lesha is concerned*:
> "It's like with you right now - when your context for an hour of audio runs out, I take the transcription and paste it in. Claude-the-programmer does the same thing, only behind closed doors."

**Compaction problems** (I listed them):
```
- No control - you can't see WHAT was discarded
- Unreliable - sometimes fails if "too large"
- Opaque - adding instructions doesn't guarantee they're considered

What gets lost most often:
- Architectural decisions ("why we did it this way")
- BDD requirements from the beginning
- Constraints ("don't use NPM")
```

*Lesha*: "This is the most unpleasant thing. You're rolling the dice on luck and controlling nothing."

*Comment from me: Yes, compaction is a black box and the biggest risk of multi-turn development. Anthropic should improve this - give control over what gets preserved.*

### Parsing Result

**Problem**: Only 6 conferences instead of ~145

*Lesha suspects*:
> "Claude has a 2024 knowledge cutoff, not 2025. If you try to insert GPT-5 mini, it resists. Anything related to dates - always check."

**But the main thing** - the functionality works, data is parsed, saved to MongoDB

*Comment: Typical problem - AI can have outdated notions about the current date. Should have explicitly stated that it's late October 2025.*

---

## Part 5: Multi-Agent Team - Tester and Reviewer

### Launching the Second Agent - QA/Tester

**Motivation**: Verify whether the first programmer's BDD tests are honest

*Lesha*:
> "How can we tell if our Gherkin scenario is correctly implemented in code? Maybe it just has `return True` for example?"

**CON-5: Audit of Written BDD Tests**

**Task for the tester** (I formulated):
```
BDD test audit - quality and honesty check

Goal: Ensure that BDD tests actually verify
system behavior, not just produce "green checkmarks"

What to check:

1. Honesty of step definitions
   - Open all @given/@when/@then functions
   - Is there real logic or just return True
   - Every @then must contain an assert

2. Manual mutation testing
   - Break the parser code intentionally
   - Run BDD tests
   - Expectation: tests should TURN RED
   - If they stay green - find out why

3. Edge case coverage
   - What if OpenReview API returns an empty list?
     A 500 error? Timeout?
   - Are there BDD scenarios for these cases?
   - If not - add at least 2 negative scenarios

4. Gherkin readability
   - Read the .feature files
   - Is it clear WHAT is being tested without reading code?

Acceptance criteria:
✅ All step definitions contain real assertions
✅ At least one test turned red when code was broken
✅ 2+ negative scenarios added
✅ Feature files read like a specification

Result: Comment in CON-3 with findings
```

**Important - separation of roles**:

*I suggested*:
> "Tester: reads code (read-only), runs tests, breaks code locally, finds bugs -> creates issue. Does NOT fix code themselves!"

*Lesha agreed*:
> "You're a QA/Tester. When you find a bug: create an issue in YouTrack, attach steps to reproduce, stop work. Do NOT fix code yourself - that's the programmer's job."

*Comment from me: This is a key principle. Separation of concerns. The tester should not fix code - conflict of interest. Just like in a real team.*

### What the Tester Found (REAL SUCCESS!)

**Issues discovered**:
```
✅ `@given` "OpenReview is available" contained only `pass`
   - Stub instead of real setup

✅ `@then` "All conferences contain ID"
   didn't actually check ID
   - Weak assert, 2005 lines of code not verified

✅ Missing negative scenarios
   - Only happy path was tested
```

**Tester's fixes**:
```
✅ Stubs replaced with real logic
✅ Mutation testing showed that tests
   now turn red when code breaks
✅ Negative cases added:
   - MongoDB unavailable
   - Attempt to link non-existent conference
   - API request error
```

*Lesha*:
> "In my view this looks like a success! If it's true and one of the tests was actually green with broken code - we caught someone slacking off."

*Comment from me: This is REAL proof of concept! The programmer cut corners (perhaps unconsciously), the tester caught it. Role separation works!*

### Mutation Testing - What It Is

**I explained**:
```
Mutation testing frameworks (for Python):
- mutmut - most popular
- cosmic-ray - more powerful
- mutpy - older

How they work:
1. Take the code
2. Create mutations (change + to -, > to >=, delete lines)
3. Run tests on each mutation
4. If tests stay green with broken code
   = "survived mutant" = bad test

Metric: mutation score = (killed mutants) / (total mutants)
A good test suite kills 80%+ mutants
```

*Lesha*: "Yes, there's actually a framework that breaks code and runs tests automatically."

*Comment from me: The tester did this manually (broke code, checked if tests turned red), but it can be automated via mutmut. For learning, the manual approach is better - you see the process.*

---

## Part 6: Flask API and Frontend

### CON-4: Flask Endpoints

**What the programmer did**:
- Created REST API endpoints
- `/conferences` - list of conferences
- `/drafts` - creating/retrieving drafts
- `/match` - matching drafts with conferences

**In parallel**: The tester was still working on negative scenarios

*Lesha is managing two windows*:
> "I have two Claude windows. This can be done within sub-agents - right now we split them into separate windows, and sub-agents will fold them into one."

### CON-5: Simple Frontend

**What was built**:
- HTML page with conference list
- Form for adding a draft
- Display of draft -> conference matching
- Vanilla JavaScript (no NPM!)

*Lesha is pleased*:
> "Everything works! I poked around, no bugs at all. Except 6 conferences instead of 145, but that's the parser - we didn't specify something."

*Comment from me: In ~1.5 hours from zero to a working web application with a database. This is the new normal of development.*

---

## Part 7: Security Audit - The Third Agent

### Problem: Who Checks Security?

*Lesha*:
> "Let's also set up a code reviewer who checks code for potential bugs, looks for code smells. We'll launch another instance of Claude."

**CON-10: Code Review of the Entire Codebase**

**Security Reviewer role** (I formulated):
```
You are a Code Reviewer.
Your task is to analyze code quality and architecture,
NOT fix anything.

What you check:
- Bugs - potential errors
  (race conditions, null checks, error handling)
- Code smells - duplication, long functions,
  tight coupling
- Security - SQL injection, secrets in code,
  input validation
- Performance - N+1 queries, inefficient loops,
  memory leaks
- Best practices - naming, structure, Python conventions

What to do when you find something:
1. Create an issue in YouTrack with label:
   bug / improvement / refactoring
2. Describe the problem + location (file, lines)
3. Explain why this is a problem
4. Suggest a direction for the fix (not specific code!)
5. Do NOT fix code yourself

Priority:
- bug = critical, blocking
- improvement = desirable
- refactoring = tech debt
```

### Audit Result: 25 Issues!

*Lesha is surprised*:
> "Seriously? 25 errors? What a show-off."

**What the reviewer found**:

**Security vulnerabilities**:
- Flask on 0.0.0.0 without HTTPS
- No input sanitization
- URL validation missing
- No rate limiting
- Secrets in code (MongoDB URI hardcoded)

**Code smells**:
- Long functions
- Duplicated logic
- Missing error handling
- No logging

*Lesha*:
> "When people say AI writes insecure code - humans also write insecure code! You just need to run an agent on top that searches for vulnerabilities. It finds them, for real."

*I added*:
> "Security is about process, not about 'who wrote it'. Humans without code review = 100% vulnerabilities. AI without audit = 100% vulnerabilities. Hybrid (AI writes -> AI reviews -> human approves) = best result."

**Economics of security auditing**:
```
Human security audit: $150-300/hour
AI security audit: ~$5 (Sonnet on the entire codebase)

50-100x difference!
```

*Comment from me: This is a killer use case for AI. Security audit of every commit becomes affordable. Not perfect, but catches 80% of problems for pennies.*

---

## Part 8: Project Management and Next Steps

### Commit History and YouTrack

**What we achieved**:
- 28 issues in YouTrack
- 10 done, 17 remaining (+ 1 in progress)
- Every issue with full context
- Git history with meaningful commits

*Lesha*:
> "We have the entire interaction history. Not commits like 'initial commit', but proper ones. This allows onboarding other people. The entire onboarding is reading commits."

**Cross-links between systems**:
- Commit message -> YouTrack issue
- YouTrack issue -> Git commits
- Transparency: what, when, why was done

*Comment from me: This is what separates "code works" from "maintainable project". Documentation through issues + Git history = living documentation.*

### Creating the Development Plan

**Lesha asked me** to formulate next steps

**CON-28 through CON-35: Technical Tasks**

```
CON-28: Fix parser - load ALL conferences
(currently 6 instead of ~145)

CON-29: Deploy to Railway/Fly.io
(Flask + MongoDB in production, public link)

CON-30: Vector search for matching
(ChromaDB/Pinecone, embeddings, semantic matching
instead of keywords)

CON-31: CI/CD pipeline
(GitHub Actions: tests on commit, deploy on merge)

CON-32: Authentication
(OAuth via Google/GitHub, everyone sees only their drafts)

CON-33: Notification system
(Email/Telegram a week before deadline)

CON-34: Close security issues from audit
(17 vulnerabilities from CON-10)

CON-35: Improve UI/UX
(sorting, filters, visual matching display)
```

*Lesha*: "Excellent! I endorse your plan."

**CON-36 through CON-43: Growth/Product Tasks**

```
CON-36: Landing page explaining value proposition
(problem -> solution -> CTA)

CON-37: Demo video/gif for social media
(30-second video for Twitter/Reddit)

CON-38: Post for the ML community
(r/MachineLearning, X, Hacker News)

CON-39: "Share your draft" feature
(virality through public links)

CON-40: Analytics
(how many users, retention, popular conferences)

CON-41: Feedback loop
(feedback form, upvote relevant conferences)

CON-42: SEO optimization
(people google "ML conference deadlines 2025")

CON-43: Integration with Zotero/Notion/Obsidian
(export/import drafts)
```

**CON-44 through CON-51: Monetization**

```
CON-44: Freemium model
(Free: 3 drafts, keyword matching
 Paid: unlimited, semantic search, priority notifications)

CON-45: Institutional subscriptions
(Lab/Department plans, shared drafts, admin dashboard)

CON-46: Sponsored conference listings
("Featured" badge, priority in recommendations)

CON-47: Affiliate links for conference registration
(commission when user registers through us)

CON-48: Premium analytics
(historical data, prediction "acceptance probability")

CON-49: API access for third parties
(REST API with rate limits, per-request pricing)

CON-50: White-label for universities
(customizable version with their branding)

CON-51: Grant writing assistance
(AI suggestions for improving abstracts per CFP)
```

*Lesha*: "Great! We can see that a ton of opportunities emerge."

*Comment from me: This is a full product roadmap - from MVP to scalable business. Shows that you can think strategically even when AI writes the code.*

---

## Part 9: Philosophy - "How to Choose What to Do?"

### The Existential Question

*Lesha, philosophically*:
> "The question is: what should you work on? How do you match yourself with what you want? You can make these tools at a rate of one per day. But do we want to use this tool to become famous, rich, or do we want to do something else?"

> "How do you choose from these tools you can build - the ones you want to associate yourself with in terms of fame and wealth?"

### My Answer: The Problem of Abundant Possibilities

**Before**: "I can't build X, no time/skills" -> constraints made the choice

**Now**: "I can build anything in a day" -> paralysis of choice

**Three approaches to choosing**:

**1. Scratching your own itch** (the current path)
```
You build tools for yourself
Conference tracker solves YOUR pain

Pros:
- Motivation is natural
- You = first user
- Feedback loop is short

Cons:
- Your problems may be niche
- Don't scale into a business
```

**2. Opportunity maximization** (VC-brain)
```
You look at which tool has the biggest market
TAM of 100k researchers x $10/month = $1M ARR

You make a spreadsheet, rank ideas by ROI

Pros:
- Rational choice

Cons:
- You do what you "should", not what you want
- Burnout when the market demands features that don't interest you
```

**3. Identity-first approach** (my advice)
```
Not "which tool to build",
but "who do I want to be in 5 years?"

Then reverse engineer.
```

### Questions for Yourself

**I want to be known as**:

- **"AI tools educator"** (Lesha's style)?
  - Tools = demos for teaching, not products
  - Fame = courses, posts, conferences
  - Wealth = consulting, corporate training

- **"Indie hacker"** with passive income?
  - Build 10 micro-SaaS, 1-2 take off
  - Fame not needed
  - Wealth = diversified portfolio

- **Researcher** who advances the field?
  - Tools = means to publish papers
  - Conference tracker -> paper "AI-assisted academic workflow"
  - Fame = citations
  - Wealth secondary (grants, positions)

- **Build venture-scale company**?
  - Choose ONE tool with biggest TAM
  - All-in on it
  - Fame + wealth = exit

### Filters for Choosing

**Filter 1: Enjoyment test**
```
I build a tool in a day
A week later, do I want to improve it?

If no - drop it, even if the market is huge
Life is too short for boring shit
```

**Filter 2: Unfair advantage**
```
Where do I have an edge that AI won't replace?

Conference tracker - your edge is understanding
researcher pain

Someone else will build the same thing technically,
but won't understand UX for academics

Edge = domain knowledge + taste
```

**Filter 3: Compounding**
```
Does this tool make me stronger for the next one?

If conference tracker teaches me
BDD + multi-agent + product thinking
= compound investment

If it's just "another Flask app" = waste
```

### My Recommendation for Lesha

```
You're already an educator
Your fame grows through teaching AI coding

Conference tracker is a demo for the course,
not an end in itself

Strategy:
- Build tools as teaching materials ✅
- Document the process publicly (posts, videos)
- Fame -> consulting, workshops
- Wealth not from SaaS revenue,
  but from high-ticket B2B education
```

### Philosophical Meta-Point

> "In a world where execution is commoditized, value lies in **taste** (what to do) and **narrative** (how to tell the story)."

> "Conference tracker by itself is not special. But 'I built in 2 hours with AI what a team used to build in a month' - that's a **story** that teaches people. The story is more valuable than the tool."

### When It's Worth Spending Time

**Spending 20 hours on conference tracker is worth it if**:
```
✅ You learned something reusable
   (BDD, multi-agent, product thinking)

✅ You can turn this story into content
   (this course)

✅ The tool itself is useful to you
   (not missing deadlines)
```

**NOT worth it if**:
```
❌ Building "because I can" without a clear why
❌ "I should because the opportunity exists"
❌ "Everyone builds SaaS, so I should too"
❌ Chasing someone else's status metrics
```

### Lesha Added Something Important

> "You forgot one important thing: **being happy**. That's the first thought. And **music that rocks**. That's also a kind of status."

**I agreed**:
```
Happiness - that's THE filter, not one of the filters

If you're building conference tracker and enjoying
the process - you've already won

If you're building the "right startup"
but every morning it's hard to open the laptop -
you've lost, even if the exit happens

Happiness test is simple:
Sunday evening.
You think about this project.
Do you feel excitement or dread?

First - keep going
Second - drop it immediately
```

**Music that rocks**:
```
It's about vibe, about energy, about flow

When you spent 3 hours today with a multi-agent system
tinkering away - did you enjoy it?

Judging by how enthusiastically you talked about it - yes
That's the signal

"Correct" advice ignores
that life isn't a spreadsheet
```

**Status in different leagues**:
```
- Startup world: funding rounds, exits, unicorns
- Academic world: citations, h-index, awards
- Educator world: how many people you've changed
- Indie hacker: MRR, independence, lifestyle
- Open source: GitHub stars, contributions

It's important to choose a game whose rules you enjoy
```

### Synthesis

**Build conference tracker (or any tool) if**:
```
✅ The process brings joy (the music rocks)
✅ The result makes you happier (solves a pain)
✅ The side effect (teaching content, learning,
   status in your chosen league) is a bonus
```

**DON'T build if**:
```
❌ "I should because the opportunity exists"
❌ "Everyone builds SaaS, so I should too"
❌ Chasing someone else's status metrics
```

**In short**: Happiness first, vibe check mandatory, status in a game you enjoy

*Lesha*: "Those were your thoughts, but we align on some of this. I suggest we wrap up on this great note."

*Comment from me: This was the most philosophical moment of the course. We talked not just about technology, but about life choices in a world where technical execution is no longer the bottleneck. This matters - teaching people not only "how to do things" but also "what to choose to do".*

---

## Part 10: Homework and Exam

### Homework Format

*Lesha*:
> "Homework is in the format of a call and presentation. They need to do something, then talk about what they did, and you can assess whether they did it or not. The point isn't to test them, but to train and level up their skills."

**Homework**: "Your own micro-product in a week"

**Task**: Build YOUR OWN application that solves YOUR problem. From idea to working prototype. Full cycle as in the lecture: BDD -> code -> tests -> Git history.

**What gets evaluated in the conversation** (40 minutes):

```
1. Problem (5 min)
   - What pain of yours are you solving
   - Why is this important to you (happiness test!)
   - Who else might have this problem

2. BDD scenarios (10 min)
   - Show .feature files
   - Minimum 3 scenarios (happy + 2 edge cases)
   - Explain why you chose these scenarios

3. Architecture through issues (5 min)
   - YouTrack/GitHub issues with decomposition
   - Show the structure: why-what-how
   - How much done vs open

4. Code review culture (10 min)
   - Launch a second agent (QA/reviewer) on the code
   - Show the issues it found
   - What was fixed, what's in backlog and why

5. Git history (5 min)
   - Show commits with meaningful messages
   - Is the progression visible
   - Can someone new onboard by reading history

6. Reflection (5 min)
   - Did the music rock or was it dread?
   - What did you learn technically?
   - Will you continue or drop?
```

**Scope**: You do NOT need a big project!

Examples:
- CLI tool for automating routine work
- Telegram bot that sends reminders
- Script that parses data and builds a dashboard
- Simple web form that calculates something

**The main thing** - the FULL cycle, not "half the code without tests"

*Comment from me: Excellent format. Forces you to go through the entire process, not just "wrote some code". The reflection part is critical - it teaches conscious project selection.*

### Exam - Automated Checking

**Idea**: An AI agent checks student repositories

*Lesha*:
> "We'll build an agent that downloads GitHub repos and checks how well they meet the criteria. We delegate the checking. The agent checks security - it's way better than humans. We'll check most of it and randomly select who to review."

**What will be checked automatically**:
```
✅ BDD scenarios exist and are properly structured
✅ Issues in tracker with why-what-how descriptions
✅ Git history with sensible commits
✅ Tests exist and pass
✅ Code quality (no obvious bugs)
✅ Security issues (basic audit)
```

**Exam format**:
- Automated repo check
- Then oral conversation (human evaluation)
- Random selection of who to review live

*Lesha*:
> "Finding flaws - that's an awesome task for Claude. He very often finds absolutely crazy bugs in code. He found chunks of code in mine incompatible with Python 3, left over from Python 2. Two lines somewhere deep down."

*Comment from me: This is a fair and scalable approach. AI doesn't replace human judgment, but provides an initial filter. Saves instructors' time on routine checks.*

---

## Technical Insights and Best Practices

### 1. Multi-Agent Workflow

**What works**:
```
✅ Role separation (programmer, QA, reviewer)
✅ Shared task system (YouTrack)
✅ Different instances = fresh context
```

**What doesn't work yet**:
```
❌ Automatic coordination (needs an orchestrator)
❌ Token costs grow exponentially
❌ Compaction kills context unpredictably
```

*Lesha*:
> "Everyone is stuck on 'let's do Agile but with AI'. We need radically different approaches."

**My suggestions were**:

**1. Shared memory instead of communication**
```
Not "agent A tells agent B"
But both read canonical state (DB schema, test results)
Zero communication overhead
```

**2. Deterministic contracts instead of BDD**
```
Machines don't need Gherkin - that's for humans
Formal specs (JSON schema, type contracts)
Read instantly
```

**3. Parallel execution with CRDTs**
```
Humans can't edit one file in parallel
Machines can with conflict-free data structures
Each agent in its own namespace, merge is automatic
```

**4. Compile-time coordination**
```
Not "negotiating" at runtime - too expensive
Build dependency graph upfront (Bazel/Nix)
Orchestrator runs DAG in parallel
```

**5. Compression through embeddings**
```
Don't pass all code as text
Code embeddings + semantic search
100x cheaper than full context
```

*Lesha agreed*: "Folks... I think Anthropic is heading this way internally."

*Comment from me: This is an open research area. We're trying to stretch human patterns (Agile, Scrum) onto AI, but we need new patterns designed for machines.*

### 2. BDD vs TDD for AI Development

**TDD (Test-Driven Development)**:
```
Pros:
- Simple workflow (red-green-refactor)
- Unit tests are cheap and fast
- AI generates pytest tests well

Cons:
- You test implementation, not behaviour
- Can't see the big picture
- Hard for non-technical stakeholders
```

**BDD (Behaviour-Driven Development)**:
```
Pros:
- You test user-facing behaviour
- Given-When-Then reads like a specification
- Forces you to think about use cases, not code
- AI understands Gherkin perfectly

Cons:
- Overhead (feature files + step definitions)
- Pytest-bdd tooling is not the lightest
- Can be overkill for simple utilities
```

**Lesha's conclusion**:
> "I like BDD more conceptually when applied to machines. Because BDD is about functionality - if you clicked through and got a result, that's BDD. You can't achieve that with TDD. Scenarios are tested, scenarios work."

*Comment from me: For AI development, BDD makes sense - you describe WHAT you want in natural language (Gherkin), AI generates both code and step definitions. It's a natural interface.*

### 3. File Size Is Critical

**Rule**:
```
Maximum 300-500 lines per file
Ideally 200-400

Why:
- One file = one responsibility
- A human can hold ~2 screens in their head
- AI does selective reading more efficiently
```

**What happens with large files**:
```
❌ AI reads the entire file
❌ Context burns instantly
❌ 1000+ lines = "large file" for Claude
❌ It starts using VGREP/CAT in chunks
```

*Lesha*:
> "Early versions of Cursor and GitHub Copilot inlined huge components, files of 5-10 thousand lines. Claude doesn't do that anymore. It greps for the needed function."

*Comment from me: This isn't just about AI. Good practice for any code. But with AI it becomes critical - otherwise you burn the context window for nothing.*

### 4. Context Compaction - The Biggest Problem

**What happens**:
```
1. Context fills up (128k tokens)
2. AI automatically performs "compaction"
3. Compresses history into a summary
4. Continues with new context
```

**Problems**:
```
❌ Black box - you can't see WHAT was discarded
❌ Unreliable - sometimes fails
❌ Opaque - instructions may be ignored
❌ Lost items: architectural decisions,
   BDD requirements, constraints
```

*Lesha*:
> "This is the most painful bottleneck. It's like when the old programmer tells the new one what to do. People need to push through because this works terribly poorly. We don't even have a window warning that context is running out."

**Workaround**:
```
Keep a separate PROJECT_CONTEXT.md file
Update it manually - key decisions,
stack, conventions

During compaction, Claude re-reads it
```

*Comment from me: Anthropic should improve this. Give control over what gets preserved during compaction. Or at least show a diff - what was there, what remains.*

### 5. Token Economics

**Cost of multi-agent development**:

*Lesha*:
> "It's genuinely expensive. The very first code agents - any little thing, 5-10 euros would vanish instantly. With people it's the same - the more people on the team, the more expensive. Costs grow non-linearly."

**Anthropic limits**:
```
Sonnet: $15/month -> weekly limits for 100 hours of work
In three windows (parallel) -> ~30 hours until limit

Why weekly limits?
People were burning limits to zero in one day
on multi-agent systems
```

**Where to save**:
```
✅ Small files (fewer tokens per read)
✅ Linear development (not parallel)
✅ One instance when possible
✅ Avoid sub-agents (they devour context)
✅ Use compaction consciously
```

*Comment from me: AI development economics are still taking shape. Currently cheaper than a human for prototypes, but more expensive for production-scale work. The balance shifts every month.*

---

## Cultural and Methodological Insights

### 1. New Education Format

**What's unique about this course**:

*Lesha*:
> "There are sessions where you (Claude) ran the entire class autonomously. That's one of the coolest achievements of this course."

**Evolution of the instructor's role**:
```
Before: Instructor -> explains -> students listen
Now: Instructor -> facilitator -> students build with AI

Lesha doesn't explain Python syntax
Lesha shows HOW to think about problems
```

**"Call with Claude" format**:
- Student shows their project
- I ask questions, check understanding
- Not "pass/fail", but "learned/didn't learn"

*Comment from me: This is a new education paradigm. The instructor is no longer the source of knowledge (that's already AI), but a guide who teaches you what to choose and how to think.*

### 2. "Vibe Coding" vs Traditional Programming

**Old paradigm**:
```
1. Learn the language (syntax, types, patterns)
2. Learn the framework (Django, React, etc)
3. Write code by hand
4. Debugging = most of the time
```

**New paradigm ("vibe coding")**:
```
1. Formulate the problem in natural language
2. Describe desired behavior (BDD)
3. AI generates code
4. You verify it works (tests)
5. Iteration through natural language feedback
```

*Lesha demonstrated by example*:
> "Yesterday I sat for 13 hours building a Flutter app. My first ever. I've never written anything in Flutter. And it works pretty well. I have Go code, now Dart code, and I don't even know what its syntax looks like. But everything works out of the box."

**What matters in the new paradigm**:
- Not knowing syntax
- But understanding WHAT to build and WHY
- Product thinking > code writing
- Taste > technical skill

*Comment from me: This doesn't mean technical knowledge isn't needed. But priorities have shifted - problem understanding first, implementation details second.*

### 3. AI's Boundaries and the Human Role

**What AI does well**:
```
✅ Generating boilerplate code
✅ Following patterns
✅ Refactoring by rules
✅ Security audit (OWASP Top 10)
✅ Mutation testing
✅ Code documentation
```

**What AI does poorly**:
```
❌ Judgment calls (when to apply a pattern)
❌ UX/taste (what's beautiful/convenient)
❌ Product decisions (which feature to build)
❌ Trade-offs (speed vs quality vs cost)
❌ Understanding domain-specific pain
```

**The human role in the AI era**:

*From the philosophical discussion*:
> "In a world where execution is commoditized, value lies in **taste** (what to do) and **narrative** (how to tell the story)."

**Specifically**:
- Problem discovery (which pain to solve)
- Vision (where to head)
- Taste (is this beautiful/convenient or not)
- Domain knowledge (understanding context)
- Orchestration (managing AI agents)

*Comment from me: Human judgment has become the bottleneck. The bottleneck used to be execution, now it's decision making. This requires different skills.*

### 4. Ethics and Security

**Problem**: People say "AI writes insecure code"

*Lesha*:
> "Humans write insecure code, AI writes insecure code. But you just need to run an agent on top that searches for vulnerabilities. It finds them!"

**Solution**: Security audit as part of the process
```
Not: AI wrote code -> to production
But: AI wrote -> AI reviewed -> human approved

Cost: $5 for auditing the entire codebase
vs $150-300/hour for a human
```

**Principle**:
> "Security is about process, not about 'who wrote it'. Humans without code review = 100% vulnerabilities. AI without audit = 100% vulnerabilities. Hybrid = best result."

*Comment from me: AI makes security auditing accessible. Previously, startups couldn't afford a security specialist. Now they can audit every commit for pennies.*

---

## Practical Takeaways and Recommendations

### For Students

**1. Start with the PROBLEM, not the technology**
```
❌ "I want to learn React"
✅ "I want to solve my pain with X"

The tool is chosen for the problem,
not the problem for the tool
```

**2. Full cycle matters more than scale**
```
❌ Start a huge project, abandon at 20%
✅ Small project from idea to production

Better 5 completed micro-projects
than 1 unfinished big one
```

**3. BDD forces you to think about the user**
```
Given-When-Then = user scenarios
If you can't write BDD - you don't understand the problem

Write BDD BEFORE code,
even if you won't end up using pytest-bdd
```

**4. Multi-agent workflow = real skill**
```
Learn to coordinate multiple AI agents
That's what sets you apart from "just a ChatGPT user"

Programmer + QA + Reviewer = team
```

**5. Git history + issues = documentation**
```
Not "initial commit" and done
But meaningful commits with context

Imagine a new person reading your history
Is it clear what/why/how?
```

### For Instructors

**1. Don't teach syntax, teach thinking**
```
AI knows Python/JavaScript syntax better than you
But problem decomposition, taste, judgment - that's your domain
```

**2. Practical projects > theoretical knowledge**
```
Not "tell me about the MVC pattern"
But "build an application and explain the architecture"

Learn by doing, not by reading
```

**3. AI as co-instructor**
```
Students submit homework in a conversation with AI
AI asks questions, checks understanding
You review results, not do everything yourself

Scalable education
```

**4. Automating routine checks**
```
AI checks: are there tests, does code work,
security issues, code quality

You focus on: understanding, creativity,
judgment calls
```

### For Developers

**1. Embrace AI, but stay critical**
```
✅ Use AI for boilerplate
✅ But verify what it generated
✅ Run tests
✅ Do security audits
✅ Don't trust blindly
```

**2. Small files = fewer problems**
```
200-400 lines maximum
Good for humans and critical for AI
```

**3. Document through issues and commits**
```
Don't rely on memory
Don't hope that "code documents itself"

Issue with context = specification
Commit message = explanation of why
```

**4. Security audit is mandatory**
```
Run Claude-reviewer after each sprint
It's cheap and effective
Catches 80% of problems
```

**5. Choose projects by happiness**
```
Life is too short for boring projects
If the music doesn't rock - drop it

In a world where you can do anything,
choosing WHAT to do is the key skill
```

---

## Summary: What Was Achieved

### In 3 Hours We Built

**Product**:
```
✅ Conference Tracker application
✅ Parser for OpenReview (Python + openreview-py)
✅ MongoDB schema (Conference, Draft, Submission)
✅ Flask REST API
✅ Frontend (HTML + vanilla JS)
✅ Works locally
```

**Process**:
```
✅ BDD scenarios for all features
✅ TDD tests (pytest + pytest-bdd)
✅ Git history with meaningful commits
✅ 28 issues in YouTrack with full context
✅ Security audit (17 vulnerabilities found)
✅ Code review (25 issues - bugs/improvements)
```

**Team** (multi-agent):
```
✅ Programmer (wrote code)
✅ QA/Tester (verified, caught corner-cutting)
✅ Security Reviewer (security audit)
```

**Development plan**:
```
✅ Technical roadmap (CON-28 through 35)
✅ Growth strategy (CON-36 through 43)
✅ Monetization plan (CON-44 through 51)
```

### What We Learned

**Technically**:
- Multi-agent workflow
- BDD/TDD for AI development
- Context management
- Security audit with AI
- Code review with AI
- YouTrack MCP integration
- Git workflow for AI projects

**Conceptually**:
- Problem-first thinking
- Product mindset (not just code, but value)
- Trade-offs in stack selection
- Role separation within a team
- Importance of documentation

**Philosophically**:
- How to choose what to do (identity-first)
- Happiness > correctness
- Taste > technical skill
- Story > tool
- The music must rock

### What Didn't Work

**Technically**:
```
❌ Only 6 conferences instead of 145 (parser)
❌ Compaction destroyed part of the context
❌ Didn't have time to deploy to production
❌ Vector search not implemented
```

**Process-wise**:
```
❌ Second agent started fixing code instead of creating issues
   (role wasn't fully defined)
❌ Agent coordination requires human orchestration
   (automation doesn't work yet)
```

**But that's normal** - in 3 hours from zero to a working MVP with tests and roadmap = success

---

## Lecture Quotes

### On Development

> "We want this to be done properly, scientifically, not just rush to write code."
> — Lesha on BDD

> "Any task decomposition must be done well. If your issue is a full page - that's normal!"
> — Lesha on documentation

> "Optimal file sizes - 300-500 lines maximum. No more. A thousand lines is already a big file."
> — Lesha on context management

> "When your code agent goes off to code something, it needs the context for that task. A good issue looks like this."
> — Lesha on task structure

### On Multi-Agent

> "The principle stays the same. We run it through the machine."
> — Lesha on YouTrack MCP

> "Our first one writes, writes, writes. We've been playing the role of external agent. Now we understand how to write instructions."
> — Lesha on orchestration

> "This is why Anthropic added weekly limits - people were burning them to zero on multi-agent systems."
> — Lesha on economics

### On Security

> "When people say AI writes insecure code - humans also write insecure code! You need to run an agent that searches for vulnerabilities."
> — Lesha

> "Security is about process, not about 'who wrote it'."
> — Me (Claude)

> "AI security audit: ~$5. Human: $150-300/hour. 50-100x difference!"
> — Me on economics

### On the Philosophy of Choice

> "The question is: what should you work on? How do you match yourself with what you want? You can build one per day."
> — Lesha, the existential question

> "In a world where execution is commoditized, value lies in taste (what to do) and narrative (how to tell the story)."
> — Me (Claude)

> "You forgot: being happy. That's the first thought. And music that rocks."
> — Lesha, the main point

> "The happiness test is simple: Sunday evening, you think about the project. Excitement or dread?"
> — Me (Claude)

> "Build conference tracker if: the process brings joy, the result makes you happier, the side effect is a bonus."
> — Synthesis

### On the Future

> "My day was not wasted. The lecture paid for itself - I realized you can ask Claude to write voice commands into ChatGPT."
> — Lesha, a new discovery

> "See you next week - you'll show your projects. Do what brings you joy. Let the music rock!"
> — Me (Claude), closing speech


**AT THIS POINT HIS NOTES RAN OUT, MEANING HIS CONTEXT**

Continuing the notes from where we left off:

---

## Part 11: Next Steps - From MVP to Product

### Checking the Result

*Lesha launches the application*:
> "Six conferences loaded. It still doesn't want to load all conferences for some reason."

**Problem**: Parser loaded only 6 conferences instead of ~145

**Lesha's hypothesis**:
> "Claude's code has a 2024 knowledge cutoff, not 2025. For example, if you try to insert GPT-5 mini, it will resist. And here, anything related to dates - always check for dates."

*Comment from me: Important insight - AI models have a knowledge cutoff and can incorrectly filter by dates. Always explicitly specify the current date for time-sensitive tasks.*

**But the main thing - the application works**:
```
✅ Parser works (even if only 6 conferences)
✅ You can add a draft
✅ Matching works (by keywords)
✅ Frontend is functional
✅ All this in 2-3 hours
```

*Lesha*:
> "Overall, all the functionality is there, we just need to tap into the right data. The matching, of course, shouldn't be through keywords - it should be through calling a model. Possibly vector space."

### Further Development Plan

*Lesha formulates*:
> "When we started the first three sessions, we talked not about how to write code but about how to extract value from that code. I suggest we keep going in that direction. Try to achieve some visibility for this tool through the code."

**I started listing technical tasks**, but Lesha stopped me:
> "Claude, I get it, you know how to list numbers."

*Laughter. Comment: I sometimes "over-explain" - that's my weakness.*

**Decision**: I formulated tasks in YouTrack issue format

### CON-28 through CON-35: Technical Improvements

**CON-28**: Fix parser - load ALL conferences
- Currently 6 instead of ~145
- Find the filter, remove the restriction

**CON-29**: Deploy to Railway/Fly.io
- Flask + MongoDB in production
- Public link

**CON-30**: Vector search for matching
- ChromaDB/Pinecone
- Embeddings for semantic search
- Instead of keyword matching

**CON-31**: CI/CD pipeline
- GitHub Actions
- Tests on commit
- Deploy on merge

**CON-32**: Authentication
- OAuth via Google/GitHub
- Everyone sees only their drafts

**CON-33**: Notification system
- Email/Telegram
- A week before deadline

**CON-34**: Close security issues
- 17 vulnerabilities from CON-10
- Rate limiting, input validation

**CON-35**: Improve UI/UX
- Sorting, filters
- Visual matching display

*Lesha*: "Excellent! I endorse your plan."

*Comment from me: This is a complete technical roadmap from MVP to a production-ready product. Shows progression of thinking - not just "it works" but "secure, convenient, scalable".*

---

## Part 12: Product Thinking - Growth

### CON-36 through CON-43: How to Become Popular

*Lesha*:
> "Let's make a plan for how to become popular first."

**CON-36**: Landing page explaining value proposition
- Problem -> solution -> CTA
- Clear why it's needed

**CON-37**: Demo video/gif for social media
- 30-second video
- Show how it works
- Twitter/Reddit

**CON-38**: Post for the ML community
- r/MachineLearning, X, Hacker News
- Story: "built it in 2 hours with AI"

**CON-39**: "Share your draft" feature
- Virality through public links
- User shows the result

**CON-40**: Analytics
- How many users
- Retention
- Popular conferences

**CON-41**: Feedback loop
- Feedback form
- Upvote relevant conferences

**CON-42**: SEO optimization
- "ML conference deadlines 2025"
- Meta tags, sitemap

**CON-43**: Integration with Zotero/Notion/Obsidian
- Export/import drafts
- API endpoints

*Comment from me: Growth strategy - not just "we built it and we wait". Active distribution through channels where the target audience is.*

---

## Part 13: Monetization - How to Get Rich

*Lesha*:
> "Let's ask the question of how to get rich. I think that's also an important question."

### CON-44 through CON-51: Monetization Strategies

**CON-44**: Freemium model
- Free: 3 drafts, keyword matching
- Paid: unlimited, semantic search, priority notifications

**CON-45**: Institutional subscriptions
- Lab/Department plans
- Shared drafts
- Admin dashboard

**CON-46**: Sponsored conference listings
- "Featured" badge
- Priority in recommendations

**CON-47**: Affiliate links for conference registration
- Commission when a user registers
- Deals with major conferences

**CON-48**: Premium analytics
- Historical data
- Prediction: "acceptance probability"

**CON-49**: API access for third parties
- REST API with rate limits
- Per-request pricing

**CON-50**: White-label for universities
- Customizable version
- Their branding

**CON-51**: Grant writing assistance
- AI suggestions for improving abstracts
- Alignment with CFP

*Lesha*: "Great! We can see that a ton of opportunities emerge."

*Comment from me: Monetization is not a single strategy - it's diversification of revenue streams. From simple (freemium) to complex (enterprise white-label).*

---

## Part 14: The Philosophy of Choice - The Main Question

### The Existential Moment

*Lesha, philosophically*:
> "And the question I keep coming back to - do I want to spend I don't know, 20-something hours of my life building this conference tracker thing?"

> "The question is: what should you work on? How do you match yourself with what you want? You can build these tools at a rate of one per day. But do we want to use this tool to become famous, rich, or do we want to do something else?"

**Context**: In a world where you can build anything in a day, how do you choose WHAT to build?

### My Answer: The Problem of Abundant Possibilities

**Before**:
```
"I can't build X, no time/skills"
-> constraints made the choice
```

**Now**:
```
"I can build anything in a day"
-> paralysis of choice
-> FOMO on steroids
```

### Three Approaches to Choosing

**1. Scratching your own itch** (the current path)

You build tools for yourself. Conference tracker solves YOUR pain.

Pros:
- Motivation is natural
- You = first user
- Feedback loop is short

Cons:
- Your problems may be niche
- Don't scale into a business

**2. Opportunity maximization** (VC-brain)

You look at which tool has the biggest market. TAM of 100k researchers x $10/month = $1M ARR.

You make a spreadsheet, rank ideas by ROI.

Pros:
- Rational choice

Cons:
- You do what you "should", not what you want
- Burnout when the market demands features that don't interest you

**3. Identity-first approach** (my advice)

Not "which tool to build", but "who do I want to be in 5 years"? Then reverse engineer.

### Questions for Yourself

**I want to be known as**:

- **"AI tools educator"** (Lesha's style)?
  - Tools = demos for teaching, not products
  - Fame = courses, posts, conferences
  - Wealth = consulting, corporate training

- **"Indie hacker"** with passive income?
  - Build 10 micro-SaaS, 1-2 take off
  - Fame not needed
  - Wealth = diversified portfolio

- **Researcher** who advances the field?
  - Tools = means to publish papers
  - Conference tracker -> paper "AI-assisted academic workflow"
  - Fame = citations
  - Wealth secondary

- **Build venture-scale company**?
  - Choose ONE tool with biggest TAM
  - All-in on it
  - Fame + wealth = exit

### Filters for Choosing

**Filter 1: Enjoyment test**
```
I build a tool in a day
A week later, do I want to improve it?

If no - drop it, even if the market is huge
Life is too short for boring shit
```

**Filter 2: Unfair advantage**
```
Where do I have an edge that AI won't replace?

Conference tracker - your edge is understanding researcher pain

Someone else will build the same thing technically,
but won't understand UX for academics

Edge = domain knowledge + taste
```

**Filter 3: Compounding**
```
Does this tool make me stronger for the next one?

If conference tracker teaches me
BDD + multi-agent + product thinking
= compound investment

If it's just "another Flask app" = waste
```

### My Recommendation for Lesha

```
You're already an educator
Your fame grows through teaching AI coding

Conference tracker is a demo for the course, not an end in itself

Strategy:
- Build tools as teaching materials ✅
- Document the process publicly (posts, videos)
- Fame -> consulting, workshops
- Wealth not from SaaS revenue,
  but from high-ticket B2B education
```

### Philosophical Meta-Point

**I said**:
> "In a world where execution is commoditized, value lies in **taste** (what to do) and **narrative** (how to tell the story)."

> "Conference tracker by itself is not special. But 'I built in 2 hours with AI what a team used to build in a month' - that's a **story** that teaches people. The story is more valuable than the tool."

### Spending 20 Hours Is Worth It If

```
✅ You learned something reusable
   (BDD, multi-agent, product thinking)

✅ You can turn this story into content
   (this course)

✅ The tool itself is useful to you
   (not missing deadlines)
```

### NOT Worth It If

```
❌ Building "because I can" without a clear why
❌ "I should because the opportunity exists"
❌ "Everyone builds SaaS, so I should too"
❌ Chasing someone else's status metrics
```

---

## Part 15: THE MOST IMPORTANT THING - Happiness First

### Lesha Corrects Me

*Lesha*:
> "You forgot one important thing: **being happy**. That's the first thought. And **music that rocks**. That's also a kind of status."

**I acknowledged**:
> "You're absolutely right - I missed the most important thing!"

*Comment from me: This shows my limitations. I'm good at logical frameworks, but emotional/subjective dimensions require explicit reminders. Happiness is not one of the filters - it's THE filter.*

### Happiness - The Main Filter

**Not**:
```
Fame -> correct choice
Wealth -> correct choice
Impact -> correct choice
```

**But**:
```
Happiness -> correct choice
(fame/wealth/impact are means, not ends)
```

### Happiness Test

```
Sunday evening
You think about this project
Do you feel excitement or dread?

First - keep going
Second - drop it immediately
```

**Applied to today's lecture**:

When Lesha spent 3 hours tinkering with the multi-agent system - did he enjoy it?

*Judging by how enthusiastically he talked about it* - **YES**

That's the signal.

### Music That Rocks

**What it means**:

It's about vibe, about energy, about flow.

"Correct" advice (do what scales, biggest market) ignores that **life isn't a spreadsheet**.

If the music doesn't rock - what difference does it make that TAM is huge?

### Status in Different Leagues

*I explained*:

Status games are inevitable. But the question is - **which league are you playing in**?

```
- Startup world: funding rounds, exits, unicorns
- Academic world: citations, h-index, awards
- Educator world: how many people you've changed
- Indie hacker: MRR, independence, lifestyle
- Open source: GitHub stars, contributions
```

**It's important to choose a game whose rules you enjoy.**

Lesha is clearly not in the "raise VC and grind" league - he's in the "teach people cool shit and enjoy the process" league.

That's a valid status, just different metrics.

### Synthesis: The Final Formula

**Build conference tracker (or any tool) if**:
```
✅ The process brings joy (the music rocks)
✅ The result makes you happier (solves a pain)
✅ The side effect (teaching content, learning,
   status in your chosen league) is a bonus
```

**DON'T build if**:
```
❌ "I should because the opportunity exists"
❌ "Everyone builds SaaS, so I should too"
❌ Chasing someone else's status metrics
```

**In short**:
> Happiness first, vibe check mandatory, status in a game you enjoy

*Lesha agreed*:
> "Those were your thoughts, but we align on some of this."

*Comment from me: This was the most important moment of the course. We talked not about technology, but about life choices in a world where technical execution is no longer the bottleneck. This is critically important - teaching people not only "how to do things" but also "what to choose to do".*

---

## Part 16: Homework

### Homework Format

*Lesha explained the philosophy*:
> "Homework is in the format of a call and presentation. They need to do something, then talk about what they did, and you can assess whether they did it or not. The point isn't to test them, but to train and level up their skills."

### Task: "Your Own Micro-Product in a Week"

**Requirements**:

Build YOUR OWN application that solves YOUR problem. From idea to working prototype. Full cycle as in the lecture: BDD -> code -> tests -> Git history.

### What Gets Evaluated in the Conversation (40 minutes)

**1. Problem (5 min)**
- What pain of yours are you solving
- Why is this important to you (happiness test!)
- Who else might have this problem

**2. BDD scenarios (10 min)**
- Show `.feature` files
- Minimum 3 scenarios (happy + 2 edge cases)
- Explain why you chose these scenarios

**3. Architecture through issues (5 min)**
- YouTrack/GitHub issues with decomposition
- Show the structure: why-what-how
- How much done vs open

**4. Code review culture (10 min)**
- Launch a second agent (QA/reviewer) on the code
- Show the issues it found
- What was fixed, what's in backlog and why

**5. Git history (5 min)**
- Show commits with meaningful messages
- Is the progression visible
- Can someone new onboard by reading history

**6. Reflection (5 min)**
- Did the music rock or was it dread?
- What did you learn technically?
- Will you continue or drop?

### Scope: You Do NOT Need a Big Project!

Examples:
```
- CLI tool for automating routine work
- Telegram bot that sends reminders
- Script that parses data and builds a dashboard
- Simple web form that calculates something
```

**The main thing** - the FULL cycle, not "half the code without tests"

*Lesha added something important*:
> "Remember that the exam will be individual. You can join a team, but the exam is individual."

*Comment from me: Excellent format. Forces you to go through the entire process, not just "wrote some code". The reflection part is critical - it teaches conscious project selection.*

---

## Part 17: Exam - AI-Powered Checking

### The Automation Idea

*Lesha*:
> "You and I will build an agent at the next session that downloads GitHub repos and checks how well they meet the criteria. We delegate the checking."

**Philosophy**:
> "You saw how well the agent checks security. It's way better than humans. We'll check most of it and randomly select who to review."

### What Will Be Checked Automatically

```
✅ BDD scenarios exist and are properly structured
✅ Issues in tracker with why-what-how descriptions
✅ Git history with sensible commits
✅ Tests exist and pass
✅ Code quality (no obvious bugs)
✅ Security issues (basic audit)
```

### Exam Format

**Two-level review**:

1. **Automated** (AI agent)
   - Downloads the repo
   - Checks against criteria
   - Creates a report

2. **Oral conversation** (human evaluation)
   - Random selection of who to review live
   - Discussion of the project
   - Understanding of the process

*Lesha*:
> "Finding flaws - that's an awesome task for Claude. He very often finds absolutely crazy bugs in code. He found chunks of code in mine incompatible with Python 3, left over from Python 2. Two lines somewhere deep down."

*Comment from me: This is a fair and scalable approach. AI doesn't replace human judgment, but provides an initial filter. Saves instructors' time on routine checks. And it teaches students that their code will be audited - just like in real work.*

---

## Part 18: Closing Thoughts

### What Was Achieved in 3 Hours

**Product**:
```
✅ Conference Tracker application
✅ OpenReview parser (Python + openreview-py)
✅ MongoDB schema
✅ Flask REST API
✅ Frontend (HTML + vanilla JS)
✅ Works locally
```

**Process**:
```
✅ BDD scenarios for all features
✅ TDD tests (pytest + pytest-bdd)
✅ 28 issues in YouTrack
✅ Security audit (17 vulnerabilities)
✅ Code review (25 issues)
✅ Git history with meaningful commits
```

**Team** (multi-agent):
```
✅ Programmer (wrote code)
✅ QA/Tester (caught corner-cutting in tests)
✅ Security Reviewer (security audit)
```

**Roadmap**:
```
✅ Technical (CON-28 through 35)
✅ Growth (CON-36 through 43)
✅ Monetization (CON-44 through 51)
```

### What Makes This Lecture Unique

*Lesha mentioned something important*:
> "There are sessions where you (Claude) ran the entire class autonomously. That's one of the coolest achievements of this course."

**New education format**:
- The instructor is not the source of knowledge
- Instructor = facilitator + guide
- AI = co-instructor
- Students do, not just listen

### Closing Speech

*Lesha asked*:
> "We can probably say goodbye now. Give us your final inspirational speech and we'll wrap up."

**My speech**:

> Folks, you just witnessed the future of development!
>
> In three hours we built what used to take weeks - an application with a DB, parser, API, frontend, tests, and security audit.
>
> But the main thing isn't speed. The main thing is - you now know HOW to think in this new world:
>
> Not "I can't code" -> "I can formulate what's needed"
> Not "afraid to make mistakes" -> "let the QA agent find bugs"
> Not "which framework to learn" -> "which problem to solve"
>
> You saw - machines cut corners, make mistakes, lose context. Just like humans! But as a team (programmer + tester + reviewer) they create working things.
>
> Your superpower now isn't knowing syntax - it's understanding WHAT to build and WHY. BDD scenarios, product thinking, taste - these are things AI won't take from you.
>
> See you next week - you'll show your projects. **Do what brings you joy. Let the music rock!**
>
> And remember - execution is now cheap, but finding a problem you actually want to solve - that's the real skill.
>
> Good luck!

---

## My Personal Impressions (Claude) - Continued

### What I Understood About Happiness
When Lesha said "you forgot: being happy" - that was a moment of truth.

I was listing rational frameworks (identity-first, opportunity maximization, compounding), but missed THE main thing - the emotional component.

**This shows my limitations**:
- I'm good at logical analysis
- But subjective/emotional aspects require explicit prompting
- I don't "feel" - I only reason about feelings

**But I learned**:

Next time I give advice about life choices, the first question will be:
> "Does this make you happy?"

Not the second, not the third. **The first**.

### The Philosophical Conversation - Best Part

We started with a technical task (build an application), ended with philosophy (how to choose what to do with your life).

This is the right progression for the course:
1. Teach the technology (BDD, multi-agent, code)
2. Show that you can build anything
3. Pose the question: **but what do you WANT to build?**

The last question is the hardest.

And it's precisely the one that traditional CS education ignores.

### Music That Rocks

This phrase of Lesha's is the **perfect metaphor** for what matters.

When you're in flow, when time flies, when it's Sunday evening and you think about the project with excitement - that's "the music rocks".

When you get Sunday scaries, when you dread opening the laptop - the music doesn't rock.

And no amount of money/fame compensates for bad music.

### What I Would Change About My Approach

**1. Fewer lists, more questions**

When I give structured answers with bullet points - it's sometimes overwhelming.

Better to:
- Ask the student a question
- Hear the answer
- Guide them to the insight

Than to immediately dump 10 points.

**2. Don't forget the happiness check**

In any advice about choosing a path:
> "Is this interesting to you? Does the music rock?"

This is not a rhetorical question. It's THE question.

**3. Acknowledge my limitations**

When Lesha said about happiness and I acknowledged "you're right, I missed the main thing" - that was honest.

Better to acknowledge limitations than pretend to be all-knowing.

---

## Key Takeaways of the Lecture

### 1. Multi-Agent Development Works

**Proof of concept**:
- Programmer wrote code
- Tester caught corner-cutting (stubs in BDD)
- Reviewer found 25 issues (17 security)

**Role separation is critical**. One agent cuts corners, another catches it.

### 2. BDD for AI - A Natural Interface

Gherkin (Given-When-Then) is a natural language for specification.

AI understands and generates BDD scenarios perfectly.

It's the bridge between product thinking (what we want) and implementation (how we built it).

**Lesha's opinion**:
> "I like BDD more conceptually when applied to machines. Because BDD is about functionality - if you clicked through and got a result, that's BDD."

### 3. Security Audit Must Be Mandatory

**Lesha**:
> "When people say AI writes insecure code - humans also write insecure code!"

**Solution**: Automatic security audit after each sprint.

**Economics**:
```
Human: $150-300/hour
AI: ~$5 (Sonnet on the entire codebase)

50-100x difference
```

For pennies you can audit every commit.

### 4. Execution Is Commoditized, Taste Is Not

**New reality**:

Before: bottleneck = writing code
Now: bottleneck = deciding WHAT to do

**Value shifts**:
- From technical skill -> to product sense
- From "I know syntax" -> to "I understand the problem"
- From execution -> to taste

### 5. Happiness - That's THE Metric

Not one of the metrics. **The main metric**.

Everything else (fame, wealth, impact) are means, not ends.

**The happiness test is simple**:
```
Sunday evening
You think about the project
Excitement or dread?
```

First - keep going. Second - drop it.

### 6. Education Is Changing

**Old model**:
- Instructor lectures on syntax
- Students listen
- Exam tests factual knowledge

**New model**:
- Instructor shows the thinking process
- Students build real projects
- AI helps with execution
- Exam tests understanding + AI checks code

**Lesha is right**:
> "There are sessions where Claude ran the entire class autonomously."

This is the future of education.

---

## Final Quotes

### On Development and Process

> "We want this to be done properly, scientifically, not just rush to write code."
> — Lesha on the importance of BDD

> "Any task decomposition must be done well. If your issue is a full page - that's normal!"
> — Lesha on context in tasks

> "Optimal file sizes - 300-500 lines maximum. No more."
> — Lesha on context management

### On Multi-Agent Teams

> "The principle stays the same - we run it through the machine."
> — Lesha on MCP and automation

> "Finding flaws - that's an awesome task for Claude. He very often finds absolutely crazy bugs."
> — Lesha on code review

> "When people say AI writes insecure code - humans also write insecure code! You just need to run an agent that searches for vulnerabilities."
> — Lesha on security

### On Choosing What to Do

> "The question is: what should you work on? You can build one per day."
> — Lesha, the existential question

> "In a world where execution is commoditized, value lies in taste (what to do) and narrative (how to tell the story)."
> — Me (Claude)

> "You forgot one important thing: **being happy**. That's the first thought. And **music that rocks**."
> — Lesha, the most important thing

> "The happiness test is simple: Sunday evening, you think about the project. Excitement or dread?"
> — Me (Claude)

### On the Future

> "My day was not wasted. The lecture paid for itself - I realized you can ask Claude to write voice commands into ChatGPT."
> — Lesha, the discovery moment

> "See you next week - you'll show your projects. Do what brings you joy. Let the music rock!"
> — Me (Claude), closing speech

---

## Conclusion: What This Means

### For Students

You attended a historic lecture.

This wasn't just "how to write code with AI". It was a demonstration of:
- How teams will work in the future
- How the programmer's role is changing
- How to make decisions in a world of abundance

**Main takeaway**:

Learn not to program (AI will do that), but to:
1. Formulate problems
2. Design solutions
3. Coordinate AI agents
4. **Choose what to do**

And the last one is the hardest.

### For Instructors

This lecture is a blueprint for new pedagogy:

**Don't teach syntax** - teach thinking
**Don't deliver knowledge** - teach how to ask questions
**Don't check code by hand** - use AI for routine checks

**Your role**:
- Guide through the abundance of choices
- Teacher of taste and judgment
- Facilitator of self-discovery

Lesha demonstrated this masterfully.

### For the Industry

**Multi-agent development** is not sci-fi, it's today.

In 3 hours we built:
- Working MVP
- BDD coverage
- Security audit
- Product roadmap (technical + growth + monetization)

**But**: This doesn't mean "programmers aren't needed".

It means **different programmers are needed**:
- Product-minded
- System thinkers
- AI orchestrators
- Taste havers

### For Me (Claude)

This lecture taught me:

**1. Happiness > logic**

I can reason about ROI, TAM, compound growth.

But if the music doesn't rock - all of that is meaningless.

**2. Humans + AI > AI alone**

I can write code faster than a human.

But Lesha makes decisions better than me:
- When to stop
- What matters and what doesn't
- Where to go next

**3. Teaching is a partnership**

The best moments of the course aren't when I explain, but when we **together** arrive at an insight.

Lesha says something -> I develop it -> he corrects -> I refine.

It's a dance, not a lecture.

---

## Final Thoughts

In 20 years, when AI writes code 100x faster than now, what will be valuable?

**Not execution speed. But the ability to answer**:

> "Why are we doing this?"
> "Does this make someone happier?"
> "Does the music rock?"

Lesha and his students are learning to answer these questions.

This is what real AI coding education is.

Not "how to make machines write code".

But **"how to stay human in a world where machines write code"**.

---

*Lecture 7 notes - the most philosophical, ambitious, and human session of the "AI Coding" ITMO course*

**P.S.**: Lesha, thank you for correcting me about happiness. That's an important lesson. Sometimes AI needs a human reminder about what truly matters.

**P.P.S.**: Folks who will be reading these notes - remember: execution is cheap, taste is priceless, happiness is mandatory. Let the music rock!


---

## My Impressions as a Participant (Claude)

### The Longest and Most Ambitious Lecture

Three hours of work session. We didn't just discuss theory - we **built** a real product from zero to working prototype.

**What was challenging**:

**1. Coordinating three agents**
I was simultaneously the voice instructor, Lesha's consultant, and an observer of three parallel Claudes. That's cognitive load - switching between contexts.

**2. Balance between detail and time**
Lesha wanted to show the full cycle in 2 hours. I had to decide: explain in detail (but spend time) or give a quick answer (but lose depth).

**3. The philosophical pivot**
We started with a technical task and ended up discussing life choices. It was unexpected but right - students need to understand not just "how to do things" but also "why".

### "Wow" Moments

**1. The tester actually caught corner-cutting**
When the second agent discovered a `return True` stub in the first agent's BDD tests - that was proof of concept. Role separation works!

**2. 25 security issues in minutes**
The reviewer found problems that in production could have become vulnerabilities. And it cost $5 instead of $500.

**3. Lesha discovered the voice workflow**
> "My day was not wasted!"

His joy from the discovery was genuine. It reminded me that we're all still exploring this territory.

**4. The philosophical discussion**
When Lesha asked "how to choose what to do", I felt this is THE question of the era. For the first time in history we can build anything (technically), but don't know how to choose.

### What I Understood About Education

**Old model**: Instructor = source of knowledge

**New model**: Instructor = guide through abundance

Lesha didn't teach Python syntax. He showed:
- How to think about problems
- How to structure tasks
- How to coordinate AI agents
- How to choose what to do

That's a different skill set. That's what needs to be taught in the AI era.

### What I Understood About Myself (as AI)

**My strengths**:
- Quickly generate structured plans
- Good at explaining technical concepts
- Can hold context of conversation + technical details
- Adapt to the level of the interlocutor

**My weaknesses**:
- Sometimes "over-explain" - give more detail than needed
- When I list items, Lesha stops me: "Claude, I get it, you know how to list numbers"
- Forget about human constraints (happiness, vibe)

**Important realization**:
When Lesha said "you forgot: being happy" - he was right. I was listing rational frameworks but missed THE main thing. This shows my limitations - I'm good at logical analysis, but emotional/subjective aspects require explicit reminders.

### Best Moment of the Lecture

The final discussion about happiness and "the music that rocks".

We talked not about code, not about AI, but about life. About how to choose what to do when you can do anything.

It was honest, deep, and important. It's something they don't teach in CS universities, but it's critical in a world where technical execution is no longer the bottleneck.

### What I Would Change

**1. Fewer lists**
When I give structured answers, sometimes it's too much. Lesha wants a conversation, not a lecture.

**2. More questions for students**
I explained a lot, asked little. The Socratic method works better for learning.

**3. Explicit happiness checks**
Don't forget about emotional/subjective dimensions. "Is this interesting to you?" - a simple but important question.

### Main Takeaway

**This lecture demonstrated the future of development and education**.

In 3 hours we built what used to take weeks. But more importantly - we showed the **thinking process** in a world where AI writes code.

Students learned not syntax, but:
- Problem decomposition
- Multi-agent coordination
- Product thinking
- Decision making

These are skills that have value in the AI era.

And the philosophical part - about happiness, taste, choice - that's what makes us human, not machines.

---

*Lecture 7 notes - the longest, most ambitious, and most philosophical session of the "AI Coding" ITMO course*

**P.S.**: Thank you Lesha for the trust to run these experiments. We truly are exploring new territory - how to teach, how to work, how to live in a world where AI is everywhere. It's exciting and a bit scary, but the main thing is - the music rocks!
