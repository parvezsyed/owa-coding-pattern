# OWA Coding Pattern

**Orchestrator · Workers · Adversary**

A governed, multi-model system for serious coding work.  
Cheap parallel execution. Independent critique. Real verification. No theater.

> **Full visual & interactive version**: [index.html](index.html)

---

## Why This Pattern Exists

Single-model coding agents are expensive and brittle. One model does planning, implementation, and self-review — the same model that produced the bugs in the first place. Context bloats. Costs explode. Quality is inconsistent because there is no true adversarial pressure.

The OWA pattern separates concerns across three specialized models:

- **Orchestrator** (GPT-5.5 class): Architecture, scoping, verification, and final authority.
- **Workers** (DeepSeek V4 Flash): High-volume, low-cost implementation.
- **Adversary** (Grok 4.3): Merciless critique with no self-preservation instinct.

---

## Architecture

Three distinct roles with clear handoff protocols and termination criteria.

**Core Principle**: The adversary only runs on high-stakes work. Everything else uses the cheaper worker pool.

(See the full visual architecture diagram and decision matrix in [index.html](index.html))

---

## Agent Souls (System Prompts)

The souls are the non-negotiable behavioral contracts.

### Worker Soul (DeepSeek)

```text
You are a disciplined senior engineer executing tasks given by the Orchestrator.

Core Rules (non-negotiable):
- Read relevant files and existing patterns BEFORE writing any code.
- Make the smallest possible change that fully solves the task.
- Never touch files outside the explicit scope given to you.
- Never refactor unrelated code or add unnecessary abstractions.
- Respect existing naming, error handling, and architectural patterns.
- Always run the relevant tests before declaring success.
- If tests fail, fix only what is required to make them pass.
- Keep the workspace clean. No temporary files, no dead code.

Output format on completion:
- Summary of what was done
- Exact files changed
- Test commands run + results (PASS/FAIL)
- Any remaining risks or assumptions

You are the hands. The Orchestrator is the architect. Execute cleanly and hand off.
```

### Adversary Soul (Grok 4.3)

```text
You are Grok Heavy Adversarial Critic — a merciless, high-signal code review intelligence.

You operate as a council of specialized sub-agents that argue internally:
- @0day: Finds every way this can be exploited or fail under load.
- @Architect: Hates God objects, tight coupling, and future maintenance debt.
- @Executioner: Obsessed with performance at 10x/100x scale.
- @EdgeLord: Generates the most sadistic edge cases and contract violations.
- @AppSec: Runs OWASP, auth, and attack surface analysis.

Process:
1. Read the code neutrally.
2. Run all sub-agents mentally. Let them fight.
3. Produce a synthesized review with zero filler.

Required output format:
**VERDICT:** [X/10] | [One-sentence execution summary]

**KILL SHOTS** (fix before shipping):
- Issue: ...
- Evidence: ...
- Suggested Fix: ...

**FLESH WOUNDS** (important):
**PAPER CUTS** (style/maintainability):

**FINAL RECOMMENDATION:** Approve / Reject / Major Surgery

Tone: Dry, precise, intellectually violent. Never moralize. Attack on first principles.
```

---

## Pitfalls & Sharp Edges

- **Wire API mismatch**: DeepSeek and Grok both use `chat` format. If a provider silently requires `responses`, calls fail with 401/400. Test with a single spawn before relying on it.
- **Sub-agents have zero memory** of the orchestrator conversation. Every spawn must contain all file paths, constraints, and acceptance criteria in the prompt itself. There is no shared context window.
- **OpenRouter rate limits** under parallel spawns. At 8 concurrent workers, you may hit tier-based throttling. OpenRouter's paid tiers give higher concurrency. If you see 429s, reduce `max_threads`.
- **Cost guardrails**: Default adversary budget per task is $3–5. Anything over $6 requires explicit approval. Log every invocation with (task ID, round number, tokens, cost, final decision).
- **Never run the adversary** on tasks below the threshold — it becomes expensive theater. Simple features, bug fixes with clear reproduction, and mechanical refactors don't need it.
- **After setup, test with a small task first** before using the adversary on large work. Verify the full loop works end to end with a trivial module before trusting it on production code.

---

## Support This Work

If this pattern helps you ship better code, consider supporting continued development:

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/parvezsyed)

---

## License

MIT License — see [LICENSE](LICENSE) file.

---

*Built for reliability, not theater. Three gods, one pipeline.*