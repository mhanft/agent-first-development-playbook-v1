# Cloud Day-1 Checklist

Run once, at bootstrap, for any cloud-deployed project — before any infrastructure work. Front-loads the gotchas so they're consumed up front instead of chased reactively.

- [ ] Cloud project/account created, billing account linked.
- [ ] **Billing / cost export enabled** — providers don't backfill; enable on Day 1 or permanently lose early cost history.
- [ ] Cost budget + alert thresholds set.
- [ ] In-project spend-surfacing mechanism planned (a cost readout the operator can check on demand).
- [ ] Expected cost ceiling recorded in the architecture doc.
- [ ] Secret storage chosen; secrets populated by the operator via file-based input (never pasted to an agent).
- [ ] IAM / access: least-privilege service identity for the running service; operator admin access confirmed.
- [ ] Deploy path defined (sandbox → prod if used; prod gated by a manual step).
- [ ] Infra-as-code repo initialized — remember: apply-then-PR only for additive infra, destructive changes PR-first.
- [ ] First deploy is a smoke deploy — confirm the pipeline end to end before real work.

This list is a starting point — extend it per provider as gotchas surface.
