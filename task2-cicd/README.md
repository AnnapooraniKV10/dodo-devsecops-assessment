
## Status (time-boxed)
`secrets-scan` job (gitleaks, allowlisted SealedSecret ciphertext via `.gitleaks.toml`)
passes. `build-scan-sign` job (Docker build → Trivy scan → GHCR push → keyless
Cosign sign) is written but not fully green — failed further into the run than
prior gitleaks-stage failures, indicating a build/push/signing step issue not
diagnosed in the time available. Pipeline design and fail-policy intent (below)
reflect the intended final state regardless of this run's outcome.

Fail policy: gitleaks blocks on any finding (secrets); Trivy blocks on
CRITICAL/HIGH with a fix available; Cosign signs images keyless via GitHub OIDC,
no stored key material.
