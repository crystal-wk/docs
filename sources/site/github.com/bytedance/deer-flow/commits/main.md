# Source: https://github.com/bytedance/deer-flow/commits/main

### Uh oh!

There was an error while loading. [Please reload this page]().

[bytedance](https://github.com/bytedance) / **[deer-flow](https://github.com/bytedance/deer-flow)** Public

- [Notifications](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow) You must be signed in to change notification settings
- [Fork 10.9k](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow)
- [Star 79.8k](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow)

 ## Branch selector

main

## User selector

All users

## Datepicker

All time

## Commit history

### Commits on Aug 12, 2026

- #### [fix(subagents): isolate background tasks from reused tool call IDs (](https://github.com/bytedance/deer-flow/commit/88252e9b318d34e7e1867155ad2c77993320788e 'fix(subagents): isolate background tasks from reused tool call IDs (#4758)

 * fix(subagents): isolate background execution IDs

 * fix(subagents): preserve correlation scope and isolate usage

 * fix(subagents): make usage attribution idempotent') [#4758](https://github.com/bytedance/deer-flow/pull/4758) [)](https://github.com/bytedance/deer-flow/commit/88252e9b318d34e7e1867155ad2c77993320788e 'fix(subagents): isolate background tasks from reused tool call IDs (#4758)

 * fix(subagents): isolate background execution IDs

 * fix(subagents): preserve correlation scope and isolate usage

 * fix(subagents): make usage attribution idempotent')

 Show description for 88252e9

 [![ZeroMadLife](https://avatars.githubusercontent.com/u/97534761?v=4&size=32)](https://github.com/ZeroMadLife) [ZeroMadLife](https://github.com/bytedance/deer-flow/commits?author=ZeroMadLife)

 authoredAug 12, 2026

 ·

 10 / 10

 Verified

 [88252e9](https://github.com/bytedance/deer-flow/commit/88252e9b318d34e7e1867155ad2c77993320788e)View commit details

 Copy full SHA for 88252e9

 Browse repository at this point

- #### [refactor(frontend): share showcase chat page (](https://github.com/bytedance/deer-flow/commit/e23dd8f88b5cc172e7ed67a0a791bd226108c80b 'refactor(frontend): share showcase chat page (#4765)') [#4765](https://github.com/bytedance/deer-flow/pull/4765) [)](https://github.com/bytedance/deer-flow/commit/e23dd8f88b5cc172e7ed67a0a791bd226108c80b 'refactor(frontend): share showcase chat page (#4765)')

 [![DaoyuanLi2816](https://avatars.githubusercontent.com/u/94409450?v=4&size=32)](https://github.com/DaoyuanLi2816) [DaoyuanLi2816](https://github.com/bytedance/deer-flow/commits?author=DaoyuanLi2816)

 authoredAug 12, 2026

 ·

 10 / 10

 Verified

 [e23dd8f](https://github.com/bytedance/deer-flow/commit/e23dd8f88b5cc172e7ed67a0a791bd226108c80b)View commit details

 Copy full SHA for e23dd8f

 Browse repository at this point

- #### [feat(memory): add Honcho backend (user-model memory provider) (](https://github.com/bytedance/deer-flow/commit/6cbf20fd39b34514f53f50fa097220a1deded65a 'feat(memory): add Honcho backend (user-model memory provider) (#4730)

 * feat(memory): honcho backend config parsing

 Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>

 * feat(memory): honcho v3 http client

 Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>

 * feat(memory): honcho memory manager (workspace-per-user, fail-closed identity, async offload)

 - HonchoMemoryManager implements the MemoryManager contract (add/get_context/
 search/get_memory/shutdown_flush + aadd/aget_context/asearch offloaded via
 asyncio.to_thread), signatures verified against manager.py's tier-1/tier-2/
 async abstracts.
 - Workspace resolution: workspace_overrides[user_id] else
 workspace_prefix + sanitize_id(user_id); missing/empty user_id fails closed
 (no-op write, empty read) rather than falling back to a shared workspace.
 User peer: user_peer_overrides[user_id] else sanitize_id(user_id).
 - get_context self-truncates to max_injection_chars and raises
 MemoryManagerError only under failure_policy.read=fail_closed; default is
 log-and-return "".
 - Restore backends/honcho/__init__.py to the noop direct-import convention
 (MANAGER_CLASS = HonchoMemoryManager) now that honcho_manager.py exists,
 replacing Task 10's temporary lazy __getattr__ scaffold.
 - Fix Task 10 deferred docstring minor: sanitize_id docstring now states the
 grammar allows up to 100 chars while this helper caps at 64.
 - 19 new tests appended to test_honcho_memory_backend.py (write/read/async/
 lifecycle/factory-discovery); 27/27 pass. Verified end-to-end that
 manager.py's drop-in backend scanner resolves "honcho" with no core edits.

 Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>

 * fix(memory): collision-resistant identity derivation, exception containment, passive-writes flag

 Task review findings (2 Critical + 1 Important), all fixed in the same worktree:

 - CRITICAL (cross-user bleed): sanitize_id is lossy -- "user.name@example.com"
 and "user-name@example.com" both sanitized to the same string, merging two
 users' memory into one workspace/peer. Add _stable_id() (sanitize_id output
 + 8-hex-char SHA-256 suffix of the raw id) and use it on the default
 (non-override) path in _workspace/_user_peer; workspace_overrides /
 user_peer_overrides still match on the raw key, unchanged. The hash suffix
 also guarantees a non-empty result for a raw id that sanitizes to "" (e.g.
 "!!!"), so _user_peer can no longer return "". Documented in the manager's
 isolation docstring.

 - CRITICAL (exception containment): client.py's _post() called response.json()
 outside the try block, so a 200 with a non-JSON body raised a bare
 JSONDecodeError that would escape add() with no upstream handler. Wrap the
 parse and raise HonchoRequestError (mirrors Mem0Client._request). Broadened
 the manager's four boundary excepts from `except HonchoRequestError` to
 `except Exception` (mirrors openviking_manager.py's broad-guard precedent),
 with `except MemoryManagerError: raise` first so a contract error is never
 swallowed or double-wrapped.

 - IMPORTANT: added requires_passive_writes_in_tool_mode: ClassVar[bool] = True
 -- Honcho's only write path is passive add() (no fact CRUD hooks), so tool
 mode must keep MemoryMiddleware writes flowing to the deriver. Mirrors
 mem0_manager.py's identical flag/rationale.

 Minors addressed: get_memory(user_id=None) empty-shape-with-no-calls test;
 empty-string user_id tests for add()/get_context(); dedicated collision test
 proving two colliding raw ids resolve to different workspaces/peers.

 10 new tests (37/37 total pass); RED verified by stashing only the
 implementation files (tests import the not-yet-existing _stable_id, so the
 whole module fails to collect) before restoring the fix.

 Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>

 * test(memory): blocking-io anchor for honcho backend; docs + config example

 - Adds test_honcho_memory_backend.py in tests/blocking_io/ with fake-client blocking IO
 - Mirrors openviking anchor structure and conftest conventions
 - Updates backends/README.md with honcho row and config keys section
 - Updates config.example.yaml with honcho commented block
 - Updates backend/AGENTS.md with honcho memory backend bullet
 - Documents workspace resolution (prefix + collision-resistant sanitized id)
 - Documents tool mode passive write retention via MemoryMiddleware
 - Documents async entrypoint offloading via asyncio.to_thread
 - Documents fail_closed vs fail_open recall failure policy

 Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>

 * fix(memory): wire close() to shutdown hook; correct honcho README defaults and tool-mode note

 - HonchoMemoryManager.close() releases the HTTP client, mirroring
 mem0_manager.py's pattern and the base MemoryManager.close() shutdown hook.
 - README: fix workspace_prefix (deerflow-u-), message_char_limit (8000),
 max_injection_chars (6000), and base_url (default http://localhost:8000,
 not required) against backends/honcho/config.py; add missing
 timeout_seconds/connect_timeout_seconds rows; replace the "middleware
 mode only" claim with wording matching reality (tool mode supported,
 search implemented, passive writes retained via MemoryMiddleware).

 Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>

 * fix(memory): honor failure_policy.read on all honcho recall paths; review nits

 Addresses PR #4730 review feedback:
 - search() and get_memory() now route through a _read_or_fallback policy
 gate (mem0's pattern), so failure_policy.read: fail_closed raises
 MemoryManagerError on every recall path as documented; get_context()
 uses the same helper, preventing future drift.
 - Session ids use the collision-resistant _stable_id derivation; bare
 sanitize_id would merge threads like "t.1"/"t-1" into one session.
 - HonchoClient accepts a transport kwarg (Mem0Client precedent) so tests
 inject httpx.MockTransport through the constructor.
 - Config: empty/null workspace/peer override values fail fast at parse
 time instead of silently falling through to the default derivation.
 - _UTC_NOW_FIELDS 1-tuple replaced by a plain _UTC_NOW_FORMAT constant.
 - README: user_peer_overrides row described the wrong target (it
 overrides the user's own peer, not assistant_peer); document the
 non-empty constraint on override values.

 Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>

 * docs(memory): qualify honcho isolation claim for shared workspace_overrides

 The module docstring claimed users cannot see each other's memory by
 construction, unconditionally. That holds for the default
 one-workspace-per-user derivation, but a workspace_overrides entry mapping
 several users to one workspace shares that workspace's search index:
 search() uses Honcho's workspace-scoped /search (no peer filter), while
 get_context()/get_memory() stay peer-scoped via working_representation.
 State the asymmetry in the docstring, the README Workspace Resolution
 section, and the workspace_overrides table row.

 Docs-only; no behavior change (review follow-up on #4730).

 Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>

 ---------

 Co-authored-by: Claude Fable 5 <noreply@anthropic.com>') [#4730](https://github.com/bytedance/deer-flow/pull/4730) [)](https://github.com/bytedance/deer-flow/commit/6cbf20fd39b34514f53f50fa097220a1deded65a 'feat(memory): add Honcho backend (user-model memory provider) (#4730)

 * feat(memory): honcho backend config parsing

 Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>

 * feat(memory): honcho v3 http client

 Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>

 * feat(memory): honcho memory manager (workspace-per-user, fail-closed identity, async offload)

 - HonchoMemoryManager implements the MemoryManager contract (add/get_context/
 search/get_memory/shutdown_flush + aadd/aget_context/asearch offloaded via
 asyncio.to_thread), signatures verified against manager.py's tier-1/tier-2/
 async abstracts.
 - Workspace resolution: workspace_overrides[user_id] else
 workspace_prefix + sanitize_id(user_id); missing/empty user_id fails closed
 (no-op write, empty read) rather than falling back to a shared workspace.
 User peer: user_peer_overrides[user_id] else sanitize_id(user_id).
 - get_context self-truncates to max_injection_chars and raises
 MemoryManagerError only under failure_policy.read=fail_closed; default is
 log-and-return "".
 - Restore backends/honcho/__init__.py to the noop direct-import convention
 (MANAGER_CLASS = HonchoMemoryManager) now that honcho_manager.py exists,
 replacing Task 10's temporary lazy __getattr__ scaffold.
 - Fix Task 10 deferred docstring minor: sanitize_id docstring now states the
 grammar allows up to 100 chars while this helper caps at 64.
 - 19 new tests appended to test_honcho_memory_backend.py (write/read/async/
 lifecycle/factory-discovery); 27/27 pass. Verified end-to-end that
 manager.py's drop-in backend scanner resolves "honcho" with no core edits.

 Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>

 * fix(memory): collision-resistant identity derivation, exception containment, passive-writes flag

 Task review findings (2 Critical + 1 Important), all fixed in the same worktree:

 - CRITICAL (cross-user bleed): sanitize_id is lossy -- "user.name@example.com"
 and "user-name@example.com" both sanitized to the same string, merging two
 users' memory into one workspace/peer. Add _stable_id() (sanitize_id output
 + 8-hex-char SHA-256 suffix of the raw id) and use it on the default
 (non-override) path in _workspace/_user_peer; workspace_overrides /
 user_peer_overrides still match on the raw key, unchanged. The hash suffix
 also guarantees a non-empty result for a raw id that sanitizes to "" (e.g.
 "!!!"), so _user_peer can no longer return "". Documented in the manager's
 isolation docstring.

 - CRITICAL (exception containment): client.py's _post() called response.json()
 outside the try block, so a 200 with a non-JSON body raised a bare
 JSONDecodeError that would escape add() with no upstream handler. Wrap the
 parse and raise HonchoRequestError (mirrors Mem0Client._request). Broadened
 the manager's four boundary excepts from `except HonchoRequestError` to
 `except Exception` (mirrors openviking_manager.py's broad-guard precedent),
 with `except MemoryManagerError: raise` first so a contract error is never
 swallowed or double-wrapped.

 - IMPORTANT: added requires_passive_writes_in_tool_mode: ClassVar[bool] = True
 -- Honcho's only write path is passive add() (no fact CRUD hooks), so tool
 mode must keep MemoryMiddleware writes flowing to the deriver. Mirrors
 mem0_manager.py's identical flag/rationale.

 Minors addressed: get_memory(user_id=None) empty-shape-with-no-calls test;
 empty-string user_id tests for add()/get_context(); dedicated collision test
 proving two colliding raw ids resolve to different workspaces/peers.

 10 new tests (37/37 total pass); RED verified by stashing only the
 implementation files (tests import the not-yet-existing _stable_id, so the
 whole module fails to collect) before restoring the fix.

 Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>

 * test(memory): blocking-io anchor for honcho backend; docs + config example

 - Adds test_honcho_memory_backend.py in tests/blocking_io/ with fake-client blocking IO
 - Mirrors openviking anchor structure and conftest conventions
 - Updates backends/README.md with honcho row and config keys section
 - Updates config.example.yaml with honcho commented block
 - Updates backend/AGENTS.md with honcho memory backend bullet
 - Documents workspace resolution (prefix + collision-resistant sanitized id)
 - Documents tool mode passive write retention via MemoryMiddleware
 - Documents async entrypoint offloading via asyncio.to_thread
 - Documents fail_closed vs fail_open recall failure policy

 Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>

 * fix(memory): wire close() to shutdown hook; correct honcho README defaults and tool-mode note

 - HonchoMemoryManager.close() releases the HTTP client, mirroring
 mem0_manager.py's pattern and the base MemoryManager.close() shutdown hook.
 - README: fix workspace_prefix (deerflow-u-), message_char_limit (8000),
 max_injection_chars (6000), and base_url (default http://localhost:8000,
 not required) against backends/honcho/config.py; add missing
 timeout_seconds/connect_timeout_seconds rows; replace the "middleware
 mode only" claim with wording matching reality (tool mode supported,
 search implemented, passive writes retained via MemoryMiddleware).

 Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>

 * fix(memory): honor failure_policy.read on all honcho recall paths; review nits

 Addresses PR #4730 review feedback:
 - search() and get_memory() now route through a _read_or_fallback policy
 gate (mem0's pattern), so failure_policy.read: fail_closed raises
 MemoryManagerError on every recall path as documented; get_context()
 uses the same helper, preventing future drift.
 - Session ids use the collision-resistant _stable_id derivation; bare
 sanitize_id would merge threads like "t.1"/"t-1" into one session.
 - HonchoClient accepts a transport kwarg (Mem0Client precedent) so tests
 inject httpx.MockTransport through the constructor.
 - Config: empty/null workspace/peer override values fail fast at parse
 time instead of silently falling through to the default derivation.
 - _UTC_NOW_FIELDS 1-tuple replaced by a plain _UTC_NOW_FORMAT constant.
 - README: user_peer_overrides row described the wrong target (it
 overrides the user's own peer, not assistant_peer); document the
 non-empty constraint on override values.

 Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>

 * docs(memory): qualify honcho isolation claim for shared workspace_overrides

 The module docstring claimed users cannot see each other's memory by
 construction, unconditionally. That holds for the default
 one-workspace-per-user derivation, but a workspace_overrides entry mapping
 several users to one workspace shares that workspace's search index:
 search() uses Honcho's workspace-scoped /search (no peer filter), while
 get_context()/get_memory() stay peer-scoped via working_representation.
 State the asymmetry in the docstring, the README Workspace Resolution
 section, and the workspace_overrides table row.

 Docs-only; no behavior change (review follow-up on #4730).

 Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>

 ---------

 Co-authored-by: Claude Fable 5 <noreply@anthropic.com>')

 Show description for 6cbf20f

 ![ajayr](https://avatars.githubusercontent.com/u/809529?v=4&size=32)![claude](https://avatars.githubusercontent.com/u/81847?v=4&size=32)

 [ajayr](https://github.com/bytedance/deer-flow/commits?author=ajayr)

 and

 [claude](https://github.com/bytedance/deer-flow/commits?author=claude)

 authoredAug 12, 2026

 ·

 10 / 10

 Verified

 [6cbf20f](https://github.com/bytedance/deer-flow/commit/6cbf20fd39b34514f53f50fa097220a1deded65a)View commit details

 Copy full SHA for 6cbf20f

 Browse repository at this point

- #### [test(llm-error): rename a stand-in, not the shared FakeError (](https://github.com/bytedance/deer-flow/commit/2df7d47b2a52cf5e14298a43e1c68800bc3177bc 'test(llm-error): rename a stand-in, not the shared FakeError (#4744)

 * test(llm-error): rename a stand-in, not the shared FakeError

 `exc.__class__.__name__ = "ReadError"` on a `FakeError` instance renames the
 class itself, so `FakeError` stays named "ReadError" for the rest of the
 session and every later test asserting error_type == "FakeError" fails.
 Declaration order hides it: the renaming test runs after its victims.

 Use the existing _ReadError stand-in, which is already named "ReadError" and
 is how the sibling _max_attempts_for test builds the same case. Add an autouse
 fixture so a future slip fails the test that causes it.

 * Potential fix for pull request finding

 Co-authored-by: Copilot Autofix powered by AI <175728472+Copilot@users.noreply.github.com>

 * style: format FakeError guard

 ---------

 Co-authored-by: Willem Jiang <willem.jiang@gmail.com>
 Co-authored-by: Copilot Autofix powered by AI <175728472+Copilot@users.noreply.github.com>') [#4744](https://github.com/bytedance/deer-flow/pull/4744) [)](https://github.com/bytedance/deer-flow/commit/2df7d47b2a52cf5e14298a43e1c68800bc3177bc 'test(llm-error): rename a stand-in, not the shared FakeError (#4744)

 * test(llm-error): rename a stand-in, not the shared FakeError

 `exc.__class__.__name__ = "ReadError"` on a `FakeError` instance renames the
 class itself, so `FakeError` stays named "ReadError" for the rest of the
 session and every later test asserting error_type == "FakeError" fails.
 Declaration order hides it: the renaming test runs after its victims.

 Use the existing _ReadError stand-in, which is already named "ReadError" and
 is how the sibling _max_attempts_for test builds the same case. Add an autouse
 fixture so a future slip fails the test that causes it.

 * Potential fix for pull request finding

 Co-authored-by: Copilot Autofix powered by AI <175728472+Copilot@users.noreply.github.com>

 * style: format FakeError guard

 ---------

 Co-authored-by: Willem Jiang <willem.jiang@gmail.com>
 Co-authored-by: Copilot Autofix powered by AI <175728472+Copilot@users.noreply.github.com>')

 Show description for 2df7d47

 ![DaoyuanLi2816](https://avatars.githubusercontent.com/u/94409450?v=4&size=32)![WillemJiang](https://avatars.githubusercontent.com/u/219644?v=4&size=32)![Copilot](https://avatars.githubusercontent.com/in/946600?v=4&size=32)

 3 peopleauthoredAug 12, 2026

 ·

 8 / 8

 Verified

 [2df7d47](https://github.com/bytedance/deer-flow/commit/2df7d47b2a52cf5e14298a43e1c68800bc3177bc)View commit details

 Copy full SHA for 2df7d47

 Browse repository at this point

- #### [feat(channels): polish Buzz frontend (](https://github.com/bytedance/deer-flow/commit/1e8cedb9f4c1fd527e91729936c42be1f05d8438 'feat(channels): polish Buzz frontend (#4727)

 * feat(channels): complete Buzz frontend copy

 * feat(channels): add official Buzz provider icon

 * test(i18n): clarify translation suite scope') [#4727](https://github.com/bytedance/deer-flow/pull/4727) [)](https://github.com/bytedance/deer-flow/commit/1e8cedb9f4c1fd527e91729936c42be1f05d8438 'feat(channels): polish Buzz frontend (#4727)

 * feat(channels): complete Buzz frontend copy

 * feat(channels): add official Buzz provider icon

 * test(i18n): clarify translation suite scope')

 Show description for 1e8cedb

 [![18062706139fcz](https://avatars.githubusercontent.com/u/90562015?v=4&size=32)](https://github.com/18062706139fcz) [18062706139fcz](https://github.com/bytedance/deer-flow/commits?author=18062706139fcz)

 authoredAug 12, 2026

 ·

 10 / 10

 Verified

 [1e8cedb](https://github.com/bytedance/deer-flow/commit/1e8cedb9f4c1fd527e91729936c42be1f05d8438)View commit details

 Copy full SHA for 1e8cedb

 Browse repository at this point

### Commits on Aug 11, 2026

- #### [test(tool-output): stop expressing "unwritable path" as a magic absolute path (](https://github.com/bytedance/deer-flow/commit/1fe71110af5b3b470bdb4b3c5e98c46b0bea37e4 'test(tool-output): stop expressing "unwritable path" as a magic absolute path (#4722)

 * test(tool-output): stop expressing "unwritable path" as a magic absolute path

 `test_returns_none_on_invalid_path` and `test_fallback_when_disk_write_fails`
 both need an `outputs_path` that `os.makedirs` refuses to create, so they can
 reach `_externalize`'s `except OSError: return None` branch. They spell that as
 the literal path `/dev/null/cannot-mkdir-here`, which only works where
 `/dev/null` is a character device.

 On Windows it is an ordinary relative path, so `os.makedirs` succeeds, both
 tests fail, and the suite writes real files to `C:\dev\null\cannot-mkdir-here\
 .tool-results\` -- outside any temporary directory, at the drive root. Running
 the backend suite a few times leaves dozens of stray files behind.

 The comment above the first test records that this is the second time the
 same assumption has broken: `/nonexistent/...` was silently created by `mkdir
 -p` when CI ran as root in a container, and `/dev/null/...` was the fix. Both
 encode a guess about the environment rather than the condition under test.

 Use a regular file as the parent component instead. Creating a directory below
 a file fails with an `OSError` subclass on every platform -- `NotADirectoryError`
 (errno 20) on POSIX, `FileNotFoundError` (errno 2) on Windows -- so the branch
 is reached deterministically, and the path lives inside the test's own
 `TemporaryDirectory`, so nothing is written outside it.

 Verified both spellings on Linux (WSL Ubuntu, non-root) and Windows; only the
 file-as-parent form fails on both. The two tests still have teeth: dropping
 `_externalize`'s `except OSError` guard makes both fail rather than pass.

 Tests only -- no production code or documented behaviour changes.

 * test(tool-output): touch the blocker file instead of writing content

 Only its existence as a regular file matters for os.makedirs to fail
 below it, so touch() states that directly.') [#4722](https://github.com/bytedance/deer-flow/pull/4722) [)](https://github.com/bytedance/deer-flow/commit/1fe71110af5b3b470bdb4b3c5e98c46b0bea37e4 'test(tool-output): stop expressing "unwritable path" as a magic absolute path (#4722)

 * test(tool-output): stop expressing "unwritable path" as a magic absolute path

 `test_returns_none_on_invalid_path` and `test_fallback_when_disk_write_fails`
 both need an `outputs_path` that `os.makedirs` refuses to create, so they can
 reach `_externalize`'s `except OSError: return None` branch. They spell that as
 the literal path `/dev/null/cannot-mkdir-here`, which only works where
 `/dev/null` is a character device.

 On Windows it is an ordinary relative path, so `os.makedirs` succeeds, both
 tests fail, and the suite writes real files to `C:\dev\null\cannot-mkdir-here\
 .tool-results\` -- outside any temporary directory, at the drive root. Running
 the backend suite a few times leaves dozens of stray files behind.

 The comment above the first test records that this is the second time the
 same assumption has broken: `/nonexistent/...` was silently created by `mkdir
 -p` when CI ran as root in a container, and `/dev/null/...` was the fix. Both
 encode a guess about the environment rather than the condition under test.

 Use a regular file as the parent component instead. Creating a directory below
 a file fails with an `OSError` subclass on every platform -- `NotADirectoryError`
 (errno 20) on POSIX, `FileNotFoundError` (errno 2) on Windows -- so the branch
 is reached deterministically, and the path lives inside the test's own
 `TemporaryDirectory`, so nothing is written outside it.

 Verified both spellings on Linux (WSL Ubuntu, non-root) and Windows; only the
 file-as-parent form fails on both. The two tests still have teeth: dropping
 `_externalize`'s `except OSError` guard makes both fail rather than pass.

 Tests only -- no production code or documented behaviour changes.

 * test(tool-output): touch the blocker file instead of writing content

 Only its existence as a regular file matters for os.makedirs to fail
 below it, so touch() states that directly.')

 Show description for 1fe7111

 [![DaoyuanLi2816](https://avatars.githubusercontent.com/u/94409450?v=4&size=32)](https://github.com/DaoyuanLi2816) [DaoyuanLi2816](https://github.com/bytedance/deer-flow/commits?author=DaoyuanLi2816)

 authoredAug 11, 2026

 ·

 8 / 8

 Verified

 [1fe7111](https://github.com/bytedance/deer-flow/commit/1fe71110af5b3b470bdb4b3c5e98c46b0bea37e4)View commit details

 Copy full SHA for 1fe7111

 Browse repository at this point

- #### [fix(wecom): serialize websocket shutdown (](https://github.com/bytedance/deer-flow/commit/38ff44778a0d11d71597c2531bfd600df855307c 'fix(wecom): serialize websocket shutdown (#4762)

 * fix(wecom): await connection task shutdown

 * fix(wecom): serialize websocket shutdown') [#4762](https://github.com/bytedance/deer-flow/pull/4762) [)](https://github.com/bytedance/deer-flow/commit/38ff44778a0d11d71597c2531bfd600df855307c 'fix(wecom): serialize websocket shutdown (#4762)

 * fix(wecom): await connection task shutdown

 * fix(wecom): serialize websocket shutdown')

 Show description for 38ff447

 [![AoHanBei](https://avatars.githubusercontent.com/u/170841481?v=4&size=32)](https://github.com/AoHanBei) [AoHanBei](https://github.com/bytedance/deer-flow/commits?author=AoHanBei)

 authoredAug 11, 2026

 ·

 9 / 9

 Verified

 [38ff447](https://github.com/bytedance/deer-flow/commit/38ff44778a0d11d71597c2531bfd600df855307c)View commit details

 Copy full SHA for 38ff447

 Browse repository at this point

- #### [fix(gateway): stamp turn\_duration on last AI message only in /messages/page (](https://github.com/bytedance/deer-flow/commit/baaf2bad47508e809baa89849d9b938e4f3e905a 'fix(gateway): stamp turn_duration on last AI message only in /messages/page (#4755)

 _enrich_thread_message_page inlined its own turn_duration loop that
 stamped EVERY AI message of a run, re-introducing #4152 on the
 /messages/page endpoint (the legacy /messages and /history endpoints
 already route through stamp_turn_duration_on_last_ai after #4163, but
 that fix missed the page path introduced earlier in #4065). A
 multi-step turn thus rendered the same run lifetime beside every
 intermediate AI message, reading as repeated thinking latency.

 Replace the inline loop with the shared stamp_turn_duration_on_last_ai
 helper so all three message endpoints agree: the run's wall-clock
 duration lands on its final visible AI message only.') [#4755](https://github.com/bytedance/deer-flow/pull/4755) [)](https://github.com/bytedance/deer-flow/commit/baaf2bad47508e809baa89849d9b938e4f3e905a 'fix(gateway): stamp turn_duration on last AI message only in /messages/page (#4755)

 _enrich_thread_message_page inlined its own turn_duration loop that
 stamped EVERY AI message of a run, re-introducing #4152 on the
 /messages/page endpoint (the legacy /messages and /history endpoints
 already route through stamp_turn_duration_on_last_ai after #4163, but
 that fix missed the page path introduced earlier in #4065). A
 multi-step turn thus rendered the same run lifetime beside every
 intermediate AI message, reading as repeated thinking latency.

 Replace the inline loop with the shared stamp_turn_duration_on_last_ai
 helper so all three message endpoints agree: the run's wall-clock
 duration lands on its final visible AI message only.')

 Show description for baaf2ba

 [![Baldwinzc](https://avatars.githubusercontent.com/u/56501736?v=4&size=32)](https://github.com/Baldwinzc) [Baldwinzc](https://github.com/bytedance/deer-flow/commits?author=Baldwinzc)

 authoredAug 11, 2026

 ·

 11 / 11

 Verified

 [baaf2ba](https://github.com/bytedance/deer-flow/commit/baaf2bad47508e809baa89849d9b938e4f3e905a)View commit details

 Copy full SHA for baaf2ba

 Browse repository at this point

- #### [fix: resolve diagnostic paths from any cwd (](https://github.com/bytedance/deer-flow/commit/6bb376abfd9934827678058ca15cba21238226d5 'fix: resolve diagnostic paths from any cwd (#4736)

 * fix: resolve diagnostic paths from any cwd

 * test: cover relative diagnostic script paths') [#4736](https://github.com/bytedance/deer-flow/pull/4736) [)](https://github.com/bytedance/deer-flow/commit/6bb376abfd9934827678058ca15cba21238226d5 'fix: resolve diagnostic paths from any cwd (#4736)

 * fix: resolve diagnostic paths from any cwd

 * test: cover relative diagnostic script paths')

 Show description for 6bb376a

 [![TNsparrow](https://avatars.githubusercontent.com/u/96582924?v=4&size=32)](https://github.com/TNsparrow) [TNsparrow](https://github.com/bytedance/deer-flow/commits?author=TNsparrow)

 authoredAug 11, 2026

 ·

 8 / 9

 Verified

 [6bb376a](https://github.com/bytedance/deer-flow/commit/6bb376abfd9934827678058ca15cba21238226d5)View commit details

 Copy full SHA for 6bb376a

 Browse repository at this point

- #### [fix(discord): prevent typing tasks after stop (](https://github.com/bytedance/deer-flow/commit/df01102dfc458559abb1acf29d9aee1fb6d9b30b 'fix(discord): prevent typing tasks after stop (#4752)

 * fix(discord): prevent typing tasks after stop

 * fix(discord): serialize typing cleanup on event loop

 * fix(discord): harden typing cleanup on loop exit') [#4752](https://github.com/bytedance/deer-flow/pull/4752) [)](https://github.com/bytedance/deer-flow/commit/df01102dfc458559abb1acf29d9aee1fb6d9b30b 'fix(discord): prevent typing tasks after stop (#4752)

 * fix(discord): prevent typing tasks after stop

 * fix(discord): serialize typing cleanup on event loop

 * fix(discord): harden typing cleanup on loop exit')

 Show description for df01102

 [![AoHanBei](https://avatars.githubusercontent.com/u/170841481?v=4&size=32)](https://github.com/AoHanBei) [AoHanBei](https://github.com/bytedance/deer-flow/commits?author=AoHanBei)

 authoredAug 11, 2026

 ·

 7 / 8

 Verified

 [df01102](https://github.com/bytedance/deer-flow/commit/df01102dfc458559abb1acf29d9aee1fb6d9b30b)View commit details

 Copy full SHA for df01102

 Browse repository at this point

- #### [refactor(sandbox): name the E2B ledger meta-field count (](https://github.com/bytedance/deer-flow/commit/46fd5c8a00a582964d86061f60f71d39b8f72e8f 'refactor(sandbox): name the E2B ledger meta-field count (#4764)

 Admission derived the live-entry count as `HLEN - 3`, where 3 was the number
 of `meta:*` fields written 35 lines earlier in initialize(). Nothing tied the
 two together, so adding a fourth meta field would shift the capacity ceiling
 by one.

 Name the offset `META_FIELD_COUNT` next to initialize(), and add a guard test
 asserting a freshly initialized ledger holds exactly those three fields, plus
 one pinning that a hard_limit of N admits exactly N reservations.

 References #4575

 Co-authored-by: icn5381 <255778606+icn5381@users.noreply.github.com>') [#4764](https://github.com/bytedance/deer-flow/pull/4764) [)](https://github.com/bytedance/deer-flow/commit/46fd5c8a00a582964d86061f60f71d39b8f72e8f 'refactor(sandbox): name the E2B ledger meta-field count (#4764)

 Admission derived the live-entry count as `HLEN - 3`, where 3 was the number
 of `meta:*` fields written 35 lines earlier in initialize(). Nothing tied the
 two together, so adding a fourth meta field would shift the capacity ceiling
 by one.

 Name the offset `META_FIELD_COUNT` next to initialize(), and add a guard test
 asserting a freshly initialized ledger holds exactly those three fields, plus
 one pinning that a hard_limit of N admits exactly N reservations.

 References #4575

 Co-authored-by: icn5381 <255778606+icn5381@users.noreply.github.com>')

 Show description for 46fd5c8

 [![icn5381](https://avatars.githubusercontent.com/u/255778606?v=4&size=32)](https://github.com/icn5381) [icn5381](https://github.com/bytedance/deer-flow/commits?author=icn5381)

 authoredAug 11, 2026

 ·

 9 / 10

 Verified

 [46fd5c8](https://github.com/bytedance/deer-flow/commit/46fd5c8a00a582964d86061f60f71d39b8f72e8f)View commit details

 Copy full SHA for 46fd5c8

 Browse repository at this point

- #### [fix(dev): exclude backend runtime state from reload (](https://github.com/bytedance/deer-flow/commit/f78730ab86d1e3e9ae328ece9fcd8936b458f5c3 'fix(dev): exclude backend runtime state from reload (#4759)') [#4759](https://github.com/bytedance/deer-flow/pull/4759) [)](https://github.com/bytedance/deer-flow/commit/f78730ab86d1e3e9ae328ece9fcd8936b458f5c3 'fix(dev): exclude backend runtime state from reload (#4759)')

 [![AnnaSuSu](https://avatars.githubusercontent.com/u/64579968?v=4&size=32)](https://github.com/AnnaSuSu) [AnnaSuSu](https://github.com/bytedance/deer-flow/commits?author=AnnaSuSu)

 authoredAug 11, 2026

 ·

 7 / 8

 Verified

 [f78730a](https://github.com/bytedance/deer-flow/commit/f78730ab86d1e3e9ae328ece9fcd8936b458f5c3)View commit details

 Copy full SHA for f78730a

 Browse repository at this point

- #### [fix(frontend): reuse clipboard fallback for Lark auth (](https://github.com/bytedance/deer-flow/commit/9ba04bf80c2af38136d2e3c9e1738ffa0b6e64be 'fix(frontend): reuse clipboard fallback for Lark auth (#4767)') [#4767](https://github.com/bytedance/deer-flow/pull/4767) [)](https://github.com/bytedance/deer-flow/commit/9ba04bf80c2af38136d2e3c9e1738ffa0b6e64be 'fix(frontend): reuse clipboard fallback for Lark auth (#4767)')

 [![18062706139fcz](https://avatars.githubusercontent.com/u/90562015?v=4&size=32)](https://github.com/18062706139fcz) [18062706139fcz](https://github.com/bytedance/deer-flow/commits?author=18062706139fcz)

 authoredAug 11, 2026

 ·

 11 / 11

 Verified

 [9ba04bf](https://github.com/bytedance/deer-flow/commit/9ba04bf80c2af38136d2e3c9e1738ffa0b6e64be)View commit details

 Copy full SHA for 9ba04bf

 Browse repository at this point

- #### [fix(test):fix the unit test error on the main](https://github.com/bytedance/deer-flow/commit/23695a07a6b33238e1803cc1b071b3e9995615c9 'fix(test):fix the unit test error on the main')

 [![WillemJiang](https://avatars.githubusercontent.com/u/219644?v=4&size=32)](https://github.com/WillemJiang) [WillemJiang](https://github.com/bytedance/deer-flow/commits?author=WillemJiang)

 committedAug 11, 2026

 ·

 7 / 8

 [23695a0](https://github.com/bytedance/deer-flow/commit/23695a07a6b33238e1803cc1b071b3e9995615c9)View commit details

 Copy full SHA for 23695a0

 Browse repository at this point

- #### [build(deps): bump langgraph-checkpoint-postgres in /backend (](https://github.com/bytedance/deer-flow/commit/a6652956356f86de6776f2fc34833c3275931a1f 'build(deps): bump langgraph-checkpoint-postgres in /backend (#4747)

 Bumps [langgraph-checkpoint-postgres](https://github.com/langchain-ai/langgraph) from 3.1.0 to 3.1.1.
 - [Release notes](https://github.com/langchain-ai/langgraph/releases)
 - [Commits](https://github.com/langchain-ai/langgraph/compare/checkpointsqlite==3.1.0...checkpointsqlite==3.1.1)

 ---
 updated-dependencies:
 - dependency-name: langgraph-checkpoint-postgres
 dependency-version: 3.1.1
 dependency-type: direct:production
 ...

 Signed-off-by: dependabot[bot] <support@github.com>
 Co-authored-by: dependabot[bot] <49699333+dependabot[bot]@users.noreply.github.com>') [#4747](https://github.com/bytedance/deer-flow/pull/4747) [)](https://github.com/bytedance/deer-flow/commit/a6652956356f86de6776f2fc34833c3275931a1f 'build(deps): bump langgraph-checkpoint-postgres in /backend (#4747)

 Bumps [langgraph-checkpoint-postgres](https://github.com/langchain-ai/langgraph) from 3.1.0 to 3.1.1.
 - [Release notes](https://github.com/langchain-ai/langgraph/releases)
 - [Commits](https://github.com/langchain-ai/langgraph/compare/checkpointsqlite==3.1.0...checkpointsqlite==3.1.1)

 ---
 updated-dependencies:
 - dependency-name: langgraph-checkpoint-postgres
 dependency-version: 3.1.1
 dependency-type: direct:production
 ...

 Signed-off-by: dependabot[bot] <support@github.com>
 Co-authored-by: dependabot[bot] <49699333+dependabot[bot]@users.noreply.github.com>')

 Show description for a665295

 [![dependabot\[bot\]](https://avatars.githubusercontent.com/in/29110?v=4&size=32)](https://github.com/apps/dependabot) [dependabot\[bot\]](https://github.com/bytedance/deer-flow/commits?author=dependabot%5Bbot%5D)

 authoredAug 11, 2026

 ·

 10 / 11

 Verified

 [a665295](https://github.com/bytedance/deer-flow/commit/a6652956356f86de6776f2fc34833c3275931a1f)View commit details

 Copy full SHA for a665295

 Browse repository at this point

- #### [docs: add Chinese backend README (](https://github.com/bytedance/deer-flow/commit/36bd6764ad7ae01360da505f8ee72c7902c71f98 'docs: add Chinese backend README (#4763)') [#4763](https://github.com/bytedance/deer-flow/pull/4763) [)](https://github.com/bytedance/deer-flow/commit/36bd6764ad7ae01360da505f8ee72c7902c71f98 'docs: add Chinese backend README (#4763)')

 [![PoetryLin](https://avatars.githubusercontent.com/u/70308444?v=4&size=32)](https://github.com/PoetryLin) [PoetryLin](https://github.com/bytedance/deer-flow/commits?author=PoetryLin)

 authoredAug 11, 2026

 ·

 8 / 8

 Verified

 [36bd676](https://github.com/bytedance/deer-flow/commit/36bd6764ad7ae01360da505f8ee72c7902c71f98)View commit details

 Copy full SHA for 36bd676

 Browse repository at this point

- #### [feat(extensions): observe task lifecycle and system model calls (](https://github.com/bytedance/deer-flow/commit/7389331e6593c7f39cdacd9b078cf946e4e0b22d 'feat(extensions): observe task lifecycle and system model calls (#4684)

 * feat(extensions): observe task lifecycle and system model calls

 PR 1 (#4636) gave extensions a middleware chain, and a middleware only sees
 what passes through the agent graph. Two runtime surfaces stay invisible to
 it: when a lead run or a subagent begins and ends, and the DeerFlow-owned
 model calls made outside the graph. This slice adds both, with no new
 Gateway surface -- routers, services, and the reference extension stay in
 PR 3.

 Contract (deerflow-extension-api 0.1.1)
 ---------------------------------------
 Two contribution kinds join `middlewares` on the registry:
 `task_lifecycle` (`on_task_start` / `on_task_stop`, receiving a `TaskInfo`
 and a conservative `TaskOutcome` of completed / aborted / failed) and
 `system_model_observer` (`on_system_model_call`, receiving a
 `SystemOperationKind`, a `SystemModelRequest` snapshot, and a
 `SystemModelResult` carrying either the response or the provider exception
 plus a duration).

 `SystemModelRequest.messages` normalizes to a tuple at construction. Goal
 evaluation and memory extraction pass a message list while title generation
 and summarization pass one prompt string, and a bare `str` already satisfies
 `Sequence` -- without normalization an observer iterating `request.messages`
 would silently walk characters. Copying also makes the frozen snapshot
 immutable in fact rather than only by declaration, since observations may run
 after the call site returns and keeps mutating its own list.

 Registry marks and rollbacks become per-bucket and positional, so an
 `install()` that fails after registering two different kinds cannot leave one
 of them behind. `needs_task_store` now covers all three kinds: a deployment
 that registers only lifecycle hooks still gets a task store.

 Task lifecycle
 --------------
 The lead worker notifies start after the run has started and stop after
 completion persistence and the completion hook, but before clearing the
 finalizing barrier and publishing the stream end -- holding the barrier
 across stop is what keeps a same-thread replacement run from overlapping this
 task's lifecycle. Cancellation raised out of the stop notification is
 deferred, not propagated in place, so a cancelled run still clears the
 barrier and emits its end frame. A subagent with a parent `run_id` wraps its
 execution in the same pair inside `finally`, reporting `parent_task_id` so a
 delegation tree is reconstructable; a subagent without a `run_id` (embedded
 client, standalone LangGraph Server) logs and skips rather than inventing a
 parent. Contributors run in registration order inside one shared 3s budget
 and every failure is logged and failed open.

 System model calls
 ------------------
 Four kinds cover the model calls the middleware chain cannot see: goal
 evaluation, memory extraction, title generation, and summarization. Each site
 reports both terminal paths without changing the provider exception the host
 observes, short-circuits on `has_system_model_observers`, and passes the live
 task store when the runtime has one (detached work gets an isolated store).
 The sync summarization half stays unobserved on purpose -- it and its only
 host caller are the sync side of an async-only runtime, so notifying there
 would block a thread on a call site the host never reaches; the reason is
 recorded at the call site.

 The DeerMem backend must stay vendorable and cannot import the extension API,
 so it reports through a new `MemoryCallbacks.on_memory_llm_result` host hook
 that the DeerFlow-side callbacks translate into an observation.

 Notification loop
 -----------------
 Extension resources must be touched on the loop that created them, but
 subagents can execute on isolated loops and DeerMem runs on a worker thread.
 The Gateway registers its serving loop before any runtime dependency starts
 and resets it last through the exit stack, so every startup-failure and
 cancellation path is covered. Awaited hooks raised on another loop are
 dispatched across with `run_coroutine_threadsafe` and awaited under the same
 budget; synchronous sites submit fire-and-forget work. Shutdown stops
 accepting detached observations before the memory flush -- that flush runs on
 a worker thread and can emit memory observations -- while keeping the loop
 alive for awaited task hooks until run and subagent drain completes.

 Tests
 -----
 `test_extension_task_lifecycle.py`, `test_extension_subagent_lifecycle.py`,
 and `test_extension_system_model_calls.py` cover ordering, fail-open, budget
 exhaustion, snapshot binding under a concurrent singleton replacement, the
 loop-dispatch and shutdown-suspension paths, and both terminal paths at every
 call site. `test_gateway_run_drain_shutdown.py` pins the stop-before-barrier
 and drain ordering.

 * fix(extensions): decide notification fail-open by origin, observe cancellation

 `_notify_each` only guarded `Exception`, so a contributor letting a
 `CancelledError` escape — an extension implementing an internal timeout with
 cancellation, say — skipped its successors and reached the worker's
 deferred-interrupt path, ending an otherwise successful run as cancelled.
 Fail-open is about where a failure came from, not its base class: only a
 genuine cancellation of the host task increments `Task.cancelling()`, so
 propagate on that and contain everything else. `KeyboardInterrupt` /
 `SystemExit` still propagate.

 `observe_system_model_call` skipped observers on cancellation for the same
 base-class reason, leaving goal / title / summarization silent on a terminal
 path that is routine — interrupt/rollback admission and shutdown both cancel
 the run task, with the provider tokens already spent. Awaiting observers there
 is unreliable (a repeated cancel interrupts that await before any of them
 runs), so report through the same non-blocking submission the synchronous
 memory bridge uses, then propagate the cancellation untouched.

 DeerMem keeps `BaseException` around its provider call, now with the reason
 recorded: that path runs on a worker thread, where cancelling the awaiting
 side never interrupts the running thread, so `CancelledError` cannot arrive
 at all. Its host-hook wrapper narrows to `Exception` — only the hook's own
 failures are non-fatal, and an observability path must not swallow a process
 teardown signal.

 * fix(extensions): warn on budget exhaustion, scope observer logs by task, propagate teardown

 Review response on #4684:

 - The memory observation bridge caught BaseException, which would swallow
 a teardown signal raised while dispatching; it now catches Exception,
 matching the boundary the DeerMem-side call site documents and tests.
 - A notification-budget timeout raised mid-hook fell into the generic
 hook-failure path and logged an asyncio-internal traceback; it now logs
 a warning like the pre-hook budget skip, while a TimeoutError a
 contributor raises on its own stays classified as a hook failure.
 - System model observer logs passed the operation kind as the task id,
 so log lines said "task goal/title/..."; they now carry the task
 scope id alongside the kind.') [#4684](https://github.com/bytedance/deer-flow/pull/4684) [)](https://github.com/bytedance/deer-flow/commit/7389331e6593c7f39cdacd9b078cf946e4e0b22d 'feat(extensions): observe task lifecycle and system model calls (#4684)

 * feat(extensions): observe task lifecycle and system model calls

 PR 1 (#4636) gave extensions a middleware chain, and a middleware only sees
 what passes through the agent graph. Two runtime surfaces stay invisible to
 it: when a lead run or a subagent begins and ends, and the DeerFlow-owned
 model calls made outside the graph. This slice adds both, with no new
 Gateway surface -- routers, services, and the reference extension stay in
 PR 3.

 Contract (deerflow-extension-api 0.1.1)
 ---------------------------------------
 Two contribution kinds join `middlewares` on the registry:
 `task_lifecycle` (`on_task_start` / `on_task_stop`, receiving a `TaskInfo`
 and a conservative `TaskOutcome` of completed / aborted / failed) and
 `system_model_observer` (`on_system_model_call`, receiving a
 `SystemOperationKind`, a `SystemModelRequest` snapshot, and a
 `SystemModelResult` carrying either the response or the provider exception
 plus a duration).

 `SystemModelRequest.messages` normalizes to a tuple at construction. Goal
 evaluation and memory extraction pass a message list while title generation
 and summarization pass one prompt string, and a bare `str` already satisfies
 `Sequence` -- without normalization an observer iterating `request.messages`
 would silently walk characters. Copying also makes the frozen snapshot
 immutable in fact rather than only by declaration, since observations may run
 after the call site returns and keeps mutating its own list.

 Registry marks and rollbacks become per-bucket and positional, so an
 `install()` that fails after registering two different kinds cannot leave one
 of them behind. `needs_task_store` now covers all three kinds: a deployment
 that registers only lifecycle hooks still gets a task store.

 Task lifecycle
 --------------
 The lead worker notifies start after the run has started and stop after
 completion persistence and the completion hook, but before clearing the
 finalizing barrier and publishing the stream end -- holding the barrier
 across stop is what keeps a same-thread replacement run from overlapping this
 task's lifecycle. Cancellation raised out of the stop notification is
 deferred, not propagated in place, so a cancelled run still clears the
 barrier and emits its end frame. A subagent with a parent `run_id` wraps its
 execution in the same pair inside `finally`, reporting `parent_task_id` so a
 delegation tree is reconstructable; a subagent without a `run_id` (embedded
 client, standalone LangGraph Server) logs and skips rather than inventing a
 parent. Contributors run in registration order inside one shared 3s budget
 and every failure is logged and failed open.

 System model calls
 ------------------
 Four kinds cover the model calls the middleware chain cannot see: goal
 evaluation, memory extraction, title generation, and summarization. Each site
 reports both terminal paths without changing the provider exception the host
 observes, short-circuits on `has_system_model_observers`, and passes the live
 task store when the runtime has one (detached work gets an isolated store).
 The sync summarization half stays unobserved on purpose -- it and its only
 host caller are the sync side of an async-only runtime, so notifying there
 would block a thread on a call site the host never reaches; the reason is
 recorded at the call site.

 The DeerMem backend must stay vendorable and cannot import the extension API,
 so it reports through a new `MemoryCallbacks.on_memory_llm_result` host hook
 that the DeerFlow-side callbacks translate into an observation.

 Notification loop
 -----------------
 Extension resources must be touched on the loop that created them, but
 subagents can execute on isolated loops and DeerMem runs on a worker thread.
 The Gateway registers its serving loop before any runtime dependency starts
 and resets it last through the exit stack, so every startup-failure and
 cancellation path is covered. Awaited hooks raised on another loop are
 dispatched across with `run_coroutine_threadsafe` and awaited under the same
 budget; synchronous sites submit fire-and-forget work. Shutdown stops
 accepting detached observations before the memory flush -- that flush runs on
 a worker thread and can emit memory observations -- while keeping the loop
 alive for awaited task hooks until run and subagent drain completes.

 Tests
 -----
 `test_extension_task_lifecycle.py`, `test_extension_subagent_lifecycle.py`,
 and `test_extension_system_model_calls.py` cover ordering, fail-open, budget
 exhaustion, snapshot binding under a concurrent singleton replacement, the
 loop-dispatch and shutdown-suspension paths, and both terminal paths at every
 call site. `test_gateway_run_drain_shutdown.py` pins the stop-before-barrier
 and drain ordering.

 * fix(extensions): decide notification fail-open by origin, observe cancellation

 `_notify_each` only guarded `Exception`, so a contributor letting a
 `CancelledError` escape — an extension implementing an internal timeout with
 cancellation, say — skipped its successors and reached the worker's
 deferred-interrupt path, ending an otherwise successful run as cancelled.
 Fail-open is about where a failure came from, not its base class: only a
 genuine cancellation of the host task increments `Task.cancelling()`, so
 propagate on that and contain everything else. `KeyboardInterrupt` /
 `SystemExit` still propagate.

 `observe_system_model_call` skipped observers on cancellation for the same
 base-class reason, leaving goal / title / summarization silent on a terminal
 path that is routine — interrupt/rollback admission and shutdown both cancel
 the run task, with the provider tokens already spent. Awaiting observers there
 is unreliable (a repeated cancel interrupts that await before any of them
 runs), so report through the same non-blocking submission the synchronous
 memory bridge uses, then propagate the cancellation untouched.

 DeerMem keeps `BaseException` around its provider call, now with the reason
 recorded: that path runs on a worker thread, where cancelling the awaiting
 side never interrupts the running thread, so `CancelledError` cannot arrive
 at all. Its host-hook wrapper narrows to `Exception` — only the hook's own
 failures are non-fatal, and an observability path must not swallow a process
 teardown signal.

 * fix(extensions): warn on budget exhaustion, scope observer logs by task, propagate teardown

 Review response on #4684:

 - The memory observation bridge caught BaseException, which would swallow
 a teardown signal raised while dispatching; it now catches Exception,
 matching the boundary the DeerMem-side call site documents and tests.
 - A notification-budget timeout raised mid-hook fell into the generic
 hook-failure path and logged an asyncio-internal traceback; it now logs
 a warning like the pre-hook budget skip, while a TimeoutError a
 contributor raises on its own stays classified as a hook failure.
 - System model observer logs passed the operation kind as the task id,
 so log lines said "task goal/title/..."; they now carry the task
 scope id alongside the kind.')

 Show description for 7389331

 [![ggnnggez](https://avatars.githubusercontent.com/u/88081804?v=4&size=32)](https://github.com/ggnnggez) [ggnnggez](https://github.com/bytedance/deer-flow/commits?author=ggnnggez)

 authoredAug 11, 2026

 ·

 9 / 11

 Verified

 [7389331](https://github.com/bytedance/deer-flow/commit/7389331e6593c7f39cdacd9b078cf946e4e0b22d)View commit details

 Copy full SHA for 7389331

 Browse repository at this point

- #### [feat(mcp): add official OpenViking tools integration (](https://github.com/bytedance/deer-flow/commit/a263af284527749b714535f1776f0247966ec8bb 'feat(mcp): add official OpenViking tools integration (#4745)

 * feat(mcp): add OpenViking tools integration

 * fix(mcp): warn on ineffective tool overrides

 * docs(mcp): clarify OpenViking resource removal

 * fix(mcp): expose native OpenViking forget tool

 * docs(mcp): document OpenViking forget guardrail') [#4745](https://github.com/bytedance/deer-flow/pull/4745) [)](https://github.com/bytedance/deer-flow/commit/a263af284527749b714535f1776f0247966ec8bb 'feat(mcp): add official OpenViking tools integration (#4745)

 * feat(mcp): add OpenViking tools integration

 * fix(mcp): warn on ineffective tool overrides

 * docs(mcp): clarify OpenViking resource removal

 * fix(mcp): expose native OpenViking forget tool

 * docs(mcp): document OpenViking forget guardrail')

 Show description for a263af2

 [![ehz0ah](https://avatars.githubusercontent.com/u/130889443?v=4&size=32)](https://github.com/ehz0ah) [ehz0ah](https://github.com/bytedance/deer-flow/commits?author=ehz0ah)

 authoredAug 11, 2026

 ·

 8 / 8

 Verified

 [a263af2](https://github.com/bytedance/deer-flow/commit/a263af284527749b714535f1776f0247966ec8bb)View commit details

 Copy full SHA for a263af2

 Browse repository at this point

- #### [fix(todo-middleware): call super in wrap\_model\_call to restore write\_todos prompt injection (](https://github.com/bytedance/deer-flow/commit/2bb230b334b6a925c4359a3984b9d1c94ad07aa4 'fix(todo-middleware): call super in wrap_model_call to restore write_todos prompt injection (#4714) (#4735)

 * fix(todo-middleware): call super in wrap_model_call to restore write_todos prompt injection (#4714)

 * test(todo-middleware): add async no-reminder system-prompt passthrough test (review feedback)') [#4714](https://github.com/bytedance/deer-flow/issues/4714) [) (](https://github.com/bytedance/deer-flow/commit/2bb230b334b6a925c4359a3984b9d1c94ad07aa4 'fix(todo-middleware): call super in wrap_model_call to restore write_todos prompt injection (#4714) (#4735)

 * fix(todo-middleware): call super in wrap_model_call to restore write_todos prompt injection (#4714)

 * test(todo-middleware): add async no-reminder system-prompt passthrough test (review feedback)') [#4735](https://github.com/bytedance/deer-flow/pull/4735) [)](https://github.com/bytedance/deer-flow/commit/2bb230b334b6a925c4359a3984b9d1c94ad07aa4 'fix(todo-middleware): call super in wrap_model_call to restore write_todos prompt injection (#4714) (#4735)

 * fix(todo-middleware): call super in wrap_model_call to restore write_todos prompt injection (#4714)

 * test(todo-middleware): add async no-reminder system-prompt passthrough test (review feedback)')

 Show description for 2bb230b

 [![ggnnggez](https://avatars.githubusercontent.com/u/88081804?v=4&size=32)](https://github.com/ggnnggez) [ggnnggez](https://github.com/bytedance/deer-flow/commits?author=ggnnggez)

 authoredAug 11, 2026

 ·

 11 / 11

 Verified

 [2bb230b](https://github.com/bytedance/deer-flow/commit/2bb230b334b6a925c4359a3984b9d1c94ad07aa4)View commit details

 Copy full SHA for 2bb230b

 Browse repository at this point

### Commits on Aug 10, 2026

- #### [build(deps): bump nanoid from 5.1.6 to 5.1.16 in /frontend (](https://github.com/bytedance/deer-flow/commit/21e2cfd7197eb8a671bf28a7468bac661f77a472 'build(deps): bump nanoid from 5.1.6 to 5.1.16 in /frontend (#4748)

 Bumps [nanoid](https://github.com/ai/nanoid) from 5.1.6 to 5.1.16.
 - [Release notes](https://github.com/ai/nanoid/releases)
 - [Changelog](https://github.com/ai/nanoid/blob/main/CHANGELOG.md)
 - [Commits](https://github.com/ai/nanoid/compare/5.1.6...5.1.16)

 ---
 updated-dependencies:
 - dependency-name: nanoid
 dependency-version: 5.1.16
 dependency-type: direct:production
 ...

 Signed-off-by: dependabot[bot] <support@github.com>
 Co-authored-by: dependabot[bot] <49699333+dependabot[bot]@users.noreply.github.com>') [#4748](https://github.com/bytedance/deer-flow/pull/4748) [)](https://github.com/bytedance/deer-flow/commit/21e2cfd7197eb8a671bf28a7468bac661f77a472 'build(deps): bump nanoid from 5.1.6 to 5.1.16 in /frontend (#4748)

 Bumps [nanoid](https://github.com/ai/nanoid) from 5.1.6 to 5.1.16.
 - [Release notes](https://github.com/ai/nanoid/releases)
 - [Changelog](https://github.com/ai/nanoid/blob/main/CHANGELOG.md)
 - [Commits](https://github.com/ai/nanoid/compare/5.1.6...5.1.16)

 ---
 updated-dependencies:
 - dependency-name: nanoid
 dependency-version: 5.1.16
 dependency-type: direct:production
 ...

 Signed-off-by: dependabot[bot] <support@github.com>
 Co-authored-by: dependabot[bot] <49699333+dependabot[bot]@users.noreply.github.com>')

 Show description for 21e2cfd

 [![dependabot\[bot\]](https://avatars.githubusercontent.com/in/29110?v=4&size=32)](https://github.com/apps/dependabot) [dependabot\[bot\]](https://github.com/bytedance/deer-flow/commits?author=dependabot%5Bbot%5D)

 authoredAug 10, 2026

 ·

 10 / 10

 Verified

 [21e2cfd](https://github.com/bytedance/deer-flow/commit/21e2cfd7197eb8a671bf28a7468bac661f77a472)View commit details

 Copy full SHA for 21e2cfd

 Browse repository at this point

- #### [fix(lark): keep CLI lock directory writable in sandboxes (](https://github.com/bytedance/deer-flow/commit/17531d7c118d6111b863f945ff910a7889a235b0 'fix(lark): keep CLI lock directory writable in sandboxes (#4701)

 * fix(lark): provide writable CLI lock directory

 * test(lark): pin nested lock mount ordering') [#4701](https://github.com/bytedance/deer-flow/pull/4701) [)](https://github.com/bytedance/deer-flow/commit/17531d7c118d6111b863f945ff910a7889a235b0 'fix(lark): keep CLI lock directory writable in sandboxes (#4701)

 * fix(lark): provide writable CLI lock directory

 * test(lark): pin nested lock mount ordering')

 Show description for 17531d7

 [![Creeper998](https://avatars.githubusercontent.com/u/98166916?v=4&size=32)](https://github.com/Creeper998) [Creeper998](https://github.com/bytedance/deer-flow/commits?author=Creeper998)

 authoredAug 10, 2026

 ·

 10 / 10

 Verified

 [17531d7](https://github.com/bytedance/deer-flow/commit/17531d7c118d6111b863f945ff910a7889a235b0)View commit details

 Copy full SHA for 17531d7

 Browse repository at this point

### Commits on Aug 9, 2026

- #### [feat(integrations): support switching Lark app credentials (](https://github.com/bytedance/deer-flow/commit/e401ae2d7b8e4fc73fc82a1143c989c54f3f4de6 'feat(integrations): support switching Lark app credentials (#4703)

 * feat(integrations): support switching Lark app credentials

 * fix(integrations): harden Lark app switching

 * refactor(integrations): simplify Lark switch flow

 * fix(integrations): reject superseded Lark flows

 * test(integrations): pass Lark flow generation

 * fix(integrations): preserve pending Lark flows

 ---------

 Co-authored-by: Willem Jiang <willem.jiang@gmail.com>') [#4703](https://github.com/bytedance/deer-flow/pull/4703) [)](https://github.com/bytedance/deer-flow/commit/e401ae2d7b8e4fc73fc82a1143c989c54f3f4de6 'feat(integrations): support switching Lark app credentials (#4703)

 * feat(integrations): support switching Lark app credentials

 * fix(integrations): harden Lark app switching

 * refactor(integrations): simplify Lark switch flow

 * fix(integrations): reject superseded Lark flows

 * test(integrations): pass Lark flow generation

 * fix(integrations): preserve pending Lark flows

 ---------

 Co-authored-by: Willem Jiang <willem.jiang@gmail.com>')

 Show description for e401ae2

 ![18062706139fcz](https://avatars.githubusercontent.com/u/90562015?v=4&size=32)![WillemJiang](https://avatars.githubusercontent.com/u/219644?v=4&size=32)

 [18062706139fcz](https://github.com/bytedance/deer-flow/commits?author=18062706139fcz)

 and

 [WillemJiang](https://github.com/bytedance/deer-flow/commits?author=WillemJiang)

 authoredAug 9, 2026

 ·

 11 / 11

 Verified

 [e401ae2](https://github.com/bytedance/deer-flow/commit/e401ae2d7b8e4fc73fc82a1143c989c54f3f4de6)View commit details

 Copy full SHA for e401ae2

 Browse repository at this point

### Commits on Aug 8, 2026

- #### [fix(dingtalk): strip leading mentions before command classification (](https://github.com/bytedance/deer-flow/commit/e16ef2969b1446162e19af7bdde1446674851e66 'fix(dingtalk): strip leading mentions before command classification (#4724)

 Group @bot /command messages are classified as commands like Feishu.') [#4724](https://github.com/bytedance/deer-flow/pull/4724) [)](https://github.com/bytedance/deer-flow/commit/e16ef2969b1446162e19af7bdde1446674851e66 'fix(dingtalk): strip leading mentions before command classification (#4724)

 Group @bot /command messages are classified as commands like Feishu.')

 Show description for e16ef29

 [![richardmilles](https://avatars.githubusercontent.com/u/76790700?v=4&size=32)](https://github.com/richardmilles) [richardmilles](https://github.com/bytedance/deer-flow/commits?author=richardmilles)

 authoredAug 8, 2026

 ·

 8 / 8

 Verified

 [e16ef29](https://github.com/bytedance/deer-flow/commit/e16ef2969b1446162e19af7bdde1446674851e66)View commit details

 Copy full SHA for e16ef29

 Browse repository at this point

- #### [fix(middleware): skip raw tool-call fallback when invalid view carries the same call (](https://github.com/bytedance/deer-flow/commit/7b576096564475da7a12268610d63954014d89ec 'fix(middleware): skip raw tool-call fallback when invalid view carries the same call (#4693)

 DanglingToolCallMiddleware._message_tool_calls collected the raw
 additional_kwargs tool_calls payload whenever structured tool_calls was
 empty, even when invalid_tool_calls was non-empty. The raw payload is a
 fallback serialization of the SAME calls — the OpenAI serializer reaches
 for it only once both structured views are empty, which is exactly the
 gating _normalize_tool_call_ids documents and implements. Collecting it
 alongside a same-id invalid entry counted the call twice and emitted two
 placeholder ToolMessages for one id — the duplicate-id shape strict
 OpenAI-compatible providers reject with HTTP 400, the failure this
 middleware exists to prevent.

 Gate the raw collection on both structured views being empty, aligning
 _message_tool_calls with _normalize_tool_call_ids.') [#4693](https://github.com/bytedance/deer-flow/pull/4693) [)](https://github.com/bytedance/deer-flow/commit/7b576096564475da7a12268610d63954014d89ec 'fix(middleware): skip raw tool-call fallback when invalid view carries the same call (#4693)

 DanglingToolCallMiddleware._message_tool_calls collected the raw
 additional_kwargs tool_calls payload whenever structured tool_calls was
 empty, even when invalid_tool_calls was non-empty. The raw payload is a
 fallback serialization of the SAME calls — the OpenAI serializer reaches
 for it only once both structured views are empty, which is exactly the
 gating _normalize_tool_call_ids documents and implements. Collecting it
 alongside a same-id invalid entry counted the call twice and emitted two
 placeholder ToolMessages for one id — the duplicate-id shape strict
 OpenAI-compatible providers reject with HTTP 400, the failure this
 middleware exists to prevent.

 Gate the raw collection on both structured views being empty, aligning
 _message_tool_calls with _normalize_tool_call_ids.')

 Show description for 7b57609

 [![Baldwinzc](https://avatars.githubusercontent.com/u/56501736?v=4&size=32)](https://github.com/Baldwinzc) [Baldwinzc](https://github.com/bytedance/deer-flow/commits?author=Baldwinzc)

 authoredAug 8, 2026

 ·

 9 / 10

 Verified

 [7b57609](https://github.com/bytedance/deer-flow/commit/7b576096564475da7a12268610d63954014d89ec)View commit details

 Copy full SHA for 7b57609

 Browse repository at this point

- #### [docs(lark): drop dead link to uncommitted sandbox init spec (](https://github.com/bytedance/deer-flow/commit/295d7c2abcf77e995951627afdd531791369b9d0 'docs(lark): drop dead link to uncommitted sandbox init spec (#4705)

 The docker/lark-cli-init/README.md referenced
 docs/superpowers/specs/2026-07-21-lark-sandbox-init-container-design.md,
 but that design spec was never committed to the repository — it is absent
 across the full git history. The link has been broken since it was
 introduced in #3971. The README already documents the init-container
 behavior standalone, so the dangling reference is removed.

 Co-authored-by: icn5381 <255778606+icn5381@users.noreply.github.com>') [#4705](https://github.com/bytedance/deer-flow/pull/4705) [)](https://github.com/bytedance/deer-flow/commit/295d7c2abcf77e995951627afdd531791369b9d0 'docs(lark): drop dead link to uncommitted sandbox init spec (#4705)

 The docker/lark-cli-init/README.md referenced
 docs/superpowers/specs/2026-07-21-lark-sandbox-init-container-design.md,
 but that design spec was never committed to the repository — it is absent
 across the full git history. The link has been broken since it was
 introduced in #3971. The README already documents the init-container
 behavior standalone, so the dangling reference is removed.

 Co-authored-by: icn5381 <255778606+icn5381@users.noreply.github.com>')

 Show description for 295d7c2

 [![icn5381](https://avatars.githubusercontent.com/u/255778606?v=4&size=32)](https://github.com/icn5381) [icn5381](https://github.com/bytedance/deer-flow/commits?author=icn5381)

 authoredAug 8, 2026

 ·

 8 / 8

 Verified

 [295d7c2](https://github.com/bytedance/deer-flow/commit/295d7c2abcf77e995951627afdd531791369b9d0)View commit details

 Copy full SHA for 295d7c2

 Browse repository at this point

- #### [fix(agents): make SQL store signatures content-sensitive (](https://github.com/bytedance/deer-flow/commit/79101269238fe53db5a56f2a1cf3224d810d13fb 'fix(agents): make SQL store signatures content-sensitive (#4709)') [#4709](https://github.com/bytedance/deer-flow/pull/4709) [)](https://github.com/bytedance/deer-flow/commit/79101269238fe53db5a56f2a1cf3224d810d13fb 'fix(agents): make SQL store signatures content-sensitive (#4709)')

 [![AoHanBei](https://avatars.githubusercontent.com/u/170841481?v=4&size=32)](https://github.com/AoHanBei) [AoHanBei](https://github.com/bytedance/deer-flow/commits?author=AoHanBei)

 authoredAug 8, 2026

 ·

 11 / 11

 Verified

 [7910126](https://github.com/bytedance/deer-flow/commit/79101269238fe53db5a56f2a1cf3224d810d13fb)View commit details

 Copy full SHA for 7910126

 Browse repository at this point

- #### [build(deps): bump langgraph-checkpoint-sqlite in /backend (](https://github.com/bytedance/deer-flow/commit/95989dfaae0198d6cef90f829b7807d2c6207e99 'build(deps): bump langgraph-checkpoint-sqlite in /backend (#4738)

 Bumps [langgraph-checkpoint-sqlite](https://github.com/langchain-ai/langgraph) from 3.1.0 to 3.1.1.
 - [Release notes](https://github.com/langchain-ai/langgraph/releases)
 - [Commits](https://github.com/langchain-ai/langgraph/compare/checkpointsqlite==3.1.0...checkpointsqlite==3.1.1)

 ---
 updated-dependencies:
 - dependency-name: langgraph-checkpoint-sqlite
 dependency-version: 3.1.1
 dependency-type: direct:production
 ...

 Signed-off-by: dependabot[bot] <support@github.com>
 Co-authored-by: dependabot[bot] <49699333+dependabot[bot]@users.noreply.github.com>') [#4738](https://github.com/bytedance/deer-flow/pull/4738) [)](https://github.com/bytedance/deer-flow/commit/95989dfaae0198d6cef90f829b7807d2c6207e99 'build(deps): bump langgraph-checkpoint-sqlite in /backend (#4738)

 Bumps [langgraph-checkpoint-sqlite](https://github.com/langchain-ai/langgraph) from 3.1.0 to 3.1.1.
 - [Release notes](https://github.com/langchain-ai/langgraph/releases)
 - [Commits](https://github.com/langchain-ai/langgraph/compare/checkpointsqlite==3.1.0...checkpointsqlite==3.1.1)

 ---
 updated-dependencies:
 - dependency-name: langgraph-checkpoint-sqlite
 dependency-version: 3.1.1
 dependency-type: direct:production
 ...

 Signed-off-by: dependabot[bot] <support@github.com>
 Co-authored-by: dependabot[bot] <49699333+dependabot[bot]@users.noreply.github.com>')

 Show description for 95989df

 [![dependabot\[bot\]](https://avatars.githubusercontent.com/in/29110?v=4&size=32)](https://github.com/apps/dependabot) [dependabot\[bot\]](https://github.com/bytedance/deer-flow/commits?author=dependabot%5Bbot%5D)

 authoredAug 8, 2026

 ·

 11 / 11

 Verified

 [95989df](https://github.com/bytedance/deer-flow/commit/95989dfaae0198d6cef90f829b7807d2c6207e99)View commit details

 Copy full SHA for 95989df

 Browse repository at this point

- #### [build(deps): bump h2 from 4.3.0 to 4.4.1 in /backend (](https://github.com/bytedance/deer-flow/commit/bbc4b48c32eef10fe5d3802f7653a5d3eff40461 'build(deps): bump h2 from 4.3.0 to 4.4.1 in /backend (#4737)

 Bumps [h2](https://github.com/python-hyper/h2) from 4.3.0 to 4.4.1.
 - [Changelog](https://github.com/python-hyper/h2/blob/master/CHANGELOG.rst)
 - [Commits](https://github.com/python-hyper/h2/compare/v4.3.0...v4.4.1)

 ---
 updated-dependencies:
 - dependency-name: h2
 dependency-version: 4.4.1
 dependency-type: indirect
 ...

 Signed-off-by: dependabot[bot] <support@github.com>
 Co-authored-by: dependabot[bot] <49699333+dependabot[bot]@users.noreply.github.com>') [#4737](https://github.com/bytedance/deer-flow/pull/4737) [)](https://github.com/bytedance/deer-flow/commit/bbc4b48c32eef10fe5d3802f7653a5d3eff40461 'build(deps): bump h2 from 4.3.0 to 4.4.1 in /backend (#4737)

 Bumps [h2](https://github.com/python-hyper/h2) from 4.3.0 to 4.4.1.
 - [Changelog](https://github.com/python-hyper/h2/blob/master/CHANGELOG.rst)
 - [Commits](https://github.com/python-hyper/h2/compare/v4.3.0...v4.4.1)

 ---
 updated-dependencies:
 - dependency-name: h2
 dependency-version: 4.4.1
 dependency-type: indirect
 ...

 Signed-off-by: dependabot[bot] <support@github.com>
 Co-authored-by: dependabot[bot] <49699333+dependabot[bot]@users.noreply.github.com>')

 Show description for bbc4b48

 [![dependabot\[bot\]](https://avatars.githubusercontent.com/in/29110?v=4&size=32)](https://github.com/apps/dependabot) [dependabot\[bot\]](https://github.com/bytedance/deer-flow/commits?author=dependabot%5Bbot%5D)

 authoredAug 8, 2026

 ·

 8 / 9

 Verified

 [bbc4b48](https://github.com/bytedance/deer-flow/commit/bbc4b48c32eef10fe5d3802f7653a5d3eff40461)View commit details

 Copy full SHA for bbc4b48

 Browse repository at this point

- #### [feat(mcp): add durable task runtime foundation (](https://github.com/bytedance/deer-flow/commit/e9387394bc10bbbf7194e8a136b24265ef244e6b 'feat(mcp): add durable task runtime foundation (#4665)

 * feat(mcp): add durable task runtime foundation

 * fix(chart): sync embedded config version

 * fix(mcp): isolate task polls during shutdown

 * feat(mcp): track consecutive poll errors on mcp_tasks

 poll_attempt_count grows on every claim (successful polls included), so it
 cannot drive a failure backoff without misjudging normal long tasks. Add
 consecutive_poll_error_count: incremented when a claim is released after a
 poll error, reset to zero by any applied snapshot. The backoff/terminal
 policy that consumes it lands with the first concrete driver.

 * fix(mcp): harden durable task lifecycle

 * fix(mcp): preserve tracked task on dedup conflict

 ---------

 Co-authored-by: Willem Jiang <willem.jiang@gmail.com>') [#4665](https://github.com/bytedance/deer-flow/pull/4665) [)](https://github.com/bytedance/deer-flow/commit/e9387394bc10bbbf7194e8a136b24265ef244e6b 'feat(mcp): add durable task runtime foundation (#4665)

 * feat(mcp): add durable task runtime foundation

 * fix(chart): sync embedded config version

 * fix(mcp): isolate task polls during shutdown

 * feat(mcp): track consecutive poll errors on mcp_tasks

 poll_attempt_count grows on every claim (successful polls included), so it
 cannot drive a failure backoff without misjudging normal long tasks. Add
 consecutive_poll_error_count: incremented when a claim is released after a
 poll error, reset to zero by any applied snapshot. The backoff/terminal
 policy that consumes it lands with the first concrete driver.

 * fix(mcp): harden durable task lifecycle

 * fix(mcp): preserve tracked task on dedup conflict

 ---------

 Co-authored-by: Willem Jiang <willem.jiang@gmail.com>')

 Show description for e938739

 ![AnnaSuSu](https://avatars.githubusercontent.com/u/64579968?v=4&size=32)![WillemJiang](https://avatars.githubusercontent.com/u/219644?v=4&size=32)

 [AnnaSuSu](https://github.com/bytedance/deer-flow/commits?author=AnnaSuSu)

 and

 [WillemJiang](https://github.com/bytedance/deer-flow/commits?author=WillemJiang)

 authoredAug 8, 2026

 ·

 9 / 10

 Verified

 [e938739](https://github.com/bytedance/deer-flow/commit/e9387394bc10bbbf7194e8a136b24265ef244e6b)View commit details

 Copy full SHA for e938739

 Browse repository at this point

### Commits on Aug 7, 2026

- #### [feat(frontend): add Browser Live to Custom Agent chats (](https://github.com/bytedance/deer-flow/commit/e5c62cab5acd9b8bf9e33533e493f17a7180db76 'feat(frontend): add Browser Live to Custom Agent chats (#4719)

 * feat(frontend): add Browser Live to Custom Agent chats

 * test(frontend): cover mock Custom Agent Browser Live') [#4719](https://github.com/bytedance/deer-flow/pull/4719) [)](https://github.com/bytedance/deer-flow/commit/e5c62cab5acd9b8bf9e33533e493f17a7180db76 'feat(frontend): add Browser Live to Custom Agent chats (#4719)

 * feat(frontend): add Browser Live to Custom Agent chats

 * test(frontend): cover mock Custom Agent Browser Live')

 Show description for e5c62ca

 [![AnnaSuSu](https://avatars.githubusercontent.com/u/64579968?v=4&size=32)](https://github.com/AnnaSuSu) [AnnaSuSu](https://github.com/bytedance/deer-flow/commits?author=AnnaSuSu)

 authoredAug 7, 2026

 ·

 10 / 10

 Verified

 [e5c62ca](https://github.com/bytedance/deer-flow/commit/e5c62cab5acd9b8bf9e33533e493f17a7180db76)View commit details

 Copy full SHA for e5c62ca

 Browse repository at this point

- #### [refactor(memory): use official OpenViking adapter (](https://github.com/bytedance/deer-flow/commit/6556d09d7f3800ca570820819455c39b4584482f 'refactor(memory): use official OpenViking adapter (#4707)

 * refactor(memory): use official OpenViking adapter

 * fix(memory): preserve OpenViking recall behavior

 * fix(memory): ignore ambient OpenViking headers') [#4707](https://github.com/bytedance/deer-flow/pull/4707) [)](https://github.com/bytedance/deer-flow/commit/6556d09d7f3800ca570820819455c39b4584482f 'refactor(memory): use official OpenViking adapter (#4707)

 * refactor(memory): use official OpenViking adapter

 * fix(memory): preserve OpenViking recall behavior

 * fix(memory): ignore ambient OpenViking headers')

 Show description for 6556d09

 [![ehz0ah](https://avatars.githubusercontent.com/u/130889443?v=4&size=32)](https://github.com/ehz0ah) [ehz0ah](https://github.com/bytedance/deer-flow/commits?author=ehz0ah)

 authoredAug 7, 2026

 ·

 13 / 13

 Verified

 [6556d09](https://github.com/bytedance/deer-flow/commit/6556d09d7f3800ca570820819455c39b4584482f)View commit details

 Copy full SHA for 6556d09

 Browse repository at this point

### Commits on Aug 5, 2026

- #### [fix(mcp): bring-up has no timeout and externalized tool outputs are counted as undelivered artifacts (](https://github.com/bytedance/deer-flow/commit/99c926b7bbcd0570870bc24ceb13ab934935f49c 'fix(mcp): bring-up has no timeout and externalized tool outputs are counted as undelivered artifacts (#4657)

 * fix: bound MCP server bring-up timeouts and exclude externalized tool outputs from delivery verification

 Two related robustness fixes:

 1. MCP server bring-up was unbounded. tool_call_timeout only covered
 session.call_tool(); tool discovery (subprocess spawn + initialize +
 tools/list) and persistent stdio session initialization could hang
 forever, blocking agent construction (and on the Gateway event loop,
 the whole process). Add a per-server session_init_timeout
 (default DEFAULT_MCP_SESSION_INIT_TIMEOUT = 60s, null disables) that
 bounds both discovery and pooled-session initialization. The session
 pool's existing cancellation handling tears down a session stuck
 mid-creation in its own task.

 2. ToolOutputBudgetMiddleware externalizes oversized tool outputs into
 outputs/.tool-results/ (configurable tool_output.storage_subdir). The
 workspace-change scanner and run delivery verification counted those
 files as produced artifacts, so any run that externalized a tool output
 without also presenting a real artifact failed with
 "Artifact delivery incomplete". Exclude TOOL_RESULTS_DIRNAME via a
 shared constant (mirroring BROWSER_FRAMES_DIRNAME) and thread the
 configured storage_subdir through snapshot capture so both
 workspace-changes events and delivery verification stay clean.

 * review: enforce single-segment tool_output.storage_subdir; document discovery-timeout cleanup

 Address review feedback:

 1. A custom tool_output.storage_subdir with a path separator (e.g.
 cache/tool-results) silently no-oped the workspace-scanner exclusion:
 os.walk yields one-segment dirnames, so a nested value never matched and
 its files were counted as produced artifacts again. ToolOutputConfig now
 validates storage_subdir as a single directory name (rejects separators,
 .., absolute, empty) with tests, so the exclusion is always sound.

 2. The discovery-timeout path now documents why cancellation is safe, mirroring
 the session-init note: discovery runs inside the adapter's nested async
 context managers, and stdio_client's finally terminates the process tree
 (SIGTERM->SIGKILL on POSIX, process-tree on Windows), so a timed-out npx
 subprocess and its children are reaped rather than accumulating.

 * review: log session-init timeouts and align API response model default with runtime config

 Address second-round review feedback:

 1. A session-init timeout raised TimeoutError without any log, unlike the
 discovery timeout which logs a WARNING. Wrap the bounded get_session in a
 try/except that logs the timeout (server name + seconds) and re-raises, so
 operators can diagnose tool-call failures caused by hung MCP sessions.

 2. McpServerConfigResponse.session_init_timeout defaulted to None while
 McpServerConfig defaults to 60s: a server created via PUT /api/mcp/config
 without the field was persisted with null (no timeout) while the same
 server created in the config file got 60s. Align the response-model default
 to DEFAULT_MCP_SESSION_INIT_TIMEOUT so API-created and file-created servers
 behave the same; an explicit null still opts out.

 * review: narrow the discovery-timeout handler to the bounded wait_for path

 The except TimeoutError clause covered both the bounded wait_for branch and
 the bare discovery branch. With session_init_timeout opted out (None), a
 TimeoutError raised by discovery itself would hit the %.1f format with None:
 logging raises TypeError internally, the WARNING is silently dropped, and a
 --- Logging error --- traceback goes to stderr.

 Narrow the handler to wrap only the wait_for call, where the branch condition
 guarantees the timeout value is not None. A discovery-internal TimeoutError on
 the opted-out path now falls through to the generic failure handler and is
 reported as 'tool discovery failed' with exc_info. Covered by a regression
 test that asserts the skip is reported without any broken format.') [#4657](https://github.com/bytedance/deer-flow/pull/4657) [)](https://github.com/bytedance/deer-flow/commit/99c926b7bbcd0570870bc24ceb13ab934935f49c 'fix(mcp): bring-up has no timeout and externalized tool outputs are counted as undelivered artifacts (#4657)

 * fix: bound MCP server bring-up timeouts and exclude externalized tool outputs from delivery verification

 Two related robustness fixes:

 1. MCP server bring-up was unbounded. tool_call_timeout only covered
 session.call_tool(); tool discovery (subprocess spawn + initialize +
 tools/list) and persistent stdio session initialization could hang
 forever, blocking agent construction (and on the Gateway event loop,
 the whole process). Add a per-server session_init_timeout
 (default DEFAULT_MCP_SESSION_INIT_TIMEOUT = 60s, null disables) that
 bounds both discovery and pooled-session initialization. The session
 pool's existing cancellation handling tears down a session stuck
 mid-creation in its own task.

 2. ToolOutputBudgetMiddleware externalizes oversized tool outputs into
 outputs/.tool-results/ (configurable tool_output.storage_subdir). The
 workspace-change scanner and run delivery verification counted those
 files as produced artifacts, so any run that externalized a tool output
 without also presenting a real artifact failed with
 "Artifact delivery incomplete". Exclude TOOL_RESULTS_DIRNAME via a
 shared constant (mirroring BROWSER_FRAMES_DIRNAME) and thread the
 configured storage_subdir through snapshot capture so both
 workspace-changes events and delivery verification stay clean.

 * review: enforce single-segment tool_output.storage_subdir; document discovery-timeout cleanup

 Address review feedback:

 1. A custom tool_output.storage_subdir with a path separator (e.g.
 cache/tool-results) silently no-oped the workspace-scanner exclusion:
 os.walk yields one-segment dirnames, so a nested value never matched and
 its files were counted as produced artifacts again. ToolOutputConfig now
 validates storage_subdir as a single directory name (rejects separators,
 .., absolute, empty) with tests, so the exclusion is always sound.

 2. The discovery-timeout path now documents why cancellation is safe, mirroring
 the session-init note: discovery runs inside the adapter's nested async
 context managers, and stdio_client's finally terminates the process tree
 (SIGTERM->SIGKILL on POSIX, process-tree on Windows), so a timed-out npx
 subprocess and its children are reaped rather than accumulating.

 * review: log session-init timeouts and align API response model default with runtime config

 Address second-round review feedback:

 1. A session-init timeout raised TimeoutError without any log, unlike the
 discovery timeout which logs a WARNING. Wrap the bounded get_session in a
 try/except that logs the timeout (server name + seconds) and re-raises, so
 operators can diagnose tool-call failures caused by hung MCP sessions.

 2. McpServerConfigResponse.session_init_timeout defaulted to None while
 McpServerConfig defaults to 60s: a server created via PUT /api/mcp/config
 without the field was persisted with null (no timeout) while the same
 server created in the config file got 60s. Align the response-model default
 to DEFAULT_MCP_SESSION_INIT_TIMEOUT so API-created and file-created servers
 behave the same; an explicit null still opts out.

 * review: narrow the discovery-timeout handler to the bounded wait_for path

 The except TimeoutError clause covered both the bounded wait_for branch and
 the bare discovery branch. With session_init_timeout opted out (None), a
 TimeoutError raised by discovery itself would hit the %.1f format with None:
 logging raises TypeError internally, the WARNING is silently dropped, and a
 --- Logging error --- traceback goes to stderr.

 Narrow the handler to wrap only the wait_for call, where the branch condition
 guarantees the timeout value is not None. A discovery-internal TimeoutError on
 the opted-out path now falls through to the generic failure handler and is
 reported as 'tool discovery failed' with exc_info. Covered by a regression
 test that asserts the skip is reported without any broken format.')

 Show description for 99c926b

 [![lllyfff](https://avatars.githubusercontent.com/u/122260771?v=4&size=32)](https://github.com/lllyfff) [lllyfff](https://github.com/bytedance/deer-flow/commits?author=lllyfff)

 authoredAug 5, 2026

 ·

 11 / 11

 Verified

 [99c926b](https://github.com/bytedance/deer-flow/commit/99c926b7bbcd0570870bc24ceb13ab934935f49c)View commit details

 Copy full SHA for 99c926b

 Browse repository at this point

- #### [fix(frontend): add public case study routes (](https://github.com/bytedance/deer-flow/commit/480a3757ed0e9e347c15f242d668ffe2f3b57b51 'fix(frontend): add public case study routes (#4635)') [#4635](https://github.com/bytedance/deer-flow/pull/4635) [)](https://github.com/bytedance/deer-flow/commit/480a3757ed0e9e347c15f242d668ffe2f3b57b51 'fix(frontend): add public case study routes (#4635)')

 [![DaoyuanLi2816](https://avatars.githubusercontent.com/u/94409450?v=4&size=32)](https://github.com/DaoyuanLi2816) [DaoyuanLi2816](https://github.com/bytedance/deer-flow/commits?author=DaoyuanLi2816)

 authoredAug 5, 2026

 ·

 9 / 10

 Verified

 [480a375](https://github.com/bytedance/deer-flow/commit/480a3757ed0e9e347c15f242d668ffe2f3b57b51)View commit details

 Copy full SHA for 480a375

 Browse repository at this point

- #### [feat(channels): add Buzz (Nostr) channel connector (](https://github.com/bytedance/deer-flow/commit/d732b90dc3737091dedf842e42eac02ba5230c40 'feat(channels): add Buzz (Nostr) channel connector (#4649)

 * feat(channels): add Buzz (Nostr) channel connector

 Adds a Buzz (https://github.com/block/buzz) channel so DeerFlow can join a
 Nostr-relay workspace as a member: it answers @mentions in channels, replies
 to DMs, and streams answers by editing one message in place.

 * app/channels/buzz_nostr.py — pure NIP-01 helpers: canonical event ids,
 BIP-340 signing/verification, chat/edit/auth builders, relay frames.
 * app/channels/buzz.py — BuzzChannel: one NIP-42-authenticated websocket,
 channel discovery (kind 39000) with one subscription per channel, live
 membership tracking (44100/44101), per-channel replay watermarks, and
 replies posted once then edited in place (kind 40003).
 * app/channels/buzz_run_policy.py — same-thread serialization, mirroring
 the Feishu precedent.

 Inbound is gated in order: signature verification, self-drop, /connect
 bind-and-return, pubkey allowlist, then mention / DM / mention-free /
 thread-follow. Off by default; needs the new optional `buzz` extra
 (coincurve, lazily imported), which detect_uv_extras resolves from
 channels.buzz.enabled the same way it already handles channels.discord.

 Two relay behaviours drove the design and are worth knowing when reviewing:
 a global {"kinds":[9]} subscription receives nothing from buzz-relay and a
 multi-value "#h" filter receives nothing either, so one REQ per channel is
 required; and a single global `since` cursor skips quiet channels, so
 watermarks are per channel.

 Signed-off-by: Ajay R <ajayr@formbuddy.com>

 * fix(channels): only publish assistant messages from the IM stream

 `_accumulate_stream_text` decided what streamed `messages-tuple` payloads
 become displayable text by rejecting ONLY payloads whose `type` contained
 "tool", so it published everything else. DeerFlow writes hidden model
 context into the messages channel as ordinary messages -- memory recall and
 the rewritten user turn as hidden HumanMessages (DynamicContextMiddleware),
 the `<durable_context_data>` block as another (DurableContextMiddleware) --
 and LangGraph fans those state writes out on the messages stream, so they
 reached every streaming IM channel as the assistant's reply.

 Proved live on a Buzz relay: the connector published a `<memory>` fact block
 and, in another run, a verbatim echo of the user's own inbound message.
 Affects Feishu, Telegram, WeCom and Buzz; worst on Buzz, where each update
 is an immutable public Nostr event that a corrective edit cannot unpublish.

 Invert the filter to an allowlist of assistant message types. Two new pure
 helpers keep it testable:

 - `_stream_payload_type` resolves the type from both shapes the function
 already handles: the `model_dump()` shape the gateway emits, and
 LangChain's `to_json()` constructor shape whose own `type` is the literal
 "constructor" and whose class name is the tail of the `id` path.
 - `_is_assistant_stream_type` matches "ai"/"assistant" by PREFIX, not
 substring -- ordinary words contain "ai" ("chain", "domain"), and a
 substring test would admit a foreign type name by accident.

 The bare-`str` branch is removed: an untyped payload cannot be attributed to
 the assistant, nothing in DeerFlow produces one (serialize_messages_tuple
 always emits `[message_dict, metadata]`), and a runtime that emitted raw text
 deltas would emit hidden context the same way. Per-message-id buffering and
 merging are unchanged.

 Tests pin both directions, including multi-chunk merging across one message
 id, so the allowlist cannot silently kill streaming, plus an end-to-end
 `_handle_streaming_chat` test asserting the live payload never reaches an
 outbound message.

 Co-Authored-By: Claude Opus 5 <noreply@anthropic.com>
 Signed-off-by: Ajay R <ajayr@formbuddy.com>

 * chore(helm): bump config_version to 33 in chart values and README

 config.example.yaml moved to 33 for the buzz channel block; the chart's
 embedded config example and its README copy track it (config_version only
 drives the outdated-config warning, per scripts/check_config_version.sh).

 Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>
 Signed-off-by: Ajay R <ajayr@formbuddy.com>

 ---------

 Signed-off-by: Ajay R <ajayr@formbuddy.com>
 Co-authored-by: Claude Opus 5 <noreply@anthropic.com>') [#4649](https://github.com/bytedance/deer-flow/pull/4649) [)](https://github.com/bytedance/deer-flow/commit/d732b90dc3737091dedf842e42eac02ba5230c40 'feat(channels): add Buzz (Nostr) channel connector (#4649)

 * feat(channels): add Buzz (Nostr) channel connector

 Adds a Buzz (https://github.com/block/buzz) channel so DeerFlow can join a
 Nostr-relay workspace as a member: it answers @mentions in channels, replies
 to DMs, and streams answers by editing one message in place.

 * app/channels/buzz_nostr.py — pure NIP-01 helpers: canonical event ids,
 BIP-340 signing/verification, chat/edit/auth builders, relay frames.
 * app/channels/buzz.py — BuzzChannel: one NIP-42-authenticated websocket,
 channel discovery (kind 39000) with one subscription per channel, live
 membership tracking (44100/44101), per-channel replay watermarks, and
 replies posted once then edited in place (kind 40003).
 * app/channels/buzz_run_policy.py — same-thread serialization, mirroring
 the Feishu precedent.

 Inbound is gated in order: signature verification, self-drop, /connect
 bind-and-return, pubkey allowlist, then mention / DM / mention-free /
 thread-follow. Off by default; needs the new optional `buzz` extra
 (coincurve, lazily imported), which detect_uv_extras resolves from
 channels.buzz.enabled the same way it already handles channels.discord.

 Two relay behaviours drove the design and are worth knowing when reviewing:
 a global {"kinds":[9]} subscription receives nothing from buzz-relay and a
 multi-value "#h" filter receives nothing either, so one REQ per channel is
 required; and a single global `since` cursor skips quiet channels, so
 watermarks are per channel.

 Signed-off-by: Ajay R <ajayr@formbuddy.com>

 * fix(channels): only publish assistant messages from the IM stream

 `_accumulate_stream_text` decided what streamed `messages-tuple` payloads
 become displayable text by rejecting ONLY payloads whose `type` contained
 "tool", so it published everything else. DeerFlow writes hidden model
 context into the messages channel as ordinary messages -- memory recall and
 the rewritten user turn as hidden HumanMessages (DynamicContextMiddleware),
 the `<durable_context_data>` block as another (DurableContextMiddleware) --
 and LangGraph fans those state writes out on the messages stream, so they
 reached every streaming IM channel as the assistant's reply.

 Proved live on a Buzz relay: the connector published a `<memory>` fact block
 and, in another run, a verbatim echo of the user's own inbound message.
 Affects Feishu, Telegram, WeCom and Buzz; worst on Buzz, where each update
 is an immutable public Nostr event that a corrective edit cannot unpublish.

 Invert the filter to an allowlist of assistant message types. Two new pure
 helpers keep it testable:

 - `_stream_payload_type` resolves the type from both shapes the function
 already handles: the `model_dump()` shape the gateway emits, and
 LangChain's `to_json()` constructor shape whose own `type` is the literal
 "constructor" and whose class name is the tail of the `id` path.
 - `_is_assistant_stream_type` matches "ai"/"assistant" by PREFIX, not
 substring -- ordinary words contain "ai" ("chain", "domain"), and a
 substring test would admit a foreign type name by accident.

 The bare-`str` branch is removed: an untyped payload cannot be attributed to
 the assistant, nothing in DeerFlow produces one (serialize_messages_tuple
 always emits `[message_dict, metadata]`), and a runtime that emitted raw text
 deltas would emit hidden context the same way. Per-message-id buffering and
 merging are unchanged.

 Tests pin both directions, including multi-chunk merging across one message
 id, so the allowlist cannot silently kill streaming, plus an end-to-end
 `_handle_streaming_chat` test asserting the live payload never reaches an
 outbound message.

 Co-Authored-By: Claude Opus 5 <noreply@anthropic.com>
 Signed-off-by: Ajay R <ajayr@formbuddy.com>

 * chore(helm): bump config_version to 33 in chart values and README

 config.example.yaml moved to 33 for the buzz channel block; the chart's
 embedded config example and its README copy track it (config_version only
 drives the outdated-config warning, per scripts/check_config_version.sh).

 Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>
 Signed-off-by: Ajay R <ajayr@formbuddy.com>

 ---------

 Signed-off-by: Ajay R <ajayr@formbuddy.com>
 Co-authored-by: Claude Opus 5 <noreply@anthropic.com>')

 Show description for d732b90

 ![ajayr](https://avatars.githubusercontent.com/u/809529?v=4&size=32)![claude](https://avatars.githubusercontent.com/u/81847?v=4&size=32)

 [ajayr](https://github.com/bytedance/deer-flow/commits?author=ajayr)

 and

 [claude](https://github.com/bytedance/deer-flow/commits?author=claude)

 authoredAug 5, 2026

 ·

 11 / 11

 Verified

 [d732b90](https://github.com/bytedance/deer-flow/commit/d732b90dc3737091dedf842e42eac02ba5230c40)View commit details

 Copy full SHA for d732b90

 Browse repository at this point

- #### [feat(tui): add transparent terminal background (](https://github.com/bytedance/deer-flow/commit/61c153ff0993c7075aeb8bb6943fd358f0ce7bc5 'feat(tui): add transparent terminal background (#4631)

 Co-authored-by: Willem Jiang <willem.jiang@gmail.com>') [#4631](https://github.com/bytedance/deer-flow/pull/4631) [)](https://github.com/bytedance/deer-flow/commit/61c153ff0993c7075aeb8bb6943fd358f0ce7bc5 'feat(tui): add transparent terminal background (#4631)

 Co-authored-by: Willem Jiang <willem.jiang@gmail.com>')

 Show description for 61c153f

 ![felix-windsor](https://avatars.githubusercontent.com/u/172729123?v=4&size=32)![WillemJiang](https://avatars.githubusercontent.com/u/219644?v=4&size=32)

 [felix-windsor](https://github.com/bytedance/deer-flow/commits?author=felix-windsor)

 and

 [WillemJiang](https://github.com/bytedance/deer-flow/commits?author=WillemJiang)

 authoredAug 5, 2026

 ·

 11 / 11

 Verified

 [61c153f](https://github.com/bytedance/deer-flow/commit/61c153ff0993c7075aeb8bb6943fd358f0ce7bc5)View commit details

 Copy full SHA for 61c153f

 Browse repository at this point