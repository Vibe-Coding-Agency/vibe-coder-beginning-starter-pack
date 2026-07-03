# 🐝 Agent Swarms Cheat Sheet

A quick reference for building systems with multiple agents working together.

## What is an agent swarm?

A swarm is a group of agents that collaborate to solve a problem no single
agent can handle well. Each agent usually has a narrow role, and they pass work
or messages between each other.

## When to consider a swarm

- One agent has too many tools or responsibilities.
- Different parts of a task need different expertise.
- You want parallel work or independent review.
- A task has clear handoffs (research → write → review → publish).

If one agent with a good prompt and a few tools can do it, start there.

## Common swarm patterns

### 1. Manager + workers

A central agent plans the work and delegates sub-tasks to specialist agents.

```
User request
    ↓
Manager agent breaks it into tasks
    ↓
Worker A, Worker B, Worker C each do one task
    ↓
Manager combines the results
    ↓
Final answer
```

Best for: complex tasks with clear sub-tasks.

### 2. Pipeline / assembly line

Each agent does one step and passes output to the next.

```
Research agent → Writer agent → Editor agent → Publisher agent
```

Best for: repeatable workflows with known stages.

### 3. Peer-to-peer

Agents share a message board or queue. Any agent can pick up work it is suited
for.

Best for: open-ended collaboration or multi-turn discussions.

### 4. Generator + critic

One agent produces output. Another agent critiques it. The producer revises.

```
Draft → Review → Revise → Review → Final
```

Best for: quality-critical output like code, writing, or designs.

## Shared state vs. message passing

| Approach | Pros | Cons |
|---|---|---|
| **Shared state** | Everyone sees the same context. | Can become a bottleneck or source of conflicts. |
| **Message passing** | Loose coupling, easier to scale. | Harder to debug if messages are lost. |
| **Hybrid** | Best of both worlds. | More complex to design. |

Start with message passing. Upgrade to shared state only when agents need
constant access to the same data.

## Coordination basics

- Give each agent a **clear role** in its system prompt.
- Define the **input and output format** for every handoff.
- Decide who starts, who finishes, and how agents know they are done.
- Set a **global timeout** so the swarm cannot run forever.
- Log every message and handoff. Swarms are hard to debug without traces.

## Typical mistakes

- Too many agents. Two or three well-defined agents usually beat ten vague ones.
- Unclear handoffs. If agents do not know who does what next, the swarm stalls.
- No termination condition. A swarm can debate itself forever.
- Hidden shared state. Make state changes explicit and logged.
- Forgetting the user. The final answer should be coherent, not a dump of
  agent outputs.

## Mini pattern library

| Pattern | Use it when… |
|---|---|
| **Map-reduce** | One agent splits work, many agents process pieces, one combines results. |
| **Voting** | Multiple agents solve the same problem and the majority wins. |
| **Moderator** | One agent keeps discussion on track and decides when to move on. |
| **Specialist panel** | Different agents represent different viewpoints (security, UX, legal). |

## Quick template for a 3-agent pipeline

```markdown
Agent 1 — Researcher
Goal: Gather relevant facts.
Output: A bullet list of findings with sources.

Agent 2 — Writer
Goal: Turn findings into a clear answer.
Input: Researcher’s bullet list.
Output: A draft answer.

Agent 3 — Editor
Goal: Check accuracy, tone, and completeness.
Input: Writer’s draft.
Output: Final answer or revision request.
```

Keep this nearby the first time you build a swarm. It will save you hours. 🐝
