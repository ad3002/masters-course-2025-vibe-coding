# Contributing Guide

Thank you for your interest in the "Vibe Coding 2025" course! We welcome contributions from the community.

## 🎯 What You Can Contribute

### Welcome

- **Use cases** — your real-world examples of working with AI tools
- **Supplementary materials** — useful links, articles, and videos related to the course topics
- **Corrections** — typos, inaccuracies, wording improvements
- **Translations** — adapting course materials to other languages
- **Tools and scripts** — automation utilities for vibe coding
- **Practical exercises** — assignments to reinforce course concepts

### Not Accepted

- Changes to the core course structure without prior approval
- Advertising paid services with no educational value
- Materials that violate licensing restrictions

## 📝 How to Contribute

### 1. Open an Issue (optional but recommended)

Before starting, create an issue describing:
- What you want to add or change
- Why it would be useful
- How it aligns with the course philosophy

### 2. Fork and Create a Branch

```bash
# Fork the repository via the GitHub UI, then clone your fork
git clone https://github.com/your-username/masters-course-2025-vibe-coding.git
cd masters-course-2025-vibe-coding

# Add upstream remote to stay in sync with the original
git remote add upstream https://github.com/ad3002/masters-course-2025-vibe-coding.git

# Create a branch for your contribution
git checkout -b feature/your-contribution-name
```

### 3. Make Your Changes

**Project structure:**

```
materials/           # Lecture materials
├── workshop1.md
├── workshop2.md
└── workshop3.md

audio/              # Audio recordings (do not edit)

examples/           # Examples and case studies (feel free to add)

tools/              # Useful scripts and utilities
```

**Formatting guidelines:**

- Use markdown for text-based materials
- Add emoji to improve readability (🚀 💡 ⚠️)
- Include syntax highlighting for code blocks
- Format links using markdown syntax

### 4. Commit

```bash
git add .
git commit -m "feat: add example of using Claude Code with FastAPI"
```

**Commit message format:**
- `feat:` — new feature or content
- `fix:` — bug fix or correction
- `docs:` — documentation changes
- `example:` — adding an example

### 5. Push and Create a Pull Request

```bash
git push origin feature/your-contribution-name
```

Then create a Pull Request via the GitHub UI with a description of:
- What was added or changed
- Why it is useful
- Usage examples (if applicable)

## ✅ Pre-Submission Checklist

- [ ] Materials align with the course philosophy (vibe coding, AI-first)
- [ ] Text has been proofread for typos
- [ ] All links are working
- [ ] Code (if any) has been tested
- [ ] PR description is included
- [ ] Formatting and style guidelines are followed

## 🤝 Contribution Examples

### Adding a Case Study

Create a file at `examples/your-case.md`:

```markdown
# Case Study Title

## Context
Brief description of the task

## Tools
- Claude Code
- Cursor

## Process
Step-by-step description

## Result
What was achieved, time spent, tokens used

## Takeaways
What worked, what didn't
```

### Adding a Tool

Create a folder `tools/tool-name/` containing:
- `README.md` — description and usage instructions
- Tool source code
- Usage examples

## 🔄 Review Process

1. The maintainer (Alexey) reviews PRs within 3-7 days
2. Comments or change requests may follow
3. Once approved, the PR is merged into main
4. Your name is added to the Contributors list

## 💬 Questions and Discussions

- **Telegram**: [@ad3002](https://t.me/ad3002)
- **GitHub Issues**: for technical questions
- **GitHub Discussions**: for discussing ideas

## 📜 License

By contributing, you agree that your materials will be distributed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Your authorship will be credited.

## 🌟 Acknowledgments

All contributors will be mentioned in the README. Significant contributions may receive special recognition.

---

*Thank you for helping make AI programming education more accessible!*
