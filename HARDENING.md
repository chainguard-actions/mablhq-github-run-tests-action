<!-- markdownlint-disable -->

# Hardening Report: mablhq--github-run-tests-action/v1.13.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **mablhq--github-run-tests-action/v1.13.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Both workflow files reference `actions/checkout@v3`, which is a mutable tag rather than a pinned 40-character commit SHA. If the tag is moved (e.g. by a supply-chain compromise), the workflow will silently execute different code. Pin to a full SHA, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v3`.

Locations:

- `.github/workflows/pr-workflow.yaml:8`
- `.github/workflows/push-workflow.yaml:8`

### missing-permissions (severity: medium)

Neither workflow file declares a top-level `permissions:` key, and neither job within them declares its own `permissions:` block. Without explicit permissions, the GITHUB_TOKEN is granted its default (potentially broad) permissions. Add a top-level `permissions:` block with the minimal scopes required (e.g. `contents: read`).

Locations:

- `.github/workflows/pr-workflow.yaml:1`
- `.github/workflows/push-workflow.yaml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

In both .github/workflows/pr-workflow.yaml and .github/workflows/push-workflow.yaml: (1) Pinned `actions/checkout@v3` to the full commit SHA `a37ce9120846195fa4ece8f58b268e6043cb2f26` with a `# v3` comment for readability. (2) Added a top-level `permissions: contents: read` block — the minimal scope required for the checkout step — to restrict the default GITHUB_TOKEN permissions.

