# 🌳 Decision Trees

Use these when you are not sure which approach to take.

## Should I use RAG, fine-tuning, or just a prompt?

```
Does the answer depend on private or frequently changing data?
├── Yes → Use RAG.
│         Does the model need a specific style or format?
│         ├── Yes → Add few-shot examples in the prompt.
│         └── No  → Plain RAG is enough.
└── No  → Does the task need specialized knowledge the model lacks?
          ├── Yes → Consider fine-tuning or a domain-specific model.
          └── No  → Start with a well-crafted prompt.
```

## Should I build an agent or a pipeline?

```
Are the steps fixed and predictable?
├── Yes → Build a pipeline. It is simpler and easier to debug.
└── No  → Does the task require decisions based on intermediate results?
          ├── Yes → Build an agent.
          └── No  → Build a pipeline with conditional branches.
```

## Which model should I use?

```
Is this a high-volume, simple task?
├── Yes → Use the smallest, cheapest model that works.
└── No  → Is reasoning, code, or complex generation required?
          ├── Yes → Use a capable frontier model.
          └── No  → Test a mid-size model first.
```

## Should I add a guardrail?

```
Is this output going to a user?
├── Yes → Validate it.
Is this input from a user?
├── Yes → Validate it.
Is this action irreversible or high-stakes?
├── Yes → Add human approval.
```

When in doubt, add observability first. You cannot decide what to fix until you
know what is breaking.
