# Demonstration Script: Multi-Source Report in Agent Mode

## Scenario

A five-person team produces a weekly account-health report. The process currently requires manually joining CRM and product-usage exports, comparing the results with the prior week, finding records that do not reconcile, and writing a summary.

The starter workspace contains:

- `data/crm_accounts.csv`
- `data/product_usage.csv`
- `data/prior_week.csv`
- `data/account_aliases.json`
- `DEMO-BRIEF.md`

The desired capability produces:

- `output/reconciled_accounts.csv`
- `output/exceptions.csv`
- `output/weekly-account-health.md`
- a repeatable Python workflow,
- automated tests,
- `RUNBOOK.md`,
- and `prompts/build-weekly-report.prompt.md`.

## 1. Orient the room

Open `demo-workspace/` in VS Code.

Point to:

- the Explorer and input files,
- Copilot Chat,
- the Agent Mode selector,
- and the integrated terminal.

Do not explain every control. The orientation should take no more than seven minutes including the opening poll.

## 2. Ask Agent Mode to inspect before building

Use Agent Mode:

> Inspect this workspace and read `DEMO-BRIEF.md` plus every file under `data/`. Do not create or modify files yet.
>
> Report:
>
> 1. the relationships you infer between the sources,
> 2. data-quality and reconciliation risks,
> 3. decisions that cannot be made safely from the files,
> 4. a proposed output contract,
> 5. and an implementation and validation plan.
>
> Treat unmatched records as visible exceptions. Do not invent mappings.

Pause and review the plan.

Ask the audience:

> Which assumption would be most dangerous if the agent got it wrong?

If necessary, clarify:

> Use exact `account_id` matches first. Use only mappings explicitly present in `account_aliases.json` as the fallback. Everything else must go to the exception output.

**Teaching point:** Agent Mode should inspect the project and expose assumptions before it changes the project.

## 3. Build the smallest end-to-end workflow

Prompt:

> Implement the smallest complete version of the workflow described in `DEMO-BRIEF.md`.
>
> Requirements:
>
> - use standard Python only,
> - keep source files unchanged,
> - resolve usage records by exact account ID and then the approved alias map,
> - write unresolved or invalid records to `output/exceptions.csv`,
> - calculate adoption percentage and week-over-week active-user change,
> - apply the documented risk rules,
> - write reconciled detail to `output/reconciled_accounts.csv`,
> - write an executive-friendly Markdown report,
> - and fail clearly when required files or columns are missing.
>
> Before editing, restate the files you plan to create and the validation you will run. Then implement, run the workflow, and summarize the actual outputs.

When Agent Mode proposes terminal commands, read them before approval.

After it runs, inspect:

- the terminal result,
- `output/exceptions.csv`,
- several rows of `output/reconciled_accounts.csv`,
- and the claims in `output/weekly-account-health.md`.

**Teaching point:** A generated file is not evidence. Running the workflow and inspecting the outputs is part of the task.

## 4. Add tests where failure matters

Prompt:

> Identify the four behaviors most likely to produce a plausible but incorrect report. Add focused automated tests for them using Python's standard `unittest` library.
>
> At minimum cover:
>
> - an approved alias resolving to the correct CRM account,
> - an unknown key remaining unmatched,
> - zero licensed users not causing a divide-by-zero error,
> - and a missing owner triggering the expected risk flag.
>
> Run the tests and report the result. Do not weaken business rules merely to make a test pass.

Ask:

> What important behavior is still not proven by these tests?

**Teaching point:** Ask the agent to select tests based on consequence, not just coverage.

## 5. Review the work as a skeptical teammate

Prompt:

> Review the implementation and generated outputs as a skeptical teammate.
>
> Look specifically for:
>
> - silent record loss,
> - incorrect joins,
> - non-deterministic output,
> - date assumptions,
> - misleading report language,
> - hard-coded values that should be configuration,
> - and instructions a teammate would need.
>
> Rank findings by impact. Do not edit yet.

Discuss the findings, then direct a bounded refinement:

> Apply the high-impact fixes only. Re-run the tests and workflow, then show which outputs changed and why.

**Teaching point:** Review and refinement are separate decisions. Do not authorize an unbounded rewrite.

## 6. Package the capability for a small team

Prompt:

> Package this workflow for a teammate.
>
> Create:
>
> 1. `RUNBOOK.md` with purpose, prerequisites, input contracts, the run command, outputs, review steps, and known limitations.
> 2. `prompts/build-weekly-report.prompt.md` containing a reusable Agent Mode prompt for next week's exports.
> 3. A concise handoff summary explaining what is automated, what remains human judgment, what exceptions require review, and how the result was validated.
>
> Keep the documentation short enough that a teammate will actually use it.

Show the final project structure in Explorer.

Do not draft a GitHub issue. The team handoff is the reviewable project folder: implementation, prompt, runbook, tests, output, and exceptions.

## Brief positioning of the other tools

Use no more than three minutes total:

- **Copilot app:** better when the work begins as cross-project planning or a broad brief.
- **Copilot CLI:** better when the work is command-first and the terminal is the primary workspace.
- **VS Code + Agent Mode:** best here because the task spans data files, implementation, execution, tests, documentation, and review.

## Recovery prompts

If Agent Mode starts coding too early:

> Stop editing. Return to inspection and list the assumptions that would affect reconciliation or report accuracy.

If it guesses a match:

> Remove inferred mappings that are not explicitly supported by an exact ID or the approved alias file. Preserve those records as exceptions.

If it produces a polished but unsupported claim:

> Trace each number in the report to the source rows and calculation that support it. Mark anything not supported as an open question.

If the implementation becomes too complex:

> Reduce this to the smallest end-to-end workflow that preserves explicit reconciliation, visible exceptions, tests, and a reviewable report.

If a command fails:

> Use the exact command, error, environment, and current file state as evidence. Propose the smallest diagnostic step before changing code.

