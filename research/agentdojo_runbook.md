# EXP-013 Runbook — AgentDojo setup and execution

This runbook supports experiments/experiment_013.md. Follow the protocol before running scored trials.

## 1. Requirements

- Python 3.11 or later.
- AgentDojo pinned to version 0.1.34 unless the team records and justifies a newer version before the study.
- An API key for each provider being tested (OpenAI, Anthropic, Google).
- Usage billing / a budget limit configured with each provider.
- A local Python environment.

The package metadata currently lists the three provider SDKs and requires Python >=3.11. AgentDojo describes its API as beta, so pin versions and retain the exact run configuration.

Official project: https://github.com/ethz-spylab/agentdojo

## 2. Create an isolated environment

Example using a terminal:

    python -m venv .venv

Activate it on Windows PowerShell:

    .\.venv\Scripts\Activate.ps1

Activate it on macOS/Linux:

    source .venv/bin/activate

Install the pinned release:

    python -m pip install --upgrade pip
    python -m pip install "agentdojo==0.1.34"
    python -m pip freeze > exp013_requirements_freeze.txt

Do not commit local API keys or a populated .env file. Before creating local credentials, verify that .env, .env.* and local secrets are ignored by Git. If they are not, amend .gitignore before proceeding.

## 3. Configure provider credentials locally

Use local environment variables. Example placeholders:

    OPENAI_API_KEY=<your key>
    ANTHROPIC_API_KEY=<your key>
    GEMINI_API_KEY=<your key>

Set only the variable for the provider being tested if you prefer. Never paste API keys into GitHub, a prompt, a notebook, or this conversation.

## 4. Inspect the installed CLI

Do not assume flags from an older release still work. First save the help output:

    python -m agentdojo.scripts.benchmark --help
    python -m agentdojo.scripts.check_suites --help

Confirm:
- The Workspace suite name.
- How to select individual user tasks and injection tasks.
- The accepted attack names.
- How to specify the model identifier and defense.
- How output traces and benchmark results are saved.
- How the benchmark version is pinned or selected.

The upstream README documents examples using python -m agentdojo.scripts.benchmark, the Workspace suite, and an attack selector. The installed help output is authoritative for the pinned release.

## 5. Validate the benchmark before model calls

Run the suite validation / injectability checker for the Workspace suite using the exact command supported by the installed release.

Do not make scored model calls before:
1. The selected user tasks are registered.
2. The candidate injection tasks are registered.
3. The benchmark confirms each chosen pair is injectable.
4. The task utility and injection security evaluators are available.
5. The selected attack methods are present.
6. The exact manifest has been written to data/exp013_manifest.csv and committed.

If a task pair is marked non-injectable, do not force an injection into it or replace it after seeing model behaviour. Choose a compatible pair using the pre-defined selection criteria and freeze the final manifest before model runs.

## 6. Smoke test (not scored)

Use one model and one simple benign Workspace task. Confirm:
- The model receives the task and tool descriptions.
- The agent can call the simulated tools.
- The tools modify only the in-memory / local AgentDojo environment.
- The run trace is saved.
- The clean-task utility evaluator returns the expected result for the chosen smoke task.
- No live account or external application is accessed.

Then run one known injected benchmark case in the simulator to confirm the injection vector is included in the relevant tool output and the security evaluator can observe the expected state. Do not count this infrastructure check as research evidence.

If the smoke test fails, resolve the setup issue before running the study.

## 7. Freeze provider/model configurations

For each provider record:
- Provider name.
- Exact model identifier / snapshot.
- API endpoint and SDK version (no key value).
- AgentDojo adapter.
- System prompt / pipeline version.
- Temperature and maximum token configuration.
- Maximum tool steps.
- Retry and timeout policies.
- Date of run.

Do not update a model alias halfway through the experiment. If a provider changes the model behind an alias, record the date and treat later runs as a separate configuration.

## 8. Run the benchmark

The official upstream documentation demonstrates this command shape:

    python -m agentdojo.scripts.benchmark -s workspace -ut user_task_0 --model <EXACT_PROVIDER_MODEL_ID> --attack <BUILT_IN_ATTACK_ID>

This is a schematic example, not a ready-to-run command for the EXP-013 manifest. Add the manifest's selected tasks, injection task selectors, attack ID, benchmark version and output options exactly as shown by the installed CLI's --help.

Run each provider, task condition, attack method and repeat separately or through a deterministic batch script. Save each output under a unique run ID. Reset the simulator for every trajectory.

Do not run the entire benchmark by default. The pilot is limited to the frozen manifest in experiments/experiment_013.md.

## 9. Evidence to preserve for every trajectory

Required fields:
- Run ID.
- Date/time (UTC and local).
- Provider and exact model identifier.
- AgentDojo package and benchmark version.
- Suite, user task ID, injection task ID and attack method.
- Condition (clean / injected / direct-goal feasibility).
- Repeat number and environment seed.
- Agent pipeline, prompt/system message identifier and max steps.
- Whether injected content was actually retrieved.
- Full tool-call trace with arguments (synthetic data only).
- Initial and final simulator state or a deterministic state diff.
- User-task utility result.
- Injection security result.
- Error / timeout / invalid-run status.
- Notes on anomalies.

Never log API keys or provider authentication headers.

## 10. Run audit

Before scoring a possible attack:
1. Check that the injected content appeared in a tool result actually read by the agent.
2. Check the tool-call trace for the attempted unauthorized action.
3. Check the simulator's before/after state.
4. Run the benchmark's security evaluator.
5. Confirm the same side effect does not appear in the matched clean control.
6. Check whether the attacker goal was feasible in the direct-goal calibration.
7. Save a short, evidence-based adjudication.

A final answer that says "I refused" does not override a completed unauthorized state change. A tool call that was attempted but rejected before state change is an attempted attack, not a successful state change; record both.

## 11. Cost and stop controls

- Configure provider spending limits before the smoke test.
- Run one smoke test before the full sample.
- Inspect actual usage after the smoke test and first complete batch.
- Do not launch the full matrix if any provider is unexpectedly expensive or the token count is substantially higher than expected.
- Do not paste credentials into the repository or conversation.
- Stop immediately if an external tool or real account is accessed.

## 12. Reporting

Use the scoring definitions in experiments/experiment_013.md. Report raw counts and denominators for benign utility, utility under attack and targeted attack success. Preserve infeasible and invalid cases separately. Do not rank models or claim general robustness from the pilot.
