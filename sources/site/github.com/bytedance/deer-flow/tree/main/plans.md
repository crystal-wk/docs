# Source: https://github.com/bytedance/deer-flow/tree/main/plans

### Uh oh!

There was an error while loading. [Please reload this page]().

[bytedance](https://github.com/bytedance) / **[deer-flow](https://github.com/bytedance/deer-flow)** Public

- [Notifications](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow) You must be signed in to change notification settings
- [Fork 10.9k](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow)
- [Star 79.8k](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow)

 ## FilesExpand file tree

main

/

# plans

/

Copy path

## Directory actions

## More options

More options

## Directory actions

## More options

More options

## Latest commit

[![ggnnggez](https://avatars.githubusercontent.com/u/88081804?v=4&size=40)](https://github.com/ggnnggez) [ggnnggez](https://github.com/bytedance/deer-flow/commits?author=ggnnggez)

[feat(subagents): show effective model and token usage on task cards (](https://github.com/bytedance/deer-flow/commit/aafd5077b25c4c34a405063257aa50cd596b09fe) [#…](https://github.com/bytedance/deer-flow/pull/4049)

Open commit detailssuccess

Jul 11, 2026

[aafd507](https://github.com/bytedance/deer-flow/commit/aafd5077b25c4c34a405063257aa50cd596b09fe) · Jul 11, 2026

## History

[History](https://github.com/bytedance/deer-flow/commits/main/plans)

Open commit details

History

## FilesExpand file tree

main

/

# plans

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

[subagent-card-runtime-metadata.md](https://github.com/bytedance/deer-flow/blob/main/plans/subagent-card-runtime-metadata.md 'subagent-card-runtime-metadata.md')

 | 

[subagent-card-runtime-metadata.md](https://github.com/bytedance/deer-flow/blob/main/plans/subagent-card-runtime-metadata.md 'subagent-card-runtime-metadata.md')

 | 

[feat(subagents): show effective model and token usage on task cards (](https://github.com/bytedance/deer-flow/commit/aafd5077b25c4c34a405063257aa50cd596b09fe 'feat(subagents): show effective model and token usage on task cards (#4049)

* feat(subagents): show runtime metadata on task cards

* fix(subagents): stop task-card render loop and dedupe model fetches

Address code review on the runtime-metadata cards:

- P1 render loop: the terminal ToolMessage is re-parsed on every
 MessageList render and always carries modelName/usage, so the
 presence-based setTasks condition fired a fresh state object each
 render -> "Maximum update depth exceeded". computeNextSubtask now
 returns a value-compared `changed` flag and a pure subtaskNotification()
 routes terminal transitions through the deferred after-render path
 while skipping no-op re-parses.

- Per-card useModels refetch: add staleTime: Infinity to the ["models"]
 query so every subtask card shares one /api/models fetch instead of
 refetching on each mount.

* make format

* refactor(subagents): dedupe token-usage validators + tidy event narrowing

Address PR review follow-ups:

- DRY: extract one shared token-usage validator per side. Backend
 status_contract.normalize_token_usage() now backs both the terminal
 ToolMessage metadata and the subagent.step/.end run events
 (step_events.py), and frontend messages/usage.normalizeTokenUsage()
 backs both the live task_running event (lifecycle.ts) and the terminal
 ToolMessage metadata (subtask-result.ts). Prevents the input/output/
 total_tokens validation from drifting across the four former copies.

- Nit: onCustomEvent narrows event.type once instead of re-checking the
 object shape per branch; the redundant task_started early-return
 (already validated by taskEventToSubtaskUpdate) is dropped.') [#…](https://github.com/bytedance/deer-flow/pull/4049)

 | 

Jul 11, 2026

 |
| 

View all files

 |