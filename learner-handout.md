# Outfitter with Microsoft

## Build the Capability

Use GitHub Copilot in VS Code to turn a bounded work outcome into a workflow that can be run, checked, and shared.

## VS Code trailhead

- **Explorer:** project files and context
- **Copilot Chat:** intent, questions, and feedback
- **Agent Mode:** multi-step work across files and tools
- **Terminal:** commands, execution, and tests

Use the Copilot app for broad planning outside a project. Use Copilot CLI when the terminal is the main workspace.

## Goal–Context–Constraints–Check

```text
Goal:
What useful capability or outcome do I need?

Context:
What sources, environment, audience, and workflow must Copilot understand?

Constraints:
What must remain unchanged? What rules and tools must it follow?

Check:
What outputs, exceptions, tests, and source checks will prove the result?
```

## Agent Mode workflow

1. **Inspect** the workspace without changing it.
2. **Plan** the files, logic, evidence, and decision boundaries.
3. **Build** the smallest complete version.
4. **Run** the workflow and inspect actual outputs.
5. **Review** assumptions and silent failure modes.
6. **Refine** only justified changes.
7. **Package** the prompt, runbook, tests, and outputs for the team.

## Strong example

```text
Goal: Build a repeatable account-health report from CRM, usage, and
prior-week exports.

Context: Usage keys do not always match CRM account IDs. Use the included
approved alias map. A five-person team reviews the report every Friday.

Constraints: Never modify source files. Never guess an unmatched account.
Use standard Python only. Keep reconciliation rules explicit.

Check: Preserve exceptions, add tests for risky rules, run the workflow,
and trace report claims back to source data.
```

## Verification checklist

- **Accuracy:** Are joins, calculations, and report claims supported by source records?
- **Safety:** Are source files immutable and outputs written separately?
- **Policy:** Is the information appropriate for Copilot and the storage location?
- **Fitness:** Do tests and representative inputs cover real conditions?
- **Transparency:** Are unmatched and ambiguous records visible?
- **Reuse:** Can a teammate run the workflow from the documentation?

## My next capability

**Capability I want to build:**  

**Folder or project it belongs in:**  

**Context Agent Mode needs:**  

**Decisions that remain mine:**  

**Evidence I require:**  

**What I will share with my team:**  

