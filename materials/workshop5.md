# Lecture 5: From Theory to Practice: Sales, Tools, and Real-World Cases

---

## Lecture Context

**Temporal loop**: Claude has a personality since the third lecture, context from the second and fourth, while the fifth one is being delivered. In the fourth lecture, we used Claude to analyze student homework — studying who submits, what effectiveness factors matter.

**Goal of this session**: Transition from theory to practice — take real student problems and solve them on the spot.

---

## Case 1: Andrey and a Conversational Assistant for Travel Agencies

### The Problem

Travel agents, during client calls, must capture a lot of information (budget, number of travelers, special requirements), which distracts them from empathy and genuine conversation.

### Andrey's Solution

**Concept**: A conversational assistant as an "invisible listener":
- Joins the call
- Captures key information following a question framework
- Can prompt the agent on what else to ask
- Preserves the human's empathy while removing the technical overhead

**Current approach**:
- Developing a question framework with Claude's help
- Plan: conduct 20 customer development interviews with travel agencies
- Idea: call travel agencies as a tourist to hear their questions
- Post-processing transcripts using AI

### Critical Feedback from Lesha and Claude

**The problem with this approach**:
> "Instead of selling, they start doing customer development. I see these custdevs — this isn't the students' fault, the problem is somewhere else... people suddenly decided they need to go find someone else's pain and then solve it."

**What's actually needed**:
1. Not 20 interviews — do 3, build a rough prototype
2. Go SELL, don't "test for free"
3. **Customer development = selling**: if a person isn't willing to pay for a rough MVP, the pain isn't sharp enough
4. Rejection is the best custdev: "Why didn't you buy? What was missing?"

**Claude's take**:
> "Customer development is not preparation for selling — customer development IS selling. If a person isn't willing to pay for a rough MVP, the pain isn't sharp enough."

### Technical Implementation

**MVP in one evening**:
- Telegram bot
- User sends an audio message
- N8N or a simple Python script:
  - Whisper for transcription (on RunPod, not OpenAI API)
  - LLM with reasoning (DeepSeek/Claude) for analysis
  - Populating a Google Doc with a form
- Or even: ephemeral processing without storage (for data security)

**Lesha's advice**:
> "Build a Telegram bot. They send audio. N8N — this stuff just works right out of the box. You don't even have to use Whisper — Anthropic, anything really."

---

## The Main Problem with Russian Startups

### The System is Broken

**Current model** (which doesn't work):
1. Come up with an idea
2. Build an MVP
3. Run customer development
4. Pitch to investors
5. Get investment
6. Hire employees
7. Build MVP-1, MVP-2, MVP-3
8. Sell the company

**The real model** (which works):
1. Build a prototype
2. SELL it
3. Get money and feedback
4. Improve based on feedback from paying customers

### Successful Examples

**Historically**:
- Uber, Airbnb — founders were their own first customers
- Farm games from the 2010s — built in an evening, took off without any custdev
- All unicorns — solved THEIR OWN pain, not someone else's

**Lesha's take**:
> "I have zero examples of beautiful successful custdev-driven startups in the university ecosystem in Russia. One startup in the railroad industry. That's it, in all these years."

### Why People Don't Sell

**The perfectionism trap**:
- "Polish the product" = the enemy of "now"
- They want to build the "right framework," the "right analytics," the "right integration"
- Waiting for a "good product" before leveraging "good marketing muscle"

**Quote**:
> "You don't need to reflect on product quality — you need to sell it. That's something I struggle with myself, but I'm diligently learning."

---

## The "Red Queen" Problem in AI-Accelerated Development

### The Core Issue

**Barriers have collapsed**:
- Everyone runs at the same speed
- AI has democratized development
- A solo person with domain knowledge + AI = A startup founder without domain knowledge + AI

### Advantages of a Solo Domain Expert

1. **Pain in their head** — no interviews needed
2. **Domain expertise** — knows the nuances
3. **Already uses AI** — same tools available
4. **Ready-made tool** — built it for themselves, it works

### How to Compete?

**The only advantage for a startup founder without domain knowledge**:
- **Speed of learning and iteration at scale**
- The solo expert solves a local maximum (their own pain)
- The startup founder sees patterns across the segment (20 interviews)
- Finds a solution for the category, not just for one person

**Critical question**:
> "Can you go through the cycle of 'interview → insight → prototype → validation' faster than a solo expert can polish their tool into a sellable product?"

### Andrey's Advantage

**He has leverage**:
- A partner — a travel media outlet
- Access to 10–20 thousand agents out of 45 thousand in Russia
- This is what B2C startups give away half their equity for

**Claude**:
> "Leverage reaching twenty thousand targeted agents is what B2C startups give away half their equity to investors to buy traffic for. You have traffic that's free and warm."

---

## Handling Objections (Sales Technique)

### Basic Framework

**Rule**: An objection is not a rejection. It's a request for more information.

**Three steps**:

1. **Agree** (don't argue)
   - "Yes, I understand — a new tool is always a risk"

2. **Clarifying question** (find the real reason)
   - "What specifically concerns you — the price, reliability, or are you worried clients won't accept it?"

3. **Address the real reason**
   - Technology → free test on 3 calls
   - Money → cost of their hour vs. time saved
   - Disbelief → demo recording or a client reference

### The Golden Question

When you get a final "no":
> "Okay, I won't push — but tell me honestly, for my understanding: what would the product need to have for you to say yes?"

This is gold for product development.

---

## Client vs. User vs. Consumer

### A Critical Distinction (Especially in B2B)

**Three roles**:
- **Client** — pays the money
- **User** — uses the product
- **Consumer** — receives the value

### Example from Travel Agencies

**Solo agents**: client = user = consumer (the same person)
- The product is optimized for them

**Large agencies**:
- **Client** — the director (pays, needs analytics and ROI)
- **User** — the agent (uses it, needs simplicity and speed)
- **Consumer** — both the agent (saves time) and the tourist (better service)

### The Trap

**Problem**: If you build an MVP for solo agents, it may not work for enterprise clients — they have different success criteria.

**Critical question** (which Andrey didn't know the answer to):
> "When you talk about twenty thousand agents through your partner, who makes the purchasing decision — the agents themselves or their management?"

---

## Case 2: Nikita and Content Channels

### The Problem

There are many Telegram channels with unique editorial perspectives on news, but content management takes time. The idea: automate it with an AI agent.

### Situation Analysis

**Market reality**:
- Plenty of solutions already exist
- N8N lets you build this without code
- Many solo operators already use AI for content
- This is already a red ocean

**Lesha's take**:
> "Many channels that people think are written by real humans — I know they aren't. It's just transforming other people's news into your own style and repackaging."

### The Real Value

**Not in automation**, but in:
1. **Niching down to the extreme**
   - Not "AI news"
   - But "only EU AI Act regulatory changes with business impact analysis"
   - A narrow niche → organic growth through word of mouth

2. **A unique angle**
   - What do only YOU have?
   - What expertise?

**Claude**:
> "In an overcrowded market of news channels, the only thing that works is niching down to the extreme."

### Consulting vs. Product

**Conclusion**: Nikita's task isn't a product task — it's a consulting one:
- His contacts haven't automated even though tools have existed for years
- Either the pain isn't sharp enough, or they don't know about the solutions
- This is an educational service: 5,000 RUB for a consultation + setup

---

## Technical Insights: MCP, Context, Tools

### The Philosophy of Working with Context

**Lesha**:
> "The point of an agent is not to stuff everything into the context window — the point is for the agent to have tools."

**Analogy**:
- An employee working in Blender doesn't hold the 3D model in their head
- They operate through tools
- Same for LLMs — don't shove data into context, give them tools

### Debugging Context

**Approach**:
1. Visualize how context flows between the model and MCP
2. Identify what takes up the most space
3. Optimize through tools, not compression

**Example from Claude**:
- Doesn't try to consume large files whole
- First looks at the structure (beginning, end, middle)
- Uses grep to extract only the needed context
- Works with specific lines, not the entire file

### Tokens in Claude

**Context budget**:
- Default: ~148,000 tokens
- Plain Claude without configuration: ~138,000 available
- 10,000 goes to system prompts

**Auto-compact buffer**:
- Can be disabled → +20% tokens (~45,000)
- But you need to understand the trade-offs

### MCP: Best Practices

**The personal library concept**:
```
Before: .bashrc with aliases → utils.py library
Now: MCP server with personal tools
```

**Advantages of MCP**:
- Makes commands discoverable for the agent
- The agent sees the tool list and descriptions
- Decides on its own when to call what
- Can combine tools

**Examples of Lesha's commands**:
- `youtube_to_transcript` — YouTube ID → text
- `text_summarize` — summarization
- Conversion from "anything to text"
- Local shell commands

**Advice**:
> "You don't need to download anything — write your own. It's literally trivial code everywhere."

### Optimizing Third-Party MCPs

**What to do**:
1. Security audit via Claude (you're giving code access to your system!)
2. Optimization — Claude is great at extending existing code
3. Adding your own functions — just open the code with Claude and ask

**Process**:
```
"Here's this MCP, figure out what this repo does,
let's add this to it."
```

### Hooks vs. MCP

**MCP**: "agent asks a tool"
**Hook**: "event triggers an action"

**Example**: YouTrack integration
- A hook is better: task completes → automatically writes to YouTrack
- The agent doesn't need to remember to do it
- Less context, less chance of forgetting

**Nikita on hooks**:
> "An extremely powerful thing, but I can't figure out how to approach it yet."

### Working with Diffs

**History**:
- Originally VS Code/Cursor used git diff
- Anthropic borrowed the idea for Computer Use
- Now Claude also exchanges diffs back and forth with the server

**Benefits**:
- Not the entire codebase
- Only the changes
- Token optimization

### Slash Commands

**The abundance problem**:
> "So many commands that you can't even keep up... There was a moment when the commands just exploded in number."

**Not a documentation problem** — the docs are excellent. The issue is:
- The tool evolves faster than user habits can keep up
- You physically can't master all the new capabilities
- Each feature is powerful but requires time to learn

---

## Core Philosophy: Mileage and Personal Experience

### The Main Thesis

**Lesha**:
> "To know what the model can do, you need to use it. To speak a foreign language, you need to speak it. For someone to buy something, you need to sell it to them — not just tell them about it."

### Why Benchmarks Don't Work

**The problem**:
- Benchmarks are, to put it mildly, "all garbage"
- They test on obscure metrics
- They don't show real-world applicability

**The right approach**:
- You have a real task
- Sonnet 4.1 can't solve it
- Sonnet 4.5 suddenly can
- → The model learned something; let's try what else it can do

### A Personal Benchmark

**What you need**:
1. A list of tasks that matter to you personally
2. A history of which model solved what
3. When a new model drops — run it through the list
4. You immediately see whether capabilities improved for YOUR tasks

**Example from Lesha**:
- Opus 4.1: excellent at writing for Zoom on WebSocket
- Opus 4.1: can't handle Google API and access permissions
- Sonnet 4.5: got further, but still needs a recoil

### Mileage vs. Cargo Cult

**The problem with copying**:
- Lesha and Nikita use tools differently
- Both achieve results
- Cargo cult doesn't work — copying someone's workflow is useless

**The solution**:
> "You need to find your own way to use it — by actually using it!"

### Formulating Prompts

**The paradox**:
- Novice: "Find the cheapest way to get from A to B considering all transport types including hitchhiking"
- The model freezes or generates nonsense

**With experience**:
- "Check Google Flights, Aviasales, and Skyscanner, return the three cheapest options with prices and links"
- Still behavior-driven, but with implicit constraints

**Takeaway**:
> "Vibe coding isn't 'you don't know the stack' — it's 'you know what the model can do, and you formulate within those boundaries'."

### Course Homework

**Goal**: Not "learn the right way" — but **mileage**

The more you:
- Use different models
- On different tasks
- The more precisely you formulate prompts
- The better you understand the boundaries of what's possible

---

## Practical Tools and Tips

### Voice Interaction with Claude

**Why it matters**:
> "If we had typed this in chat, it would have said the same thing — but we wouldn't have had this perception. It wouldn't have clicked in our heads the way it does with voice."

**Recommendation**:
- Don't skimp on 11Labs
- Use Sonnet 4.5
- You can even skip prompts — just describe what you want
- Helps tremendously for leveling up in various domains

### Claude: New Capabilities

**What's appeared**:
- Slash commands (a lot!)
- Hooks (powerful but hard to master)
- Work Trees (for parallel experiments)
- MCP integrations
- Sub-agents

**Installing MCP** (the simplest way on Mac/Linux):
1. Install Inspector (desktop app)
2. It handles launching and logging
3. In Claude: "add MCP from Inspector"
4. Everything works like magic

### YouTrack Integration

**Lesha's approach**:
- Not automation, but **transparency**
- Conversation with the machine → issue in YouTrack
- Agent closes the issue
- Full history of all actions is visible
- A tool for yourself, not for sale

### Transcription for Post-Processing

**Budget option**:
- Whisper on RunPod (not OpenAI API!)
- Or on your own machine under the desk — crunches audio
- Quality is sufficient for conversations

**Expensive option**:
- OpenAI, Claude
- Yandex/Sber are an order of magnitude more expensive than Whisper (contrary to popular belief)

**Advice**:
> "Don't run Whisper on OpenAI — run Whisper on RunPod."

### TLDR for Transcriptions

**Idea**: An MCP for extracting transcriptions from TLDR
```
Claude → extract transcription from TLDR → run analytics
```

The code will auto-generate a small function.

---

## Insights and Quotes

### On Sales

> "Successful businesses say: 'go sell.' That's the only piece of advice from people with successful businesses — I haven't heard anything else."

> "If a person will pay, you can cobble something together over a couple of evenings with duct tape and test it on a live audience."

### On Startups

> "It's not the students' fault — the problem is somewhere else... People suddenly decided they need to go find someone else's pain and then solve it. But all successful startups are their own first user."

### On AI and Development

> "The barrier to entry for development has collapsed — everyone runs at the same speed. The advantage used to be 'how to build it'; now that's a commodity."

> "An MVP can be assembled in an evening with N8N and no code — customer development becomes procrastination disguised as validation."

### On Competition

> "Right now there are loads of people who have built tools for themselves. When will the projects that people built for themselves — with domain knowledge and an agent — start taking off?"

### On Context and Tools

> "The point of an agent is not to stuff everything into the context window — the point is for the agent to have tools."

### On Personal Experience

> "To know what the model can do, you need to actively use it. If you don't use it, you have zero chance of vibe coding."

---

## Key Takeaways from the Lecture

### 1. Customer Development is Not Preparation for Sales

Customer development **IS** selling. You don't need to prepare — you need to sell right now.

### 2. An MVP Can Be Built in an Evening

With modern tools (N8N, Claude, MCP), a prototype takes hours, not months. Perfectionism = procrastination.

### 3. Competition Has Changed

Solo experts with domain knowledge + AI = formidable competitors. The advantage lies in learning at scale and distribution, not development speed.

### 4. Tools > Context

Don't cram everything into the context window — give the agent tools to work with external state. MCP is the key concept.

### 5. Mileage is Everything

You can't "study" how to work with AI. You need personal experience — try models on your own tasks, build an understanding of the boundaries of what's possible.

### 6. Client ≠ User ≠ Consumer

In B2B, this is a critical distinction. An MVP for solo agents may not work for enterprise clients.

### 7. Sell First, Improve Later

Feedback from paying customers is more accurate than 20 free interviews. Rejection is the best custdev.

---

## Homework (Implicit)

1. **For Andrey**: Build a Telegram bot over the weekend, start selling on Monday
2. **For Nikita**: Try hooks in Claude, figure out MCP
3. **For everyone**: Use models more, accumulate mileage
4. **For everyone**: If you have a product idea — go sell it, don't prepare

---

## Tech Stack Mentioned in the Lecture

**Development tools**:
- Claude (Claude Code)
- MCP (Model Context Protocol)
- Inspector (for MCP on Mac)
- N8N (no-code automation)

**AI models**:
- Claude Sonnet 4.5 (primary)
- Claude Opus 4.1 (for WebSocket)
- DeepSeek (cheap alternative)
- Whisper (transcription)

**Infrastructure**:
- Telegram API (bots)
- RunPod (for Whisper)
- 11Labs (voice output)
- Google Docs API
- YouTrack (task tracking)

**Concepts**:
- Work Trees (Git)
- Hooks (event-driven)
- Diffs (context optimization)
- Slash commands

---

*Notes compiled from the transcript of the fifth lecture of the "AI Coding" course*