# 🧠 Module 1 — Foundations of AI-native Engineering

*Estimated reading time: 10 minutes*  
*Save this file. Come back whenever you need a reminder of the big picture.*

---

## What this module is about

Before you write a single line of AI code, it helps to know how the pieces fit
together. This module builds the mental model that separates a neat demo from a
system you can actually ship.

By the end, you should be able to look at any AI feature and ask the right
questions: What is the model supposed to do? How do I know it worked? What
happens when it fails? How much does it cost to run?

## 🤖 Models, agents, and systems

A **model** is just a function that turns an input into an output. A large
language model (LLM) takes tokens and predicts the next tokens. That is it. The
magic is in how you wrap that function into a useful system.

An **agent** is a loop: the model looks at a situation, decides on an action,
acts, observes the result, and repeats. The action might be calling a tool,
calling an API, or generating text for a user.

Most production systems are not pure agents. They are **pipelines**: retrieval,
then generation, then validation, then logging. Use an agent when the task
really needs iteration and decision-making. Use a pipeline when the steps are
predictable.

### Quick reminder

- **Model** = prediction engine.
- **Agent** = loop of thought → action → observation.
- **Pipeline** = fixed sequence of steps.
- **System** = model/agent/pipeline + infrastructure + monitoring + guardrails.

## 📏 Context windows and tokens

Models do not read words; they read **tokens**. A token is roughly a syllable or
a common word piece. In English, 100 tokens is about 75 words.

Every model has a **context window**: the maximum number of tokens it can
process in one call. If you feed it more than that, something gets dropped or
the call fails.

### Why this matters

- Long inputs cost more and run slower.
- Summarizing or chunking long documents is usually required.
- The model cannot “remember” anything outside the context window unless you
  put it there.

### Practical tip

When you design a feature, estimate the token count of a typical input and
output. Double it for safety. Then check the pricing for the model you chose.

## 🧪 Evaluation design

“Does it look good?” is not an evaluation. A good evaluation has three parts:

1. **A clear task.** What exactly should the system do?
2. **A dataset.** Representative inputs and the correct or acceptable outputs.
3. **A metric.** A number that tells you if you are getting better or worse.

### Common metrics

- **Exact match** — output equals expected output.
- **F1 / accuracy** — classification-style tasks.
- **BERTScore / BLEU** — similarity between generated and reference text.
- **Human rating** — useful but expensive and slow.
- **Task-specific metrics** — did the SQL query run? Did the API call succeed?

### Beginner-friendly evaluation rule

Start with a small set of hand-written examples — 20 to 50 is enough. Run your
system on them after every change. If the score drops, you broke something.

## 🧰 The production toolchain

A real AI system touches more than the model. Here are the moving parts you
will meet:

| Layer | What it does | Examples |
|---|---|---|
| **Model** | Generates text, embeddings, or structured output | OpenAI, Anthropic, local models |
| **Gateway / router** | Routes requests, handles retries, rate limits, fallbacks | LiteLLM, custom proxy |
| **Cache** | Saves money by reusing similar requests | Redis, semantic cache |
| **Vector store** | Stores embeddings for retrieval | Pinecone, Weaviate, pgvector |
| **Observability** | Logs, traces, metrics | Langfuse, LangSmith, custom |
| **Guardrails** | Validates inputs and outputs | Rule-based + model-based checks |

You do not need all of these on day one. But you should know they exist so you
can add them when the time comes.

## ⚠️ Failure modes to expect

AI systems fail differently than traditional software. They are probabilistic,
not deterministic. Here are the classics:

- **Hallucination** — the model makes up facts.
- **Instruction drift** — the model does something close but wrong.
- **Context overflow** — inputs are too long.
- **Tool misuse** — an agent calls the wrong function or with bad arguments.
- **Latency / cost surprises** — a spike in traffic makes the feature unusable.
- **Regression** — a new prompt or model version performs worse on old cases.

The goal is not to eliminate every failure. The goal is to detect failures,
handle them gracefully, and measure them.

## ✅ Module 1 checklist

- [ ] I can explain the difference between a model, an agent, and a pipeline.
- [ ] I can estimate token counts for my inputs and outputs.
- [ ] I have written at least 20 evaluation examples for one task.
- [ ] I have listed the likely failure modes for my feature.
- [ ] I have sketched the toolchain my system will need.

## 📝 Practice prompt

Pick one AI feature idea. Write one paragraph describing the task, the success
criteria, and three ways it could fail. Then write five input/output examples.

That one page is more valuable than a hundred blog posts.
