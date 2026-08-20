<!-- markdownlint-disable -->

# Hardening Report: romeovs--lcov-reporter-action/v0.2.21

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **romeovs--lcov-reporter-action/v0.2.21** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Two `uses:` references in .github/workflows/release.yml are pinned to mutable branch or tag refs instead of full 40-character commit SHAs, making the workflow vulnerable to supply-chain attacks if those refs are moved or compromised:
- `uses: actions/checkout@master` (line 14) — branch ref
- `uses: actions/create-release@latest` (line 17) — tag ref
These should be replaced with pinned SHA refs, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4`.

Locations:

- `.github/workflows/release.yml:14`
- `.github/workflows/release.yml:17`

### missing-permissions (severity: medium)

The workflow file .github/workflows/release.yml has no top-level `permissions:` key and the only job (`build`) also has no job-level `permissions:` key. Without explicit permissions, the workflow runs with the default (potentially broad) GITHUB_TOKEN permissions. A minimal permissions block (e.g. `contents: write` for creating releases) should be declared.

Locations:

- `.github/workflows/release.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed .github/workflows/release.yml: (1) Pinned `actions/checkout@master` to SHA `61b9e3751b92087fd0b06925ba6dd6314e06f089 # master` and `actions/create-release@latest` to SHA `0cb9c9b65d5d1901c1f53e5e66eaf4afd303e70e # latest`. (2) Added a top-level `permissions: contents: write` block — the minimum permission required for creating GitHub releases.

