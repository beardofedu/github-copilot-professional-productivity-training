# Outfitter with Microsoft

## Training design

**Theme:** Build the Capability  
**Length:** 60 minutes  
**Format:** Live presentation, VS Code demonstration, and audience Q&A  
**Audience:** People who build dashboards, apps, automations, AI agents, and code  
**Primary tools:** VS Code and GitHub Copilot Agent Mode  
**Productivity focus:** Personal execution and small-team reuse  

## Outcome

By the end of the session, participants will be able to open a real work folder in VS Code, give Agent Mode a bounded outcome, collaborate with it through implementation and validation, and package the result so a teammate can understand and reuse it.

## Learning objectives

Participants will be able to:

1. Navigate the four VS Code surfaces used in the session: Explorer, Copilot Chat, Agent Mode, and the integrated terminal.
2. Use **Goal–Context–Constraints–Check** to frame an outcome rather than request isolated code.
3. Ask Agent Mode to inspect multiple source files, propose a plan, implement a workflow, run validation, and report what changed.
4. Separate deterministic automation from decisions that still require human judgment.
5. Verify reconciled data and generated reports with tests, exception outputs, and source-level spot checks.
6. Package a script, reusable prompt, runbook, and outputs for a small team.
7. Recognize when the Copilot app or CLI is a better entry point without fragmenting the core workflow across tools.

## Key message

> Outfitter builds capability: bring a real outcome into VS Code, let Agent Mode work across the project, and keep human judgment at every decision boundary.

The session assumes mixed experience. Some attendees already build sophisticated solutions in VS Code; others need a quick orientation. The demonstration should feel credible to experienced builders while making each interaction legible to newer users.

## 60-minute run of show

| Time | Segment | Purpose |
|---|---|---|
| 0:00–0:07 | VS Code trailhead | Open a folder and locate Explorer, Copilot Chat, Agent Mode, and the terminal. |
| 0:07–0:12 | Build the Capability | Frame personal and small-team productivity and set the Agent Mode mental model. |
| 0:12–0:20 | Frame the outcome | Teach Goal–Context–Constraints–Check using the recurring-report scenario. |
| 0:20–0:44 | Agent Mode demonstration | Inspect, reconcile, automate, test, and review a multi-source weekly report. |
| 0:44–0:51 | Package for the team | Create a runbook and reusable prompt; explain repo/shared-folder handoff. |
| 0:51–0:56 | Trust the evidence | Review exceptions, tests, source checks, safety, and policy. |
| 0:56–1:00 | Q&A and next build | Select one bounded capability to build in the next week. |

More than half of the instructional time is spent in VS Code. The Copilot app and CLI are covered as short decision points, not as separate demo stages.

## Productivity patterns

1. **Understand** — inspect unfamiliar data, scripts, project structure, or failures.
2. **Build** — create a dashboard component, app feature, automation, agent, or script.
3. **Transform** — clean, normalize, join, reconcile, and reshape data.
4. **Automate** — turn a recurring process into a repeatable, observable workflow.
5. **Review** — test assumptions, find edge cases, and improve maintainability.
6. **Share** — package the capability so a teammate can run, inspect, and adapt it.

## Tool selection

| Tool | Use it when… | Example |
|---|---|---|
| VS Code + Agent Mode | The work spans files, code, data, terminal commands, tests, and iterative edits. | Build and validate a recurring account-health report from three sources. |
| Copilot Chat in VS Code | You need an explanation, a design conversation, or a focused edit without autonomous project work. | Explain the reconciliation logic or compare two implementation approaches. |
| Copilot app | The task begins outside a project or needs broad planning across work. | Turn rough requirements into a project brief before opening VS Code. |
| Copilot CLI | The task is primarily command-oriented or begins in a terminal. | Investigate logs, inspect a directory, or explain a command sequence. |
| Repo or shared folder | The capability is ready for small-team review and reuse. | Share the script, prompt, runbook, tests, and generated outputs together. |

## Demonstration scenario

A small team manually produces a weekly account-health report from three exports:

- a CRM account list,
- product-usage data whose account keys do not always match the CRM,
- and the prior week's snapshot.

The workflow must:

1. reconcile account identifiers using an approved alias map,
2. preserve unmatched records in an exception file rather than silently dropping them,
3. calculate adoption and week-over-week change,
4. flag risks such as missing owners, low adoption, stale activity, and near-term renewals,
5. generate a concise Markdown report,
6. add automated tests for the highest-risk rules,
7. and package the capability with a runbook and reusable prompt.

This is deliberately more advanced than parsing one CSV. It demonstrates project-level reasoning, multi-file edits, terminal execution, testing, exception handling, and team reuse.

## Agent Mode interaction pattern

1. **Inspect:** Read the workspace and state what is known, ambiguous, and risky.
2. **Plan:** Propose files, logic, validation, and decision boundaries.
3. **Build:** Implement the smallest end-to-end version.
4. **Run:** Execute the workflow and inspect actual outputs.
5. **Review:** Critique assumptions, silent failure modes, and maintainability.
6. **Refine:** Apply only justified changes.
7. **Package:** Add a runbook and reusable prompt for the team.

## Assessment

- **Opening check:** Participants identify Explorer, Chat, Agent Mode, and the terminal.
- **Prompt check:** Participants name which part of Goal–Context–Constraints–Check is missing from a weak prompt.
- **Demo check:** Participants identify which reconciliation decisions must remain explicit and reviewable.
- **Exit commitment:** Participants name one capability they will build, the evidence they will require, and what they will share with their team.

## Delivery requirements

- Start from the included `demo-workspace/` folder.
- Use synthetic data only.
- Increase VS Code and terminal font sizes for the room.
- Keep Agent Mode confirmations visible; narrate why an action is safe before approving it.
- Do not allow the agent to overwrite source exports.
- Keep a completed backup branch or folder ready, but demonstrate from the starter workspace.
- If the live result differs, teach from the difference instead of hiding it.
- Keep Copilot app and CLI coverage to approximately three minutes total.

## Success measures

- Newer participants can follow the VS Code workflow without getting lost in the interface.
- Experienced participants see a credible multi-source automation rather than a toy example.
- Participants can describe Agent Mode as a project collaborator that still requires boundaries and evidence.
- Participants leave with a reusable method for personal work and small-team handoff.

