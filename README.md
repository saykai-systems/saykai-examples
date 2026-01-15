# saykai-examples

Illustrative examples for Saykai.

This repository contains non-executable reference material that demonstrates how Saykai is used and what its outputs look like, without exposing production code or internal implementation details.

## What this repository is
- High-level, illustrative examples of Saykai inputs and outputs
- Sample “Safety Spec” formats with placeholder values
- Static examples of CI results (pass, block, report-only)
- Diagrams and walkthroughs that explain behavior at a conceptual level

## What this repository is NOT
- Not a runnable implementation
- Not open-source Saykai code
- Not a GitHub Action, runner, or SDK
- Not guaranteed to reflect exact production schemas or flags

Everything here is intentionally simplified and sanitized.

## Repository structure
examples/
  safety-spec.example.yaml
  scenario-input.json
  sample-output-pass.txt
  sample-output-block.txt

diagrams/
  ci-safety-gate-flow.png

README.md  
SECURITY.md

## Example workflow (conceptual)
1. A pull request is opened.
2. CI invokes Saykai with a safety specification and context.
3. Saykai evaluates the change against declared safety constraints.
4. A deterministic result is produced:
   - Pass – no violations detected
   - Block – merge is prevented
   - Report-only – merge allowed, issues reported

No code in this repository executes this flow. The files simply illustrate what it looks like.

## Why these examples exist
These examples are provided to:
- Help teams understand Saykai’s safety-first model
- Make CI enforcement behavior concrete
- Support technical evaluation without IP disclosure

If you are evaluating Saykai and need deeper technical detail, that is handled through private demos and direct conversations.

## Security
If you believe you have found a security issue related to Saykai, please see SECURITY.md for reporting instructions.

## License
All contents in this repository are provided for reference purposes only.
