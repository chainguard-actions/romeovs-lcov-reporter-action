<!-- markdownlint-disable -->

# Hardening Report: romeovs--lcov-reporter-action/v0.2.20

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **romeovs--lcov-reporter-action/v0.2.20** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Two `uses:` references in .github/workflows/release.yml are pinned to mutable branch or tag refs instead of immutable 40-character SHA digests. This exposes the workflow to supply-chain attacks if the referenced action is compromised or the branch/tag is moved:
- `actions/checkout@master` (branch ref)
- `actions/create-release@latest` (tag ref)
These should be replaced with full SHA-pinned references, e.g. `actions/checkout@<40-char-sha> # master`.

Locations:

- `.github/workflows/release.yml:13`
- `.github/workflows/release.yml:16`

### missing-permissions (severity: medium)

The workflow file .github/workflows/release.yml has no top-level `permissions:` key and no job-level `permissions:` key on any job. Without explicit permissions, the workflow inherits the default repository token permissions, which may be broader than necessary. A minimal permissions block (e.g. `contents: write` for creating releases) should be added at the top level or per-job.

Locations:

- `.github/workflows/release.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed .github/workflows/release.yml: (1) Pinned actions/checkout@master to SHA 61b9e3751b92087fd0b06925ba6dd6314e06f089 and actions/create-release@latest to SHA 0cb9c9b65d5d1901c1f53e5e66eaf4afd303e70e, preserving original refs as comments. (2) Added top-level `permissions: contents: write` block — the minimum permission required for creating GitHub releases.

