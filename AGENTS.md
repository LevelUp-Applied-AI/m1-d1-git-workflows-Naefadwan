1. Testing Requirements What must pass before any AI-assisted change is committed?

## Testing Requirements

All changes must pass `python test_environment.py` before committing.
Any code added to `src/` must have a corresponding test in `tests/`
that passes with `pytest tests/ -v`.

Additional medical‑standard requirements:
- Validate that any code interacting with clinical data includes
  automated checks for HIPAA/PHI handling and de‑identification.
- Clinical or regulatory review must sign off on changes that
  touch patient‑related logic or data models.

2. Secrets Policy What should never appear in a prompt or be committed?

## Secrets Policy

Do not include API keys, database passwords, file paths containing
personal data, or raw data content in any prompt. Never commit
`.env`, `*.key`, or any file containing credentials.

For medical projects the policy is stricter:
- **Protected Health Information (PHI)** must never appear in
  prompts, logs, or version control. Use synthetic or de‑identified
  data for development and testing.
- Enforce HIPAA compliance; document any third‑party access to
  clinical data and ensure proper encryption and auditing.
3. Scope Boundaries Which files may the agent edit? Which require human review?

## Scope Boundaries

Agents may edit files in `src/` and `notebooks/`.
Do not modify `requirements.txt` without human review.
Do not modify `setup.sh` without running and testing the result locally.
Do not touch `.gitignore` without confirming the change doesn't
accidentally exclude source files.

Medical notes:
- Any code files that process or store clinical information require
  review by a qualified clinician or compliance officer before
  merging.
- Do not introduce new data schemas for patient records without
  prior architectural sign‑off.
4. Reproducibility Standard What does “done” mean for an AI-assisted change?

## Reproducibility Standard

All AI-assisted changes require local-first execution: the change
must run locally and produce the expected output before it is
committed or pushed. "The AI generated it" is not a substitute
for running it.

In a medical context, reproducibility also means:
- Tests should be executed with realistic but compliant datasets.
- Document any assumptions about clinical data formats or
  regulatory requirements so reviewers can verify correctness.