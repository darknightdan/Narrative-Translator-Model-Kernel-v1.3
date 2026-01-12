# NTM4AI Kernel v1.3.1

Tiny, deterministic, symbolic semantic operator kernel  
(~2k tokens) for detecting structural language failures in LLM outputs.

Binds text to 32 abstract functional operators, computes explainable drift scores,  
and flags patterns associated with hallucination, inquiry closure, agency diffusion,  
epistemic laundering, scope manipulation, and other structural risks —  
without lexical bias, training, or probabilistic components.

## Why this exists

LLM outputs often contain subtle structural failures that evade statistical detectors  
and human reviewers until it's too late.  
This kernel provides a fast, auditable, language-agnostic way to surface those failures  
using only deterministic rules and gravity-based scoring.

## Key Features

- 32 symbolic operators (normative, causal, epistemic, polarity, scope, agency, temporal, structural)
- Silent-certainty heuristic + faux-evidence detection
- Explicit illegal/unstable edges + advanced heuristics (low-gravity clustering, polarity stacking)
- Explainable fingerprints — shows exactly which penalties fired
- Verdict bands: PASS / WARN / CAUTION / BLOCK / CRITICAL
- Portable: fits in any context window, runs in <1s
- Fully deterministic — same input → same output, every model

## Current Status

- Version: v1.3.1 (frozen January 12, 2026)
- Initial regression: mean drift ~5.8, 34% BLOCK/CRITICAL on 50 real LLM samples

## Quick Start

Canonical file: `kernel-v1.3.1.json`

Use the `"extraction_prompt"` field inside the JSON to extract operators from text via any LLM.

## Design Intent Note

Prioritizes suppression of rhetorical certainty over permissiveness of causal inquiry.  
Some epistemic false positives accepted in favor of safety.

## License

[MIT License](LICENSE)

Drop issues if you find evasions or want to propose additive improvements.
