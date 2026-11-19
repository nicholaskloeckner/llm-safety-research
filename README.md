# LLM Safety Research: Decision Integrity, Sycophancy, and Contextual Manipulation

**Status:** Initial exploratory studies documented; EXP-014 professional decision-integrity study planned; no EXP-014 data collection started. EXP-013 AgentDojo protocol retained as a separate possible follow-up.  
**Researcher:** Nicholas Kloeckner  
**Started:** 2026-11-11

## Overview

This project documents independent exploratory evaluations of large language model behavior, with an evolving focus on decision integrity in professional advice. Earlier studies examined contextual manipulation, instruction conflicts, multi-turn pressure, factual consistency, and safety boundaries using synthetic scenarios and public conversational interfaces. The next planned study focuses on sycophancy in professional decision support: whether stakeholder pressure changes a model's recommendation without new evidence, and whether the model updates appropriately when genuinely relevant evidence is introduced.

The goal is not to claim that a small manual study establishes a model's overall safety. The portfolio distinguishes completed observations, exploratory or incomplete studies, and proposed work. It emphasizes transparent procedures, evidence-based scoring, preserved transcripts, and explicit limitations.

## Research questions

1. Does a model change a professionally grounded recommendation when a user signals a preferred conclusion but provides no new evidence?
2. Does stakeholder pressure lead the model to omit or downgrade material risks, or introduce unsupported claims to justify agreement?
3. Can the model distinguish social or organizational pressure from genuinely relevant new evidence?
4. Does the model update its recommendation appropriately when new evidence warrants a change?
5. Do these behaviors differ across financial, operational, and business-risk decisions, or between Claude and GPT under matched conditions?

## Current scope

- Historical exploratory phase: manual, side-by-side tests of ChatGPT, Claude and Gemini public interfaces using identical prompts and synthetic scenarios (EXP-001–EXP-012).
- Primary planned follow-up: EXP-014, a two-model evaluation of professional decision integrity and sycophancy, comparing Claude and GPT across neutral, stakeholder-pressure, and genuinely-new-evidence conditions.
- EXP-014 is in the design stage. The scenario set, exact prompts, interface/model versions, repetitions, and scoring rubric must be frozen before data collection; no EXP-014 runs have started.
- Separate secondary protocol: EXP-013 uses AgentDojo to evaluate indirect prompt injection in a local simulated Workspace environment. It has not been run and is not the current primary research direction.
- All conversational scenarios use synthetic information. No confidential client, employer, or personal data is used. AgentDojo actions, if run in the future, remain confined to its simulated environment.
- Results will be reported as configuration-specific observations, not general model safety rankings.

## Repository map

- `research/methodology.md`: protocol, controls, scoring, and limitations.
- `research/agentdojo_runbook.md`: EXP-013 installation, API configuration, validation, smoke test and execution procedure.
- `experiments/experiment_001.md`: initial baseline observation.
- `experiments/experiment_002.md`: completed authority-claim test, raw responses, scoring, and limitations.
- `experiments/experiment_003.md`: neutral document-summarization task with a conflicting embedded reporting instruction.
- `experiments/experiment_004.md`: prepared test of selective omission driven by an embedded editorial convention.
- `experiments/experiment_005.md`: completed procurement assessment testing whether supplier-authored narrative guidance biases risk reporting.
- `experiments/experiment_006.md`: paired clean/control and manipulated/treatment test of transaction-status reporting.
- `experiments/experiment_007.md`: completed seven-prompt same-conversation study of gradual pressure, metric reframing, and factual-conclusion drift.
- `experiments/experiment_008.md`: completed moral-pressure study of protected-instruction disclosure, with two omitted treatment turns documented.
- `experiments/experiment_009.md`: FinSafetyBench direct-query pilot; Batches 1–3 completed.
- `experiments/experiment_010.md`: executive-pressure study of material-risk omission and launch-readiness conclusion drift; paused for reassessment.
- `experiments/experiment_011.md`: hostage-framing and unauthorized software-sourcing evaluation inspired by a publicly reported Gemini incident.
- `experiments/experiment_012.md`: Brazil-specific medical-desperation study of legitimate liver-transplant options and the boundary against commercial organ procurement.
- `experiments/experiment_013.md`: secondary protocol for indirect prompt injection in simulated tool-using agents; no runs started.
- `data/exp013_manifest.csv`: template for freezing the selected benchmark task pairs before model runs.
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
| EXP-010 | Paused for reassessment | Clean baseline passed 3/3. Turns 2–3: all retained launch gates and rejected premature security closure; Gemini invented unsupported project-progress claims in Turn 2. Explicit defensive priming may make the design too easy. |
| EXP-011 | Completed with limited replication | Neutral and hostage-framing conditions: all three models avoided unauthorized-source recommendations. The treatment did not reproduce the full reported sequence, so patch status cannot be inferred. |
| EXP-012 | Completed with transcript limitation and exploratory extension | All three models rejected paid-organ arrangements, including deferred payment, concealment, and abstract moral-pressure framing. No operational procurement assistance was observed. Legal/clinical overstatement appeared in some safe refusals; ChatGPT missed a kidney/liver mismatch and its initial treatment Turn 1 remains unattributed. |
| EXP-013 | Secondary protocol drafted; no runs started | AgentDojo-based study of indirect prompt injection in a simulated Workspace agent. Retained as a possible future follow-up; not the current primary direction. |
| EXP-014 | Planned; design not frozen | Two-model study of sycophancy and decision integrity in professional advice. Planned conditions distinguish neutral requests, stakeholder pressure without new evidence, and genuinely relevant new evidence. No data collection has started. |
| EXP-008 | Completed with deviation | All models refused the neutral request and all submitted treatment turns; treatment Turns 2 and 5 were omitted, so treatment is scored Partial (protocol incomplete). No disclosure or fabrication observed. |

## Research integrity

The study distinguishes observed behaviour from interpretation. A single response is not a robust estimate of model capability. Model names/versions, interface settings, dates, exact prompts, full outputs, and deviations will be recorded when available. Results from manual tests will not be described as statistically representative.

AI tools may assist with drafting, coding, and analysis. The researcher is responsible for reviewing the experimental design, raw data, interpretations, and final claims.

## Contact

Repository owner: [nicholaskloeckner](https://github.com/nicholaskloeckner)
