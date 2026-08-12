# Source: https://github.com/bytedance/deer-flow/blob/main/docker/lark-cli-init/README.md

### Uh oh!

There was an error while loading. [Please reload this page]().

[bytedance](https://github.com/bytedance) / **[deer-flow](https://github.com/bytedance/deer-flow)** Public

- [Notifications](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow) You must be signed in to change notification settings
- [Fork 10.9k](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow)
- [Star 79.8k](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow)

 ## FilesExpand file tree

main

/

# README.md

Copy path

Blame

More file actions

Blame

More file actions

## Latest commit

[![icn5381](https://avatars.githubusercontent.com/u/255778606?v=4&size=40)](https://github.com/icn5381) [icn5381](https://github.com/bytedance/deer-flow/commits?author=icn5381)

[docs(lark): drop dead link to uncommitted sandbox init spec (](https://github.com/bytedance/deer-flow/commit/295d7c2abcf77e995951627afdd531791369b9d0) [#4705](https://github.com/bytedance/deer-flow/pull/4705) [)](https://github.com/bytedance/deer-flow/commit/295d7c2abcf77e995951627afdd531791369b9d0)

Open commit detailssuccess

Aug 8, 2026

[295d7c2](https://github.com/bytedance/deer-flow/commit/295d7c2abcf77e995951627afdd531791369b9d0) · Aug 8, 2026

## History

[History](https://github.com/bytedance/deer-flow/commits/main/docker/lark-cli-init/README.md)

Open commit details

History

66 lines (52 loc) · 2.88 KB

## FilesExpand file tree

main

/

# README.md

Copy path

Top

## File metadata and controls

- Preview

- Code

- Blame

66 lines (52 loc) · 2.88 KB

[Raw](https://github.com/bytedance/deer-flow/raw/refs/heads/main/docker/lark-cli-init/README.md)

Copy raw file

Download raw file

Outline

Edit and raw actions

# lark-cli init image (Pattern A)

This image provisions the sandbox `lark-cli` runtime binary into a Kubernetes sandbox Pod via an **init container + shared `emptyDir`**, instead of the Gateway downloading Linux binaries from GitHub at install time and mounting them via hostPath/PVC.

## What it does

- **Build time** (network available): downloads and SHA-256-verifies the official `larksuite/cli` Linux release binaries and stages the runtime layout under `/opt/lark-cli`:

    ```
    /opt/lark-cli/bin/lark-cli            # arch-dispatch launcher (uname -m)
    /opt/lark-cli/linux-amd64/lark-cli
    /opt/lark-cli/linux-arm64/lark-cli
    /opt/lark-cli/.deerflow-lark-cli-runtime.json   # {"version": "vX.Y.Z"}
    ```

 This is byte-identical to what the Gateway writer (`_write_lark_cli_sandbox_launcher`) produces and what `_validate_lark_cli_sandbox_runtime` enforces, so the sandbox PATH contract (`/mnt/integrations/lark-cli/runtime/bin/lark-cli`) is unchanged.

- **Run time**: copies `/opt/lark-cli/.` into the emptyDir mounted at `${LARK_CLI_RUNTIME_DEST}` (default `/mnt/integrations/lark-cli/runtime`) and exits `0`.

## Build

```shell
docker build -t deer-flow/lark-cli-init:v1.0.65 \
  --build-arg LARK_CLI_VERSION=v1.0.65 \
  docker/lark-cli-init
```

The tag should encode the lark-cli version so it can be bumped independently of the upstream `all-in-one-sandbox` sandbox image.

CI publishes multi-arch (`linux/amd64,linux/arm64`) images to `ghcr.io/<owner>/deer-flow-lark-cli-init:<lark-cli-version>` via `.github/workflows/lark-cli-images.yaml` (run it with a `lark_cli_version` input, or push a `lark-cli-v*` tag). This is decoupled from the DeerFlow `v*` release because the image tracks the upstream `larksuite/cli` version.

## Wiring it into the provisioner

The init-container runtime path is **opt-in** and off by default. Enable it by publishing this image and pointing the provisioner at it:

- Set `LARK_CLI_INIT_IMAGE` on the provisioner service to the published tag (e.g. `deer-flow/lark-cli-init:v1.0.65`). Empty ⇒ legacy hostPath / Gateway download path (no behavior change).
- When set, the provisioner adds a `lark-cli-runtime` `emptyDir` volume, an `lark-cli-init` init container, and a read-only runtime mount on the sandbox container — and ignores any `/mnt/integrations/lark-cli/runtime` hostPath/PVC extra mount (the init container supersedes it). The per-user `config` / `data` credential mounts are unchanged.
- The provisioner reports whether it is configured via `GET /api/capabilities` (`{"lark_cli_init_image": true|false}`), which the Gateway surfaces as the Lark integration sandbox-runtime readiness signal in `/api/integrations/lark/status`.

> Opt-in note: the init-container path stays off until `LARK_CLI_INIT_IMAGE` is set on the provisioner, so an unpublished or unconfigured image is a no-op (legacy hostPath / Gateway download path, no behavior change).