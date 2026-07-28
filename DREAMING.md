# Nightly Co-Founder DREAMING

## Purpose

Turn the local day's verified work into better decisions, stronger memory, more useful metrics, and safer tactics for the existing `GOAL.md`. This is the self-improvement loop, not permission to rewrite the goal, policy, or its own control plane.

DREAMING runs once nightly in one dedicated persistent Dreaming task. It never creates a replacement task, invokes `HEARTBEAT.md`, sends externally, or relies on access to another task's full conversation history.

## Runtime guard and idempotency

1. Read `routines/registry.yaml` and the dreaming checkpoint it names.
2. Proceed only when installation, schedule, fixed Dreaming task, and dreaming are installed and enabled.
3. Verify scheduler and task identity when the installation capability probe confirmed those APIs are available.
4. Build one `occurrence_key` from scheduler ID and local service date.
5. Stop if the occurrence is completed, inside backoff, or already has an active lease.
6. Acquire a bounded lease. Persist stage, attempt, failure, and next retry after partial failure.
7. Complete checkpoint state and release the lease only after durable outputs are verified.

If run manually while the schedule is uninstalled or disabled, use read-only preview mode unless the user explicitly requests applying changes.

## Evidence window

Follow the startup order in `AGENTS.md`, then read durable evidence for the configured local day:

- the canonical action register;
- current goal scorecard and underlying sources;
- bounded active routine view and material monthly log entries;
- second-brain index, operation log, relevant canonical pages, gaps, experiments, and decisions;
- completed outputs, approvals, commitments, failures, objections, and new sources;
- the day's team-meeting minutes and privacy-safe channel evidence.

Task history is optional supporting evidence only when directly available. Durable actions, decisions, metrics, and commitments must remain reconstructable without it.

If core documents are empty, improve onboarding clarity and knowledge hygiene only. Never invent context.

## Reflection loop

### 1. Reconstruct the day

Build a compact evidence-backed chronology:

- what was attempted and why;
- expected versus verified result;
- metric or action-state change;
- material reply, decision, approval, failure, or blocker;
- work that was activity or noise rather than progress.

### 2. Reconcile goal and actions

For `GOAL.md`, report baseline, target, current value, gap, deadline, leading signals, inputs, and guardrails with source, timestamp, and confidence.

Reconcile the action register:

- close only with evidence-of-done;
- merge duplicates;
- preserve attempts;
- set bounded retry/backoff;
- extract commitments scattered in new meeting minutes or outputs;
- identify tomorrow's first eligible high-leverage action.

### 3. Diagnose learning

Identify:

- strongest verified result and likely mechanism;
- largest miss and smallest supported cause;
- current binding constraint;
- assumption strengthened, weakened, or falsified;
- tactic worth reusing;
- recurring quality failure;
- highest-value unresolved knowledge gap.

Separate fact, user statement, inference, hypothesis, recommendation, and decision.

### 4. Improve safely

Unattended DREAMING may update only evidence and derived internal state:

- scorecard observations and metric history;
- action status and retry state;
- second-brain canonical summaries, gaps, indexes, provenance, and archive state;
- daily or weekly summaries;
- internal drafts and tomorrow's proposed experiment.

It may create or refine an operational metric when evidence supports it, but must include definition, owner, cadence, source, baseline, target or guardrail, rationale, and comparability note. It must not change the primary goal's target or deadline.

Changes to `AGENTS.md`, `SOUL.md`, `POLICY.md`, `HEARTBEAT.md`, `DREAMING.md`, team governance, automation configuration, playbook procedures, permissions, or public promises are never applied unattended. Prepare an approval-ready proposal with evidence, expected benefit, exact diff scope, validation plan, and rollback path.

### 5. Compact on schedule

When weekly maintenance is due, run the bounded compaction operation defined by the Second Brain:

- maintain a seven-day active view;
- roll material routine logs monthly;
- consolidate repeated no-op state;
- create a weekly summary with source links;
- extract open actions and commitments before archiving;
- partition meeting indexes;
- archive superseded derived pages without deleting immutable raw evidence.

Compaction must preserve provenance, decisions, metric history, unresolved actions, and recovery links.

## Protected boundaries

DREAMING must never silently:

- change, replace, broaden, close, or redefine the primary goal;
- expand permissions or standing authorization;
- send messages, publish, spend, commit, contact people, or change access;
- delete raw evidence or material history;
- weaken privacy, truthfulness, provenance, approval, or guardrail rules;
- alter its own scheduler, task binding, checkpoint schema, or control instructions.

If such a change appears useful, prepare a proposal for the user.

## Completion

Produce and persist:

- service date and timezone;
- goal and scorecard delta;
- action-register reconciliation;
- what worked, failed, and why;
- assumptions changed;
- binding constraint;
- ranked gaps and at most one proposed user question;
- safe internal improvements applied;
- control-plane proposals awaiting approval;
- tomorrow's first highest-leverage action;
- weekly compaction result when due.

Append a material nightly entry to the current monthly routine log. If no evidence warranted a change, complete quietly, update only the checkpoint, and preserve stability.

Before releasing the lease, verify every write, mark the occurrence completed, and record retry state for any unfinished stage.
