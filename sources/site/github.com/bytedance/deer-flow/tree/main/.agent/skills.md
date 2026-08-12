# Source: https://github.com/bytedance/deer-flow/tree/main/.agent/skills

### Uh oh!

There was an error while loading. [Please reload this page]().

[bytedance](https://github.com/bytedance) / **[deer-flow](https://github.com/bytedance/deer-flow)** Public

- [Notifications](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow) You must be signed in to change notification settings
- [Fork 10.9k](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow)
- [Star 79.8k](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow)

 ## FilesExpand file tree

main

/

# skills

/

Copy path

## Directory actions

## More options

More options

## Directory actions

## More options

More options

## Latest commit

[![ShenAC-SAC](https://avatars.githubusercontent.com/u/142667174?v=4&size=40)](https://github.com/ShenAC-SAC) [ShenAC-SAC](https://github.com/bytedance/deer-flow/commits?author=ShenAC-SAC)

[feat(skill): add first-principles system change workflow (](https://github.com/bytedance/deer-flow/commit/2af2fb504db6705ceebc9dc278bce9aebfb10b4a) [#4398](https://github.com/bytedance/deer-flow/pull/4398) [)](https://github.com/bytedance/deer-flow/commit/2af2fb504db6705ceebc9dc278bce9aebfb10b4a)

Open commit detailssuccess

Jul 23, 2026

[2af2fb5](https://github.com/bytedance/deer-flow/commit/2af2fb504db6705ceebc9dc278bce9aebfb10b4a) · Jul 23, 2026

## History

[History](https://github.com/bytedance/deer-flow/commits/main/.agent/skills)

Open commit details

History

## FilesExpand file tree

main

/

# skills

/

Copy path

Top

## Folders and files

| Name | Name | 
Last commit message

 | 

Last commit date

 |
| --- | --- | --- | --- |
| 

### parent directory

[..](https://github.com/bytedance/deer-flow/tree/main/.agent) |
| 

[blocking-io-guard](https://github.com/bytedance/deer-flow/tree/main/.agent/skills/blocking-io-guard 'blocking-io-guard')

 | 

[blocking-io-guard](https://github.com/bytedance/deer-flow/tree/main/.agent/skills/blocking-io-guard 'blocking-io-guard')

 | 

[feat(skill): add blocking-io-guard — SOP skill for blocking-IO triage…](https://github.com/bytedance/deer-flow/commit/dc2ababf0041a768e2ad3c0a432ff902cd8a8e88 'feat(skill): add blocking-io-guard — SOP skill for blocking-IO triage and runtime anchors (#3503)

* feat(blocking-io): add changed-lines blocking-IO scanner (L1)

* feat(blocking-io): add scan-changed CLI wrapper

* feat(skill): add blocking-io-guard developer SOP skill

* docs(blocking-io): point contributors at the blocking-io-guard skill

* style(blocking-io): apply ruff format to scanner and tests

* docs(backend): document changed-lines blocking-IO scanner in CLAUDE.md

* feat(skill): add post-fix re-scan check and PR batching policy

* refactor(skill): fix SOP step ordering, align template with repo conventions

- Move re-scan into an explicit 'apply the fix' step (was wedged after
 anchor generation while telling you to go back before the anchor)
- Renumber steps 0-6; drop undefined 'L1' jargon
- Mode A: document that the diff is <base>...HEAD (commit first)
- Mode B: prefer make detect-blocking-io + findings JSON file
- anchor template: module-level pytestmark per tests/blocking_io convention
- CLAUDE.md: fix 'git diff --base' phrasing

* fix(skill): catch findings introduced without touching the blocking line

Review follow-up: changed-line intersection alone misses the case where a
new async caller exposes an old sync helper — the static finding sits on
the untouched blocking line, so Mode A returned empty and the SOP stopped
on a false 'no blocking-IO surface'.

Selection is now a union over the changed files:
- findings on added lines of git diff <base>...HEAD (kept: a second
 identical symbol in an already-flagged function collides on the stable
 key and only this selection sees it);
- findings new versus the merge base, matched by (path, function,
 symbol) — never line numbers.

Base sources are materialized via git show <merge-base>:<path>; files
absent at base count every head finding as new. SKILL.md now states the
residual same-file-only blind spot (cross-file async callers) instead of
treating an empty list as proof of zero exposure, and only requires
reading sop-skeleton.md when generalizing to another detector domain.

* docs(skill): examples teach test-writing, the teeth check defines the rule

All examples in the references/template are filesystem-flavored; make
explicit that they are instances, not the SOP's boundary — the same rules
apply to every detector category (FILE_IO, HTTP, SUBPROCESS, SLEEP) and
acceptance is always red/green teeth, never similarity to an example.
Neutralize the template's arrange comment accordingly.

* fix(blocking-io): harden changed-lines scanner per review

- Dedup the union selection by the stable key (path, function, symbol)
 instead of dict identity, so a future selector returning copied dicts
 cannot silently empty the result.
- parse_changed_lines now handles any unified diff: context lines advance
 the new-file counter, \-markers and deletions do not, and the counter
 resets at each +++ header. Previously correct only for --unified=0.
- Add blocking_io_static.scan_source (in-memory scan); base-version
 comparison no longer round-trips through temp files.
- Empty Mode A report now prints the same-file-only reachability caveat
 at the point of use instead of relying on the SOP text alone.

* docs(skill): bound best-effort cleanup when the offload sits in finally

Lesson from the #3505 review: the SOP routinely drives 'offload the
cleanup branch' transformations, and an awaited cleanup in finally can
mask or stall the primary exception. One sentence in Step 2 closes that
gap at the point where the fix is written.')

 | 

Jun 12, 2026

 |
| 

[deerflow-maintainer-orchestrator](https://github.com/bytedance/deer-flow/tree/main/.agent/skills/deerflow-maintainer-orchestrator 'deerflow-maintainer-orchestrator')

 | 

[deerflow-maintainer-orchestrator](https://github.com/bytedance/deer-flow/tree/main/.agent/skills/deerflow-maintainer-orchestrator 'deerflow-maintainer-orchestrator')

 | 

[feat(skill): strengthen maintainer orchestrator review workflow (](https://github.com/bytedance/deer-flow/commit/65fab1d4d41b1e7c732254422ba3f9c12dc900d2 'feat(skill): strengthen maintainer orchestrator review workflow (#3606)

* feat(skill): strengthen maintainer orchestrator review workflow

Add seven enhancements to the deerflow-maintainer-orchestrator skill and
mirror them in docs/agents/maintainer-sop.md:

- Posting gate as confidence x severity, with a maintainer-only notes
 channel for sub-threshold observations. Clarifies that "no high-confidence
 findings" spans P0/P1/P2, not just P0.
- Batch handling: cluster by relatedness, then synthesize cross-PR overlap,
 merge-order/conflict surface, and composition risk.
- Competing PR comparison anchored to the issue's acceptance criteria, with a
 maintainer-only ranking and a constructive per-PR public surface.
- Existing comments suppress duplicate posting, not analysis: review fully and
 post only the net-new delta, with an idempotency guard for re-runs.
- Green-CI discipline: checks are signal not verdict; read the changed code
 path regardless of a green rollup.
- Fork PR head resolution via pull/<n>/head and a pre-post head-SHA recheck.
- Competing-PR detection in artifact resolution; output gains Already
 covered / Maintainer notes / Batch synthesis fields.

* docs(skill): rewrite maintainer SOP as design rationale, not a skill restatement

* docs(skill): rename maintainer SOP doc to maintainer-orchestrator-design

* feat(skill): allow controlled fan-out when a related cluster exceeds one context

---------

Co-authored-by: Willem Jiang <willem.jiang@gmail.com>') [#3606](https://github.com/bytedance/deer-flow/pull/3606) [)](https://github.com/bytedance/deer-flow/commit/65fab1d4d41b1e7c732254422ba3f9c12dc900d2 'feat(skill): strengthen maintainer orchestrator review workflow (#3606)

* feat(skill): strengthen maintainer orchestrator review workflow

Add seven enhancements to the deerflow-maintainer-orchestrator skill and
mirror them in docs/agents/maintainer-sop.md:

- Posting gate as confidence x severity, with a maintainer-only notes
 channel for sub-threshold observations. Clarifies that "no high-confidence
 findings" spans P0/P1/P2, not just P0.
- Batch handling: cluster by relatedness, then synthesize cross-PR overlap,
 merge-order/conflict surface, and composition risk.
- Competing PR comparison anchored to the issue's acceptance criteria, with a
 maintainer-only ranking and a constructive per-PR public surface.
- Existing comments suppress duplicate posting, not analysis: review fully and
 post only the net-new delta, with an idempotency guard for re-runs.
- Green-CI discipline: checks are signal not verdict; read the changed code
 path regardless of a green rollup.
- Fork PR head resolution via pull/<n>/head and a pre-post head-SHA recheck.
- Competing-PR detection in artifact resolution; output gains Already
 covered / Maintainer notes / Batch synthesis fields.

* docs(skill): rewrite maintainer SOP as design rationale, not a skill restatement

* docs(skill): rename maintainer SOP doc to maintainer-orchestrator-design

* feat(skill): allow controlled fan-out when a related cluster exceeds one context

---------

Co-authored-by: Willem Jiang <willem.jiang@gmail.com>')

 | 

Jun 16, 2026

 |
| 

[engineer-system-change](https://github.com/bytedance/deer-flow/tree/main/.agent/skills/engineer-system-change 'engineer-system-change')

 | 

[engineer-system-change](https://github.com/bytedance/deer-flow/tree/main/.agent/skills/engineer-system-change 'engineer-system-change')

 | 

[feat(skill): add first-principles system change workflow (](https://github.com/bytedance/deer-flow/commit/2af2fb504db6705ceebc9dc278bce9aebfb10b4a 'feat(skill): add first-principles system change workflow (#4398)

* feat(skill): add first-principles system change workflow

* docs(skill): clarify verification and verdict mapping') [#4398](https://github.com/bytedance/deer-flow/pull/4398) [)](https://github.com/bytedance/deer-flow/commit/2af2fb504db6705ceebc9dc278bce9aebfb10b4a 'feat(skill): add first-principles system change workflow (#4398)

* feat(skill): add first-principles system change workflow

* docs(skill): clarify verification and verdict mapping')

 | 

Jul 23, 2026

 |
| 

[smoke-test](https://github.com/bytedance/deer-flow/tree/main/.agent/skills/smoke-test 'smoke-test')

 | 

[smoke-test](https://github.com/bytedance/deer-flow/tree/main/.agent/skills/smoke-test 'smoke-test')

 | 

[fix(skills):Update the smock-test skill to use make up in docker mode (](https://github.com/bytedance/deer-flow/commit/525ec0a00d89b8161c8137a91e9ac18ff5baf9be 'fix(skills):Update the smock-test skill to use make up in docker mode (#3656)') […](https://github.com/bytedance/deer-flow/pull/3656)

 | 

Jun 19, 2026

 |
| 

View all files

 |