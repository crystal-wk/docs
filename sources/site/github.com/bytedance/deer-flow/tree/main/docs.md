# Source: https://github.com/bytedance/deer-flow/tree/main/docs

### Uh oh!

There was an error while loading. [Please reload this page]().

[bytedance](https://github.com/bytedance) / **[deer-flow](https://github.com/bytedance/deer-flow)** Public

- [Notifications](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow) You must be signed in to change notification settings
- [Fork 10.9k](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow)
- [Star 79.8k](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow)

 ## FilesExpand file tree

main

/

# docs

/

Copy path

## Directory actions

## More options

More options

## Directory actions

## More options

More options

## Latest commit

[![ehz0ah](https://avatars.githubusercontent.com/u/130889443?v=4&size=40)](https://github.com/ehz0ah) [ehz0ah](https://github.com/bytedance/deer-flow/commits?author=ehz0ah)

[refactor(memory): use official OpenViking adapter (](https://github.com/bytedance/deer-flow/commit/6556d09d7f3800ca570820819455c39b4584482f) [#4707](https://github.com/bytedance/deer-flow/pull/4707) [)](https://github.com/bytedance/deer-flow/commit/6556d09d7f3800ca570820819455c39b4584482f)

Open commit detailssuccess

Aug 7, 2026

[6556d09](https://github.com/bytedance/deer-flow/commit/6556d09d7f3800ca570820819455c39b4584482f) · Aug 7, 2026

## History

[History](https://github.com/bytedance/deer-flow/commits/main/docs)

Open commit details

History

## FilesExpand file tree

main

/

# docs

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

[..](https://github.com/bytedance/deer-flow/tree/main) |
| 

[agents](https://github.com/bytedance/deer-flow/tree/main/docs/agents 'agents')

 | 

[agents](https://github.com/bytedance/deer-flow/tree/main/docs/agents 'agents')

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

[plans](https://github.com/bytedance/deer-flow/tree/main/docs/plans 'plans')

 | 

[plans](https://github.com/bytedance/deer-flow/tree/main/docs/plans 'plans')

 | 

[feat(authz): enforce model authorization at Gateway routes and runtime (](https://github.com/bytedance/deer-flow/commit/540940bac18b99cf5bf0a9db67a4dc4c3881584f 'feat(authz): enforce model authorization at Gateway routes and runtime (#4063 Phase 3) (#4540)

* feat(authz): enforce model authorization at Gateway routes and runtime (#4063 Phase 3)

Phase 3 / Models — the first of three resource-type PRs (Models, Skills,
Sandbox). The RBAC provider already maps "model" → config key "models"
(rbac.py _RESOURCE_POLICY_KEYS), so no schema change is needed.

Gateway route layer (mirrors Phase 2A):
- resolve_model_authorization() in authz.py returns (provider, principal),
 reusing _get_cached_route_provider and build_principal_from_context,
 including the INTERNAL_SYSTEM_ROLE → None pop for internal callers.
- list_models filters via provider.filter_resources(principal, "model", names).
- get_model checks provider.authorize("model", "use"). Deny → 403 (not 404,
 since the model exists but the role lacks permission).

Runtime resolution layer (mirrors Phase 1B):
- _authorize_model_name() in agent.py runs after _resolve_model_name. On deny,
 falls back to the first allowed model (RFC §9: graceful, not crash). All
 models denied + fail_closed → ValueError (matches existing contract).

authorization.enabled: false is a complete no-op on both layers. Anonymous
requests (user=None) bypass filtering. 18 new tests + 314 existing tests pass.

* fix(authz): enforce model:use on the embedded DeerFlowClient path (Phase 3 follow-up)

Round 4 review (willem-bd): _authorize_model_name only covered the Gateway
runtime path (_make_lead_agent). The parallel lead-agent construction path
DeerFlowClient._ensure_agent (client.py) filtered tools but not the model,
so a library/embedded consumer with role-scoped model policies could run a
model the role is denied model:use for.

- Insert _authorize_model_name in _ensure_agent, mirroring _make_lead_agent.
- Resolve None default to the first configured model before the gate so the
 implicit default (create_chat_model(name=None)) is also authorized.
- Update test_authorization_filters_framework_tools_and_reuses_provider: the
 stub provider now returns an allow decision for model:use (checked during
 assembly) and patches resolve_authorization_provider in the agent namespace.
- Add 3 DeerFlowClient._ensure_agent path tests (real-path fallback,
 None-default resolution, disabled no-op); 24 tests total.

* docs(authz): document get_model provider-unavailable fail-open path + test

zhfeng review (round 5): get_model's docstring only mentioned the deny→403
path, not the provider-resolution-error + fail-open path (which allows the
request, mirroring list_models's documented fail-open semantics). The
behavior itself is correct and symmetric with list_models, but it was
undocumented and the _AuthorizationUnavailable path had no test coverage.

- Extend get_model docstring to state the provider-error fail-closed/fail-open
 outcome, matching list_models's wording.
- Add test_get_model_provider_unavailable_fail_closed_vs_open exercising the
 _AuthorizationUnavailable path (provider cannot be resolved at all), pinning
 fail-closed→403 / fail-open→200.

---------

Co-authored-by: Willem Jiang <willem.jiang@gmail.com>')

 | 

Aug 1, 2026

 |
| 

[pr-evidence](https://github.com/bytedance/deer-flow/tree/main/docs/pr-evidence 'pr-evidence')

 | 

[pr-evidence](https://github.com/bytedance/deer-flow/tree/main/docs/pr-evidence 'pr-evidence')

 | 

[Implement skill self-evolution and skill\_manage flow (](https://github.com/bytedance/deer-flow/commit/888f7bfb9d1d2eb4570d51aec4dfe62ddac15e05 'Implement skill self-evolution and skill_manage flow (#1874)

* chore: ignore .worktrees directory

* Add skill_manage self-evolution flow

* Fix CI regressions for skill_manage

* Address PR review feedback for skill evolution

* fix(skill-evolution): preserve history on delete

* fix(skill-evolution): tighten scanner fallbacks

* docs: add skill_manage e2e evidence screenshot

* fix(skill-manage): avoid blocking fs ops in session runtime

---------

Co-authored-by: Willem Jiang <willem.jiang@gmail.com>') [#1874](https://github.com/bytedance/deer-flow/pull/1874) [)](https://github.com/bytedance/deer-flow/commit/888f7bfb9d1d2eb4570d51aec4dfe62ddac15e05 'Implement skill self-evolution and skill_manage flow (#1874)

* chore: ignore .worktrees directory

* Add skill_manage self-evolution flow

* Fix CI regressions for skill_manage

* Address PR review feedback for skill evolution

* fix(skill-evolution): preserve history on delete

* fix(skill-evolution): tighten scanner fallbacks

* docs: add skill_manage e2e evidence screenshot

* fix(skill-manage): avoid blocking fs ops in session runtime

---------

Co-authored-by: Willem Jiang <willem.jiang@gmail.com>')

 | 

Apr 6, 2026

 |
| 

[superpowers](https://github.com/bytedance/deer-flow/tree/main/docs/superpowers 'superpowers')

 | 

[superpowers](https://github.com/bytedance/deer-flow/tree/main/docs/superpowers 'superpowers')

 | 

[perf(frontend): bound delivery, bundles, and long-running UI work (](https://github.com/bytedance/deer-flow/commit/459dd78707c7082662b49a4728e95d52d631d26a 'perf(frontend): bound delivery, bundles, and long-running UI work (#4622)

* docs: design frontend performance remediation

* docs: plan frontend performance remediation

* test(frontend): add route asset performance budgets

* perf(nginx): compress textual responses safely

* perf(frontend): lazy load case study media

* perf(frontend): bound static demo file tracing

* perf(frontend): restore static locale boundaries

* perf(frontend): defer closed workspace panels

* perf(frontend): split editors and deduplicate highlighting

* perf(frontend): index incremental message derivation

* perf(frontend): stabilize paged history cache policy

* perf(frontend): bound streaming markdown renders

* perf(frontend): virtualize message history

* perf(frontend): bound and virtualize chat lists

* perf(frontend): suspend inactive decorative animation

* perf(browser): stream latest frames as binary

* perf(artifacts): stream bounded text previews

* docs: finalize performance runtime boundaries

* style(backend): apply test formatting

* fix(frontend): keep translation functions client-side

* perf(frontend): defer decorative animation bundles

* test(frontend): lock optimized route budgets

* fix: harden frontend performance boundaries

* test(frontend): update i18n provider fixture

* fix(frontend): preserve sidebar pagination position

* style(backend): format artifact range test') [#4622](https://github.com/bytedance/deer-flow/pull/4622)

 | 

Aug 1, 2026

 |
| 

[tui](https://github.com/bytedance/deer-flow/tree/main/docs/tui 'tui')

 | 

[tui](https://github.com/bytedance/deer-flow/tree/main/docs/tui 'tui')

 | 

[feat(tui): Hermes-like terminal workbench (`deerflow`) backed by Deer…](https://github.com/bytedance/deer-flow/commit/ef5f54c5bf3657f89445ba23c7d5785b8df5e648 'feat(tui): Hermes-like terminal workbench (`deerflow`) backed by DeerFlowClient (#3760)

* feat(tui): add Hermes-like terminal workbench backed by DeerFlowClient

Implements the `deerflow` TUI from RFC #3540: a terminal-native, embedded
workbench over the existing harness (no Gateway/frontend/nginx/Docker), built
Python-native with Textual and learning UX patterns from tao-pi.

Architecture — every layer except the Textual app is pure and unit-tested:
- view_state.py: ViewState + reduce(state, action), the testable heart
- runtime.py: StreamEvent -> reducer actions (pure translate + threaded driver)
- message_format / command_registry / input_history / render / theme: pure
- app.py: Textual App; runs the sync DeerFlowClient.stream() on a worker thread
 and marshals actions back to the UI thread. Slash command palette, model and
 thread modal pickers, ↑/↓ history, Ctrl+C interrupt, TTY-aware fallback.
- cli.py: pure launch-mode planning + headless --print/--json + `deerflow`
 console script (textual is an optional [tui] extra; degrades to headless help)

Web UI visibility (the RFC's key decision): persistence.py writes a threads_meta
row under the local default user into the same DB the Gateway reads, so terminal
sessions appear in the Web UI sidebar without running the Gateway. Best-effort,
no-op on the memory backend; all DB work on one long-lived background loop.

Tests: 95 TUI tests — pure layers via pytest, app/palette/overlays via Textual's
pilot harness with a fake session, and a threads_meta read/write round-trip.
ruff clean; respects the harness->app import boundary. Docs: backend/docs/TUI.md
plus CLAUDE.md/README updates and preview screenshots.

Co-Authored-By: Claude Opus 4.8 <noreply@anthropic.com>

* fix(tui): de-duplicate streamed assistant text and tool cards; keep Tab in composer

Self-test surfaced three issues, all root-caused to consuming non-strict
streaming from DeerFlowClient (proven by the client's own
test_dedup_requires_messages_before_values_invariant, which shows the client can
re-emit a message id's full content twice):

- Assistant text was doubled (e.g. "answer answer") because the reducer blindly
 concatenated same-id deltas. Now merges by content: a re-send or cumulative
 snapshot replaces; only genuine increments append.
- Tool activity showed duplicate and empty "gear" cards from partial/re-emitted
 tool-call chunks. ToolStarted now de-dupes by tool_call_id, drops id-less
 noise chunks, and fills the name on a later chunk; a tool result with no prior
 card still surfaces as a completed card.
- Tab moved focus off the composer to the scroll region (felt like broken cursor
 logic). Tab is now consumed by the composer (completes a command when the
 palette is open, no-op otherwise).

Adds reducer tests for each case plus a Tab-focus test; 102 TUI tests pass.

Co-Authored-By: Claude Opus 4.8 <noreply@anthropic.com>

* fix(tui): make Esc interrupt an active run (matches the status hint)

The status line advertised "esc interrupt" but Esc was only wired to close the
slash palette, so it did nothing during a run. Esc now: closes the palette when
open, interrupts the active run when streaming, and is a no-op when idle. The
interrupt logic is shared with Ctrl+C via _interrupt_run(). Adds a regression
test.

Co-Authored-By: Claude Opus 4.8 <noreply@anthropic.com>

* fix(tui): stop prior answers duplicating on threads with history

On a thread with history, DeerFlowClient re-emits every prior message on each
new turn (its streamed_ids dedup is per-stream-call), and a re-emitted older
message can arrive after a newer message has already started. The reducer only
matched the *most recent* assistant row by id and otherwise appended, so each
re-emitted older answer was duplicated verbatim at the end of the transcript.

Match an assistant row by id anywhere in the transcript and merge in place.
Tool cards already de-dupe by call id globally, so they were unaffected.

Co-Authored-By: Claude Opus 4.8 <noreply@anthropic.com>

* fix(tui): correct CJK cursor drift in the composer

Confirmed a Textual Input bug (latest 8.2.7): Input._cursor_offset adds an
unconditional +1 at the end of the value, overshooting by one cell after
double-width (CJK) characters. That misplaces the hardware/IME cursor — the
drift seen when typing Chinese in iTerm2 (the on-screen block cursor, drawn
separately in render_line, is fine; English doesn't use an IME so it looks
correct). Reproduced with a bare Input, so it's upstream, not our layout.

Add ComposerInput(Input) overriding _cursor_offset to the true cell position and
use it for the composer. Numeric tests pin the CJK end/mid and ASCII cases.

Co-Authored-By: Claude Opus 4.8 <noreply@anthropic.com>

* feat(tui): render finalized assistant messages as Markdown

The transcript showed raw Markdown (literal **bold**, ## headings, - lists,
links). Finalized assistant messages now render as Rich Markdown — headings,
bold/italic, lists, inline code + code blocks, blockquotes, horizontal rules and
links — with the ● speaker marker aligned to the top of the body.

The actively-streaming message stays plain text so partial Markdown doesn't
reflow/jump, then snaps to its rendered form when the run ends. Transcript
re-renders are coalesced on a ~60ms timer (dirty flag) so per-token Markdown
re-parsing stays smooth on long threads. Tests cover both the rendered and the
streaming-plain paths.

Co-Authored-By: Claude Opus 4.8 <noreply@anthropic.com>

* style(tui): apply ruff format

CI lint runs `ruff format --check` via uvx (latest ruff); apply the formatter so
the lint-backend job passes. No behavior change.

Co-Authored-By: Claude Opus 4.8 <noreply@anthropic.com>

* chore(tui): address code-quality review comments

From github-code-quality[bot] on #3760:
- runtime.py: give the `_ClientLike` Protocol method a docstring body instead of
 a bare `...` (flagged as a no-effect statement), matching the harness
 convention for Protocol stubs (e.g. SafetyTerminationDetector).
- test_tui_cli_main.py: drop the unnecessary `lambda: _FakeSession()` wrappers in
 monkeypatch.setattr; pass `_FakeSession` directly (same behavior).

Co-Authored-By: Claude Opus 4.8 <noreply@anthropic.com>

* fix(tui): keep history Markdown-rendered when a follow-up run starts

Previously the transcript rendered "the last assistant row" as plain text while
streaming. But when a follow-up turn starts, the last assistant row is the
*previous, finalized* answer until the new message begins — and the client
re-emits prior messages early in the turn — so sending a follow-up reverted the
previous answer from rendered Markdown back to raw text.

Track the actively-streaming message id in ViewState instead: it's reset on
RunStarted, set only when an AssistantDelta actually adds new content (history
re-emits are no-ops and don't mark it), and cleared on RunEnded. The renderer
keeps only that one message plain; all history stays Markdown.

Co-Authored-By: Claude Opus 4.8 <noreply@anthropic.com>

* docs(readme): add Terminal Workbench (TUI) section to root README

Mention the new `deerflow` TUI alongside the Embedded Python Client in the root
README.md and README_zh.md (install, launch/headless commands, feature summary,
Web UI visibility), with a ToC entry and a preview screenshot. Links to
backend/docs/TUI.md for the full guide.

Co-Authored-By: Claude Opus 4.8 <noreply@anthropic.com>

* fix(tui): address review feedback (willem-bd)

Ten findings from the TUI code review:

1. /resume was dead-ended — registered + in /help + tested as a builtin, but no
 dispatch branch. Wired it to thread resolution / the switcher.
2. --resume <title> was forwarded raw into the checkpointer (blank thread).
 Added Session.resolve_ref() to resolve id-or-title via list_threads; used by
 --resume and /resume.
3. str(get("id","")) returned "None" for an explicit id:None (truthy), defeating
 the empty-id guard so unrelated null-id tool calls collapsed into one card.
 Coerce via a None-safe helper.
4. Headless --print/--json no longer spin up the persistence loop/engine/pool
 (open_session(persistence=False)).
5. _LoopThread + engine are now closed: Session.close() (dispose engine + stop
 loop) called from a try/finally around app.run().
6. --cli --continue (and piped --cli) now run headless instead of erroring.
7. Cancelled runs no longer persist a truncated title (guard on _cancelled).
8. Palette highlight resets to the top when the filter set changes.
9. Dropped the never-populated tools count from the header.
10. Documented the `not row.error` merge guard.

Adds regression tests for each; 126 TUI tests pass, ruff check + format clean.

Co-Authored-By: Claude Opus 4.8 <noreply@anthropic.com>

---------

Co-authored-by: Claude Opus 4.8 <noreply@anthropic.com>
Co-authored-by: Willem Jiang <willem.jiang@gmail.com>')

 | 

Jun 25, 2026

 |
| 

[CODE\_CHANGE\_SUMMARY\_BY\_FILE.md](https://github.com/bytedance/deer-flow/blob/main/docs/CODE_CHANGE_SUMMARY_BY_FILE.md 'CODE_CHANGE_SUMMARY_BY_FILE.md')

 | 

[CODE\_CHANGE\_SUMMARY\_BY\_FILE.md](https://github.com/bytedance/deer-flow/blob/main/docs/CODE_CHANGE_SUMMARY_BY_FILE.md 'CODE_CHANGE_SUMMARY_BY_FILE.md')

 | 

[docs: clean gateway runtime transition remnants (](https://github.com/bytedance/deer-flow/commit/74e3e80cf6fc02a3eefa73f32b08882808aac9c6 'docs: clean gateway runtime transition remnants (#3334)') [#3334](https://github.com/bytedance/deer-flow/pull/3334) [)](https://github.com/bytedance/deer-flow/commit/74e3e80cf6fc02a3eefa73f32b08882808aac9c6 'docs: clean gateway runtime transition remnants (#3334)')

 | 

Jun 2, 2026

 |
| 

[OPENVIKING.md](https://github.com/bytedance/deer-flow/blob/main/docs/OPENVIKING.md 'OPENVIKING.md')

 | 

[OPENVIKING.md](https://github.com/bytedance/deer-flow/blob/main/docs/OPENVIKING.md 'OPENVIKING.md')

 | 

[refactor(memory): use official OpenViking adapter (](https://github.com/bytedance/deer-flow/commit/6556d09d7f3800ca570820819455c39b4584482f 'refactor(memory): use official OpenViking adapter (#4707)

* refactor(memory): use official OpenViking adapter

* fix(memory): preserve OpenViking recall behavior

* fix(memory): ignore ambient OpenViking headers') [#4707](https://github.com/bytedance/deer-flow/pull/4707) [)](https://github.com/bytedance/deer-flow/commit/6556d09d7f3800ca570820819455c39b4584482f 'refactor(memory): use official OpenViking adapter (#4707)

* refactor(memory): use official OpenViking adapter

* fix(memory): preserve OpenViking recall behavior

* fix(memory): ignore ambient OpenViking headers')

 | 

Aug 7, 2026

 |
| 

[SKILL\_NAME\_CONFLICT\_FIX.md](https://github.com/bytedance/deer-flow/blob/main/docs/SKILL_NAME_CONFLICT_FIX.md 'SKILL_NAME_CONFLICT_FIX.md')

 | 

[SKILL\_NAME\_CONFLICT\_FIX.md](https://github.com/bytedance/deer-flow/blob/main/docs/SKILL_NAME_CONFLICT_FIX.md 'SKILL_NAME_CONFLICT_FIX.md')

 | 

[refactor: split backend into harness (deerflow.\*) and app (app.\*) (](https://github.com/bytedance/deer-flow/commit/76803b826f30028e691ea981bf51da641c0be632 'refactor: split backend into harness (deerflow.*) and app (app.*) (#1131)

* refactor: extract shared utils to break harness→app cross-layer imports

Move _validate_skill_frontmatter to src/skills/validation.py and
CONVERTIBLE_EXTENSIONS + convert_file_to_markdown to src/utils/file_conversion.py.
This eliminates the two reverse dependencies from client.py (harness layer)
into gateway/routers/ (app layer), preparing for the harness/app package split.

Co-Authored-By: Claude Opus 4.6 <noreply@anthropic.com>

* refactor: split backend/src into harness (deerflow.*) and app (app.*)

Physically split the monolithic backend/src/ package into two layers:

- **Harness** (`packages/harness/deerflow/`): publishable agent framework
 package with import prefix `deerflow.*`. Contains agents, sandbox, tools,
 models, MCP, skills, config, and all core infrastructure.

- **App** (`app/`): unpublished application code with import prefix `app.*`.
 Contains gateway (FastAPI REST API) and channels (IM integrations).

Key changes:
- Move 13 harness modules to packages/harness/deerflow/ via git mv
- Move gateway + channels to app/ via git mv
- Rename all imports: src.* → deerflow.* (harness) / app.* (app layer)
- Set up uv workspace with deerflow-harness as workspace member
- Update langgraph.json, config.example.yaml, all scripts, Docker files
- Add build-system (hatchling) to harness pyproject.toml
- Add PYTHONPATH=. to gateway startup commands for app.* resolution
- Update ruff.toml with known-first-party for import sorting
- Update all documentation to reflect new directory structure

Boundary rule enforced: harness code never imports from app.
All 429 tests pass. Lint clean.

Co-Authored-By: Claude Opus 4.6 <noreply@anthropic.com>

* chore: add harness→app boundary check test and update docs

Add test_harness_boundary.py that scans all Python files in
packages/harness/deerflow/ and fails if any `from app.*` or
`import app.*` statement is found. This enforces the architectural
rule that the harness layer never depends on the app layer.

Update CLAUDE.md to document the harness/app split architecture,
import conventions, and the boundary enforcement test.

Co-Authored-By: Claude Opus 4.6 <noreply@anthropic.com>

* feat: add config versioning with auto-upgrade on startup

When config.example.yaml schema changes, developers' local config.yaml
files can silently become outdated. This adds a config_version field and
auto-upgrade mechanism so breaking changes (like src.* → deerflow.*
renames) are applied automatically before services start.

- Add config_version: 1 to config.example.yaml
- Add startup version check warning in AppConfig.from_file()
- Add scripts/config-upgrade.sh with migration registry for value replacements
- Add `make config-upgrade` target
- Auto-run config-upgrade in serve.sh and start-daemon.sh before starting services
- Add config error hints in service failure messages

Co-Authored-By: Claude Opus 4.6 <noreply@anthropic.com>

* fix comments

* fix: update src.* import in test_sandbox_tools_security to deerflow.*

Co-Authored-By: Claude Opus 4.6 <noreply@anthropic.com>

* fix: handle empty config and search parent dirs for config.example.yaml

Address Copilot review comments on PR #1131:
- Guard against yaml.safe_load() returning None for empty config files
- Search parent directories for config.example.yaml instead of only
 looking next to config.yaml, fixing detection in common setups

Co-Authored-By: Claude Opus 4.6 <noreply@anthropic.com>

* fix: correct skills root path depth and config_version type coercion

- loader.py: fix get_skills_root_path() to use 5 parent levels (was 3)
 after harness split, file lives at packages/harness/deerflow/skills/
 so parent×3 resolved to backend/packages/harness/ instead of backend/
- app_config.py: coerce config_version to int() before comparison in
 _check_config_version() to prevent TypeError when YAML stores value
 as string (e.g. config_version: "1")
- tests: add regression tests for both fixes

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>

* fix: update test imports from src.* to deerflow.*/app.* after harness refactor

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>

---------

Co-authored-by: Claude Opus 4.6 <noreply@anthropic.com>') [#1131](https://github.com/bytedance/deer-flow/pull/1131)

 | 

Mar 14, 2026

 |
| 

View all files

 |