<!-- markdownlint-disable -->

# Hardening Report: mablhq--github-run-tests-action/v1.11

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **mablhq--github-run-tests-action/v1.11** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Both workflow files reference `actions/checkout@main`, which is a mutable branch ref rather than a pinned 40-character commit SHA. This means the action could be silently updated to a malicious version without any change to the workflow file, creating a supply-chain attack risk. Each file should pin to a full SHA, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4`.

Locations:

- `.github/workflows/pr-workflow.yaml:8`
- `.github/workflows/push-workflow.yaml:8`

### missing-permissions (severity: medium)

Neither `pr-workflow.yaml` nor `push-workflow.yaml` defines a top-level `permissions:` block, and no job-level `permissions:` blocks are present either. Without explicit permissions, workflows run with the default (potentially broad) token permissions. A minimal `permissions:` block (e.g. `contents: read`) should be added at the top level or per-job to follow the principle of least privilege.

Locations:

- `.github/workflows/pr-workflow.yaml:1`
- `.github/workflows/push-workflow.yaml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed both workflow files (.github/workflows/pr-workflow.yaml and .github/workflows/push-workflow.yaml):
1. Pinned `actions/checkout@main` to the full commit SHA `actions/checkout@f548e57e544e1ff5a4c46bf1e1b8685f8e4a348a # main` to prevent supply-chain attacks via mutable branch refs.
2. Added a top-level `permissions: contents: read` block to both workflows to enforce least-privilege token access.

