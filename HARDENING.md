<!-- markdownlint-disable -->

# Hardening Report: mablhq--github-run-tests-action/v1.12

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **mablhq--github-run-tests-action/v1.12** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Both workflow files reference `actions/checkout@v3`, which is a mutable tag and not pinned to a full 40-character commit SHA. A tag can be moved to point to a different (potentially malicious) commit, enabling supply-chain attacks. Each reference should be replaced with the full SHA, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v3`.

Locations:

- `.github/workflows/pr-workflow.yaml:8`
- `.github/workflows/push-workflow.yaml:8`

### missing-permissions (severity: medium)

Neither workflow file declares a top-level `permissions:` block, and no job within them declares job-level permissions. Without explicit permissions, GitHub Actions grants the default token permissions (which can include `write` access to repository contents and other scopes depending on the repository settings). A minimal `permissions:` block should be added to restrict the GITHUB_TOKEN to only the scopes actually needed.

Locations:

- `.github/workflows/pr-workflow.yaml:1`
- `.github/workflows/push-workflow.yaml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed both workflow files (.github/workflows/pr-workflow.yaml and .github/workflows/push-workflow.yaml):
1. Pinned `actions/checkout@v3` to full SHA `actions/checkout@a37ce9120846195fa4ece8f58b268e6043cb2f26 # v3` in both files.
2. Added top-level `permissions: contents: read` block to both files, granting only the minimum scope needed for the checkout step.

