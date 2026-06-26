<!-- markdownlint-disable -->

# Hardening Report: hspaans--latexmk-action/v2.1.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **hspaans--latexmk-action/v2.1.1** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The action.yml uses a Docker image reference with a mutable tag ('docker://ghcr.io/hspaans/latexmk-action:2.1') instead of an immutable SHA digest. A tag can be silently overwritten to point to a different (potentially malicious) image, enabling supply-chain attacks. The image reference should use a SHA256 digest, e.g. 'docker://ghcr.io/hspaans/latexmk-action@sha256:<64-hex-char-digest>'.

Locations:

- `action.yml:21`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Replaced the mutable Docker image tag 'ghcr.io/hspaans/latexmk-action:2.1' with the immutable SHA256 digest 'ghcr.io/hspaans/latexmk-action@sha256:6a184a9675f159b474b4d5001e4ae328686befd19029bf0903f2ad35c07e0f27' in action.yml line 21. The original tag '2.1' is preserved as a comment for readability.

