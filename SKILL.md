---
name: change-safeguard
description: "Mandatory pre-change safeguarding checks and post-change side-effect scan: three-tier backup, environment baseline recording, five-point post-change scan."
category: devops
version: 1.0.0
---

# change-safeguard

## Trigger Conditions

This skill is automatically loaded when the task involves:
- Changing configuration, restarting, upgrading, migrating, refactoring, deleting
- Fixing, modifying, adjusting, replacing, installing, uninstalling
- Any operation that may alter system state

## Checklist — Before the Change

- [ ] **Is there a backup?**
  - Server level → cross-machine backup (a copy on the same machine is not a backup)
  - Project level → outside the project directory, or current git commit contains all uncommitted work
  - File level → leave a `.bak` file, or git commit
- [ ] **Has the environment baseline been recorded?**
  - systemd service list (`systemctl list-units --type=service`)
  - Listening ports (`ss -tlnp`)
  - Docker container status
  - Mount points (`mount` / `df -h`)
  - crontab entries
  - Network configuration (`ip addr`, `ip route`)
  - Compare each item after the change — differences are problems

## Checklist — After the Change

- [ ] **Root cause:** Did I treat the symptom or the root cause? Why did the problem occur?
- [ ] **Same-pattern scan:** Are there other places in the system with the same pattern that need adjustment?
- [ ] **Side-effect review:** Did this change inadvertently affect something else?
- [ ] **Newly exposed issues:** Did the adjustment reveal previously hidden problems?
- [ ] **Residual cleanup:** Are old configurations, comments, or rollback paths still present?

## Pitfalls

1. **Do not defer all verification to the final step.** Verify actual functionality (not just exit code 0) after each step.
2. **"It's just a small change" is a trap.** Any change can have cascading effects — small changes still need a baseline record.
3. **Checking only the target is only half the job.** The five-point scan is a necessary part of the closure loop.
