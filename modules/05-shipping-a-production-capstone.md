# 🚢 Module 5 — Shipping a Production Capstone

*Estimated reading time: 12 minutes*  
*Save this file. Come back whenever you are about to deploy something real.*

---

## What this module is about

A prototype runs on your laptop. A production system runs where users can reach
it, stays up, handles errors, and can be maintained by someone else. This
module covers the last mile: deployment, monitoring, documentation, and
handoff.

## 🚀 Deployment basics

Your AI feature needs to live somewhere. Common patterns:

- **Serverless functions** — great for intermittent traffic, easy to scale.
- **Containers** — consistent environment, works almost anywhere.
- **Managed AI platforms** — some providers offer hosted endpoints.
- **Edge / CDN** — for latency-sensitive or static parts.

Pick the simplest thing that meets your scale and latency needs. You can
always move later.

## 🔄 CI/CD for AI systems

Continuous integration and deployment mean every change is tested and deployed
automatically. For AI systems, your pipeline should:

1. Run unit tests for code.
2. Run the regression evaluation suite.
3. Check for prompt or model version changes.
4. Deploy to a staging environment.
5. Run smoke tests.
6. Deploy to production with a canary or rollback plan.

Never deploy a new prompt or model without running evaluations first.

## 🏗️ Infrastructure as code

Write your infrastructure in code using tools like Terraform, Pulumi, or CloudFormation.

Benefits:

- You can recreate the environment in minutes.
- Changes are reviewed in pull requests.
- You know exactly what is running.
- Rollbacks are easier.

Start small: define the compute, database, vector store, and secrets. Expand
from there.

## 📡 Monitoring and alerting

Production monitoring answers three questions:

1. **Is it up?** — health checks, uptime monitoring.
2. **Is it fast enough?** — latency percentiles.
3. **Is it right?** — error rates, evaluation scores, user feedback.

Set alerts for:

- Error rate above a threshold.
- Latency p95 above a threshold.
- Cost per hour above a threshold.
- Evaluation score drop.

## 📖 Runbooks

A runbook is a step-by-step guide for common incidents. Write these before you
need them:

- How to roll back a bad deployment.
- How to disable the AI feature if it misbehaves.
- How to rotate API keys.
- How to handle a model provider outage.
- How to investigate a specific bad output.

Keep runbooks short. One page per scenario is usually enough.

## ✍️ Documentation and handoff

If you get hit by a bus tomorrow, can someone else run your system? Document:

- What the system does and why it exists.
- Architecture diagram.
- How to run it locally.
- How to deploy it.
- How to update the prompt or model.
- How to read the dashboards.
- Who to page when things break.

## 💼 Showing business value

Engineering is not done until the business understands the outcome. Be ready
to report:

- Time saved.
- Errors reduced.
- Customer satisfaction impact.
- Cost compared to the old way.
- Uptime and reliability.

Use real numbers when you can. Estimates are fine early on, but replace them
with measured data as soon as possible.

## ✅ Module 5 checklist

- [ ] My system is deployed to a staging and production environment.
- [ ] CI/CD runs tests and evaluations before deploying.
- [ ] Infrastructure is defined as code.
- [ ] I have dashboards and alerts.
- [ ] I have runbooks for common incidents.
- [ ] Documentation is good enough for another engineer to take over.

## 📝 Practice prompt

Imagine you are handing off your capstone to a teammate. Write a one-page
handoff doc with: what it does, how to deploy it, how to monitor it, and how to
roll it back.
