# 🍳 Failure Mode Cookbook

A quick recipe book for common AI system problems.

## “The model made something up”

**Likely causes:**
- The prompt did not give enough context.
- The model was asked a question outside its knowledge.
- The temperature was too high.

**Fixes:**
- Add RAG or restrict the answer to provided context.
- Lower temperature for factual tasks.
- Tell the model to say “I don’t know.”

## “The answer is technically right but useless”

**Likely causes:**
- The task description is vague.
- The output format is not constrained.
- The evaluation does not match user needs.

**Fixes:**
- Add examples of good output.
- Specify audience, length, and format.
- Collect user feedback and re-evaluate.

## “It works locally but fails in production”

**Likely causes:**
- Different model version in production.
- Longer inputs in production exceed context limits.
- Missing error handling for timeouts or provider errors.

**Fixes:**
- Pin model versions.
- Measure input lengths from real traffic.
- Add retries, fallbacks, and circuit breakers.

## “Costs are unexpectedly high”

**Likely causes:**
- Inputs are longer than expected.
- A loop is running unbounded.
- A large model is used for simple tasks.

**Fixes:**
- Add token limits and input truncation.
- Cap agent iteration counts.
- Route simple tasks to smaller models.

## “Users are jailbreaking the system”

**Likely causes:**
- No input validation.
- Output is rendered without escaping.
- System prompt leaks into output.

**Fixes:**
- Validate inputs and filter dangerous patterns.
- Escape output before rendering.
- Add output guardrails that detect system-prompt content.

## General debugging workflow

1. Reproduce the failure with a trace.
2. Identify which component failed: input, retrieval, model, or output.
3. Add the case to your evaluation suite.
4. Fix the component.
5. Re-run the suite to confirm nothing else broke.
