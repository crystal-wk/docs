# Source: https://github.com/bytedance/deer-flow/tree/main/backend

### Uh oh!

There was an error while loading. [Please reload this page]().

[bytedance](https://github.com/bytedance) / **[deer-flow](https://github.com/bytedance/deer-flow)** Public

- [Notifications](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow) You must be signed in to change notification settings
- [Fork 10.9k](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow)
- [Star 79.8k](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow)

 ## FilesExpand file tree

main

/

# backend

/

Copy path

## Directory actions

## More options

More options

## Directory actions

## More options

More options

## Latest commit

[![ZeroMadLife](https://avatars.githubusercontent.com/u/97534761?v=4&size=40)](https://github.com/ZeroMadLife) [ZeroMadLife](https://github.com/bytedance/deer-flow/commits?author=ZeroMadLife)

[fix(subagents): isolate background tasks from reused tool call IDs (](https://github.com/bytedance/deer-flow/commit/88252e9b318d34e7e1867155ad2c77993320788e) [#…](https://github.com/bytedance/deer-flow/pull/4758)

Open commit detailssuccess

Aug 12, 2026

[88252e9](https://github.com/bytedance/deer-flow/commit/88252e9b318d34e7e1867155ad2c77993320788e) · Aug 12, 2026

## History

[History](https://github.com/bytedance/deer-flow/commits/main/backend)

Open commit details

History

## FilesExpand file tree

main

/

# backend

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

[.vscode](https://github.com/bytedance/deer-flow/tree/main/backend/.vscode '.vscode')

 | 

[.vscode](https://github.com/bytedance/deer-flow/tree/main/backend/.vscode '.vscode')

 | 

[chore: specify project title](https://github.com/bytedance/deer-flow/commit/ce0b6f775459f0e8e60fa091896e647770e6ef34 'chore: specify project title')

 | 

Jan 14, 2026

 |
| 

[app](https://github.com/bytedance/deer-flow/tree/main/backend/app 'app')

 | 

[app](https://github.com/bytedance/deer-flow/tree/main/backend/app 'app')

 | 

[fix(wecom): serialize websocket shutdown (](https://github.com/bytedance/deer-flow/commit/38ff44778a0d11d71597c2531bfd600df855307c 'fix(wecom): serialize websocket shutdown (#4762)

* fix(wecom): await connection task shutdown

* fix(wecom): serialize websocket shutdown') [#4762](https://github.com/bytedance/deer-flow/pull/4762) [)](https://github.com/bytedance/deer-flow/commit/38ff44778a0d11d71597c2531bfd600df855307c 'fix(wecom): serialize websocket shutdown (#4762)

* fix(wecom): await connection task shutdown

* fix(wecom): serialize websocket shutdown')

 | 

Aug 11, 2026

 |
| 

[docs](https://github.com/bytedance/deer-flow/tree/main/backend/docs 'docs')

 | 

[docs](https://github.com/bytedance/deer-flow/tree/main/backend/docs 'docs')

 | 

[feat(mcp): add official OpenViking tools integration (](https://github.com/bytedance/deer-flow/commit/a263af284527749b714535f1776f0247966ec8bb 'feat(mcp): add official OpenViking tools integration (#4745)

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

 | 

Aug 11, 2026

 |
| 

[extension\_test\_fixtures](https://github.com/bytedance/deer-flow/tree/main/backend/extension_test_fixtures 'extension_test_fixtures')

 | 

[extension\_test\_fixtures](https://github.com/bytedance/deer-flow/tree/main/backend/extension_test_fixtures 'extension_test_fixtures')

 | 

[feat(extensions): observe task lifecycle and system model calls (](https://github.com/bytedance/deer-flow/commit/7389331e6593c7f39cdacd9b078cf946e4e0b22d 'feat(extensions): observe task lifecycle and system model calls (#4684)

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

 | 

Aug 11, 2026

 |
| 

[packages](https://github.com/bytedance/deer-flow/tree/main/backend/packages 'packages')

 | 

[packages](https://github.com/bytedance/deer-flow/tree/main/backend/packages 'packages')

 | 

[fix(subagents): isolate background tasks from reused tool call IDs (](https://github.com/bytedance/deer-flow/commit/88252e9b318d34e7e1867155ad2c77993320788e 'fix(subagents): isolate background tasks from reused tool call IDs (#4758)

* fix(subagents): isolate background execution IDs

* fix(subagents): preserve correlation scope and isolate usage

* fix(subagents): make usage attribution idempotent') [#…](https://github.com/bytedance/deer-flow/pull/4758)

 | 

Aug 12, 2026

 |
| 

[samples/other\_agent\_demo](https://github.com/bytedance/deer-flow/tree/main/backend/samples/other_agent_demo 'This path skips through empty directories')

 | 

[samples/other\_agent\_demo](https://github.com/bytedance/deer-flow/tree/main/backend/samples/other_agent_demo 'This path skips through empty directories')

 | 

[\[feat\] memory: pluggable MemoryManager interface for backend onboardi…](https://github.com/bytedance/deer-flow/commit/01a89f23794e3730519c70e87350157721ceffe7 '[feat] memory: pluggable MemoryManager interface for backend onboarding (#4326)

* refactor(memory): pluggable MemoryManager interface for backend onboarding

Optimize the MemoryManager interface layer so new backends (mem0/openviking)
onboard with less code and the contract stays stable as capabilities are
added. A minimal backend now implements only from_config + add + get_context
(verified by test_memory_manager_interface.py::_MinimalBackend onboarding via
the factory); the factory no longer knows a backend's private hooks.

- MemoryManager: ABC -> pydantic BaseModel; three-tier methods (tier-1
 add/get_context abstract; tier-2 management defaults; tier-3 optional hooks
 warm/reload/fact + on_pre_compress/on_turn_start). Dropped 3 self-serving
 hooks. 6 hasattr probe sites -> direct call + try/except NotImplementedError.
- from_config classmethod: factory thins to resolve + inject storage_path +
 collect host hooks + call from_config; DeerMem-specific hook consumption
 moved from factory to DeerMem.from_config.
- Invariants: @model_validator (mode='tool' requires search via supports_search
 ClassVar); DeerMemConfig storage_path-is-file check moved here from factory.
- Async: aadd/aget_context/asearch default to the sync path (speculative).
- Callbacks: MemoryCallbacks + LangfuseMemoryCallbacks; on_memory_llm_call
 subsumes tracing_callback (same signature/timing/mutation); deleted the
 tracing_callback field. DeerMem decoupled from langfuse (portability).
- noop keeps read-op empty overrides (avoids router 500s on the
 disable-memory-via-noop path); only delete/export inherit the base raise.

Behavior preserved: 661 passed / 13 skipped. Docs: backends/README.md rewritten
(three-tier + from_config + callbacks); samples README updated; removed stale
private doc paths.

Co-Authored-By: Claude <noreply@anthropic.com>

* fix(memory): 501 on unsupported read/manage endpoints + accurate warm log

Review follow-up on the three-tier MemoryManager refactor.

- Read/manage endpoints (GET /memory, /memory/export, /memory/status,
 DELETE /memory, POST /memory/import) and the /memory/reload fallback now
 catch NotImplementedError -> 501, matching the fact-CRUD endpoints. The
 hasattr->try/except migration had skipped these: they were @abstractmethod
 before (every backend implemented them, so they never raised), so once they
 became tier-2 default-raise a minimal backend (only add + get_context) hit a
 raw 500 -- there is no global NotImplementedError handler. get_memory is
 shared via _get_memory_or_501 (covers /memory, export, status, reload
 fallback). noop is unchanged: its read-op empty overrides never raise.
- warm() base default returns None (tri-state: True=warmed, False=failed,
 None=nothing to warm) so the Gateway lifespan logs "skipping" for a
 non-DeerMem backend (e.g. noop) instead of the inaccurate "warmed
 successfully" it never earned. DeerMem.warm keeps True/False.
- Tests: 6 router 501 tests (read/manage + reload fallback) + 2 lifespan
 warm-log tests (None->skipping, False->warning); conformance/pluggable
 assert warm() is None.

705 passed / 13 skipped; lint clean.

Co-Authored-By: Claude <noreply@anthropic.com>

* fix(memory): review follow-ups - search-flag consistency, client reload, backend_config purity

Address review feedback on the three-tier MemoryManager refactor:

- [Medium] supports_search/search drift: the invariant now requires the
 supports_search ClassVar flag to MATCH whether search() is actually
 overridden (type(self).search is not MemoryManager.search), so the flag
 can't drift from the impl. Catches both directions at instantiation: a
 backend that overrides search() but forgets supports_search=True (was a
 misleading tool-mode rejection), and one that sets the flag without
 overriding (was a runtime NotImplementedError on the first memory_search).
 noop sets supports_search=True to match its search() override. Conformance
 adds drift + consistent-backend tests.
- [Low] client.reload_memory fallback: wrap the get_memory fallback so a
 minimal backend (only add + get_context) surfaces a clean NotImplementedError
 ("implements neither reload_memory nor get_memory") instead of an uncaught
 propagation -- mirrors the router's 501. Test added.
- [Low] backend_config purity: DeerMem.from_config restores backend_config to
 the pure data the host passed after model_post_init parses the injected hooks
 into DeerMemConfig (self._config, PrivateAttr); the field stays serializable
 (no callables/LLM) and matches the README ("host hooks NOT in backend_config").
 Test asserts purity + hooks wired.
- [Low] CHANGELOG: breaking-change note that mode='tool' + non-search backend
 now fails fast at startup (was silently empty) so operators recognize it on
 upgrade.
- [Nit] .gitignore: drop the env-specific .tmp-pytest/ entry (--basetemp is
 local-only, not make test/CI).

709 passed / 13 skipped; lint clean.

Co-Authored-By: Claude <noreply@anthropic.com>

* docs(changelog): correct memory tool-mode fail-fast note

The CHANGELOG entry said mode='tool' + a non-search backend "(e.g. noop)"
fails fast at startup, but noop overrides search() (returns []) and sets
supports_search=True (required by the consistency invariant), so noop IS
search-capable and noop+tool does NOT fail fast. The fail-fast only affects a
custom backend that onboards without overriding search(). Reworded to drop the
misleading noop example and state both shipping backends implement search().

Co-Authored-By: Claude <noreply@anthropic.com>

---------

Co-authored-by: Claude <noreply@anthropic.com>')

 | 

Jul 22, 2026

 |
| 

[scripts](https://github.com/bytedance/deer-flow/tree/main/backend/scripts 'scripts')

 | 

[scripts](https://github.com/bytedance/deer-flow/tree/main/backend/scripts 'scripts')

 | 

[feat(checkpoint): checkpoint history cache (](https://github.com/bytedance/deer-flow/commit/c8cf1bf2fbd4ecd180fe33306b38c6f28b341d6f 'feat(checkpoint): checkpoint history cache (#4638)

* feat(checkpoint-cache): delta-mode checkpoint history cache with recursive compose

Read-only, invalidation-free cache for LangGraph delta-channel history
({writes, seed}) at the get_delta_channel_history choke point:

- database.checkpoint_cache config (memory|redis; max_entries 0=disabled;
 redis bounded by TTL, Gateway/async only)
- memory LRU backend (copy-on-read, zero-serde hit path) and redis backend
 (lazy import, degrades to all-miss on outage)
- CachedHistorySaver: recursive composition from the nearest warm ancestor
 (depth budget 8), caching each level; depth-0 cold chains delegate one
 inner fast-path walk. Entries keyed by immutable
 (db, thread, ns, checkpoint_id, channel) — no invalidation, coherent
 across workers
- provider wiring: wraps in delta mode only (async + sync), full mode
 untouched; sync path is memory-only
- bench opt-in: DEERFLOW_CHECKPOINT_BENCH_HISTORY_CACHE=1

sqlite bench (500 updates, payload 2KB): write phase 2.28x at f=250,
1.32x at f=10; one delegated walk per thread cold start.

* chore(config): bump config_version to 32 for database.checkpoint_cache

The checkpoint history cache feature added the database.checkpoint_cache
section to config.example.yaml; bump the schema version so existing
deployments get the outdated-config warning and can run make config-upgrade.

* chore(helm): bump config_version to 32 in chart values and README

* fix(checkpoint-cache): purge thread history entries on delete paths

Addresses review on #4638: delete_thread/prune removed source-of-truth
checkpoints but left the thread's materialized history payloads in the
cache (memory: until LRU eviction; redis: until TTL, default 1 day) — a
data-lifecycle gap for tenant offboarding / GDPR-style erasure.

- Cache contract gains thread-scoped adelete_thread/delete_thread
 (lifecycle purge, not invalidation; entries remain immutable)
- Memory backend: stem scan over the LRU map; redis: SCAN MATCH + UNLINK,
 outage degrades to TTL-bounded retention without raising
- CachedHistorySaver purges on delete_thread/adelete_thread and
 prune/aprune (prune rewrites chains, so pre-prune histories must go);
 delete_for_runs stays delegation-only (run->thread mapping unavailable,
 no in-tree callers), documented in code
- ttl_seconds description documents the residual-retention window
- Tests: thread-scoped purge on both backends, saver-level delete/prune
 purge, prefix-safety (t1 vs t10), redis outage degradation, and the
 pinned no-purge behavior of delete_for_runs

* fix(checkpoint-cache): stable db identity, prefix-aware sync singleton, explicit zero TTL

Addresses Copilot review on #4638:

- checkpoint_cache_db_hash now hashes the credential-free postgres
 identity (host:port/database + schema): credential rotation no longer
 changes the cache namespace (cold cache + orphaned keys until TTL).
 Unparseable URLs fall back to the raw string.
- The sync-path memory cache singleton is also keyed by its key_prefix:
 a namespace change (db identity change or operator override) recreates
 the cache instead of leaving stale-prefix entries unreachable and
 unpurgeable.
- ttl_seconds=0 is now an explicit, documented opt-out of redis expiry
 (SET without EX; redis maxmemory policy only) instead of a silent
 'ttl_seconds or None' coercion.

Tests: credential-rotation hash stability, unparseable-URL fallback,
prefix-change singleton recreation, same-prefix singleton reuse, and
zero-TTL wire behavior (ex=None).

---------

Co-authored-by: Willem Jiang <willem.jiang@gmail.com>') [#4638](https://github.com/bytedance/deer-flow/pull/4638) [)](https://github.com/bytedance/deer-flow/commit/c8cf1bf2fbd4ecd180fe33306b38c6f28b341d6f 'feat(checkpoint): checkpoint history cache (#4638)

* feat(checkpoint-cache): delta-mode checkpoint history cache with recursive compose

Read-only, invalidation-free cache for LangGraph delta-channel history
({writes, seed}) at the get_delta_channel_history choke point:

- database.checkpoint_cache config (memory|redis; max_entries 0=disabled;
 redis bounded by TTL, Gateway/async only)
- memory LRU backend (copy-on-read, zero-serde hit path) and redis backend
 (lazy import, degrades to all-miss on outage)
- CachedHistorySaver: recursive composition from the nearest warm ancestor
 (depth budget 8), caching each level; depth-0 cold chains delegate one
 inner fast-path walk. Entries keyed by immutable
 (db, thread, ns, checkpoint_id, channel) — no invalidation, coherent
 across workers
- provider wiring: wraps in delta mode only (async + sync), full mode
 untouched; sync path is memory-only
- bench opt-in: DEERFLOW_CHECKPOINT_BENCH_HISTORY_CACHE=1

sqlite bench (500 updates, payload 2KB): write phase 2.28x at f=250,
1.32x at f=10; one delegated walk per thread cold start.

* chore(config): bump config_version to 32 for database.checkpoint_cache

The checkpoint history cache feature added the database.checkpoint_cache
section to config.example.yaml; bump the schema version so existing
deployments get the outdated-config warning and can run make config-upgrade.

* chore(helm): bump config_version to 32 in chart values and README

* fix(checkpoint-cache): purge thread history entries on delete paths

Addresses review on #4638: delete_thread/prune removed source-of-truth
checkpoints but left the thread's materialized history payloads in the
cache (memory: until LRU eviction; redis: until TTL, default 1 day) — a
data-lifecycle gap for tenant offboarding / GDPR-style erasure.

- Cache contract gains thread-scoped adelete_thread/delete_thread
 (lifecycle purge, not invalidation; entries remain immutable)
- Memory backend: stem scan over the LRU map; redis: SCAN MATCH + UNLINK,
 outage degrades to TTL-bounded retention without raising
- CachedHistorySaver purges on delete_thread/adelete_thread and
 prune/aprune (prune rewrites chains, so pre-prune histories must go);
 delete_for_runs stays delegation-only (run->thread mapping unavailable,
 no in-tree callers), documented in code
- ttl_seconds description documents the residual-retention window
- Tests: thread-scoped purge on both backends, saver-level delete/prune
 purge, prefix-safety (t1 vs t10), redis outage degradation, and the
 pinned no-purge behavior of delete_for_runs

* fix(checkpoint-cache): stable db identity, prefix-aware sync singleton, explicit zero TTL

Addresses Copilot review on #4638:

- checkpoint_cache_db_hash now hashes the credential-free postgres
 identity (host:port/database + schema): credential rotation no longer
 changes the cache namespace (cold cache + orphaned keys until TTL).
 Unparseable URLs fall back to the raw string.
- The sync-path memory cache singleton is also keyed by its key_prefix:
 a namespace change (db identity change or operator override) recreates
 the cache instead of leaving stale-prefix entries unreachable and
 unpurgeable.
- ttl_seconds=0 is now an explicit, documented opt-out of redis expiry
 (SET without EX; redis maxmemory policy only) instead of a silent
 'ttl_seconds or None' coercion.

Tests: credential-rotation hash stability, unparseable-URL fallback,
prefix-change singleton recreation, same-prefix singleton reuse, and
zero-TTL wire behavior (ex=None).

---------

Co-authored-by: Willem Jiang <willem.jiang@gmail.com>')

 | 

Aug 2, 2026

 |
| 

[tests](https://github.com/bytedance/deer-flow/tree/main/backend/tests 'tests')

 | 

[tests](https://github.com/bytedance/deer-flow/tree/main/backend/tests 'tests')

 | 

[fix(subagents): isolate background tasks from reused tool call IDs (](https://github.com/bytedance/deer-flow/commit/88252e9b318d34e7e1867155ad2c77993320788e 'fix(subagents): isolate background tasks from reused tool call IDs (#4758)

* fix(subagents): isolate background execution IDs

* fix(subagents): preserve correlation scope and isolate usage

* fix(subagents): make usage attribution idempotent') [#…](https://github.com/bytedance/deer-flow/pull/4758)

 | 

Aug 12, 2026

 |
| 

[.gitignore](https://github.com/bytedance/deer-flow/blob/main/backend/.gitignore '.gitignore')

 | 

[.gitignore](https://github.com/bytedance/deer-flow/blob/main/backend/.gitignore '.gitignore')

 | 

[feat(memory): memory message processing (](https://github.com/bytedance/deer-flow/commit/8145d66a33a34baf8f1e9b93926d74a133e07c41 'feat(memory): memory message processing (#4447)

* feat(memory): signals-based update pipeline + always-on watermark/trivial filter

Refactor the DeerMem memory update pipeline (message_processing -> queue ->
updater) around a signals frozenset seam, replacing the
(filtered, correction_detected, reinforcement_detected) 3-tuple with
(filtered, signals: frozenset[str]) end to end.

message_processing:
- Externalize signal-detection patterns to YAML (message_patterns/*.yaml).
- Extend signals from correction/reinforcement to a 6-class set
 (correction/reinforcement/preference/identity/goal/decision); detect_signals
 returns a frozenset aligned with the fact category enum.
- Pure-acknowledgment turns ("ok"/"好的"/...) are always filtered out before
 enqueue (whole-message fullmatch), saving an extraction LLM call.

queue (core/queue.py):
- In-memory list + debounce timer, with flush_sync (graceful-shutdown drain
 that joins an in-flight worker under a hard timeout) and queue_max_depth
 backpressure (signal-bearing updates always admitted; QueueFull otherwise).
- Same-key updates coalesce with a signal union; per-batch success/fail summary.

updater (core/updater.py):
- head500+tail500 message truncation (replaces the 1000-char head chop).
- Always-on per-thread watermark: feed only messages added since the last
 extraction. The watermark is in-memory and is not advanced on failure, so a
 failed/lost update is re-fed on the next conversation turn.
- [MANUAL] prompt marker for user-authored facts (source.type="manual").
- Post-invoke extraction_callback (host-injected) emitting facts_extracted /
 facts_accepted / rejected_low_confidence; the host default logs metrics and
 flags >60% rejection.

Confidence filtering remains in _apply_updates (the existing
fact_confidence_threshold check); there is no separate write gate.
Consolidation stays opt-in (lossy). The ABC add/add_nowait signature is
unchanged, so the summarization flush hook and host are unaffected.

Tests: add test_message_processing_signals, test_updater_truncation,
test_updater_watermark; update queue/updater/consolidation/staleness/pluggable
tests for the signals seam.

Co-Authored-By: Claude <noreply@anthropic.com>

* fix(memory): harden update pipeline per PR review

- Catch QueueFull in DeerMem.add/add_nowait so backpressure degrades to
 'update skipped' instead of propagating into after_agent /
 summarization_hook and breaking the agent run (peer middlewares
 self-guard; MemoryMiddleware was the lone exception). Emergency
 (add_nowait) always admits under backpressure -- its data cannot be
 re-fed next turn.
- Rewrite the watermark from index-based to content/identity-based
 (_message_identity + _feed_after_watermark) so it stays correct when
 summarization removes the conversation front -- an index watermark
 pointed at the wrong message and silently skipped un-extracted tail
 turns. The emergency flush bypasses the watermark (bypass_watermark on
 ConversationContext, threaded through update_memory) and coexists with
 (does not replace) a pending normal update, so a flush cannot drop a
 pending update's un-extracted tail.
- Populate facts_accepted / rejected_low_confidence inside _apply_updates
 at the real confidence-filter site (passed_threshold) instead of
 re-deriving the threshold in _finalize_update -- eliminates metric drift.
- Emit extraction metrics in a finally with an 'attempted' flag so
 exception failures (parse error, apply_changes raise after retry) are
 observable, not only the happy path.
- Re-detect signals on the post-watermark feed for the extraction hint so
 it no longer references turns the LLM cannot see; admission-time signals
 still drive backpressure.
- Move the post-batch reschedule inside the queue lock to close a
 non-atomic self._timer race with a concurrent add.

Co-Authored-By: Claude <noreply@anthropic.com>

* fix(memory): address follow-up review nits (LRU, metric name, docstring)

- Bound the in-memory watermark cache with a configurable LRU
 (watermark_max_keys, default 4096, 0=unbounded). A dropped key re-extracts
 one batch on that thread's next turn (the documented restart behavior), so
 eviction is safe and preserves the content-identity watermark's
 front-removal guarantee. Adds _watermark_get/_watermark_set helpers and a
 bounded-LRU regression test.
- Rename the extraction metric facts_accepted -> facts_passed_confidence so
 the name matches what the >60% rejection-rate warning assumes (a
 confidence-gate signal, not a persisted-fact count); drop the stale
 "historical semantics" justification. Brand-new callback, one consumer.
- Fix the stale test_message_processing_signals module docstring: the signals
 seam is already swapped to frozenset, and a stale stage-numbering prefix is
 removed.

Co-Authored-By: Claude <noreply@anthropic.com>

---------

Co-authored-by: Claude <noreply@anthropic.com>') [#4447](https://github.com/bytedance/deer-flow/pull/4447) [)](https://github.com/bytedance/deer-flow/commit/8145d66a33a34baf8f1e9b93926d74a133e07c41 'feat(memory): memory message processing (#4447)

* feat(memory): signals-based update pipeline + always-on watermark/trivial filter

Refactor the DeerMem memory update pipeline (message_processing -> queue ->
updater) around a signals frozenset seam, replacing the
(filtered, correction_detected, reinforcement_detected) 3-tuple with
(filtered, signals: frozenset[str]) end to end.

message_processing:
- Externalize signal-detection patterns to YAML (message_patterns/*.yaml).
- Extend signals from correction/reinforcement to a 6-class set
 (correction/reinforcement/preference/identity/goal/decision); detect_signals
 returns a frozenset aligned with the fact category enum.
- Pure-acknowledgment turns ("ok"/"好的"/...) are always filtered out before
 enqueue (whole-message fullmatch), saving an extraction LLM call.

queue (core/queue.py):
- In-memory list + debounce timer, with flush_sync (graceful-shutdown drain
 that joins an in-flight worker under a hard timeout) and queue_max_depth
 backpressure (signal-bearing updates always admitted; QueueFull otherwise).
- Same-key updates coalesce with a signal union; per-batch success/fail summary.

updater (core/updater.py):
- head500+tail500 message truncation (replaces the 1000-char head chop).
- Always-on per-thread watermark: feed only messages added since the last
 extraction. The watermark is in-memory and is not advanced on failure, so a
 failed/lost update is re-fed on the next conversation turn.
- [MANUAL] prompt marker for user-authored facts (source.type="manual").
- Post-invoke extraction_callback (host-injected) emitting facts_extracted /
 facts_accepted / rejected_low_confidence; the host default logs metrics and
 flags >60% rejection.

Confidence filtering remains in _apply_updates (the existing
fact_confidence_threshold check); there is no separate write gate.
Consolidation stays opt-in (lossy). The ABC add/add_nowait signature is
unchanged, so the summarization flush hook and host are unaffected.

Tests: add test_message_processing_signals, test_updater_truncation,
test_updater_watermark; update queue/updater/consolidation/staleness/pluggable
tests for the signals seam.

Co-Authored-By: Claude <noreply@anthropic.com>

* fix(memory): harden update pipeline per PR review

- Catch QueueFull in DeerMem.add/add_nowait so backpressure degrades to
 'update skipped' instead of propagating into after_agent /
 summarization_hook and breaking the agent run (peer middlewares
 self-guard; MemoryMiddleware was the lone exception). Emergency
 (add_nowait) always admits under backpressure -- its data cannot be
 re-fed next turn.
- Rewrite the watermark from index-based to content/identity-based
 (_message_identity + _feed_after_watermark) so it stays correct when
 summarization removes the conversation front -- an index watermark
 pointed at the wrong message and silently skipped un-extracted tail
 turns. The emergency flush bypasses the watermark (bypass_watermark on
 ConversationContext, threaded through update_memory) and coexists with
 (does not replace) a pending normal update, so a flush cannot drop a
 pending update's un-extracted tail.
- Populate facts_accepted / rejected_low_confidence inside _apply_updates
 at the real confidence-filter site (passed_threshold) instead of
 re-deriving the threshold in _finalize_update -- eliminates metric drift.
- Emit extraction metrics in a finally with an 'attempted' flag so
 exception failures (parse error, apply_changes raise after retry) are
 observable, not only the happy path.
- Re-detect signals on the post-watermark feed for the extraction hint so
 it no longer references turns the LLM cannot see; admission-time signals
 still drive backpressure.
- Move the post-batch reschedule inside the queue lock to close a
 non-atomic self._timer race with a concurrent add.

Co-Authored-By: Claude <noreply@anthropic.com>

* fix(memory): address follow-up review nits (LRU, metric name, docstring)

- Bound the in-memory watermark cache with a configurable LRU
 (watermark_max_keys, default 4096, 0=unbounded). A dropped key re-extracts
 one batch on that thread's next turn (the documented restart behavior), so
 eviction is safe and preserves the content-identity watermark's
 front-removal guarantee. Adds _watermark_get/_watermark_set helpers and a
 bounded-LRU regression test.
- Rename the extraction metric facts_accepted -> facts_passed_confidence so
 the name matches what the >60% rejection-rate warning assumes (a
 confidence-gate signal, not a persisted-fact count); drop the stale
 "historical semantics" justification. Brand-new callback, one consumer.
- Fix the stale test_message_processing_signals module docstring: the signals
 seam is already swapped to frozenset, and a stale stage-numbering prefix is
 removed.

Co-Authored-By: Claude <noreply@anthropic.com>

---------

Co-authored-by: Claude <noreply@anthropic.com>')

 | 

Jul 26, 2026

 |
| 

[.python-version](https://github.com/bytedance/deer-flow/blob/main/backend/.python-version '.python-version')

 | 

[.python-version](https://github.com/bytedance/deer-flow/blob/main/backend/.python-version '.python-version')

 | 

[chore: add Python and LangGraph stuff](https://github.com/bytedance/deer-flow/commit/c2a62a2266e0756b5e69f7fc6054626f233da07c 'chore: add Python and LangGraph stuff')

 | 

Jan 13, 2026

 |
| 

[AGENTS.md](https://github.com/bytedance/deer-flow/blob/main/backend/AGENTS.md 'AGENTS.md')

 | 

[AGENTS.md](https://github.com/bytedance/deer-flow/blob/main/backend/AGENTS.md 'AGENTS.md')

 | 

[fix(subagents): isolate background tasks from reused tool call IDs (](https://github.com/bytedance/deer-flow/commit/88252e9b318d34e7e1867155ad2c77993320788e 'fix(subagents): isolate background tasks from reused tool call IDs (#4758)

* fix(subagents): isolate background execution IDs

* fix(subagents): preserve correlation scope and isolate usage

* fix(subagents): make usage attribution idempotent') [#…](https://github.com/bytedance/deer-flow/pull/4758)

 | 

Aug 12, 2026

 |
| 

[CLAUDE.md](https://github.com/bytedance/deer-flow/blob/main/backend/CLAUDE.md 'CLAUDE.md')

 | 

[CLAUDE.md](https://github.com/bytedance/deer-flow/blob/main/backend/CLAUDE.md 'CLAUDE.md')

 | 

[docs: adopt AGENTS.md as source of truth (CLAUDE.md imports via @AGEN…](https://github.com/bytedance/deer-flow/commit/ff7ecdbd37f8ac81ac8137befea55b967efa70e4 'docs: adopt AGENTS.md as source of truth (CLAUDE.md imports via @AGENTS.md) + refresh module guides (#3770)

* docs: add root-level CLAUDE.md to orient the monorepo

Adds a thin top-level CLAUDE.md that maps the monorepo and delegates depth
to backend/CLAUDE.md and frontend/CLAUDE.md, per issue #3761.

Includes the project overview + service topology (Nginx 2026, Gateway 8001,
Frontend 3000, optional Provisioner 8002), a top-level repository map, root
`make` vs. per-module command sections, "where to go next" links to the module
guides and primary root docs, and the repo-wide cross-cutting conventions
(documentation-update policy, TDD expectation, format before pushing).

No code or behavior changes; root points down, modules own depth.

Closes #3761

Co-Authored-By: Claude Opus 4.8 <noreply@anthropic.com>

* docs: make AGENTS.md the source of truth, CLAUDE.md a thin @AGENTS.md importer

Adopt the AGENTS.md convention so the same agent guidance serves Claude Code,
Codex, and other tools. At each level (root, backend, frontend) the content
lives in AGENTS.md and CLAUDE.md just imports it via `@AGENTS.md`.

- root: move the monorepo orientation layer to AGENTS.md; CLAUDE.md -> @AGENTS.md.
 Fix an incorrect "TUI" reference (not present on main) and repoint the module
 links to the AGENTS.md files.
- backend: move the guide to AGENTS.md (was an AGENTS.md -> @CLAUDE.md pointer;
 direction is now flipped). Refresh stale content: rebuild the full middleware
 chain (~26 ordered steps incl. InputSanitization, ToolOutputBudget,
 DynamicContext, TokenBudget, SafetyFinishReason) from the actual build
 functions; drop the brittle "11 middleware components" count; expand the
 community-tools list to the real set.
- frontend: merge the practical Next.js guide with the existing AGENTS.md's
 unique sections (LangGraph diagram, tech-stack versions, interaction
 ownership, resources) into one AGENTS.md (CLAUDE.md -> @AGENTS.md). Fix the
 stale src/ layout (remove the no-longer-present server/ better-auth entry;
 add the now-active auth/agents/blog/... modules and routes) and drop a bogus
 interaction-ownership bullet referencing files that don't exist.

Docs only; no code or behavior changes.

Co-Authored-By: Claude Opus 4.8 <noreply@anthropic.com>

---------

Co-authored-by: Claude Opus 4.8 <noreply@anthropic.com>')

 | 

Jun 25, 2026

 |
| 

[CONTRIBUTING.md](https://github.com/bytedance/deer-flow/blob/main/backend/CONTRIBUTING.md 'CONTRIBUTING.md')

 | 

[CONTRIBUTING.md](https://github.com/bytedance/deer-flow/blob/main/backend/CONTRIBUTING.md 'CONTRIBUTING.md')

 | 

[docs: fix stale docs and typos (](https://github.com/bytedance/deer-flow/commit/629477fd5c1914a129c76798d9c3e5b85a51ba25 'docs: fix stale docs and typos (#3913)') [#3913](https://github.com/bytedance/deer-flow/pull/3913) [)](https://github.com/bytedance/deer-flow/commit/629477fd5c1914a129c76798d9c3e5b85a51ba25 'docs: fix stale docs and typos (#3913)')

 | 

Jul 3, 2026

 |
| 

[Dockerfile](https://github.com/bytedance/deer-flow/blob/main/backend/Dockerfile 'Dockerfile')

 | 

[Dockerfile](https://github.com/bytedance/deer-flow/blob/main/backend/Dockerfile 'Dockerfile')

 | 

[feat: add Lark CLI integration (](https://github.com/bytedance/deer-flow/commit/7aa314b4c1fc38e3db11e23ddea329595aeb9ebc 'feat: add Lark CLI integration (#3971)

* feat: add lark cli integration

* fix: polish lark integration actions

* feat: support lark incremental permissions

* fix: detect lark authorization completion

* fix: harden lark integration install

* feat: expand lark auth scopes and reuse host auth in sandbox

Default lark auth to least-privilege (recommend=false, base sign-in only)
and expose the full set of lark-cli --domain business domains as native
--domain grants instead of a 4-domain read-only mapping. Resolve the
skill pack from the latest larksuite/cli GitHub release at install time
with content-hash integrity, and surface version/runtime drift in status.

Share the per-user lark-cli config/data profile between the Gateway
Settings auth flow and agent conversations by mounting the integration
dirs into the AIO sandbox and injecting the matching env for lark-cli
commands, with an allowlisted extra_mounts path in the provisioner/K8s
backend and traversal guards on integration paths.

* style: fix lint issues from ruff and prettier

Sort imports in the provisioner PVC test and re-wrap two long i18n
description strings to satisfy backend ruff and frontend prettier CI.

* fix(lark): address managed integration review feedback

* fix(frontend): stabilize integrations settings e2e

* test(sandbox): isolate remote backend legacy visibility check

* test: fix backend unit failures after merge

* Harden Lark integration review fixes

* Format Lark integration E2E test

* fix(lark): harden sandbox credential exposure and status disclosure

Address willem_bd's security review on PR #3971:

- Mount the per-user lark-cli config dir (long-lived appSecret) read-only
 into the AIO sandbox; only the refreshable-token data dir stays writable.
- Redact host filesystem paths (install_path, cli.path) from
 GET /lark/status and the config/auth complete responses for non-admin
 callers, fail-closed on any auth error.
- Document the npm postinstall trade-off (--ignore-scripts is not viable
 because @larksuite/cli fetches its platform binary in postinstall).
- Document the sandbox credential trust boundary in AGENTS.md and README,
 pointing at the sidecar-broker follow-up (#4338).

---------

Co-authored-by: Willem Jiang <willem.jiang@gmail.com>') [#3971](https://github.com/bytedance/deer-flow/pull/3971) [)](https://github.com/bytedance/deer-flow/commit/7aa314b4c1fc38e3db11e23ddea329595aeb9ebc 'feat: add Lark CLI integration (#3971)

* feat: add lark cli integration

* fix: polish lark integration actions

* feat: support lark incremental permissions

* fix: detect lark authorization completion

* fix: harden lark integration install

* feat: expand lark auth scopes and reuse host auth in sandbox

Default lark auth to least-privilege (recommend=false, base sign-in only)
and expose the full set of lark-cli --domain business domains as native
--domain grants instead of a 4-domain read-only mapping. Resolve the
skill pack from the latest larksuite/cli GitHub release at install time
with content-hash integrity, and surface version/runtime drift in status.

Share the per-user lark-cli config/data profile between the Gateway
Settings auth flow and agent conversations by mounting the integration
dirs into the AIO sandbox and injecting the matching env for lark-cli
commands, with an allowlisted extra_mounts path in the provisioner/K8s
backend and traversal guards on integration paths.

* style: fix lint issues from ruff and prettier

Sort imports in the provisioner PVC test and re-wrap two long i18n
description strings to satisfy backend ruff and frontend prettier CI.

* fix(lark): address managed integration review feedback

* fix(frontend): stabilize integrations settings e2e

* test(sandbox): isolate remote backend legacy visibility check

* test: fix backend unit failures after merge

* Harden Lark integration review fixes

* Format Lark integration E2E test

* fix(lark): harden sandbox credential exposure and status disclosure

Address willem_bd's security review on PR #3971:

- Mount the per-user lark-cli config dir (long-lived appSecret) read-only
 into the AIO sandbox; only the refreshable-token data dir stays writable.
- Redact host filesystem paths (install_path, cli.path) from
 GET /lark/status and the config/auth complete responses for non-admin
 callers, fail-closed on any auth error.
- Document the npm postinstall trade-off (--ignore-scripts is not viable
 because @larksuite/cli fetches its platform binary in postinstall).
- Document the sandbox credential trust boundary in AGENTS.md and README,
 pointing at the sidecar-broker follow-up (#4338).

---------

Co-authored-by: Willem Jiang <willem.jiang@gmail.com>')

 | 

Jul 26, 2026

 |
| 

[Makefile](https://github.com/bytedance/deer-flow/blob/main/backend/Makefile 'Makefile')

 | 

[Makefile](https://github.com/bytedance/deer-flow/blob/main/backend/Makefile 'Makefile')

 | 

[fix(dev): exclude backend runtime state from reload (](https://github.com/bytedance/deer-flow/commit/f78730ab86d1e3e9ae328ece9fcd8936b458f5c3 'fix(dev): exclude backend runtime state from reload (#4759)') [#4759](https://github.com/bytedance/deer-flow/pull/4759) [)](https://github.com/bytedance/deer-flow/commit/f78730ab86d1e3e9ae328ece9fcd8936b458f5c3 'fix(dev): exclude backend runtime state from reload (#4759)')

 | 

Aug 11, 2026

 |
| 

[README.md](https://github.com/bytedance/deer-flow/blob/main/backend/README.md 'README.md')

 | 

[README.md](https://github.com/bytedance/deer-flow/blob/main/backend/README.md 'README.md')

 | 

[fix(discord): prevent typing tasks after stop (](https://github.com/bytedance/deer-flow/commit/df01102dfc458559abb1acf29d9aee1fb6d9b30b 'fix(discord): prevent typing tasks after stop (#4752)

* fix(discord): prevent typing tasks after stop

* fix(discord): serialize typing cleanup on event loop

* fix(discord): harden typing cleanup on loop exit') [#4752](https://github.com/bytedance/deer-flow/pull/4752) [)](https://github.com/bytedance/deer-flow/commit/df01102dfc458559abb1acf29d9aee1fb6d9b30b 'fix(discord): prevent typing tasks after stop (#4752)

* fix(discord): prevent typing tasks after stop

* fix(discord): serialize typing cleanup on event loop

* fix(discord): harden typing cleanup on loop exit')

 | 

Aug 11, 2026

 |
| 

[README\_zh.md](https://github.com/bytedance/deer-flow/blob/main/backend/README_zh.md 'README_zh.md')

 | 

[README\_zh.md](https://github.com/bytedance/deer-flow/blob/main/backend/README_zh.md 'README_zh.md')

 | 

[docs: add Chinese backend README (](https://github.com/bytedance/deer-flow/commit/36bd6764ad7ae01360da505f8ee72c7902c71f98 'docs: add Chinese backend README (#4763)') [#4763](https://github.com/bytedance/deer-flow/pull/4763) [)](https://github.com/bytedance/deer-flow/commit/36bd6764ad7ae01360da505f8ee72c7902c71f98 'docs: add Chinese backend README (#4763)')

 | 

Aug 11, 2026

 |
| 

[debug.py](https://github.com/bytedance/deer-flow/blob/main/backend/debug.py 'debug.py')

 | 

[debug.py](https://github.com/bytedance/deer-flow/blob/main/backend/debug.py 'debug.py')

 | 

[feat(debug): print presented file paths with physical resolution (](https://github.com/bytedance/deer-flow/commit/4063dd71575f32533a2248048df0d8dca66c0c1a 'feat(debug): print presented file paths with physical resolution (#2825)

Surface artifacts produced via the present_files tool in the CLI debug
REPL so headless clients without a frontend (VS Code launch configs,
etc.) can locate output files. Each turn prints newly added artifacts
plus their resolved host path. Works for any source that goes through
present_files — ACP agents, subagents, or sandbox writes.

Co-authored-by: Claude Opus 4 <noreply@anthropic.com>') [#2825](https://github.com/bytedance/deer-flow/pull/2825) [)](https://github.com/bytedance/deer-flow/commit/4063dd71575f32533a2248048df0d8dca66c0c1a 'feat(debug): print presented file paths with physical resolution (#2825)

Surface artifacts produced via the present_files tool in the CLI debug
REPL so headless clients without a frontend (VS Code launch configs,
etc.) can locate output files. Each turn prints newly added artifacts
plus their resolved host path. Works for any source that goes through
present_files — ACP agents, subagents, or sandbox writes.

Co-authored-by: Claude Opus 4 <noreply@anthropic.com>')

 | 

May 9, 2026

 |
| 

[langgraph.json](https://github.com/bytedance/deer-flow/blob/main/backend/langgraph.json 'langgraph.json')

 | 

[langgraph.json](https://github.com/bytedance/deer-flow/blob/main/backend/langgraph.json 'langgraph.json')

 | 

[fix: resolve make dev and test-e2e errors (](https://github.com/bytedance/deer-flow/commit/c5d57b453382d794174f16ab354b930d1a246ca5 'fix: resolve make dev and test-e2e errors (#2570)') [#2570](https://github.com/bytedance/deer-flow/pull/2570) [)](https://github.com/bytedance/deer-flow/commit/c5d57b453382d794174f16ab354b930d1a246ca5 'fix: resolve make dev and test-e2e errors (#2570)')

 | 

Apr 26, 2026

 |
| 

[pyproject.toml](https://github.com/bytedance/deer-flow/blob/main/backend/pyproject.toml 'pyproject.toml')

 | 

[pyproject.toml](https://github.com/bytedance/deer-flow/blob/main/backend/pyproject.toml 'pyproject.toml')

 | 

[feat(channels): add Buzz (Nostr) channel connector (](https://github.com/bytedance/deer-flow/commit/d732b90dc3737091dedf842e42eac02ba5230c40 'feat(channels): add Buzz (Nostr) channel connector (#4649)

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

 | 

Aug 5, 2026

 |
| 

[ruff.toml](https://github.com/bytedance/deer-flow/blob/main/backend/ruff.toml 'ruff.toml')

 | 

[ruff.toml](https://github.com/bytedance/deer-flow/blob/main/backend/ruff.toml 'ruff.toml')

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

[sitecustomize.py](https://github.com/bytedance/deer-flow/blob/main/backend/sitecustomize.py 'sitecustomize.py')

 | 

[sitecustomize.py](https://github.com/bytedance/deer-flow/blob/main/backend/sitecustomize.py 'sitecustomize.py')

 | 

[Fix 'make dev' failure in Windows environment (](https://github.com/bytedance/deer-flow/commit/18bbb82f07a6893414fde8ac0ab22c837276ab19 'Fix 'make dev' failure in Windows environment (#3236)

* fix: Solving the problem of "make dev" failing to start in Windows environment

* fix: revert the change to the startup_config and fix the lint errors

* fix: Address Copilot review feedback

- Validate wait-for-port input and avoid PowerShell port interpolation
- Require Python 3 in serve.sh launcher detection
- Keep Windows event loop policy setup in sitecustomize only
- Clarify sitecustomize process-wide backend behavior') [#3236](https://github.com/bytedance/deer-flow/pull/3236) [)](https://github.com/bytedance/deer-flow/commit/18bbb82f07a6893414fde8ac0ab22c837276ab19 'Fix 'make dev' failure in Windows environment (#3236)

* fix: Solving the problem of "make dev" failing to start in Windows environment

* fix: revert the change to the startup_config and fix the lint errors

* fix: Address Copilot review feedback

- Validate wait-for-port input and avoid PowerShell port interpolation
- Require Python 3 in serve.sh launcher detection
- Keep Windows event loop policy setup in sitecustomize only
- Clarify sitecustomize process-wide backend behavior')

 | 

Jun 9, 2026

 |
| 

[uv.lock](https://github.com/bytedance/deer-flow/blob/main/backend/uv.lock 'uv.lock')

 | 

[uv.lock](https://github.com/bytedance/deer-flow/blob/main/backend/uv.lock 'uv.lock')

 | 

[build(deps): bump langgraph-checkpoint-postgres in /backend (](https://github.com/bytedance/deer-flow/commit/a6652956356f86de6776f2fc34833c3275931a1f 'build(deps): bump langgraph-checkpoint-postgres in /backend (#4747)

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

 | 

Aug 11, 2026

 |
| 

View all files

 |

## [README.md](https://github.com/bytedance/deer-flow/tree/main/backend#readme)

Outline

# DeerFlow Backend

**Language:** English | [简体中文](https://github.com/bytedance/deer-flow/blob/main/backend/README_zh.md)

DeerFlow is a LangGraph-based AI super agent with sandbox execution, persistent memory, and extensible tool integration. The backend enables AI agents to execute code, browse the web, manage files, delegate tasks to subagents, and retain context across conversations - all in isolated, per-thread environments.

---

## Architecture

```
                        ┌──────────────────────────────────────┐
                        │          Nginx (Port 2026)           │
                        │      Unified reverse proxy           │
                        └───────┬──────────────────┬───────────┘
                                │
            /api/langgraph/*    │    /api/* (other)
            rewritten to /api/* │
                                ▼
               ┌────────────────────────────────────────┐
               │        Gateway API (8001)              │
               │        FastAPI REST + agent runtime    │
               │                                        │
               │ Models, MCP, Skills, Memory, Uploads,  │
               │ Artifacts, Threads, Runs, Streaming    │
               │                                        │
               │ ┌────────────────────────────────────┐ │
               │ │ Lead Agent                         │ │
               │ │ Middleware Chain, Tools, Subagents │ │
               │ └────────────────────────────────────┘ │
               └────────────────────────────────────────┘
```

**Request Routing** (via Nginx):

- `/api/langgraph/*` → Gateway LangGraph-compatible API - agent interactions, threads, streaming
- `/api/*` (other) → Gateway API - models, MCP, skills, memory, artifacts, uploads, thread-local cleanup
- `/` (non-API) → Frontend - Next.js web interface

---

## Core Components

### Lead Agent

The single LangGraph agent (`lead_agent`) is the runtime entry point, created via `make_lead_agent(config)`. It combines:

- **Dynamic model selection** with thinking and vision support
- **Middleware chain** for cross-cutting concerns (9 middlewares)
- **Tool system** with sandbox, MCP, community, and built-in tools
- **Subagent delegation** for parallel task execution
- **System prompt** with skills injection, memory context, and working directory guidance

### Middleware Chain

Middlewares execute in strict order, each handling a specific concern:

| # | Middleware | Purpose |
| --- | --- | --- |
| 1 | **ThreadDataMiddleware** | Creates per-thread isolated directories (workspace, uploads, outputs) |
| 2 | **UploadsMiddleware** | Injects newly uploaded files into conversation context |
| 3 | **SandboxMiddleware** | Acquires sandbox environment for code execution |
| 4 | **SummarizationMiddleware** | Reduces context when approaching token limits (optional) |
| 5 | **TodoListMiddleware** | Tracks multi-step tasks in plan mode (optional) |
| 6 | **TitleMiddleware** | Auto-generates conversation titles after first exchange |
| 7 | **MemoryMiddleware** | Queues conversations for async memory extraction |
| 8 | **ViewImageMiddleware** | Injects image data for vision-capable models (conditional) |
| 9 | **ClarificationMiddleware** | Intercepts clarification requests and interrupts execution (must be last) |

### Sandbox System

Per-thread isolated execution with virtual path translation:

- **Abstract interface**: `execute_command`, `read_file`, `write_file`, `list_dir`
- **Providers**: `LocalSandboxProvider` (filesystem) and `AioSandboxProvider` (Docker, in community/). Async runtime paths use async sandbox lifecycle hooks so startup, readiness polling, and release do not block the event loop. `AioSandboxProvider` validates active-cache and warm-pool containers during acquire/reuse, dropping definitively dead entries so a thread can provision a fresh sandbox after an unexpected container exit while keeping `get()` as an in-memory lookup. Backend health-check failures are treated as unknown, not dead, and a container that cannot be verified during discovery is simply not adopted (acquire falls through to create instead of failing).
- **Virtual paths**: `/mnt/user-data/{workspace,uploads,outputs}` → thread-specific physical directories
- **Skills path**: `/mnt/skills` → `deer-flow/skills/` directory
- **Skills loading**: Recursively discovers nested `SKILL.md` files under `skills/{public,custom}` and preserves nested container paths
- **SkillScan**: Native offline deterministic scanning runs before the LLM skill scanner on installs and agent-managed skill writes; `CRITICAL` findings block and warning findings become LLM context
- **File-write safety**: `str_replace` serializes read-modify-write per `(sandbox.id, path)` so isolated sandboxes keep concurrency even when virtual paths match
- **Tools**: `bash`, `ls`, `read_file`, `write_file`, `str_replace` (`write_file` overwrites by default and exposes `append` for end-of-file writes; `bash` is disabled by default when using `LocalSandboxProvider`; use `AioSandboxProvider` for isolated shell access)

### Subagent System

Async task delegation with concurrent execution:

- **Built-in agents**: `general-purpose` (full toolset) and `bash` (command specialist, exposed only when shell access is available)
- **Concurrency**: Max 3 subagents per turn, 15-minute timeout
- **Execution**: Background thread pools with status tracking and SSE events
- **Flow**: Agent calls `task()` tool → executor runs subagent in background → polls for completion → returns result

### Memory System

LLM-powered persistent context retention across conversations:

- **Automatic extraction**: Analyzes conversations for user context, facts, and preferences
- **Scope-safe writes**: Middleware extraction stores only durable, descriptive user-level facts; global summaries also require descriptive authority, while contradiction removals and consolidated facts fail closed when scope metadata is missing or task/project-local
- **Atomic replacements**: A contradiction removal linked to a replacement runs only after the replacement survives scope/confidence gates, deduplication, and fact-limit trimming
- **Structured storage**: User context (work, personal, top-of-mind), history, and confidence-scored facts
- **Debounced updates**: Batches updates to minimize LLM calls (configurable wait time)
- **System prompt injection**: Top facts + context injected into agent prompts
- **Run-level memory identity**: `GET /api/threads/{thread_id}/runs/{run_id}/events?event_types=context:memory` returns the SHA-256 identity of the effective hidden memory block without copying memory text into the event store
- **Storage**: JSON file with mtime-based cache invalidation

### Tool Ecosystem

| Category | Tools |
| --- | --- |
| **Sandbox** | `bash`, `ls`, `read_file`, `write_file`, `str_replace` |
| **Built-in** | `present_files`, `ask_clarification`, `view_image`, `task` (subagent) |
| **Community** | Tavily (web search), Jina AI (web fetch), Crawl4AI (web fetch), Firecrawl (scraping), fastCRW (scraping), DuckDuckGo (image search) |
| **MCP** | Any Model Context Protocol server (stdio, SSE, HTTP transports) |
| **Skills** | Domain-specific workflows injected via system prompt |

### Gateway API

FastAPI application providing REST endpoints for frontend integration:

| Route | Purpose |
| --- | --- |
| `GET /api/models` | List available LLM models |
| `GET/PUT /api/mcp/config` | Manage MCP server configurations |
| `POST /api/mcp/cache/reset` | Reset cached MCP tools so they reload on next use |
| `GET/PUT /api/skills` | List and manage skills |
| `POST /api/skills/install` | Install skill from `.skill` archive |
| `GET /api/memory` | Retrieve memory data |
| `POST /api/memory/reload` | Force memory reload |
| `GET /api/memory/config` | Memory configuration |
| `GET /api/memory/status` | Combined config + data |
| `GET /api/threads/{id}/runs/{run_id}/events` | Debug/audit events for one run; filter `event_types=context:memory` for effective memory identity |
| `POST /api/threads/{id}/uploads` | Upload files (auto-converts PDF/PPT/Excel/Word to Markdown, rejects directory paths, auto-renames duplicate filenames in one request) |
| `GET /api/threads/{id}/uploads/list` | List uploaded files |
| `DELETE /api/threads/{id}` | Delete DeerFlow-managed local thread data after LangGraph thread deletion; unexpected failures are logged server-side and return a generic 500 detail |
| `GET /api/threads/{id}/artifacts/{path}` | Serve generated artifacts |

### IM Channels

The IM bridge supports Feishu, Slack, and Telegram. Slack and Telegram still use the final `runs.wait()` response path, while Feishu now streams through `runs.stream(["messages-tuple", "values"])`, serializes rapid same-thread turns inside the channel manager, and updates a single in-thread card per source message in place.

Discord registers each typing-indicator loop before inbound message handling yields and refuses to start new typing work after the channel stops. Typing tasks are owned by the dedicated Discord event loop, so normal shutdown schedules bounded cancellation, awaiting, and map cleanup on that loop before closing the client. The Discord worker also drains the tasks in its `finally` block while its loop is still usable, covering disconnect and exception exits; if `stop()` encounters an already-stopped foreign loop, it never awaits those loop-bound tasks from the main loop. This serializes registration and cleanup across the main and Discord threads while preventing shutdown hangs and cross-loop `RuntimeError`s.

For Feishu card updates, DeerFlow stores the running card's `message_id` per inbound message and patches that same card until the run finishes, preserving the existing `OK` / `DONE` reaction flow. When a follow-up arrives inside an existing Feishu topic while another turn is still running, the later message now waits on the mapped DeerFlow `thread_id`, receives a queued/running card on that exact source message, and keeps a compact source-message blockquote in subsequent patches so rapid consecutive questions remain distinguishable.

---

## Quick Start

### Prerequisites

- Python 3.12+
- [uv](https://docs.astral.sh/uv/) package manager
- API keys for your chosen LLM provider

### Installation

```shell
cd deer-flow

# Copy configuration files
cp config.example.yaml config.yaml

# Install backend dependencies
cd backend
make install
```

### Configuration

Edit `config.yaml` in the project root:

```yaml
models:
  - name: gpt-4o
    display_name: GPT-4o
    use: langchain_openai:ChatOpenAI
    model: gpt-4o
    api_key: $OPENAI_API_KEY
    supports_thinking: false
    supports_vision: true

  - name: gpt-5-responses
    display_name: GPT-5 (Responses API)
    use: langchain_openai:ChatOpenAI
    model: gpt-5
    api_key: $OPENAI_API_KEY
    use_responses_api: true
    output_version: responses/v1
    supports_vision: true
```

Set your API keys:

```shell
export OPENAI_API_KEY="your-api-key-here"
```

### Running

**Full Application** (from project root):

```shell
make dev  # Starts Gateway + Frontend + Nginx
```

Access at: [http://localhost:2026](http://localhost:2026)

**Backend Only** (from backend directory):

```shell
# Gateway API + embedded agent runtime
make dev
```

Direct access: Gateway at [http://localhost:8001](http://localhost:8001)

**Terminal Workbench (TUI)** — a terminal-native UI over the embedded harness, no services required:

```shell
uv pip install 'deerflow-harness[tui]'   # optional 'textual' dependency
deerflow                                 # launch the TUI
deerflow --print "summarize this repo"   # headless one-shot
deerflow --recursion-limit 250 --print "run a longer task"
```

Sessions opened in the TUI appear in the Web UI sidebar (it writes the shared `threads_meta` store under the local default user). See [docs/TUI.md](https://github.com/bytedance/deer-flow/blob/main/backend/docs/TUI.md).

---

## Project Structure

```
backend/
├── packages/harness/           # deerflow-harness package (import: deerflow.*)
│   └── deerflow/
│       ├── agents/             # Agent system
│       │   ├── lead_agent/     # Main agent (factory, prompts)
│       │   ├── middlewares/    # Middleware components
│       │   ├── memory/         # Memory extraction & storage
│       │   └── thread_state.py # ThreadState schema
│       ├── sandbox/            # Sandbox execution
│       │   ├── local/          # Local filesystem provider
│       │   ├── sandbox.py      # Abstract interface
│       │   ├── tools.py        # bash, ls, read/write/str_replace
│       │   └── middleware.py   # Sandbox lifecycle
│       ├── subagents/          # Subagent delegation
│       │   ├── builtins/       # general-purpose, bash agents
│       │   ├── executor.py     # Background execution engine
│       │   └── registry.py     # Agent registry
│       ├── tools/builtins/     # Built-in tools
│       ├── mcp/                # MCP protocol integration
│       ├── models/             # Model factory
│       ├── skills/             # Skill discovery & loading
│       ├── config/             # Configuration system
│       ├── runtime/            # Embedded run execution (RunManager, StreamBridge)
│       ├── persistence/        # Checkpointer/store engines & schema migrations
│       ├── guardrails/         # Pre-tool-call authorization providers
│       ├── tracing/            # Tracer factory & trace metadata
│       ├── uploads/            # Uploads manager
│       ├── tui/                # Terminal UI (`deerflow` console script)
│       ├── community/          # Community tools & providers
│       ├── reflection/         # Dynamic module loading
│       └── utils/              # Utilities
├── app/                        # FastAPI Gateway + IM channels (import: app.*)
│   ├── gateway/                # Gateway API
│   │   ├── app.py              # Application setup
│   │   └── routers/            # Route modules
│   └── channels/               # IM channel integrations
├── docs/                       # Documentation
├── tests/                      # Test suite
├── langgraph.json              # LangGraph graph registry for tooling/Studio compatibility
├── pyproject.toml              # Python dependencies
├── Makefile                    # Development commands
└── Dockerfile                  # Container build
```

`langgraph.json` is not the default service entrypoint. The scripts and Docker deployments run the Gateway embedded runtime; the file is kept for LangGraph tooling, Studio, or direct LangGraph Server compatibility.

---

## Configuration

### Main Configuration (`config.yaml`)

Place in project root. Config values starting with `$` resolve as environment variables.

Key sections:

- `models` - LLM configurations with class paths, API keys, thinking/vision flags
- `tools` - Tool definitions with module paths and groups
- `tool_groups` - Logical tool groupings
- `sandbox` - Execution environment provider
- `skills` - Skills directory paths
- `title` - Auto-title generation settings
- `summarization` - Context summarization settings
- `subagents` - Subagent system (enabled/disabled)
- `memory` - Memory system settings (enabled, storage, debounce, facts limits)

Provider note:

- `models[*].use` references provider classes by module path (for example `langchain_openai:ChatOpenAI`).
- If a provider module is missing, DeerFlow now returns an actionable error with install guidance (for example `uv add langchain-google-genai`).

### Extensions Configuration (`extensions_config.json`)

MCP servers and skill states in a single file:

```json
{
  "mcpServers": {
    "github": {
      "enabled": true,
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {"GITHUB_TOKEN": "$GITHUB_TOKEN"}
    },
    "secure-http": {
      "enabled": true,
      "type": "http",
      "url": "https://api.example.com/mcp",
      "oauth": {
        "enabled": true,
        "token_url": "https://auth.example.com/oauth/token",
        "grant_type": "client_credentials",
        "client_id": "$MCP_OAUTH_CLIENT_ID",
        "client_secret": "$MCP_OAUTH_CLIENT_SECRET"
      }
    },
    "postgres": {
      "enabled": false,
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-postgres", "postgresql://localhost/mydb"],
      "description": "PostgreSQL database access",
      "routing": {
        "mode": "prefer",
        "priority": 50,
        "keywords": ["orders", "users", "SQL", "database", "table"]
      },
      "tools": {
        "query": {
          "routing": {
            "priority": 100,
            "keywords": ["query database", "orders table", "metrics"]
          }
        }
      }
    }
  },
  "skills": {
    "pdf-processing": {"enabled": true}
  }
}
```

`routing` adds soft MCP preference hints to the agent prompt. It helps the model prefer a configured MCP tool for matching requests without forbidding other tools. When `tool_search.enabled=true` defers MCP schemas, matching routing metadata can auto-promote up to `tool_search.auto_promote_top_k` deferred schemas before the model call.

### Environment Variables

- `DEER_FLOW_CONFIG_PATH` - Override config.yaml location
- `DEER_FLOW_EXTENSIONS_CONFIG_PATH` - Override extensions\_config.json location
- Model API keys: `OPENAI_API_KEY`, `ANTHROPIC_API_KEY`, `DEEPSEEK_API_KEY`, etc.
- Tool API keys: `TAVILY_API_KEY`, `GITHUB_TOKEN`, etc.

### LangSmith Tracing

DeerFlow has built-in [LangSmith](https://smith.langchain.com) integration for observability. When enabled, all LLM calls, agent runs, tool executions, and middleware processing are traced and visible in the LangSmith dashboard.

**Setup:**

1. Sign up at [smith.langchain.com](https://smith.langchain.com) and create a project.
2. Add the following to your `.env` file in the project root:

```shell
LANGSMITH_TRACING=true
LANGSMITH_ENDPOINT=https://api.smith.langchain.com
LANGSMITH_API_KEY=lsv2_pt_xxxxxxxxxxxxxxxx
LANGSMITH_PROJECT=xxx
```

**Legacy variables:** The `LANGCHAIN_TRACING_V2`, `LANGCHAIN_API_KEY`, `LANGCHAIN_PROJECT`, and `LANGCHAIN_ENDPOINT` variables are also supported for backward compatibility. `LANGSMITH_*` variables take precedence when both are set.

### Langfuse Tracing

DeerFlow also supports [Langfuse](https://langfuse.com) observability for LangChain-compatible runs.

Add the following to your `.env` file:

```shell
LANGFUSE_TRACING=true
LANGFUSE_PUBLIC_KEY=pk-lf-xxxxxxxxxxxxxxxx
LANGFUSE_SECRET_KEY=sk-lf-xxxxxxxxxxxxxxxx
LANGFUSE_BASE_URL=https://cloud.langfuse.com
```

If you are using a self-hosted Langfuse deployment, set `LANGFUSE_BASE_URL` to your Langfuse host.

### Dual Provider Behavior

If both LangSmith and Langfuse are enabled, DeerFlow initializes and attaches both callbacks so the same run data is reported to both systems.

If a provider is explicitly enabled but required credentials are missing, or the provider callback cannot be initialized, DeerFlow raises an error when tracing is initialized during model creation instead of silently disabling tracing.

**Docker:** In `docker-compose.yaml`, tracing is disabled by default (`LANGSMITH_TRACING=false`). Set `LANGSMITH_TRACING=true` and/or `LANGFUSE_TRACING=true` in your `.env`, together with the required credentials, to enable tracing in containerized deployments.

---

## Development

### Commands

```shell
make install    # Install dependencies
make dev        # Run Gateway API + embedded agent runtime with safe reload (port 8001)
make gateway    # Run Gateway API without reload (port 8001)
make lint       # Run linter (ruff)
make format     # Format code (ruff)
make detect-blocking-io  # Inventory blocking IO that may block the backend event loop
make migrate-rev MSG="..."  # Autogenerate a new alembic revision against the live ORM models
```

`make dev` pre-creates and excludes `DEER_FLOW_HOME` (by default `backend/.deer-flow`) and `backend/sandbox` from Uvicorn's reload watcher. Use this target instead of a bare `uvicorn --reload`: agent tasks write Python and other runtime files under `DEER_FLOW_HOME`, and watching that directory can restart the Gateway during an active run.

### Schema Migrations

DeerFlow's application tables (`runs`, `threads_meta`, `feedback`, `users`, `run_events`, and the `channel_*` tables) are owned by alembic. The Gateway runs `alembic upgrade head` automatically on startup via `bootstrap_schema(engine, backend=...)`, so operators do not run `alembic` manually in production. Bootstrap is concurrency-safe (Postgres advisory lock across processes; per-engine `asyncio.Lock` inside one SQLite process) and idempotent against pre-existing schemas (empty / legacy / versioned).

When you add or change an ORM model, ship the change as a new revision under `packages/harness/deerflow/persistence/migrations/versions/`:

```shell
make migrate-rev MSG="add foo column to runs"
```

The target invokes `scripts/_autogen_revision.py`, which builds a fresh temp SQLite at `head` and diffs the live models against it — so a clean checkout does not need a pre-existing `./data/deerflow.db`. Review the generated file and switch raw `op.add_column` / `op.drop_column` calls to the idempotent helpers in `migrations/_helpers.py` before committing. There is no `make migrate` / `make migrate-stamp` target on purpose — Gateway startup is the only execution path, which keeps operational mistakes off the table. See `backend/CLAUDE.md` (Schema Migrations) for the full design.

### Code Style

- **Linter/Formatter**: `ruff`
- **Line length**: 240 characters
- **Python**: 3.12+ with type hints
- **Quotes**: Double quotes
- **Indentation**: 4 spaces

### Testing

```shell
# Offline backend suite (live external-API tests are excluded)
make test

# Explicit real-API DeerFlowClient integration suite
make test-live
```

The live suite requires a valid root `config.yaml` and API credentials. It may incur API costs or create local sandboxes, artifacts, and files, so it is not part of default test runs or CI. Direct pytest invocation of `tests/test_client_live.py` also requires `DEER_FLOW_RUN_LIVE_TESTS=1`.

`make detect-blocking-io` statically scans backend business code for blocking IO that may run on the backend event loop and is not test-coverage-bound. It prints a concise summary for human review and writes complete JSON findings to `.deer-flow/blocking-io-findings.json` at the repository root (regardless of whether the target is invoked from the repo root or from `backend/`). JSON findings include both broad IO category and review-oriented fields such as `priority`, `location`, `blocking_call`, `event_loop_exposure`, `reason`, and `code`. `priority` is a deterministic review ordering from the operation type, not proof of a bug. Bare-name same-file calls are resolved by function name, so duplicate helper names in one file can conservatively over-report async reachability.

---

## Technology Stack

- **LangGraph** (1.0.6+) - Agent framework and multi-agent orchestration
- **LangChain** (1.2.3+) - LLM abstractions and tool system
- **FastAPI** (0.115.0+) - Gateway REST API
- **langchain-mcp-adapters** - Model Context Protocol support
- **agent-sandbox** - Sandboxed code execution
- **markitdown** - Multi-format document conversion
- **tavily-python** / **firecrawl-py** - Web search and scraping

---

## Documentation

- [Configuration Guide](https://github.com/bytedance/deer-flow/blob/main/backend/docs/CONFIGURATION.md)
- [Architecture Details](https://github.com/bytedance/deer-flow/blob/main/backend/docs/ARCHITECTURE.md)
- [API Reference](https://github.com/bytedance/deer-flow/blob/main/backend/docs/API.md)
- [File Upload](https://github.com/bytedance/deer-flow/blob/main/backend/docs/FILE_UPLOAD.md)
- [Path Examples](https://github.com/bytedance/deer-flow/blob/main/backend/docs/PATH_EXAMPLES.md)
- [Context Summarization](https://github.com/bytedance/deer-flow/blob/main/backend/docs/summarization.md)
- [Plan Mode](https://github.com/bytedance/deer-flow/blob/main/backend/docs/plan_mode_usage.md)
- [Setup Guide](https://github.com/bytedance/deer-flow/blob/main/backend/docs/SETUP.md)

---

## License

See the [LICENSE](https://github.com/bytedance/deer-flow/blob/main/LICENSE) file in the project root.

## Contributing

See [CONTRIBUTING.md](https://github.com/bytedance/deer-flow/blob/main/backend/CONTRIBUTING.md) for contribution guidelines.