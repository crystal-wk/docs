# Source: https://github.com/bytedance/deer-flow/commits?author=MiaoRuidx

### Uh oh!

There was an error while loading. [Please reload this page]().

[bytedance](https://github.com/bytedance) / **[deer-flow](https://github.com/bytedance/deer-flow)** Public

- [Notifications](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow) You must be signed in to change notification settings
- [Fork 10.9k](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow)
- [Star 79.8k](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow)

 ## Branch selector

main

## User selector

![](https://avatars.githubusercontent.com/u/12540796?v=4&size=32)

MiaoRuidx

## Datepicker

All time

## Commit history

### Commits on Jul 31, 2026

- #### [fix(sandbox): enforce deployment-wide E2B capacity (](https://github.com/bytedance/deer-flow/commit/0cc28d2c4225752bc4808bf160f0a635d0214e5e 'fix(sandbox): enforce deployment-wide E2B capacity (#4575)

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

 Show description for 0cc28d2

 [![MiaoRuidx](https://avatars.githubusercontent.com/u/12540796?v=4&size=32)](https://github.com/MiaoRuidx) [MiaoRuidx](https://github.com/bytedance/deer-flow/commits?author=MiaoRuidx)

 authoredJul 31, 2026

 ·

 10 / 10

 Verified

 [0cc28d2](https://github.com/bytedance/deer-flow/commit/0cc28d2c4225752bc4808bf160f0a635d0214e5e)View commit details

 Copy full SHA for 0cc28d2

 Browse repository at this point

### Commits on Jul 28, 2026

- #### [fix(runtime): cancel runs across live gateway workers (](https://github.com/bytedance/deer-flow/commit/8a78c264b7697b552ec748044a161692e95d01c9 'fix(runtime): cancel runs across live gateway workers (#4500)

 * docs(runtime): design cross-worker cancellation

 * fix(runtime): cancel runs across gateway workers

 * fix(runtime): harden cross-worker cancellation races

 让取消请求与 owner 终态写入通过持久化 CAS 决定先后，保证首次取消 action 在不同 worker 路由下保持一致。\n\n将 heartbeat 收敛为续租后仅发送本地中止信号，并补齐完成竞态与路由重试的回归用例。

 * docs(runtime): drop implementation plan from PR

 移除仅用于实现过程的跨 worker 取消设计记录，保留 README 和 backend/AGENTS.md 中面向最终行为的文档。

 * fix(runtime): preserve local cancel fallback

 * test(runtime): adapt worker run manager fakes

 * docs(runtime): fix run cancel migration registry

 ---------

 Co-authored-by: MiaoRuidx <12540796+MiaoRuidx@users.noreply.github.com>') [#4500](https://github.com/bytedance/deer-flow/pull/4500) [)](https://github.com/bytedance/deer-flow/commit/8a78c264b7697b552ec748044a161692e95d01c9 'fix(runtime): cancel runs across live gateway workers (#4500)

 * docs(runtime): design cross-worker cancellation

 * fix(runtime): cancel runs across gateway workers

 * fix(runtime): harden cross-worker cancellation races

 让取消请求与 owner 终态写入通过持久化 CAS 决定先后，保证首次取消 action 在不同 worker 路由下保持一致。\n\n将 heartbeat 收敛为续租后仅发送本地中止信号，并补齐完成竞态与路由重试的回归用例。

 * docs(runtime): drop implementation plan from PR

 移除仅用于实现过程的跨 worker 取消设计记录，保留 README 和 backend/AGENTS.md 中面向最终行为的文档。

 * fix(runtime): preserve local cancel fallback

 * test(runtime): adapt worker run manager fakes

 * docs(runtime): fix run cancel migration registry

 ---------

 Co-authored-by: MiaoRuidx <12540796+MiaoRuidx@users.noreply.github.com>')

 Show description for 8a78c26

 [![MiaoRuidx](https://avatars.githubusercontent.com/u/12540796?v=4&size=32)](https://github.com/MiaoRuidx) [MiaoRuidx](https://github.com/bytedance/deer-flow/commits?author=MiaoRuidx)

 authoredJul 28, 2026

 ·

 10 / 10

 Verified

 [8a78c26](https://github.com/bytedance/deer-flow/commit/8a78c264b7697b552ec748044a161692e95d01c9)View commit details

 Copy full SHA for 8a78c26

 Browse repository at this point

### Commits on Jul 25, 2026

- #### [fix: guard pending run startup cancellation (](https://github.com/bytedance/deer-flow/commit/735f67a5b27264d6166b45b56687a9896ad10bc3 'fix: guard pending run startup cancellation (#4450)

 * fix: guard pending run startup cancellation

 * fix(run): address startup review feedback

 * fix(run): narrow start_run store contract

 ---------

 Co-authored-by: MiaoRuidx <12540796+MiaoRuidx@users.noreply.github.com>
 Co-authored-by: Willem Jiang <willem.jiang@gmail.com>') [#4450](https://github.com/bytedance/deer-flow/pull/4450) [)](https://github.com/bytedance/deer-flow/commit/735f67a5b27264d6166b45b56687a9896ad10bc3 'fix: guard pending run startup cancellation (#4450)

 * fix: guard pending run startup cancellation

 * fix(run): address startup review feedback

 * fix(run): narrow start_run store contract

 ---------

 Co-authored-by: MiaoRuidx <12540796+MiaoRuidx@users.noreply.github.com>
 Co-authored-by: Willem Jiang <willem.jiang@gmail.com>')

 Show description for 735f67a

 ![MiaoRuidx](https://avatars.githubusercontent.com/u/12540796?v=4&size=32)![WillemJiang](https://avatars.githubusercontent.com/u/219644?v=4&size=32)

 [MiaoRuidx](https://github.com/bytedance/deer-flow/commits?author=MiaoRuidx)

 and

 [WillemJiang](https://github.com/bytedance/deer-flow/commits?author=WillemJiang)

 authoredJul 25, 2026

 ·

 9 / 10

 Verified

 [735f67a](https://github.com/bytedance/deer-flow/commit/735f67a5b27264d6166b45b56687a9896ad10bc3)View commit details

 Copy full SHA for 735f67a

 Browse repository at this point

### Commits on Jul 24, 2026

- #### [fix: make orphan reconciliation lease-aware (](https://github.com/bytedance/deer-flow/commit/80c06414f844e6d249ffdff6c6e4016ccd2a67ae 'fix: make orphan reconciliation lease-aware (#4434)

 让启动/孤儿 run 恢复在最终写入前通过 claim_for_takeover 原子重查 lease，避免 owner 在扫描后续约成功仍被误标为 error。

 补充扫描后续约的回归测试，并把 reconciliation 写失败测试迁移到 takeover claim 路径。

 Co-authored-by: MiaoRuidx <12540796+MiaoRuidx@users.noreply.github.com>
 Co-authored-by: Willem Jiang <willem.jiang@gmail.com>') [#4434](https://github.com/bytedance/deer-flow/pull/4434) [)](https://github.com/bytedance/deer-flow/commit/80c06414f844e6d249ffdff6c6e4016ccd2a67ae 'fix: make orphan reconciliation lease-aware (#4434)

 让启动/孤儿 run 恢复在最终写入前通过 claim_for_takeover 原子重查 lease，避免 owner 在扫描后续约成功仍被误标为 error。

 补充扫描后续约的回归测试，并把 reconciliation 写失败测试迁移到 takeover claim 路径。

 Co-authored-by: MiaoRuidx <12540796+MiaoRuidx@users.noreply.github.com>
 Co-authored-by: Willem Jiang <willem.jiang@gmail.com>')

 Show description for 80c0641

 ![MiaoRuidx](https://avatars.githubusercontent.com/u/12540796?v=4&size=32)![WillemJiang](https://avatars.githubusercontent.com/u/219644?v=4&size=32)

 [MiaoRuidx](https://github.com/bytedance/deer-flow/commits?author=MiaoRuidx)

 and

 [WillemJiang](https://github.com/bytedance/deer-flow/commits?author=WillemJiang)

 authoredJul 24, 2026

 ·

 10 / 10

 Verified

 [80c0641](https://github.com/bytedance/deer-flow/commit/80c06414f844e6d249ffdff6c6e4016ccd2a67ae)View commit details

 Copy full SHA for 80c0641

 Browse repository at this point

### Commits on Jul 23, 2026

- #### [fix(run): add run event stream contract (](https://github.com/bytedance/deer-flow/commit/f1632cc3511fd614879dcdfdf1f349ae392b746d 'fix(run): add run event stream contract (#4342)

 * docs: document run event stream contract

 * fix(run): address event stream review feedback

 ---------

 Co-authored-by: MiaoRuidx <12540796+MiaoRuidx@users.noreply.github.com>
 Co-authored-by: Willem Jiang <willem.jiang@gmail.com>') [#4342](https://github.com/bytedance/deer-flow/pull/4342) [)](https://github.com/bytedance/deer-flow/commit/f1632cc3511fd614879dcdfdf1f349ae392b746d 'fix(run): add run event stream contract (#4342)

 * docs: document run event stream contract

 * fix(run): address event stream review feedback

 ---------

 Co-authored-by: MiaoRuidx <12540796+MiaoRuidx@users.noreply.github.com>
 Co-authored-by: Willem Jiang <willem.jiang@gmail.com>')

 Show description for f1632cc

 ![MiaoRuidx](https://avatars.githubusercontent.com/u/12540796?v=4&size=32)![WillemJiang](https://avatars.githubusercontent.com/u/219644?v=4&size=32)

 [MiaoRuidx](https://github.com/bytedance/deer-flow/commits?author=MiaoRuidx)

 and

 [WillemJiang](https://github.com/bytedance/deer-flow/commits?author=WillemJiang)

 authoredJul 23, 2026

 ·

 10 / 10

 Verified

 [f1632cc](https://github.com/bytedance/deer-flow/commit/f1632cc3511fd614879dcdfdf1f349ae392b746d)View commit details

 Copy full SHA for f1632cc

 Browse repository at this point