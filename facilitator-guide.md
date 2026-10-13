# Facilitator Guide: Outfitter with Microsoft

## Before the session

- Open the repository's `demo-workspace/` folder in VS Code.
- Confirm GitHub Copilot is signed in and Agent Mode is available.
- Open Explorer, Copilot Chat, and the integrated terminal.
- Keep source control visible but start with no generated script or outputs.
- Test the demo from a clean copy and keep completed outputs available as backup.
- Increase editor, Chat, and terminal font sizes.
- Use synthetic data only.
- Check the four events in the closing segment are still upcoming and that registration links work; update the slide and handout if a date has passed.

## 0:00–0:07 — VS Code trailhead

**Say:** “Outfitter is about building capability. Today, our workshop is VS Code, and Agent Mode is our project collaborator.”

Show only the surfaces participants need:

1. **Explorer:** the project folder and source files.
2. **Copilot Chat:** where intent and feedback are communicated.
3. **Agent Mode:** where Copilot can inspect files, edit the project, and use tools.
4. **Integrated terminal:** where commands, scripts, and tests run.

Clarify the modes:

- **Ask/Chat:** explanation and focused conversation.
- **Edit:** targeted changes you direct.
- **Agent:** a bounded outcome that may require multiple files, commands, and iteration.

Tell newer participants they do not need to memorize shortcuts. Tell experienced participants the value of the demo is the project-level interaction and review pattern, not basic VS Code navigation.

Opening poll:

- I build in VS Code most weeks.
- I use Copilot Chat but rarely use Agent Mode.
- I use Agent Mode for multi-file work.
- I am new to VS Code.

## 0:07–0:12 — Build the Capability

Frame the persona:

> Outfitter builds dashboards, apps, automation, AI agents, and code. The objective is not more generated text; it is a useful capability that can be run, checked, and shared.

Personal productivity means reducing the friction in a task you own. Small-team productivity means leaving behind enough context, tests, and instructions for someone else to reuse the work.

Briefly position the other tools:

- Use the **Copilot app** when the work begins as broad planning outside a project.
- Use **Copilot CLI** when the task is predominantly terminal-first.
- Stay in **VS Code** when the work spans files, code, outputs, and validation.

Do not open separate demos for the app or CLI.

## 0:12–0:20 — Goal–Context–Constraints–Check

### Weak request

> Build the weekly report.

Ask what the agent would have to guess: sources, joining rules, risk definitions, output format, safety boundaries, and evidence.

### Stronger request

> **Goal:** Build a repeatable account-health report from the CRM, usage, and prior-week exports.  
> **Context:** Usage keys do not always match CRM account IDs. An approved alias map is included. The report is reviewed by a five-person team every Friday.  
> **Constraints:** Never modify source files. Never guess an unmatched account. Use standard Python only. Keep reconciliation rules explicit and readable.  
> **Check:** Create exception output, add tests for risky rules, run the workflow, and summarize the evidence before calling it complete.

Explain that the **Check** turns a request into an accountable workflow.

## 0:20–0:44 — Agent Mode demonstration

Follow the [polished demonstration script](demo-script.html). The Markdown source remains available in `demo-script.md`.

Narrate the interaction pattern:

- “First, I want the agent to inspect—not implement.”
- “I am reviewing its assumptions before authorizing edits.”
- “The exception file is a feature: uncertainty must remain visible.”
- “Now the agent is running the work, not merely displaying code.”
- “Tests and output inspection are the evidence.”

Ask the audience at three points:

1. After the plan: “What decision is still underspecified?”
2. Before running: “What could silently make this report wrong?”
3. After output: “Which result would you spot-check against the sources?”

If Agent Mode asks to run a command, read it aloud and explain its impact before approving it.

## 0:44–0:51 — Package for a small team

Ask Agent Mode to add:

- `RUNBOOK.md` with prerequisites, commands, inputs, outputs, and known limitations,
- `prompts/build-weekly-report.prompt.md` with the reusable task prompt,
- tests beside the implementation,
- and a concise handoff summary.

**Say:** “The deliverable is not only the script. The capability is the script plus the prompt, evidence, instructions, and visible exceptions.”

Show how a teammate can:

1. inspect the runbook,
2. replace the dated exports,
3. run the command,
4. review exceptions,
5. and verify the Markdown report.

This replaces the former GitHub issue step.

## 0:51–0:55 — Trust the evidence

Use four checks:

1. **Accuracy:** Do joins, calculations, and report claims match the sources?
2. **Safety:** Are source files immutable? Are outputs written to a separate folder?
3. **Policy:** Is the data appropriate for Copilot and the chosen storage location?
4. **Fitness:** Do tests and representative inputs cover real conditions?

Highlight the most important failure mode: a polished report built from silently dropped or incorrectly matched records.

## 0:55–0:58 — Keep building

Close the capability loop before Q&A. Every option here is remote-accessible, so nobody needs to travel.

| Event | When | Why it fits | Link |
|---|---|---|---|
| GitHub Universe 2026 | October 28–29, 2026 | Free virtual pass. Keynotes and sessions on Copilot, Agent Mode, and agentic workflows, available on demand afterward. | <https://githubuniverse.com> |
| Microsoft Ignite 2026 | November 17–20, 2026 | Free digital pass. Copilot, agents, and the broader Microsoft tooling these capabilities connect to. | <https://ignite.microsoft.com> |
| Microsoft Reactor — GitHub Copilot series | Recurring live sessions | Short, free, hands-on classes on Copilot Chat, Agent Mode, and MCP in VS Code. | <https://developer.microsoft.com/reactor> |
| GitHub events and webinars | Ongoing | Upcoming webinars plus on-demand recordings. | <https://github.com/resources/events> |

Say it this way:

> Pick one of these and pair it with the capability you are about to write down. Register before you leave the room — a session you attend with a specific build in mind is worth far more than one you attend out of general interest.

Confirm dates and registration links the week you deliver; schedules change. If a date has passed, point to the on-demand recordings instead.

## 0:58–1:00 — Q&A and next build

Ask participants to choose a task with:

- more than one meaningful step,
- a recurring or reusable outcome,
- bounded inputs,
- a clear verification method,
- and low enough risk for a first experiment.

Have them record:

- Capability I want to build:
- Folder or project it belongs in:
- Context Agent Mode needs:
- Decisions that remain mine:
- Evidence I require:
- What I will share with my team:

## Facilitation guardrails

- Do not turn the orientation into a product tour.
- Do not let Agent Mode begin implementation before the plan and assumptions are reviewed.
- Do not imply every ambiguity should be automated; preserve human decision points.
- Do not hide agent errors. Use the exact error as new context.
- Do not equate a successful command with a correct business outcome.
- Do not share sensitive organizational data in the demonstration.
- Keep the focus on a durable workflow, not on writing Python syntax.
