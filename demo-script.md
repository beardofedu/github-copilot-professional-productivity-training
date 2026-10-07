# Demonstration Script: One Task, Four Surfaces

## Scenario

A program coordinator receives a weekly CSV export and a few rough notes. They need to:

1. identify records with a missing owner or due date,
2. produce a short Markdown summary,
3. and create a GitHub issue for the follow-up work.

Use synthetic data throughout.

## Demo data

Create `weekly-status.csv`:

```csv
Item,Owner,DueDate,Status
Confirm venue,Avery,2026-10-12,In progress
Publish attendee guide,,2026-10-14,Not started
Verify accessibility,Jordan,,In progress
Send final reminder,Sam,2026-10-18,Not started
Archive materials,Avery,2026-10-22,Planned
```

Create `weekly-notes.txt`:

```text
Need follow-up on blank fields.
The summary should be readable in GitHub.
Do not change the CSV.
We need a repeatable process every Friday.
```

## 1. Copilot app — Shape the work

**Prompt:**

> I have a weekly CSV status export and rough notes. I need to identify records with a missing owner or due date, create a concise Markdown summary, and prepare a GitHub issue for follow-up. Before suggesting tools or code, break the work into steps, list what you need to know, and identify which decisions require human judgment.

**Teaching point:** Start by clarifying the task. Do not ask for code before understanding the workflow.

**Follow-up prompt:**

> Assume the CSV columns are `Item`, `Owner`, `DueDate`, and `Status`; the source file must never be changed; and the process will run manually every Friday. Recommend which parts belong in the CLI, VS Code, and GitHub.com. Include a verification step for each part.

## 2. CLI — Inspect safely

From the demo directory, ask Copilot CLI:

> Explain a read-only command I can use to confirm the CSV exists, display its header, and count its data rows. Do not run or suggest anything that modifies files. Explain each part of the command.

Run the proposed read-only command after inspection.

Then ask:

> Based on the header `Item,Owner,DueDate,Status`, propose a read-only way to identify rows that may have an empty Owner or DueDate. Warn me about any limitations of parsing CSV as plain text.

**Teaching point:** Ask for the safest first step and limitations, not merely a command.

## 3. VS Code — Create and refine the script

Open the demo folder in VS Code.

**Prompt:**

> Create a PowerShell script named `New-WeeklyStatusSummary.ps1`.
>
> **Goal:** Read `weekly-status.csv`, identify rows with a missing `Owner` or `DueDate`, and write `weekly-status-summary.md`.
>
> **Context:** The columns are `Item`, `Owner`, `DueDate`, and `Status`. The script runs manually on Windows every Friday.
>
> **Constraints:** Never modify the CSV. Use built-in PowerShell features only. Fail clearly if the file or expected columns are missing. Sort flagged records by Item. Keep the Markdown concise.
>
> **Check:** First explain your approach. Then provide the script and three manual test cases, including a valid file with no missing fields and an empty CSV.

Review the generated script before running it.

Ask:

> Review this script for assumptions, destructive behavior, unclear error messages, and edge cases. Do not change it yet. Rank findings by impact.

Then:

> Apply only the high-impact fixes. Add a `-WhatIf`-style preview option if that is meaningful for this script; otherwise explain why it is not.

Run against the synthetic data and inspect `weekly-status-summary.md`.

**Teaching point:** The first output is a draft. Review and testing are part of prompting.

## 4. GitHub.com — Make the work shareable

Open the demonstration repository on GitHub.com.

Use Copilot to help draft an issue:

> Draft a GitHub issue from this summary. Include:
>
> - a concise problem statement,
> - the affected records,
> - acceptance criteria,
> - an owner-confirmation checklist,
> - and a verification step.
>
> Do not invent owners or due dates. Mark unknown values as `Needs input`.

Review the issue before publishing. If this is a live environment, stop before submission unless publishing the synthetic issue was explicitly planned.

**Teaching point:** Copilot can turn individual work into a clear, reviewable handoff, but the user owns what is published.

## Recovery prompts

If a generated answer is too generic:

> You made assumptions that are not in my request. List those assumptions, ask only the questions that would materially change the result, and then produce a smaller first version.

If code fails:

> Here is the exact command, complete error, environment, and relevant input. Explain the likely cause, propose the smallest diagnostic check, and wait before changing the script.

If the answer is too complex:

> Rewrite this for a person who understands the work process but is not a professional developer. Preserve the safeguards and verification steps.

