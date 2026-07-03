# 📊 Module 3 — Model Operations and Observability

*Estimated reading time: 10 minutes*  
*Save this file. Come back whenever your AI feature is running in production.*

---

## What this module is about

A model in production is a service. It needs monitoring, versioning, cost
controls, and a way to detect regressions. This module covers the operations
side of AI systems — often called **LLMops** or **model operations**.

## 📈 Metrics you should track

Not every number matters. Start with these:

| Metric | Why it matters |
|---|---|
| **Latency (p50, p95, p99)** | Users notice slow responses. |
| **Cost per request / per user** | Models can get expensive fast. |
| **Token usage** | Helps you optimize prompts and catch runaway inputs. |
| **Error rate** | Failed calls, timeouts, bad outputs. |
| **Evaluation score** | Is quality getting better or worse over time? |
| **User feedback** | Thumbs up/down, corrections, support tickets. |

Track these in a dashboard. Review them at least weekly when you are iterating.

## 🔍 Tracing

A **trace** is the full story of one request: the input, the model call, the
tool calls, the retrieved documents, the final output, and any errors.

Tracing helps you answer questions like:

- Why did this user get a bad answer?
- Which retrieval chunk caused the hallucination?
- How long did the database query take?

### What to capture

- Input and output.
- Model name and version.
- Prompt template used.
- Tool calls and their results.
- Retrieved documents or context.
- Latency of each step.
- User and session identifiers.

Tools like Langfuse, LangSmith, or a simple structured logger can do this.

## 🏷️ Prompt versioning

Prompts are code. Treat them like code:

- Store prompts in version control.
- Give each version an ID.
- Log which version was used for each request.
- Run evaluations before promoting a new version.

This matters because a small prompt change can cause big quality shifts.

## 🚦 Routing and fallbacks

Not every request needs the biggest, most expensive model. A common pattern:

- Use a small/cheap model for simple classification or routing.
- Use a large model only for complex generation.
- Fall back to another provider if the first one is down or slow.

This is sometimes called a **model gateway**. It saves money and improves
reliability.

## 💰 Cost guardrails

Set limits before you need them:

- Per-user daily token limits.
- Per-request max token limits.
- Alerts when spend exceeds a threshold.
- Circuit breakers for runaway loops.

A good guardrail is invisible until it saves you from a surprise bill.

## 🔄 Continuous evaluation

Production data changes. A prompt that worked last month may fail this month.

Set up a **regression suite**: a set of representative inputs with expected
outputs. Run it automatically:

- Before every prompt or model change.
- Nightly against a sample of production traffic.
- After every model version update.

If the score drops, stop the rollout and investigate.


## 💡 Worked example: the Friday latency spike

You deploy a new prompt on Friday. On Monday, users complain the feature is
slow.

With good observability, you open the dashboard and see:
- p95 latency jumped from 800 ms to 4 seconds.
- Token usage per request tripled.
- The new prompt includes a long system message that was not measured during
  testing.

With a trace, you find the exact request and the prompt version. You roll back
to the previous version, add the prompt to your regression suite, and re-deploy
a shorter version on Tuesday. Without observability, you are guessing.

## ✅ Module 3 checklist

- [ ] I have a dashboard with latency, cost, token usage, and error rate.
- [ ] I capture traces for at least a sample of requests.
- [ ] My prompts are versioned and logged.
- [ ] I have routing or fallback logic for model/provider failures.
- [ ] I run a regression evaluation suite before deploying changes.

## 📝 Practice prompt

Pick a small AI feature. Write down the five metrics you would track, the
alerts you would set, and the regression test you would run before each
deployment.
