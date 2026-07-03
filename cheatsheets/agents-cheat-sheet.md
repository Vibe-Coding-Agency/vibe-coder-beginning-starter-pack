# 🤖 Agents Cheat Sheet

A one-page reminder for building reliable agents.

## What an agent actually is

An agent is just a loop:

```
observe → decide → act → observe → decide → act → …
```

The model looks at the current state, picks an action, the system executes it,
and the result goes back to the model. Repeat until the task is done or a
limit is hit.

## When to use an agent

Use an agent when:

- The steps are not known in advance.
- The task needs decisions based on intermediate results.
- Tools or external data must be used dynamically.

Use a **pipeline** when the steps are fixed and predictable. Pipelines are
cheaper, faster, and easier to debug.

## The four parts of a good agent

| Part | Job | Tip |
|---|---|---|
| **System prompt** | Defines role, goals, and rules. | Keep it short. Put the most important constraint last. |
| **Tools** | Functions the agent can call. | One tool = one clear action. Good docs matter more than clever code. |
| **State / memory** | What the agent remembers between steps. | Start with explicit state. Avoid hidden memory early on. |
| **Controller** | Decides when to stop, retry, or escalate. | Always set a max step count and timeout. |

## Tool design checklist

- [ ] Does one tool do exactly one thing?
- [ ] Is the input schema strict and documented?
- [ ] Does it return a plain, parseable result?
- [ ] Does it fail safely with a useful error message?
- [ ] Can the model tell from the result what to do next?

If a tool returns raw stack traces or HTML, the agent will get confused.

## Common agent patterns

### ReAct-style

The model outputs both reasoning and an action. Great for transparency and
debugging.

```
Thought: I need the current weather.
Action: get_weather(location="Chicago")
Observation: 72°F, sunny.
Thought: Now I can answer the user.
```

### Plan-and-execute

The model first writes a plan, then executes each step. Better for multi-step
tasks where the plan can be shown to a user.

### Reflection

After each action, the model checks if the result matches expectations and
decides whether to continue, retry, or ask for help.

## Guardrails you should add

- **Max steps** — stop the loop after N iterations.
- **Timeout** — kill long-running calls.
- **Tool allowlist** — only expose tools the agent actually needs.
- **Output validation** — check the model’s tool call before executing it.
- **Human-in-the-loop** — require approval for irreversible actions.

## Typical mistakes

- Giving the agent too many tools. Start with 2–3.
- Letting the agent loop forever.
- Hiding state from the model. The model can only act on what is in its
  context.
- Trusting the agent to pick the right tool without clear descriptions.

## Quick template

```markdown
You are a helpful research assistant.

Rules:
- Use only the provided tools.
- If you cannot find the answer, say so.
- Stop after 5 steps or when the user’s question is answered.

Available tools:
1. search_web(query) — returns search results.
2. read_page(url) — returns the text of a web page.
3. final_answer(text) — returns the answer to the user.
```

Save this and come back whenever your agent starts acting weird. 🔧
