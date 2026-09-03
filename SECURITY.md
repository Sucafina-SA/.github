# Security

## Reporting

Do not open a public issue for a security problem. Contact the research
engineering lead directly.

## Secrets

`gitleaks` runs as a pre-commit hook in every repo. If it fires:

| Case | Action |
| --- | --- |
| A real secret | **Rotate it immediately.** Removing the commit is not enough — assume it is compromised the moment it is pushed. Then move it to `.env` (gitignored) or a secret manager. |
| False positive, one line | `# gitleaks:allow` on that line |
| False positive, a whole file | Add an `exclude` pattern in `.pre-commit-config.yaml`, as is already done for `uv.lock` — its SHA256 hashes read as high-entropy tokens |

Never `--no-verify` past a gitleaks finding.

`.env.example` documents variable **names** only. A real value in that file is
the same incident as a real value in the code.

## Data

Repos in this org read licensed market data. Never commit a data file, and never
attach an upstream store read-write from a downstream repo — if a number
upstream is wrong it is fixed upstream, with a test.
