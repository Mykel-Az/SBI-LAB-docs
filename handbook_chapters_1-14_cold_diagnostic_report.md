# Cold Diagnostic Report — Handbook Chapters 1–14

**Date:** October 30, 2026  
**Mode:** Chapter-review cold diagnostic  
**Format:** Voice discussion  
**Diagnostic status:** Completed — 10 questions

## Scope

The diagnostic sampled foundational software-engineering ideas and their application to the Field Dispatch Assistant and prior RetailBox work. Questions covered definitions, why concepts exist, design choices, trade-offs, project responsibilities, contracts, and debugging.

The questions were intentionally mixed. They were not a chapter-by-chapter examination, so the results indicate areas to review rather than proving that an entire chapter has or has not been mastered.

## Overall assessment

You can often recognize the purpose of an engineering concept and connect it to a real project. Your strongest answers came when you described something you had actually built or could point to in your architecture.

The main weakness was precision: several answers began with a reasonable idea but did not clearly state the principle, explain the mechanism, or finish the trade-off. Under interview pressure, you sometimes circled around the point instead of giving a direct answer first.

## Diagnostic results

| # | Topic assessed | What your answer demonstrated | Assessment |
|---|---|---|---|
| 1 | Basic software concept / reusable implementation | You associated the idea with reusable functionality, but the definition was difficult to follow and the distinction between a function and calling a function was unclear. | **Weak recall and communication** |
| 2 | Separating domain logic from framework code | You explained that the dispatch logic lives in a pure Python package and that Django views/serializers call it, while the package does not depend on Django. | **Strong project application** |
| 3 | Invariants | You described invariants as rules that must not be broken and gave the example of a technician needing at least one skill. The explanation was broadly correct but could be more exact. | **Basic understanding; needs depth** |
| 4 | Enforcing a business rule across entry points | You proposed a shared skill-matching function and having the relevant parts of the system call it, rather than duplicating the check in views. | **Good application and consistency reasoning** |
| 5 | Trade-offs of extracting logic from Django | You identified that moving logic out of Django can mean giving up framework conveniences such as built-in facilities. The answer did not fully distinguish which conveniences are lost and which are retained. | **Partial trade-off understanding** |
| 6 | Trade-offs of enforcing invariants | You initially returned to the benefits of centralizing checks. You eventually identified that duplicated checks can drift when one endpoint is missed, but did not clearly state a direct cost of strict invariant enforcement. | **Trade-off gap** |
| 7 | Dispatch engine responsibility | You described the package as owning the dispatch domain logic and algorithm for deciding which technician is assigned to a job. | **Good project understanding** |
| 8 | RetailBox Paystack integration | You described a subscription system for merchants' customers, including recurring subscriptions and cancellation. You said the payment service was built with FastAPI and exposed endpoints called by the Django backend. Your explanation of the exact request, webhook, and state-update flow was not detailed enough to assess those mechanics. | **Useful project evidence; depth gap** |
| 9 | Function/interface changes and compatibility | You suggested isolating a changed behavior in a new function rather than unexpectedly changing a function used by other views. You did not explicitly cover defining and preserving a contract or how callers would be tested. | **Partial understanding; needs precision** |
| 10 | Debugging incorrect dispatch assignments | You proposed rolling back the faulty release, identifying and debugging the change, then adding an invariant or contract to catch similar errors. You did not mention a specific regression test or how you would verify the fix before redeployment. | **Sound incident instinct; operational depth to develop** |

## Strengths

- **Project application:** You gave a concrete explanation of the pure Python `dispatch_engine` boundary and its relationship with Django.
- **Centralizing business rules:** You understood why a rule should not be independently reimplemented in every view or endpoint.
- **Invariant recognition:** You can explain the idea in plain language and produce a relevant technician-skill example.
- **Incident response instinct:** You started with rollback, then investigation, correction, and a preventive guard.
- **Relevant experience:** You connected the Paystack discussion to a subscription capability you said you built, including a FastAPI service called by the Django backend.

## Weaknesses and feedback labels

- **R — Recall gap:** The opening definition was hesitant and unclear. You need to retrieve core definitions cleanly without building the answer while speaking.
- **C — Communication gap:** You often used several partial phrases before reaching the point. Lead with a one-sentence answer, then explain it.
- **D — Depth gap:** Your answers often identified *what* a component does but did not explain its guarantees, boundaries, failure behavior, or verification.
- **T — Trade-off gap:** You found it difficult to name a direct downside when asked for one. You sometimes repeated the benefit instead of stating the cost.
- **P — Project-evidence gap:** Your Field Dispatch Assistant explanation was specific. The Paystack explanation needs a more precise account of what the FastAPI service did, how Django called it, and what the webhook handled. Do not claim details you did not implement.
- **A — Application gap:** You have a reasonable design instinct, but need to make it concrete with interfaces, validation location, tests, and failure handling.
- **K — Knowledge gap:** No major factual misconception was conclusively demonstrated in this short sample. The diagnostic was not broad enough to rule out knowledge gaps across all 14 chapters.

## Questions that exposed the most difficulty

1. **Question 1:** Give a precise definition without conflating a function with a function call.
2. **Question 5:** State the actual cost of extracting logic from a framework, rather than only naming framework features.
3. **Question 6:** Give one direct downside of strict invariant enforcement.
4. **Question 9:** Explain how a caller-facing contract protects consumers when an implementation changes.
5. **Question 8:** Describe the actual Paystack integration flow precisely, separating the FastAPI service, Django caller, and provider webhook responsibilities.

## Chapter-group assessment

The diagnostic was not evenly distributed across all 14 chapters. It concentrated more heavily on separation of concerns, invariants, modularity, interfaces, and contracts, while some earlier foundations received limited direct testing.

Therefore, **there is not enough evidence to claim confidently that chapters 1–5 are your weakest group**. The clearest observed weakness is explaining foundational ideas precisely and articulating trade-offs. We should use the first review session to test the earlier foundations before finalizing the ranking.

## Proposed review sequence

1. **Session 1 — Chapters 1–5:** Rebuild the foundations and test recall, definitions, and the underlying problems each idea solves.
2. **Session 2 — Chapters 6–11:** Review the middle group, emphasizing how the concepts connect and where they appear in real backend systems.
3. **Session 3 — Chapters 12–14:** Review abstraction, modularity, and contracts, using the Field Dispatch Assistant and the Paystack integration where the user's actual implementation supports the discussion.

Each session should remain interactive: one question at a time, no lecture before your attempt, and a hint ladder unless you request a different format. We'll correct answers after you respond and finish with a session report.

## Recommended answer structure

For most conceptual interview questions, practice this sequence:

1. **Definition:** State what it is in one sentence.
2. **Problem:** Explain why it exists.
3. **Mechanism:** Explain how it works or where the rule is enforced.
4. **Example:** Connect it to a real system or project.
5. **Trade-off:** State what the design costs or makes harder.

For project questions, distinguish clearly between what you personally implemented, what the framework/provider handled, and what you would design differently today.

## Recommended next session

Begin with **Session 1 — Chapters 1–5**, as a diagnostic review rather than assuming those chapters are definitely the weakest. Use short spoken answers and press for precise definitions, concrete examples, and one explicit trade-off per relevant topic.
