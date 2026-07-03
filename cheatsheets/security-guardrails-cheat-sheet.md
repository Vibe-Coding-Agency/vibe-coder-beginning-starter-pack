# 🛡️ Security Guardrails Cheat Sheet

A quick checklist for making AI features safer.

## Before the model sees input

- [ ] Validate format (JSON, email, etc.).
- [ ] Check input length.
- [ ] Strip or escape risky content.
- [ ] Use allowlists when possible.
- [ ] Detect and handle prompt injection attempts.

## After the model produces output

- [ ] Validate output format if structured.
 [ ] Run content safety filters.
- [ ] Check for PII leakage.
- [ ] Refuse low-confidence answers.
- [ ] Encode output before rendering in HTML/SQL/shell.

## System-level controls

- [ ] Rate limiting per user and per IP.
- [ ] Max token limits per request.
- [ ] Circuit breakers for runaway loops.
- [ ] Audit logging enabled.
- [ ] API keys rotated regularly.
- [ ] Human approval for high-stakes actions.

## Questions to ask

- What is the worst input a user could send?
- What is the worst output the model could produce?
- What data would an attacker want to steal?
- Which compliance rules apply?
