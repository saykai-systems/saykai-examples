# verify-demo

Two **real** Safety Packs, produced by `saykai-runner` v1.4.0 and signed with a demo-only Ed25519 key. Unlike the fabricated sample in `artifacts/`, you can verify these.

| File | What it is |
| :--- | :--- |
| `safety-pack-block.json` | A blocked run: `velocity_smoother.max_velocity[0]` raised to 0.60 against a 0.45 limit |
| `safety-pack-pass.json` | A clean run on the original config |
| `saykai-signing.pub` | The demo public key (one 64-character hex key per line) |
| `scan_targets_block/`, `scan_targets_pass/` | The Nav2 files each run audited |
| `saykai-policy.yml` | The policy each run was judged against (illustrative thresholds) |
| `block-output.txt`, `pass-output.txt` | Console output of each run |

## Verify in your browser

Open <https://saykai.com/verify>. Your browser re-computes the SHA-256 seal and checks the Ed25519 signature locally. Nothing is uploaded. Edit one character in the pack and it fails.

## Verify on the command line

```
saykai-runner verify safety-pack-block.json --public-key saykai-signing.pub
```

Expected: `STATUS: VERIFIED`. The same command on a pack with any edit prints `STATUS: TAMPERED`.

## What verification proves

- The record is exactly what the runner sealed: the SHA-256 seal matches, every top-level field agrees with the sealed payload, and the signature was made by the private half of the key you trust.
- It does not prove who holds the key. You decide which key to trust, which is why the public key is published here and on the website, so you can compare the two copies.
- This demo key signs these samples only. In your own CI you hold your own signing key (`saykai-runner keygen`), so only you can sign your evidence and anyone with your public key can verify it.

The `operator` field in each pack (`runner` on `gha-runner-01`) is generic on purpose: the runs were made in a clean Linux environment.
