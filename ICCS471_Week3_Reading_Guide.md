# Week 3 reading: context and supervised changes

**ICCS471 · Support reading · About 8–10 minutes**

No separate written submission is required. Read this when you need help interpreting the workflow in IA 3.1 or IA 3.2.

## 1. A repository contains relationships

A repository map helps you find the parts that matter to a change. Knowing that `rules.py` exists is only a start. Ask which functions call its rules, what inputs they pass, and which tests describe the current behaviour.

A caller is a function that uses another function. A repository fact should include evidence and a consequence. For example, in a reading-list app: “`load_items` reads from `items.json`, so adding search should not silently change the storage format.” The file/function reference and the relevant code must actually support the claim.

For the booking task, inspect the implementation, its imports and relevant tests. Distinguish a comment describing intended behaviour from code implementing that behaviour. A type annotation alone does not enforce runtime input validation.

## 2. Context is what you make available to this request

The agent needs the current task, relevant code, existing behaviour and constraints. Select files because they help answer a question: where data lives, how an operation behaves, which callers must keep working, or how a claim can be checked.

Make clear which files you attach or ask the agent to read. If its answer refers to a function, confirm the reference. An open editor window or a confident summary does not establish that every relevant file was inspected.

In a small repository, reading all implementation files is reasonable. In a larger one, begin with the entry point and follow the relevant calls. Add context as questions arise. Avoid substituting a large dump of unrelated files for a clear task.

## 3. Project instructions should guide decisions

`AGENTS.md` is a conventional file for project guidance. It can state conventions, boundaries and useful check commands. Automatic discovery varies by agent and settings. For this assignment, attach or paste it into the request if you cannot establish that it was loaded.

Keep reusable guidance separate from the current task. For example, “Preserve public interfaces” may belong in project guidance. “Implement the new search operation” belongs in the current request. Point to the agreed specification for detailed feature rules.

Instructions do not guarantee compliance or disable tool capabilities. You still review proposed actions and resulting changes. Confirm which checks are useful and whether a command is within the task before allowing it.

For the built-in Copilot workflow, Ask explains, Plan researches before implementation, and Agent implements using available tools. Review the plan before using Start Implementation. Custom agents/tools can differ.

## 4. A checkpoint makes comparison possible

Before editing, keep the starter and record a Git baseline. Run the known creation tests. Their passing result establishes a starting observation about those cases; it does not show that the new function works.

A stub is an unfinished function body. In this starter, calling the move stub raises `NotImplementedError`. The expected smoke-test errors should disappear as the feature is implemented correctly. An import error or a failing creation baseline has a different cause.

Keep an untouched extracted copy as well. It supports file comparison and recovery if Git setup is blocked. See the repository README for commands and practical steps.

## 5. The diff shows the actual change

Read a summary to orient yourself, then inspect the changed lines. Ask:

- Does the change implement the requested behaviour?
- What existing caller or behaviour could it affect?
- Did the agent change tests, data structures or files beyond the agreed scope?

`git diff HEAD` compares tracked working changes with the current commit, including staged changes. New untracked files need separate inspection. If implementation is already committed, compare with your recorded baseline commit. The README includes a file-comparison fallback.

A two-line shared-rule edit can have a wide effect. In the lecture example, replacing strict overlap comparisons with inclusive comparisons rejects valid back-to-back bookings. The change looks small, but it alters what existing callers receive.

## 6. Supervision can retain a sound decision

A useful intervention identifies the mismatch, the reason and the next step. “Restore strict comparisons because the specification allows adjacency; show the repair and rerun the existing case” is reviewable.

Sometimes the change is sound. Explain the code reference and the consequence you checked, then retain it. The assignment does not require you to manufacture an error. It asks you to show a decision you can defend.

For IA 3.2, record one decision with a code reference in REVIEW.md. No transcript is required.

## 7. Expected outcomes precede generated tests

Before asking AI to write a test, specify its starting records, requested action and expected result yourself. Read the resulting assertions. Does the test examine the property you intended, or merely run the function?

For example, “search returns the matching entry and leaves the stored list unchanged” contains two claims. A test asserting only the returned match establishes only one of them.

After repairs, run both relevant new checks and the existing baseline. Report actual results. When execution is blocked, report the error and limit your claim to what source inspection supports.

## 8. Keep the decision proportional to the evidence

An implemented feature can be ready for further review while still needing stronger checks. Identify one specific requirement to investigate next. Week 4 develops this evidence work.

Business suitability also matters. A prototype can satisfy its technical rules while leaving customer approval or staff workflow questions unresolved. Record such a question without silently adding an approval system to this task.

## Optional official references

These are reference lookups, not additional assignments. Product interfaces may change; the course workflow relies on observable actions and file evidence.

- [VS Code: custom instructions](https://code.visualstudio.com/docs/agent-customization/custom-instructions) — look up project instruction files and loading behaviour for your setup.
- [Git: diff](https://git-scm.com/docs/git-diff) — compare versions and understand `HEAD` comparisons.
- [Git: status](https://git-scm.com/docs/git-status) — identify tracked changes and new files.
- [Python 3.12: unittest](https://docs.python.org/3.12/library/unittest.html) — running test modules and reading results.

Reference pages checked during preparation on 25 September 2026.

- [VS Code: planning](https://code.visualstudio.com/docs/agents/run/planning) — planning and implementation handoff (checked 1 October 2026).
