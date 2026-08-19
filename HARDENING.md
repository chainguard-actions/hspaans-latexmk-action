<!-- markdownlint-disable -->

# Hardening Report: hspaans--latexmk-action/v2.1.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **hspaans--latexmk-action/v2.1.1** was hardened automatically. 5 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

action.yml references a Docker image using a mutable tag ('docker://ghcr.io/hspaans/latexmk-action:2.1') instead of an immutable SHA digest. This is vulnerable to supply-chain attacks if the tag is moved.

Locations:

- `action.yml:21`

### unpinned-uses (severity: high)

docker-image.yml uses multiple action references pinned to mutable tags instead of full 40-character commit SHAs: actions/checkout@v4 (two occurrences), docker/setup-qemu-action@v3, docker/setup-buildx-action@v3, docker/login-action@v3, docker/build-push-action@v6.

Locations:

- `.github/workflows/docker-image.yml:22`
- `.github/workflows/docker-image.yml:34`
- `.github/workflows/docker-image.yml:37`
- `.github/workflows/docker-image.yml:40`
- `.github/workflows/docker-image.yml:43`
- `.github/workflows/docker-image.yml:48`

### unpinned-uses (severity: high)

dependabot-auto-merge.yml uses 'dependabot/fetch-metadata@v2', a mutable tag reference instead of a full 40-character commit SHA.

Locations:

- `.github/workflows/dependabot-auto-merge.yml:20`

### unpinned-uses (severity: high)

hadolint.yml uses 'actions/checkout@v4' and 'github/codeql-action/upload-sarif@v3', both mutable tag references instead of full 40-character commit SHAs. (hadolint/hadolint-action is correctly pinned to a SHA.)

Locations:

- `.github/workflows/hadolint.yml:28`
- `.github/workflows/hadolint.yml:38`

### missing-permissions (severity: medium)

docker-image.yml has no top-level 'permissions:' key and neither of its jobs (build-test, build-release) defines a job-level 'permissions:' block. This means the workflow runs with the default, overly broad token permissions.

Locations:

- `.github/workflows/docker-image.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all findings:
1. action.yml: Pinned docker://ghcr.io/hspaans/latexmk-action:2.1 to @sha256:6a184a9675f159b474b4d5001e4ae328686befd19029bf0903f2ad35c07e0f27, preserving the docker:// scheme and tag inline.
2. docker-image.yml: Pinned all 6 mutable action tags to full commit SHAs (actions/checkout@11d5960..., docker/setup-qemu-action@c7c534..., docker/setup-buildx-action@8d2750..., docker/login-action@c94ce9..., docker/build-push-action@10e90e...). Added top-level permissions: {contents: read} and job-level permissions (build-test: contents:read; build-release: contents:read + packages:write).
3. dependabot-auto-merge.yml: Pinned dependabot/fetch-metadata@v2 to @21025c705c08248db411dc16f3619e6b5f9ea21a.
4. hadolint.yml: Pinned actions/checkout@v4 to @11d5960... and github/codeql-action/upload-sarif@v3 to @4187e74...

