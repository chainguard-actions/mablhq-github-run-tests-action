<!-- markdownlint-disable -->

# Hardening Report: mablhq--github-run-tests-action/v1.14

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **mablhq--github-run-tests-action/v1.14** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Both workflow files reference GitHub Actions using mutable version tags (@v4) instead of full 40-character commit SHA digests. This exposes the workflow to supply-chain attacks if the tag is moved to a malicious commit. Affected references: `actions/checkout@v4` and `actions/setup-node@v4` in both pr-workflow.yaml and push-workflow.yaml.

Locations:

- `.github/workflows/pr-workflow.yaml:9`
- `.github/workflows/pr-workflow.yaml:10`
- `.github/workflows/push-workflow.yaml:9`
- `.github/workflows/push-workflow.yaml:10`

### missing-permissions (severity: medium)

Neither workflow file defines a top-level `permissions:` block, and neither job within them defines job-level permissions. Without explicit permissions, the GITHUB_TOKEN is granted its default (often broad) permissions, violating the principle of least privilege.

Locations:

- `.github/workflows/pr-workflow.yaml:1`
- `.github/workflows/push-workflow.yaml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed both .github/workflows/pr-workflow.yaml and .github/workflows/push-workflow.yaml:
1. Pinned `actions/checkout@v4` to full SHA `11d5960a326750d5838078e36cf38b85af677262` (# v4 comment preserved).
2. Pinned `actions/setup-node@v4` to full SHA `49933ea5288caeca8642d1e84afbd3f7d6820020` (# v4 comment preserved).
3. Added top-level `permissions: {}` to both workflow files to enforce least-privilege GITHUB_TOKEN access.

