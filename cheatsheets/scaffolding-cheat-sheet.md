# 🔧 Scaffolding Cheat Sheet

*Also called a harness, controller, or orchestration layer.*

A one-page reminder for the code that wraps a model and makes it usable in
production.

## What is scaffolding?

The **model** is the brain. The **scaffolding** is everything else: the code
that calls the model, runs tools, tracks state, parses outputs, handles
errors, and decides when to stop.

If the model is the engine, the scaffolding is the car around it.

## What scaffolding does

| Job | Why it matters |
|---|---|
| **Prompt assembly** | Builds the final prompt from templates, examples, and context. |
| **Model calling** | Sends the request, handles retries, timeouts, and fallbacks. |
| **Output parsing** | Turns model text into structured data your code can use. |
| **Tool execution** | Calls functions the model asks for and returns results. |
| **State management** | Keeps track of conversation history, memory, and intermediate results. |
| **Loop control** | Decides when to keep going, retry, or finish. |
| **Error handling** | Catches bad outputs, failed tools, and provider errors. |
| **Logging / tracing** | Records what happened so you can debug and improve. |

## Minimal scaffolding for a tool-using agent

```python
import json

def run_agent(user_input, tools, max_steps=5):
    state = {"input": user_input, "messages": []}

    for step in range(max_steps):
        # 1. Build prompt
        prompt = build_prompt(state, tools)

        # 2. Call model
        response = call_model(prompt)

        # 3. Parse output
        action = parse_action(response)

        # 4. Decide what to do
        if action["type"] == "final_answer":
            return action["answer"]

        if action["type"] == "tool_call":
            # 5. Execute tool
            result = execute_tool(action["tool"], action["args"])

            # 6. Update state
            state["messages"].append({
                "step": step,
                "action": action,
                "result": result,
            })
        else:
            # Unknown action: log, retry, or stop
            handle_bad_action(action)

    return "I ran out of steps without finishing."
```

This is the shape of almost every agent system.

## Key design decisions

### Where does the state live?

- **In-memory** — simplest, but lost if the process restarts.
- **Database / cache** — survives restarts, supports long-running tasks.
- **Thread-local / request context** — good for web apps.

Start in-memory. Move to a store when you need persistence.

### How do you parse model output?

- **Structured output / JSON mode** — ask the model to return JSON. Validate the
  schema.
- **Tool-calling API** — the model returns a structured tool call. Easier to
  parse reliably.
- **Regex / string parsing** — fast but fragile. Use only for simple cases.

Prefer tool-calling APIs or JSON mode. They save hours of parsing pain.

### How do you handle errors?

- **Model timeout** → retry with backoff, then fallback or fail gracefully.
- **Bad output format** → return a clear error to the model and ask it to try
  again.
- **Tool failure** → return the error as an observation. Do not crash the loop.
- **Max steps reached** → stop and report incomplete status.

A good harness never lets one bad call kill the whole task.

## Common scaffolding patterns

| Pattern | Use it when… |
|---|---|
| **ReAct loop** | The model needs to reason and act repeatedly. |
| **Plan-then-execute** | The task has clear phases. |
| **Tool-calling API** | You want reliable, parseable tool requests. |
| **Human-in-the-loop** | Some actions need approval. |
| **Multi-turn conversation** | The user and agent go back and forth. |

## Typical mistakes

- Putting too much logic in the prompt instead of the scaffolding.
- Letting the model decide when to stop without a hard limit.
- Not validating tool arguments before executing them.
- Losing conversation history between calls.
- Logging only the final output, not the full trace.
- Running untrusted model output as code or commands.

## Quick checklist

- [ ] I can assemble a prompt from templates and state.
- [ ] I can call the model and retry on failure.
- [ ] I can parse the model’s output safely.
- [ ] I can execute tools and return results.
- [ ] I track state across steps.
- [ ] I enforce a max step count and timeout.
- [ ] I log the full trace for debugging.

## Remember

The model is only one piece of the system. Solid scaffolding is what turns a
clever demo into a product you can ship. 🔧
