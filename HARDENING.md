<!-- markdownlint-disable -->

# Hardening Report: romeovs--lcov-reporter-action/v0.3.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **romeovs--lcov-reporter-action/v0.3.1** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow file .github/workflows/release.yml references two actions using mutable branch/tag refs instead of pinned full 40-character SHA digests. This exposes the workflow to supply-chain attacks if the referenced branch or tag is moved to point at malicious code.

- `uses: actions/checkout@master` (line 14) — uses the mutable `master` branch
- `uses: actions/create-release@latest` (line 17) — uses the mutable `latest` tag

Both should be pinned to a full commit SHA, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4`.

Locations:

- `.github/workflows/release.yml:14`
- `.github/workflows/release.yml:17`

### missing-permissions (severity: medium)

The workflow file .github/workflows/release.yml has no top-level `permissions:` key and the only job (`build`) also has no job-level `permissions:` key. Without explicit permissions, the workflow inherits the default repository token permissions, which may be broader than necessary (e.g. write access to contents). A minimal permissions block such as `permissions: contents: write` should be declared at the job or workflow level.

Locations:

- `.github/workflows/release.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed .github/workflows/release.yml: (1) Pinned actions/checkout@master to SHA 61b9e3751b92087fd0b06925ba6dd6314e06f089 and actions/create-release@latest to SHA 0cb9c9b65d5d1901c1f53e5e66eaf4afd303e70e, with inline comments preserving the original ref names. (2) Added top-level `permissions: contents: write` block — the minimum required for creating GitHub releases via the GITHUB_TOKEN.

