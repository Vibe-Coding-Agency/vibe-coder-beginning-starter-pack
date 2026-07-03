# 🛡️ Module 4 — Security and Compliance for AI Systems

*Estimated reading time: 10 minutes*  
*Save this file. Come back whenever you are reviewing an AI feature for risk.*

---

## What this module is about

AI features introduce new attack surfaces: prompt injection, data leakage,
toxic outputs, and more. This module teaches you to think like an attacker and
a regulator at the same time.

Security is not a one-time checklist. It is a habit of asking “what could go
wrong?” before shipping.

## 🎯 Threat modeling for AI

Threat modeling means listing the ways someone could abuse or break your
system. A simple framework for AI features:

1. **What is the worst thing an input could do?**
   - Inject instructions, leak data, generate harmful content.
2. **What is the worst thing an output could do?**
   - Reveal private training data, hallucinate legal advice, offend a user.
3. **Who are the actors?**
   - End users, attackers, insiders, third-party services.
4. **Where is the trust boundary?**
   - Any input from outside your system is untrusted.

Run this exercise before you write code. It is much cheaper than fixing an
incident.

## 🚧 Input validation and filtering

Treat user input as untrusted. Common defenses:

- **Instruction defense** — tell the model to ignore embedded instructions.
- **Allowlists** — accept only known-safe formats or values.
- **Denylists** — block known harmful patterns.
- **Output encoding** — never render model output directly into HTML, SQL, or
  shell commands without escaping.
- **Human-in-the-loop** — require approval for high-stakes actions.

### Practical tip

Allowlists are stronger than denylists. If you know the input should be an
email address, validate it as an email address. Do not just scan for bad words.

## 🛡️ Output validation and guardrails

Even with good inputs, models can produce bad outputs. Add guards:

- **Content filters** — block hate, violence, sexual content, etc.
- **Factuality checks** — for high-stakes claims, require a source.
- **Format validation** — if the output should be JSON, validate the schema.
- **Confidence thresholds** — refuse to answer when the model is unsure.
- **Post-processing** — remove PII, redact sensitive data.

## 📝 Audit logging

If something goes wrong, you need to know what happened. Log:

- Who made the request.
- What the input was.
- What model and prompt version were used.
- What the output was.
- What tools or data were accessed.
- Whether any guardrails triggered.

Keep logs secure and accessible only to authorized people.

## 🔒 Privacy-preserving design

- Do not send more data to the model than necessary.
- Avoid sending PII to third-party APIs unless required.
- Use data-retention settings offered by model providers.
- Consider on-prem or local models for highly sensitive workloads.
- Be transparent with users about what data is used and why.

## ⚖️ Compliance mapping

Different industries have different rules. You do not need to be a lawyer, but
you should know which regulations apply to your data:

- **GDPR / CCPA** — user data rights and consent.
- **HIPAA** — health data in the US.
- **SOC 2 / ISO 27001** — security controls for SaaS.
- **Sector-specific rules** — finance, government, etc.

Map each AI feature to the controls it must satisfy. Document the mapping.

## ✅ Module 4 checklist

- [ ] I have a threat model for my AI feature.
- [ ] Inputs are validated before they reach the model.
- [ ] Outputs are validated before they reach the user.
- [ ] I log requests, outputs, and guardrail triggers.
- [ ] I know which compliance frameworks apply and have documented controls.

## 📝 Practice prompt

Pick one AI feature. Write down three possible attacks and the defenses you
would add. Then list the data you would log for each request.
