# Karpathy Rules — Software Engineering & AI-Assisted Coding

> Adapted from Andrej Karpathy's principles on LLM-assisted engineering.
> Applied to: Lab Activity 3 — Real-Time Software Engineering & Testing (Ch. 21)

---

## Core Principles

### 1. Read the Code, Don't Trust the Summary
- Always read the actual implementation — never assume what the AI generated is correct.
- Diffs are your ground truth. Summaries can lie. Code cannot.

### 2. Prompt → Review → Iterate (PRI Loop)
- Never accept first-pass AI output as production-ready.
- Treat every AI-generated test case or test script as a *draft*.
- Review manually, run it, fail it intentionally, then iterate.

### 3. Use AI as a Pair Programmer, Not an Oracle
- AI is a high-speed autocomplete with reasoning. Not infallible.
- You own the logic. AI suggests. You decide.
- Ask AI to explain its reasoning — if it can't, that's a red flag.

### 4. Small Context Windows = Sharp Focus
- Break problems into atomic tasks.
- For test case generation: one feature = one focused AI prompt.
- Avoid "generate all tests for the whole system" prompts.

### 5. Test the Tests
- A test suite is only as good as its failure mode.
- Force failures deliberately to confirm test logic is correct.
- Boundary conditions and negative paths matter more than happy paths.

### 6. Version Everything
- Every AI-assisted workflow must be tracked (git or equivalent).
- Log prompts that generated significant outputs.
- Treat AI sessions as audit trails, not magic.

### 7. Know When to Stop Using AI
- Complex business logic, legal/regulatory constraints, security-critical paths → human-only review.
- Real-time systems (Ch. 21): timing constraints, interrupt handling, and safety properties must be verified by domain experts, not AI alone.

---

## Applied to Real-Time Software Engineering (Ch. 21)

| Karpathy Rule | Ch. 21 Application |
|---|---|
| Read the code | Review generated real-time task schedulers manually |
| PRI Loop | Test → observe timing → adjust deadlines iteratively |
| Pair programmer | AI suggests interrupt handlers; you validate timing constraints |
| Small context | One real-time task per test session |
| Test the tests | Inject timing violations to verify watchdog behavior |
| Version everything | Tag every timing model change in version control |

---

## Vibe-Coding Standard (applied here)

- Code with energy and flow — but never skip the review gate.
- If it *feels* right but you can't *explain* it → stop. Understand first.
- Red-team your own prompts: "What's the worst thing this could generate?"

---

*Last updated: 2026-06-12 | Lab Activity 3 — SE Testing Exercise*
