# K1S WorkerBee Codex Planner

Codex plugin package for WorkerBee-aware planning.

This plugin helps Codex turn cloud-native work into decision-complete plans that use WorkerBee as a local runtime truth surface: build, deploy, inspect, probe, review, and export in bounded checkpoints.

## What It Adds

- A `workerbee-planner` skill for Codex planning around WorkerBee, k1s, containers, services, manifests, ingress, databases, queues, security review, and runtime validation.
- A local WorkerBee MCP server entry pointing at `http://127.0.0.1:8765/mcp`.
- A repo-local Codex marketplace snapshot under `.agents/plugins/marketplace.json`.
- Audience-calibrated guidance for beginner, operator, and expert users.

## Layout

```text
.agents/plugins/marketplace.json
plugins/k1s-workerbee-codex-planner/
  .codex-plugin/plugin.json
  .mcp.json
  skills/workerbee-planner/SKILL.md
```

## Prerequisites

Start the WorkerBee MCP daemon before relying on live WorkerBee tools:

```bash
workerbee mcp start
workerbee mcp status
```

The plugin can still provide static planning guidance when WorkerBee is unavailable, but live project status, logs, probes, and deploy validation require the MCP server.

## Install Locally

From this repository root:

```bash
codex plugin marketplace add "$(pwd)"
codex plugin add k1s-workerbee-codex-planner@k1s-workerbee
```

The marketplace name is `k1s-workerbee`.

## Validate

```bash
python3 /home/m4xx3d0ut/.codex/skills/.system/plugin-creator/scripts/validate_plugin.py \
  plugins/k1s-workerbee-codex-planner

python3 -m json.tool .agents/plugins/marketplace.json >/dev/null
python3 -m json.tool plugins/k1s-workerbee-codex-planner/.mcp.json >/dev/null
```

## Usage

Ask Codex to plan WorkerBee-backed work, for example:

```text
Plan how to bring this service up in WorkerBee and validate ingress, logs, and security posture.
```

The planner should inspect repo truth first, adapt detail to the user's technical background, and produce WorkerBee checkpoints that another Codex session can execute directly.

## License

Apache-2.0. See [LICENSE](LICENSE).
