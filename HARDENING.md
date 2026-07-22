<!-- markdownlint-disable -->

# Hardening Report: hspaans--latexmk-action/v2.1.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **hspaans--latexmk-action/v2.1.0** was hardened automatically. 5 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The `runs.image` in action.yml references a mutable Docker image tag (`docker://ghcr.io/hspaans/latexmk-action:2.1`) instead of an immutable SHA digest. This is vulnerable to supply-chain attacks if the image tag is overwritten.

Locations:

- `action.yml:22`

### unpinned-uses (severity: high)

The following `uses:` references in dependabot-auto-merge.yml are pinned to mutable version tags rather than full 40-character commit SHAs: `dependabot/fetch-metadata@v2`.

Locations:

- `.github/workflows/dependabot-auto-merge.yml:21`

### unpinned-uses (severity: high)

The following `uses:` references in docker-image.yml are pinned to mutable version tags rather than full 40-character commit SHAs: `actions/checkout@v4` (two occurrences), `docker/setup-qemu-action@v3`, `docker/setup-buildx-action@v3`, `docker/login-action@v3`, `docker/build-push-action@v6`.

Locations:

- `.github/workflows/docker-image.yml:22`
- `.github/workflows/docker-image.yml:37`
- `.github/workflows/docker-image.yml:41`
- `.github/workflows/docker-image.yml:45`
- `.github/workflows/docker-image.yml:49`
- `.github/workflows/docker-image.yml:55`

### permissions (severity: medium)

docker-image.yml has no top-level `permissions:` key and neither the `build-test` nor `build-release` job defines a job-level `permissions:` block. This means the workflow runs with the default (broad) token permissions.

Locations:

- `.github/workflows/docker-image.yml:1`

### unpinned-uses (severity: high)

The following `uses:` references in hadolint.yml are pinned to mutable version tags rather than full 40-character commit SHAs: `actions/checkout@v4`, `github/codeql-action/upload-sarif@v3`. (Note: `hadolint/hadolint-action@54c9adbab1582c2ef04b2016b760714a4bfde3cf` is correctly pinned.)

Locations:

- `.github/workflows/hadolint.yml:28`
- `.github/workflows/hadolint.yml:40`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, permissions

**Notes:**

Fixed all findings:
1. action.yml: Pinned Docker image `ghcr.io/hspaans/latexmk-action:2.1` to immutable digest `sha256:6a184a9675f159b474b4d5001e4ae328686befd19029bf0903f2ad35c07e0f27`, preserving `docker://` scheme and tag inline.
2. dependabot-auto-merge.yml: Pinned `dependabot/fetch-metadata@v2` → `@21025c705c08248db411dc16f3619e6b5f9ea21a # v2`.
3. docker-image.yml: Pinned all 6 action references to full commit SHAs; added top-level `permissions: {}` and minimal job-level permissions (`contents: read` for build-test; `contents: read` + `packages: write` for build-release).
4. hadolint.yml: Pinned `actions/checkout@v4` → `@11d5960a326750d5838078e36cf38b85af677262 # v4` and `github/codeql-action/upload-sarif@v3` → `@4187e74d05793876e9989daffde9c3e66b4acd07 # v3`.

