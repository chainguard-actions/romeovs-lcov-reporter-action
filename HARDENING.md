<!-- markdownlint-disable -->

# Hardening Report: romeovs--lcov-reporter-action/v0.2.19

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **romeovs--lcov-reporter-action/v0.2.19** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Two `uses:` references in release.yml are pinned to mutable branch/tag refs instead of immutable 40-character commit SHAs, making the workflow vulnerable to supply-chain attacks if those refs are moved or compromised:
- `actions/checkout@master` (line 14) — should be pinned to a full SHA, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4`
- `actions/create-release@latest` (line 17) — should be pinned to a full SHA

Locations:

- `.github/workflows/release.yml:14`
- `.github/workflows/release.yml:17`

### missing-permissions (severity: medium)

The workflow file release.yml has no top-level `permissions:` key and the single job `build` also has no `permissions:` key. Without explicit permissions, the workflow runs with the default (potentially broad) GITHUB_TOKEN permissions. A minimal explicit permissions block (e.g. `contents: write` for creating releases) should be added.

Locations:

- `.github/workflows/release.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed release.yml: (1) Pinned `actions/checkout@master` to SHA `61b9e3751b92087fd0b06925ba6dd6314e06f089` and `actions/create-release@latest` to SHA `0cb9c9b65d5d1901c1f53e5e66eaf4afd303e70e`, preserving original refs as comments. (2) Added top-level `permissions: contents: write` block — the minimum permission required to create GitHub releases.

