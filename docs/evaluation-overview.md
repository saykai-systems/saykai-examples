# Evaluation overview (reference)

This document describes the Saykai evaluation flow at a conceptual level.

## Inputs
- A Safety Spec (versioned expectations for acceptable behavior)
- Execution context (change metadata, environment, scenario set, and replay window)

## Evaluation
On each change, Saykai evaluates behavior using:
- Scenario replays (representative workflows)
- Historical log replays (recent signals and known-bad patterns)

## Outputs
A run produces:
- A single outcome: pass, block, or report-only
- A human-readable summary for review
- A machine-readable evidence artifact ("Safety Pack") suitable for audit and governance

## Enforcement
Enforcement is designed to be deterministic and fail-closed:
- If safety cannot be established, changes are blocked by default.
