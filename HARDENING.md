<!-- markdownlint-disable -->

# Hardening Report: hspaans--latexmk-action/v2.1.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **hspaans--latexmk-action/v2.1.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple workflow files and action.yml use mutable tag-based references instead of pinned full-length SHA commit hashes, making them vulnerable to supply-chain attacks.

- action.yml: `image: 'docker://ghcr.io/hspaans/latexmk-action:2.1'` — uses a mutable image tag instead of a SHA digest (e.g. `@sha256:<64-hex-char-digest>`)
- dependabot-auto-merge.yml: `uses: dependabot/fetch-metadata@v2`
- docker-image.yml: `uses: actions/checkout@v4`, `uses: docker/setup-qemu-action@v3`, `uses: docker/setup-buildx-action@v3`, `uses: docker/login-action@v3`, `uses: docker/build-push-action@v6`
- hadolint.yml: `uses: actions/checkout@v4`, `uses: github/codeql-action/upload-sarif@v3`

Locations:

- `action.yml:20`
- `.github/workflows/dependabot-auto-merge.yml:22`
- `.github/workflows/docker-image.yml:24`
- `.github/workflows/docker-image.yml:38`
- `.github/workflows/docker-image.yml:41`
- `.github/workflows/docker-image.yml:44`
- `.github/workflows/docker-image.yml:47`
- `.github/workflows/docker-image.yml:53`
- `.github/workflows/hadolint.yml:29`
- `.github/workflows/hadolint.yml:36`

### missing-permissions (severity: medium)

The workflow file `.github/workflows/docker-image.yml` has no top-level `permissions:` key and neither of its jobs (`build-test`, `build-release`) defines a job-level `permissions:` block. Without explicit permissions, the workflow runs with the default (potentially broad) token permissions, violating the principle of least privilege.

Locations:

- `.github/workflows/docker-image.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all unpinned action/image references by replacing mutable tags with full SHA digests: (1) action.yml: pinned ghcr.io/hspaans/latexmk-action:2.1 to sha256:6a184a9675f159b474b4d5001e4ae328686befd19029bf0903f2ad35c07e0f27; (2) dependabot-auto-merge.yml: pinned dependabot/fetch-metadata@v2 to @21025c705c08248db411dc16f3619e6b5f9ea21a; (3) docker-image.yml: pinned actions/checkout@v4, docker/setup-qemu-action@v3, docker/setup-buildx-action@v3, docker/login-action@v3, docker/build-push-action@v6 to their respective full SHAs; (4) hadolint.yml: pinned actions/checkout@v4 and github/codeql-action/upload-sarif@v3 to full SHAs. Added missing permissions to docker-image.yml: top-level 'permissions: contents: read', job-level 'permissions: contents: read' for build-test, and 'permissions: contents: read, packages: write' for build-release (packages: write needed to push to ghcr.io).

