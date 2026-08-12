# Source: https://github.com/bytedance/deer-flow/commits?author=ajayr

### Uh oh!

There was an error while loading. [Please reload this page]().

[bytedance](https://github.com/bytedance) / **[deer-flow](https://github.com/bytedance/deer-flow)** Public

- [Notifications](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow) You must be signed in to change notification settings
- [Fork 10.9k](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow)
- [Star 79.8k](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow)

 ## Branch selector

main

## User selector

![](https://avatars.githubusercontent.com/u/809529?v=4&size=32)

ajayr

## Datepicker

All time

## Commit history

### Commits on Aug 12, 2026

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

### Commits on Aug 5, 2026

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

### Commits on Jul 27, 2026

- #### [fix(browserless): accept the](https://github.com/bytedance/deer-flow/commit/6456c35675dfbfdfc25ec5346e52ed8a8de1c5ef 'fix(browserless): accept the `timeout` config key and harden coercion (#4519)

 `browserless` reads `cfg["timeout_s"]`, while its sibling web providers
 `crawl4ai` and `jina_ai` read `cfg["timeout"]`. Tool configs allow extra
 fields, so the unrecognised spelling is dropped without a diagnostic: someone
 adapting one provider's config snippet for another silently gets the 30s
 default instead of the timeout they set. (Observed in the other direction, on a
 deployment whose crawl4ai entry carried `timeout_s`.)

 Accept both keys, preferring the documented `timeout_s` when both are present.

 While adding coverage, two pre-existing bugs in the same three lines surfaced,
 both already guarded in crawl4ai/jina_ai but not here:

 - `timeout_s: "30s"` (or any non-numeric string) raised ValueError out of
 `float(raw)` during tool construction rather than falling back.
 - `timeout_s: off` -- YAML parses that as `False`, and `float(False)` is
 `0.0`, so every request timed out immediately against a healthy server.

 `_coerce_timeout` now mirrors the sibling providers: booleans and unparsable
 strings fall back to the default, with a warning for the string case.

 Tests: five cases in tests/test_browserless_client.py covering both keys, the
 precedence order, and both coercion bugs. Verified red before the fix (3 of 5
 fail) and green after.

 Co-authored-by: Claude Opus 5 <noreply@anthropic.com>') ``[timeout](https://github.com/bytedance/deer-flow/commit/6456c35675dfbfdfc25ec5346e52ed8a8de1c5ef 'fix(browserless): accept the `timeout` config key and harden coercion (#4519)  `browserless` reads `cfg["timeout_s"]`, while its sibling web providers `crawl4ai` and `jina_ai` read `cfg["timeout"]`. Tool configs allow extra fields, so the unrecognised spelling is dropped without a diagnostic: someone adapting one provider's config snippet for another silently gets the 30s default instead of the timeout they set. (Observed in the other direction, on a deployment whose crawl4ai entry carried `timeout_s`.)  Accept both keys, preferring the documented `timeout_s` when both are present.  While adding coverage, two pre-existing bugs in the same three lines surfaced, both already guarded in crawl4ai/jina_ai but not here:  - `timeout_s: "30s"` (or any non-numeric string) raised ValueError out of   `float(raw)` during tool construction rather than falling back. - `timeout_s: off` -- YAML parses that as `False`, and `float(False)` is   `0.0`, so every request timed out immediately against a healthy server.  `_coerce_timeout` now mirrors the sibling providers: booleans and unparsable strings fall back to the default, with a warning for the string case.  Tests: five cases in tests/test_browserless_client.py covering both keys, the precedence order, and both coercion bugs. Verified red before the fix (3 of 5 fail) and green after.  Co-authored-by: Claude Opus 5 <noreply@anthropic.com>')`` [config key and harden coercion (](https://github.com/bytedance/deer-flow/commit/6456c35675dfbfdfc25ec5346e52ed8a8de1c5ef 'fix(browserless): accept the `timeout` config key and harden coercion (#4519)

 `browserless` reads `cfg["timeout_s"]`, while its sibling web providers
 `crawl4ai` and `jina_ai` read `cfg["timeout"]`. Tool configs allow extra
 fields, so the unrecognised spelling is dropped without a diagnostic: someone
 adapting one provider's config snippet for another silently gets the 30s
 default instead of the timeout they set. (Observed in the other direction, on a
 deployment whose crawl4ai entry carried `timeout_s`.)

 Accept both keys, preferring the documented `timeout_s` when both are present.

 While adding coverage, two pre-existing bugs in the same three lines surfaced,
 both already guarded in crawl4ai/jina_ai but not here:

 - `timeout_s: "30s"` (or any non-numeric string) raised ValueError out of
 `float(raw)` during tool construction rather than falling back.
 - `timeout_s: off` -- YAML parses that as `False`, and `float(False)` is
 `0.0`, so every request timed out immediately against a healthy server.

 `_coerce_timeout` now mirrors the sibling providers: booleans and unparsable
 strings fall back to the default, with a warning for the string case.

 Tests: five cases in tests/test_browserless_client.py covering both keys, the
 precedence order, and both coercion bugs. Verified red before the fix (3 of 5
 fail) and green after.

 Co-authored-by: Claude Opus 5 <noreply@anthropic.com>') [#4519](https://github.com/bytedance/deer-flow/pull/4519) [)](https://github.com/bytedance/deer-flow/commit/6456c35675dfbfdfc25ec5346e52ed8a8de1c5ef 'fix(browserless): accept the `timeout` config key and harden coercion (#4519)

 `browserless` reads `cfg["timeout_s"]`, while its sibling web providers
 `crawl4ai` and `jina_ai` read `cfg["timeout"]`. Tool configs allow extra
 fields, so the unrecognised spelling is dropped without a diagnostic: someone
 adapting one provider's config snippet for another silently gets the 30s
 default instead of the timeout they set. (Observed in the other direction, on a
 deployment whose crawl4ai entry carried `timeout_s`.)

 Accept both keys, preferring the documented `timeout_s` when both are present.

 While adding coverage, two pre-existing bugs in the same three lines surfaced,
 both already guarded in crawl4ai/jina_ai but not here:

 - `timeout_s: "30s"` (or any non-numeric string) raised ValueError out of
 `float(raw)` during tool construction rather than falling back.
 - `timeout_s: off` -- YAML parses that as `False`, and `float(False)` is
 `0.0`, so every request timed out immediately against a healthy server.

 `_coerce_timeout` now mirrors the sibling providers: booleans and unparsable
 strings fall back to the default, with a warning for the string case.

 Tests: five cases in tests/test_browserless_client.py covering both keys, the
 precedence order, and both coercion bugs. Verified red before the fix (3 of 5
 fail) and green after.

 Co-authored-by: Claude Opus 5 <noreply@anthropic.com>')

 Show description for 6456c35

 ![ajayr](https://avatars.githubusercontent.com/u/809529?v=4&size=32)![claude](https://avatars.githubusercontent.com/u/81847?v=4&size=32)

 [ajayr](https://github.com/bytedance/deer-flow/commits?author=ajayr)

 and

 [claude](https://github.com/bytedance/deer-flow/commits?author=claude)

 authoredJul 27, 2026

 ·

 11 / 11

 Verified

 [6456c35](https://github.com/bytedance/deer-flow/commit/6456c35675dfbfdfc25ec5346e52ed8a8de1c5ef)View commit details

 Copy full SHA for 6456c35

 Browse repository at this point

- #### [docs(config): Crawl4AI >= 0.9 requires a bearer token (](https://github.com/bytedance/deer-flow/commit/28553040feffd645b8a99393f5fa0f54f73f01cb 'docs(config): Crawl4AI >= 0.9 requires a bearer token (#4518)

 The commented Crawl4AI web_fetch example still describes the pre-0.9 server:
 it says JWT auth is off by default, marks `token:` as only needed "if the
 server has JWT auth enabled", and pins 0.8.6 in the docker run line.

 Crawl4AI 0.9.0 made the Docker API server secure-by-default. Auth is on for
 every request except GET /health, and a server started without
 CRAWL4AI_API_TOKEN binds 127.0.0.1 only. Following the current example against
 a current image therefore yields either HTTP 401 on every fetch, or a server a
 containerised DeerFlow cannot reach -- with no hint that auth is the cause.

 0.8.6 is also worth moving off: 0.8.7 fixed two pre-auth RCEs (CVSS 9.8), and
 0.8.8/0.8.9 closed SSRF gaps in the same server.

 No code change is needed -- Crawl4AiClient already sends
 `Authorization: Bearer <token>` whenever `token` is set, so this is purely
 the example catching up with the upstream server. Comment-only, so
 config_version is unchanged.

 Co-authored-by: Claude Opus 5 <noreply@anthropic.com>') [#4518](https://github.com/bytedance/deer-flow/pull/4518) [)](https://github.com/bytedance/deer-flow/commit/28553040feffd645b8a99393f5fa0f54f73f01cb 'docs(config): Crawl4AI >= 0.9 requires a bearer token (#4518)

 The commented Crawl4AI web_fetch example still describes the pre-0.9 server:
 it says JWT auth is off by default, marks `token:` as only needed "if the
 server has JWT auth enabled", and pins 0.8.6 in the docker run line.

 Crawl4AI 0.9.0 made the Docker API server secure-by-default. Auth is on for
 every request except GET /health, and a server started without
 CRAWL4AI_API_TOKEN binds 127.0.0.1 only. Following the current example against
 a current image therefore yields either HTTP 401 on every fetch, or a server a
 containerised DeerFlow cannot reach -- with no hint that auth is the cause.

 0.8.6 is also worth moving off: 0.8.7 fixed two pre-auth RCEs (CVSS 9.8), and
 0.8.8/0.8.9 closed SSRF gaps in the same server.

 No code change is needed -- Crawl4AiClient already sends
 `Authorization: Bearer <token>` whenever `token` is set, so this is purely
 the example catching up with the upstream server. Comment-only, so
 config_version is unchanged.

 Co-authored-by: Claude Opus 5 <noreply@anthropic.com>')

 Show description for 2855304

 ![ajayr](https://avatars.githubusercontent.com/u/809529?v=4&size=32)![claude](https://avatars.githubusercontent.com/u/81847?v=4&size=32)

 [ajayr](https://github.com/bytedance/deer-flow/commits?author=ajayr)

 and

 [claude](https://github.com/bytedance/deer-flow/commits?author=claude)

 authoredJul 27, 2026

 ·

 7 / 8

 Verified

 [2855304](https://github.com/bytedance/deer-flow/commit/28553040feffd645b8a99393f5fa0f54f73f01cb)View commit details

 Copy full SHA for 2855304

 Browse repository at this point

### Commits on Jul 16, 2026

- #### [fix(memory): treat explicit null backend\_config values as omitted in DeerMemConfig (](https://github.com/bytedance/deer-flow/commit/5c80c07dfee3a8a0ca67878ed23a27d0d5030fc1 'fix(memory): treat explicit null backend_config values as omitted in DeerMemConfig (#4217)

 config.example.yaml ships backend_config.model: as a bare key whose children
 are all comments, which YAML parses to None (make config-upgrade then writes
 an explicit model: null). DeerMemConfig.model is a non-Optional field with a
 default, so from_backend_config(**{"model": None}) raised a ValidationError
 and every run failed with "Input should be a valid dictionary or instance of
 DeerMemModelConfig". Drop None entries in from_backend_config so YAML null /
 empty keys fall back to field defaults, matching the documented "empty =
 host default LLM" semantics. Upstream bug (#4122 schema); regression-pinned
 in test_deermem_self_contained.py.

 Co-authored-by: Claude Fable 5 <noreply@anthropic.com>') [#4217](https://github.com/bytedance/deer-flow/pull/4217) [)](https://github.com/bytedance/deer-flow/commit/5c80c07dfee3a8a0ca67878ed23a27d0d5030fc1 'fix(memory): treat explicit null backend_config values as omitted in DeerMemConfig (#4217)

 config.example.yaml ships backend_config.model: as a bare key whose children
 are all comments, which YAML parses to None (make config-upgrade then writes
 an explicit model: null). DeerMemConfig.model is a non-Optional field with a
 default, so from_backend_config(**{"model": None}) raised a ValidationError
 and every run failed with "Input should be a valid dictionary or instance of
 DeerMemModelConfig". Drop None entries in from_backend_config so YAML null /
 empty keys fall back to field defaults, matching the documented "empty =
 host default LLM" semantics. Upstream bug (#4122 schema); regression-pinned
 in test_deermem_self_contained.py.

 Co-authored-by: Claude Fable 5 <noreply@anthropic.com>')

 Show description for 5c80c07

 ![ajayr](https://avatars.githubusercontent.com/u/809529?v=4&size=32)![claude](https://avatars.githubusercontent.com/u/81847?v=4&size=32)

 [ajayr](https://github.com/bytedance/deer-flow/commits?author=ajayr)

 and

 [claude](https://github.com/bytedance/deer-flow/commits?author=claude)

 authoredJul 16, 2026

 ·

 10 / 10

 Verified

 [5c80c07](https://github.com/bytedance/deer-flow/commit/5c80c07dfee3a8a0ca67878ed23a27d0d5030fc1)View commit details

 Copy full SHA for 5c80c07

 Browse repository at this point

### Commits on Jul 2, 2026

- #### [feat(community): add Crawl4AI web\_fetch provider (](https://github.com/bytedance/deer-flow/commit/1f74082987e983ea7b9e60853291abacf9af1568 'feat(community): add Crawl4AI web_fetch provider (#3821)

 * feat(community): add Crawl4AI web_fetch provider

 Crawl4AI is a self-hosted, no-API-key web fetcher: it runs headless
 Chromium and returns server-cleaned "fit" markdown directly via its
 POST /md endpoint, so no client-side readability extraction is needed.
 It sits alongside the existing self-hosted Browserless provider.

 - deerflow.community.crawl4ai: async Crawl4AiClient + web_fetch_tool
 (reads base_url/timeout_s/token/filter from config; "Error:" string
 convention; 4096-char cap), mirroring the browserless provider
 - tests: 17 unit cases (success, HTTP error, success:false, empty,
 timeout, request error, token header, truncation, config reads)
 - config.example.yaml: commented web_fetch example
 - doctor: register as a no-key (free) web_fetch provider
 - setup wizard: add to WEB_FETCH_PROVIDERS (no API key)
 - docs: README, CONTRIBUTING, CONFIGURATION, AGENTS provider lists

 Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>

 * fix(community): address Crawl4AI provider review feedback

 - timeout: robust _coerce_timeout (bool / non-numeric -> default) mirroring
 jina, so 'timeout: off' no longer becomes 0.0 and times out every request
 - read web_fetch config once per invocation and pass values into the client,
 so a concurrent hot-reload can't split base_url from filter
 - rename config key timeout_s -> timeout to match jina/infoquest (the
 default providers); update config.example.yaml + setup wizard
 - validate + normalize the markdown filter against {fit,raw,bm25,llm};
 unknown values fall back to fit with a warning instead of an opaque HTTP 400
 - client: a non-JSON 200 body (reverse proxy / auth wall) now reports the
 content-type + snippet instead of a generic JSONDecodeError
 - tests: 22 cases (added non-JSON-200, _coerce_timeout, _coerce_filter,
 invalid-filter fallback, read-config-once)

 Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>

 ---------

 Co-authored-by: Claude Opus 4.8 (1M context) <noreply@anthropic.com>
 Co-authored-by: DanielWalnut <45447813+hetaoBackend@users.noreply.github.com>
 Co-authored-by: Willem Jiang <willem.jiang@gmail.com>') [#3821](https://github.com/bytedance/deer-flow/pull/3821) [)](https://github.com/bytedance/deer-flow/commit/1f74082987e983ea7b9e60853291abacf9af1568 'feat(community): add Crawl4AI web_fetch provider (#3821)

 * feat(community): add Crawl4AI web_fetch provider

 Crawl4AI is a self-hosted, no-API-key web fetcher: it runs headless
 Chromium and returns server-cleaned "fit" markdown directly via its
 POST /md endpoint, so no client-side readability extraction is needed.
 It sits alongside the existing self-hosted Browserless provider.

 - deerflow.community.crawl4ai: async Crawl4AiClient + web_fetch_tool
 (reads base_url/timeout_s/token/filter from config; "Error:" string
 convention; 4096-char cap), mirroring the browserless provider
 - tests: 17 unit cases (success, HTTP error, success:false, empty,
 timeout, request error, token header, truncation, config reads)
 - config.example.yaml: commented web_fetch example
 - doctor: register as a no-key (free) web_fetch provider
 - setup wizard: add to WEB_FETCH_PROVIDERS (no API key)
 - docs: README, CONTRIBUTING, CONFIGURATION, AGENTS provider lists

 Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>

 * fix(community): address Crawl4AI provider review feedback

 - timeout: robust _coerce_timeout (bool / non-numeric -> default) mirroring
 jina, so 'timeout: off' no longer becomes 0.0 and times out every request
 - read web_fetch config once per invocation and pass values into the client,
 so a concurrent hot-reload can't split base_url from filter
 - rename config key timeout_s -> timeout to match jina/infoquest (the
 default providers); update config.example.yaml + setup wizard
 - validate + normalize the markdown filter against {fit,raw,bm25,llm};
 unknown values fall back to fit with a warning instead of an opaque HTTP 400
 - client: a non-JSON 200 body (reverse proxy / auth wall) now reports the
 content-type + snippet instead of a generic JSONDecodeError
 - tests: 22 cases (added non-JSON-200, _coerce_timeout, _coerce_filter,
 invalid-filter fallback, read-config-once)

 Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>

 ---------

 Co-authored-by: Claude Opus 4.8 (1M context) <noreply@anthropic.com>
 Co-authored-by: DanielWalnut <45447813+hetaoBackend@users.noreply.github.com>
 Co-authored-by: Willem Jiang <willem.jiang@gmail.com>')

 Show description for 1f74082

 ![ajayr](https://avatars.githubusercontent.com/u/809529?v=4&size=32)![claude](https://avatars.githubusercontent.com/u/81847?v=4&size=32)![hetaoBackend](https://avatars.githubusercontent.com/u/45447813?v=4&size=32)![WillemJiang](https://avatars.githubusercontent.com/u/219644?v=4&size=32)

 4 peopleauthoredJul 2, 2026

 ·

 9 / 9

 Verified

 [1f74082](https://github.com/bytedance/deer-flow/commit/1f74082987e983ea7b9e60853291abacf9af1568)View commit details

 Copy full SHA for 1f74082

 Browse repository at this point

- #### [fix(auth): persist csrf\_token cookie for the access\_token lifetime (](https://github.com/bytedance/deer-flow/commit/70d53da787fb323ae61348bb97b3eccb65d1c3ee 'fix(auth): persist csrf_token cookie for the access_token lifetime (#3872)

 The csrf_token double-submit cookie is set without max_age (a session
 cookie), while the access_token cookie is persistent over HTTPS
 (max_age = token_expiry_days, see _set_session_cookie). The two cookies
 represent one session but had different lifetimes.

 iOS Safari home-screen PWAs evict session cookies when iOS terminates the
 standalone web app, but keep persistent ones. On reopen the user still
 appears logged in (the persistent access_token survives and GET
 /api/v1/auth/me is CSRF-exempt), but the session-only csrf_token is gone,
 so the frontend's readCsrfCookie() returns null and sends no X-CSRF-Token
 header. The first state-changing request then fails with 403 "CSRF token
 missing. Include X-CSRF-Token header." Only re-login restored it. This
 only manifests over HTTPS, which is why plain-HTTP local dev never sees it.

 Give csrf_token the same max_age as access_token at both mint sites --
 CSRFMiddleware (auth POSTs) and _set_csrf_cookie (OIDC GET callback) --
 mirroring _set_session_cookie's `... if is_https else None` guard so the
 double-submit pair always shares a lifetime: persistent together over
 HTTPS, session-only together over plain HTTP.

 Regression tests in tests/test_auth_type_system.py:
 - test_csrf_cookie_persistent_on_https
 - test_csrf_cookie_session_only_on_http
 - test_oidc_callback_csrf_cookie_persistent_on_https

 Co-authored-by: Claude Opus 4.8 (1M context) <noreply@anthropic.com>') [#3872](https://github.com/bytedance/deer-flow/pull/3872) [)](https://github.com/bytedance/deer-flow/commit/70d53da787fb323ae61348bb97b3eccb65d1c3ee 'fix(auth): persist csrf_token cookie for the access_token lifetime (#3872)

 The csrf_token double-submit cookie is set without max_age (a session
 cookie), while the access_token cookie is persistent over HTTPS
 (max_age = token_expiry_days, see _set_session_cookie). The two cookies
 represent one session but had different lifetimes.

 iOS Safari home-screen PWAs evict session cookies when iOS terminates the
 standalone web app, but keep persistent ones. On reopen the user still
 appears logged in (the persistent access_token survives and GET
 /api/v1/auth/me is CSRF-exempt), but the session-only csrf_token is gone,
 so the frontend's readCsrfCookie() returns null and sends no X-CSRF-Token
 header. The first state-changing request then fails with 403 "CSRF token
 missing. Include X-CSRF-Token header." Only re-login restored it. This
 only manifests over HTTPS, which is why plain-HTTP local dev never sees it.

 Give csrf_token the same max_age as access_token at both mint sites --
 CSRFMiddleware (auth POSTs) and _set_csrf_cookie (OIDC GET callback) --
 mirroring _set_session_cookie's `... if is_https else None` guard so the
 double-submit pair always shares a lifetime: persistent together over
 HTTPS, session-only together over plain HTTP.

 Regression tests in tests/test_auth_type_system.py:
 - test_csrf_cookie_persistent_on_https
 - test_csrf_cookie_session_only_on_http
 - test_oidc_callback_csrf_cookie_persistent_on_https

 Co-authored-by: Claude Opus 4.8 (1M context) <noreply@anthropic.com>')

 Show description for 70d53da

 ![ajayr](https://avatars.githubusercontent.com/u/809529?v=4&size=32)![claude](https://avatars.githubusercontent.com/u/81847?v=4&size=32)

 [ajayr](https://github.com/bytedance/deer-flow/commits?author=ajayr)

 and

 [claude](https://github.com/bytedance/deer-flow/commits?author=claude)

 authoredJul 2, 2026

 ·

 9 / 9

 Verified

 [70d53da](https://github.com/bytedance/deer-flow/commit/70d53da787fb323ae61348bb97b3eccb65d1c3ee)View commit details

 Copy full SHA for 70d53da

 Browse repository at this point

### Commits on Jun 26, 2026

- #### [fix(nginx): preserve upstream X-Forwarded-Proto when behind another TLS proxy (](https://github.com/bytedance/deer-flow/commit/71c5c4a072af0be1301fd6c3c017603cbebd6f7e 'fix(nginx): preserve upstream X-Forwarded-Proto when behind another TLS proxy (#3793)

 When DeerFlow's nginx runs behind another TLS-terminating reverse proxy
 (Pangolin/Traefik, Cloudflare, Caddy), every location block overwrote the
 already-correct X-Forwarded-Proto with $scheme (= http on the private hop).
 The Gateway then treated HTTPS browser traffic as HTTP: the auth-origin check
 rejected the login POST with 403 "Cross-site auth request denied", and session
 cookies lost the Secure flag and max-age.

 Preserve an upstream X-Forwarded-Proto via a map that falls back to $scheme when
 nginx is itself the TLS edge, so standalone `make dev` / Docker is unchanged.

 Co-authored-by: Claude Opus 4.8 (1M context) <noreply@anthropic.com>') [#3793](https://github.com/bytedance/deer-flow/pull/3793) [)](https://github.com/bytedance/deer-flow/commit/71c5c4a072af0be1301fd6c3c017603cbebd6f7e 'fix(nginx): preserve upstream X-Forwarded-Proto when behind another TLS proxy (#3793)

 When DeerFlow's nginx runs behind another TLS-terminating reverse proxy
 (Pangolin/Traefik, Cloudflare, Caddy), every location block overwrote the
 already-correct X-Forwarded-Proto with $scheme (= http on the private hop).
 The Gateway then treated HTTPS browser traffic as HTTP: the auth-origin check
 rejected the login POST with 403 "Cross-site auth request denied", and session
 cookies lost the Secure flag and max-age.

 Preserve an upstream X-Forwarded-Proto via a map that falls back to $scheme when
 nginx is itself the TLS edge, so standalone `make dev` / Docker is unchanged.

 Co-authored-by: Claude Opus 4.8 (1M context) <noreply@anthropic.com>')

 Show description for 71c5c4a

 ![ajayr](https://avatars.githubusercontent.com/u/809529?v=4&size=32)![claude](https://avatars.githubusercontent.com/u/81847?v=4&size=32)

 [ajayr](https://github.com/bytedance/deer-flow/commits?author=ajayr)

 and

 [claude](https://github.com/bytedance/deer-flow/commits?author=claude)

 authoredJun 26, 2026

 ·

 6 / 6

 Verified

 [71c5c4a](https://github.com/bytedance/deer-flow/commit/71c5c4a072af0be1301fd6c3c017603cbebd6f7e)View commit details

 Copy full SHA for 71c5c4a

 Browse repository at this point