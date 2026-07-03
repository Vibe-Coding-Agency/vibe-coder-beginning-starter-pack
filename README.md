# 🚀 Vibe Coder Beginning Starter Pack

Hey, future vibe coder! 👋

Welcome to the **Vibe Coding Academy Starter Pack** — your friendly on-ramp to
becoming the kind of engineer who ships real, production-grade AI systems.

If you’ve ever looked at AI demos and thought, *“That’s cool, but how does it
actually run in production?”* — you’re in exactly the right place. This repo is
a high-level map of what we teach, how we validate it, and how you can start
building today.

No PhD required. No fancy hardware required. Just curiosity, a keyboard, and a
willingness to ship. 💪

## 🌟 What is this repo?

This is the public syllabus and certification plan for the **Vibe Coding
Academy**. It’s designed to be:

- **Self-contained** — you can read it start to finish in about one hour.
- **Beginner-friendly** — we explain the big picture before the deep weeds.
- **Production-focused** — every module ends with something you can actually
  ship, not a toy notebook.
- **Offline-ready** — clone it, save it to your hard drive, and refer back to
  it whenever you need a refresher. No paywalls, no logins.

Think of it as the trailer + table of contents + quick-reference handbook for
the Academy experience.

## 🗂️ What’s inside

| Path | What it is |
|---|---|
| `README.md` | This file — the overview, tracks, and certification plan. |
| `how-to-use-this-repo.md` | A suggested reading path. |
| `modules/` | Five in-depth guides (~10 minutes each). Read these for the core ideas. |
| `cheatsheets/` | One-page references you can keep open while building. |
| `checklists/` | Step-by-step lists to run before shipping. |
| `reference/` | Decision trees and a failure-mode cookbook for quick decisions. |
| `glossary.md` | Definitions for terms used across the repo. |

Total reading time: roughly **one hour**. You can finish it in a single focused
session or dip in and out as you build.

## 🎯 Who is this for?

This starter pack is for you if:

- ✅ You’re a software engineer who wants to add AI-native skills to your
  toolkit.
- ✅ You’re a team lead figuring out how to train your engineers on real AI
  systems.
- ✅ You’ve built a few AI demos and want to learn what “production-ready”
  actually means.
- ✅ You like learning by building, breaking, and shipping things.

If that sounds like you, keep reading! 📖

## 🗺️ How to use this starter pack

1. Read the overview below to understand the Academy structure.
2. Read the modules in order:
   - [`modules/01-foundations-of-ai-native-engineering.md`](modules/01-foundations-of-ai-native-engineering.md)
   - [`modules/02-building-rag-and-agentic-systems.md`](modules/02-building-rag-and-agentic-systems.md)
   - [`modules/03-model-operations-and-observability.md`](modules/03-model-operations-and-observability.md)
   - [`modules/04-security-and-compliance-for-ai-systems.md`](modules/04-security-and-compliance-for-ai-systems.md)
   - [`modules/05-shipping-a-production-capstone.md`](modules/05-shipping-a-production-capstone.md)
3. Keep the [`cheatsheets/`](cheatsheets/) and [`checklists/`](checklists/) open
   while you work.
4. Check [`glossary.md`](glossary.md) whenever a term slips your mind.
5. **When you’re ready for a cohort**, reach out at
   [Vibe Coding Agency](https://vibecodingagency.com/products/vibe-coding-academy/).

Go at your own pace. Ask questions. Break things. That’s how you learn. 🔧

## 📚 Syllabus

The Academy is built around five competency areas. Each one ends with a
production-oriented project that gets reviewed like real engineering work.

### 1. Foundations of AI-native engineering 🧠

Build the mental model that separates a cool demo from a reliable product.

- What agents are (and aren’t)
- Inference, context windows, and tokens
- How to design good evaluations
- The production toolchain: models, gateways, caching, routing
- Turning a prompt into a real feature

**Your project:** Write a small design doc for an AI feature, including what
success looks like and what could go wrong.

### 2. Building RAG and agentic systems 🔍

Move past “chat with your PDF” to systems that actually retrieve, reason, and
act.

- Chunking text and choosing embeddings
- Retrieval pipelines and re-ranking
- Tool use and planning
- Multi-agent orchestration
- Long-running, stateful workflows

**Your project:** Build a RAG or agent system with tests, logs, and a simple
 eval suite.

### 3. Model operations and observability 📊

Treat AI models like the critical services they are.

- Metrics, tracing, and logging for AI calls
- Prompt versioning and A/B routing
- Cost guardrails and rate limiting
- Continuous evaluation so regressions don’t sneak in

**Your project:** Add observability to your Module 2 system — dashboards,
alerts, and a rollback plan.

### 4. Security and compliance for AI systems 🛡️

Build systems that are hard to misuse and easy to audit.

- Threat modeling for AI features
- Input filtering and output validation
- Guardrails that actually work
- Audit logging and privacy-aware design

**Your project:** Write a short security review and add guardrails to your
system.

### 5. Shipping a production capstone 🚢

Put it all together into something another engineer can run, monitor, and
extend.

- Deployment, CI/CD, and infrastructure basics
- Monitoring and on-call runbooks
- Documentation and handoff
- Showing business value

**Your project:** Ship an end-to-end AI system and present it in a capstone
review. This is the big one! 🎉

## 🛤️ Tracks

We offer two ways to go through the Academy. Same syllabus, different pace and
support.

### Challenger — Full-Time Track

For engineers who want to prove they can ship under real pressure.

- **Format:** 10-week immersive cohort
- **Best for:** Individual engineers ready to go all in
- **Selection:** Application + short technical screening
- **Time:** 80–100 hours/week of building
- **Finish line:** Demo-day presentation

### Accelerator — Team Track

For companies that want to level up a small group of engineers together.

- **Format:** 6-week immersive cohort
- **Best for:** Teams who need a focused step-out from delivery pressure
- **Selection:** Nominated by your company
- **Time:** Full-time step-out for the duration
- **Finish line:** Production-grade capstone tied to business ROI

## 🏅 Certification Plan

You earn certifications by shipping work, not by passing quizzes. Here are the
three levels:

### Level 1 — Foundations 🌱

- Finish the Module 1 self-study materials.
- Complete an applied design review.
- Ship one small artifact (a tool, API wrapper, or simple integration).

### Level 2 — Practitioner 🛠️

- Complete Modules 2 and 3.
- Build a RAG or agentic system with automated evals and observability.
- Pass a code review and systems-design conversation.

### Level 3 — Production Engineer 🚀

- Complete Modules 4 and 5.
- Ship a full production capstone with monitoring, security controls, docs,
  and a handoff record.
- Present your capstone to a review panel.

Level 3 is the standard the Academy uses to recommend engineers for high-trust,
AI-native engineering roles. You’ve got this. 💪

## 💾 Save it locally

This repo is intentionally text-only. You can:

```bash
git clone https://github.com/Vibe-Coding-Agency/vibe-coder-beginning-starter-pack.git
```

Then open it in any text editor or Markdown reader. No internet connection
required. Search it, annotate it, keep it forever.

## 🤝 Need help or want to join a cohort?

You don’t have to do this alone.

- 🌐 Learn more about the program:
  [Vibe Coding Academy](https://vibecodingagency.com/products/vibe-coding-academy/)
- 📖 Read the educational overview:
  [Academy resources](https://vibecodingagency.com/resources/vibe-coding-academy/)
- ✉️ Questions or cohort inquiries:
  [hello@vibecodingagency.com](mailto:hello@vibecodingagency.com?subject=Vibe%20Coding%20Academy%20cohort%20inquiry)

## 🙌 Welcome to the journey

AI engineering is moving fast, but the fundamentals are learnable. Start small,
ship often, and keep going. We’re glad you’re here.

Let’s build something great. 🚀

---

Built with care by [Vibe Coding Agency](https://vibecodingagency.com).
