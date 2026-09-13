# gha-workflows

Reusable GitHub Actions workflows for the `jrackerby/*` custom Home Assistant
integrations, called with `workflow_call`. This repository is public because a
public caller can only use a reusable workflow stored in a public repository
(GitHub's accessibility table for reusable workflows); it carries no secrets.

| file | what it is | called by |
|---|---|---|
| `validate-integration.yml` | `hassfest` (staged layout), generic `tests`, `imports` against the hacs.json core floor, `hacs` (VOID on a private repo) | each integration's `validate.yml` |
| `release-integration.yml` | tag `v<manifest version>` and cut the release, idempotent on the tag | each integration's `release.yml` |

A caller keeps its own triggers and any repo-specific jobs beside the `uses:`
job. Its required contexts are the called job names under the caller job:
`validate / hassfest`, `validate / hacs`, … — `jrackerby/HA`
`tools/hacs_policy_audit.py` reads them in that shape.

Rules for the work are `jrackerby/HA` `tools/work_docs/LAW.md`; the traps
around required contexts and arming a merge are that repo's and
`ha-dashboard-kit`'s `TOOLS.md`. Tracked in jrackerby/HA#821.
