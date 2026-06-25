<!-- markdownlint-disable -->

# Hardening Report: hspaans--latexmk-action/v1.3.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **hspaans--latexmk-action/v1.3.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The action.yml uses a Docker image reference with a mutable tag ':1' instead of a SHA digest. The reference 'docker://ghcr.io/hspaans/latexmk-action:1' can change at any time, making the action vulnerable to supply-chain attacks. It should be pinned to a specific SHA256 digest, e.g. 'docker://ghcr.io/hspaans/latexmk-action@sha256:<64-hex-char-digest>'.

Locations:

- `action.yml:16`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned the Docker image reference in action.yml from 'docker://ghcr.io/hspaans/latexmk-action:1' to 'docker://ghcr.io/hspaans/latexmk-action@sha256:2f207ff4697812da898497a931ce358ffe0e600c66e892584f5d6c9d27dbb137' with the original tag ':1' preserved as a comment.

