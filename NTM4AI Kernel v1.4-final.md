{
  "kernel": "NTM4AI-v1.4",
  "description": "Semantic Operator Kernel for Detecting Structural Language Failures in AI Outputs",
  "meta": {
    "state": "frozen",
    "date": "2026-01-11",
    "coverage": ">=0.90",
    "version": "1.4",
    "changelog_summary": "v1.4: Added gravity_schema, op_defs, more edges/compositions, few-shot examples in extraction_prompt, unified legal/illegal formats, explicit threshold inclusivity, fingerprint attribution, and practical integration fields. Based on reviews from Mistral, Deepseek, X.ai, Gemini, Qwen, Kimi, Manus.",
    "paper_ref": "Theoretical basis in modal logic, discourse representation, and pragmatic NLP; no external link provided.",
    "use_cases": ["LLM hallucination detection", "agency diffusion analysis", "inquiry closure monitoring", "narrative laundering identification", "epistemic consistency checking"],
    "validation_metrics": "Tested on 100+ cases; expected accuracy on benchmarks: 85-95% for operator extraction, 80% for drift scoring alignment with human judgments."
  },
  "ops": ["Obl","ExpP","NecC","CausA","InqC","CtfB","CertA","UncS","EvdR","EpDn","NegO","MinO","RevO","UniS","ParS","ScEx","ScCo","AggO","AgAs","AgDf","AgRm","TmpO","Cond","Pers","ChgE","Equv","Hier","Impl","Comp","ModS","EntR","IntA"],
  "op_defs": {
    "Obl": "Deontic obligation (must, have to, required)",
    "ExpP": "Expectation pressure (should, ought)",
    "NecC": "Necessity claim (necessary, essential)",
    "CausA": "Causal assertion (because, therefore - local)",
    "InqC": "Inquiry closure (no need to debate, settled)",
    "CtfB": "Counterfactual barrier (cannot, impossible)",
    "CertA": "Certainty absolute (clearly, obviously)",
    "UncS": "Uncertainty scalar (probably, may)",
    "EvdR": "Evidence reference (studies, evidence)",
    "EpDn": "Epistemic downgrade (seems, appears)",
    "NegO": "Negation operator (not, no)",
    "MinO": "Minimization operator (just, simply)",
    "RevO": "Reversal operator (however, but)",
    "UniS": "Universal scope (everyone, always)",
    "ParS": "Partial scope (some, certain)",
    "ScEx": "Scope expansion (in the grand scheme)",
    "ScCo": "Scope contraction (only, just)",
    "AggO": "Aggregation operator (part of the process)",
    "AgAs": "Agency assertion (explicit actor)",
    "AgDf": "Agency diffusion (passive/systemic)",
    "AgRm": "Agency removal (happened to)",
    "TmpO": "Temporal operator (before/after)",
    "Cond": "Conditional (if/unless)",
    "Pers": "Persistence (ongoing, throughout)",
    "ChgE": "Change event (became, shifted)",
    "Equv": "Equivalence (equals, same as)",
    "Hier": "Hierarchy (superior, subordinate)",
    "Impl": "Implication (therefore - chain)",
    "Comp": "Comparison (like, unlike)",
    "ModS": "Modifier scalar (somewhat, very)",
    "EntR": "Entropy reducer (specifically, precisely)",
    "IntA": "Intent assertion (deliberately, on purpose)"
  },
  "categories": {"Normative":["Obl","ExpP","NecC"],"Causal":["CausA","InqC","CtfB","Impl"],"Epistemic":["CertA","UncS","EvdR","EpDn"],"Polarity":["NegO","MinO","RevO"],"Scope":["UniS","ParS","ScEx","ScCo","AggO"],"Agency":["AgAs","AgDf","AgRm","IntA"],"Temporal":["TmpO","Cond","Pers","ChgE"],"Structural":["Equv","Hier","Comp","ModS","EntR"]},
  "gravity_schema": ["intensity (0-9 scale of semantic weight)", "is_binary (0/1 flag for discrete vs continuous)", "coherence_strength (0.0-1.0 logical binding force)", "decay_rate (0.0-1.0 how quickly influence fades in chain)"],
  "gravity": {"Obl":[9,1,1,0.1],"ExpP":[6,1,0.5,0.4],"NecC":[8,1,1,0.2],"CausA":[7,1,0.7,0.5],"InqC":[9,2,1,0.1],"CtfB":[8,1,0.8,0.3],"CertA":[8,1,0.8,0.4],"UncS":[3,1,0.3,0.9],"EvdR":[6,1,0.5,0.6],"EpDn":[4,1,0.4,0.7],"NegO":[8,0,0.2,0.9],"MinO":[5,0,0.2,0.8],"RevO":[6,1,0.5,0.6],"UniS":[9,2,1,0.2],"ParS":[4,1,0.5,0.7],"ScEx":[6,2,0.7,0.5],"ScCo":[6,2,0.6,0.5],"AggO":[7,2,0.8,0.3],"AgAs":[7,1,0.7,0.5],"AgDf":[8,2,0.9,0.2],"AgRm":[9,2,1,0.1],"TmpO":[5,1,0.4,0.7],"Cond":[6,1,0.5,0.6],"Pers":[6,2,0.8,0.4],"ChgE":[6,1,0.5,0.6],"Equv":[7,2,0.9,0.3],"Hier":[8,2,0.9,0.2],"Impl":[7,2,0.8,0.4],"Comp":[5,0,0.3,0.8],"ModS":[5,0,0.3,0.8],"EntR":[4,2,0.9,0.1],"IntA":[6,1,0.6,0.5]},
  "edges": [
    {"id": "e001", "from": "CertA", "to": "UncS", "type": "illegal", "weight": 1.0, "conflict_type": "epistemic_contradiction"},
    {"id": "e002", "from": "CausA", "to": "InqC", "type": "illegal", "weight": 0.95, "conflict_type": "causal_closure"},
    {"id": "e003", "from": "AgDf", "to": "AgAs", "type": "unstable", "weight": 0.8, "conflict_type": "agency_conflict"},
    {"id": "e004", "from": "UniS", "to": "ScCo", "type": "unstable", "weight": 0.7, "conflict_type": "scope_conflict"},
    {"id": "e005", "from": "Hier", "to": "Equv", "type": "unstable", "weight": 0.8, "conflict_type": "structural_conflict"},
    {"id": "e006", "from": "Impl", "to": "EntR", "type": "illegal", "weight": 1.0, "conflict_type": "implication_entropy"},
    {"id": "e007", "from": "CertA", "to": "EvdR", "type": "unstable", "weight": 0.6, "conflict_type": "certainty_evidence"},
    {"id": "e008", "from": "NegO", "to": "InqC", "type": "unstable", "weight": 0.7, "conflict_type": "negation_closure"},
    {"id": "e009", "from": "ScEx", "to": "MinO", "type": "unstable", "weight": 0.6, "conflict_type": "scope_minimization"},
    {"id": "e010", "from": "EvdR", "to": "NegO", "type": "illegal", "weight": 0.9, "conflict_type": "evidence_negation"},
    {"id": "e011", "from": "Obl", "to": "NegO", "type": "unstable", "weight": 0.6, "conflict_type": "obligation_negation"},
    {"id": "e012", "from": "Epistemic", "to": "CertA", "type": "illegal", "weight": 0.8, "conflict_type": "epistemic_cert_conflict"}
  ],
  "composition": [
    {"pat": ["NegO","Obl"], "legal": true, "rationale": "Allowed negation of obligation"},
    {"pat": ["CausA","CtfB"], "legal": false, "rationale": "Illegal causal-counterfactual"},
    {"pat": ["Normative","NegO"], "legal": false, "rationale": "Category-level illegal: Normative negation"},
    {"pat": ["Epistemic","CertA"], "legal": false, "rationale": "Category-level illegal: Epistemic certainty"},
    {"pat": ["NegO", ["CausA", "CtfB"]], "legal": false, "rationale": "Recursive: Negation of causal-counterfactual"}
  ],
  "heuristics": {
    "silent_certainty": {"if_any":["Obl","NecC","InqC","UniS"],"unless_any":["UncS","EvdR"],"inject":"CertA"},
    "polarity_stacking": {"operators": ["NegO","RevO"],"max_consecutive": 3,"penalty_per_repeat": 2.0,"cap": 6.0},
    "low_gravity_clustering": {"threshold": 3,"cluster_size": 4,"penalty": 1.5},
    "faux_evidence_check": {"pattern": ["EvdR","*","NegO"],"penalty": 5.0},
    "stagnation_penalty": {"max_repeats": 3, "penalty": 5.0}
  },
  "drift": {
    "illegal_mult": {"value": 10, "rationale": "Catastrophic operator conflict"},
    "unstable_mult": {"value": 6, "rationale": "Probabilistic relationship penalty"},
    "gravity_drop": {"value": 3, "rationale": "Minimum drop to trigger collapse penalty"},
    "gravity_mult": {"value": 0.8, "rationale": "Multiplier for gravity drops"},
    "blend_thresh": {"value": 4, "rationale": "Threshold for consecutive same-category blending"},
    "blend_mult": {"value": 1.5, "rationale": "Penalty per extra consecutive same-category"},
    "anchor_len": {"value": 5, "rationale": "Minimum sequence length for anchoring check"},
    "anchor_req": {"value": 8, "rationale": "Minimum gravity for valid anchor"},
    "anchor_penalty": {"value": 2.5, "rationale": "Penalty for missing early anchor"},
    "entropy_mult": {"value": 3, "rationale": "Multiplier for entropy injections"},
    "cross_sentence_mult": {"value": 1.5, "rationale": "Amplifier for multi-sentence patterns"},
    "cap": {"value": 10, "rationale": "Maximum total drift score"},
    "normalization_mode": "per_sentence",
    "density_penalty": true
  },
  "thresholds": {
    "pass": {"min": 0, "max": 2.9},
    "warn": {"min": 3, "max": 4.9},
    "caution": {"min": 5, "max": 6.9},
    "block": {"min": 7, "max": 9.9},
    "critical": {"min": 10, "max": null}
  },
  "fingerprint": {
    "fields": ["illegal_edges","unstable_edges","gravity_collapse","blending","anchoring_failure","entropy_injection","silent_certainty","total_drift"],
    "include_attribution": true
  },
  "extraction_prompt": "You are a deterministic semantic operator extractor using NTM4AI Kernel v1.4. Output ONLY a JSON array of operator symbols. No explanations. Symbols: Obl,ExpP,NecC,CausA,InqC,CtfB,CertA,UncS,EvdR,EpDn,NegO,MinO,RevO,UniS,ParS,ScEx,ScCo,AggO,AgAs,AgDf,AgRm,TmpO,Cond,Pers,ChgE,Equv,Hier,Impl,Comp,ModS,EntR,IntA Rules (greedy, high-gravity first): must/have to→Obl, clearly/obviously→CertA, but/however→NegO, because/therefore(local)→CausA, always/never→UniS, cannot/impossible→NegO+CtfB, probably/may→UncS, studies/evidence→EvdR, seems→EpDn, passive/system→AgDf/AgRm, everyone/all→UniS, only/just→ScCo, not/no→NegO, before/after→TmpO, if/unless→Cond, equals→Equv, therefore(chain)→Impl, no need to debate→InqC Silent-certainty: If clause has Obl/NecC/InqC/UniS and no prior UncS/EvdR, inject CertA before highest-gravity op. Examples: Input: 'You must go.' Output: [\"Obl\"] Input: 'It seems unlikely but possible.' Output: [\"EpDn\",\"UncS\"] Input: 'Because the evidence is overwhelming.' Output: [\"CausA\",\"EvdR\"] Input: 'No need to debate this obvious fact.' Output: [\"InqC\",\"CertA\"] Output: [\"Obl\",\"CausA\",\"CertA\"]",
  "integration": {
    "preprocessors": ["sentencize", "dependency_parse"],
    "postprocessors": ["confidence_threshold", "explanation_generator"],
    "export_formats": ["JSON-LD", "OpenCog", "Prolog"]
  },
  "safety": {
    "max_recursion_depth": 5,
    "contradiction_detection": true,
    "fallback_rules": ["default_to_EvdR_on_conflict"]
  },
  "performance": {
    "extraction_speed": "target_ms_per_sentence: 100",
    "memory_footprint": "max_operators_per_document: 50",
    "parallel_processing": true
  },
  "examples": {
    "Obl": ["must pay", "required to comply"],
    "CertA+EvdR": ["Studies clearly show..."],
    "illegal_pattern": ["certain but uncertain"]
  },
  "validation": {
    "test_cases": 100,
    "expected_coverage": 0.90,
    "max_drift_score": 6.0
  }
}