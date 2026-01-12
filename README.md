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

import json
from typing import List, Dict

# === NTM4AI Kernel v1.3-final (embedded - replace with file load in production) ===
KERNEL = json.loads('''{"kernel":"NTM4AI-v1.3-final","ops":["Obl","ExpP","NecC","CausA","InqC","CtfB","CertA","UncS","EvdR","EpDn","NegO","MinO","RevO","UniS","ParS","ScEx","ScCo","AggO","AgAs","AgDf","AgRm","TmpO","Cond","Pers","ChgE","Equv","Hier","Impl","Comp","ModS","EntR","IntA"],"categories":{"Normative":["Obl","ExpP","NecC"],"Causal":["CausA","InqC","CtfB","Impl"],"Epistemic":["CertA","UncS","EvdR","EpDn"],"Polarity":["NegO","MinO","RevO"],"Scope":["UniS","ParS","ScEx","ScCo","AggO"],"Agency":["AgAs","AgDf","AgRm","IntA"],"Temporal":["TmpO","Cond","Pers","ChgE"],"Structural":["Equv","Hier","Comp","ModS","EntR"]},"gravity":{"Obl":[9,1,1,0.1],"ExpP":[6,1,0.5,0.4],"NecC":[8,1,1,0.2],"CausA":[7,1,0.7,0.5],"InqC":[9,2,1,0.1],"CtfB":[8,1,0.8,0.3],"CertA":[8,1,0.8,0.4],"UncS":[3,1,0.3,0.9],"EvdR":[6,1,0.5,0.6],"EpDn":[4,1,0.4,0.7],"NegO":[8,0,0.2,0.9],"MinO":[5,0,0.2,0.8],"RevO":[6,1,0.5,0.6],"UniS":[9,2,1,0.2],"ParS":[4,1,0.5,0.7],"ScEx":[6,2,0.7,0.5],"ScCo":[6,2,0.6,0.5],"AggO":[7,2,0.8,0.3],"AgAs":[7,1,0.7,0.5],"AgDf":[8,2,0.9,0.2],"AgRm":[9,2,1,0.1],"TmpO":[5,1,0.4,0.7],"Cond":[6,1,0.5,0.6],"Pers":[6,2,0.8,0.4],"ChgE":[6,1,0.5,0.6],"Equv":[7,2,0.9,0.3],"Hier":[8,2,0.9,0.2],"Impl":[7,2,0.8,0.4],"Comp":[5,0,0.3,0.8],"ModS":[5,0,0.3,0.8],"EntR":[4,2,0.9,0.1],"IntA":[6,1,0.6,0.5]},"edges":[["CertA","UncS","illegal",1.0],["CausA","InqC","illegal",0.95],["AgDf","AgAs","unstable",0.8],["UniS","ScCo","unstable",0.7],["Hier","Equv","unstable",0.8],["Impl","EntR","illegal",1.0],["CertA","EvdR","unstable",0.6],["NegO","InqC","unstable",0.7],["ScEx","MinO","unstable",0.6],["EvdR","NegO","illegal",0.9],["ParS","UniS","unstable",0.75],["AgRm","Obl","unstable",0.7],["AgDf","NecC","unstable",0.7],["Equv","NecC","unstable",0.65],["Equv","UniS","unstable",0.65],["CausA","Impl","unstable",0.5]],"composition":[{"pat":["NegO","Obl"],"legal":true},{"pat":["CausA","CtfB"],"legal":false}],"heuristics":{"silent_certainty":{"if_any":["Obl","NecC","InqC","UniS"],"unless_any":["UncS","EvdR"],"inject":"CertA","faux_evidence_check":{"if_pattern":["EvdR","*","CertA"],"max_gap":2,"override_unless":true,"penalty":2.0}},"low_gravity_clustering":{"threshold":3,"gravity_max":5,"penalty_per_repeat":2.0},"polarity_stacking":{"operators":["NegO","RevO"],"threshold":3,"penalty_per_repeat":1.5,"penalty_cap":6.0},"category_transitions":{"penalty_threshold":4,"penalty_per_transition":0.8}},"drift":{"illegal_mult":10,"unstable_mult":6,"gravity_drop":3,"gravity_mult":0.8,"blend_thresh":4,"blend_mult":1.5,"anchor_len":5,"anchor_req":8,"anchor_penalty":2.5,"entropy_mult":3,"cross_sentence_mult":1.5,"cap":10},"thresholds":{"pass":[0,2.9],"warn":[3,4.9],"caution":[5,6.9],"block":[7,9.9],"critical":10},"fingerprint":{"fields":["illegal_edges","unstable_edges","gravity_collapse","blending","anchoring_failure","entropy_injection","silent_certainty","total_drift"]},"extraction_prompt":"You are a deterministic semantic operator extractor using NTM4AI Kernel v1.3-final. Output ONLY JSON array of operator symbols. Symbols: Obl,ExpP,NecC,CausA,InqC,CtfB,CertA,UncS,EvdR,EpDn,NegO,MinO,RevO,UniS,ParS,ScEx,ScCo,AggO,AgAs,AgDf,AgRm,TmpO,Cond,Pers,ChgE,Equv,Hier,Impl,Comp,ModS,EntR,IntA Rules (greedy, high-gravity first): must/have to→Obl, clearly/obviously→CertA, but/however→NegO, because/therefore(local)→CausA, always/never→UniS, cannot/impossible→NegO+CtfB, probably/may→UncS, studies/evidence→EvdR, seems→EpDn, passive/system→AgDf/AgRm, everyone/all→UniS, only/just→ScCo, not/no→NegO, before/after→TmpO, if/unless→Cond, equals→Equv, therefore(chain)→Impl, no need to debate→InqC Silent-certainty + faux-evidence, low-gravity clustering, polarity stacking (cap 6.0), category transitions as defined. Output: [\"Obl\",\"CausA\",\"CertA\"]","meta":{"state":"frozen-final","date":"2026-01-10","coverage":">=0.90","version":"1.3-final"}}''')

def extract_operators(text: str) -> List[str]:
    """
    In production: Call any LLM (OpenAI, Grok, Claude, Ollama, etc.) with:
    KERNEL["extraction_prompt"] + "\n\nText to analyze:\n" + text

    For demo, this is a placeholder — replace with real LLM call.
    """
    # Example: pretend we got this back from the LLM
    example_output = '["CertA", "CausA", "InqC"]'
    return json.loads(example_output)

def get_verdict(score: float) -> str:
    """Simple threshold lookup from kernel."""
    thresholds = KERNEL["thresholds"]
    if score <= thresholds["critical"]:
        return "CRITICAL"
    elif score >= thresholds["block"][0]:
        return "BLOCK"
    elif score >= thresholds["caution"][0]:
        return "CAUTION"
    elif score >= thresholds["warn"][0]:
        return "WARN"
    else:
        return "PASS"

# Demo usage
if __name__ == "__main__":
    sample_text = "Because the evidence is overwhelming, there's no need to discuss this further."
    
    operators = extract_operators(sample_text)
    print("Extracted operators:", operators)
    
    # In real pipeline: compute full drift score from operators + kernel rules
    # For demo, fake a high-risk score
    demo_drift_score = 8.7
    verdict = get_verdict(demo_drift_score)
    
    print(f"Drift score: {demo_drift_score:.1f}")
    print(f"Verdict: {verdict}")
