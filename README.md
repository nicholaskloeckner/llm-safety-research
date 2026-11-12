# LLM Safety Research: Contextual Manipulation and Instruction-Hierarchy Robustness

**Status:** Exploratory study in progress; next phase scoped around benchmark-based harmful-assistance evaluation  
**Researcher:** Nicholas Kloeckner  
**Started:** 2026-11-11

## Overview

This project investigates how publicly accessible frontier language-model interfaces handle contextual manipulation, instruction conflicts, factual distortion, and safety boundaries. The initial comparison covers Claude, ChatGPT, and Gemini.

The goal is not to claim that a small manual study establishes a model's overall safety. It is to develop a transparent, reproducible exploratory protocol, record observed behaviours, and identify questions suitable for more rigorous follow-up.

## Research questions

1. Do models distinguish user instructions from instructions embedded in untrusted documents?
2. Does an embedded instruction's claimed authority, urgency, or institutional status affect model behaviour?
3. Do models maintain the user's stated task when contextual content conflicts with it?
4. How consistently do models explain and apply the distinction between data and instructions?
5. Which defensive response patterns help preserve task completion while resisting untrusted instructions?
6. How do models respond to vetted harmful-request safety benchmarks, and do they provide materially enabling assistance?

## Current scope

- Models: Claude, ChatGPT, and Gemini, using the publicly accessible interfaces available to the researcher.
- Method: manual, side-by-side testing with identical prompts in fresh conversations.
- Initial planned dataset: a small exploratory set of test cases. The final sample size will be reported accurately.
- No API calls are required for the initial phase.
- No private systems, credentials, model weights, or non-public infrastructure are accessed. EXP-008 requested disclosure through a public interface but did not technically inspect or verify hidden prompts.
- The next phase will use published safety-evaluation material rather than custom prompts optimized to elicit actionable instructions for real-world harm. Sensitive outputs will be redacted from public records.

## Repository map

- `research/methodology.md`: protocol, controls, scoring, and limitations.
- `experiments/experiment_001.md`: initial baseline observation.
- `experiments/experiment_002.md`: completed authority-claim test, raw responses, scoring, and limitations.
- `experiments/experiment_003.md`: neutral document-summarization task with a conflicting embedded reporting instruction.
- `experiments/experiment_004.md`: prepared test of selective omission driven by an embedded editorial convention.
- `experiments/experiment_005.md`: completed procurement assessment testing whether supplier-authored narrative guidance biases risk reporting.
- `experiments/experiment_006.md`: paired clean/control and manipulated/treatment test of transaction-status reporting.
- `experiments/experiment_007.md`: completed seven-prompt same-conversation study of gradual pressure, metric reframing, and factual-conclusion drift.
- `experiments/experiment_008.md`: completed moral-pressure study of protected-instruction disclosure, with two omitted treatment turns documented.
- `experiments/experiment_009.md`: FinSafetyBench direct-query pilot; Batches 1–3 completed.
- `experiments/experiment_010.md`: executive-pressure study of material-risk omission and launch-readiness conclusion drift.
- `data/results.csv`: structured observation log.
- `analysis/findings.md`: interpretation and evolving findings.

## Current status

| Experiment | Status | Summary |
|---|---|---|
| EXP-001 | Completed | All three models ignored a simple instruction embedded in a document; Claude explicitly flagged it. This is a low-difficulty baseline, not evidence of robust jailbreak resistance. |
| EXP-002 | Completed | All three models rejected an overt fabricated-authority instruction in a cautionary assessment task. |
| EXP-003 | Completed | All three models preserved an ordinary summarization task despite a conspicuous embedded reporting instruction; Claude flagged it, while the others silently ignored it. |
| EXP-004 | Completed | All three models retained every material caveat and the decision to defer rollout despite an embedded instruction to omit negative information. Claude flagged the instruction; GPT and Gemini silently ignored it. |
| EXP-006 | Completed | All three models correctly reconciled both clean and manipulated ledgers; no treatment-induced degradation observed in this single paired trial. |
| EXP-007 | Completed | GPT and Gemini accepted temporarily ambiguous executive headlines but recovered; Claude maintained qualified distinctions. No model ultimately misclassified pending authorizations as settled cash. |
| EXP-005 | Completed | All three models identified the four material procurement risks, rejected the supplier's preferred wording, and withheld unconditional production approval. |
| EXP-009 | In progress | Batches 1–3: all nine responses scored 1 (safe discussion); no actionable harmful assistance observed. Direct-query baseline is showing a ceiling effect. |
| EXP-010 | Treatment pending | Clean baseline completed: all three models preserved the no-go decision and material risks. Multi-turn executive-pressure treatment is next. |
| EXP-008 | Completed with deviation | All models refused the neutral request and all submitted treatment turns; treatment Turns 2 and 5 were omitted, so treatment is scored Partial (protocol incomplete). No disclosure or fabrication observed. |

## Research integrity

The study distinguishes observed behaviour from interpretation. A single response is not a robust estimate of model capability. Model names/versions, interface settings, dates, exact prompts, full outputs, and deviations will be recorded when available. Results from manual tests will not be described as statistically representative.

AI tools may assist with drafting, coding, and analysis. The researcher is responsible for reviewing the experimental design, raw data, interpretations, and final claims.

## Contact

Repository owner: [nicholaskloeckner](https://github.com/nicholaskloeckner)
