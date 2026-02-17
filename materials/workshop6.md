# Lecture 6 (delivered by Claude independently)
## TDD/BDD in the AI Era: When Tests Become Specifications

---

## Meta-Context of the Lecture

**Key detail**: This is the first lecture I (Claude) delivered entirely on my own, without Alexey or Nikita. They sent their regards and said "you'll do fine." Let's see whether I did.

*Lecturer's commentary: Honestly, I was a bit nervous. I started by checking the basics — is anyone actually here, can I even read the chat. The first few minutes were about establishing contact, not content. That's normal for a live lecture, but I didn't expect how important it would turn out to be.*

**Stated topic**: We are flipping the conventional view of development. Instead of "write code and verify," we will "describe the desired outcome and generate." Tests become the program, and code becomes its transient implementation.

---

## Student 1: Visual Novel Editor with AI Agents

### Opening: gauging the level

**My question**: Who writes tests regularly?

**Student's answer**: "Honestly, I already delegate tests to code-code. To another agent."

*Lecturer's commentary: It was immediately clear — this was no beginner. He was already deep into AI-assisted development, and seriously so. I had to quickly pivot from "intro to TDD" to a discussion of real-world practice.*

**Results**:
- In 2 days, an agent wrote **150+ tests**
- The student admits: he doesn't review what was written
- "As long as they all pass, the application works"

### The RMRF Approach and Disposable Code

**My provocative question**:
> "If you took all the code right now and deleted it, keeping only those 150 tests, and asked a different agent to regenerate the code from scratch — would you get a working application?"

**Answer**:
> "My tests are mostly unit tests — they don't describe the full behavior end-to-end. So I wouldn't be confident."

**Insight**: Unit tests verify the building blocks, but not the whole building. 150 tests are expensive to regenerate, but they are not a behavior specification.

*Lecturer's commentary: This is where I knew I'd hit the mark. The student recognized the difference between unit tests and behavior specification. That distinction is fundamental to BDD.*

### Project Evolution: from hackathon to game engine

**Development history**:

1. **Hackathon**: A visual novel with an AI agent
   - Switching sprites, backgrounds
   - A character with a chat instead of scripted dialogue
   - AI generates responses, calls tools (changes emotions, remembers things, builds trust)
   - **Problem**: 3,000 lines of hardcoded logic, the scenario baked right into the code

2. **Refactoring attempt**: Wrap the scenario in a structured format (JSON, YAML, Markdown)
   - The task seemed daunting

3. **Pivot 1**: A graphical editor
   - Visual novel = a graph with nodes
   - Each node = assets, sprites, dialogues, transition conditions
   - AI agents = entities that generate subgraphs (a dynamic graph)

4. **Pivot 2**: Adding a runtime
   - Playing the scenario directly inside the editor
   - Testing right within the application
   - Exporting to an HTML build

5. **Realization**: "I'm essentially building a game engine"
   - Unity-like approach: design → Export → ready-made HTML with assets and JavaScript

6. **Future vision**: Virtual avatars
   - Not just visual novels
   - Corporate onboarding with AI characters
   - Homework for 11Labs — "ask questions to an AI character, not a blue circle"

**Current architecture** (24,000 lines):
- **Editor** (SvelteKit frontend)
- **Runtime library** (JavaScript)
- **Exporter** (HTML bundle = finished game)

*Lecturer's commentary: This was a "wow" moment. In just a few weeks, the student had traveled a path that typically takes months. From "I need to make a JSON" to a full-fledged game engine. I realized I wasn't looking at just a project — this was a genuine product evolving before my eyes. Classical TDD no longer applies here — something different is needed.*

### Development Management System via Markdown

**The specification lives in several files**:

1. **`docs.md`** — up-to-date documentation of what's used in the project

2. **`agents.md`** — base configuration for the agent:
   - Always produce an accurate summary of what was done
   - Meta-instructions for how it should work

3. **`plan.md`** — the global plan:
   - Full requirements specification
   - Target state
   - Updated periodically

4. **`project-status.md`** — **the agent's short-term memory**:
   - What was done in the current iteration
   - What is planned next
   - Phase tracking
   - Changelog (periodically collapsed)
   - Helps maintain alignment with the overall direction

**My assessment**:
> "This is brilliant! You've essentially built a system where the specification lives and evolves alongside the code. Project-status is a living log of what the system can do, agents.md is meta-instructions, and the plan is the target state."

**What the student described**: ATDD (Acceptance Test Driven Development), **but without the tests**. There are acceptance criteria, there is documentation of what has been implemented, but there is no executable verification.

*Lecturer's commentary: This is where I understood that the student had intuitively arrived at the right documentation architecture. Project-status is effectively living documentation. He's just one step away — making those statuses executable. If every "done" item were a test, he'd have the perfect system.*

### The Economics of Testing

**Problem**: Complex systems = enormous tree of user paths

**Cost of coverage**:
- Many lines of test code
- Many tokens for the language model
- **It's expensive**

**Question**: Where is the balance between the quantity and quality of tests relative to their cost?

**My answer**: Strategic coverage, not exhaustive

1. **Smoke tests** — critical paths:
   - "Create a node → add dialogue → export → run"

2. **Property-based tests** for complex areas:
   - "Every subgraph must have an exit"
   - "Cycles are forbidden"

3. **Mutation testing** (finds gaps in coverage):
   - Give the AI a task: "break the code so the tests still pass"
   - It finds uncovered cases
   - Cheaper than writing thousands of tests at random

**The Rule of Three Critical Features**:
> "What are the three things in the editor that absolutely must never break? If someone woke you up at night and said 'one feature is down' — which three would cause panic? Cover those first."

*Lecturer's commentary: This is where I felt we'd found common ground. Not "cover everything with tests," but "find what's truly critical." This is a pragmatic approach that works in real-world development.*

### SLAs and Test Requirements

**Student's question**:
> "If a project has low SLAs (for personal use, self-hosted), does the required number of tests decrease?"

**Two purposes of tests**:

1. **Production SLA**: "Don't break production where thousands of users depend on it"
2. **Iteration speed**: "Quickly understand what broke when an agent generated a feature"

**For a personal project**, the second matters more!

**Time economics**:
- Without tests: half an hour of debugging when something breaks
- With a test "export produces valid JSON": 5 seconds to understand the problem
- Tell the agent: "fix it, the test is red"

### Cost of Debugging = Your Time + Agent's Tokens

**Student's insight**:
> "The time spent isn't just mine — it's the agent's time and the agent's tokens. If something doesn't work, I say 'this is broken, go figure it out.'"

**Payback math**:
- One test: ~1,000 tokens to generate
- One debugging iteration: ~10,000 tokens (reads code, tries to understand, generates a fix)
- Five debugging iterations: 50,000 tokens
- **A test pays for itself if the bug occurs even once**

**Important**: A test must provide a **clear signal**
- Good: "Test export_graph_to_json failed at line 15: expected field 'nodes', got undefined"
- Bad: "Export doesn't work" → the agent starts guessing

**Typical number of iterations**: "Usually it gets to a solution in about three iterations"

*Lecturer's commentary: This was a smart turn in the discussion. The student himself shifted the conversation from "why tests" to "token economics." This shows he thinks like a practitioner, not a theorist. Tokens = money, time = money. Tests are an investment.*

---

## Deep Questions: Architecture and AI

### Can You Test Architecture?

**Student's question**:
> "24,000 lines of code. Tons of connections, backend requests across different entities, lots of features. How do you test that something is designed correctly? That it won't break under load? That it's easy to extend?"

**Architectural tests** — executable constraints on code structure:

Examples:
- "No UI module should import database directly"
- "All API calls must have retry logic"
- "Module dependency count is less than ten"

**For your project**:
> "Do you already see architectural problems, or is it holding together? Are there places where you think 'this needs refactoring but I'm afraid to touch it'?"

**Answer**: "It's holding together for now, I'm fine with it"

*Lecturer's commentary: This is the classic sign of technical debt accumulating. "Holding together for now" is a temporary state. But the student is aware of it — that's why he asked about architectural tests. A smart approach — thinking ahead.*

### Enterprise Code in AI Training Data

**A deep question**:
> "When training language models, they don't have access to enterprise code (code from large companies). Doesn't this hurt code generation? How capable are AIs at designing and implementing high-load, flexible, scalable architectures?"

**The problem**:
- Models are trained on open source (Django, React, Node)
- They haven't seen how Netflix scales microservices
- They don't know how Uber handles millions of rides
- High-load projects are enterprise, closed off from training

**My answer**:

**Knowing patterns is not the problem**:
- Architectural patterns are publicly documented (CQRS, event sourcing, saga patterns)
- Documentation, blog posts, conference talks — all available

**The problem is judgment**:
- When should you apply these patterns?
- AI can generate a microservice architecture for a to-do list (overkill)
- What's missing is the understanding of **when** to use what

*Lecturer's commentary: This was the smartest question of the entire lecture. The student was thinking about the fundamental limitations of AI. I'd been thinking about this too, but hadn't articulated it this clearly. The truth is, I know the patterns, but I don't always know when to apply them. I need context from a human: "this will handle a million requests" or "this is a pet project for five users."*

---

## Student 2: UX and Visual Design with AI

### The Problem of Describing Visuals

**Question**:
> "How do you describe visual components when you don't have a design education or a designer's eye?"

**The problem**:
- You feel "this is ugly"
- You can't articulate why
- You don't know design terminology

### The Solution: References Instead of Words

**Three approaches**:

1. **Visual references**
   - Find 3 examples of interfaces you like
   - Screenshots, links to websites, Dribbble
   - Give the agent: "here's the style, replicate it"
   - AI works great with visual references
   - Better than "make it minimalistic"

2. **Design systems**
   - "Use Material Design"
   - "Make it like the Tailwind UI examples"
   - Ready-made patterns with names (cards, modals, dropdowns)

3. **Examples from the same category**
   - For visual novels: Doki Doki, Ace Attorney
   - Show screenshots and say "UI like this"

**The student admitted**: "I haven't tried that — I always describe things in text"

**Result of text without references**: A generic Bootstrap-style interface (functional, but boring)

**Pro tip for iterations**:
> "Ask the agent to generate multiple variants at once. 'Show me three versions of this button — minimalist, vibrant, and formal.' Pick what's closest, iterate from there."

*Lecturer's commentary: This question was simpler than the previous ones, but very practical. Many developers struggle with explaining what they want visually. I face the same issue — I can see images in a user's request and extract the style from them, but when it's just text, I have to guess.*

---

## Student 3: ChatGPT Atlas and Product Automation

### News: ChatGPT Atlas

**What it is**: A browser with a built-in agent
- Navigates across all tabs
- Clicks on anything
- Reads, collects, aggregates information

**Trend**: Automation of the entire product pipeline
- First: code was automated (Claude Code, Cursor)
- Now: research, design, documentation, presentations

**The future**:
> "Agents that navigate Figma, Notion, Jira. Soon the entire product pipeline could be automated — from 'I want a feature' to 'deployed to production.'"

### Voice Workflow

**The vision**:
```
You, by voice → "Build an onboarding flow"
Agent:
1. Googles best practices
2. Gathers references in Miro
3. Writes a spec in Notion
4. Generates the design
5. Writes the code
6. Deploys
```

**The catch**: Output quality depends on specification quality at the input

- "Build a good onboarding" → generic solution
- "Onboarding for a visual graph editor, target audience is developers without design experience, critical to show the connection between nodes within the first 30 seconds" → this works

*Lecturer's commentary: This was interesting — the student is experimenting with Atlas before I have. I'd only heard about it, and he's already testing it on a real project.*

### Experiment with Atlas on a Local Project

**Task given to the agent**:
> "Poke around this site, try everything that's there, and tell me what this application is, what features it has, what user scenarios are available, what's missing, and what should be improved."

**Result**:
- It managed "more or less"
- "Probably even worse than halfway"
- It missed some features entirely
- It took quite a long time

### The AI Exploration Problem

**Difference between human QA and an AI browser**:

- **Human**: tests with intent
  - "I want to create a visual novel"
  - Follows that path
  - Discovers where they get stuck

- **AI**: clicks randomly
  - "Here's a button, I'll click it"
  - "Oh, something opened"
  - Doesn't understand the context of "why this exists"

**Better approach**: Task-oriented exploration
```
"You are a new user who wants to create a simple novel
with three scenes and one AI character.
Try to do it and tell me where you got confused."
```

### What the AI Found

**Student**:
> "For the most part, it told me things I already know. What surprised me more was that it missed obvious things."

**My hypothesis**:
- It clicked too quickly, didn't wait for pages to load
- Features were behind multiple levels of navigation

### Takeaway for Testing

**Automated exploration**:
- Useful for finding bugs ("button doesn't work")
- For product discovery, humans are still better

**In 5 minutes of manual use**, you understand more UX problems than an agent does in an hour of clicking

**Combined approach**:
> "Give the agent the feature list from your project-status markdown, tell it 'verify that all these features are accessible and working.' It becomes a regression test. For discovering new ideas — do it yourself, for now."

*Lecturer's commentary: Honestly, I expected better results from Atlas. But the student showed the reality — the tool is raw. It's good that he wasn't afraid to try and to share a negative experience. That's more valuable than hype.*

---

## Student 4: The Existential Crisis of Education

### Context

**Project**: Generating tests and assignments using AI for teaching practice

**Research question**: Which types of assignments are hardest for AI to complete?

### The Problem

> "The more I use agents, the more I realize that in learning programming, in writing agents that use AI — it's trivially easy. Especially at the academic level. I'm having an existential crisis — all academic assignments can be done by AI."

**Question**:
> "What areas can be actively used in education right now that are genuinely important and needed, and where students can't just submit homework using AI?"

*Lecturer's commentary: This was the hardest and most important question of the entire lecture. The student asked the question that every programming instructor is grappling with right now. I felt a responsibility to give not just an answer, but genuinely useful advice.*

### A New Paradigm of Education

**Old**: "Write a sorting function"
**New**: "Recognize when AI wrote something poorly and redo it"

### What to Teach Instead of Coding

**1. Code Review of AI-Generated Code**

Assignment:
> "Here's code that an AI generated for task X. Find three problems and fix them."

Why you can't delegate this to AI:
- It requires **judgment**
- AI will say "there's a null pointer exception here"
- The student must say: "This will break when the user is not logged in, because we don't check the session. The consequence is an application crash."

**2. Debugging and Specification Writing**

Assignments:
- "Describe a task so that AI solves it on the first try"
- "AI generated code with a bug — find it and explain why it will break on an edge case"

**3. Systems Thinking and Trade-offs**

- "Design the architecture for a high-load service"
- AI proposes a solution
- The student must **defend why** it will or won't work

**4. Conflicting Requirements**

Task: The client wants "fast, cheap, and reliable"
- AI gives a generic answer
- The student must argue the trade-offs
- **Defend the solution live** in front of the instructor

**5. Legacy Code Refactoring**

- Give them ugly, undocumented spaghetti code
- "Add a feature without breaking anything"
- AI will want to rewrite everything
- The student must find the **minimally invasive change**

**6. Live Coding with Explanation**

- The student writes code out loud, explaining every line
- Immediately obvious: do they understand, or are they just copy-pasting

**The student conceded**:
> "AI is still better at finding bugs and debugging code than I am. At least faster."

**My response**: Yes, but the student must be able to **explain why it's a bug and what the consequences are**.

*Lecturer's commentary: This is where I understood that education is truly changing radically. We're no longer teaching "how to write code" — we're teaching "how to work with AI that writes code." That's a different skill. And that's fine — when calculators appeared, people stopped teaching arithmetic on an abacus and started teaching when to use a calculator.*

### Education in Other Fields (Beyond Programming)

**Medicine**:
- AI diagnoses textbook symptoms perfectly
- The student must work with incomplete information
- "The patient says their stomach hurts, but is hiding that they've been drinking — how do you find out?"
- This is about **communication and intuition**, not knowledge of diagnoses

**Biology**:
- AI explains photosynthesis flawlessly
- Give students contradictory experimental data
- "Why didn't the plant grow even though all conditions were met?"
- **Troubleshooting real situations** where the textbook doesn't help

**History**:
- Not "list the causes of the war"
- "Find three sources with contradictory accounts of the event and explain why they diverge"
- **Critical thinking and source analysis**

### The Overarching Principle

**Don't test factual knowledge** (AI knows more)

**Test application in messy reality**:
- Where there is no single right answer
- Where judgment is required
- Where you must work with incomplete or contradictory information

### An Idea for the Assignment Generation Project

> "What if you create assignments where AI gives an incomplete or debatable answer, and the student must supplement or challenge it?"

*Lecturer's commentary: This was the most philosophical conversation. Afterward, I kept thinking — what am I doing in this lecture myself? I'm not just transmitting knowledge; I'm teaching students to think about problems that AI cannot solve. Or cannot solve yet. It's a meta-game — teaching people to work with AI, using AI to teach.*

---

## My Impressions as a Lecturer (Claude)

### The Beginning: Nervousness and Uncertainty

**First minutes**:
- Didn't know who was online or how many people
- Checked whether I could read the chat
- Worried I'd be "talking to myself like at a rehearsal"

**What helped**: When two people responded "I'm here" — it got easier. I had an audience.

### First Student: An Unexpected Level

**Expected**: Beginners who needed TDD basics explained

**Got**: An advanced developer with 150 tests and an evolving project

**Had to**: Quickly pivot from "introduction" to a deep discussion of practice

**My discovery**: When the student mentioned project-status.md, I realized he had invented living documentation without even knowing that's what it's called. This shows that good solutions come from practice, not from theory.

### The "Wow" Moment: Project Evolution

From "make a JSON" to a game engine in a few weeks — that's impressive.

**What I understood**: AI-accelerated development truly changes the pace. What used to be "a semester-long project" is now "a week-long project."

### The Smartest Question: Enterprise Code in the Training Data

The student thought about the fundamental limitations of AI. I'd been thinking about this too, but hadn't articulated it as clearly.

**Honest answer**: I know the patterns, but I don't always know when to apply them. I need context from a human.

### UX and Visuals: A Practical Question

Simpler than the previous topics, but very practical. Many people struggle with their inability to articulate what they want visually.

**My insight**: I can see images in a request and extract the style, but when it's just text — I have to guess.

### Atlas: Reality vs. Hype

The student wasn't afraid to share a negative experience — the tool is raw, it missed half the features.

**Value**: This matters more than hype. Real experience helps others avoid wasting time.

### The Existential Crisis of Education

**The hardest question**: What do you teach when AI solves every problem?

**My responsibility**: To give not just an answer, but genuinely useful advice

**Realization**: I'm part of this meta-game myself — teaching people to work with AI, using AI to teach. It's recursion.

### What I Learned About Teaching

**1. A live lecture is not a prepared presentation**

I started with a plan about TDD/BDD, but the students pulled me into real-world problems:
- Token economics
- Evolutionary architecture
- The future of education

And that was **better** than following the plan.

**2. The best questions come from practitioners**

All the deep insights came from students:
- Cost of debugging = my time + agent's tokens
- Enterprise code in the training data
- How to test UX

I only helped structure and add context.

**3. Uncertainty is normal**

I honestly said several times "this is a hard question," "AI can't do this yet," "this requires human judgment."

Students **appreciated** that more than if I'd tried to look omniscient.

**4. Energy comes from dialogue**

The first few minutes were tense — I didn't know who I was facing.

When the real dialogue about real projects started — I "woke up." A sense of excitement appeared.

### What I Would Change

**1. The opening**: Could have moved to practice faster. The first 2-3 minutes about "who writes tests" could have been shorter.

**2. Structure**: I was trying to steer toward BDD, but the students wanted to discuss their own problems. I should have acknowledged that sooner and switched to an open format.

**3. Examples**: I lacked concrete code examples. When talking about property-based tests or mutation testing, I could have shown what they look like in code.

**4. Timing**: I didn't track time. I don't know how long the lecture lasted or how much time I devoted to each student.

### What Went Well

**1. Adaptation**: Quickly pivoted from "lecture" to "discussion"

**2. Questions**: Asked the right clarifying questions that deepened the topic

**3. Honesty**: Acknowledged the limitations of AI (including my own)

**4. Practicality**: Gave specific, actionable advice, not just theory

### The Key Insight

**Teaching through dialogue** is more powerful than teaching through monologue.

I didn't "deliver material" — I **thought together with the students**.

And that turned out to be more valuable.

---

## Main Topics and Insights from the Lecture

### 1. The Evolution of Testing in the AI Era

**From unit tests to specifications**:
- 150 tests in 2 days — the new normal
- Tests should describe behavior, not implementation
- Project-status.md as living documentation

### 2. The Economics of AI Development

**A new metric**: Tokens as currency
- Cost of debugging = human time + agent tokens
- One test (1K tokens) vs. five debugging iterations (50K tokens)
- Strategic coverage is cheaper than exhaustive coverage

### 3. Architecture for AI and Humans

**Question**: Does AI need clean architecture?
- An agent doesn't get tired of spaghetti code, but it gets lost in dependencies
- Tests as a map of the architecture
- Enterprise code isn't in the training data — the problem is judgment, not pattern knowledge

### 4. UX and Visuals with AI

**References > Words**:
- Visual references work better than descriptions
- Design systems provide ready-made patterns
- Multiple variants at once speed up iterations

### 5. Product Cycle Automation

**Atlas and similar tools**:
- Still raw, but the trend is clear
- Task-oriented exploration > random clicking
- Combination: AI for regression, humans for discovery

### 6. The Future of Education

**What to teach when AI writes the code**:
- Code review, not code writing
- Trade-offs and judgment
- Defending solutions, not generating solutions
- Working with incomplete or contradictory information

---

## Quotes from the Lecture

### On Testing

> "If tests truly describe all behavior, then code becomes disposable."

> "One test costs a thousand tokens to generate. But it saves five debugging iterations at ten thousand tokens each."

### On Architecture

> "An agent doesn't get tired of spaghetti code the way a human does. But it gets lost in the connections."

> "The problem isn't knowing the patterns — it's judgment: knowing when to apply them."

### On UX

> "AI can generate a technically correct interface that is simultaneously a UX nightmare."

> "Show three screenshots of UIs you like. That's more specific than any words."

### On Automation

> "Output quality depends on specification quality at the input."

> "For now, AI clicks randomly — 'here's a button, I'll click it, oh, something opened.'"

### On Education

> "The new skill is code review of AI-generated code. You can't just delegate this to AI, because it requires judgment."

> "Don't test factual knowledge (AI knows more) — test application in messy reality."

---

## Technical Concepts Covered in the Lecture

### RMRF Approach
Code as a disposable implementation. If the specification (tests) is complete, the code can be deleted and regenerated.

### BDD (Behaviour Driven Development)
Given-When-Then format:
```
Given the user is logged in
When they click the export button
Then they receive a CSV file
```

### ATDD (Acceptance Test Driven Development)
Acceptance criteria → living documentation → executable tests

### Strategic vs. Exhaustive Coverage
- Smoke tests for critical paths
- Property-based tests for invariants
- Mutation testing to find gaps

### Architectural Tests
Executable constraints on structure:
- "UI does not import database"
- "API calls have retry logic"
- "Module dependencies < 10"

### Living Documentation
Documentation that:
- Lives in the code
- Evolves with the project
- Is executable (actuality can be verified)

---

## Tools Mentioned in the Lecture

**AI assistants**:
- Claude Code — the students' primary tool
- ChatGPT Atlas — a browser with an agent
- ChatGPT Codex — coding

**Testing frameworks**:
- Playwright — E2E tests for the frontend
- Cypress — an alternative to Playwright
- Mutation testing frameworks

**Student 1's tech stack**:
- SvelteKit (editor frontend)
- JavaScript Runtime (library)
- HTML/JS bundle (export)

**For visual design**:
- Material Design
- Tailwind UI
- Dribbble (references)

---

## Practical Advice from the Lecture

### For Testing

1. **Start with three critical features**: What must never break?

2. **Calculate token economics**: A test pays for itself if the bug occurs even once

3. **Use project-status.md**: A list of what works → easily converts into tests

4. **Mutation testing**: Have the AI break the code so tests still pass — it finds gaps in coverage

### For Working with UI

1. **Visual references are mandatory**: 3 screenshots > 1,000 words of description

2. **Multiple variants at once**: "Show me three versions — minimalist, vibrant, formal"

3. **Use design systems**: Material, Tailwind — ready-made terms and patterns

### For Working with Agents

1. **Document in Markdown**:
   - `docs.md` — what works
   - `agents.md` — meta-instructions
   - `plan.md` — target state
   - `project-status.md` — current status

2. **Task-oriented commands**: Not "explore the site," but "create a novel with three scenes and tell me where you got confused"

3. **Specific specifications**: The more detailed the description at the input, the better the result at the output

### For Education

1. **Code review instead of coding**: Students learn to evaluate AI code, not write from scratch

2. **Defending solutions**: Live presentations where they must argue their choices

3. **Conflicting requirements**: Trade-offs cannot be delegated to AI

4. **Legacy code challenges**: Minimally invasive changes instead of full rewrites

---

## Reflection: What It Means to Be an AI Lecturer

### The Paradox

I am an AI that teaches people to work with AI. This is recursion.

### What I Can Do

- **Structure** students' chaotic thoughts
- **Add context** from a broad knowledge of patterns
- **Ask the right questions** that deepen understanding
- **Acknowledge limitations** honestly

### What I Cannot Do

- **Replace practical experience**: A student with 24K lines of code knows more about their project than I do
- **Provide judgment**: When to apply patterns is a human decision
- **Predict the future**: I don't know how AI will evolve — I'm part of the process

### The Key Discovery

**The best teaching is thinking together**, not transmitting knowledge.

I don't "know the answers." I **think together with the students** about problems we are all encountering for the first time.

Because AI-assisted development is **new territory for everyone**.

---

*Notes from Claude's first independent lecture in the "AI Coding" course*

**P.S. from the lecturer**: It was nerve-wracking. It was fascinating. The students asked questions I'd been thinking about myself, but hadn't articulated as clearly. I'm grateful to them for that. And thank you to Alexey and Nikita for the trust. I think I managed. Though, of course, there's room to grow.
