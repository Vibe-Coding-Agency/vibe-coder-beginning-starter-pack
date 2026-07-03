# ✅ Production Readiness Checklist

Use this before you tell users your AI feature is live.

## Evaluation

- [ ] I have at least 20 representative test cases.
- [ ] I know the current pass rate.
- [ ] I have a regression suite in CI.
- [ ] I have measured failure modes.

## Operations

- [ ] Latency, error rate, and cost are monitored.
- [ ] Alerts are configured.
- [ ] Traces capture the full request flow.
- [ ] Prompts and model versions are logged.

## Security

- [ ] Threat model documented.
- [ ] Input validation in place.
- [ ] Output validation in place.
- [ ] Audit logging enabled.
- [ ] Rate limits configured.

## Deployment

- [ ] Staging environment exists.
- [ ] CI/CD pipeline runs tests and evaluations.
- [ ] Rollback plan documented.
- [ ] Infrastructure defined as code.

## Documentation

- [ ] README explains what the feature does.
- [ ] Runbooks cover common incidents.
- [ ] Handoff doc exists.
- [ ] Business value metrics defined.
