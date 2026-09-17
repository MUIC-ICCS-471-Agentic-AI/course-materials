# From Request to Evidence

**ICCS471 — Weeks 1–2 reading**  
**Expected time: 12–15 minutes**

Agentic tools can move quickly from a sentence to working code. That speed is useful, but it creates a problem: a short request can hide many decisions. If those decisions remain unstated, the agent may make them for you.

This course therefore begins before the code. You will learn to turn a request into bounded work, supervise what happens, and decide whether the evidence is strong enough to accept the result.

## A request is not yet a specification

Consider this request:

> Prevent booking conflicts.

It sounds clear until you try to implement it.

- What counts as a conflict?
- Can one booking begin at the exact time another ends?
- Are conflicts checked for a room, a person, or both?
- What happens to cancelled bookings?
- Are all times in the same time zone?
- Should the system reject the request, suggest another time, or modify an existing booking?

An agent can fill these gaps and produce code. That does not mean it filled them correctly.

Before implementation, separate the task into several kinds of information.

| Term | Meaning | Booking example |
|---|---|---|
| **Request** | The initial expression of need; it may be incomplete. | Prevent booking conflicts. |
| **Requirement** | Behaviour the software must provide. | Reject a new booking that overlaps an active booking for the same room. |
| **Constraint** | A boundary the solution must respect. | Do not change the database schema. |
| **Exclusion** | Work deliberately outside the task. | Do not add automatic rescheduling. |
| **Acceptance criterion** | An observable condition used to judge the result. | A booking from 10:30–11:30 is rejected when 10:00–11:00 already exists. |
| **Assumption** | Something treated as true but not yet confirmed. | All stored times use the same time zone. |
| **Uncertainty** | A question that remains unresolved. | Whether cancelled bookings should block the time slot. |

These categories do not exist to make the task longer. They prevent hidden decisions from becoming hidden defects.

## Bound the work before asking for code

A useful task description tells the agent what success means and what it must not disturb. For the booking request, an initial version might be:

### Required behaviour

- Reject overlapping bookings for the same room.
- Allow adjacent bookings: a booking ending at 11:00 does not conflict with one starting at 11:00.
- Return a clear conflict message.
- Preserve existing behaviour outside booking creation.

### Constraints and exclusions

- Use the existing data model.
- Do not modify existing bookings.
- Do not add automatic rescheduling.

### Questions or assumptions

- Confirm how cancelled bookings are treated.
- Confirm the time-zone policy.

This is still not a perfect specification. It is much safer than the original sentence because the important boundaries are visible and reviewable.

## Acceptance criteria make success observable

Requirements describe expected behaviour. Acceptance criteria turn that behaviour into examples or conditions that can be checked.

For example:

1. If Room A already has a booking from 10:00 to 11:00, a new Room A booking from 10:30 to 11:30 is rejected.
2. A new Room A booking from 11:00 to 12:00 is accepted.
3. A booking for Room B at the same time is not rejected because of the Room A booking.
4. Rejection returns the expected status and a useful conflict message.
5. Existing bookings remain unchanged.

Notice the second criterion. It is a boundary case: the two bookings touch but do not overlap. Boundary cases often expose mistakes that ordinary examples miss.

You should also look for counterexamples—cases that challenge the proposed rule. If the agent uses `new_start <= existing_end`, it may reject the adjacent 11:00 booking even though adjacency should be allowed. A generated test suite may miss this if the agent made the same mistaken assumption in both the code and the tests.

## A plan is something to review

When an agent proposes a plan, do not treat the plan as permission to proceed. Read it as an engineering proposal.

Check for:

- **Omissions:** Is a requirement, constraint, or boundary case missing?
- **Unsupported assumptions:** Has the agent decided something that the task did not establish?
- **Unnecessary complexity:** Is it proposing a larger design than the task requires?
- **Specification drift:** Has the plan quietly changed the problem?
- **Weak verification:** Will the proposed checks actually test the important behaviour?

A good plan is not necessarily the longest plan. It is a plan whose scope, decisions, risks, and checks you can understand and defend.

## Verification, validation, and judgment are related—not interchangeable

These words serve different purposes.

### Verification

Verification asks whether the implemented product conforms to its engineering specification: the stated requirements, constraints, and acceptance criteria.

> Did we build it correctly according to what we specified?

For the booking task, verification includes checking overlap behaviour, adjacency, room independence, error responses, regression risks, and the actual code changes.

### Validation

Validation asks whether the product, as used in its intended context, serves the stakeholder's actual need and purpose. It can also reveal that the written requirement captured the wrong problem.

> Did we build the right thing for the actual problem?

Suppose the implementation correctly prevents room conflicts, but the real problem was double-booking a lecturer across different rooms. The software may be verified against its specification and still fail validation against the user's need.

The **question and reference point** determine which activity you are doing, not whether a human or an automated test performs the check. Running a booking demo to check its stated overlap rule contributes to verification. Trying a representative booking workflow and assessing whether it solves the users' actual scheduling problem can contribute to validation. Both require evidence; neither is a guess based on a passing test message.

### Engineering judgment

Engineering judgment is the human decision made using evidence, context, uncertainty, constraints, and risk.

It includes deciding whether to:

- accept the work
- reject or correct it
- ask for stronger evidence
- reduce or revise the scope
- escalate an unresolved issue
- stop the agent before it causes unnecessary change

Judgment is not another word for verification or validation, and it is not a third type of test. It is what you use to decide what evidence is needed and what action is justified by that evidence.

## Claims are not evidence

An agent may report:

> Implemented booking-conflict prevention. All tests pass.

This is a claim. It may be true, but the summary alone does not establish it.

Useful evidence could include:

- the actual diff and the files changed
- relevant existing and new tests
- test output that you ran or observed
- manual checks of important boundary cases
- static analysis, linting, or type checks where relevant
- confirmation that unrelated behaviour was not changed
- an explanation of remaining assumptions and limitations

Even passing tests have limits. Tests establish only the behaviours they exercise, under the assumptions encoded in them. If the implementation and its generated tests share the same misunderstanding, both can agree and both can be wrong.

This is why sufficiently independent verification matters. Independence does not always require a different person or tool. It can come from using a separately derived acceptance criterion, constructing a counterexample, inspecting the diff, or checking the result from a different direction.

## What “Done” means in this course

“The agent finished” is not the same as “the work is Done.”

For a bounded task, engineering completion normally means that:

- the accepted requirements and scope are satisfied
- important constraints and exclusions were respected
- the changes are understood and appropriately limited
- relevant checks pass
- important boundary cases and counterexamples were considered
- the evidence is strong enough for the risk involved
- known limitations and unresolved uncertainty are stated honestly

Verification does not provide absolute proof that software contains no defects. It supports a defensible decision within a defined scope.

## The working habit

When using an agent, keep returning to five questions:

1. **What exactly are we trying to achieve?**
2. **What is in scope, out of scope, assumed, or uncertain?**
3. **What did the agent actually change?**
4. **What evidence supports its claims?**
5. **Can I justify accepting this result?**

That is the foundation of the course workflow:

> **Build it. Verify it. Justify it.**

The tool may generate much of the work. Responsibility for the accepted result remains human.

## Check your understanding

Before Week 2, make sure you can explain:

- one difference between a request and a requirement
- one useful constraint and one acceptance criterion for the booking task
- why the adjacency case matters
- the difference between verification and validation
- why engineering judgment cannot be delegated entirely to the agent
- why “all tests pass” may still be insufficient evidence

You do not need to submit written answers unless instructed.

## References

- MIT Missing Semester. (2026). [Agentic Coding](https://missing.csail.mit.edu/2026/agentic-coding/).
- GitHub. [Asking GitHub Copilot questions in your IDE](https://docs.github.com/en/copilot/how-tos/chat-with-copilot/chat-in-ide).
- IEEE Computer Society. [Guide to the Software Engineering Body of Knowledge resources](https://www.computer.org/education/bodies-of-knowledge/software-engineering/resources/).
