# countinghouse-deploy

How a hosted countinghouse instance is deployed, backed up and watched:
the gateway ([countinghouse](https://github.com/mchen6/countinghouse)),
the registry ([countinghouse-registry](https://github.com/mchen6/countinghouse-registry))
and Redis, as one unit an operator can stand up, upgrade and restore.
The same files serve whoever runs the instance: the maintainers for a
pilot, or an operator in their own environment, unchanged.

Status: scope only (2026-11-10). Nothing here runs yet.

## Scope

- **A one-command Compose install** for a single host, with a guide
  that gets from nothing to a first tool call in fifteen minutes, and
  later a **Helm chart** for Kubernetes,
  following the posture in countinghouse's `docs/deployment.md` and the
  Kubernetes mapping in its multi-language modules note.
- **Backups and restore**: the registry's sqlite file through Litestream,
  Redis RDB snapshots, both to object storage; a restore runbook that is
  exercised by a test.
- **Secrets**: files with the discipline countinghouse already enforces
  (mode 0600, no symlinks, environment variable as the alternative), fed
  from sops or Kubernetes Secrets. Never values in a chart.
- **Telemetry**: an OpenTelemetry Collector tailing the JSON-lines logs
  both programs write (the countinghouse logger record), exporting to the
  operator's backend. No SDK instrumentation inside the programs.
- **Smoke tests**: start the unit, publish a fixture module, enable a
  fixture remote entry, call a tool through the gateway, read the usage
  record, tear down.
- **Runbooks**: upgrade, rotate secrets, restore, rotate an instance key.

## Not in scope

- Customer-specific configuration, domains or credentials.
- A status page (a hosted service), an authorization server (brought by
  the operator), payments.
- Running third-party package entries in containers: that is a separate
  program, planned as `countinghouse-host`.

## Licence

Apache-2.0.
