---
name: repo-quality-gate
description: Enforces review and validation standards for this AWS data engineering lab repository. Use when editing code, reviewing changes, preparing commits, or deciding if work is merge-ready.
disable-model-invocation: true
---

# Repo Quality Gate

Apply this skill for code changes in `udemy-aws-de-labs`.

## 1) Workflow Foundation (Ground Truth First)

Scope of work:
- Default working directory: repository root `.` (`udemy-aws-de-labs`).
- Do not assume project-wide build tooling; this repository is a set of independent labs and assignments.

Read these files first before coding:
1. `README.md` (repo context and caveats)
2. The target module being changed (for example `Lab2-Airflow-Spark-Dynamo/glue-pyspark.py`)
3. Closest test file(s), if present:
   - `Assignment5-CI-CD-of-Lambda/test_lambda.py`
   - `Lab9-CICD-GithubActions-Lambda-Glue-ECS/ecs/test_app.py`
   - `Lab9-CICD-GithubActions-Lambda-Glue-ECS/glue-pythonshell/test_glue.py`
   - `Lab9-CICD-GithubActions-Lambda-Glue-ECS/lambda-functions/test_lambda_function.py`
4. Any local execution helper scripts in the same lab (for example `local-docker-development.sh` / `.ps1`)

Rule: if a file conflicts with these sources, treat the above as ground truth and call out the conflict explicitly.

## 2) Targeted Validation (Run What Applies)

Run checks closest to the changed files. Prefer fast, deterministic checks first.

Python syntax check:
```bash
python -m py_compile <changed_python_file.py>
```

Shell script syntax check:
```bash
bash -n <changed_script.sh>
```

JSON validity check:
```bash
python -m json.tool <changed_file.json> > /dev/null
```

Test execution (module-focused first, then broader if needed):
```bash
pytest Assignment5-CI-CD-of-Lambda/test_lambda.py -q
pytest Lab9-CICD-GithubActions-Lambda-Glue-ECS/ecs/test_app.py -q
pytest Lab9-CICD-GithubActions-Lambda-Glue-ECS/glue-pythonshell/test_glue.py -q
pytest Lab9-CICD-GithubActions-Lambda-Glue-ECS/lambda-functions/test_lambda_function.py -q
```

Optional quality tools (run only if already installed/configured in current environment):
```bash
ruff check <changed_paths>
black --check <changed_paths>
mypy <changed_paths>
```

If a required tool is missing, report it and continue with available checks instead of silently skipping validation.

## 3) Testing Standards (Proof Level)

Unit Tests (small, isolated behavior):
- Validate one function/class behavior at a time.
- Mock network, AWS services, filesystem, and clocks.
- Fast and deterministic; should run locally without cloud dependencies.

Integration Tests (multi-component behavior):
- Validate boundaries between components (for example Lambda -> DynamoDB logic, ingestion -> transformation flow).
- Use realistic inputs and verify contracts between systems.
- May use controlled mocks/simulators (for example `moto`) but must prove collaboration behavior, not only single-function output.

Acceptance rule:
- Small logic change: at least unit-level proof.
- Cross-module/dataflow change: unit + integration-level proof (or explicit rationale why integration proof is not possible yet).

## 4) Brevity and Logic (Noise Detection)

Flag and remove noise:
- Redundant comments that restate obvious code.
- Duplicated logic or repeated constants without reason.
- Repeated prose in docs/PR notes that adds no new information.
- Dead code and unused imports/variables.

Standard: every line should have a clear functional or explanatory purpose.

## 5) Feedback Levels

Use exactly these levels in reviews:

- **Blocker**: must be fixed before merge.
  - Examples: incorrect logic, broken tests, unsafe behavior, data corruption risk, missing required validation.
- **Nit**: minor suggestion that does not block merge.
  - Examples: naming clarity, micro-refactors, comment polish, non-critical formatting.

When reporting feedback, prefer short bullets and classify each item as `Blocker` or `Nit`.

## 6) Release Rules (Major.Minor.Build)

Version format: `Major.Minor.Build` (three numeric segments), optionally prefixed by `v` in tags.

Bump guidance:
- **Major**: breaking behavior or contract changes.
- **Minor**: backward-compatible feature additions.
- **Build**: fixes, docs, refactors, or internal improvements without feature/contract break.

Verification checklist for release readiness:
1. New version follows `X.Y.Z` format.
2. Version progression is monotonic (no rollback or duplicate).
3. Change scope matches bump type.
4. Release note or commit message states the reason for the bump.

