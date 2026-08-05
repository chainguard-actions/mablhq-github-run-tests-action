<!-- markdownlint-disable -->

# Hardening Report: mablhq--github-run-tests-action/v1.15

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **mablhq--github-run-tests-action/v1.15** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### missing-permissions (severity: medium)

The workflow file has no top-level `permissions:` key and the single job also has no `permissions:` key. This means the workflow runs with the default (potentially broad) token permissions. A `permissions:` block with minimal specific scopes should be added.

Locations:

- `.github/workflows/pr-workflow.yaml:1`
- `.github/workflows/push-workflow.yaml:1`

### unpinned-uses (severity: high)

Both workflow files reference GitHub Actions using mutable version tags (`@v4`) instead of pinned full-length SHA commit hashes. This exposes the workflow to supply-chain attacks if the tag is moved to a malicious commit. Affected references:
- `actions/checkout@v4` (pr-workflow.yaml line 9, push-workflow.yaml line 9)
- `actions/setup-node@v4` (pr-workflow.yaml line 10, push-workflow.yaml line 10)

These should be pinned to their full 40-character SHA digests, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4`.

Locations:

- `.github/workflows/pr-workflow.yaml:9`
- `.github/workflows/pr-workflow.yaml:10`
- `.github/workflows/push-workflow.yaml:9`
- `.github/workflows/push-workflow.yaml:10`

## Iteration Notes

### Iteration 1

**Fixes applied:** missing-permissions, unpinned-uses

**Notes:**

Fixed both workflow files (.github/workflows/pr-workflow.yaml and .github/workflows/push-workflow.yaml):
1. Added `permissions: {}` top-level block to both files to restrict default token permissions.
2. Pinned `actions/checkout@v4` to SHA `11d5960a326750d5838078e36cf38b85af677262 # v4` in both files.
3. Pinned `actions/setup-node@v4` to SHA `49933ea5288caeca8642d1e84afbd3f7d6820020 # v4` in both files.

