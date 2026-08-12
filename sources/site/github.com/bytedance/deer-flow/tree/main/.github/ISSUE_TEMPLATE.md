# Source: https://github.com/bytedance/deer-flow/tree/main/.github/ISSUE_TEMPLATE

### Uh oh!

There was an error while loading. [Please reload this page]().

[bytedance](https://github.com/bytedance) / **[deer-flow](https://github.com/bytedance/deer-flow)** Public

- [Notifications](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow) You must be signed in to change notification settings
- [Fork 10.9k](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow)
- [Star 79.8k](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow)

 ## FilesExpand file tree

main

/

# ISSUE\_TEMPLATE

/

Copy path

## Directory actions

## More options

More options

## Directory actions

## More options

More options

## Latest commit

[![18062706139fcz](https://avatars.githubusercontent.com/u/90562015?v=4&size=40)](https://github.com/18062706139fcz) [18062706139fcz](https://github.com/bytedance/deer-flow/commits?author=18062706139fcz)

[feat(scripts): add redacted community support bundle generator (](https://github.com/bytedance/deer-flow/commit/cf026464897ff42e25e278fe3daea3af5381b5e4) [#3886](https://github.com/bytedance/deer-flow/pull/3886) [)](https://github.com/bytedance/deer-flow/commit/cf026464897ff42e25e278fe3daea3af5381b5e4)

Open commit detailssuccess

Jul 1, 2026

[cf02646](https://github.com/bytedance/deer-flow/commit/cf026464897ff42e25e278fe3daea3af5381b5e4) · Jul 1, 2026

## History

[History](https://github.com/bytedance/deer-flow/commits/main/.github/ISSUE_TEMPLATE)

Open commit details

History

## FilesExpand file tree

main

/

# ISSUE\_TEMPLATE

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

[bug-report.yml](https://github.com/bytedance/deer-flow/blob/main/.github/ISSUE_TEMPLATE/bug-report.yml 'bug-report.yml')

 | 

[bug-report.yml](https://github.com/bytedance/deer-flow/blob/main/.github/ISSUE_TEMPLATE/bug-report.yml 'bug-report.yml')

 | 

[feat(scripts): add redacted community support bundle generator (](https://github.com/bytedance/deer-flow/commit/cf026464897ff42e25e278fe3daea3af5381b5e4 'feat(scripts): add redacted community support bundle generator (#3886)

* feat(scripts): add redacted community support bundle generator

Add `make support-bundle` (scripts/support_bundle.py) to help users file
high-signal, privacy-safe GitHub issues for local setup/config/runtime
problems.

The command produces:
- `*-issue-summary.md` to paste into the issue body
- `*-issue-draft.md` scaffold for AI-assisted filing (REQUIRED placeholders,
 never invents repro/expected/summary facts)
- an optional evidence zip under `.deer-flow/support-bundles/` containing a
 stable `triage.json` plus redacted environment/config/extensions/git/doctor
 evidence

Privacy: secrets are redacted across config values, URL userinfo, query
strings, CLI flags, custom headers, bearer/sk- tokens, and home paths. The
bundle never includes `.env`, raw conversation messages, or user file
contents; optional `--thread-id` adds file manifests only. `thread_id` input
is validated against path traversal.

Wire it into the Makefile, AGENTS.md, README/README_zh, CONTRIBUTING, and the
bug-report issue template. Covered by backend/tests/test_support_bundle.py.

* fix(scripts): redact MCP env values by default in support bundle

Address PR #3886 review (willem-bd, P2): the key-name allowlist let literal
secrets under non-standard env keys (e.g. SUPABASE_SERVICE_ROLE_KEY,
R2_ACCESS_KEY, hardcoded AIza… keys) leak verbatim into the bundle that users
are told is safe to share publicly.

Mask all MCP `env` values by default, keeping only `$VAR`/`${VAR}` references
visible, and broaden SECRET_KEY_RE (access_key, pwd, private_key). Add tests
for non-keyword env secrets, broadened key names, and end-to-end zip redaction.') [#3886](https://github.com/bytedance/deer-flow/pull/3886) [)](https://github.com/bytedance/deer-flow/commit/cf026464897ff42e25e278fe3daea3af5381b5e4 'feat(scripts): add redacted community support bundle generator (#3886)

* feat(scripts): add redacted community support bundle generator

Add `make support-bundle` (scripts/support_bundle.py) to help users file
high-signal, privacy-safe GitHub issues for local setup/config/runtime
problems.

The command produces:
- `*-issue-summary.md` to paste into the issue body
- `*-issue-draft.md` scaffold for AI-assisted filing (REQUIRED placeholders,
 never invents repro/expected/summary facts)
- an optional evidence zip under `.deer-flow/support-bundles/` containing a
 stable `triage.json` plus redacted environment/config/extensions/git/doctor
 evidence

Privacy: secrets are redacted across config values, URL userinfo, query
strings, CLI flags, custom headers, bearer/sk- tokens, and home paths. The
bundle never includes `.env`, raw conversation messages, or user file
contents; optional `--thread-id` adds file manifests only. `thread_id` input
is validated against path traversal.

Wire it into the Makefile, AGENTS.md, README/README_zh, CONTRIBUTING, and the
bug-report issue template. Covered by backend/tests/test_support_bundle.py.

* fix(scripts): redact MCP env values by default in support bundle

Address PR #3886 review (willem-bd, P2): the key-name allowlist let literal
secrets under non-standard env keys (e.g. SUPABASE_SERVICE_ROLE_KEY,
R2_ACCESS_KEY, hardcoded AIza… keys) leak verbatim into the bundle that users
are told is safe to share publicly.

Mask all MCP `env` values by default, keeping only `$VAR`/`${VAR}` references
visible, and broaden SECRET_KEY_RE (access_key, pwd, private_key). Add tests
for non-keyword env secrets, broadened key names, and end-to-end zip redaction.')

 | 

Jul 1, 2026

 |
| 

[config.yml](https://github.com/bytedance/deer-flow/blob/main/.github/ISSUE_TEMPLATE/config.yml 'config.yml')

 | 

[config.yml](https://github.com/bytedance/deer-flow/blob/main/.github/ISSUE_TEMPLATE/config.yml 'config.yml')

 | 

[feat(issue-templates): add structured bug & feature issue forms (](https://github.com/bytedance/deer-flow/commit/f97b0c0f745042a24d5f313326f0722fa0097103 'feat(issue-templates): add structured bug & feature issue forms (#3359)

Replace the single runtime-information form with:
- config.yml: disable blank issues, route Q&A/ideas to Discussions, link security policy
- bug-report.yml: reproducible bug form (folds in the old runtime/environment fields + affected-area picker)
- feature-request.yml: scoped proposal form

Uses only default labels (bug/enhancement) so it is self-contained.') [#3359](https://github.com/bytedance/deer-flow/pull/3359) [)](https://github.com/bytedance/deer-flow/commit/f97b0c0f745042a24d5f313326f0722fa0097103 'feat(issue-templates): add structured bug & feature issue forms (#3359)

Replace the single runtime-information form with:
- config.yml: disable blank issues, route Q&A/ideas to Discussions, link security policy
- bug-report.yml: reproducible bug form (folds in the old runtime/environment fields + affected-area picker)
- feature-request.yml: scoped proposal form

Uses only default labels (bug/enhancement) so it is self-contained.')

 | 

Jun 3, 2026

 |
| 

[feature-request.yml](https://github.com/bytedance/deer-flow/blob/main/.github/ISSUE_TEMPLATE/feature-request.yml 'feature-request.yml')

 | 

[feature-request.yml](https://github.com/bytedance/deer-flow/blob/main/.github/ISSUE_TEMPLATE/feature-request.yml 'feature-request.yml')

 | 

[feat(issue-templates): add structured bug & feature issue forms (](https://github.com/bytedance/deer-flow/commit/f97b0c0f745042a24d5f313326f0722fa0097103 'feat(issue-templates): add structured bug & feature issue forms (#3359)

Replace the single runtime-information form with:
- config.yml: disable blank issues, route Q&A/ideas to Discussions, link security policy
- bug-report.yml: reproducible bug form (folds in the old runtime/environment fields + affected-area picker)
- feature-request.yml: scoped proposal form

Uses only default labels (bug/enhancement) so it is self-contained.') [#3359](https://github.com/bytedance/deer-flow/pull/3359) [)](https://github.com/bytedance/deer-flow/commit/f97b0c0f745042a24d5f313326f0722fa0097103 'feat(issue-templates): add structured bug & feature issue forms (#3359)

Replace the single runtime-information form with:
- config.yml: disable blank issues, route Q&A/ideas to Discussions, link security policy
- bug-report.yml: reproducible bug form (folds in the old runtime/environment fields + affected-area picker)
- feature-request.yml: scoped proposal form

Uses only default labels (bug/enhancement) so it is self-contained.')

 | 

Jun 3, 2026

 |
| 

View all files

 |