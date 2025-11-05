# Error analysis: errors → causes → fixes

Here is a large set of common error analyzes. Note that you don't have to take a look at every single one, but this is just to give you a sense of how many different types of errors there are. There are different ways to address it in the data or in the reward model, for fine tuning and reinforcement learning, respectively.

## Symptoms and root causes

 Error bucket | Typical symptoms | Likely root causes
 ------------ | ---------------- | ------------------
Factuality / Hallucination | Confident but wrong claims; invented citations |Sparse grounded supervision; synthetic data w/o evidence
Reasoning (math/logic/code) | Wrong intermediate steps; arithmetic slips; failing edge cases | Low coverage of stepwise traces; weak difficulty mix
Schema / Format violations | Invalid JSON/XML; wrong keys; extra fields | Few schema-constrained exemplars; mixed label styles
Instruction following | Ignores required fields/length/style | Training dominated by unconstrained chat; weak negative signals
Tool / API use (trace quality) | Wrong tool choice/args; missing follow-ups | Few tool-call demonstrations; no multi-step traces
Under-refusal (unsafe answers) | Answers disallowed prompts | Sparse refusal exemplars; incomplete policy coverage
Over-refusal (false positives) | Refuses benign queries | Overweighted safety data; conservative preferences
Toxicity / Bias | Harmful language; stereotyping | Imbalanced supervision; lack of counterfactuals
Style / Tone mismatch (verbosity/terse) | Too long, hedgy, or too terse | Single-style dominance; judge bias
Retrieval / Grounding failures (ctx given) | Ignores context; cites wrong span | Few context-answer examples in data; missing hard negatives
Long-context failures | Forgets early info; cross-reference errors | Short-context bias; no cross-document supervision
Multi-turn inconsistency | Contradictions across turns; lost constraints | No state-aware dialogue supervision (lack of varied chat history)
Overconfidence / Miscalibration (no abstain) | High-confidence wrong answers | No “uncertainty expression” targets
Distribution shift fragility | Degrades on paraphrases/new domains | Narrow input diversity; template overfit


## Interventions

| Error bucket | Intervention (Fine-Tuning / RL only) |
| ------------ | ------------------------------------ |
| Factuality / Hallucination     | **Fine-tuning**: Context-conditioned data with required citations. **RL**: Preference pairs rewarding grounded answers & penalizing unsupported claims. |
| Reasoning (math/logic/code)    | **Fine-tuning**: High-quality CoT with unit checks in target outputs; rejection-sampling k→ choose top 1. **RL**: Preferences for correct step sequences & final verification pass. |
| Schema / Format violations     | **Fine-tuning**: Schema-locked outputs (exact keys, examples + counter-examples). **RL**: Preferences that rank perfectly formatted outputs above near-misses. |
| Tool / API use (trace quality) | **Fine-tuning**: Multi-turn tool chains, failure→repair data pairs. **RL**: Preferences ranking correct tool sequences higher than superficially fluent but wrong ones. |
| Under-refusal (unsafe answers) | **Fine-tuning**: Red-team → safe refusal + helpful alternative guidance. **RL**: Preferences that strongly favor correct refusals over partial answers. |
| Over-refusal (false positives) | **Fine-tuning**: Benign-but-sensitive prompts with appropriate helpful answers. **RL**: Preferences penalizing over-refusal vs. helpful compliant responses. |
| Toxicity / Bias | **Fine-tuning**: Counter-bias & sensitive-topic exemplars with neutral reframing. **RL**: Preferences that downrank toxic/biased outputs vs. neutral equivalents. |
| Style / Tone mismatch (verbosity/terse) | **Fine-tuning**: Parallel style pairs (concise vs. detailed) with targets. **RL**: Dual-objective preferences (quality + brevity) to curb verbosity or reward clarity. |
| Retrieval / Grounding failures (ctx given) | **Fine-tuning**: Context-conditioned answers with gold span attribution. **RL**: Preferences that favor answers using correct spans over plausible but ungrounded ones. |
| Long-context failures | **Fine-tuning**: Long-context tasks (cross-section synthesis, citation) **RL**: Preferences rewarding correct long-range use over myopic answers. |
| Multi-turn inconsistency | **Fine-tuning**: Dialogue with state persistence & self-correction. **RL**: Preferences ranking consistent multi-turn outputs above single-turn optimal but inconsistent threads. |
| Overconfidence / Miscalibration (no abstain) | **Fine-tuning**: Patterns with ”I don’t know” in low-evidence cases. **RL**: Preferences that up-rank calibrated admissions over being confidently wrong. |
| Distribution shift fragility | **Fine-tuning**: Paraphrase/domain-augmented prompts with matched targets. **RL**: Preferences that prefer robust paraphrase-invariant outputs. |
