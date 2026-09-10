# State — YYYY-MM-DD

```
DOCUMENT_CLASS = DATED_SNAPSHOT
IS_CANONICAL_TRUTH = NO
LIVE_FACTS_REQUIRE_FRESH_READ = YES
```

A dated photograph of the current state. **Current state only** — a fact that changes
replaces the old line. It never stacks.

**Source marks used in this file:** `command (date)` = machine output ·
`path:line (date)` = read from a file · `URL (date)` = page fetched ·
`person (date)` = someone said it. **No mark means NOT VERIFIED.**

**Size limit: [N] lines.** This is not decoration. A snapshot that grows without
bound stops being read, and a file nobody reads is worse than no file, because it
still looks authoritative. When it goes over, something is in the wrong place —
usually history that belongs in the decision log, or detail that belongs in the
structured owner of that fact.

---

## Where things stand

[One paragraph. The phase, and what is currently being worked on.]

## What is running

[Only what has been observed running, with the command and date that observed it.
Not what should be running.]

## What is decided

[Pointers to the decision log, not restatements of it. `DECISIONS.md`, entry date.]

## Open, not decided

[Questions that are actually open. Distinguish "we chose not to decide yet" from
"nobody has looked" — those are different states and they age differently.]

## Not verified

[The honest list. Things assumed, inherited, or read once in a secondary source and
never confirmed. This section existing is what keeps the rest of the file honest;
a state file with no unverified items is usually a state file that stopped looking.]
