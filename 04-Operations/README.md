# 04-Operations

Canonical domain for production-ready LTS operations scripts and standard operating procedures (SOPs).

## Scope

- Safe automation scripts with deterministic execution controls.
- Operational runbooks for incident response and service verification.
- Long-term support patterns for maintainable platform operations.

## LTS Script Targets

- `net-debug`
- `docker-net-audit`

All scripts in this domain must default to safe execution and require explicit `--run` for system-modifying behavior.
