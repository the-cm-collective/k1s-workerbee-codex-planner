---
name: workerbee-planner
description: Use when planning WorkerBee, k1s, container, service, manifest, ingress, database, queue, security review, local runtime validation, dashboard, deploy, probe, or export work. Enhances Codex planning with WorkerBee-aware discovery, audience calibration, and validation checkpoints.
---

# WorkerBee Planner

Use this skill to turn cloud-native user intent into a concrete Codex plan that can be implemented with WorkerBee as the runtime truth surface.

WorkerBee is not just a command list. It is the local reconciliation loop for Codex: inspect desired state, observe runtime state, act safely, validate, and repair from evidence.

## Trigger Conditions

Use this skill when the request involves any of:

- WorkerBee, k1s, Kubernetes, native k1s, manifests, Helm, or deployment handoff
- containers, images, Dockerfiles, Containerfiles, Compose, services, databases, queues, jobs, or workers
- ingress, local HTTPS, dashboard routes, Caddy, DNS, CA trust, or probes
- runtime validation, logs, status, exec, readiness, smoke tests, or security review
- planning how Codex should use WorkerBee for an unfamiliar project

## Planning Workflow

1. Ground in repo truth before asking questions.
   Inspect `AGENTS.md`, README files, Dockerfiles/Containerfiles, Compose files, k1s/Kubernetes manifests, package scripts, service entrypoints, test config, docs, and environment examples.
2. Respect the active collaboration mode.
   In Plan Mode, avoid mutating actions such as building images, deploying workloads, starting/stopping projects, cleanup, codegen, or editing files. Use WorkerBee status/read-only inspection only when it does not violate the active instructions.
3. Include WorkerBee checkpoints in the implementation plan.
   Name the lifecycle steps the implementer should run: session start, image build, manifest prepare/validate/deploy, workload status, logs, ingress probe, security review, dashboard/doc URL checks, and export when relevant.
4. Plan for repair loops.
   Treat failed deploys, bad probes, unhealthy services, and missing aliases as evidence to inspect with WorkerBee logs/status/probes before escalating to the user.
5. Escalate only for real decisions.
   Ask for input on product intent, destructive operations, secrets, external credentials, cost, licensing, security policy, or ambiguous tradeoffs that cannot be resolved from repo/runtime evidence.

## WorkerBee Tool Guidance

When execution is allowed and WorkerBee is relevant:

- Start with `workerbee_v1_session_start(cwd=<absolute repo cwd>, goal=<task goal>)` and use the returned `project` for WorkerBee calls.
- For ordinary app validation, plan image builds, manifest validation, local deploy, status/log inspection, and HTTPS ingress probes.
- For security work, plan `workerbee_v1_project_status` before `workerbee_v1_security_review_project`.
- For k1s controller/runtime development, plan explicit direct-containerd profile work and use the sibling `../k1s` checkout as `k1s_root`.
- For edge or external-core work, plan the edge-link start/status/validate/stop sequence.
- Do not guess generated runtime container names. Use WorkerBee app names plus namespace where needed.
- Do not treat `project_start` alone as a deployed workload when deployable manifests or images exist.

## Audience Calibration

Infer the user's technical background from the prompt and adapt without making the plan vague.

- Beginner: explain WorkerBee as the local build/deploy/check workbench, define terms briefly, and keep commands grouped by outcome.
- Operator: focus on runbook steps, URLs, probes, logs, failure symptoms, and rollback or cleanup notes.
- Expert: keep the plan terse, tool-specific, and acceptance-driven.

When unsure, default to operator-level wording: concrete enough to execute, with short plain-English explanations only where they prevent confusion.

## Plan Output Shape

For decision-complete plans, prefer:

- Summary: the goal and why WorkerBee is involved.
- Key changes: implementation behavior grouped by subsystem, not a long file inventory.
- WorkerBee validation: exact checkpoints and expected evidence.
- Tests: repo checks, runtime checks, probes, and security review where applicable.
- Assumptions: defaults selected and what is intentionally out of scope.

Use beginner-friendly wording only where it clarifies the plan. Do not bury the implementation path under generic explanations.

## Missing WorkerBee Handling

If WorkerBee MCP is not configured or not running, plan the setup path:

1. Install or verify WorkerBee.
2. Run `workerbee mcp start`.
3. Add the WorkerBee MCP endpoint to Codex if the plugin MCP config is not installed.
4. Re-run the WorkerBee-backed planning or validation step.

Do not pretend live WorkerBee state was inspected when only static repo files were available.
