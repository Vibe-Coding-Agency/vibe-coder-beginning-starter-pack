# 🔍 Module 2 — Building RAG and Agentic Systems

*Estimated reading time: 12 minutes*  
*Save this file. Come back whenever you are designing retrieval or agent logic.*

---

## What this module is about

Retrieval-Augmented Generation (RAG) and agents are the two most common ways to
build useful AI features on top of a language model. This module explains how
they work and what to watch out for when you build them.

## 📚 What is RAG?

RAG means: before asking the model to answer, fetch relevant documents and put
them in the prompt. The model then answers based on the retrieved content.

The classic flow looks like this:

```
User question
    ↓
Turn question into an embedding
    ↓
Search vector store for similar chunks
    ↓
Put the top chunks + question into the prompt
    ↓
Model generates an answer
    ↓
Optional: validate and cite sources
```

RAG is great when the answer depends on a specific body of knowledge that the
model does not already know or that changes often.

## ✂️ Chunking strategies

Chunking is how you split documents before embedding them. Bad chunking kills
good retrieval.

### Common approaches

- **Fixed-size chunks** — split every N tokens or characters. Simple but can
  cut sentences in half.
- **Sentence or paragraph chunks** — split at natural boundaries. Better for
  readability.
- **Semantic chunks** — group related sentences together using embeddings.
  More advanced.
- **Hierarchical chunks** — keep small chunks for retrieval and larger chunks
  for context. Useful for long documents.

### Practical tip

Start with paragraph-sized chunks with a small overlap. Measure retrieval
accuracy before you get fancy.

## 🔎 Retrieval, re-ranking, and query transformation

Retrieval is not just one cosine-similarity search. A good RAG system often
uses multiple stages.

1. **Initial retrieval** — vector search or keyword search to get candidates.
2. **Query transformation** — rewrite the user question into a better search
   query. This helps with vague or conversational inputs.
3. **Re-ranking** — a smaller model scores how relevant each candidate is to
   the question.
4. **Fusion** — combine results from multiple retrieval methods.

### Why re-rank?

Vector similarity is not the same as relevance. Re-ranking can push the truly
useful chunks to the top.

## 🛠️ What are agents?

An agent is a system that uses a model to decide what to do next. It can:

- Call tools (APIs, code runners, databases).
- Plan multi-step tasks.
- Reflect on results and retry.
- Maintain state across turns.

### Simple agent loop

```
1. Observe the current state.
2. Decide the next action.
3. Execute the action.
4. Observe the new state.
5. Repeat until done or until a limit is reached.
```

### Tool use

Tools are just functions the agent can call. The model is given a description
of each tool and must produce a valid call. The system executes the call and
returns the result.

Good tool design is half the battle. Each tool should:

- Do one thing clearly.
- Have a clear input schema.
- Return a result that the model can understand.
- Fail in a predictable way.

## 🎭 Multi-agent orchestration

Sometimes one agent is not enough. You might have:

- A planner agent that breaks a task into steps.
- A research agent that retrieves facts.
- A writer agent that produces output.
- A reviewer agent that checks quality.

Multi-agent systems can be powerful, but they add coordination overhead. Start
with one agent and split only when the logic gets too complex.

## ⚠️ Common RAG and agent pitfalls

- **Retrieving chunks without enough context** — the model gets fragments, not
  answers.
- **Trusting similarity scores blindly** — always spot-check retrieved chunks.
- **Letting agents loop forever** — set max iteration and timeout limits.
- **Unclear tool descriptions** — the agent picks the wrong tool.
- **No evals for retrieval** — you cannot improve what you do not measure.


## 💡 Worked example: internal docs bot

Your company has 200 pages of internal documentation. You want a bot that
answers “How do I set up the staging database?”

**Chunking:** Split each page by heading. Keep paragraphs intact.
**Retrieval:** Embed the chunks and the question. Fetch the top 5.
**Re-ranking:** Score the 5 chunks for relevance to the exact question.
**Generation:** Prompt: “Answer using only the context below. Cite the source
page. If the context does not contain the answer, say so.”

Without the “cite the source” instruction, the bot will hallucinate page names.
Without re-ranking, it may include irrelevant pages. These small details make
RAG usable.

## ✅ Module 2 checklist

- [ ] I chose a chunking strategy and can explain why.
- [ ] I have a retrieval pipeline with a search and a re-ranking step.
- [ ] My agent has clear tools with schemas and error handling.
- [ ] I set limits on agent loops (max steps, timeouts).
- [ ] I measure retrieval accuracy and end-to-end answer quality.

## 📝 Practice prompt

Take a help-desk scenario. Write a RAG pipeline that answers “How do I reset my
password?” from a set of help articles. Then write an agent that can open a
ticket if the answer is not good enough.
