# Evidence Contracts

**Drop-in contract files that make a coding agent prove its work instead of claiming it.**

Copy one file into your repository. Your agent stops saying "done" and starts saying
what it ran, when, and what came back.

The method, the reasoning behind it, and the server it was tested on:
**[edgebuildlabs.github.io](https://edgebuildlabs.github.io/)** (also in
[Português](https://edgebuildlabs.github.io/pt/) and [Español](https://edgebuildlabs.github.io/es/)).
The brand site, for hiring: [edgebuildlabs.tech](https://edgebuildlabs.tech/) (PT, EN).

---

## The problem

Your agent reports success. The tests never ran. The file was never written. The
service is not up. The claim was generated from context, not from the machine.

This is the dominant failure mode of agentic coding in 2026, and it is not a model
defect you can prompt away with "be accurate." It is a missing contract. Nothing in
the loop ever required the agent to distinguish *what it observed* from *what it
inferred* — so it doesn't, and the two arrive in the same confident sentence.

Exit code `0` proves a command returned. It does not prove the mission succeeded.

## The rule that does most of the work

> **Every claim of state carries a source and a date — or the words NOT VERIFIED.**

A claim of state is any sentence asserting that something **is** or **was** the case:
the test passed, the file exists, the service is running, the API returns 200. The mark
travels attached to the claim:

- `src/auth.ts:42 (2026-09-10)` — read from a file
- `pytest -q (now)` — output of a command run this turn
- `https://example.com/docs (2026-09-10)` — a page fetched
- **NOT VERIFIED** — with half a line saying why

Opinion, recommendation and reasoning carry nothing. They are visibly not facts.

That is the whole trick. It sounds trivial. It is not: it forces the agent to *notice*
the difference between memory and observation at the moment of writing, which is the
only moment where noticing changes anything.

## The ladder

```
STARTED  !=  COMPLETED  !=  VALIDATED  !=  PASS
```

A live process, an exit code of zero, and the word "done" are all upstream of PASS.
A receipt that contradicts an error, a zero-usage metric, or a missing artifact is not
a PASS — it is an unfinished investigation.

**Tests passing is not validation.** It is evidence that the code does what the test
says, which is a different and much smaller claim than the one usually made from it.

## Classify before blaming the model

When something fails, the model is the *last* hypothesis, not the first. Name the layer
before assigning cause:

`auth` · `quota` · `transport` · `wrong shell` · `harness` · `path` · `permission` ·
`sandbox` · `tool` · `orchestration` · `model` · `product`

Most "the model is dumb today" incidents are an expired token, a rate limit, a command
running in a shell that isn't the one you think, or a path that doesn't exist in the
sandbox. Checking that list first costs thirty seconds and resolves the majority.

---

## What's in here

| File | What it is |
|---|---|
| [`AGENTS.md`](AGENTS.md) | The contract. Copy it into your repo root — as `AGENTS.md`, `CLAUDE.md`, `.cursorrules`, or whatever your tool reads. |
| [`DECISIONS.md`](DECISIONS.md) | An append-only decision ledger, with a worked example. |
| [`STATE.md`](STATE.md) | A dated snapshot file that is allowed to be wrong only in one direction. |

Three files to copy, plus this README and a public-domain licence. No dependencies,
no install. It is a contract, not a framework.

## Quickstart

```bash
curl -O https://raw.githubusercontent.com/edgebuildlabs/evidence-contracts/main/AGENTS.md
```

Then open it and delete what doesn't apply to you. Every section is independent —
the source-and-date rule alone is worth the copy, and it is the first section for
exactly that reason.

If your tool reads a differently-named file, rename it. The filename is the least
important part.

---

## Why these particular rules

They were not designed at a whiteboard. They are what was left after running a
multi-agent system in production and repeatedly discovering that a confident report
and a true report look identical until you demand the receipt.

Each one exists because something specific went wrong without it:

**Append-only decisions, never edited in place.** A decision record that can be
rewritten is a record of your current beliefs, not of what you decided. Corrections
append; the wrong entry stays visible with the right one after it.

**Admission state.** A capability is `PROPOSED` until it has run, and then it is
`RUNTIME_PROVEN` with a pointer to the evidence that proved it. Nothing is counted
because it looks like it should work.

**One fact, one owner.** Exactly one place holds each canonical fact. No parallel
`CURRENT/`, `LATEST/`, `CANDIDATE/` hierarchies for the same thing — those always
diverge, and then no one knows which is true.

**Documents declare their own class.** A file that is derived navigation says so at
the top, and says that live facts require a fresh read. A map that doesn't admit it's
a map gets treated as the territory.

**Prose rots.** Never restate a volatile value in prose. Point at the structured owner
of that fact instead. A literal copied into a paragraph is correct exactly until the
next change, and then it is a lie with good grammar.

**Fresh evidence immediately before acting.** Not evidence from earlier in the session
— evidence from this minute, recorded next to the action it justified.

**Narrow authorization, with the negative space written down.** An authorization says
what is permitted *and* lists what is explicitly not permitted by it. The list of what
you didn't authorize is the part that gets forgotten.

## Where this came from

These contracts run a real system: a multi-agent orchestration layer on a single VPS,
and a game server built under it — rootless Podman, systemd Quadlet as the single
recreation path, `--read-only`, `--cap-drop=all`, `--security-opt=no-new-privileges`,
non-root user namespace, image pinned by digest rather than tag, daily backup with a
proven restore.

The owner of that system wrote none of that configuration. The entire contribution was
asking *"did you verify that, or are you inferring it?"* until only the verified part
was left.

That is what these files automate.

## License

CC0 1.0 — public domain. Copy it, change it, ship it, don't credit anyone. If it
saves you one wrong "done", it paid for itself.
