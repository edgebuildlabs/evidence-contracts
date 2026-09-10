# Decisions — append-only

**Format.** Each entry is dated in UTC and labeled either `ACCEPTED` (the person with
authority agreed) or `PROPOSED` (not yet agreed, not yet proven). Entries are **never
edited in place** — a correction is a new entry appended below the wrong one, which
stays visible.

**Why append-only.** A record that can be rewritten is a record of what you believe
now, not of what you decided then. The value of a decision log is entirely in being
able to ask "what did we know when we chose this?" — and editing destroys exactly
that.

**What belongs here.** Decisions that would be expensive to re-derive, or that
someone will later assume were made differently. Not routine implementation choices.

---

## TEMPLATE — copy below this line

## YYYY-MM-DD — [short title: the decision, not the topic]

[Two or three sentences: what was decided, and the reasoning that was actually
operative — not a reconstruction that makes it sound smarter than it was.]

**ACCEPTED** — `KEY=VALUE`, scope `NARROW_SCOPE_NAME`.

**Not authorized by this decision:** [the negative space. List what someone might
reasonably assume this covers and does not. This is the part that gets forgotten,
and the reason to write it down is that six weeks from now the assumption will feel
obvious to whoever reads only the first half.]

**Evidence at decision time:** [what was true on the machine at that minute, gathered
immediately before acting — command output, versions, hashes, ports, status. Not
recalled from earlier in the session.]

**Action taken immediately after this record:** [the literal commands or changes.]

---

## EXAMPLE — a real-shaped entry

## 2026-08-30 — Stop and disable the legacy gateway service

The legacy profile has been superseded and is now preserved as rollback history
rather than as a running system. Given that this session runs without a permission
prompt on shell commands, one further plain-language confirmation was requested
before acting, and given.

**ACCEPTED** — `LEGACY_STOP_DISABLE=YES`, scope `STOP_AND_DISABLE_ONLY`.

**Not authorized by this decision:** deleting or cleaning up legacy files, config,
state, auth, containers, workspaces, or evidence; any mutation of the current
profile; restarting legacy; any change beyond this record and the stop/disable
itself. This does not reopen the earlier designation decision.

**Evidence at decision time:** legacy service `active+enabled`, PID 1488478, port
18789, running since 2026-08-29T03:52:00Z. Current service `active+enabled`, PID
1679465, port 19789. This session's own live turn on the current profile is itself
evidence that it does not depend on legacy being up.

**Action taken immediately after this record:** `systemctl --user stop <legacy>`
then `systemctl --user disable <legacy>`. Nothing deleted; nothing under the current
profile touched. Result confirmed with fresh post-action evidence.
