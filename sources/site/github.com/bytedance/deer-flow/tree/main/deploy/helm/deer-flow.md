# Source: https://github.com/bytedance/deer-flow/tree/main/deploy/helm/deer-flow

### Uh oh!

There was an error while loading. [Please reload this page]().

[bytedance](https://github.com/bytedance) / **[deer-flow](https://github.com/bytedance/deer-flow)** Public

- [Notifications](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow) You must be signed in to change notification settings
- [Fork 10.9k](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow)
- [Star 79.8k](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow)

 ## FilesExpand file tree

main

/

# deer-flow

/

Copy path

## Directory actions

## More options

More options

## Directory actions

## More options

More options

## Latest commit

![ajayr](https://avatars.githubusercontent.com/u/809529?v=4&size=40)![claude](https://avatars.githubusercontent.com/u/81847?v=4&size=40)

[ajayr](https://github.com/bytedance/deer-flow/commits?author=ajayr)

and

[claude](https://github.com/bytedance/deer-flow/commits?author=claude)

[feat(channels): add Buzz (Nostr) channel connector (](https://github.com/bytedance/deer-flow/commit/d732b90dc3737091dedf842e42eac02ba5230c40) [#4649](https://github.com/bytedance/deer-flow/pull/4649) [)](https://github.com/bytedance/deer-flow/commit/d732b90dc3737091dedf842e42eac02ba5230c40)

Open commit detailssuccess

Aug 5, 2026

[d732b90](https://github.com/bytedance/deer-flow/commit/d732b90dc3737091dedf842e42eac02ba5230c40) · Aug 5, 2026

## History

[History](https://github.com/bytedance/deer-flow/commits/main/deploy/helm/deer-flow)

Open commit details

History

## FilesExpand file tree

main

/

# deer-flow

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

[..](https://github.com/bytedance/deer-flow/tree/main/deploy/helm) |
| 

[templates](https://github.com/bytedance/deer-flow/tree/main/deploy/helm/deer-flow/templates 'templates')

 | 

[templates](https://github.com/bytedance/deer-flow/tree/main/deploy/helm/deer-flow/templates 'templates')

 | 

[fix(sandbox): enforce disabled skills in filesystem views (](https://github.com/bytedance/deer-flow/commit/f2e832330e6717c3fa660253b0ba0990cc6b7344 'fix(sandbox): enforce disabled skills in filesystem views (#4178)

* fix(sandbox): project enabled skills into sandbox views

* fix(skills): keep projection mutations consistent

* fix(skills): fail closed on projection errors

* fix(skills): isolate per-scope failures during boot projection rebuild

rebuild_all_skill_projections() propagated any exception from the public
rebuild or from a single user's rebuild straight out of the gateway
lifespan startup, uncaught. A single broken user directory (bad
permissions, corrupted _skill_states.json, unreadable content) would
therefore abort gateway boot for every user, not just that one -
_rebuild_*_locked already fails closed internally (clears the view and
re-raises), so the boot loop only needed to stop treating that re-raise
as fatal.

Each scope's rebuild now fails closed independently and boot continues;
a scope left empty by a boot failure self-heals on the next sandbox
acquire via ensure_skill_projections().

Also patches deerflow.skills.projection.rebuild_all_skill_projections in
the memory-flush lifespan test fixture, matching the two sibling
fixtures in the same file — this call is now on the lifespan startup
path and the fixture's minimal SimpleNamespace config predates it.

* test(skills): update authz test for the projection-aware public toggle

_persist_shared_skill_state (introduced earlier in this branch) reads
the shared extensions_config.json fresh from disk under the projection
lock instead of through the cached get_extensions_config() singleton -
that's the whole point of the fix (stale worker caches must not clobber
another worker's concurrent update). The name no longer exists on the
skills router module, so the test's monkeypatch of it started raising
AttributeError instead of exercising the endpoint.

The mock storage in this test isn't a real LocalSkillStorage instance,
so _persist_shared_skill_state's projection-mutation branch is already
skipped (nullcontext) and it falls back to a fresh ExtensionsConfig()
for the nonexistent tmp config_path - no replacement monkeypatch needed.

* fix(sandbox): make skill projection ensure best-effort in acquire

acquire() called _ensure_skills_projection() directly, outside any
try/except, in both LocalSandboxProvider and AioSandboxProvider. Every
other skill-mount setup path in these providers has always caught
exceptions and logged a warning rather than failing sandbox acquire
outright (e.g. when config.yaml can't be resolved) - these two new call
sites broke that contract, so any projection failure (including simply
not having a config.yaml, as in CI's test environment) now failed
acquire() itself instead of just leaving skill mounts off.

_ensure_skills_projection now catches its own exceptions and returns
None; both providers' callers already tolerate that (a None projection
skips the skill-specific mounts, matching the existing degrade path)
after making _append_public_skill_mapping and the custom/legacy mount
block in LocalSandboxProvider explicitly None-safe.

Caught by running the full suite with config.yaml removed, matching
CI's environment - not caught locally because a real config.yaml was
present, masking the failure.

* fix(sandbox): make E2B skill projection mounts best-effort

_skill_projection_mounts called ensure_skill_projections with no guard,
unlike Local/AIO's _ensure_skills_projection. A raise propagated out of
_apply_mounts before the configured-mounts loop ran, so a skills
projection failure dropped the operator's own configured mounts too -
only caught by create()'s outer warning, with nothing applied at all.

Swallow here and return an empty mount list on failure, matching the
Local/AIO pattern: still fail-closed for skills, but no longer widens
the blast radius to unrelated configured mounts.

Review feedback from PR #4178.

* docs(skills): document projection trade-offs flagged in review

- _update_tree_digest: note the metadata-only (not content) hashing
 trade-off and why runtime writes through this codebase are still
 covered regardless (rebuild-under-lock + rename always changes inode).
- LocalSandboxProvider.acquire: note the acquire-time self-heal cost
 (cheap on a fresh manifest, ~400ms rebuild under lock on stale/drift).
- skill_projection_mutation: drop the no-op except-Exception-then-raise;
 a raise from the mutation already propagates past the yield with the
 view left cleared, no explicit re-raise needed.
- provisioner README: spell out that hostPath skills volumes require
 the gateway and K8s node to share DEER_FLOW_HOST_BASE_DIR (single-node
 or shared storage), and that the custom/legacy volumes' hostPath type
 Directory (not DirectoryOrCreate) makes a violation of that assumption
 a visible Pod-creation failure instead of a silent empty mount.

Review feedback from PR #4178.

* fix(skills): lazily repair user projections

* fix(skills): close projection review gaps

* fix(skills): refresh user projection enable state

* fix(skills): close projection review follow-ups

* fix(skills): preserve state across projection writes

---------

Co-authored-by: Willem Jiang <willem.jiang@gmail.com>') [#4178](https://github.com/bytedance/deer-flow/pull/4178) [)](https://github.com/bytedance/deer-flow/commit/f2e832330e6717c3fa660253b0ba0990cc6b7344 'fix(sandbox): enforce disabled skills in filesystem views (#4178)

* fix(sandbox): project enabled skills into sandbox views

* fix(skills): keep projection mutations consistent

* fix(skills): fail closed on projection errors

* fix(skills): isolate per-scope failures during boot projection rebuild

rebuild_all_skill_projections() propagated any exception from the public
rebuild or from a single user's rebuild straight out of the gateway
lifespan startup, uncaught. A single broken user directory (bad
permissions, corrupted _skill_states.json, unreadable content) would
therefore abort gateway boot for every user, not just that one -
_rebuild_*_locked already fails closed internally (clears the view and
re-raises), so the boot loop only needed to stop treating that re-raise
as fatal.

Each scope's rebuild now fails closed independently and boot continues;
a scope left empty by a boot failure self-heals on the next sandbox
acquire via ensure_skill_projections().

Also patches deerflow.skills.projection.rebuild_all_skill_projections in
the memory-flush lifespan test fixture, matching the two sibling
fixtures in the same file — this call is now on the lifespan startup
path and the fixture's minimal SimpleNamespace config predates it.

* test(skills): update authz test for the projection-aware public toggle

_persist_shared_skill_state (introduced earlier in this branch) reads
the shared extensions_config.json fresh from disk under the projection
lock instead of through the cached get_extensions_config() singleton -
that's the whole point of the fix (stale worker caches must not clobber
another worker's concurrent update). The name no longer exists on the
skills router module, so the test's monkeypatch of it started raising
AttributeError instead of exercising the endpoint.

The mock storage in this test isn't a real LocalSkillStorage instance,
so _persist_shared_skill_state's projection-mutation branch is already
skipped (nullcontext) and it falls back to a fresh ExtensionsConfig()
for the nonexistent tmp config_path - no replacement monkeypatch needed.

* fix(sandbox): make skill projection ensure best-effort in acquire

acquire() called _ensure_skills_projection() directly, outside any
try/except, in both LocalSandboxProvider and AioSandboxProvider. Every
other skill-mount setup path in these providers has always caught
exceptions and logged a warning rather than failing sandbox acquire
outright (e.g. when config.yaml can't be resolved) - these two new call
sites broke that contract, so any projection failure (including simply
not having a config.yaml, as in CI's test environment) now failed
acquire() itself instead of just leaving skill mounts off.

_ensure_skills_projection now catches its own exceptions and returns
None; both providers' callers already tolerate that (a None projection
skips the skill-specific mounts, matching the existing degrade path)
after making _append_public_skill_mapping and the custom/legacy mount
block in LocalSandboxProvider explicitly None-safe.

Caught by running the full suite with config.yaml removed, matching
CI's environment - not caught locally because a real config.yaml was
present, masking the failure.

* fix(sandbox): make E2B skill projection mounts best-effort

_skill_projection_mounts called ensure_skill_projections with no guard,
unlike Local/AIO's _ensure_skills_projection. A raise propagated out of
_apply_mounts before the configured-mounts loop ran, so a skills
projection failure dropped the operator's own configured mounts too -
only caught by create()'s outer warning, with nothing applied at all.

Swallow here and return an empty mount list on failure, matching the
Local/AIO pattern: still fail-closed for skills, but no longer widens
the blast radius to unrelated configured mounts.

Review feedback from PR #4178.

* docs(skills): document projection trade-offs flagged in review

- _update_tree_digest: note the metadata-only (not content) hashing
 trade-off and why runtime writes through this codebase are still
 covered regardless (rebuild-under-lock + rename always changes inode).
- LocalSandboxProvider.acquire: note the acquire-time self-heal cost
 (cheap on a fresh manifest, ~400ms rebuild under lock on stale/drift).
- skill_projection_mutation: drop the no-op except-Exception-then-raise;
 a raise from the mutation already propagates past the yield with the
 view left cleared, no explicit re-raise needed.
- provisioner README: spell out that hostPath skills volumes require
 the gateway and K8s node to share DEER_FLOW_HOST_BASE_DIR (single-node
 or shared storage), and that the custom/legacy volumes' hostPath type
 Directory (not DirectoryOrCreate) makes a violation of that assumption
 a visible Pod-creation failure instead of a silent empty mount.

Review feedback from PR #4178.

* fix(skills): lazily repair user projections

* fix(skills): close projection review gaps

* fix(skills): refresh user projection enable state

* fix(skills): close projection review follow-ups

* fix(skills): preserve state across projection writes

---------

Co-authored-by: Willem Jiang <willem.jiang@gmail.com>')

 | 

Jul 31, 2026

 |
| 

[Chart.yaml](https://github.com/bytedance/deer-flow/blob/main/deploy/helm/deer-flow/Chart.yaml 'Chart.yaml')

 | 

[Chart.yaml](https://github.com/bytedance/deer-flow/blob/main/deploy/helm/deer-flow/Chart.yaml 'Chart.yaml')

 | 

[feat(deploy): first-class Helm chart for Kubernetes deployment (](https://github.com/bytedance/deer-flow/commit/bc9ee9645cc1aa79ca2d230a671b167614085a73 'feat(deploy): first-class Helm chart for Kubernetes deployment (#3987)

* feat(helm): add production-ready Helm chart for Kubernetes deployment

Adds deploy/helm/deer-flow, a native-Kubernetes translation of the
production docker-compose stack, plus CI to publish its images and chart.

* ci(release): gate releases on version-source consistency

Add a reusable verify-versions workflow invoked by both chart.yaml and
container.yaml on v* tags. It runs scripts/verify_versions.sh against the
tag and fails the release — skipping all image and chart publishing — when
Chart.yaml (version + appVersion), backend/pyproject.toml, or
frontend/package.json don't all match the tag.

Add scripts/verify_versions.sh (the check, also runnable locally) and
scripts/bump_version.sh (bumps all four sources in lockstep, then
self-verifies). Document the release flow in RELEASING.md and link it from
AGENTS.md.

* fix(deploy): address Helm chart review feedback (#3987)

Three review items from willem-bd:

1. nginx IPv6 listen strip never matched. The sed pattern required a `;`
 immediately after `2026`, but the rendered config emits
 `listen [::]:2026 default_server;` (space + `default_server` before the
 `;`), so the line was never deleted and nginx crash-looped on pods
 without IPv6 (`socket() :::2026 failed (97: Address family not
 supported)`). Drop the trailing `;` from the pattern so it matches.
 Same latent bug fixed in docker-compose-dev.yaml.

2. Passwords were spliced into DSNs verbatim, so a password containing
 URL-special chars (@ : / # ? % [ ] space) produced a malformed DSN and
 a confusing parse error. Add a `deer-flow.urlEscape` helper
 (replace-based: Sprig lacks urlqueryescape, and regexReplaceAllLiteral
 treats the replacement as a regex template so `[`/`]`/`?` break it) and
 apply it to the password in the postgres and redis DSNs. The raw
 `postgres-password` / `redis-password` keys stay unencoded - they back
 POSTGRES_PASSWORD / REDIS_PASSWORD, not a URL segment.

3. NODE_HOST defaulted to "gateway", which can never route: the gateway
 Service is ClusterIP:8001 and knows nothing of a sandbox NodePort, so a
 user who skips the caveat gets unreachable sandboxes with no error at
 install time. Default NODE_HOST to the provisioner pod's node IP via
 the downward API (status.hostIP) - a NodePort is exposed on every node,
 so <node-IP>:<NodePort> routes from the gateway on most clusters.
 `provisioner.nodeHost` remains an override for CNIs/policies that block
 pod->node-IP traffic. Updated NOTES.txt, values.yaml, and the chart
 README. (#3929 remains the long-term fix - ClusterIP + cluster-DNS URL
 removes NODE_HOST and the NodePort exposure entirely.)

Validated with helm lint, helm template (incl. a special-char password
rendering the encoded DSNs), and a sed pattern-match check.

* fix(deploy): address round-2 Helm chart review feedback (#3987)

Three "Medium" items from willem-bd:

1. No helm lint / helm template gate before publish. A template regression
 ships as an immutable OCI artifact (GHCR won't overwrite --version), so
 gate packaging on `helm lint` + `helm template --include-crds` in
 chart.yaml before `helm package`. (ct lint / helm-unittest deferred.)

2. Action pinning inconsistent + PR body overstates it. SHA-pin
 actions/checkout (v6.0.3, df4cb1c0) and actions/attest-build-provenance
 (v2.4.0, e8998f94) across the publishing workflows (chart.yaml,
 container.yaml, verify-versions.yml), matching the existing docker/*
 SHA-pin pattern. Resolves the checkout @v4/@v6 mismatch and makes the
 "SHA-pinned actions" claim accurate. Other pre-existing workflows left
 untouched (out of scope for this PR).

3. Provisioner RBAC broader than needed. Dropped the unused update/patch
 verbs and the pods/exec + events rules from the provisioner Role -
 audited against docker/provisioner/app.py, which only calls
 get/create/delete on pods and get/list/create/delete on services. Fixed
 NOTES.txt to accurately describe the grant instead of understating it as
 "create Pods and Services". The remaining scope concern - verbs apply to
 all Pods in the namespace, not just sandbox Pods - is still deferred
 (RBAC can't scope by label; needs a dedicated namespace or admission
 control), now noted in NOTES.txt and README.

Validated with helm lint + helm template (narrowed Role renders with
exactly get/list/watch/create/delete).

* feat(helm): enable sandbox+web tools out of the box

The chart's default config loaded zero agent tools (config.tools empty ->
"Total tools loaded: 0"), so a fresh install gave an agent that could do
nothing useful. Add tool_groups + tools to the default config block:

- web: web_search (ddg), web_fetch (jina), image_search - no API key
- file:read: ls, read_file, glob, grep
- file:write: write_file, str_replace
- bash

The file/bash tools run inside the AIO sandbox the chart already
configures; the web tools need outbound internet from the gateway pod
(swap backends or drop entries for air-gapped clusters - see
config.example.yaml).

Also bump config_version 15 -> 19 to match config.example.yaml (the chart
had drifted behind). NOTES.txt and the README example updated to match.

* ci(helm): add chart validation + config_version drift check on PR

Extend the chart workflow with a PR-triggered validate-chart job that runs
helm lint, helm template --include-crds, and a config_version drift check:
it parses config_version from both config.example.yaml and the chart's
values.yaml and fails the build (with a ::error:: naming the files to bump)
if the chart is behind the example. This catches the kind of drift this
PR is fixing - the chart sat at v15 while the example moved to v19 - before
it can merge again.

verify-versions and publish-chart stay tag-only; publish-chart now
needs: [verify-versions, validate-chart]. validate-chart runs on both
PRs and tag pushes: the tag arm is required because a job that `needs`
a skipped job is itself skipped under the default success() check, so
validate-chart must actually run on tag pushes or publish-chart would
never fire.

* Bump config version to 20') [#3987](https://github.com/bytedance/deer-flow/pull/3987) [)](https://github.com/bytedance/deer-flow/commit/bc9ee9645cc1aa79ca2d230a671b167614085a73 'feat(deploy): first-class Helm chart for Kubernetes deployment (#3987)

* feat(helm): add production-ready Helm chart for Kubernetes deployment

Adds deploy/helm/deer-flow, a native-Kubernetes translation of the
production docker-compose stack, plus CI to publish its images and chart.

* ci(release): gate releases on version-source consistency

Add a reusable verify-versions workflow invoked by both chart.yaml and
container.yaml on v* tags. It runs scripts/verify_versions.sh against the
tag and fails the release — skipping all image and chart publishing — when
Chart.yaml (version + appVersion), backend/pyproject.toml, or
frontend/package.json don't all match the tag.

Add scripts/verify_versions.sh (the check, also runnable locally) and
scripts/bump_version.sh (bumps all four sources in lockstep, then
self-verifies). Document the release flow in RELEASING.md and link it from
AGENTS.md.

* fix(deploy): address Helm chart review feedback (#3987)

Three review items from willem-bd:

1. nginx IPv6 listen strip never matched. The sed pattern required a `;`
 immediately after `2026`, but the rendered config emits
 `listen [::]:2026 default_server;` (space + `default_server` before the
 `;`), so the line was never deleted and nginx crash-looped on pods
 without IPv6 (`socket() :::2026 failed (97: Address family not
 supported)`). Drop the trailing `;` from the pattern so it matches.
 Same latent bug fixed in docker-compose-dev.yaml.

2. Passwords were spliced into DSNs verbatim, so a password containing
 URL-special chars (@ : / # ? % [ ] space) produced a malformed DSN and
 a confusing parse error. Add a `deer-flow.urlEscape` helper
 (replace-based: Sprig lacks urlqueryescape, and regexReplaceAllLiteral
 treats the replacement as a regex template so `[`/`]`/`?` break it) and
 apply it to the password in the postgres and redis DSNs. The raw
 `postgres-password` / `redis-password` keys stay unencoded - they back
 POSTGRES_PASSWORD / REDIS_PASSWORD, not a URL segment.

3. NODE_HOST defaulted to "gateway", which can never route: the gateway
 Service is ClusterIP:8001 and knows nothing of a sandbox NodePort, so a
 user who skips the caveat gets unreachable sandboxes with no error at
 install time. Default NODE_HOST to the provisioner pod's node IP via
 the downward API (status.hostIP) - a NodePort is exposed on every node,
 so <node-IP>:<NodePort> routes from the gateway on most clusters.
 `provisioner.nodeHost` remains an override for CNIs/policies that block
 pod->node-IP traffic. Updated NOTES.txt, values.yaml, and the chart
 README. (#3929 remains the long-term fix - ClusterIP + cluster-DNS URL
 removes NODE_HOST and the NodePort exposure entirely.)

Validated with helm lint, helm template (incl. a special-char password
rendering the encoded DSNs), and a sed pattern-match check.

* fix(deploy): address round-2 Helm chart review feedback (#3987)

Three "Medium" items from willem-bd:

1. No helm lint / helm template gate before publish. A template regression
 ships as an immutable OCI artifact (GHCR won't overwrite --version), so
 gate packaging on `helm lint` + `helm template --include-crds` in
 chart.yaml before `helm package`. (ct lint / helm-unittest deferred.)

2. Action pinning inconsistent + PR body overstates it. SHA-pin
 actions/checkout (v6.0.3, df4cb1c0) and actions/attest-build-provenance
 (v2.4.0, e8998f94) across the publishing workflows (chart.yaml,
 container.yaml, verify-versions.yml), matching the existing docker/*
 SHA-pin pattern. Resolves the checkout @v4/@v6 mismatch and makes the
 "SHA-pinned actions" claim accurate. Other pre-existing workflows left
 untouched (out of scope for this PR).

3. Provisioner RBAC broader than needed. Dropped the unused update/patch
 verbs and the pods/exec + events rules from the provisioner Role -
 audited against docker/provisioner/app.py, which only calls
 get/create/delete on pods and get/list/create/delete on services. Fixed
 NOTES.txt to accurately describe the grant instead of understating it as
 "create Pods and Services". The remaining scope concern - verbs apply to
 all Pods in the namespace, not just sandbox Pods - is still deferred
 (RBAC can't scope by label; needs a dedicated namespace or admission
 control), now noted in NOTES.txt and README.

Validated with helm lint + helm template (narrowed Role renders with
exactly get/list/watch/create/delete).

* feat(helm): enable sandbox+web tools out of the box

The chart's default config loaded zero agent tools (config.tools empty ->
"Total tools loaded: 0"), so a fresh install gave an agent that could do
nothing useful. Add tool_groups + tools to the default config block:

- web: web_search (ddg), web_fetch (jina), image_search - no API key
- file:read: ls, read_file, glob, grep
- file:write: write_file, str_replace
- bash

The file/bash tools run inside the AIO sandbox the chart already
configures; the web tools need outbound internet from the gateway pod
(swap backends or drop entries for air-gapped clusters - see
config.example.yaml).

Also bump config_version 15 -> 19 to match config.example.yaml (the chart
had drifted behind). NOTES.txt and the README example updated to match.

* ci(helm): add chart validation + config_version drift check on PR

Extend the chart workflow with a PR-triggered validate-chart job that runs
helm lint, helm template --include-crds, and a config_version drift check:
it parses config_version from both config.example.yaml and the chart's
values.yaml and fails the build (with a ::error:: naming the files to bump)
if the chart is behind the example. This catches the kind of drift this
PR is fixing - the chart sat at v15 while the example moved to v19 - before
it can merge again.

verify-versions and publish-chart stay tag-only; publish-chart now
needs: [verify-versions, validate-chart]. validate-chart runs on both
PRs and tag pushes: the tag arm is required because a job that `needs`
a skipped job is itself skipped under the default success() check, so
validate-chart must actually run on tag pushes or publish-chart would
never fire.

* Bump config version to 20')

 | 

Jul 9, 2026

 |
| 

[README.md](https://github.com/bytedance/deer-flow/blob/main/deploy/helm/deer-flow/README.md 'README.md')

 | 

[README.md](https://github.com/bytedance/deer-flow/blob/main/deploy/helm/deer-flow/README.md 'README.md')

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

[values.yaml](https://github.com/bytedance/deer-flow/blob/main/deploy/helm/deer-flow/values.yaml 'values.yaml')

 | 

[values.yaml](https://github.com/bytedance/deer-flow/blob/main/deploy/helm/deer-flow/values.yaml 'values.yaml')

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

View all files

 |

## [README.md](https://github.com/bytedance/deer-flow/tree/main/deploy/helm/deer-flow#readme)

Outline

# DeerFlow Helm Chart

Deploys the full DeerFlow stack to Kubernetes: **gateway** (backend + embedded LangGraph runtime), **frontend** (Next.js), **nginx** (internal reverse proxy preserving the compose routing), and the **provisioner** (K8s-native sandbox that spawns code-execution Pods on demand).

This chart translates the production `docker/docker-compose.yaml` into native Kubernetes resources. No existing repo files are modified.

## Prerequisites

- A Kubernetes cluster (Docker Desktop K8s, OrbStack, kind, k3d, or a real cluster).
- `kubectl` + `helm` 3.8+ installed (OCI registry support stabilized in 3.8; earlier 3.x needs `HELM_EXPERIMENTAL_OCI=1`).
- The three DeerFlow images — either the published ones (see "Install the published chart" below) or built locally (see step 1).
- An Ingress controller (e.g. ingress-nginx) if you enable `ingress`.

## Install the published chart (GHCR)

The chart and all three images are published to GHCR on every `v*` release tag (see `.github/workflows/container.yaml` and `chart.yaml`). Skip the build step and install directly:

```shell
helm install deer-flow oci://ghcr.io/<owner>/charts/deer-flow \
  --version <version> \
  -n deer-flow --create-namespace \
  -f my-values.yaml
```

where `<owner>` is the GitHub owner the chart is published from and `<version>` matches the release tag without the leading `v` (tag `v0.1.0` → `--version 0.1.0`).

> **Note:** the helm chart is new in 2.1.0 - no chart was published before it. It publishes to `oci://ghcr.io/<owner>/charts/deer-flow` (the `charts/` prefix keeps it distinct from the `deer-flow-{backend,frontend,provisioner}` image packages).

Point the chart at the published images:

```yaml
image:
  registry: ghcr.io/<owner>     # owner prefix; images are <owner>/deer-flow-<name>
  tag: "<version>"              # match the release tag (sans leading `v`)
  pullSecrets:
    - { name: regcred }         # only if the GHCR package is private
```

The chart's `gatewayImage` / `frontendImage` / `provisionerImage` defaults already match the published image names (`deer-flow-backend`, `deer-flow-frontend`, `deer-flow-provisioner`), so only `registry` and `tag` are required. New GHCR packages default to **private** — flip the package to public in its GHCR settings page for unauthenticated pulls, otherwise create a pull secret (step 1) and reference it via `image.pullSecrets`.

> The OCI chart and the images are versioned independently of the chart's `appVersion`; always set `image.tag` to the release that matches your chart `--version` unless you have a reason to pin differently.

## 1\. Build & push images (custom builds only)

Skip this section if you're using the published chart above. To build the images yourself from the existing Dockerfiles:

```shell
REGISTRY=ghcr.io/yourorg
TAG=latest

# backend - build with the `postgres` extra so multi-replica deploys can use
# shared Postgres (matches the published image)
docker build -t $REGISTRY/deer-flow-backend:$TAG --build-arg UV_EXTRAS=postgres -f backend/Dockerfile .
# frontend
docker build -t $REGISTRY/deer-flow-frontend:$TAG -f frontend/Dockerfile .
# provisioner
docker build -t $REGISTRY/deer-flow-provisioner:$TAG -f docker/provisioner/Dockerfile docker/provisioner

docker push $REGISTRY/deer-flow-backend:$TAG
docker push $REGISTRY/deer-flow-frontend:$TAG
docker push $REGISTRY/deer-flow-provisioner:$TAG
```

These names match the chart's `gatewayImage` / `frontendImage` / `provisionerImage` defaults, so only `image.registry` and `image.tag` need to point at them.

If your registry needs auth, create a pull secret:

```shell
kubectl create secret docker-registry regcred \
  --docker-server=ghcr.io \
  --docker-username=youruser \
  --docker-password=yourtoken \
  -n deer-flow
```

## 2\. Configure values

Copy and edit `values.yaml` → `my-values.yaml`. At minimum set:

```yaml
image:
  registry: ghcr.io/yourorg
  tag: latest
  pullSecrets:
    - { name: regcred }

ingress:
  enabled: true
  className: nginx
  host: deer-flow.example.com
  tls:
    enabled: true
    secretName: deer-flow-tls

secrets:
  OPENAI_API_KEY: sk-...
  # add channel tokens, search keys, etc. as needed
```

Provide your model config under `config` (keep secrets as `$VAR` references — they resolve from the `secrets` map):

```yaml
config: |
  config_version: 33
  models:
    - name: gpt-4
      use: langchain_openai:ChatOpenAI
      model: gpt-4
      api_key: $OPENAI_API_KEY
      request_timeout: 600.0
  sandbox:
    use: deerflow.community.aio_sandbox:AioSandboxProvider
    provisioner_url: http://provisioner:8002
  database:
    backend: postgres
    postgres_url: $DATABASE_URL
    pool_recycle: 300
    command_timeout: 30
  checkpointer:
    type: postgres
    connection_string: $DATABASE_URL
  stream_bridge:
    type: redis   # cross-pod SSE; URL from DEER_FLOW_STREAM_BRIDGE_REDIS_URL
  # Tools MUST be listed explicitly - the agent gets none otherwise
  # (BUILTIN_TOOLS only adds present_file + ask_clarification). The chart
  # default in values.yaml enables the sandbox tools + web tools (web_search,
  # web_fetch, image_search - no API key); when you override `config:`, copy
  # them in. Full list in values.yaml / config.example.yaml. The web tools need
  # outbound egress from the gateway pod.
  tool_groups:
    - name: web
    - name: file:read
    - name: file:write
    - name: bash
  tools:
    - name: web_search
      group: web
      use: deerflow.community.ddg_search.tools:web_search_tool
      max_results: 5
    - name: web_fetch
      group: web
      use: deerflow.community.jina_ai.tools:web_fetch_tool
      timeout: 10
    - name: image_search
      group: web
      use: deerflow.community.image_search.tools:image_search_tool
      max_results: 5
    - name: bash
      group: bash
      use: deerflow.sandbox.tools:bash_tool
    # also: ls, read_file, glob, grep, write_file, str_replace (see values.yaml)
```

`$DATABASE_URL` is injected from the postgres Secret (see below). The `checkpointer:` section is required for multi-replica operation — the LangGraph Store (cross-thread memory + thread list) reads it and does not fall back to `database:`. `stream_bridge.type: redis` is the default and routes live SSE events through the bundled redis StatefulSet (or `redis.external`). Because `config:` is a single override blob, a partial `config:` replaces the chart default entirely - keep the `tools:`/`tool_groups:` block (or the agent will have no tools) and the `sandbox:`/`database:`/`checkpointer:`/`stream_bridge:` sections shown above.

## 3\. Install (from a local chart checkout)

For a custom build or local development, install from the chart directory:

```shell
helm install deer-flow deploy/helm/deer-flow \
  -n deer-flow --create-namespace \
  -f my-values.yaml
```

## 4\. Verify

```shell
kubectl -n deer-flow get pods
kubectl -n deer-flow port-forward svc/nginx 2026:2026
curl http://localhost:2026/health          # gateway health via nginx
```

Hit the Ingress host (map it in `/etc/hosts` for local clusters) to load the UI.

Provisioner sanity check:

```shell
kubectl -n deer-flow exec deploy/deer-flow-provisioner -- curl -s localhost:8002/health
```

## Architecture notes

- **PostgreSQL is the default database.** A bundled single-instance postgres StatefulSet (`postgresql.enabled: true`) runs in the namespace and the gateway connects via the in-cluster Service. The DSN is auto-generated into a Secret (key `database-url`) and injected as `DATABASE_URL`; `config.yaml` references it as `$DATABASE_URL` in `database.postgres_url`. Schema is bootstrapped automatically on gateway startup (alembic `create_all` + `stamp head`). For real HA, disable the bundled instance and point at a managed DB:

    ```yaml
    postgresql:
      enabled: false
      external:
        host: mydb.example.com   # or set databaseUrl / existingSecret
        port: 5432
        database: deerflow
        username: deerflow
        password: changeme
    ```

- **Graceful shutdown & memory drain.** The gateway pod sets `terminationGracePeriodSeconds` (default 45s, overridable via `gateway.terminationGracePeriodSeconds`) plus an optional `preStop` sleep (`gateway.preStopSleepSeconds`, default 5s). The grace period MUST exceed the Gateway's graceful-shutdown work — channel stop (~5s) plus the memory-queue drain (`memory.shutdown_flush_timeout_seconds`, default 30s) plus a buffer — because the drain runs on a daemon thread and K8s SIGKILLs anything still running at the end of the grace window. K8s defaults to 30s, which SIGKILLs the drain mid-flight and silently re-introduces the memory loss the drain is fixing. **When you raise `memory.shutdown_flush_timeout_seconds`, raise `gateway.terminationGracePeriodSeconds` to match** (channel stop + drain + buffer).
- **Gateway replicas.** Postgres + the Redis stream bridge together make the gateway's _persisted_ state (checkpointer + run/thread metadata) and _live stream_ path cross-pod-safe. The default is still 1 replica: **do not raise `gateway.replicas` past 1 yet.** Run control — `create_or_reject` dedup, `cancel`, and orphan reconciliation — is still worker-local (in-process `asyncio.Lock` + in-memory `record.task`), tracked by [issue #3948](https://github.com/bytedance/deer-flow/issues/3948). With >1 replica a double-submit can create two runs on one thread (checkpoint corruption), a cancel can land on a non-owner pod (409), and a crashed pod's runs stay `pending`/`running` forever. Stay on 1 replica until that work lands.
- **Redis stream bridge.** A bundled single-instance redis StatefulSet (`redis.enabled: true`, `redis:7-alpine`) runs in the namespace and the gateway connects via the in-cluster Service. Per-run SSE events are stored in Redis Streams (PR #3191) so a client connected to any gateway pod receives live events and reconnect resumes from `Last-Event-ID`. The URL is auto-generated into a Secret (key `redis-url`) and injected as `DEER_FLOW_STREAM_BRIDGE_REDIS_URL`; `config.yaml` sets `stream_bridge.type: redis` by default. No-auth by default (ClusterIP isolation, matching compose); set `redis.auth.password` to enable AUTH. For a managed Redis, disable the bundled instance and point at it via `redis.external`.
- **Persistence.** A PVC (`<release>-home`) backs `/app/backend/.deer-flow` (sqlite DB, memory, custom agents, per-thread user-data). The gateway mounts it with `subPath: deer-flow` so the layout matches the provisioner's PVC user-data mode. Default `ReadWriteOnce`; use `ReadWriteMany` (NFS) on multi-node clusters so sandbox Pods on other nodes can mount it.
- **Provisioner RBAC.** The provisioner gets a ServiceAccount with a namespaced Role (get/list/watch/create/delete on pods + services) and a narrow ClusterRole (namespace get/create). It uses in-cluster service-account creds — no kubeconfig mount. The unused update/patch/pods-exec/events verbs were dropped (audited against `docker/provisioner/app.py`).
- **Skills.** Disabled by default (emptyDir at `/app/skills`). Populate via `skills.existingClaim` or `skills.configMap`, or bake skills into a custom gateway image.

## Security

### Enforced posture

All workloads run as **non-root** with **all Linux capabilities dropped**. No container escalates privileges or runs as uid 0.

| workload | runAsUser | fsGroup | writable-path handling |
| --- | --- | --- | --- |
| gateway | 1000 | 1000 | `.deer-flow` PVC group-writable via fsGroup; `PYTHONDONTWRITEBYTECODE=1` suppresses `.pyc` writes; `UV_CACHE_DIR=/tmp` |
| frontend | 1000 (`node`) | 1000 | `emptyDir` at `/app/frontend/.next/cache` (root-owned in the image) |
| nginx | 101 (`nginx`) | 101 | command writes the rendered config to `/tmp/nginx.conf` and loads `nginx -c /tmp/nginx.conf` (since `/etc/nginx` is root-owned); `emptyDir` at `/var/cache/nginx` |
| provisioner | 1000 | — | no PVC; `PYTHONDONTWRITEBYTECODE=1` |
| postgres | 999 (`postgres`) | 999 | official `postgres:16` entrypoint detects non-root and skips the chown/gosu dance; data PVC group-writable via fsGroup |
| redis | 999 (`redis`) | 999 | official `redis:7-alpine` entrypoint detects non-root and skips the gosu dance; data PVC group-writable via fsGroup |

Every container sets:

- `runAsNonRoot: true`
- `allowPrivilegeEscalation: false`
- `capabilities.drop: ["ALL"]`
- `seccompProfile: { type: RuntimeDefault }`

All listening ports are >1024 (8001 / 3000 / 2026 / 8002 / 5432), so no `NET_BIND_SERVICE` capability is required.

**ConfigMap rollout.** ConfigMaps mount via `subPath`, which does **not** receive in-place updates — a `helm upgrade` that changes only a ConfigMap would leave pods on stale config. Each pod template carries a `checksum/*` annotation (SHA256 of the rendered ConfigMap): `checksum/config` + `checksum/extensions` on the gateway, `checksum/nginx` on nginx. Any content change alters the pod spec and triggers a rolling restart.

**Resource defaults.** Every workload ships with modest requests+limits in `values.yaml`; override per workload (`gateway.resources`, `frontend.resources`, `nginx.resources`, `provisioner.resources`, `postgresql.primary.resources`, `redis.primary.resources`).

### Not yet enforced (deferred hardening)

These are intentionally **not** set in this chart revision. Each can be added per-workload with testing:

- **`readOnlyRootFilesystem: true`** — makes the container's root filesystem immutable so a compromised process can't persist changes to the image. Not enabled because it requires auditing every runtime write path and mounting an `emptyDir` over each. Known paths:
 - gateway / frontend / nginx / provisioner: `/tmp` (uv cache, python tempfiles, the nginx config + pid, node temp) — one `emptyDir` at `/tmp` each.
 - postgres: `/tmp` **and** `/var/run/postgresql` (the Unix-socket dir). The first four are mechanical. **postgres is the hard case** — the official image writes its socket to `/var/run/postgresql` and isn't designed for a read-only root, so it may need socket-path redirection (`PGHOST`/`unix_socket_directories`). Optionally, add `USER` directives to the `backend/Dockerfile`, `frontend/Dockerfile`, and `docker/provisioner/Dockerfile` so the images are non-root by default (defense in depth — the chart already forces the uid via `securityContext`, so this is not required). A cluster enforcing the `restricted` Pod Security Admission standard would require this setting.
- **Provisioner RBAC narrowing.** The Role grants get/list/watch/create/delete on pods and services in the namespace (update/patch/pods-exec/events were dropped as unused). These verbs still apply to _all_ Pods in the namespace, not just sandbox Pods — RBAC can't scope by label, so the remaining options are a dedicated sandbox namespace or admission control (OPA/Kyverno).
- **`startupProbe`.** Workloads have readiness + liveness probes but no startup probe. The gateway's `livenessProbe.initialDelaySeconds: 30` covers slow starts today; a `startupProbe` would let it take arbitrarily long to initialize without risking a liveness kill during a cold start (e.g. slow model config load).

None of these affect correctness of the current deployment.

### Migrating an existing volume to non-root

`fsGroup` does **not** apply to `subPath` mounts, and it changes group ownership but not file mode — so a PVC written by an earlier **root** run (e.g. a cluster that ran the gateway as root before enabling this hardening, or a backup restore of root-owned files) will keep files like `.jwt_secret` at `0600 root:root`. The non-root gateway (uid 1000) then can't read them and crashes on the first auth request with `RuntimeError: Failed to read JWT secret from .../​.jwt_secret`.

**Fresh installs are unaffected** — uid 1000 creates every file as `1000:1000`.

To fix an existing root-written PVC, run a one-shot root pod that chowns the volume to the gateway uid (1000), then restart the gateway:

```shell
cat <<'EOF' | kubectl apply -n deer-flow -f -
apiVersion: v1
kind: Pod
metadata: { name: fix-home-perms, namespace: deer-flow }
spec:
  restartPolicy: Never
  containers:
    - name: chown
      image: busybox:1.36
      command: ["sh", "-c"]
      args: ["chown -R 1000:1000 /home-pvc/deer-flow && chmod -R g+rwX /home-pvc/deer-flow"]
      volumeMounts:
        - { name: home, mountPath: /home-pvc }
  volumes:
    - name: home
      persistentVolumeClaim: { claimName: deer-flow-deer-flow-home }
EOF
kubectl -n deer-flow wait --for=condition=Ready pod/fix-home-perms --timeout=30s
kubectl -n deer-flow delete pod fix-home-perms
kubectl -n deer-flow rollout restart deploy/deer-flow-deer-flow-gateway
```

(On a single-node cluster the fix pod can mount the RWO PVC concurrently with the gateway; on multi-node, scale the gateway to 0 first.) A durable alternative — an opt-in root `volumePermissions` initContainer that chowns on every start (the Bitnami pattern) — is not yet wired into this chart; it would introduce a root container, so it's left as an operator decision for now.

## Sandbox Service type

The provisioner exposes each sandbox Pod behind a per-sandbox Service whose type is controlled by `provisioner.sandboxServiceType` (default `ClusterIP`).

**`ClusterIP` (default, recommended).** The provisioner returns a cluster-DNS URL - `http://sandbox-<id>-svc.<namespace>.svc.cluster.local:8080` - so the gateway reaches its sandbox entirely inside the cluster network. No node IP, no high port, and the code-execution surface is **not** bound on every node's interfaces. This is correct for the chart, where the gateway always runs in-cluster.

**`NodePort` (Docker-Compose/hybrid escape hatch).** Set `provisioner.sandboxServiceType: NodePort` only when the gateway is _not_ in K8s (e.g. the compose dev path, where the gateway is a container reaching sandbox Pods on the host's Docker Desktop K8s). The provisioner then returns `http://{NODE_HOST}:{NodePort}`. `NODE_HOST` defaults to the provisioner pod's node IP via the [downward API](https://kubernetes.io/docs/concepts/workloads/pods/downward-api/) (`status.hostIP`); because a NodePort is exposed on every node, the gateway can reach `<node-IP>:<NodePort>` on most clusters without configuration. Override `provisioner.nodeHost` only if your CNI or network policy blocks pod->node-IP traffic:

```shell
kubectl get nodes -o wide    # use INTERNAL-IP or EXTERNAL-IP
```

```yaml
provisioner:
  sandboxServiceType: NodePort
  nodeHost: 192.168.x.x
```

On multi-node clusters, also switch `persistence.home.accessMode` to `ReadWriteMany` (this is orthogonal to the Service type - it governs whether a sandbox Pod can be scheduled on a node other than the gateway's).

## Lint / dry-run

```shell
helm lint deploy/helm/deer-flow
helm template deer-flow deploy/helm/deer-flow -n deer-flow -f my-values.yaml | \
  kubectl apply --dry-run=client -f -
```

## Uninstall

```shell
helm uninstall deer-flow -n deer-flow
# the PVC is NOT deleted by default — remove it manually if desired:
kubectl -n deer-flow delete pvc -l app.kubernetes.io/instance=deer-flow
```