# 📝 Prompt Engineering Cheat Sheet

Save this and refer back whenever your model is not doing what you want.

## The basics

- **Be specific.** Vague prompts give vague answers.
- **Give examples.** Show the model what good output looks like.
- **Assign a role.** “You are a careful code reviewer.”
- **Ask for reasoning.** “Explain your reasoning step by step.”
- **Set constraints.** “Answer in one paragraph.” “Use JSON.”

## A simple template

```markdown
Role: You are a [role].
Task: [Describe what to do.]
Context: [Background the model needs.]
Format: [How the output should look.]
Examples: [One or two examples of good output.]
```

## Common fixes

| Symptom | Fix |
|---|---|
| Output too long | Add a max length constraint. |
| Output too vague | Add examples or ask for specifics. |
| Wrong format | Show the exact JSON schema. |
| Model makes things up | Ask it to cite sources or say “I don’t know.” |
| Ignores instructions | Repeat the key instruction at the end. |

## Remember

A prompt is code. Version it, test it, and measure the results.
