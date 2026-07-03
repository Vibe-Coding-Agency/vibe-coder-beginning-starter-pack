# 🔍 RAG Pipeline Cheat Sheet

A quick reference for building retrieval-augmented generation systems.

## The pipeline

```
Documents
    ↓
Chunk
    ↓
Embed
    ↓
Store in vector database
    ↓
User asks a question
    ↓
Embed question
    ↓
Retrieve top-K chunks
    ↓
Re-rank (optional but recommended)
    ↓
Generate answer with context
    ↓
Validate and cite
```

## Chunking rules of thumb

- One paragraph or one section per chunk.
- 200–500 tokens per chunk is a good starting point.
- Add overlap of one sentence between chunks.
- Preserve semantic boundaries.

## Retrieval tips

- Use keyword search + vector search together (hybrid) when possible.
- Re-rank with a cross-encoder for better relevance.
- Retrieve more chunks than you send to the model, then filter.
- Always check retrieved chunks during development.

## Generation tips

- Include citations or source IDs in the prompt.
- Tell the model to say “I don’t know” when context is insufficient.
- Limit the answer length to reduce hallucination.

## Red flags

- Chunks cut off mid-sentence.
- Retrieved chunks are irrelevant.
- Model answers from memory instead of context.
- No citation or source tracking.
