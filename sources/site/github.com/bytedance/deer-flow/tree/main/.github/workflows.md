# Source: https://github.com/bytedance/deer-flow/tree/main/.github/workflows

### Uh oh!

There was an error while loading. [Please reload this page]().

[bytedance](https://github.com/bytedance) / **[deer-flow](https://github.com/bytedance/deer-flow)** Public

- [Notifications](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow) You must be signed in to change notification settings
- [Fork 10.9k](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow)
- [Star 79.8k](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow)

 ## FilesExpand file tree

main

/

# workflows

/

Copy path

## Directory actions

## More options

More options

## Directory actions

## More options

More options

## Latest commit

[![MiaoRuidx](https://avatars.githubusercontent.com/u/12540796?v=4&size=40)](https://github.com/MiaoRuidx) [MiaoRuidx](https://github.com/bytedance/deer-flow/commits?author=MiaoRuidx)

[fix(sandbox): enforce deployment-wide E2B capacity (](https://github.com/bytedance/deer-flow/commit/0cc28d2c4225752bc4808bf160f0a635d0214e5e) [#4575](https://github.com/bytedance/deer-flow/pull/4575) [)](https://github.com/bytedance/deer-flow/commit/0cc28d2c4225752bc4808bf160f0a635d0214e5e)

Open commit detailssuccess

Jul 31, 2026

[0cc28d2](https://github.com/bytedance/deer-flow/commit/0cc28d2c4225752bc4808bf160f0a635d0214e5e) · Jul 31, 2026

## History

[History](https://github.com/bytedance/deer-flow/commits/main/.github/workflows)

Open commit details

History

## FilesExpand file tree

main

/

# workflows

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

[..](https://github.com/bytedance/deer-flow/tree/main/.github) |
| 

[backend-blocking-io-tests.yml](https://github.com/bytedance/deer-flow/blob/main/.github/workflows/backend-blocking-io-tests.yml 'backend-blocking-io-tests.yml')

 | 

[backend-blocking-io-tests.yml](https://github.com/bytedance/deer-flow/blob/main/.github/workflows/backend-blocking-io-tests.yml 'backend-blocking-io-tests.yml')

 | 

[fix(ci): added 2.0.x-dev into CI workflow monitor (](https://github.com/bytedance/deer-flow/commit/7a407fe122a7d5560532ea42d600d15a2cc8bf06 'fix(ci): added 2.0.x-dev into CI workflow monitor (#3668)') [#3668](https://github.com/bytedance/deer-flow/pull/3668) [)](https://github.com/bytedance/deer-flow/commit/7a407fe122a7d5560532ea42d600d15a2cc8bf06 'fix(ci): added 2.0.x-dev into CI workflow monitor (#3668)')

 | 

Jun 20, 2026

 |
| 

[backend-unit-tests.yml](https://github.com/bytedance/deer-flow/blob/main/.github/workflows/backend-unit-tests.yml 'backend-unit-tests.yml')

 | 

[backend-unit-tests.yml](https://github.com/bytedance/deer-flow/blob/main/.github/workflows/backend-unit-tests.yml 'backend-unit-tests.yml')

 | 

[fix(sandbox): enforce deployment-wide E2B capacity (](https://github.com/bytedance/deer-flow/commit/0cc28d2c4225752bc4808bf160f0a635d0214e5e 'fix(sandbox): enforce deployment-wide E2B capacity (#4575)

* docs: design deployment-wide E2B capacity

* fix(sandbox): enforce deployment-wide E2B capacity

* fix(sandbox): address E2B capacity review findings

* fix(sandbox): grace stale E2B capacity inventory

---------

Co-authored-by: MiaoRuidx <12540796+MiaoRuidx@users.noreply.github.com>') [#4575](https://github.com/bytedance/deer-flow/pull/4575) [)](https://github.com/bytedance/deer-flow/commit/0cc28d2c4225752bc4808bf160f0a635d0214e5e 'fix(sandbox): enforce deployment-wide E2B capacity (#4575)

* docs: design deployment-wide E2B capacity

* fix(sandbox): enforce deployment-wide E2B capacity

* fix(sandbox): address E2B capacity review findings

* fix(sandbox): grace stale E2B capacity inventory

---------

Co-authored-by: MiaoRuidx <12540796+MiaoRuidx@users.noreply.github.com>')

 | 

Jul 31, 2026

 |
| 

[chart.yaml](https://github.com/bytedance/deer-flow/blob/main/.github/workflows/chart.yaml 'chart.yaml')

 | 

[chart.yaml](https://github.com/bytedance/deer-flow/blob/main/.github/workflows/chart.yaml 'chart.yaml')

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

[container.yaml](https://github.com/bytedance/deer-flow/blob/main/.github/workflows/container.yaml 'container.yaml')

 | 

[container.yaml](https://github.com/bytedance/deer-flow/blob/main/.github/workflows/container.yaml 'container.yaml')

 | 

[ci(containers): bake postgres extra into published backend image (](https://github.com/bytedance/deer-flow/commit/790b13fe1978ec4516c2e265dc0c5c3bb69e91a7 'ci(containers): bake postgres extra into published backend image (#4015)

The tag-publish workflow (container.yaml) built backend/Dockerfile with no
build-args, so UV_EXTRAS was empty and the published *-backend image shipped
without the Postgres driver (only --extra redis). Multi-replica deployments
(K8s/Helm) that need shared Postgres persistence instead of file-based SQLite
could not use the release image without rebuilding it.

Pass UV_EXTRAS=postgres so the release image includes
deerflow-harness[postgres]. Additive only: single-replica sqlite/redis setups
keep working; the Postgres driver is added, mirroring how redis is already
always baked in.') [#4015](https://github.com/bytedance/deer-flow/pull/4015) [)](https://github.com/bytedance/deer-flow/commit/790b13fe1978ec4516c2e265dc0c5c3bb69e91a7 'ci(containers): bake postgres extra into published backend image (#4015)

The tag-publish workflow (container.yaml) built backend/Dockerfile with no
build-args, so UV_EXTRAS was empty and the published *-backend image shipped
without the Postgres driver (only --extra redis). Multi-replica deployments
(K8s/Helm) that need shared Postgres persistence instead of file-based SQLite
could not use the release image without rebuilding it.

Pass UV_EXTRAS=postgres so the release image includes
deerflow-harness[postgres]. Additive only: single-replica sqlite/redis setups
keep working; the Postgres driver is added, mirroring how redis is already
always baked in.')

 | 

Jul 9, 2026

 |
| 

[e2e-tests.yml](https://github.com/bytedance/deer-flow/blob/main/.github/workflows/e2e-tests.yml 'e2e-tests.yml')

 | 

[e2e-tests.yml](https://github.com/bytedance/deer-flow/blob/main/.github/workflows/e2e-tests.yml 'e2e-tests.yml')

 | 

[fix(auth): recover from setup status timeouts (](https://github.com/bytedance/deer-flow/commit/f881996e1abb2ce04ad451e6abfaa3a1d5721c24 'fix(auth): recover from setup status timeouts (#4371)

* fix(auth): recover from setup status timeouts

* test(auth): cover setup status recovery flows

---------

Co-authored-by: Willem Jiang <willem.jiang@gmail.com>') [#4371](https://github.com/bytedance/deer-flow/pull/4371) [)](https://github.com/bytedance/deer-flow/commit/f881996e1abb2ce04ad451e6abfaa3a1d5721c24 'fix(auth): recover from setup status timeouts (#4371)

* fix(auth): recover from setup status timeouts

* test(auth): cover setup status recovery flows

---------

Co-authored-by: Willem Jiang <willem.jiang@gmail.com>')

 | 

Jul 26, 2026

 |
| 

[frontend-unit-tests.yml](https://github.com/bytedance/deer-flow/blob/main/.github/workflows/frontend-unit-tests.yml 'frontend-unit-tests.yml')

 | 

[frontend-unit-tests.yml](https://github.com/bytedance/deer-flow/blob/main/.github/workflows/frontend-unit-tests.yml 'frontend-unit-tests.yml')

 | 

[fix(ci): added 2.0.x-dev into CI workflow monitor (](https://github.com/bytedance/deer-flow/commit/7a407fe122a7d5560532ea42d600d15a2cc8bf06 'fix(ci): added 2.0.x-dev into CI workflow monitor (#3668)') [#3668](https://github.com/bytedance/deer-flow/pull/3668) [)](https://github.com/bytedance/deer-flow/commit/7a407fe122a7d5560532ea42d600d15a2cc8bf06 'fix(ci): added 2.0.x-dev into CI workflow monitor (#3668)')

 | 

Jun 20, 2026

 |
| 

[label-sync.yml](https://github.com/bytedance/deer-flow/blob/main/.github/workflows/label-sync.yml 'label-sync.yml')

 | 

[label-sync.yml](https://github.com/bytedance/deer-flow/blob/main/.github/workflows/label-sync.yml 'label-sync.yml')

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

[lark-cli-images.yaml](https://github.com/bytedance/deer-flow/blob/main/.github/workflows/lark-cli-images.yaml 'lark-cli-images.yaml')

 | 

[lark-cli-images.yaml](https://github.com/bytedance/deer-flow/blob/main/.github/workflows/lark-cli-images.yaml 'lark-cli-images.yaml')

 | 

[ci(lark): publish lark-cli-init/broker images (](https://github.com/bytedance/deer-flow/commit/1b5220e35e7a120131b6abbbbd336acf2385837b 'ci(lark): publish lark-cli-init/broker images (#4558)

* ci(lark): publish lark-cli-init/broker images (#4532)

Add .github/workflows/lark-cli-images.yaml to build and push the two
optional Lark sandbox runtime images (Pattern A init container and
Pattern B broker sidecar) to GHCR.

These track the upstream larksuite/cli version, not the DeerFlow v*
release, so the workflow is decoupled from container.yaml / the
verify-versions gate:

- Trigger via workflow_dispatch (lark_cli_version input) or a lark-cli-v*
 tag (version read from after the prefix).
- Multi-arch linux/amd64,linux/arm64 (the images stage a real
 arch-dispatched lark-cli binary), via QEMU + Buildx.
- Per-component build context: lark-cli-init builds from its own dir
 (relative COPY), lark-cli-broker from the repo root (it copies the
 shared build-runtime.sh + the harness lark_broker.py).
- Tagged by lark-cli version; no latest; gated on the upstream repo.

Docs: document the independent publishing in RELEASING.md and both image
READMEs, replacing the "publishing is a fast-follow" notes.

Closes #4532

* fix(ci): scope broker build context past root .dockerignore

The repo-root .dockerignore excludes the whole `docker/` tree, but the
lark-cli-broker image builds from a repo-root context and must COPY
`docker/lark-cli-init/build-runtime.sh` and
`docker/lark-cli-broker/entrypoint.sh` (plus the harness lark_broker.py).
Under root .dockerignore those COPYs fail (excluded from context).

Add docker/lark-cli-broker/Dockerfile.dockerignore: BuildKit uses this
per-Dockerfile ignore-file instead of the root one for `-f
docker/lark-cli-broker/Dockerfile` builds, keeping `docker/` and
`backend/` in context while still dropping .git/venv/frontend/docs noise.

lark-cli-init is unaffected (it builds from its own dir context).

* fix(ci): harden lark-cli version input against shell injection

Address PR #4558 review: pass the workflow_dispatch input through an env
var instead of interpolating ${{ inputs.lark_cli_version }} directly into
the run: script, so a dispatched value can't be expression-injected into
the runner shell if the repo gate ever widens. Also fix the multi-arch
comment verb (stage -> ships).') [#4558](https://github.com/bytedance/deer-flow/pull/4558) [)](https://github.com/bytedance/deer-flow/commit/1b5220e35e7a120131b6abbbbd336acf2385837b 'ci(lark): publish lark-cli-init/broker images (#4558)

* ci(lark): publish lark-cli-init/broker images (#4532)

Add .github/workflows/lark-cli-images.yaml to build and push the two
optional Lark sandbox runtime images (Pattern A init container and
Pattern B broker sidecar) to GHCR.

These track the upstream larksuite/cli version, not the DeerFlow v*
release, so the workflow is decoupled from container.yaml / the
verify-versions gate:

- Trigger via workflow_dispatch (lark_cli_version input) or a lark-cli-v*
 tag (version read from after the prefix).
- Multi-arch linux/amd64,linux/arm64 (the images stage a real
 arch-dispatched lark-cli binary), via QEMU + Buildx.
- Per-component build context: lark-cli-init builds from its own dir
 (relative COPY), lark-cli-broker from the repo root (it copies the
 shared build-runtime.sh + the harness lark_broker.py).
- Tagged by lark-cli version; no latest; gated on the upstream repo.

Docs: document the independent publishing in RELEASING.md and both image
READMEs, replacing the "publishing is a fast-follow" notes.

Closes #4532

* fix(ci): scope broker build context past root .dockerignore

The repo-root .dockerignore excludes the whole `docker/` tree, but the
lark-cli-broker image builds from a repo-root context and must COPY
`docker/lark-cli-init/build-runtime.sh` and
`docker/lark-cli-broker/entrypoint.sh` (plus the harness lark_broker.py).
Under root .dockerignore those COPYs fail (excluded from context).

Add docker/lark-cli-broker/Dockerfile.dockerignore: BuildKit uses this
per-Dockerfile ignore-file instead of the root one for `-f
docker/lark-cli-broker/Dockerfile` builds, keeping `docker/` and
`backend/` in context while still dropping .git/venv/frontend/docs noise.

lark-cli-init is unaffected (it builds from its own dir context).

* fix(ci): harden lark-cli version input against shell injection

Address PR #4558 review: pass the workflow_dispatch input through an env
var instead of interpolating ${{ inputs.lark_cli_version }} directly into
the run: script, so a dispatched value can't be expression-injected into
the runner shell if the repo gate ever widens. Also fix the multi-arch
comment verb (stage -> ships).')

 | 

Jul 29, 2026

 |
| 

[lint-check.yml](https://github.com/bytedance/deer-flow/blob/main/.github/workflows/lint-check.yml 'lint-check.yml')

 | 

[lint-check.yml](https://github.com/bytedance/deer-flow/blob/main/.github/workflows/lint-check.yml 'lint-check.yml')

 | 

[chore(ci): enforce uv.lock is in sync (](https://github.com/bytedance/deer-flow/commit/5b61214f7bf5a4365a342c57b59539e5c9bd8ed9 'chore(ci): enforce uv.lock is in sync (#3679)

Add a uv lock --check guard in two places so a stale uv.lock cannot be
committed unnoticed (as happened with the groundroute extra):

- pre-commit: a local uv-lock-check hook, scoped to the backend
 pyproject.toml files and uv.lock.
- CI: a "Check uv.lock is in sync" step in the lint-backend job, run
 before uv sync so the install step cannot mask a stale lock by
 regenerating it.') [#3679](https://github.com/bytedance/deer-flow/pull/3679) [)](https://github.com/bytedance/deer-flow/commit/5b61214f7bf5a4365a342c57b59539e5c9bd8ed9 'chore(ci): enforce uv.lock is in sync (#3679)

Add a uv lock --check guard in two places so a stale uv.lock cannot be
committed unnoticed (as happened with the groundroute extra):

- pre-commit: a local uv-lock-check hook, scoped to the backend
 pyproject.toml files and uv.lock.
- CI: a "Check uv.lock is in sync" step in the lint-backend job, run
 before uv sync so the install step cannot mask a stale lock by
 regenerating it.')

 | 

Jun 21, 2026

 |
| 

[nightly.yaml](https://github.com/bytedance/deer-flow/blob/main/.github/workflows/nightly.yaml 'nightly.yaml')

 | 

[nightly.yaml](https://github.com/bytedance/deer-flow/blob/main/.github/workflows/nightly.yaml 'nightly.yaml')

 | 

[ci(helm): publish chart to charts/ namespace prefix on GHCR (](https://github.com/bytedance/deer-flow/commit/f3e4e5f8f09773cd2364c971ddf5034675dd1494 'ci(helm): publish chart to charts/ namespace prefix on GHCR (#4175)

* ci(helm): publish chart to charts/ namespace prefix on GHCR

Push the Helm chart to ghcr.io/<owner>/charts/deer-flow (via a `charts/`
prefix on the `helm push` target) instead of the bare `deer-flow`
package. This namespaces the chart apart from the image packages
(deer-flow-{backend,frontend,provisioner}) without renaming the chart:
Chart.yaml `name` stays `deer-flow`, so dir = chart name = in-cluster
resource/selector names, and no `nameOverride` hack is needed.

The chart is new in 2.1.0 (chart infra landed in #3987, after v2.0.0),
so 2.1.0 is the first chart release. Early nightly builds remain at the
legacy non-prefixed ghcr.io/<owner>/deer-flow.

Also refresh chart release docs:
- Replace the removed scripts/build-and-push.sh in the chart README with
 raw `docker build`/`push` commands (contexts/args match container.yaml).
- Point NOTES.txt's empty-registry warning at the README section instead
 of the removed script.
- Retarget RELEASING.md version examples from 2.2.0 to 2.1.0.
- Bump the chart README's helm prerequisite to 3+.

* docs(helm): require helm 3.8+ and note legacy chart package cleanup

Address PR #4175 review:
- bump documented minimum to helm 3.8 (OCI registry support stabilized
 there; earlier 3.x needs HELM_EXPERIMENTAL_OCI=1)
- add a post-release note to delete/revoke the legacy bare
 ghcr.io/<owner>/deer-flow chart package after 2.1.0') [#4175](https://github.com/bytedance/deer-flow/pull/4175) [)](https://github.com/bytedance/deer-flow/commit/f3e4e5f8f09773cd2364c971ddf5034675dd1494 'ci(helm): publish chart to charts/ namespace prefix on GHCR (#4175)

* ci(helm): publish chart to charts/ namespace prefix on GHCR

Push the Helm chart to ghcr.io/<owner>/charts/deer-flow (via a `charts/`
prefix on the `helm push` target) instead of the bare `deer-flow`
package. This namespaces the chart apart from the image packages
(deer-flow-{backend,frontend,provisioner}) without renaming the chart:
Chart.yaml `name` stays `deer-flow`, so dir = chart name = in-cluster
resource/selector names, and no `nameOverride` hack is needed.

The chart is new in 2.1.0 (chart infra landed in #3987, after v2.0.0),
so 2.1.0 is the first chart release. Early nightly builds remain at the
legacy non-prefixed ghcr.io/<owner>/deer-flow.

Also refresh chart release docs:
- Replace the removed scripts/build-and-push.sh in the chart README with
 raw `docker build`/`push` commands (contexts/args match container.yaml).
- Point NOTES.txt's empty-registry warning at the README section instead
 of the removed script.
- Retarget RELEASING.md version examples from 2.2.0 to 2.1.0.
- Bump the chart README's helm prerequisite to 3+.

* docs(helm): require helm 3.8+ and note legacy chart package cleanup

Address PR #4175 review:
- bump documented minimum to helm 3.8 (OCI registry support stabilized
 there; earlier 3.x needs HELM_EXPERIMENTAL_OCI=1)
- add a post-release note to delete/revoke the legacy bare
 ghcr.io/<owner>/deer-flow chart package after 2.1.0')

 | 

Jul 15, 2026

 |
| 

[replay-e2e.yml](https://github.com/bytedance/deer-flow/blob/main/.github/workflows/replay-e2e.yml 'replay-e2e.yml')

 | 

[replay-e2e.yml](https://github.com/bytedance/deer-flow/blob/main/.github/workflows/replay-e2e.yml 'replay-e2e.yml')

 | 

[fix(ci): added 2.0.x-dev into CI workflow monitor (](https://github.com/bytedance/deer-flow/commit/7a407fe122a7d5560532ea42d600d15a2cc8bf06 'fix(ci): added 2.0.x-dev into CI workflow monitor (#3668)') [#3668](https://github.com/bytedance/deer-flow/pull/3668) [)](https://github.com/bytedance/deer-flow/commit/7a407fe122a7d5560532ea42d600d15a2cc8bf06 'fix(ci): added 2.0.x-dev into CI workflow monitor (#3668)')

 | 

Jun 20, 2026

 |
| 

[skill-review-ci.yml](https://github.com/bytedance/deer-flow/blob/main/.github/workflows/skill-review-ci.yml 'skill-review-ci.yml')

 | 

[skill-review-ci.yml](https://github.com/bytedance/deer-flow/blob/main/.github/workflows/skill-review-ci.yml 'skill-review-ci.yml')

 | 

[feat(skills): add skill review quality gate (](https://github.com/bytedance/deer-flow/commit/41658c5ff40f3f1a8a3bffcb8bc58a39117d44e2 'feat(skills): add skill review quality gate (#4037)

* feat(skills): add skill review quality gate

* fix(skills): skip review eval fixtures in CI

* fix(skills): ignore review eval fixtures in bundled scans

* fix(skill-review): harden review gate boundaries

* fix(skills): address skill review gate feedback') [#4037](https://github.com/bytedance/deer-flow/pull/4037) [)](https://github.com/bytedance/deer-flow/commit/41658c5ff40f3f1a8a3bffcb8bc58a39117d44e2 'feat(skills): add skill review quality gate (#4037)

* feat(skills): add skill review quality gate

* fix(skills): skip review eval fixtures in CI

* fix(skills): ignore review eval fixtures in bundled scans

* fix(skill-review): harden review gate boundaries

* fix(skills): address skill review gate feedback')

 | 

Jul 11, 2026

 |
| 

[triage.yml](https://github.com/bytedance/deer-flow/blob/main/.github/workflows/triage.yml 'triage.yml')

 | 

[triage.yml](https://github.com/bytedance/deer-flow/blob/main/.github/workflows/triage.yml 'triage.yml')

 | 

[fix(ci): consolidate PR/issue labeling and fix reviewing-job crash + …](https://github.com/bytedance/deer-flow/commit/90e23bfd090b5608625f610219042de8394b3afa 'fix(ci): consolidate PR/issue labeling and fix reviewing-job crash + label thrash (#3455)

* fix(ci): consolidate PR/issue labeling into one triage.yml; fix reviewing crash & label thrash

- Replace pr-labeler + pr-triage + issue-triage with a single triage.yml; drop actions/labeler.
 Its sync-labels removed labels outside its config (clobbered size/risk/needs-validation and
 could clobber maintainer labels). Area is now computed in-script and reconciled only within
 owned namespaces (area:/size//risk:/needs-validation); first-time/reviewing are add-only.
- reviewing: gate on author_association in {OWNER,MEMBER,COLLABORATOR} + user.type==='User'
 instead of getCollaboratorPermissionLevel, which 404'd on bot reviewers ('Copilot is not a
 user') and crashed the job. Excludes all review bots with no denylist and no API call.
- Read live state (listFiles + listLabelsOnIssue) not the stale event payload, so rapid
 synchronize events converge instead of thrashing. Size churn excludes lockfiles/snapshots.

* fix(ci): read labels live via paginate in reviewing & issue-triage jobs

Address review feedback on #3455:
- reviewing: listLabelsOnIssue now paginates (per_page:100) instead of the
 default 30, matching pr-labels, so a 'reviewing' label is never missed on
 PRs with many labels.
- issue-triage: read live labels via the API instead of the event payload,
 consistent with the live-state reads documented in the header.')

 | 

Jun 9, 2026

 |
| 

[verify-versions.yml](https://github.com/bytedance/deer-flow/blob/main/.github/workflows/verify-versions.yml 'verify-versions.yml')

 | 

[verify-versions.yml](https://github.com/bytedance/deer-flow/blob/main/.github/workflows/verify-versions.yml 'verify-versions.yml')

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

View all files

 |