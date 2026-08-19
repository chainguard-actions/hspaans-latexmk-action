<!-- markdownlint-disable -->

# Hardening Report: hspaans--latexmk-action/v1.3.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **hspaans--latexmk-action/v1.3.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple workflow files and action.yml reference mutable tags or branch names instead of pinned SHA digests, making the action vulnerable to supply-chain attacks:
- action.yml: `image: 'docker://ghcr.io/hspaans/latexmk-action:1'` uses mutable tag `:1` instead of a SHA digest (e.g. `@sha256:<64-hex-char-digest>`)
- container-release.yml: `uses: hspaans/.github/.github/workflows/container-release.yml@master` uses branch ref `@master`
- docker-image.yml: `uses: actions/checkout@v4` uses tag `@v4`
- hadolint.yml: `uses: actions/checkout@v4` uses tag `@v4`; `uses: github/codeql-action/upload-sarif@v3` uses tag `@v3`

Locations:

- `action.yml:16`
- `.github/workflows/container-release.yml:12`
- `.github/workflows/docker-image.yml:14`
- `.github/workflows/hadolint.yml:22`
- `.github/workflows/hadolint.yml:28`

### missing-permissions (severity: medium)

Two workflow files have no top-level `permissions:` key and no job-level `permissions:` key on any of their jobs. Without explicit permissions, the GITHUB_TOKEN is granted default (potentially write) permissions, violating the principle of least privilege.
- container-release.yml: no permissions declared at top-level or job level
- docker-image.yml: no permissions declared at top-level or job level

Locations:

- `.github/workflows/container-release.yml:1`
- `.github/workflows/docker-image.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all unpinned action/image references by resolving real SHAs: (1) action.yml: pinned ghcr.io/hspaans/latexmk-action:1 to sha256:2f207ff4697812da898497a931ce358ffe0e600c66e892584f5d6c9d27dbb137 (docker:// scheme preserved); (2) container-release.yml: pinned hspaans/.github@master to commit SHA 880d91388b14f0155475ac3d961e4aa6d0225df8; (3) docker-image.yml: pinned actions/checkout@v4 to 11d5960a326750d5838078e36cf38b85af677262; (4) hadolint.yml: pinned actions/checkout@v4 to 11d5960a326750d5838078e36cf38b85af677262 and github/codeql-action/upload-sarif@v3 to 4187e74d05793876e9989daffde9c3e66b4acd07. Added `permissions: {}` top-level blocks to container-release.yml and docker-image.yml to enforce least-privilege GITHUB_TOKEN access.

