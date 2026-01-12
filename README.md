# NTM4AI Kernel v1.3-final

**A tiny, deterministic, symbolic semantic operator kernel for detecting structural language failures in LLM outputs.**

NTM4AI binds text to 32 abstract functional operators, computes explainable drift scores, and flags patterns associated with hallucination, inquiry closure, agency diffusion, epistemic laundering, scope manipulation, and other structural risks — **without any lexical bias, training, or probabilistic components**.

### Why this exists

LLM outputs often contain subtle structural failures that evade statistical detectors and human reviewers until it's too late.  
This kernel provides a fast, auditable, language-agnostic way to surface those failures using only deterministic rules and gravity-based scoring.

### Key Features

- **32 symbolic operators** covering normative, causal, epistemic, polarity, scope, agency, temporal, and structural forces
- **Silent-certainty heuristic** + faux-evidence detection to catch implied certainty without grounding
- **16 explicit edges** (illegal/unstable) + 4 advanced heuristics (low-gravity clustering, polarity stacking, category transitions)
- **Explainable fingerprints** — shows exactly which penalties fired (illegal edges, gravity drops, blending, etc.)
- **Verdict bands**: PASS / WARN / CAUTION / BLOCK / CRITICAL
- **Portable**: ~2k tokens — fits in any context window, runs on CPU in <1s
- **Fully deterministic** — same input → same output, every time, every model
