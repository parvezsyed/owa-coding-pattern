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

```svg
<svg class="arch-svg" viewBox="0 0 1000 410" xmlns="http://www.w3.org/2000/svg">
    <defs>
      <linearGradient id="bgGrad" x1="0%" y1="0%" x2="100%" y2="100%">
        <stop offset="0%" stop-color="#0f1216"/>
        <stop offset="100%" stop-color="#0a0c0f"/>
      </linearGradient>
      <linearGradient id="orchGrad" x1="0%" y1="0%" x2="0%" y2="100%">
        <stop offset="0%" stop-color="#1e3a8a"/>
        <stop offset="100%" stop-color="#1a3280"/>
      </linearGradient>
      <linearGradient id="workGrad" x1="0%" y1="0%" x2="0%" y2="100%">
        <stop offset="0%" stop-color="#064e3b"/>
        <stop offset="100%" stop-color="#054530"/>
      </linearGradient>
      <linearGradient id="advGrad" x1="0%" y1="0%" x2="0%" y2="100%">
        <stop offset="0%" stop-color="#7f1d1d"/>
        <stop offset="100%" stop-color="#6b1717"/>
      </linearGradient>
      <filter id="glowBlue" x="-20%" y="-20%" width="140%" height="140%">
        <feGaussianBlur in="SourceGraphic" stdDeviation="4" result="blur"/>
        <feMerge><feMergeNode in="blur"/><feMergeNode in="SourceGraphic"/></feMerge>
      </filter>
      <filter id="glowGreen" x="-20%" y="-20%" width="140%" height="140%">
        <feGaussianBlur in="SourceGraphic" stdDeviation="4" result="blur"/>
        <feMerge><feMergeNode in="blur"/><feMergeNode in="SourceGraphic"/></feMerge>
      </filter>
      <filter id="glowRed" x="-20%" y="-20%" width="140%" height="140%">
        <feGaussianBlur in="SourceGraphic" stdDeviation="4" result="blur"/>
        <feMerge><feMergeNode in="blur"/><feMergeNode in="SourceGraphic"/></feMerge>
      </filter>
      <marker id="arrBlue" markerWidth="9" markerHeight="7" refX="9" refY="3.5" orient="auto">
        <polygon points="0 0, 9 3.5, 0 7" fill="#3b82f6"/>
      </marker>
      <marker id="arrGreen" markerWidth="9" markerHeight="7" refX="9" refY="3.5" orient="auto">
        <polygon points="0 0, 9 3.5, 0 7" fill="#10b981"/>
      </marker>
      <marker id="arrRed" markerWidth="9" markerHeight="7" refX="9" refY="3.5" orient="auto">
        <polygon points="0 0, 9 3.5, 0 7" fill="#ef4444"/>
      </marker>
    </defs>

    <!-- Background -->
    <rect x="0" y="0" width="1000" height="410" rx="18" fill="url(#bgGrad)" stroke="#1f242c" stroke-width="1"/>

    <!-- ===== ORCHESTRATOR (top) ===== -->
    <rect x="195" y="28" width="610" height="105" rx="16" fill="url(#orchGrad)" stroke="#3b82f6" stroke-width="2.5" filter="url(#glowBlue)"/>
    <text x="500" y="55" text-anchor="middle" fill="#e4e7eb" font-size="19" font-weight="700" letter-spacing="0.08em">ORCHESTRATOR</text>
    <text x="500" y="75" text-anchor="middle" fill="#93c5fd" font-size="12" font-family="ui-monospace, SFMono-Regular, Menlo, monospace">GPT-5.5</text>
    <text x="500" y="93" text-anchor="middle" fill="#bfdbfe" font-size="10.5">Planning &amp; Decomposition &amp; Synthesis &amp; Quality Gates</text>
    <text x="500" y="112" text-anchor="middle" fill="#fbbf24" font-size="10" font-family="ui-monospace, SFMono-Regular, Menlo, monospace" font-weight="600">ACCEPT · REFINE · REJECT</text>

    <!-- ===== WORKERS (left) ===== -->
    <rect x="42" y="195" width="440" height="110" rx="16" fill="url(#workGrad)" stroke="#10b981" stroke-width="2.5" filter="url(#glowGreen)"/>
    <rect x="48" y="201" width="8" height="98" rx="4" fill="#0d9488" opacity="0.15"/>
    <rect x="60" y="201" width="8" height="98" rx="4" fill="#0d9488" opacity="0.1"/>
    <rect x="72" y="201" width="8" height="98" rx="4" fill="#0d9488" opacity="0.06"/>
    <text x="262" y="228" text-anchor="middle" fill="#e4e7eb" font-size="16" font-weight="700" letter-spacing="0.06em">WORKERS  ×8</text>
    <text x="262" y="252" text-anchor="middle" fill="#6ee7b7" font-size="11.5" font-family="ui-monospace, SFMono-Regular, Menlo, monospace">DeepSeek V4 Flash / Pro</text>
    <text x="262" y="274" text-anchor="middle" fill="#4ade80" font-size="10.5">Parallel execution · Cheap · Bounded scope</text>
    <text x="262" y="294" text-anchor="middle" fill="#6ee7b7" font-size="10" font-style="italic">Returns diffs + test results</text>

    <!-- ===== ADVERSARY (right) ===== -->
    <rect x="518" y="195" width="440" height="110" rx="16" fill="url(#advGrad)" stroke="#ef4444" stroke-width="2.5" filter="url(#glowRed)"/>
    <text x="738" y="228" text-anchor="middle" fill="#e4e7eb" font-size="16" font-weight="700" letter-spacing="0.06em">ADVERSARY</text>
    <text x="738" y="252" text-anchor="middle" fill="#fca5a5" font-size="11.5" font-family="ui-monospace, SFMono-Regular, Menlo, monospace">Grok 4.3 · Independent Critique</text>
    <text x="738" y="274" text-anchor="middle" fill="#f87171" font-size="10.5">HELD · STRAINED · BROKEN layers</text>
    <text x="738" y="294" text-anchor="middle" fill="#fca5a5" font-size="10" font-style="italic">Counter-Resonance flags</text>

    <!-- ===== ARROWS (arrow zone: y=133 to y=195) ===== -->
    <!-- LEFT LANE: Orch ↔ Workers -->
    <!-- SPAWN (blue down) — label at mid-zone -->
    <path d="M 300 133 L 252 195" fill="none" stroke="#3b82f6" stroke-width="2.2" marker-end="url(#arrBlue)" opacity="0.9"/>
    <text x="255" y="167" text-anchor="end" fill="#60a5fa" font-size="10" font-family="ui-monospace, SFMono-Regular, Menlo, monospace" font-weight="600">SPAWN</text>

    <!-- DIFFS+TESTS (green dashed up) — label left of arrow, at SPAWN y-level -->
    <path d="M 430 195 L 460 133" fill="none" stroke="#10b981" stroke-width="2" stroke-dasharray="6,4" marker-end="url(#arrGreen)" opacity="0.75"/>
    <text x="425" y="167" text-anchor="end" fill="#34d399" font-size="9.5" font-family="ui-monospace, SFMono-Regular, Menlo, monospace">DIFFS+TESTS</text>

    <!-- RIGHT LANE: Orch ↔ Adversary -->
    <!-- REVIEW (blue down) — label at mid-zone -->
    <path d="M 700 133 L 748 195" fill="none" stroke="#3b82f6" stroke-width="2.2" marker-end="url(#arrBlue)" opacity="0.9"/>
    <text x="755" y="167" text-anchor="start" fill="#60a5fa" font-size="10" font-family="ui-monospace, SFMono-Regular, Menlo, monospace" font-weight="600">REVIEW</text>

    <!-- VERDICT (red dashed up) — label at SPAWN y-level -->
    <path d="M 570 195 L 540 133" fill="none" stroke="#ef4444" stroke-width="2" stroke-dasharray="6,4" marker-end="url(#arrRed)" opacity="0.75"/>
    <text x="545" y="167" text-anchor="end" fill="#f87171" font-size="9.5" font-family="ui-monospace, SFMono-Regular, Menlo, monospace">VERDICT</text>

    <!-- Cross-lane subtle flow hint -->
    <path d="M 482 250 Q 500 250 518 250" fill="none" stroke="#374151" stroke-width="1" stroke-dasharray="3,5" opacity="0.4"/>

    <!-- ===== SECTION LABEL ===== -->
    <text x="500" y="360" text-anchor="middle" fill="#e4e7eb" font-size="10" font-weight="500" font-family="ui-monospace, SFMono-Regular, Menlo, monospace">The Orchestrator is the sole decision maker. Workers execute. The Adversary critiques. None of these models trust each other.</text>
  </svg>
```

---

## The Iteration Cycle (Phases)

The iteration cycle that makes this pattern powerful — each phase has a clear owner and output:

```svg
<svg class="arch-svg" viewBox="0 0 1100 280" xmlns="http://www.w3.org/2000/svg">
    <defs>
      <linearGradient id="phaseBg" x1="0%" y1="0%" x2="100%" y2="100%">
        <stop offset="0%" stop-color="#0f1216"/>
        <stop offset="100%" stop-color="#0a0c0f"/>
      </linearGradient>
      <marker id="parr" markerWidth="8" markerHeight="6" refX="8" refY="3" orient="auto">
        <polygon points="0 0, 8 3, 0 6" fill="#4b5563"/>
      </marker>
    </defs>

    <!-- Background -->
    <rect x="0" y="0" width="1100" height="280" rx="16" fill="url(#phaseBg)" stroke="#1f242c" stroke-width="1"/>

    <!-- ===== PHASE 1: DECOMPOSE (Orchestrator) ===== -->
    <rect x="15" y="30" width="160" height="195" rx="12" fill="#181b20" stroke="#3b82f6" stroke-width="2.5"/>
    <circle cx="95" cy="30" r="15" fill="#1e3a8a" stroke="#3b82f6" stroke-width="2"/>
    <text x="95" y="35" text-anchor="middle" fill="#e4e7eb" font-size="12" font-weight="700" font-family="ui-monospace, SFMono-Regular, Menlo, monospace">1</text>
    <text x="95" y="68" text-anchor="middle" fill="#e4e7eb" font-size="13" font-weight="700" letter-spacing="0.04em">DECOMPOSE</text>
    <text x="95" y="86" text-anchor="middle" fill="#93c5fd" font-size="10" font-family="ui-monospace, SFMono-Regular, Menlo, monospace">GPT-5.5</text>
    <line x1="30" y1="96" x2="160" y2="96" stroke="#252a32" stroke-width="1"/>
    <text x="30" y="115" fill="#9ca3af" font-size="9.5">Break task into bounded,</text>
    <text x="30" y="133" fill="#9ca3af" font-size="9.5">testable slices. Define</text>
    <text x="30" y="151" fill="#9ca3af" font-size="9.5">interfaces &amp; criteria.</text>

    <!-- Arrow 1→2 -->
    <line x1="175" y1="127" x2="190" y2="127" stroke="#4b5563" stroke-width="2" marker-end="url(#parr)"/>

    <!-- ===== PHASE 2: IMPLEMENT (Worker) ===== -->
    <rect x="195" y="30" width="160" height="195" rx="12" fill="#181b20" stroke="#10b981" stroke-width="2.5"/>
    <circle cx="275" cy="30" r="15" fill="#064e3b" stroke="#10b981" stroke-width="2"/>
    <text x="275" y="35" text-anchor="middle" fill="#e4e7eb" font-size="12" font-weight="700" font-family="ui-monospace, SFMono-Regular, Menlo, monospace">2</text>
    <text x="275" y="68" text-anchor="middle" fill="#e4e7eb" font-size="13" font-weight="700" letter-spacing="0.04em">IMPLEMENT</text>
    <text x="275" y="86" text-anchor="middle" fill="#6ee7b7" font-size="10" font-family="ui-monospace, SFMono-Regular, Menlo, monospace">DeepSeek V4 Flash</text>
    <line x1="210" y1="96" x2="340" y2="96" stroke="#252a32" stroke-width="1"/>
    <text x="210" y="115" fill="#9ca3af" font-size="9.5">Parallel execution (up</text>
    <text x="210" y="133" fill="#9ca3af" font-size="9.5">to 8). Each produces</text>
    <text x="210" y="151" fill="#9ca3af" font-size="9.5">diff + test results.</text>

    <!-- Arrow 2→3 -->
    <line x1="355" y1="127" x2="370" y2="127" stroke="#4b5563" stroke-width="2" marker-end="url(#parr)"/>

    <!-- ===== PHASE 3: INTEGRATE (Orchestrator) ===== -->
    <rect x="375" y="30" width="160" height="195" rx="12" fill="#181b20" stroke="#3b82f6" stroke-width="2.5"/>
    <circle cx="455" cy="30" r="15" fill="#1e3a8a" stroke="#3b82f6" stroke-width="2"/>
    <text x="455" y="35" text-anchor="middle" fill="#e4e7eb" font-size="12" font-weight="700" font-family="ui-monospace, SFMono-Regular, Menlo, monospace">3</text>
    <text x="455" y="68" text-anchor="middle" fill="#e4e7eb" font-size="13" font-weight="700" letter-spacing="0.04em">INTEGRATE</text>
    <text x="455" y="86" text-anchor="middle" fill="#93c5fd" font-size="10" font-family="ui-monospace, SFMono-Regular, Menlo, monospace">GPT-5.5</text>
    <line x1="390" y1="96" x2="520" y2="96" stroke="#252a32" stroke-width="1"/>
    <text x="390" y="115" fill="#9ca3af" font-size="9.5">Collect outputs, merge,</text>
    <text x="390" y="133" fill="#9ca3af" font-size="9.5">run cross-cutting tests.</text>
    <text x="390" y="151" fill="#9ca3af" font-size="9.5">Resolve all conflicts.</text>

    <!-- Arrow 3→4 -->
    <line x1="535" y1="127" x2="550" y2="127" stroke="#4b5563" stroke-width="2" marker-end="url(#parr)"/>

    <!-- ===== PHASE 4: CRITIQUE (Adversary) ===== -->
    <rect x="555" y="30" width="160" height="195" rx="12" fill="#181b20" stroke="#ef4444" stroke-width="2.5"/>
    <circle cx="635" cy="30" r="15" fill="#7f1d1d" stroke="#ef4444" stroke-width="2"/>
    <text x="635" y="35" text-anchor="middle" fill="#e4e7eb" font-size="12" font-weight="700" font-family="ui-monospace, SFMono-Regular, Menlo, monospace">4</text>
    <text x="635" y="68" text-anchor="middle" fill="#e4e7eb" font-size="13" font-weight="700" letter-spacing="0.04em">CRITIQUE</text>
    <text x="635" y="86" text-anchor="middle" fill="#fca5a5" font-size="10" font-family="ui-monospace, SFMono-Regular, Menlo, monospace">Grok 4.3</text>
    <line x1="570" y1="96" x2="700" y2="96" stroke="#252a32" stroke-width="1"/>
    <text x="570" y="115" fill="#9ca3af" font-size="9.5">For high-risk segments,</text>
    <text x="570" y="133" fill="#9ca3af" font-size="9.5">spawn the adversary.</text>
    <text x="570" y="151" fill="#9ca3af" font-size="9.5">HELD/STRAINED/BROKEN.</text>

    <!-- Arrow 4→5 -->
    <line x1="715" y1="127" x2="730" y2="127" stroke="#4b5563" stroke-width="2" marker-end="url(#parr)"/>

    <!-- ===== PHASE 5: REFINE (Orchestrator) ===== -->
    <rect x="735" y="30" width="160" height="195" rx="12" fill="#181b20" stroke="#3b82f6" stroke-width="2.5"/>
    <circle cx="815" cy="30" r="15" fill="#1e3a8a" stroke="#3b82f6" stroke-width="2"/>
    <text x="815" y="35" text-anchor="middle" fill="#e4e7eb" font-size="12" font-weight="700" font-family="ui-monospace, SFMono-Regular, Menlo, monospace">5</text>
    <text x="815" y="68" text-anchor="middle" fill="#e4e7eb" font-size="13" font-weight="700" letter-spacing="0.04em">REFINE</text>
    <text x="815" y="86" text-anchor="middle" fill="#93c5fd" font-size="10" font-family="ui-monospace, SFMono-Regular, Menlo, monospace">GPT-5.5</text>
    <line x1="750" y1="96" x2="880" y2="96" stroke="#252a32" stroke-width="1"/>
    <text x="750" y="115" fill="#9ca3af" font-size="9.5">Address adversary</text>
    <text x="750" y="133" fill="#9ca3af" font-size="9.5">findings. Re-spawn for</text>
    <text x="750" y="151" fill="#9ca3af" font-size="9.5">BROKEN, patch STRAINED.</text>

    <!-- Arrow 5→6 -->
    <line x1="895" y1="127" x2="910" y2="127" stroke="#4b5563" stroke-width="2" marker-end="url(#parr)"/>

    <!-- ===== PHASE 6: DELIVER (Orchestrator) ===== -->
    <rect x="915" y="30" width="160" height="195" rx="12" fill="#181b20" stroke="#3b82f6" stroke-width="2.5"/>
    <circle cx="995" cy="30" r="15" fill="#1e3a8a" stroke="#3b82f6" stroke-width="2"/>
    <text x="995" y="35" text-anchor="middle" fill="#e4e7eb" font-size="12" font-weight="700" font-family="ui-monospace, SFMono-Regular, Menlo, monospace">6</text>
    <text x="995" y="68" text-anchor="middle" fill="#e4e7eb" font-size="13" font-weight="700" letter-spacing="0.04em">DELIVER</text>
    <text x="995" y="86" text-anchor="middle" fill="#93c5fd" font-size="10" font-family="ui-monospace, SFMono-Regular, Menlo, monospace">GPT-5.5</text>
    <line x1="930" y1="96" x2="1060" y2="96" stroke="#252a32" stroke-width="1"/>
    <text x="930" y="115" fill="#9ca3af" font-size="9.5">Final validation, commit,</text>
    <text x="930" y="133" fill="#9ca3af" font-size="9.5">summary. Only declare</text>
    <text x="930" y="151" fill="#9ca3af" font-size="9.5">done after re-verify.</text>

    <!-- ===== ROLE LEGEND (bottom) ===== -->
    <rect x="280" y="245" width="12" height="12" rx="3" fill="#3b82f6" opacity="0.8"/>
    <text x="298" y="255" fill="#9ca3af" font-size="9.5">Orchestrator (GPT-5.5)</text>
    <rect x="450" y="245" width="12" height="12" rx="3" fill="#10b981" opacity="0.8"/>
    <text x="468" y="255" fill="#9ca3af" font-size="9.5">Worker (DeepSeek)</text>
    <rect x="605" y="245" width="12" height="12" rx="3" fill="#ef4444" opacity="0.8"/>
    <text x="623" y="255" fill="#9ca3af" font-size="9.5">Adversary (Grok 4.3)</text>
  </svg>
```

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