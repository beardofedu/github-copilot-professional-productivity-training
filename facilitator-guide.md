# Facilitator Guide

## Before the session

- Open the Copilot app, VS Code, a terminal with Copilot CLI available, and the demonstration repository on GitHub.com.
- Place the synthetic `weekly-status.csv` and `weekly-notes.txt` files in the demo workspace.
- Test the full demonstration once from a clean starting point.
- Keep the final script and expected outputs available as backups.
- Prepare the opening poll and a visible timer.

## 0:00–0:05 — From installation to intention

**Say:** “Installing Copilot gives you access to a capability, but it does not give you a workflow. Today is about closing that gap.”

Ask for a show of hands or poll:

- I was not sure what to ask.
- I tried it, but the answer was too generic.
- I did not know which Copilot experience to use.
- I was unsure whether I could trust the result.
- I have already found a repeatable use case.

Frame the audience:

- Their existing skills and professional judgment are the starting point.
- Professional developers may use Copilot differently, but software development is not the target of this session.
- The aim is to reduce friction in everyday knowledge work and scripting.

## 0:05–0:12 — Where Copilot fits

Introduce the five patterns: **Understand, Draft, Transform, Automate, Review**.

Use quick examples:

- “Explain this PowerShell script in plain language.”
- “Draft a checklist from these policy notes.”
- “Turn these meeting notes into decisions and action items.”
- “Help me automate this repeated file-processing task.”
- “Review this result for missing assumptions and edge cases.”

Then introduce the surface rule:

> Start where the work and its context already live.

Do not present the surfaces as a maturity ladder. They are different workspaces for different contexts.

## 0:12–0:20 — Goal–Context–Constraints–Check

### Weak prompt

> Make me a script for this report.

Ask the audience what Copilot would have to guess.

### Improved prompt

> **Goal:** Create a PowerShell script that reads `weekly-status.csv`, finds rows with a missing owner or due date, and writes a Markdown summary.  
> **Context:** The file has the columns `Item`, `Owner`, `DueDate`, and `Status`. This runs manually on Windows once a week.  
> **Constraints:** Do not modify the source CSV. Use only built-in PowerShell features. Explain the script before showing it.  
> **Check:** Include a dry-run example and three test cases, including an empty file.

Explain:

- **Goal:** What outcome do you need?
- **Context:** What does Copilot need to know that it cannot safely assume?
- **Constraints:** What must it use, avoid, preserve, or limit?
- **Check:** How will you determine whether the result is correct?

Emphasize that a prompt is not a one-time incantation. Good use is a conversation:

1. Ask for a plan.
2. Inspect assumptions.
3. Request a small first version.
4. Test it.
5. Bring errors or observations back.
6. Ask for refinement.

## 0:20–0:36 — Demonstration

Follow `demo-script.md`. Keep the demonstration moving even if Copilot produces different wording. The teaching target is the interaction pattern, not a predetermined answer.

Narrate these transitions:

- Copilot app: “I am shaping the task before touching files.”
- CLI: “I am working where the files and commands already are.”
- VS Code: “Now the artifact itself needs focused editing and testing.”
- GitHub.com: “The result becomes shared, reviewable work.”

Pause after the first generated script and ask: “What would you verify before running this?”

## 0:36–0:45 — More workday use cases

Present one example per productivity pattern. Encourage participants to translate the example into their own role.

### Understand

> Explain this error message for a non-developer. List the three most likely causes, what evidence would distinguish them, and the safest first check.

### Draft

> Turn these rough notes into a concise operating procedure. Preserve every requirement, flag ambiguities, and add a verification checklist.

### Transform

> Convert this unstructured list into a table with owner, due date, dependency, and status. Do not invent missing values; mark them as `Needs input`.

### Automate

> Before writing code, identify which steps in this weekly process are deterministic enough to automate and which still require human judgment.

### Review

> Review this plan as a skeptical colleague. Find missing assumptions, unclear ownership, failure modes, and claims that need a source.

## 0:45–0:51 — Trust and responsible use

Use the phrase:

> Copilot can accelerate production, but it does not transfer accountability.

Cover four checks:

1. **Accuracy:** Does the result match the source data and task?
2. **Safety:** Could the command modify, delete, disclose, or overwrite something?
3. **Policy:** Is the information appropriate to provide under organizational rules?
4. **Fitness:** Does the result work in the real environment, not only in the example?

For commands and scripts:

- Ask for an explanation.
- Prefer a dry run or read-only first step.
- Test on synthetic or copied data.
- Review file paths and destructive operations.
- Keep a rollback or backup when the task changes data.

For factual summaries:

- Ask Copilot to distinguish facts, inferences, and unanswered questions.
- Open and verify cited sources.
- Do not treat confident language as evidence.

## 0:51–1:00 — Q&A and next action

When answering, map questions back to:

- the productivity pattern,
- the best surface,
- the needed context,
- and the verification method.

Close with a one-week experiment:

> Choose a task you already understand, that takes 15–60 minutes, happens more than once, and has a result you can verify.

Ask participants to record:

- My task:
- My Copilot surface:
- Context I will provide:
- Constraint I will set:
- How I will check the result:

## Facilitation guardrails

- If a demonstration fails, show the error and model how to give it back to Copilot with context.
- Do not imply that every workflow should be automated.
- Do not use “AI magic” language; connect outcomes to the quality of context, iteration, and review.
- Do not let syntax dominate. Explain what the script accomplishes and how the participant verifies it.
- Do not compare participants to professional developers. Reinforce the value of their existing domain knowledge.

