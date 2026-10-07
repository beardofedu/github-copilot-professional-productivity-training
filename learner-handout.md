# GitHub Copilot for Professional Productivity

## Start with work, not a feature

Choose a task you already understand and can verify. Good first tasks are repeated, bounded, and low-risk.

Copilot can help you:

- **Understand** unfamiliar material.
- **Draft** a useful first version.
- **Transform** information into a better format.
- **Automate** repeatable steps.
- **Review** work for gaps and risks.

## Goal–Context–Constraints–Check

Use this pattern when you are unsure what to type:

```text
Goal:
What outcome do I need?

Context:
What does Copilot need to know about the source, audience, environment, or workflow?

Constraints:
What must it use, avoid, preserve, or limit?

Check:
How will I verify that the result is correct and safe?
```

## Example

```text
Goal: Create a script that identifies incomplete rows in a weekly CSV
and writes a Markdown summary.

Context: The columns are Item, Owner, DueDate, and Status. I run this
manually on Windows every Friday.

Constraints: Do not modify the CSV. Use built-in PowerShell features.
Explain the approach before showing code.

Check: Include a dry-run example and tests for valid, incomplete, and
empty input files.
```

## Choose the surface

| If the work is… | Start with… |
|---|---|
| Broad, ambiguous, or spread across tasks | Copilot app |
| In commands, files, or a terminal workflow | Copilot CLI |
| In scripts, configuration, or structured text | VS Code |
| In an issue, pull request, or repository | GitHub.com |

## Make it a conversation

1. Ask for a plan.
2. Inspect assumptions.
3. Request a small first version.
4. Test or verify it.
5. Share the exact result or error.
6. Refine only what needs improvement.

## Verify before use

- Does it match the source and intended outcome?
- Could it modify, overwrite, delete, or disclose anything?
- Is the information appropriate to share under organizational policy?
- Did you test it in the real environment or with representative data?
- For factual claims, did you open and verify the source?

## My one-week experiment

**Task:**  

**Copilot surface:**  

**Context I will provide:**  

**Constraint I will set:**  

**How I will check the result:**  

