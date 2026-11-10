# Decisions

## 2026-11-10

- Created, public, Apache-2.0, as the home of deployment automation for a
  hosted instance (gateway + registry + Redis). Decided by the reviewer
  session under the maintainer's delegation, answering the private
  component-gap analysis.
- Secrets are never in the repository or a chart: files or environment
  under countinghouse's secret-file discipline, sourced from sops or
  Kubernetes Secrets.
- Telemetry is a collector tailing logs, not SDK instrumentation: the
  programs keep writing one log format, and the operator picks the backend.
- Backups: Litestream for sqlite, RDB for Redis, to object storage; a
  restore is a tested procedure, not a document.
- Self-hosting is the default: nothing here may assume the maintainers
  run the instance. A customer runs the same Compose file and the same
  guide, unchanged (the maintainer's decision of 2026-11-10 on the pilot
  scope).
