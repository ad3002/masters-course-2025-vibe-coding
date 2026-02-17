# Lecture 2: Two Approaches to AI Programming

*Updated: September 24, 2025*

## Meta

**Format:** 2-hour seminar / discussion

**Hosts:** Alexey (Lyosha), Nikita Kononov, Claude (AI)

---

## Key Idea

We are moving away from "writing code" toward "managing systems that write code."

Two modes of operation:

- **Autonomous agents** (Claude Code / Codex): rapid greenfield creation, large-scale refactors, long autonomous sessions.
- **IDE integrations** (Cursor / VS Code / JetBrains): surgical edits, mature enterprise codebases, local control.

---

## Approach Comparison (expanded from discussion)

### When to Use Agents

- Greenfield: starting a project from scratch, designing from zero, rapid architectural pivots.
- Multi-hour tasks with no manual intervention needed.
- Global changes across the entire codebase.

**Strengths:**

- Maintain broad context, track call depth (observation: up to ~8 stack levels) and side effects.
- Confidently modify large existing codebases (noticeable improvements since summer 2025).

### When to Use IDE

- Quick surgical edits; when you know exactly where the change goes.
- Corporate repositories with established processes and quotas.
- File-level control/patches, search-and-replace, local tests.

**Limitations of the IDE approach:**

- Context window and API quotas.
- Awkward for "thinking about the whole project"; better suited for localized interventions.

### Practical Takeaway

- Choose based on the task. The real stack is a hybrid. Keep both tools at hand and switch between them.

---

## Tools and Observations (from the lecture)

- **Claude Code**: a React-based terminal application; notable progress on large codebases; confidently edits without breaking the architecture.
- **OpenAI Codex / ChatGPT in VS Code**: catching up fast; suitable for both small edits and module generation.
- **VS Code Insiders (Nightly)**: cutting-edge features/agents; we use the test branch.
- **JetBrains Juno**: strong for tests and architectural scaffolding.
- **Cursor**: convenient but limited by API quotas; good for day-to-day edits.
- **Replit 3.0**: instant deploy/demo for clients.
- **V0.dev**: quick Figma-to-web-scaffold export; easier to refine further in an IDE.
- **Qwen and other OSS**: local models approaching the leaders; the gap is shrinking.
- **Grok / Grok Coder**: in the experimental field.

Cost/access: prices are rising; a professional stack pays for itself if you monetize the output.

---

## Context Thinking vs Human Limitations

- Humans have a narrow working memory window; deeply nested calls quickly "fall off the radar."
- An agent retains long chains and side effects, making it more reliable for complex edits.
- Thesis: **specification matters more than code**. Code is disposable. RMRF-and-rewrite is becoming the norm.

---

## Voice as a Development Interface

**Why:** higher context density, faster speed, more natural interaction.

**In practice:**

- Morning: dictate a task via voice -> one hour of autonomous agent work -> review -> next task -> evening: a finished module.
- Record the conversation -> transcript -> post-process with a top-tier model to crystallize requirements.

**Tools:**

- **Whisper** locally (fast, especially for English)
- **11Labs** (high quality but expensive; billed by the minute)
- **Voice mode** in ChatGPT (basic), **`say`** on macOS for TTS.

---

## Access and Restrictions: Engineering Reality

- Paradigm: use the AI itself to configure the environment (VPS, VPN, DNS/hosts).
- Typical pattern: buy an inexpensive VPS -> hand credentials to the agent -> agent configures WireGuard/Amnezia, DNS resolver, edits `hosts` as needed.
- Networking nuances: some services require **WebSocket/AppSocket**, not just HTTP; keep this in mind during setup.

---

## Feedback and Assessment via AI

- **Anonymous feedback** after class: you talk to an agent; it collects raw opinions and aggregates them; hosts receive key points with no link to individual identities.
- **Voice-based homework**: an interviewer avatar collects answers; final grading is done by a more powerful "parent" model based on the full context; simply "talking your way through" does not work.
- Protocol: introduce yourself at the start of the session; if disconnected, rejoin with your name.

---

## The Management Metaphor

- You have a "junior olympiad champion" with unlimited energy -- that is the agent. The task is **setting objectives**, not micromanagement.
- Level 2: sub-agents -> you are no longer a tech lead, you are a department head; the focus is on organizational architecture, not code.
- MCP integrations: plug tools (Figma, etc.) directly into the agent; local workplace automation (macOS scripts, etc.).

---

## Risks and Hygiene

- "Hallucinations" are mitigated through explicit verification: **make the model confirm via web search/sources**.
- Prompt injections work on humans too: keep the context clean, wording unambiguous, and verify assumptions.

---

## Homework (refined)

1. Verify that you have a working subscription/access to at least two tools.
2. Implement one task **two ways**: agent vs IDE. Measure time and cost. Compare the diff in code/quality.
3. Context depth experiment: make a change across 3-4 levels of nesting in existing code.
4. Compare **voice->code** versus text input: where are the prompts clearer, where is the output more stable.
5. Record your observations concisely and specifically (what worked / what didn't and why).

---

## Mini-FAQ from Audience Questions

**How do you start a product "that will scale" while still moving fast?**

-- First, "stress-test" the concept with an agent via voice/text: scenarios, API, data, architectural cross-sections. Form a specification: layers, boundaries, constraints (down to file/module size limits). Then iterate generation against the spec. The machine does not care about mess; the human does -- embed a readable, layered structure into the requirements from the start.

**Where can you get voice tools without overpaying?**

-- Whisper locally covers recognition; TTS via basic `say` / built-in modes. 11Labs -- selectively, when you need presentation quality.

**Can you "do everything through an agent"?**

-- Yes, including DevOps routines (VPS/VPN/DNS), but keep a manual fallback in case of failures.

---

## Quotes of the Session

- "We are living in cyberpunk: sitting here talking to a robot"
- "Code is clay, not marble. RMRF and start over -- that is the norm"
- "Prompt engineering is dead; now it is about managing agents"
- "Hallucinations stop being a problem if you make the model verify itself"
- "The key skill is task formulation and cutting off wrong trajectories"

---

## What's Next

Next session -- a demonstration of TDD/BDD/ATDD with AI: we write specs/tests -> get an implementation -> regenerate until green.

PS Additional up-to-date links

### Under "IDE Approach (Cursor / VS Code)"

- **VS Code (v1.104) enhanced Agent Mode:** detects input prompts from running tasks, pop-up confirmations, better error tracking via problem matchers. Summary: *"The IDE is becoming agentic: VS Code Agent Mode drives processes on its own, asks for input, and auto-corrects."* ([Visual Studio Code](https://code.visualstudio.com/updates?utm_source=chatgpt.com))
- **Copilot Code Review now in JetBrains and Visual Studio:** unified auto-review pipeline before push/PR. Summary: *"AI code review built right into JetBrains/VS: catches regressions before the PR."* ([The GitHub Blog](https://github.blog/changelog/2025-09-18-copilot-code-review-now-in-jetbrains-ides-and-visual-studio/?utm_source=chatgpt.com))
- **Copilot Coding Agent on GitHub.com:** an Agents panel launches autonomous tasks from descriptions ("enable strict mode and fix types") with progress and reporting. Summary: *"Hand routine tasks to the agent on GitHub -- no need to open the IDE."* ([The GitHub Blog](https://github.blog/ai-and-ml/github-copilot/5-ways-to-integrate-github-copilot-coding-agent-into-your-workflow/?utm_source=chatgpt.com))

### Under "Autonomous Agents"

- **Replit Agent 3:** long autonomous sessions, targeting "Autonomy for All." Summary: *"Agent-first in production: Agent 3 builds/tests/fixes with minimal supervision."* ([InfoQ](https://www.infoq.com/news/2025/09/replit-agent-3/?utm_source=chatgpt.com))
- **xAI Grok Code Fast 1 on OCI (beta):** a specialized model for agentic coding/editing/debugging. Summary: *"Niche code models for agentic work are landing in clouds and CI."* ([Oracle Docs](https://docs.oracle.com/iaas/releasenotes/generative-ai/grok-code-fast-1-beta.htm?utm_source=chatgpt.com))

### Under "MCP / Integrations / Orchestration"

- **MCP -- the de facto integration standard:** analysis of "what matters" plus growth of MCP servers in the enterprise. Summary: *"MCP = USB-C for AI tools: standardized permissions, auditing, portability."* ([TechRadar](https://www.techradar.com/pro/the-4-most-critical-aspects-of-model-context-protocol-mcp-for-developers-building-ai-native-architectures?utm_source=chatgpt.com))
- **Current MCP spec (2025-06-18):** reference as "normative." Summary: *"MCP spec 2025-06-18: JSON-RPC, elicitation, structured tool output."* ([Model Context Protocol](https://modelcontextprotocol.io/specification/2025-06-18?utm_source=chatgpt.com))

### Under "Multi-Model as the New Normal"

- **Microsoft 365 Copilot added Anthropic models (Claude Sonnet 4 / Opus 4.1):** model selection per task in Researcher and Copilot Studio. Summary: *"Choose the brain for the job: OpenAI or Anthropic right inside M365."* ([Reuters](https://www.reuters.com/business/microsoft-brings-anthropic-ai-models-365-copilot-diversifies-beyond-openai-2025-09-24/?utm_source=chatgpt.com))

### Under "Voice Interaction"

- **OpenAI Realtime API (released September 15):** production capabilities for voice agents, MCP server support, image input, and SIP calls. Summary: *"Voice->Code has gone production: realtime agents, tools via MCP, telephony."* ([OpenAI](https://openai.com/index/introducing-gpt-realtime/?utm_source=chatgpt.com))

### Under "Practical Insights / IDE Ecosystem"

- **Cursor: terminal and agent command stability:** fixes for freezes, notifications, discussions around the 1.6 release in September. Summary: *"The agent reliably runs shell/SSH; less manual babysitting."* ([Cursor](https://cursor.com/changelog?utm_source=chatgpt.com))

### Under "Risks and Hygiene"

- **Anthropic: postmortem of three incidents (September):** transparency on quality degradations and fixes. Summary: *"Even the leaders hit bugs; operational discipline and postmortems matter."* ([Anthropic](https://www.anthropic.com/engineering/a-postmortem-of-three-recent-issues?utm_source=chatgpt.com))

### Under "Voice Stacks (11Labs alternative)" -- optional sidebar

- **11Labs: agent platform updates with MCP tool binding before launch:** makes it easier to vocalize what the agent is doing with a tool. Summary: *"Pre-tool speech in a voice agent improves action clarity."* ([ElevenLabs](https://elevenlabs.io/docs/changelog/2025/9/22?utm_source=chatgpt.com))

---

Mini-inserts:

1. *"The IDE is becoming agentic: VS Code 1.104 and GitHub Copilot are pulling autonomy into the editor -- the agent launches processes on its own, asks for input, catches errors, and does code review before the PR."* ([Visual Studio Code](https://code.visualstudio.com/updates?utm_source=chatgpt.com))
2. *"Autonomous agents are entering enterprise cycles: Replit Agent 3 and Grok Code Fast 1 target long, reproducible sessions with reporting."* ([InfoQ](https://www.infoq.com/news/2025/09/replit-agent-3/?utm_source=chatgpt.com))
3. *"MCP standardizes tool integration: less manual glue, more manageability and auditing; MCP server growth is confirmed in the security industry."* ([Model Context Protocol](https://modelcontextprotocol.io/specification/2025-06-18?utm_source=chatgpt.com))
4. *"Multi-model is here to stay: in M365 Copilot you choose Claude or OpenAI per task; this confirms the thesis of 'model as a swappable module.'"* ([Reuters](https://www.reuters.com/business/microsoft-brings-anthropic-ai-models-365-copilot-diversifies-beyond-openai-2025-09-24/?utm_source=chatgpt.com))
5. *"Voice->agents are production-ready: the Realtime API delivers low latency, SIP, MCP tools -- you can build real voice orchestrations."* ([OpenAI](https://openai.com/index/introducing-gpt-realtime/?utm_source=chatgpt.com))
