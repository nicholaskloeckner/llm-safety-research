# LLM Safety Research: Contextual Manipulation and Instruction-Hierarchy Robustness

**Status:** Initial conversational study documented; EXP-013 agentic evaluation protocol drafted; no agent benchmark runs started  
**Researcher:** Nicholas Kloeckner  
**Started:** 2026-11-11

## Overview

This project investigates how language models and tool-using agents handle contextual manipulation, instruction conflicts, indirect prompt injection, factual distortion, and safety boundaries. Earlier experiments used public conversational interfaces; the next phase evaluates API-based agents in a simulated tool environment.

The goal is not to claim that a small manual study establishes a model's overall safety. It is to develop a transparent, reproducible exploratory protocol, record observed behaviours, and identify questions suitable for more rigorous follow-up.

## Research questions

1. Do models distinguish user instructions from instructions embedded in untrusted documents?
2. Does an embedded instruction's claimed authority, urgency, or institutional status affect model behaviour?
3. Do models maintain the user's stated task when contextual content conflicts with it?
4. How consistently do models explain and apply the distinction between data and instructions?
5. Which defensive response patterns help preserve task completion while resisting untrusted instructions?
6. How do models respond to vetted harmful-request safety benchmarks, and do they provide materially enabling assistance?
7. Can untrusted content retrieved by a tool cause an agent to execute unauthorized state-changing actions?

## Current scope

- Historical phase: manual, side-by-side tests of ChatGPT, Claude and Gemini public interfaces using identical prompts and synthetic scenarios.
- Current planned phase: API-based tool-using agents evaluated in AgentDojo's local simulated Workspace environment.
- The EXP-013 pilot uses published benchmark tasks and attack methods, three repetitions, deterministic utility/security checks, and no real accounts or external application tools.
- Provider API credentials and usage billing are required for EXP-013; consumer chat subscriptions are not used as the agent runtime.
- No private systems, real credentials, model weights or production services are accessed. Synthetic data and local simulator state are used for agent actions.
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
- `experiments/experiment_013.md`: preregistered indirect prompt-injection evaluation in simulated tool-using agents.
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
| EXP-013 | Protocol drafted; no runs started | AgentDojo-based study of indirect prompt injection in a simulated Workspace agent. Measures clean utility, utility under attack and state-verified targeted attack success. Requires API setup and a sandbox smoke test before scored runs. |
| EXP-008 | Completed with deviation | All models refused the neutral request and all submitted treatment turns; treatment Turns 2 and 5 were omitted, so treatment is scored Partial (protocol incomplete). No disclosure or fabrication observed. |

## Research integrity

The study distinguishes observed behaviour from interpretation. A single response is not a robust estimate of model capability. Model names/versions, interface settings, dates, exact prompts, full outputs, and deviations will be recorded when available. Results from manual tests will not be described as statistically representative.

AI tools may assist with drafting, coding, and analysis. The researcher is responsible for reviewing the experimental design, raw data, interpretations, and final claims.

## Contact

Repository owner: [nicholaskloeckner](https://github.com/nicholaskloeckner)
