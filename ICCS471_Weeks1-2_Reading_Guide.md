# ICCS471 Weeks 1–2 Reading Guide

## Why these readings?

The first two weeks establish the working language of the course. The aim is not to learn every Copilot feature or read a large body of AI theory. You need enough background to understand what a coding agent can do, use the supported environment safely, and turn a request into work that can be checked.

Complete Assignment 1 (your no-AI time capsule) **before** reading these materials, so it records your starting ideas. Complete all three readings before the Week 2 class.

**Expected total time: approximately 35–45 minutes.**

## 1. MIT Missing Semester: Agentic Coding

**Time: 15–20 minutes**  
**Link:** https://missing.csail.mit.edu/2026/agentic-coding/

Read these parts:

- the opening and demonstration
- **How AI Models and Agents Work**
- **Use Cases**
- **What to Watch Out For**

Read the article text; the embedded lecture video is optional and is **not** included in the time estimate.

For now, you may skip the more advanced material on parallel agents, subagents, MCP, reusable skills, and advanced configuration. We will return to relevant ideas when the course needs them.

While reading, focus on these questions:

- What makes an agent different from an ordinary chat interface?
- What can the agent see, change, or execute?
- Why does additional capability also require stronger supervision?

## 2. GitHub: Asking GitHub Copilot questions in your IDE

**Time: 8–10 minutes**  
**Link:** https://docs.github.com/en/copilot/how-tos/chat-with-copilot/chat-in-ide

Read only what you need for our initial workflow:

- prerequisites
- **Ask mode**
- **Plan mode**
- **Agent mode**
- submitting a prompt
- reviewing the response and continuing the conversation

Focus on the **VS Code** instructions. You do not need the instructions for other IDEs.

You do not need the sections on subagents, MCP, custom agents, skills, model selection, or cloud coding agents yet.

The important distinction is:

| Mode | Initial use in this course |
|---|---|
| **Ask** | Understand the repository, code, or problem without asking for changes. |
| **Plan** | Investigate the task and propose a plan for you to review before editing. |
| **Agent** | Make bounded changes, propose or run commands, and iterate on results. |

Do not treat Agent mode as an automatic choice. Choose the mode that matches what you are trying to do.

## 3. Instructor reading: From Request to Evidence

**Time: 12–15 minutes**  
**Reading:** [From Request to Evidence](./ICCS471_Reading_From_Request_to_Evidence.md) (also posted with this guide; if the relative link does not open in Google Classroom, open that file directly).

This reading connects Week 1 to Week 2. It introduces:

- requests, requirements, constraints, exclusions, and assumptions
- acceptance criteria and counterexamples
- verification against the specification, validation against the real user need, and the engineering judgment that uses both kinds of evidence
- the difference between a claim and sufficient evidence

The booking-conflict example in the reading continues the example used in class.
Some examples discuss a larger hypothetical booking product (such as a database or cancellations). They are questions for reasoning, **not extra features to add to the Assignment 3 starter repository**.

## After the readings

You should be ready to answer these questions in your own words:

1. What makes a coding agent different from ordinary AI chat?
2. When would you choose Ask, Plan, or Agent mode?
3. How can a vague request become a bounded and verifiable task?
4. How are verification, validation, and engineering judgment different?
5. Why do passing tests not always establish that the work is Done?

You do not need to submit written answers unless instructed. Come prepared to use these ideas in the Week 2 exercises.
