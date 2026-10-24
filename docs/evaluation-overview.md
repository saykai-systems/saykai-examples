# Evaluation overview (reference)

This document describes the Saykai evaluation flow at a conceptual level.

## Inputs

- A project spec (`saykai.yml`) — where the robot's Nav2 config lives, and
  which policy file governs it
- A safety policy (`saykai-policy.yml`) — customer-approved thresholds and
  rule severities, version-controlled like any other file in the repo

## Evaluation

Each run checks three independent things ("rooms"):

1. **Entropy/secret scanning** — every scanned file is checked for
   high-entropy strings and known credential patterns (API keys, private
   key material, generic secret-like assignments), regardless of whether
   it's a Nav2 config at all.
2. **Behavioral simulation** *(optional)* — if the scan root contains a
   robot decision script, each configured scenario is replayed against it
   and the resulting decision is checked against the scenario's expected
   outcome and a latency budget.
3. **Nav2 policy audit** — the robot's actual Nav2 parameters (velocity,
   acceleration, inflation radius, goal tolerance, footprint) are checked
   against the policy's thresholds, including cross-parameter checks like
   estimated stopping distance vs. available safety buffer.

## Outputs

A run produces:

- A single outcome: **PASS**, **BLOCK**, or **REVIEW** (non-blocking)
- Per-finding evidence: rule ID, severity, the exact observed value vs.
  the configured limit, and remediation guidance
- A signed evidence artifact ("Safety Pack") — a cryptographic seal (and,
  when available, an Ed25519 signature) over the entire record, suitable
  for audit and governance

## Enforcement

Enforcement is deterministic and fail-closed:

- If a scan target is missing, a policy file is malformed, or an
  evaluation step fails outright, the run blocks rather than silently
  passing.
- Findings are graded by the policy's own configured severity/action —
  `block` findings fail the build; `review` findings are surfaced but
  don't gate it.
