# Source: https://github.com/bytedance/deer-flow/blob/main/backend/docs/MEMORY_SETTINGS_REVIEW.md

### Uh oh!

There was an error while loading. [Please reload this page]().

[bytedance](https://github.com/bytedance) / **[deer-flow](https://github.com/bytedance/deer-flow)** Public

- [Notifications](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow) You must be signed in to change notification settings
- [Fork 10.9k](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow)
- [Star 79.8k](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow)

 ## FilesExpand file tree

main

/

# MEMORY\_SETTINGS\_REVIEW.md

Copy path

Blame

More file actions

Blame

More file actions

## Latest commit

![LittleChenLiya](https://avatars.githubusercontent.com/u/64821731?v=4&size=40)![WillemJiang](https://avatars.githubusercontent.com/u/219644?v=4&size=40)

[LittleChenLiya](https://github.com/bytedance/deer-flow/commits?author=LittleChenLiya)

and

[WillemJiang](https://github.com/bytedance/deer-flow/commits?author=WillemJiang)

[feat: support manual add and edit for memory facts (](https://github.com/bytedance/deer-flow/commit/fc7de7fffe3e9cd229d16dbfa4dd6a61251242ad) [#1538](https://github.com/bytedance/deer-flow/pull/1538) [)](https://github.com/bytedance/deer-flow/commit/fc7de7fffe3e9cd229d16dbfa4dd6a61251242ad)

Open commit detailssuccess

Mar 29, 2026

[fc7de7f](https://github.com/bytedance/deer-flow/commit/fc7de7fffe3e9cd229d16dbfa4dd6a61251242ad) · Mar 29, 2026

## History

[History](https://github.com/bytedance/deer-flow/commits/main/backend/docs/MEMORY_SETTINGS_REVIEW.md)

Open commit details

History

63 lines (44 loc) · 1.86 KB

## FilesExpand file tree

main

/

# MEMORY\_SETTINGS\_REVIEW.md

Copy path

Top

## File metadata and controls

- Preview

- Code

- Blame

63 lines (44 loc) · 1.86 KB

[Raw](https://github.com/bytedance/deer-flow/raw/refs/heads/main/backend/docs/MEMORY_SETTINGS_REVIEW.md)

Copy raw file

Download raw file

Outline

Edit and raw actions

# Memory Settings Review

Use this when reviewing the Memory Settings add/edit flow locally with the fewest possible manual steps.

## Quick Review

1. Start DeerFlow locally using any working development setup you already use.

 Examples:

    ```shell
    make dev
    ```

 or

    ```shell
    make docker-start
    ```

 If you already have DeerFlow running locally, you can reuse that existing setup.

2. Load the sample memory fixture.

    ```shell
    python scripts/load_memory_sample.py
    ```

3. Open `Settings > Memory`.

 Default local URLs:

 - App: `http://localhost:2026`
 - Local frontend-only fallback: `http://localhost:3000`

## Minimal Manual Test

1. Click `Add fact`.
2. Create a new fact with:
 - Content: `Reviewer-added memory fact`
 - Category: `testing`
 - Confidence: `0.88`
3. Confirm the new fact appears immediately and shows `Manual` as the source.
4. Edit the sample fact `This sample fact is intended for edit testing.` and change it to:
 - Content: `This sample fact was edited during manual review.`
 - Category: `testing`
 - Confidence: `0.91`
5. Confirm the edited fact updates immediately.
6. Refresh the page and confirm both the newly added fact and the edited fact still persist.

## Optional Sanity Checks

- Search `Reviewer-added` and confirm the new fact is matched.
- Search `workflow` and confirm category text is searchable.
- Switch between `All`, `Facts`, and `Summaries`.
- Delete the disposable sample fact `Delete fact testing can target this disposable sample entry.` and confirm the list updates immediately.
- Clear all memory and confirm the page enters the empty state.

## Fixture Files

- Sample fixture: `backend/docs/memory-settings-sample.json`
- Default local runtime target: `backend/.deer-flow/memory.json`

The loader script creates a timestamped backup automatically before overwriting an existing runtime memory file.