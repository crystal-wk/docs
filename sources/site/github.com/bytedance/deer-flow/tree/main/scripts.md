# Source: https://github.com/bytedance/deer-flow/tree/main/scripts

### Uh oh!

There was an error while loading. [Please reload this page]().

[bytedance](https://github.com/bytedance) / **[deer-flow](https://github.com/bytedance/deer-flow)** Public

- [Notifications](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow) You must be signed in to change notification settings
- [Fork 10.9k](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow)
- [Star 79.8k](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow)

 ## FilesExpand file tree

main

/

# scripts

/

Copy path

## Directory actions

## More options

More options

## Directory actions

## More options

More options

## Latest commit

[![TNsparrow](https://avatars.githubusercontent.com/u/96582924?v=4&size=40)](https://github.com/TNsparrow) [TNsparrow](https://github.com/bytedance/deer-flow/commits?author=TNsparrow)

[fix: resolve diagnostic paths from any cwd (](https://github.com/bytedance/deer-flow/commit/6bb376abfd9934827678058ca15cba21238226d5) [#4736](https://github.com/bytedance/deer-flow/pull/4736) [)](https://github.com/bytedance/deer-flow/commit/6bb376abfd9934827678058ca15cba21238226d5)

Open commit detailsfailure

Aug 11, 2026

[6bb376a](https://github.com/bytedance/deer-flow/commit/6bb376abfd9934827678058ca15cba21238226d5) · Aug 11, 2026

## History

[History](https://github.com/bytedance/deer-flow/commits/main/scripts)

Open commit details

History

## FilesExpand file tree

main

/

# scripts

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

[wizard](https://github.com/bytedance/deer-flow/tree/main/scripts/wizard 'wizard')

 | 

[wizard](https://github.com/bytedance/deer-flow/tree/main/scripts/wizard 'wizard')

 | 

[feat(wizard): add OrcaRouter as an LLM provider (](https://github.com/bytedance/deer-flow/commit/d0957409f1648ad5c7899202e055b032c25ca836 'feat(wizard): add OrcaRouter as an LLM provider (#4598)

OrcaRouter is an OpenAI-compatible routing gateway. Mirror the existing
OpenRouter entry in the setup wizard's LLM_PROVIDERS: reuse
langchain_openai:ChatOpenAI pointed at api.orcarouter.ai/v1 with env var
ORCAROUTER_API_KEY. Default model pins a tool-capable model; orcarouter/auto
is also selectable.

Disclosure: I'm an engineer on the OrcaRouter team.

Co-authored-by: jinhaosong-source <jinhaosong@myflashcloud.com>') [#4598](https://github.com/bytedance/deer-flow/pull/4598) [)](https://github.com/bytedance/deer-flow/commit/d0957409f1648ad5c7899202e055b032c25ca836 'feat(wizard): add OrcaRouter as an LLM provider (#4598)

OrcaRouter is an OpenAI-compatible routing gateway. Mirror the existing
OpenRouter entry in the setup wizard's LLM_PROVIDERS: reuse
langchain_openai:ChatOpenAI pointed at api.orcarouter.ai/v1 with env var
ORCAROUTER_API_KEY. Default model pins a tool-capable model; orcarouter/auto
is also selectable.

Disclosure: I'm an engineer on the OrcaRouter team.

Co-authored-by: jinhaosong-source <jinhaosong@myflashcloud.com>')

 | 

Jul 31, 2026

 |
| 

[\_detector\_cli.py](https://github.com/bytedance/deer-flow/blob/main/scripts/_detector_cli.py '_detector_cli.py')

 | 

[\_detector\_cli.py](https://github.com/bytedance/deer-flow/blob/main/scripts/_detector_cli.py '_detector_cli.py')

 | 

[chore(blocking-io): fail-loud repo-root resolution and shared detecto…](https://github.com/bytedance/deer-flow/commit/a838546a2b369d024c32d319d3445a5f4e9264a8 'chore(blocking-io): fail-loud repo-root resolution and shared detector CLI shim (#3512)

* chore(blocking-io): fail-loud repo-root resolution and shared detector CLI shim

The three detectors resolved REPO_ROOT with depth-indexed
Path(__file__).resolve().parents[4]. If a detector file ever moves to a
different directory depth, scan roots resolve under the wrong directory
and the detector reports zero findings with no error — a silent-zero
failure shape for a detection tool.

- Add support/detectors/repo_root.py: resolve the repo root by walking
 upward to the .git marker (checked with exists() so git worktrees,
 where .git is a file, also resolve), raising RuntimeError when no
 marker is found. All three detectors use it at import time, so a
 relocated detector fails loudly instead of scanning an empty tree.
- Extract scripts/_detector_cli.py from the three character-identical
 CLI shims; the sys.path computation lives in one place and raises
 when backend/tests cannot be found.
- tests/test_detector_repo_root.py pins: resolution from an unmarked
 location raises instead of returning an empty scan; all three
 detectors share the resolved root; each CLI shim delegates to its
 detector.

Testing: backend `make test` (4278 passed); smoke-ran
`make detect-blocking-io`, `make detect-thread-boundaries`, and
`scripts/scan_changed_blocking_io.py --base upstream/main`.

Closes #3510 (review follow-up to #3503).

* chore(blocking-io): declare detector modules import-only, drop script-mode residue

Adversarial review caught that blocking_io_static.py and
thread_boundaries.py kept shebangs and __main__ blocks but can no longer
run as plain scripts: the new `from support.detectors.repo_root import`
executes before anything puts backend/tests on sys.path, so direct
invocation dies with ModuleNotFoundError before argparse.

Direct execution was never a documented entry point (Makefile targets,
the scripts/ shims, the blocking-io-guard skill, and tests all go
through the support.detectors package), so converge on import-only
instead of re-adding per-module bootstrap: drop the shebangs and the now
unreachable __main__ blocks (plus the `import sys` they kept alive) and
state the supported entry points in each module docstring. The shim
delegation tests in test_detector_repo_root.py pin the supported CLI
paths.

Testing: backend `make test` (4278 passed); `make detect-blocking-io`
and `make detect-thread-boundaries` smoke-ran.')

 | 

Jun 12, 2026

 |
| 

[bump\_version.sh](https://github.com/bytedance/deer-flow/blob/main/scripts/bump_version.sh 'bump_version.sh')

 | 

[bump\_version.sh](https://github.com/bytedance/deer-flow/blob/main/scripts/bump_version.sh 'bump_version.sh')

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

[check.py](https://github.com/bytedance/deer-flow/blob/main/scripts/check.py 'check.py')

 | 

[check.py](https://github.com/bytedance/deer-flow/blob/main/scripts/check.py 'check.py')

 | 

[fix: resolve diagnostic paths from any cwd (](https://github.com/bytedance/deer-flow/commit/6bb376abfd9934827678058ca15cba21238226d5 'fix: resolve diagnostic paths from any cwd (#4736)

* fix: resolve diagnostic paths from any cwd

* test: cover relative diagnostic script paths') [#4736](https://github.com/bytedance/deer-flow/pull/4736) [)](https://github.com/bytedance/deer-flow/commit/6bb376abfd9934827678058ca15cba21238226d5 'fix: resolve diagnostic paths from any cwd (#4736)

* fix: resolve diagnostic paths from any cwd

* test: cover relative diagnostic script paths')

 | 

Aug 11, 2026

 |
| 

[check.sh](https://github.com/bytedance/deer-flow/blob/main/scripts/check.sh 'check.sh')

 | 

[check.sh](https://github.com/bytedance/deer-flow/blob/main/scripts/check.sh 'check.sh')

 | 

[feat(dx): Setup Wizard + doctor command —](https://github.com/bytedance/deer-flow/commit/eef0a6e2dadefd360a74ffbc19c5fb6d0bb7d426 'feat(dx): Setup Wizard + doctor command — closes #2030 (#2034)') [closes](https://github.com/bytedance/deer-flow/commit/eef0a6e2dadefd360a74ffbc19c5fb6d0bb7d426 'feat(dx): Setup Wizard + doctor command — closes #2030 (#2034)') [#2030](https://github.com/bytedance/deer-flow/issues/2030) [(](https://github.com/bytedance/deer-flow/commit/eef0a6e2dadefd360a74ffbc19c5fb6d0bb7d426 'feat(dx): Setup Wizard + doctor command — closes #2030 (#2034)') [#2034](https://github.com/bytedance/deer-flow/pull/2034) [)](https://github.com/bytedance/deer-flow/commit/eef0a6e2dadefd360a74ffbc19c5fb6d0bb7d426 'feat(dx): Setup Wizard + doctor command — closes #2030 (#2034)')

 | 

Apr 10, 2026

 |
| 

[check\_chart\_sandbox\_service.sh](https://github.com/bytedance/deer-flow/blob/main/scripts/check_chart_sandbox_service.sh 'check_chart_sandbox_service.sh')

 | 

[check\_chart\_sandbox\_service.sh](https://github.com/bytedance/deer-flow/blob/main/scripts/check_chart_sandbox_service.sh 'check_chart_sandbox_service.sh')

 | 

[fix(helm): default sandbox Services to ClusterIP (](https://github.com/bytedance/deer-flow/commit/d57f695769833dce874737203faefb94c920e0a5 'fix(helm): default sandbox Services to ClusterIP (#3929) (#4190)

* fix(helm): default sandbox Services to ClusterIP (#3929)

The K8s sandbox provisioner supports both NodePort and ClusterIP via
SANDBOX_SERVICE_TYPE (added in #4016), but the Helm chart never set it,
so real-cluster installs inherited the NodePort default. That bound the
code-execution sandbox on every node's interfaces - including externally
reachable ones on GKE/EKS/AKS - and pinned every sandbox URL to one node
IP (SPOF on node reboot/drain/ephemeral-IP).

Default the chart to ClusterIP: the provisioner returns a cluster-DNS URL
(http://sandbox-<id>-svc.<ns>.svc.cluster.local:8080) so the gateway->
sandbox hop stays inside the cluster network - no node IP, no 30xxx port,
no external exposure. The chart always runs the gateway in-cluster, so
ClusterIP is always correct there.

NodePort remains an opt-in (provisioner.sandboxServiceType: NodePort +
nodeHost) for the Docker-Compose/hybrid path where the gateway is not in
K8s and cannot resolve .svc.cluster.local; the provisioner code default
stays NodePort for that path.

- values.yaml: add provisioner.sandboxServiceType ("ClusterIP")
- provisioner-deployment.yaml: emit SANDBOX_SERVICE_TYPE; gate the
 NODE_HOST block on NodePort mode (default "ClusterIP" for upgrade safety)
- NOTES.txt + README.md: document ClusterIP default + NodePort opt-in

No change to docker/provisioner/app.py (already mode-aware since #4016)
or RBAC (services verbs already cover ClusterIP).

* test(helm): assert sandbox Service-type gating + CHANGELOG the default flip (#3929)

Address review on #4190:

- Add scripts/check_chart_sandbox_service.sh: renders the chart for the
 default (ClusterIP, no NODE_HOST), the NodePort opt-in (both emitted),
 and NodePort+nodeHost (literal value, not downward API). Locks in the
 #3929 gating so a regression (e.g. re-adding an unconditional NODE_HOST,
 or dropping the `default "ClusterIP"` upgrade-safety fallback) fails CI.
 Wired into .github/workflows/chart.yaml validate-chart job. (#2)
- CHANGELOG [Unreleased] -> Changed: note the NodePort->ClusterIP default
 flip on upgrade + the `sandboxServiceType: NodePort` opt-back-in. (#4)

No chart template changes (the gating itself landed in the first commit).

---------

Co-authored-by: Willem Jiang <willem.jiang@gmail.com>') [#3929](https://github.com/bytedance/deer-flow/issues/3929) [) (](https://github.com/bytedance/deer-flow/commit/d57f695769833dce874737203faefb94c920e0a5 'fix(helm): default sandbox Services to ClusterIP (#3929) (#4190)

* fix(helm): default sandbox Services to ClusterIP (#3929)

The K8s sandbox provisioner supports both NodePort and ClusterIP via
SANDBOX_SERVICE_TYPE (added in #4016), but the Helm chart never set it,
so real-cluster installs inherited the NodePort default. That bound the
code-execution sandbox on every node's interfaces - including externally
reachable ones on GKE/EKS/AKS - and pinned every sandbox URL to one node
IP (SPOF on node reboot/drain/ephemeral-IP).

Default the chart to ClusterIP: the provisioner returns a cluster-DNS URL
(http://sandbox-<id>-svc.<ns>.svc.cluster.local:8080) so the gateway->
sandbox hop stays inside the cluster network - no node IP, no 30xxx port,
no external exposure. The chart always runs the gateway in-cluster, so
ClusterIP is always correct there.

NodePort remains an opt-in (provisioner.sandboxServiceType: NodePort +
nodeHost) for the Docker-Compose/hybrid path where the gateway is not in
K8s and cannot resolve .svc.cluster.local; the provisioner code default
stays NodePort for that path.

- values.yaml: add provisioner.sandboxServiceType ("ClusterIP")
- provisioner-deployment.yaml: emit SANDBOX_SERVICE_TYPE; gate the
 NODE_HOST block on NodePort mode (default "ClusterIP" for upgrade safety)
- NOTES.txt + README.md: document ClusterIP default + NodePort opt-in

No change to docker/provisioner/app.py (already mode-aware since #4016)
or RBAC (services verbs already cover ClusterIP).

* test(helm): assert sandbox Service-type gating + CHANGELOG the default flip (#3929)

Address review on #4190:

- Add scripts/check_chart_sandbox_service.sh: renders the chart for the
 default (ClusterIP, no NODE_HOST), the NodePort opt-in (both emitted),
 and NodePort+nodeHost (literal value, not downward API). Locks in the
 #3929 gating so a regression (e.g. re-adding an unconditional NODE_HOST,
 or dropping the `default "ClusterIP"` upgrade-safety fallback) fails CI.
 Wired into .github/workflows/chart.yaml validate-chart job. (#2)
- CHANGELOG [Unreleased] -> Changed: note the NodePort->ClusterIP default
 flip on upgrade + the `sandboxServiceType: NodePort` opt-back-in. (#4)

No chart template changes (the gating itself landed in the first commit).

---------

Co-authored-by: Willem Jiang <willem.jiang@gmail.com>') [#4190](https://github.com/bytedance/deer-flow/pull/4190) [)](https://github.com/bytedance/deer-flow/commit/d57f695769833dce874737203faefb94c920e0a5 'fix(helm): default sandbox Services to ClusterIP (#3929) (#4190)

* fix(helm): default sandbox Services to ClusterIP (#3929)

The K8s sandbox provisioner supports both NodePort and ClusterIP via
SANDBOX_SERVICE_TYPE (added in #4016), but the Helm chart never set it,
so real-cluster installs inherited the NodePort default. That bound the
code-execution sandbox on every node's interfaces - including externally
reachable ones on GKE/EKS/AKS - and pinned every sandbox URL to one node
IP (SPOF on node reboot/drain/ephemeral-IP).

Default the chart to ClusterIP: the provisioner returns a cluster-DNS URL
(http://sandbox-<id>-svc.<ns>.svc.cluster.local:8080) so the gateway->
sandbox hop stays inside the cluster network - no node IP, no 30xxx port,
no external exposure. The chart always runs the gateway in-cluster, so
ClusterIP is always correct there.

NodePort remains an opt-in (provisioner.sandboxServiceType: NodePort +
nodeHost) for the Docker-Compose/hybrid path where the gateway is not in
K8s and cannot resolve .svc.cluster.local; the provisioner code default
stays NodePort for that path.

- values.yaml: add provisioner.sandboxServiceType ("ClusterIP")
- provisioner-deployment.yaml: emit SANDBOX_SERVICE_TYPE; gate the
 NODE_HOST block on NodePort mode (default "ClusterIP" for upgrade safety)
- NOTES.txt + README.md: document ClusterIP default + NodePort opt-in

No change to docker/provisioner/app.py (already mode-aware since #4016)
or RBAC (services verbs already cover ClusterIP).

* test(helm): assert sandbox Service-type gating + CHANGELOG the default flip (#3929)

Address review on #4190:

- Add scripts/check_chart_sandbox_service.sh: renders the chart for the
 default (ClusterIP, no NODE_HOST), the NodePort opt-in (both emitted),
 and NodePort+nodeHost (literal value, not downward API). Locks in the
 #3929 gating so a regression (e.g. re-adding an unconditional NODE_HOST,
 or dropping the `default "ClusterIP"` upgrade-safety fallback) fails CI.
 Wired into .github/workflows/chart.yaml validate-chart job. (#2)
- CHANGELOG [Unreleased] -> Changed: note the NodePort->ClusterIP default
 flip on upgrade + the `sandboxServiceType: NodePort` opt-back-in. (#4)

No chart template changes (the gating itself landed in the first commit).

---------

Co-authored-by: Willem Jiang <willem.jiang@gmail.com>')

 | 

Jul 16, 2026

 |
| 

[check\_config\_version.sh](https://github.com/bytedance/deer-flow/blob/main/scripts/check_config_version.sh 'check_config_version.sh')

 | 

[check\_config\_version.sh](https://github.com/bytedance/deer-flow/blob/main/scripts/check_config_version.sh 'check_config_version.sh')

 | 

[ci: add nightly build for images + helm chart (](https://github.com/bytedance/deer-flow/commit/7d1a8fb75371f73db8b525a8b5701a489786b803 'ci: add nightly build for images + helm chart (#4050)

* ci: add nightly build workflow for images + helm chart

Nightly build of backend/frontend/provisioner images and the helm chart,
pushed to GHCR with nightly + nightly-YYYYMMDD tags (latest stays on v*
releases). amd64 only. Gated to the upstream repo (bytedance/deer-flow).

Documented in RELEASING.md.

* ci(nightly): harden chart patch + dedupe config_version check

Address PR #4050 review feedback:

- Gate the in-workflow chart patches with grep assertions so a drifted
 Chart.yaml/values.yaml fails loudly instead of silently shipping a chart
 that pulls the release `latest` images (sed exits 0 on zero matches).
- Suffix the nightly chart version with the short SHA
 (<base>-nightly.<date>-<sha>) so a same-day re-dispatch re-publishes
 cleanly; OCI chart versions are immutable and otherwise collide.
- Note in the image-tags comment that :nightly-<date> is mutable within a
 day and :sha-<short> is the only truly immutable pin.
- Extract the config_version drift check into scripts/check_config_version.sh,
 shared by chart.yaml and nightly.yaml, so the parsing logic lives in one
 place.') [#4050](https://github.com/bytedance/deer-flow/pull/4050) [)](https://github.com/bytedance/deer-flow/commit/7d1a8fb75371f73db8b525a8b5701a489786b803 'ci: add nightly build for images + helm chart (#4050)

* ci: add nightly build workflow for images + helm chart

Nightly build of backend/frontend/provisioner images and the helm chart,
pushed to GHCR with nightly + nightly-YYYYMMDD tags (latest stays on v*
releases). amd64 only. Gated to the upstream repo (bytedance/deer-flow).

Documented in RELEASING.md.

* ci(nightly): harden chart patch + dedupe config_version check

Address PR #4050 review feedback:

- Gate the in-workflow chart patches with grep assertions so a drifted
 Chart.yaml/values.yaml fails loudly instead of silently shipping a chart
 that pulls the release `latest` images (sed exits 0 on zero matches).
- Suffix the nightly chart version with the short SHA
 (<base>-nightly.<date>-<sha>) so a same-day re-dispatch re-publishes
 cleanly; OCI chart versions are immutable and otherwise collide.
- Note in the image-tags comment that :nightly-<date> is mutable within a
 day and :sha-<short> is the only truly immutable pin.
- Extract the config_version drift check into scripts/check_config_version.sh,
 shared by chart.yaml and nightly.yaml, so the parsing logic lives in one
 place.')

 | 

Jul 11, 2026

 |
| 

[cleanup-containers.sh](https://github.com/bytedance/deer-flow/blob/main/scripts/cleanup-containers.sh 'cleanup-containers.sh')

 | 

[cleanup-containers.sh](https://github.com/bytedance/deer-flow/blob/main/scripts/cleanup-containers.sh 'cleanup-containers.sh')

 | 

[feat: send custom event](https://github.com/bytedance/deer-flow/commit/9bf3a12c30abaea3e897f82c55116e7cc1d8b4db 'feat: send custom event')

 | 

Feb 6, 2026

 |
| 

[config-upgrade.sh](https://github.com/bytedance/deer-flow/blob/main/scripts/config-upgrade.sh 'config-upgrade.sh')

 | 

[config-upgrade.sh](https://github.com/bytedance/deer-flow/blob/main/scripts/config-upgrade.sh 'config-upgrade.sh')

 | 

[Fix Windows startup and dependency checks (](https://github.com/bytedance/deer-flow/commit/82c3dbbc6bb6c7a8e5349144ffd77125d22618b2 'Fix Windows startup and dependency checks (#1709)

* windows check and dev fixes

* fix windows startup scripts

* fix windows startup scripts

---------

Co-authored-by: Willem Jiang <willem.jiang@gmail.com>') [#1709](https://github.com/bytedance/deer-flow/pull/1709) [)](https://github.com/bytedance/deer-flow/commit/82c3dbbc6bb6c7a8e5349144ffd77125d22618b2 'Fix Windows startup and dependency checks (#1709)

* windows check and dev fixes

* fix windows startup scripts

* fix windows startup scripts

---------

Co-authored-by: Willem Jiang <willem.jiang@gmail.com>')

 | 

Apr 1, 2026

 |
| 

[configure.py](https://github.com/bytedance/deer-flow/blob/main/scripts/configure.py 'configure.py')

 | 

[configure.py](https://github.com/bytedance/deer-flow/blob/main/scripts/configure.py 'configure.py')

 | 

[fix: make check/config cross-platform for Windows (](https://github.com/bytedance/deer-flow/commit/a79d4146956446e56d3db707f17d6d05f98fe527 'fix: make check/config cross-platform for Windows (#1080) (#1093)

* fix: make check/config cross-platform for Windows (#1080)

- replace shell-based check/config recipes with Python entrypoints
- add a cross-platform dependency checker script
- add a cross-platform config bootstrap script
- route make targets through a Python variable for consistent invocation
- preserve existing config-abort behavior when config file already exists

* Apply suggestions from code review

Co-authored-by: Copilot <175728472+Copilot@users.noreply.github.com>

---------

Co-authored-by: Copilot <175728472+Copilot@users.noreply.github.com>') [#1080](https://github.com/bytedance/deer-flow/issues/1080) [) (](https://github.com/bytedance/deer-flow/commit/a79d4146956446e56d3db707f17d6d05f98fe527 'fix: make check/config cross-platform for Windows (#1080) (#1093)

* fix: make check/config cross-platform for Windows (#1080)

- replace shell-based check/config recipes with Python entrypoints
- add a cross-platform dependency checker script
- add a cross-platform config bootstrap script
- route make targets through a Python variable for consistent invocation
- preserve existing config-abort behavior when config file already exists

* Apply suggestions from code review

Co-authored-by: Copilot <175728472+Copilot@users.noreply.github.com>

---------

Co-authored-by: Copilot <175728472+Copilot@users.noreply.github.com>') [#1093](https://github.com/bytedance/deer-flow/pull/1093) [)](https://github.com/bytedance/deer-flow/commit/a79d4146956446e56d3db707f17d6d05f98fe527 'fix: make check/config cross-platform for Windows (#1080) (#1093)

* fix: make check/config cross-platform for Windows (#1080)

- replace shell-based check/config recipes with Python entrypoints
- add a cross-platform dependency checker script
- add a cross-platform config bootstrap script
- route make targets through a Python variable for consistent invocation
- preserve existing config-abort behavior when config file already exists

* Apply suggestions from code review

Co-authored-by: Copilot <175728472+Copilot@users.noreply.github.com>

---------

Co-authored-by: Copilot <175728472+Copilot@users.noreply.github.com>')

 | 

Mar 13, 2026

 |
| 

[deploy.sh](https://github.com/bytedance/deer-flow/blob/main/scripts/deploy.sh 'deploy.sh')

 | 

[deploy.sh](https://github.com/bytedance/deer-flow/blob/main/scripts/deploy.sh 'deploy.sh')

 | 

[fix(docker): bind the published entry port to loopback by default (](https://github.com/bytedance/deer-flow/commit/2a143dced6adb80190b07c7db3ca79bff3a853ad 'fix(docker): bind the published entry port to loopback by default (#4618)

README documents DeerFlow as deployed by default "in a local trusted
environment (accessible only via the 127.0.0.1 loopback interface)", but both
compose files published nginx as `"${PORT:-2026}:2026"`, which Docker binds to
0.0.0.0 and [::]. The shipped artifact did not match its own documented
default, so running it on a LAN or cloud host produced a wider surface than
the docs implied without the operator changing anything -- and the agent can
execute commands.

Publish as `"${BIND_HOST:-127.0.0.1}:${PORT:-2026}:2026"` in both compose
files, so the default matches the documented model while operators who front
the stack with their own TLS/auth can still widen it via BIND_HOST. The
Gateway keeps binding 0.0.0.0:8001 inside the container (nginx reaches it over
the compose network) and its port stays unpublished, so the published nginx
port is the entire external surface.

BREAKING CHANGE: a deployment that relied on the previous 0.0.0.0 default
becomes unreachable from other hosts after this upgrade. Set BIND_HOST=0.0.0.0
in .env to restore it, after putting authentication in front and completing
first-run setup.

Also:
- .env.example documents BIND_HOST and PORT with the reasoning.
- deploy.sh reports the address the stack actually bound and, when it is not
 loopback, tells the operator to complete first-run setup immediately. It
 reads BIND_HOST/PORT from .env via a new read_dotenv_value helper following
 compose precedence; the shell does not source .env, so reading the
 environment alone would have reported "loopback only" for a stack .env had
 exposed. The pre-existing ${PORT} summary line had the same defect and is
 fixed with it.
- test_compose_default_bind_host.py pins the loopback default, that BIND_HOST
 stays overridable, and that no service in either compose file publishes a
 port without an explicit bind address, so a later addition cannot drift back
 to 0.0.0.0 unnoticed.') [#4618](https://github.com/bytedance/deer-flow/pull/4618)

 | 

Aug 1, 2026

 |
| 

[detect\_blocking\_io\_static.py](https://github.com/bytedance/deer-flow/blob/main/scripts/detect_blocking_io_static.py 'detect_blocking_io_static.py')

 | 

[detect\_blocking\_io\_static.py](https://github.com/bytedance/deer-flow/blob/main/scripts/detect_blocking_io_static.py 'detect_blocking_io_static.py')

 | 

[chore(blocking-io): fail-loud repo-root resolution and shared detecto…](https://github.com/bytedance/deer-flow/commit/a838546a2b369d024c32d319d3445a5f4e9264a8 'chore(blocking-io): fail-loud repo-root resolution and shared detector CLI shim (#3512)

* chore(blocking-io): fail-loud repo-root resolution and shared detector CLI shim

The three detectors resolved REPO_ROOT with depth-indexed
Path(__file__).resolve().parents[4]. If a detector file ever moves to a
different directory depth, scan roots resolve under the wrong directory
and the detector reports zero findings with no error — a silent-zero
failure shape for a detection tool.

- Add support/detectors/repo_root.py: resolve the repo root by walking
 upward to the .git marker (checked with exists() so git worktrees,
 where .git is a file, also resolve), raising RuntimeError when no
 marker is found. All three detectors use it at import time, so a
 relocated detector fails loudly instead of scanning an empty tree.
- Extract scripts/_detector_cli.py from the three character-identical
 CLI shims; the sys.path computation lives in one place and raises
 when backend/tests cannot be found.
- tests/test_detector_repo_root.py pins: resolution from an unmarked
 location raises instead of returning an empty scan; all three
 detectors share the resolved root; each CLI shim delegates to its
 detector.

Testing: backend `make test` (4278 passed); smoke-ran
`make detect-blocking-io`, `make detect-thread-boundaries`, and
`scripts/scan_changed_blocking_io.py --base upstream/main`.

Closes #3510 (review follow-up to #3503).

* chore(blocking-io): declare detector modules import-only, drop script-mode residue

Adversarial review caught that blocking_io_static.py and
thread_boundaries.py kept shebangs and __main__ blocks but can no longer
run as plain scripts: the new `from support.detectors.repo_root import`
executes before anything puts backend/tests on sys.path, so direct
invocation dies with ModuleNotFoundError before argparse.

Direct execution was never a documented entry point (Makefile targets,
the scripts/ shims, the blocking-io-guard skill, and tests all go
through the support.detectors package), so converge on import-only
instead of re-adding per-module bootstrap: drop the shebangs and the now
unreachable __main__ blocks (plus the `import sys` they kept alive) and
state the supported entry points in each module docstring. The shim
delegation tests in test_detector_repo_root.py pin the supported CLI
paths.

Testing: backend `make test` (4278 passed); `make detect-blocking-io`
and `make detect-thread-boundaries` smoke-ran.')

 | 

Jun 12, 2026

 |
| 

[detect\_thread\_boundaries.py](https://github.com/bytedance/deer-flow/blob/main/scripts/detect_thread_boundaries.py 'detect_thread_boundaries.py')

 | 

[detect\_thread\_boundaries.py](https://github.com/bytedance/deer-flow/blob/main/scripts/detect_thread_boundaries.py 'detect_thread_boundaries.py')

 | 

[chore(blocking-io): fail-loud repo-root resolution and shared detecto…](https://github.com/bytedance/deer-flow/commit/a838546a2b369d024c32d319d3445a5f4e9264a8 'chore(blocking-io): fail-loud repo-root resolution and shared detector CLI shim (#3512)

* chore(blocking-io): fail-loud repo-root resolution and shared detector CLI shim

The three detectors resolved REPO_ROOT with depth-indexed
Path(__file__).resolve().parents[4]. If a detector file ever moves to a
different directory depth, scan roots resolve under the wrong directory
and the detector reports zero findings with no error — a silent-zero
failure shape for a detection tool.

- Add support/detectors/repo_root.py: resolve the repo root by walking
 upward to the .git marker (checked with exists() so git worktrees,
 where .git is a file, also resolve), raising RuntimeError when no
 marker is found. All three detectors use it at import time, so a
 relocated detector fails loudly instead of scanning an empty tree.
- Extract scripts/_detector_cli.py from the three character-identical
 CLI shims; the sys.path computation lives in one place and raises
 when backend/tests cannot be found.
- tests/test_detector_repo_root.py pins: resolution from an unmarked
 location raises instead of returning an empty scan; all three
 detectors share the resolved root; each CLI shim delegates to its
 detector.

Testing: backend `make test` (4278 passed); smoke-ran
`make detect-blocking-io`, `make detect-thread-boundaries`, and
`scripts/scan_changed_blocking_io.py --base upstream/main`.

Closes #3510 (review follow-up to #3503).

* chore(blocking-io): declare detector modules import-only, drop script-mode residue

Adversarial review caught that blocking_io_static.py and
thread_boundaries.py kept shebangs and __main__ blocks but can no longer
run as plain scripts: the new `from support.detectors.repo_root import`
executes before anything puts backend/tests on sys.path, so direct
invocation dies with ModuleNotFoundError before argparse.

Direct execution was never a documented entry point (Makefile targets,
the scripts/ shims, the blocking-io-guard skill, and tests all go
through the support.detectors package), so converge on import-only
instead of re-adding per-module bootstrap: drop the shebangs and the now
unreachable __main__ blocks (plus the `import sys` they kept alive) and
state the supported entry points in each module docstring. The shim
delegation tests in test_detector_repo_root.py pin the supported CLI
paths.

Testing: backend `make test` (4278 passed); `make detect-blocking-io`
and `make detect-thread-boundaries` smoke-ran.')

 | 

Jun 12, 2026

 |
| 

[detect\_uv\_extras.py](https://github.com/bytedance/deer-flow/blob/main/scripts/detect_uv_extras.py 'detect_uv_extras.py')

 | 

[detect\_uv\_extras.py](https://github.com/bytedance/deer-flow/blob/main/scripts/detect_uv_extras.py 'detect_uv_extras.py')

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

[docker.sh](https://github.com/bytedance/deer-flow/blob/main/scripts/docker.sh 'docker.sh')

 | 

[docker.sh](https://github.com/bytedance/deer-flow/blob/main/scripts/docker.sh 'docker.sh')

 | 

[fix(docker): set DEER\_FLOW\_ROOT for log commands (](https://github.com/bytedance/deer-flow/commit/276481371e613d56c111c4fdc1067c87bdf24079 'fix(docker): set DEER_FLOW_ROOT for log commands (#4658)

* fix(docker): set DEER_FLOW_ROOT for log commands

* fix(docker): set root before restart

* docs(docker): clarify log command') [#4658](https://github.com/bytedance/deer-flow/pull/4658) [)](https://github.com/bytedance/deer-flow/commit/276481371e613d56c111c4fdc1067c87bdf24079 'fix(docker): set DEER_FLOW_ROOT for log commands (#4658)

* fix(docker): set DEER_FLOW_ROOT for log commands

* fix(docker): set root before restart

* docs(docker): clarify log command')

 | 

Aug 4, 2026

 |
| 

[doctor.py](https://github.com/bytedance/deer-flow/blob/main/scripts/doctor.py 'doctor.py')

 | 

[doctor.py](https://github.com/bytedance/deer-flow/blob/main/scripts/doctor.py 'doctor.py')

 | 

[fix: resolve diagnostic paths from any cwd (](https://github.com/bytedance/deer-flow/commit/6bb376abfd9934827678058ca15cba21238226d5 'fix: resolve diagnostic paths from any cwd (#4736)

* fix: resolve diagnostic paths from any cwd

* test: cover relative diagnostic script paths') [#4736](https://github.com/bytedance/deer-flow/pull/4736) [)](https://github.com/bytedance/deer-flow/commit/6bb376abfd9934827678058ca15cba21238226d5 'fix: resolve diagnostic paths from any cwd (#4736)

* fix: resolve diagnostic paths from any cwd

* test: cover relative diagnostic script paths')

 | 

Aug 11, 2026

 |
| 

[export\_claude\_code\_oauth.py](https://github.com/bytedance/deer-flow/blob/main/scripts/export_claude_code_oauth.py 'export_claude_code_oauth.py')

 | 

[export\_claude\_code\_oauth.py](https://github.com/bytedance/deer-flow/blob/main/scripts/export_claude_code_oauth.py 'export_claude_code_oauth.py')

 | 

[feat: add Claude Code OAuth and Codex CLI as LLM providers (](https://github.com/bytedance/deer-flow/commit/835ba041f8e5eb7faa59aa7192a231a02f2a798e 'feat: add Claude Code OAuth and Codex CLI as LLM providers (#1166)

* feat: add Claude Code OAuth and Codex CLI providers

Port of bytedance/deer-flow#1136 from @solanian's feat/cli-oauth-providers branch.\n\nCarries the feature forward on top of current main without the original CLA-blocked commit metadata, while preserving attribution in the commit message for review.

* fix: harden CLI credential loading

Align Codex auth loading with the current ~/.codex/auth.json shape, make Docker credential mounts directory-based to avoid broken file binds on hosts without exported credential files, and add focused loader tests.

* refactor: tighten codex auth typing

Replace the temporary Any return type in CodexChatModel._load_codex_auth with the concrete CodexCliCredential type after the credential loader was stabilized.

* fix: load Claude Code OAuth from Keychain

Match Claude Code's macOS storage strategy more closely by checking the Keychain-backed credentials store before falling back to ~/.claude/.credentials.json. Keep explicit file overrides and add focused tests for the Keychain path.

* fix: require explicit Claude OAuth handoff

* style: format thread hooks reasoning request

* docs: document CLI-backed auth providers

* fix: address provider review feedback

* fix: harden provider edge cases

* Fix deferred tools, Codex message normalization, and local sandbox paths

* chore: narrow PR scope to OAuth providers

* chore: remove unrelated frontend changes

* chore: reapply OAuth branch frontend scope cleanup

* fix: preserve upload guards with reasoning effort wiring

---------

Co-authored-by: Willem Jiang <willem.jiang@gmail.com>') [#1166](https://github.com/bytedance/deer-flow/pull/1166) [)](https://github.com/bytedance/deer-flow/commit/835ba041f8e5eb7faa59aa7192a231a02f2a798e 'feat: add Claude Code OAuth and Codex CLI as LLM providers (#1166)

* feat: add Claude Code OAuth and Codex CLI providers

Port of bytedance/deer-flow#1136 from @solanian's feat/cli-oauth-providers branch.\n\nCarries the feature forward on top of current main without the original CLA-blocked commit metadata, while preserving attribution in the commit message for review.

* fix: harden CLI credential loading

Align Codex auth loading with the current ~/.codex/auth.json shape, make Docker credential mounts directory-based to avoid broken file binds on hosts without exported credential files, and add focused loader tests.

* refactor: tighten codex auth typing

Replace the temporary Any return type in CodexChatModel._load_codex_auth with the concrete CodexCliCredential type after the credential loader was stabilized.

* fix: load Claude Code OAuth from Keychain

Match Claude Code's macOS storage strategy more closely by checking the Keychain-backed credentials store before falling back to ~/.claude/.credentials.json. Keep explicit file overrides and add focused tests for the Keychain path.

* fix: require explicit Claude OAuth handoff

* style: format thread hooks reasoning request

* docs: document CLI-backed auth providers

* fix: address provider review feedback

* fix: harden provider edge cases

* Fix deferred tools, Codex message normalization, and local sandbox paths

* chore: narrow PR scope to OAuth providers

* chore: remove unrelated frontend changes

* chore: reapply OAuth branch frontend scope cleanup

* fix: preserve upload guards with reasoning effort wiring

---------

Co-authored-by: Willem Jiang <willem.jiang@gmail.com>')

 | 

Mar 22, 2026

 |
| 

[load\_memory\_sample.py](https://github.com/bytedance/deer-flow/blob/main/scripts/load_memory_sample.py 'load_memory_sample.py')

 | 

[load\_memory\_sample.py](https://github.com/bytedance/deer-flow/blob/main/scripts/load_memory_sample.py 'load_memory_sample.py')

 | 

[feat: add memory management actions and local filters in memory setti…](https://github.com/bytedance/deer-flow/commit/7eb3a150b5f3f3824515417685e49f00a6acd2fd 'feat: add memory management actions and local filters in memory settings (#1467)

* Add MVP memory management actions

* Fix memory settings locale coverage

* Polish memory management interactions

* Add memory search and type filters

* Refine memory settings review feedback

* docs: simplify memory settings review setup

* fix: restore memory updater compatibility helpers

* fix: address memory settings review feedback

* docs: soften memory sample review wording

---------

Co-authored-by: Willem Jiang <willem.jiang@gmail.com>
Co-authored-by: JeffJiang <for-eleven@hotmail.com>')

 | 

Mar 29, 2026

 |
| 

[nginx.sh](https://github.com/bytedance/deer-flow/blob/main/scripts/nginx.sh 'nginx.sh')

 | 

[nginx.sh](https://github.com/bytedance/deer-flow/blob/main/scripts/nginx.sh 'nginx.sh')

 | 

[docs: fix stale docs and typos (](https://github.com/bytedance/deer-flow/commit/629477fd5c1914a129c76798d9c3e5b85a51ba25 'docs: fix stale docs and typos (#3913)') [#3913](https://github.com/bytedance/deer-flow/pull/3913) [)](https://github.com/bytedance/deer-flow/commit/629477fd5c1914a129c76798d9c3e5b85a51ba25 'docs: fix stale docs and typos (#3913)')

 | 

Jul 3, 2026

 |
| 

[pnpm.py](https://github.com/bytedance/deer-flow/blob/main/scripts/pnpm.py 'pnpm.py')

 | 

[pnpm.py](https://github.com/bytedance/deer-flow/blob/main/scripts/pnpm.py 'pnpm.py')

 | 

[fix: align pnpm consumers with Corepack fallback (](https://github.com/bytedance/deer-flow/commit/4e449385516c03b6b279ced004ff0ada493d56ef 'fix: align pnpm consumers with Corepack fallback (#4405)

* fix: align pnpm consumers with Corepack fallback

* fix: run pnpm helper from frontend workspace

* fix: preserve Corepack resolution hint') [#4405](https://github.com/bytedance/deer-flow/pull/4405) [)](https://github.com/bytedance/deer-flow/commit/4e449385516c03b6b279ced004ff0ada493d56ef 'fix: align pnpm consumers with Corepack fallback (#4405)

* fix: align pnpm consumers with Corepack fallback

* fix: run pnpm helper from frontend workspace

* fix: preserve Corepack resolution hint')

 | 

Jul 29, 2026

 |
| 

[review\_changed\_public\_skills.py](https://github.com/bytedance/deer-flow/blob/main/scripts/review_changed_public_skills.py 'review_changed_public_skills.py')

 | 

[review\_changed\_public\_skills.py](https://github.com/bytedance/deer-flow/blob/main/scripts/review_changed_public_skills.py 'review_changed_public_skills.py')

 | 

[fix(skills): recognize fully deleted public skill packages in review …](https://github.com/bytedance/deer-flow/commit/656f6b364c30b1137b84bf0d8f01002bab5eaefe 'fix(skills): recognize fully deleted public skill packages in review CI (#4169)

select_skill_packages() resolved every changed non-SKILL.md path to its
owning package via an unconditional depth-3 fallback, then queued that
path for review. When a PR deletes an entire public skill package (not
just SKILL.md, but its scripts/assets/etc. too), the fallback still
returned the package directory even though it no longer exists on disk
post-deletion. The review CLI then reported a false
structure.missing-skill-md blocker for a path that isn't there,
failing CI on a routine, correct package removal.

Skip a resolved package only when every changed file under it was a
deletion and the package directory itself is gone from disk - i.e. the
whole package was intentionally removed. A package left in a
broken/partial state (e.g. SKILL.md deleted while sibling files
remain) still resolves to an existing directory, so it is unaffected
and continues to be queued and flagged.')

 | 

Jul 14, 2026

 |
| 

[run-with-git-bash.cmd](https://github.com/bytedance/deer-flow/blob/main/scripts/run-with-git-bash.cmd 'run-with-git-bash.cmd')

 | 

[run-with-git-bash.cmd](https://github.com/bytedance/deer-flow/blob/main/scripts/run-with-git-bash.cmd 'run-with-git-bash.cmd')

 | 

[fix: use Git Bash for Windows local startup (](https://github.com/bytedance/deer-flow/commit/580920ef63929ad60bea835bf043483f314db0dc 'fix: use Git Bash for Windows local startup (#1551)

* fix: use Git Bash for Windows local startup

* Apply suggestions from code review

Co-authored-by: Copilot <175728472+Copilot@users.noreply.github.com>

* Apply suggestions from code review

Co-authored-by: Copilot <175728472+Copilot@users.noreply.github.com>

---------

Co-authored-by: Willem Jiang <willem.jiang@gmail.com>
Co-authored-by: Copilot <175728472+Copilot@users.noreply.github.com>') [#1551](https://github.com/bytedance/deer-flow/pull/1551) [)](https://github.com/bytedance/deer-flow/commit/580920ef63929ad60bea835bf043483f314db0dc 'fix: use Git Bash for Windows local startup (#1551)

* fix: use Git Bash for Windows local startup

* Apply suggestions from code review

Co-authored-by: Copilot <175728472+Copilot@users.noreply.github.com>

* Apply suggestions from code review

Co-authored-by: Copilot <175728472+Copilot@users.noreply.github.com>

---------

Co-authored-by: Willem Jiang <willem.jiang@gmail.com>
Co-authored-by: Copilot <175728472+Copilot@users.noreply.github.com>')

 | 

Mar 29, 2026

 |
| 

[sandbox\_memory\_profile.py](https://github.com/bytedance/deer-flow/blob/main/scripts/sandbox_memory_profile.py 'sandbox_memory_profile.py')

 | 

[sandbox\_memory\_profile.py](https://github.com/bytedance/deer-flow/blob/main/scripts/sandbox_memory_profile.py 'sandbox_memory_profile.py')

 | 

[chore: add sandbox memory profiling tools (](https://github.com/bytedance/deer-flow/commit/0d0968a3646e4cc0b5a80267375e153dcb61c129 'chore: add sandbox memory profiling tools (#3249)

* chore: add sandbox memory profiling tools

* chore: keep sandbox memory PR profiling-only

* Format sandbox memory profiling script') [#3249](https://github.com/bytedance/deer-flow/pull/3249) [)](https://github.com/bytedance/deer-flow/commit/0d0968a3646e4cc0b5a80267375e153dcb61c129 'chore: add sandbox memory profiling tools (#3249)

* chore: add sandbox memory profiling tools

* chore: keep sandbox memory PR profiling-only

* Format sandbox memory profiling script')

 | 

Jun 3, 2026

 |
| 

[scan\_changed\_blocking\_io.py](https://github.com/bytedance/deer-flow/blob/main/scripts/scan_changed_blocking_io.py 'scan_changed_blocking_io.py')

 | 

[scan\_changed\_blocking\_io.py](https://github.com/bytedance/deer-flow/blob/main/scripts/scan_changed_blocking_io.py 'scan_changed_blocking_io.py')

 | 

[chore(blocking-io): fail-loud repo-root resolution and shared detecto…](https://github.com/bytedance/deer-flow/commit/a838546a2b369d024c32d319d3445a5f4e9264a8 'chore(blocking-io): fail-loud repo-root resolution and shared detector CLI shim (#3512)

* chore(blocking-io): fail-loud repo-root resolution and shared detector CLI shim

The three detectors resolved REPO_ROOT with depth-indexed
Path(__file__).resolve().parents[4]. If a detector file ever moves to a
different directory depth, scan roots resolve under the wrong directory
and the detector reports zero findings with no error — a silent-zero
failure shape for a detection tool.

- Add support/detectors/repo_root.py: resolve the repo root by walking
 upward to the .git marker (checked with exists() so git worktrees,
 where .git is a file, also resolve), raising RuntimeError when no
 marker is found. All three detectors use it at import time, so a
 relocated detector fails loudly instead of scanning an empty tree.
- Extract scripts/_detector_cli.py from the three character-identical
 CLI shims; the sys.path computation lives in one place and raises
 when backend/tests cannot be found.
- tests/test_detector_repo_root.py pins: resolution from an unmarked
 location raises instead of returning an empty scan; all three
 detectors share the resolved root; each CLI shim delegates to its
 detector.

Testing: backend `make test` (4278 passed); smoke-ran
`make detect-blocking-io`, `make detect-thread-boundaries`, and
`scripts/scan_changed_blocking_io.py --base upstream/main`.

Closes #3510 (review follow-up to #3503).

* chore(blocking-io): declare detector modules import-only, drop script-mode residue

Adversarial review caught that blocking_io_static.py and
thread_boundaries.py kept shebangs and __main__ blocks but can no longer
run as plain scripts: the new `from support.detectors.repo_root import`
executes before anything puts backend/tests on sys.path, so direct
invocation dies with ModuleNotFoundError before argparse.

Direct execution was never a documented entry point (Makefile targets,
the scripts/ shims, the blocking-io-guard skill, and tests all go
through the support.detectors package), so converge on import-only
instead of re-adding per-module bootstrap: drop the shebangs and the now
unreachable __main__ blocks (plus the `import sys` they kept alive) and
state the supported entry points in each module docstring. The shim
delegation tests in test_detector_repo_root.py pin the supported CLI
paths.

Testing: backend `make test` (4278 passed); `make detect-blocking-io`
and `make detect-thread-boundaries` smoke-ran.')

 | 

Jun 12, 2026

 |
| 

[serve.sh](https://github.com/bytedance/deer-flow/blob/main/scripts/serve.sh 'serve.sh')

 | 

[serve.sh](https://github.com/bytedance/deer-flow/blob/main/scripts/serve.sh 'serve.sh')

 | 

[fix: align pnpm consumers with Corepack fallback (](https://github.com/bytedance/deer-flow/commit/4e449385516c03b6b279ced004ff0ada493d56ef 'fix: align pnpm consumers with Corepack fallback (#4405)

* fix: align pnpm consumers with Corepack fallback

* fix: run pnpm helper from frontend workspace

* fix: preserve Corepack resolution hint') [#4405](https://github.com/bytedance/deer-flow/pull/4405) [)](https://github.com/bytedance/deer-flow/commit/4e449385516c03b6b279ced004ff0ada493d56ef 'fix: align pnpm consumers with Corepack fallback (#4405)

* fix: align pnpm consumers with Corepack fallback

* fix: run pnpm helper from frontend workspace

* fix: preserve Corepack resolution hint')

 | 

Jul 29, 2026

 |
| 

[setup-sandbox.sh](https://github.com/bytedance/deer-flow/blob/main/scripts/setup-sandbox.sh 'setup-sandbox.sh')

 | 

[setup-sandbox.sh](https://github.com/bytedance/deer-flow/blob/main/scripts/setup-sandbox.sh 'setup-sandbox.sh')

 | 

[fix(sandbox): stop setup-sandbox from pre-pulling the stale :latest s…](https://github.com/bytedance/deer-flow/commit/857fb96269e7716807f7e961f3a83c3a08e8b33b 'fix(sandbox): stop setup-sandbox from pre-pulling the stale :latest sandbox image (#3983)

* fix(sandbox): stop setup-sandbox from pre-pulling the stale :latest image

scripts/setup-sandbox.sh's fallback (used whenever config.yaml has no
uncommented sandbox.image) pulled the volces mirror's :latest tag. We
confirmed in #3921/#3922 that this tag is frozen on the pre-1.9.3
all-in-one-sandbox digest (1.0.0.156), which lacks the /v1/bash/*
routes required-secrets skills need — so the one script whose entire
job is 'pre-pull a working sandbox image' was pre-pulling a known-broken
one. Pin the fallback to :1.11.0 instead.

Also update config.example.yaml's commented image: example and
'Recommended' line to the same version, so uncommenting the example
doesn't reproduce the same trap.

Out of scope on purpose: aio_sandbox_provider.py's DEFAULT_IMAGE
constant (the harness-level default for AioSandboxProvider itself)
is a separate, broader default-image decision already flagged to
maintainers in #3921 — this PR only fixes the pre-pull helper script.

Reported in #3914 (a real user deleted their stale local image, reran
make setup-sandbox, and got the same broken :latest image back).

* fix(sandbox): make setup-sandbox warn when the pull won't affect the runtime image

Self-review caught a real gap in the previous commit: AioSandboxProvider
resolves its image as `sandbox_config.image or DEFAULT_IMAGE`
(aio_sandbox_provider.py:214), and DEFAULT_IMAGE is deliberately left
untouched (still the frozen :latest, per #3921 — that's a maintainer
decision, not this PR's scope). So when config.yaml has no uncommented
sandbox.image, pre-pulling :1.11.0 alone creates a NEW inconsistency:
the script reports success pulling a modern image, but the sandbox
that actually starts still falls back to the broken :latest — silently
leaving the user's underlying required-secrets/bash.exec problem
unfixed, which is worse than the previous consistent-but-broken
behavior (pre-pull :latest, run :latest).

Make the unconfigured path loud about this instead of silent: print
the exact config.yaml snippet needed to make the pulled image actually
take effect.')

 | 

Jul 7, 2026

 |
| 

[setup\_wizard.py](https://github.com/bytedance/deer-flow/blob/main/scripts/setup_wizard.py 'setup_wizard.py')

 | 

[setup\_wizard.py](https://github.com/bytedance/deer-flow/blob/main/scripts/setup_wizard.py 'setup_wizard.py')

 | 

[feat(im): Add user-owned IM channel connections (](https://github.com/bytedance/deer-flow/commit/aa015462a7e9003c0f6973c66655cea25f9ba23f 'feat(im): Add user-owned IM channel connections (#3487)

* Add user-owned IM channel connections

* Fix dev startup and channel connect popup

* Use async channel connect flow

* Harden dev service daemon startup

* Support local IM channel connections

* Align IM connections with local channels

* Fix safe user id digest algorithm

* Address Copilot IM channel feedback

* Address IM channel review comments

* Support all integrated IM channel connections

* Format additional channel connection tests

* Keep unavailable channel connect buttons clickable

* Fix IM channel provider icons

* Add runtime setup for enabled IM channels

* Guard global shortcut key handling

* Keep configured IM channels editable

* Avoid password autofill for channel secrets

* Make channel threads visible to connection owners

* Persist IM runtime config locally

* Allow disconnecting runtime IM channels

* Route no-auth channel sessions to local user

* Use default user for auth-disabled local mode

* Show IM channel source on threads

* Prefill IM channel runtime config

* Reflect IM channel runtime health

* Ignore Feishu message read events

* Ignore Feishu non-content message events

* Let setup wizard enable IM channels

* Fix frontend formatting after merge

* Stabilize backend tests without local config

* Isolate channel runtime config tests

* Address channel connection review comments

* Use sha256 user buckets with legacy migration

* Ensure runtime IM channels are ready after restart

* Persist disconnected IM channel state

* Address channel connection review comments

* Address channel connection review findings

Frontend connect flow:
- Open the runtime-config dialog only when a provider still needs
 credentials; configured providers go straight to the connect flow, so
 the binding-code/deep-link path is reachable from the UI again.
- After saving credentials, continue into the connect flow when a user
 binding is still required (multi-user mode) instead of stopping at a
 "Connected" toast.
- Extract shared provider-state helpers to core/channels/provider-state
 and add unit + e2e coverage for the direct-connect and
 configure-then-connect paths.

Provider status semantics:
- Report connection_status from the user's newest connection row;
 with no binding it is not_connected, except in auth-disabled local
 mode where a configured running channel is effectively connected.

Concurrency and event-loop correctness:
- Offload ChannelRuntimeConfigStore construction and writes, channel
 service construction, and Slack connection replies to threads; add a
 tests/blocking_io/ anchor for the runtime-config handlers.
- Consume binding codes with a conditional UPDATE so a code can only be
 used once under concurrent workers; retry upsert_connection as an
 update when a concurrent insert wins the unique constraint.
- Serialize ensure_channel_ready per channel so concurrent provider
 polls cannot double-start a channel worker.

Config and migration hardening:
- Stop mutating the get_app_config()-cached Telegram provider config;
 the runtime store now owns the UI-entered bot username.
- Register channel_connections in STARTUP_ONLY_FIELDS with the
 standardized startup-only Field description.
- Match the legacy unsafe-id bucket by recomputing its exact SHA-1 name
 so another user's same-prefix bucket can never be migrated.
- Remove the unused Telegram process_webhook_update path and document
 src/core/channels in the frontend docs.

Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>

* Address PR review comments on authz scoping and channel runtime

Security (review feedback from ShenAC-SAC):
- Scope internal-token callers to the connection owner carried in
 X-DeerFlow-Owner-User-Id instead of bypassing owner checks outright,
 in both require_permission(owner_check=True) and the stateless run
 endpoints. Internal callers keep access to their own and
 shared/legacy threads, and may claim a default-owned channel thread
 for its real owner, but a leaked internal token no longer grants
 cross-user thread access.
- Require admin privileges for POST/DELETE /api/channels/{provider}/
 runtime-config: runtime credentials and channel workers are
 instance-wide shared state (same model as the MCP config API).
 Read-only provider listing stays available to all users.

Performance (review feedback from willem-bd):
- Skip the redundant thread channel-metadata PATCH after the first
 successful backfill per thread.
- Reuse the per-connection Slack WebClient until its token changes
 instead of constructing one per outbound message.
- Reconcile channel readiness for all providers concurrently in
 GET /api/channels/providers.

Also resolve the code-quality unused-import flag in the blocking-io
anchor by pre-importing the channel service via importlib.

Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>

* Fix prettier formatting in provider-state test

Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>

* Reconcile UI runtime channel config with config reload on restart

Main now reloads a channel's config.yaml entry on restart_channel()
(#3514, issue #3497). Adapt the user-owned connection flow to coexist:

- configure_channel() restarts with reload_config=False — the caller
 just supplied the authoritative config (browser-entered credentials
 that are never written to config.yaml), so a file reload must not
 clobber it with the stale on-disk entry.
- _load_channel_config() re-applies the UI runtime-store overlay used
 at startup, so an operator-triggered restart keeps browser-entered
 credentials for channels without a config.yaml entry and does not
 resurrect a channel disconnected from the UI.
- Offload the reload's disk IO (config.yaml + runtime store) with
 asyncio.to_thread, matching the blocking-IO policy on this branch.

Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>

---------

Co-authored-by: Claude Fable 5 <noreply@anthropic.com>') [#3487](https://github.com/bytedance/deer-flow/pull/3487) [)](https://github.com/bytedance/deer-flow/commit/aa015462a7e9003c0f6973c66655cea25f9ba23f 'feat(im): Add user-owned IM channel connections (#3487)

* Add user-owned IM channel connections

* Fix dev startup and channel connect popup

* Use async channel connect flow

* Harden dev service daemon startup

* Support local IM channel connections

* Align IM connections with local channels

* Fix safe user id digest algorithm

* Address Copilot IM channel feedback

* Address IM channel review comments

* Support all integrated IM channel connections

* Format additional channel connection tests

* Keep unavailable channel connect buttons clickable

* Fix IM channel provider icons

* Add runtime setup for enabled IM channels

* Guard global shortcut key handling

* Keep configured IM channels editable

* Avoid password autofill for channel secrets

* Make channel threads visible to connection owners

* Persist IM runtime config locally

* Allow disconnecting runtime IM channels

* Route no-auth channel sessions to local user

* Use default user for auth-disabled local mode

* Show IM channel source on threads

* Prefill IM channel runtime config

* Reflect IM channel runtime health

* Ignore Feishu message read events

* Ignore Feishu non-content message events

* Let setup wizard enable IM channels

* Fix frontend formatting after merge

* Stabilize backend tests without local config

* Isolate channel runtime config tests

* Address channel connection review comments

* Use sha256 user buckets with legacy migration

* Ensure runtime IM channels are ready after restart

* Persist disconnected IM channel state

* Address channel connection review comments

* Address channel connection review findings

Frontend connect flow:
- Open the runtime-config dialog only when a provider still needs
 credentials; configured providers go straight to the connect flow, so
 the binding-code/deep-link path is reachable from the UI again.
- After saving credentials, continue into the connect flow when a user
 binding is still required (multi-user mode) instead of stopping at a
 "Connected" toast.
- Extract shared provider-state helpers to core/channels/provider-state
 and add unit + e2e coverage for the direct-connect and
 configure-then-connect paths.

Provider status semantics:
- Report connection_status from the user's newest connection row;
 with no binding it is not_connected, except in auth-disabled local
 mode where a configured running channel is effectively connected.

Concurrency and event-loop correctness:
- Offload ChannelRuntimeConfigStore construction and writes, channel
 service construction, and Slack connection replies to threads; add a
 tests/blocking_io/ anchor for the runtime-config handlers.
- Consume binding codes with a conditional UPDATE so a code can only be
 used once under concurrent workers; retry upsert_connection as an
 update when a concurrent insert wins the unique constraint.
- Serialize ensure_channel_ready per channel so concurrent provider
 polls cannot double-start a channel worker.

Config and migration hardening:
- Stop mutating the get_app_config()-cached Telegram provider config;
 the runtime store now owns the UI-entered bot username.
- Register channel_connections in STARTUP_ONLY_FIELDS with the
 standardized startup-only Field description.
- Match the legacy unsafe-id bucket by recomputing its exact SHA-1 name
 so another user's same-prefix bucket can never be migrated.
- Remove the unused Telegram process_webhook_update path and document
 src/core/channels in the frontend docs.

Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>

* Address PR review comments on authz scoping and channel runtime

Security (review feedback from ShenAC-SAC):
- Scope internal-token callers to the connection owner carried in
 X-DeerFlow-Owner-User-Id instead of bypassing owner checks outright,
 in both require_permission(owner_check=True) and the stateless run
 endpoints. Internal callers keep access to their own and
 shared/legacy threads, and may claim a default-owned channel thread
 for its real owner, but a leaked internal token no longer grants
 cross-user thread access.
- Require admin privileges for POST/DELETE /api/channels/{provider}/
 runtime-config: runtime credentials and channel workers are
 instance-wide shared state (same model as the MCP config API).
 Read-only provider listing stays available to all users.

Performance (review feedback from willem-bd):
- Skip the redundant thread channel-metadata PATCH after the first
 successful backfill per thread.
- Reuse the per-connection Slack WebClient until its token changes
 instead of constructing one per outbound message.
- Reconcile channel readiness for all providers concurrently in
 GET /api/channels/providers.

Also resolve the code-quality unused-import flag in the blocking-io
anchor by pre-importing the channel service via importlib.

Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>

* Fix prettier formatting in provider-state test

Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>

* Reconcile UI runtime channel config with config reload on restart

Main now reloads a channel's config.yaml entry on restart_channel()
(#3514, issue #3497). Adapt the user-owned connection flow to coexist:

- configure_channel() restarts with reload_config=False — the caller
 just supplied the authoritative config (browser-entered credentials
 that are never written to config.yaml), so a file reload must not
 clobber it with the stale on-disk entry.
- _load_channel_config() re-applies the UI runtime-store overlay used
 at startup, so an operator-triggered restart keeps browser-entered
 credentials for channels without a config.yaml entry and does not
 resurrect a channel disconnected from the UI.
- Offload the reload's disk IO (config.yaml + runtime store) with
 asyncio.to_thread, matching the blocking-IO policy on this branch.

Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>

---------

Co-authored-by: Claude Fable 5 <noreply@anthropic.com>')

 | 

Jun 12, 2026

 |
| 

[start-daemon.sh](https://github.com/bytedance/deer-flow/blob/main/scripts/start-daemon.sh 'start-daemon.sh')

 | 

[start-daemon.sh](https://github.com/bytedance/deer-flow/blob/main/scripts/start-daemon.sh 'start-daemon.sh')

 | 

[feat: unified serve.sh with gateway mode support (](https://github.com/bytedance/deer-flow/commit/ca2fb95ee6bae08073ad058ecaecbf180c32a50c 'feat: unified serve.sh with gateway mode support (#1847)') [#1847](https://github.com/bytedance/deer-flow/pull/1847) [)](https://github.com/bytedance/deer-flow/commit/ca2fb95ee6bae08073ad058ecaecbf180c32a50c 'feat: unified serve.sh with gateway mode support (#1847)')

 | 

Apr 5, 2026

 |
| 

[support\_bundle.py](https://github.com/bytedance/deer-flow/blob/main/scripts/support_bundle.py 'support_bundle.py')

 | 

[support\_bundle.py](https://github.com/bytedance/deer-flow/blob/main/scripts/support_bundle.py 'support_bundle.py')

 | 

[fix(gateway):unify thread id validation (](https://github.com/bytedance/deer-flow/commit/095092418ccf072aa866c0a663c4056c206091e5 'fix(gateway):unify thread id validation (#4589)

* fix(gateway): unify thread ID validation at the API boundary

Thread ID entry points accepted arbitrary strings while downstream
consumers (filesystem paths, Kubernetes Provisioner, JSONL event store)
each enforced different character restrictions, so invalid IDs were
persisted first and only failed later during sandbox/workspace init.

Centralize validation in deerflow.utils.thread_id (pattern
^[A-Za-z0-9_-]{1,64}$): validate at routers, RunCreateRequest,
scheduler dispatch, paths.py, JSONL store, embedded client, and align
the Provisioner pattern (pinned by a parity test). UUIDs are still
generated only when no ID is supplied; caller-supplied opaque IDs stay
supported.

Deliberate exceptions: DELETE /threads/{id} keeps str as the legacy
cleanup escape hatch (filesystem cleanup guarded), read-only
client.get_thread stays unvalidated, and scheduler rows with legacy
invalid IDs record a failed dispatch instead of raising out of the
poll loop.

* docs: document canonical thread ID contract

README: caller-supplied thread IDs need not be UUIDs; the canonical
pattern and per-endpoint behavior. AGENTS.md: the shared
deerflow.utils.thread_id contract, its enforcement boundaries, and the
legacy-ID escape hatches.

* fix(gateway): close thread ID validation gaps at remaining entry points

Follow-up to the canonical thread ID contract: a full audit found the
uniform-422 coverage only reached about half of the thread_id surfaces.

- routers: 18 routes still took a bare thread_id: str — 13 in
 thread_runs.py (including the five messages/events/workspace-changes
 reads that returned 500 on the JSONL event store vs 404/empty on the
 DB store), 4 read routes in threads.py, and the suggestions route
 flagged in review. DELETE /api/threads/{id} keeps str as the declared
 legacy-cleanup escape hatch.
- client: upload_files/delete_upload/list_uploads/get_artifact now
 validate up front, fulfilling the RFC's 'all mutating entry points'
 clause (get_thread stays unvalidated as the declared legacy read path).
- tui: the /resume literal-ref fallback validates against the canonical
 contract and reports a descriptive error instead of failing deep in
 the client.
- scripts/support_bundle.py: replace the drifted dot-allowing pattern
 with a byte-identical copy of THREAD_ID_PATTERN (kept local so the
 script still runs with a broken venv).

* test(gateway): guard the canonical thread ID contract against regressions

- test_thread_id_route_contract.py: static AST sweep asserting every
 route handler with a thread_id parameter annotates ThreadId
 (whitelist: the DELETE escape hatch), plus a runtime sweep hitting
 all 44 thread_id routes with a non-canonical ID and asserting a 422
 that names thread_id, plus a websocket upgrade-rejection case.
- test_thread_id_validation.py: client entry-point validation,
 support_bundle pattern parity, and TUI literal-ref fallback tests.
- Align two tests that encoded the old contract (dotted IDs).') [#4589](https://github.com/bytedance/deer-flow/pull/4589) [)](https://github.com/bytedance/deer-flow/commit/095092418ccf072aa866c0a663c4056c206091e5 'fix(gateway):unify thread id validation (#4589)

* fix(gateway): unify thread ID validation at the API boundary

Thread ID entry points accepted arbitrary strings while downstream
consumers (filesystem paths, Kubernetes Provisioner, JSONL event store)
each enforced different character restrictions, so invalid IDs were
persisted first and only failed later during sandbox/workspace init.

Centralize validation in deerflow.utils.thread_id (pattern
^[A-Za-z0-9_-]{1,64}$): validate at routers, RunCreateRequest,
scheduler dispatch, paths.py, JSONL store, embedded client, and align
the Provisioner pattern (pinned by a parity test). UUIDs are still
generated only when no ID is supplied; caller-supplied opaque IDs stay
supported.

Deliberate exceptions: DELETE /threads/{id} keeps str as the legacy
cleanup escape hatch (filesystem cleanup guarded), read-only
client.get_thread stays unvalidated, and scheduler rows with legacy
invalid IDs record a failed dispatch instead of raising out of the
poll loop.

* docs: document canonical thread ID contract

README: caller-supplied thread IDs need not be UUIDs; the canonical
pattern and per-endpoint behavior. AGENTS.md: the shared
deerflow.utils.thread_id contract, its enforcement boundaries, and the
legacy-ID escape hatches.

* fix(gateway): close thread ID validation gaps at remaining entry points

Follow-up to the canonical thread ID contract: a full audit found the
uniform-422 coverage only reached about half of the thread_id surfaces.

- routers: 18 routes still took a bare thread_id: str — 13 in
 thread_runs.py (including the five messages/events/workspace-changes
 reads that returned 500 on the JSONL event store vs 404/empty on the
 DB store), 4 read routes in threads.py, and the suggestions route
 flagged in review. DELETE /api/threads/{id} keeps str as the declared
 legacy-cleanup escape hatch.
- client: upload_files/delete_upload/list_uploads/get_artifact now
 validate up front, fulfilling the RFC's 'all mutating entry points'
 clause (get_thread stays unvalidated as the declared legacy read path).
- tui: the /resume literal-ref fallback validates against the canonical
 contract and reports a descriptive error instead of failing deep in
 the client.
- scripts/support_bundle.py: replace the drifted dot-allowing pattern
 with a byte-identical copy of THREAD_ID_PATTERN (kept local so the
 script still runs with a broken venv).

* test(gateway): guard the canonical thread ID contract against regressions

- test_thread_id_route_contract.py: static AST sweep asserting every
 route handler with a thread_id parameter annotates ThreadId
 (whitelist: the DELETE escape hatch), plus a runtime sweep hitting
 all 44 thread_id routes with a non-canonical ID and asserting a 422
 that names thread_id, plus a websocket upgrade-rejection case.
- test_thread_id_validation.py: client entry-point validation,
 support_bundle pattern parity, and TUI literal-ref fallback tests.
- Align two tests that encoded the old contract (dotted IDs).')

 | 

Aug 1, 2026

 |
| 

[sync\_labels.py](https://github.com/bytedance/deer-flow/blob/main/scripts/sync_labels.py 'sync_labels.py')

 | 

[sync\_labels.py](https://github.com/bytedance/deer-flow/blob/main/scripts/sync_labels.py 'sync_labels.py')

 | 

[feat(ci): PR/issue auto-labeling + declarative label sync (](https://github.com/bytedance/deer-flow/commit/aca7acc105e544864c14874a8f570e5cef020e36 'feat(ci): PR/issue auto-labeling + declarative label sync (#3360)

- .github/labels.yml: declarative source of truth (29 namespaced labels)
- scripts/sync_labels.py + label-sync.yml: idempotent label sync (self-bootstraps on merge)
- labeler.yml + pr-labeler.yml: area:* labels by changed path (actions/labeler)
- pr-triage.yml: size/*, risk:*, needs-validation, first-time-contributor, reviewing
- issue-triage.yml: needs-triage on new issues (self-healing)

All PR workflows use pull_request_target but never check out or run PR code
(read changed-file metadata via the API only).') [#3360](https://github.com/bytedance/deer-flow/pull/3360) [)](https://github.com/bytedance/deer-flow/commit/aca7acc105e544864c14874a8f570e5cef020e36 'feat(ci): PR/issue auto-labeling + declarative label sync (#3360)

- .github/labels.yml: declarative source of truth (29 namespaced labels)
- scripts/sync_labels.py + label-sync.yml: idempotent label sync (self-bootstraps on merge)
- labeler.yml + pr-labeler.yml: area:* labels by changed path (actions/labeler)
- pr-triage.yml: size/*, risk:*, needs-validation, first-time-contributor, reviewing
- issue-triage.yml: needs-triage on new issues (self-healing)

All PR workflows use pull_request_target but never check out or run PR code
(read changed-file metadata via the API only).')

 | 

Jun 3, 2026

 |
| 

[tool-error-degradation-detection.sh](https://github.com/bytedance/deer-flow/blob/main/scripts/tool-error-degradation-detection.sh 'tool-error-degradation-detection.sh')

 | 

[tool-error-degradation-detection.sh](https://github.com/bytedance/deer-flow/blob/main/scripts/tool-error-degradation-detection.sh 'tool-error-degradation-detection.sh')

 | 

[refactor(lead-agent): make build\_middlewares public to drop the last …](https://github.com/bytedance/deer-flow/commit/0fb18e368c21d64bff48c4fc144aedac7a6743d8 'refactor(lead-agent): make build_middlewares public to drop the last cross-module private import (#3458)

`client.py` imported the private `_build_middlewares` from `agent.py` across a
module boundary and called it as public API. Because the `_` name signals
"module-private, no external callers", any future rename or signature change
silently breaks the embedded `DeerFlowClient` path — and the test suite even
monkeypatched `deerflow.client._build_middlewares`, baking the leak in.

`DeerFlowClient` is a lead-agent variant that genuinely needs the lead agent's
full middleware composition, so make the dependency honest: promote the helper
to a documented public entry point `build_middlewares` and update every in-repo
caller. Found during #3341 review; #3341 already removed one such leak
(`_assemble_deferred` -> public `assemble_deferred_tools`) and left this one out
of scope on purpose.

- agent.py: rename def + both internal call sites; expand the docstring into a
 public-entry-point contract and document the previously-undocumented
 model_name / app_config / deferred_setup params
- client.py: import + call site now use the public name (removes the last
 cross-module private import)
- scripts/tool-error-degradation-detection.sh: update its import + call site
- tests (5 files): update monkeypatch/patch targets and direct calls
- docs (backend/CLAUDE.md, plan_mode_usage.md, middlewares.mdx): sync the live
 references that describe the symbol as current API

Pure mechanical rename, no behavior change. Historical design docs (rfc,
superpowers spec) intentionally keep the old name as point-in-time records.

Closes #3431')

 | 

Jun 9, 2026

 |
| 

[verify\_versions.sh](https://github.com/bytedance/deer-flow/blob/main/scripts/verify_versions.sh 'verify_versions.sh')

 | 

[verify\_versions.sh](https://github.com/bytedance/deer-flow/blob/main/scripts/verify_versions.sh 'verify_versions.sh')

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

[wait-for-port.sh](https://github.com/bytedance/deer-flow/blob/main/scripts/wait-for-port.sh 'wait-for-port.sh')

 | 

[wait-for-port.sh](https://github.com/bytedance/deer-flow/blob/main/scripts/wait-for-port.sh 'wait-for-port.sh')

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

View all files

 |