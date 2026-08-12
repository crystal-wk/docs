# Source: https://github.com/bytedance/deer-flow/tags

### Uh oh!

There was an error while loading. [Please reload this page]().

[bytedance](https://github.com/bytedance) / **[deer-flow](https://github.com/bytedance/deer-flow)** Public

- [Notifications](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow) You must be signed in to change notification settings
- [Fork 10.9k](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow)
- [Star 79.8k](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow)

# Tags: bytedance/deer-flow

Tags

## [v2.0.0](https://github.com/bytedance/deer-flow/releases/tag/v2.0.0)

Toggle v2.0.0's commit message

```
Updated the v2.0.0 release note
```

- Jun 25, 2026
- [7e7f041](https://github.com/bytedance/deer-flow/commit/7e7f0410797693cf882594555ba414e0361d4c6f)
- [zip](https://github.com/bytedance/deer-flow/archive/refs/tags/v2.0.0.zip)
- [tar.gz](https://github.com/bytedance/deer-flow/archive/refs/tags/v2.0.0.tar.gz)
- Immutable . This tag is bound to an immutable release and cannot be reused.

- [Notes](https://github.com/bytedance/deer-flow/releases/tag/v2.0.0)

## [v2.0.0-rc1](https://github.com/bytedance/deer-flow/releases/tag/v2.0.0-rc1)

Toggle v2.0.0-rc1's commit message

Verified

# Verified

This commit was created on GitHub.com and signed with GitHub’s **verified signature**.

GPG key ID: B5690EEEBB952194

Verified

[Learn about vigilant mode](https://docs.github.com/github/authenticating-to-github/displaying-verification-statuses-for-all-of-your-commits)

```
Prepare 2.0.0 release (#3603)

* bump the version of deer-flow to 2.0.0

* Added CHANGELOG to the release branch

* Update the changelogs files with the latest changes
```

- Jun 19, 2026
- [98127f5](https://github.com/bytedance/deer-flow/commit/98127f58456b254df96cc7da6f3f1b5f2528bef5)
- [zip](https://github.com/bytedance/deer-flow/archive/refs/tags/v2.0.0-rc1.zip)
- [tar.gz](https://github.com/bytedance/deer-flow/archive/refs/tags/v2.0.0-rc1.tar.gz)

## [v2.0.0-rc0](https://github.com/bytedance/deer-flow/releases/tag/v2.0.0-rc0)

Toggle v2.0.0-rc0's commit message

Verified

# Verified

This commit was created on GitHub.com and signed with GitHub’s **verified signature**.

GPG key ID: B5690EEEBB952194

Verified

[Learn about vigilant mode](https://docs.github.com/github/authenticating-to-github/displaying-verification-statuses-for-all-of-your-commits)

```
fix(frontend): cap deeply nested list indentation to prevent render c…

…rash (#3393) (#3570)

* fix(frontend): cap deeply nested list indentation to prevent render crash

Deeply nested lists make marked's recursive list tokenizer overflow the
call stack during Streamdown's lexing useMemo, throwing an uncaught
"RangeError: Maximum call stack size exceeded" that replaces the chat
route with an error page (issue #3393); on larger stacks the same input
exhausts the heap, which the render error boundary cannot catch.

Mirror the existing capBlockquoteNesting guard with capListNesting, which
clamps leading whitespace to 200 columns (~100 nesting levels) only when
pathologically deep indentation is present, leaving normal content and
fenced code untouched. Wire both through capMarkdownNesting.

* fix(frontend): satisfy prettier format check in preprocess test

* fix(frontend): exempt indented code from list-indent cap (PR #3570 review)

* fix(frontend): keep capping all deep indentation outside fenced code

Revert the indented-code exemption from the PR #3570 review nit. Taken
literally the suggested guard (insideFence || INDENTED_CODE_RE.test(line))
no-ops capListNesting, because INDENTED_CODE_RE matches every line with
4+ leading spaces — i.e. exactly the deep-indent lines the cap targets.
A context-aware exemption (only treat 4+-space lines as code after a
blank line) instead reopens the crash: blank-separated deeply nested list
items get exempted and still blow up marked (verified: OOM at depth ~1.5k).

Unlike blockquotes (markers take <=3 leading spaces, so deep-quote lines
never look like indented code), list vs. indented-code indentation is
ambiguous line-by-line, so any exemption is exploitable. Keep capping all
deep indentation outside fenced code; the only cost is mild corruption of
a >200-column indented-code line, which never occurs in real content and
is strictly preferable to a render crash. Add a regression test locking
the blank-line case.
```

- Jun 14, 2026
- [25fbd25](https://github.com/bytedance/deer-flow/commit/25fbd25b05b962ac5ae9fdcfbb3902a59ebebf6b)
- [zip](https://github.com/bytedance/deer-flow/archive/refs/tags/v2.0.0-rc0.zip)
- [tar.gz](https://github.com/bytedance/deer-flow/archive/refs/tags/v2.0.0-rc0.tar.gz)

## [v2.0-m1-rc3](https://github.com/bytedance/deer-flow/releases/tag/v2.0-m1-rc3)

Toggle v2.0-m1-rc3's commit message

Verified

# Verified

This commit was created on GitHub.com and signed with GitHub’s **verified signature**.

GPG key ID: B5690EEEBB952194

Verified

[Learn about vigilant mode](https://docs.github.com/github/authenticating-to-github/displaying-verification-statuses-for-all-of-your-commits)

```
fix(skills): harden slash skill activation across chat channels (#3466)

* support slash skill activation

* format slash skill activation

* Preserve slash skill activation with uploads

* Address slash skill review feedback

* Address slash skill follow-up review

* Fix lazy slash skill storage resolution

* Keep slash skill activation out of system prompt

* Address slash skill review issues

* fix: harden slash skill command handling

* feat(frontend): add slash skill autocomplete

* fix: address slash skill review feedback

* fix: preserve slash skill text for IM uploads
```

- Jun 9, 2026
- [16391e3](https://github.com/bytedance/deer-flow/commit/16391e35ab7106e3e1f706139dd043dadf62ca93)
- [zip](https://github.com/bytedance/deer-flow/archive/refs/tags/v2.0-m1-rc3.zip)
- [tar.gz](https://github.com/bytedance/deer-flow/archive/refs/tags/v2.0-m1-rc3.tar.gz)

## [v2.0-m1-rc2](https://github.com/bytedance/deer-flow/releases/tag/v2.0-m1-rc2)

Toggle v2.0-m1-rc2's commit message

Verified

# Verified

This commit was created on GitHub.com and signed with GitHub’s **verified signature**.

GPG key ID: B5690EEEBB952194

Verified

[Learn about vigilant mode](https://docs.github.com/github/authenticating-to-github/displaying-verification-statuses-for-all-of-your-commits)

```
feat(subagents): extend deferred MCP tool loading to subagents (#3432)

* feat(subagents): extend deferred MCP tool loading to subagents (#3341)

Subagents now reuse the lead agent's deferred-tool path: when
tool_search.enabled, MCP tool schemas are withheld from the model and
surfaced by name in <available-deferred-tools>, fetched on demand via the
generated tool_search helper. DeferredToolFilterMiddleware deterministically
rewrites request.tools to hide the deferred schemas (the prompt section is
discovery only, not enforcement).

Consolidates the assembly into deerflow.tools.builtins.tool_search, now the
single home for both assemble_deferred_tools (centralized fail-closed guard,
replacing the lead-only private _assemble_deferred) and the relocated
get_deferred_tools_prompt_section. Shared by every build path: lead agent,
embedded client, and subagent executor.

tool_search is appended after the subagent's name-level tool policy and is
treated as infrastructure: its catalog is built from the already
policy-filtered list, so it can never surface a tool the policy denied.

Follow-up to #3370. Fixes #3341.

* test(subagents): assert the real middleware builder emits a working deferred filter (#3341)

The existing recipe test hand-constructs DeferredToolFilterMiddleware, so it
cannot catch a regression in how build_subagent_runtime_middlewares (the call
executor._create_agent actually makes) wires the deferred setup into the
filter. Add a test that sources the filter from the real builder given a real
setup and runs it through a graph: a wrong catalog hash would silently stop
promotion, a dropped filter would stop hiding — both now caught.

Running the full real middleware stack is intentionally avoided (the other
runtime middlewares need sandbox/thread infra to execute, which would make the
test flaky); their attachment + ordering before Safety stays locked in
test_tool_error_handling_middleware.py.

* test(subagents): keep executor tests config-free in CI

* chore: trigger ci

* Potential fix for pull request finding

Co-authored-by: Copilot Autofix powered by AI <175728472+Copilot@users.noreply.github.com>

---------

Co-authored-by: Willem Jiang <willem.jiang@gmail.com>
Co-authored-by: Copilot Autofix powered by AI <175728472+Copilot@users.noreply.github.com>
```

- Jun 8, 2026
- [3b6dd0a](https://github.com/bytedance/deer-flow/commit/3b6dd0a4e32ec5133382573514f9c728f4c99945)
- [zip](https://github.com/bytedance/deer-flow/archive/refs/tags/v2.0-m1-rc2.zip)
- [tar.gz](https://github.com/bytedance/deer-flow/archive/refs/tags/v2.0-m1-rc2.tar.gz)

## [v2.0-m1-rc1](https://github.com/bytedance/deer-flow/releases/tag/v2.0-m1-rc1)

Toggle v2.0-m1-rc1's commit message

Verified

# Verified

This commit was created on GitHub.com and signed with GitHub’s **verified signature**.

GPG key ID: B5690EEEBB952194

Verified

[Learn about vigilant mode](https://docs.github.com/github/authenticating-to-github/displaying-verification-statuses-for-all-of-your-commits)

```
fix(harness)!: hydrate runs from RunStore and persist interrupted sta…

…tus (#2932)

* fix(harness): hydrate run history from RunStore and persist cancellation status

fix:
- Make RunManager.get() async and hydrate from RunStore when in-memory record is missing
- Merge store rows into list_by_thread() with in-memory precedence for active runs
- Persist interrupted status to RunStore in cancel() and create_or_reject(interrupt|rollback)
- Extract _persist_status() to reuse the best-effort store update pattern
- Await run_mgr.get() in all gateway endpoints
- Return 409 with distinct message for store-only runs not active on current worker

Closes #2812, Closes #2813

Co-Authored-By: Claude Opus 4.7 <noreply@anthropic.com>

* fix(harness): consistent sort and guarded hydration in RunManager

fix:
- list_by_thread() now sorts by created_at desc (newest first) even when
  no RunStore is configured, matching the store-backed code path
- guard _record_from_store() call sites in get() and list_by_thread()
  with best-effort error handling so a single malformed store row cannot
  turn read paths into 500s

test:
- update test_list_by_thread assertion to expect newest-first order
- seed MemoryRunStore via public put() API instead of writing to _runs

* fix(harness): guard store-only runs from streaming and fix get() TOCTOU

Add RunRecord.store_only flag set by _record_from_store so callers can
distinguish hydrated history from live in-memory runs.  join_run and
stream_existing_run (action=None) now return 409 instead of hanging
forever on an empty MemoryStreamBridge channel.

Re-check _runs under lock after the store await in RunManager.get() so a
concurrent create() that lands between the two checks returns the
authoritative in-memory record rather than a stale store-hydrated copy.

Co-Authored-By: Claude Sonnet 4 <noreply@anthropic.com>

* fix(harness): reorder bridge fetch in join_run and make list_by_thread limit explicit

Move get_stream_bridge() after the store_only guard in join_run so a
missing bridge cannot produce 503 for historical runs before the 409
guard fires.

Add limit parameter to RunManager.list_by_thread (default 100, matching
the store's page size) and pass it explicitly to the store call.
Update docstring to document the limit instead of claiming all runs are
returned.

Co-Authored-By: Claude Sonnet 4 <noreply@anthropic.com>

* fix(harness): cap list_by_thread result to limit after merge

Apply [:limit] to all return paths in list_by_thread so the method
consistently returns at most limit records regardless of how many
in-memory runs exist, making the limit parameter a true upper bound
on the response size rather than just a store-query hint.

Co-Authored-By: Claude Sonnet 4 <noreply@anthropic.com>

* fix `list_by_thread` docstring

Co-authored-by: Copilot Autofix powered by AI <175728472+Copilot@users.noreply.github.com>

* fix(runtime): add update_model_name to RunStore to prevent SQL integrity errors

RunManager.update_model_name() was calling _persist_to_store() which uses
RunStore.put(), but RunRepository.put() is insert-only. This caused integrity
errors when updating model_name for existing runs in SQL-backed stores.

fix:
- Add abstract update_model_name method to RunStore base class
- Implement update_model_name in MemoryRunStore
- Implement update_model_name in RunRepository with proper normalization
- Add _persist_model_name helper in RunManager
- Update RunManager.update_model_name to use the new method

test:
- Add tests for update_model_name functionality
- Add integration tests for RunManager with SQL-backed store

Co-Authored-By: Claude Opus 4.7 <noreply@anthropic.com>

* fix(runtime): handle NULL status/on_disconnect in _record_from_store

`dict.get(key, default)` only uses the default when the key is absent,
so a SQL row with an explicit NULL status would pass `None` to
`RunStatus(None)` and raise, breaking hydration for otherwise valid rows.
Switch to `row.get(...) or fallback` so both missing and NULL values
get a safe default. Add tests for get() and list_by_thread() with a
NULL status row to prevent regression.

Co-Authored-By: Claude Sonnet 4 <noreply@anthropic.com>

* fix(runs): address PR review feedback on store consistency changes

- Fix list_by_thread limit semantics: pass store_limit = max(0, limit - len(memory_records)) to store so newer store records are not crowded out by in-memory records
- Remove dead code: cancelled guard after raise is always True, simplify to if wait and record.task
- Document _record_from_store NULL fallback policy (status→pending, on_disconnect→cancel) in docstring

Co-Authored-By: Claude Sonnet 4 <noreply@anthropic.com>

---------

Co-authored-by: Claude Opus 4.7 <noreply@anthropic.com>
Co-authored-by: Copilot Autofix powered by AI <175728472+Copilot@users.noreply.github.com>
```

- May 18, 2026
- [c810e9f](https://github.com/bytedance/deer-flow/commit/c810e9f809222ad8449348667b5c438803c7885e)
- [zip](https://github.com/bytedance/deer-flow/archive/refs/tags/v2.0-m1-rc1.zip)
- [tar.gz](https://github.com/bytedance/deer-flow/archive/refs/tags/v2.0-m1-rc1.tar.gz)

## [v2.0-m1-rc0](https://github.com/bytedance/deer-flow/releases/tag/v2.0-m1-rc0)

Toggle v2.0-m1-rc0's commit message

Verified

# Verified

This commit was created on GitHub.com and signed with GitHub’s **verified signature**.

GPG key ID: B5690EEEBB952194

Verified

[Learn about vigilant mode](https://docs.github.com/github/authenticating-to-github/displaying-verification-statuses-for-all-of-your-commits)

```
fix(i18n): add Chinese translations for account settings page (#2712)

The account settings page had all user-facing strings (profile labels,
  password form placeholders, validation messages, button text) hardcoded
  in English. Replace them with i18n translation keys so the page renders
  correctly when the locale is set to Chinese.

 Fixed #2710
```

- May 4, 2026
- [af6e48c](https://github.com/bytedance/deer-flow/commit/af6e48ccaaf816cc0990439820b13d59a4499bda)
- [zip](https://github.com/bytedance/deer-flow/archive/refs/tags/v2.0-m1-rc0.zip)
- [tar.gz](https://github.com/bytedance/deer-flow/archive/refs/tags/v2.0-m1-rc0.tar.gz)

## [v2.0-m0](https://github.com/bytedance/deer-flow/releases/tag/v2.0-m0)

Toggle v2.0-m0's commit message

```
Tag the v2.0-m1
```

- Apr 13, 2026
- [979a461](https://github.com/bytedance/deer-flow/commit/979a461af5bd4e61ec1654c99f3ec9589a2edbb3)
- [zip](https://github.com/bytedance/deer-flow/archive/refs/tags/v2.0-m0.zip)
- [tar.gz](https://github.com/bytedance/deer-flow/archive/refs/tags/v2.0-m0.tar.gz)