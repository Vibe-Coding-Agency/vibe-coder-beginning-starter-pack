# 📊 Observability Cheat Sheet

What to watch when an AI system is live.

## Metrics dashboard

Track these at minimum:

- Requests per minute.
- Latency p50, p95, p99.
- Error rate.
- Cost per request / per hour.
- Token usage (input and output).
- Evaluation score over time.
- User feedback (thumbs up/down).

## Every trace should include

- Timestamp.
- User / session ID.
- Input and output.
- Model name and version.
- Prompt version ID.
- Tool calls and results.
- Retrieved context (for RAG).
- Latency per step.
- Any guardrail triggers.

## Alerts you actually need

- Error rate > 1% for 5 minutes.
- p99 latency above your SLA.
- Hourly cost above budget.
- Evaluation score drops below threshold.
- Spike in user-reported bad outputs.

## Useful habit

Review a sample of traces every week. You will spot problems before your users do.
