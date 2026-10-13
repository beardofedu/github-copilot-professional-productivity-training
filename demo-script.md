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

### Instructor review guide: workflow and generated outputs

#### Implementation script or scripts

- **Expected structure:** A small standard-library workflow should read the four fixed inputs, validate required columns, resolve exact IDs before aliases, calculate metrics and flags, and write all three outputs. The report date should be explicitly set to `2026-10-09`, ideally as a named constant or command argument rather than scattered literals.
- **Verify:** Find the exact-ID-first branch, the only approved aliases (`CONTOSO-ENERGY` → `ACCT-1002` and `AW-004` → `ACCT-1004`), the zero-license guard, and explicit handling for unmatched usage and CRM accounts with no current usage. The run should exit successfully, name the files written, and report counts that reconcile five resolved usage keys, `UNKNOWN-77`, and missing current usage for `ACCT-1006`.
- **Narrate:** The code is valuable because the business rules are visible and repeatable, not because Copilot produced a lot of code. Show where uncertainty becomes an exception instead of being hidden.
- **Red flags:** The script uses today's date, hard-codes an unapproved match, modifies `data/`, silently drops a row, uses integer division, catches an error and still reports success, or claims six clean reconciliations. A successful run should have no traceback and should return exit code 0; a missing file or required column should produce a clear non-zero failure.

#### `output/reconciled_accounts.csv`

- **Expected structure:** One header row plus reviewable account detail with source identity, current and prior usage, adoption, week-over-week change, and risk or review reasons. All five resolved usage records should be traceable even if the implementation places an invalid resolved record only in the exception file.
- **Verify:** Representative values are `ACCT-1001` at `72%` adoption and `+4` active users, `ACCT-1002` at `32.5%` and `-3`, `ACCT-1003` at `22.5%` and `-4`, and `ACCT-1004` at `95%` and `+4`. `ACCT-1005` must show adoption as unavailable—not `0%`—because both active and licensed users are zero.
- **Narrate:** Spot-check values back to both source files. Emphasize that a plausible percentage is not enough; identity resolution, denominator handling, prior-week comparison, and the reason for each flag all need evidence.
- **Red flags:** Alias keys appear as new accounts, percentages are rounded into misleading whole numbers, `ACCT-1005` causes a divide-by-zero or becomes `0%`, `ACCT-1006` is presented as current, or the file contains fewer records without an explained exception.

#### `output/exceptions.csv`

- **Expected structure:** Each unresolved or invalid condition should retain the source key or account ID, a reason, and enough original context to investigate. One row per record or one row per reason are both acceptable if the choice is documented.
- **Verify:** The exceptions must account for `UNKNOWN-77` as an unapproved usage key, `ACCT-1006` as a CRM account with no current usage row, and `ACCT-1005` as a zero-license record whose adoption is unavailable. Do not validate only by row count because one record may have multiple reasons.
- **Narrate:** Exceptions are a designed output, not debris. They preserve the human decisions that automation cannot make safely.
- **Red flags:** The file is empty, contains only `UNKNOWN-77`, omits source values, treats `UNKNOWN-77` as a guessed account, or fails to surface the zero-license and missing-current-usage conditions somewhere reviewable.

#### `output/weekly-account-health.md`

- **Expected structure:** A dated report should separate factual totals, rule-based account flags, unresolved exceptions, and recommended human review. Claims should be traceable to the CSV outputs and use `2026-10-09` as the report date.
- **Verify:** The report should distinguish six CRM accounts from six usage rows; five usage keys resolve and one does not. Under the stated rules, `ACCT-1004` is the only resolved account with no flag. `ACCT-1001` is within 37 days of renewal; `ACCT-1002` is below 40% adoption; `ACCT-1003` has no owner, `22.5%` adoption, 38-day-old activity, and renewal in 72 days; `ACCT-1005` has unavailable adoption, 55-day-old activity, and renewal in 22 days; and `ACCT-1006` has incomplete current reconciliation.
- **Narrate:** Separate facts from interpretations. Healthy usage does not erase a renewal flag, and polished prose must not turn an unresolved record into a conclusion.
- **Red flags:** The report uses the current date, calls all six accounts reconciled, says `ACCT-1005` has zero adoption, omits `ACCT-1006` or `UNKNOWN-77`, combines facts and recommendations without labels, or contains totals that cannot be reproduced from the outputs.

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

### Instructor review guide: automated tests

- **Expected structure:** A discoverable `unittest` module—typically under `tests/`—should exercise reconciliation and calculations with controlled fixtures or temporary files. Tests should call production logic rather than duplicate its implementation.
- **Verify:** At minimum, tests prove `CONTOSO-ENERGY` resolves to `ACCT-1002`, `UNKNOWN-77` remains unmatched, zero licensed users return unavailable adoption without raising an error, and a blank owner flags `ACCT-1003`. A normal standard-library run should end with at least `Ran 4 tests` and `OK`; additional focused tests are welcome.
- **Narrate:** These tests defend against believable wrong answers: a guessed join, a lost exception, a broken denominator, or a missing business-rule flag. The terminal result is evidence only when the tests target production behavior.
- **Red flags:** Tests only check that files exist, depend on previously generated output, alter the source CSVs, assert the same formula they reimplemented locally, swallow warnings, or pass while the workflow command fails.

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

### Instructor review guide: team handoff files

#### `RUNBOOK.md`

- **Expected structure:** Purpose, Python prerequisite, fixed input contracts, exact run and test commands, output descriptions, review steps, failure behavior, and known limitations should fit in a short operational document.
- **Verify:** A teammate can identify `2026-10-09` as the deterministic demo date, knows that exact IDs precede the alias map, can find all three outputs, and is told to review `UNKNOWN-77`, `ACCT-1006`, and the zero-license condition for `ACCT-1005`.
- **Narrate:** The runbook turns a one-time demo into an operable team capability. It should explain how to judge the result, not merely how to launch the script.
- **Red flags:** The documented commands do not match the files created, required columns or exception review are absent, the runbook promises automatic resolution of unknown accounts, or it omits the test command and failure expectations.

#### `prompts/build-weekly-report.prompt.md`

- **Expected structure:** A reusable Agent Mode prompt should instruct the agent to inspect first, preserve `data/`, enforce exact-ID-then-approved-alias matching, keep exceptions visible, run tests and the workflow, and summarize evidence before claiming success.
- **Verify:** The prompt names the input and output contracts, requires a supplied report date rather than today's date, asks for explicit validation, and preserves human review for unmatched, invalid, or incomplete records.
- **Narrate:** A reusable prompt carries forward guardrails and review habits, not this week's conclusions. Next week's numbers may change, but the safety contract should not.
- **Red flags:** The prompt embeds this week's calculated results as expected future values, authorizes inferred mappings, lets the agent overwrite source exports, omits test execution, or asks for a polished summary without requiring exception and source reconciliation.

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
