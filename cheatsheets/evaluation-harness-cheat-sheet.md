# 🧪 Evaluation Harness Cheat Sheet

A one-page reminder for building a repeatable evaluation harness for your AI
system.

## What is an evaluation harness?

An evaluation harness is the code that runs your system against a dataset and
reports the results. It is not the model, the prompt, or the dataset. It is the
infrastructure that makes evaluation reliable and repeatable.

Without a harness, you are just eyeballing outputs and hoping for the best.

## The four pieces

| Piece | Job | Example |
|---|---|---|
| **Dataset** | A set of representative inputs and expected outputs. | `evals/support_tickets.jsonl` |
| **Task runner** | Calls your system on each example and captures the output. | A Python script or pytest suite. |
| **Metric** | Scores how close the output is to what you wanted. | Accuracy, F1, exact match, custom scorer. |
| **Reporter** | Shows results so you can compare over time. | CLI table, JSON report, dashboard. |

## A minimal harness template

```python
import json
from my_system import answer_question

def load_dataset(path):
    with open(path) as f:
        return [json.loads(line) for line in f]

def score(expected, actual):
    return 1.0 if expected.lower().strip() == actual.lower().strip() else 0.0

def run_eval(dataset_path):
    examples = load_dataset(path)
    total = 0
    correct = 0
    for ex in examples:
        actual = answer_question(ex["input"])
        s = score(ex["expected"], actual)
        total += 1
        correct += s
        print(f"Input: {ex['input'][:60]}... Score: {s}")
    print(f"Accuracy: {correct / total:.2%}")

if __name__ == "__main__":
    run_eval("evals/questions.jsonl")
```

Start here. Add complexity only when you need it.

## Dataset tips

- **Represent real traffic.** Synthetic examples are fine for bootstrapping,
  but real user inputs are better.
- **Include edge cases.** Empty inputs, very long inputs, ambiguous questions,
  and adversarial examples.
- **Version your dataset.** Treat it like code. Tag releases.
- **Keep expected outputs stable.** If you change the expected answer, you are
  changing the test.

## Choosing metrics

| Task type | Good metrics |
|---|---|
| Classification | Accuracy, precision, recall, F1 |
| Generation | Exact match, BERTScore, human rating, task success |
| RAG | Retrieval recall, answer relevance, citation accuracy |
| Agents | Task completion rate, steps used, error rate |
| Code | Execution success, unit test pass rate |

Pick one primary metric. Everything else is supporting detail.

## Regression testing workflow

1. Build your harness and dataset.
2. Establish a baseline score.
3. Make a change to your system.
4. Re-run the harness.
5. If the score drops, fix the change or expand the dataset.
6. If the score rises, commit both the change and the new baseline.

Run this in CI before every merge.

## Common mistakes

- **Evaluating on the training data.** Your system will look better than it is.
- **Only using one metric.** One number never tells the whole story.
- **Ignoring failures.** A failing example is a bug report. Investigate it.
- **Letting the dataset rot.** Update it as your system and users evolve.
- **No baseline.** You cannot tell if a change helped without a baseline.

## Quick checklist

- [ ] I have a dataset that represents real usage.
- [ ] I have one primary metric that matters to users.
- [ ] I can run the harness with a single command.
- [ ] The harness runs in CI.
- [ ] I compare results against a known baseline.
- [ ] I investigate every regression, not just the average score.

## Remember

A good harness makes you brave. You can change prompts, models, and code with
confidence because the harness will tell you if something broke. 🧪
