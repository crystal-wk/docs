# Source: https://github.com/bytedance/deer-flow/releases

### Uh oh!

There was an error while loading. [Please reload this page]().

[bytedance](https://github.com/bytedance) / **[deer-flow](https://github.com/bytedance/deer-flow)** Public

- [Notifications](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow) You must be signed in to change notification settings
- [Fork 10.9k](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow)
- [Star 79.8k](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow)

# Releases: bytedance/deer-flow

Releases · bytedance/deer-flow

## Release list

Jump to release

- [DeerFlow 2.0.0 released](https://github.com/bytedance/deer-flow/releases#release-v2.0.0)

## DeerFlow 2.0.0 released

[DeerFlow 2.0.0 released](https://github.com/bytedance/deer-flow/releases/tag/v2.0.0) [Latest](https://github.com/bytedance/deer-flow/releases/latest)

[Latest](https://github.com/bytedance/deer-flow/releases/latest)

Compare

# Choose a tag to compare

## Sorry, something went wrong.

Filter

Loading 

## Sorry, something went wrong.

### Uh oh!

There was an error while loading. [Please reload this page]().

## No results found

[View all tags](https://github.com/bytedance/deer-flow/tags)

![@WillemJiang](https://avatars.githubusercontent.com/u/219644?s=40&v=4) [WillemJiang](https://github.com/WillemJiang) released this 25 Jun 16:23

Immutable release. Only release title and notes can be modified.

[v2.0.0](https://github.com/bytedance/deer-flow/tree/v2.0.0)

[`7e7f041`](https://github.com/bytedance/deer-flow/commit/7e7f0410797693cf882594555ba414e0361d4c6f)

# DeerFlow 2.0.0

DeerFlow 2.0 is a **ground-up rewrite** around a "super agent" harness that 
orchestrates **sub-agents**, **persistent memory**, **sandboxed execution**, 
and an extensible **skills/tools** system. It shares no code with the 1.x line, 
which lives on the [`main-1.x` branch](https://github.com/bytedance/deer-flow/tree/main-1.x).

This release closes the [2.0.0 milestone](https://github.com/bytedance/deer-flow/milestone/1) 
with **182 merged PRs** since the first 2.0 milestone tag.

> 📖 Full notes: [CHANGELOG.md](https://github.com/bytedance/deer-flow/blob/v2.0.0/CHANGELOG.md) · [中文版](https://github.com/bytedance/deer-flow/blob/v2.0.0/CHANGELOG_zh.md)

---

## ⚠️ Breaking change

- **Run hydration** — runs now hydrate from `RunStore` and persist `interrupted` 
 status. Cancellation now requires the worker who owns the run; cross-worker 
 cancels return `409` instead of silently appearing successful. (\[[#2932](https://github.com/bytedance/deer-flow/pull/2932)\])

## ✨ Highlights

- **Custom agents that update themselves** — agents can persist edits to their 
 own `SOUL.md` / `config.yaml` from a normal chat, with full per-user 
 isolation. (\[[#2713](https://github.com/bytedance/deer-flow/pull/2713)\])
- **User-owned IM channel connections** — users can bind their own Slack, 
 Telegram, Discord, Feishu/Lark, DingTalk, WeChat, and WeCom accounts on top 
 of operator-configured bots. (\[[#3487](https://github.com/bytedance/deer-flow/pull/3487)\])
- **More models & community search** — StepFun and MiMo reasoning models, 
 MiniMax for image/video/podcast skills plus a new music-generation skill, 
 and Brave Search / SearXNG / Browserless / Serper Google Images tools. 
 (\[[#3461](https://github.com/bytedance/deer-flow/pull/3461)\], \[[#3298](https://github.com/bytedance/deer-flow/pull/3298)\], \[[#3437](https://github.com/bytedance/deer-flow/pull/3437)\], \[[#3528](https://github.com/bytedance/deer-flow/pull/3528)\], \[[#3451](https://github.com/bytedance/deer-flow/pull/3451)\], \[[#3575](https://github.com/bytedance/deer-flow/pull/3575)\])
- **Richer channels** — Discord gets mention-only mode, thread routing, and 
 typing indicators; Telegram streams replies by editing the placeholder 
 message in place. (\[[#2842](https://github.com/bytedance/deer-flow/pull/2842)\], \[[#3534](https://github.com/bytedance/deer-flow/pull/3534)\])
- **Configurable loop detection** with per-tool frequency overrides and 
 deferred warning injection. (\[[#2586](https://github.com/bytedance/deer-flow/pull/2586)\], \[[#2711](https://github.com/bytedance/deer-flow/pull/2711)\], \[[#2752](https://github.com/bytedance/deer-flow/pull/2752)\])
- **Subagent token usage** streams to the header in real time, with spans 
 attributed to the parent thread's Langfuse trace. (\[[#2882](https://github.com/bytedance/deer-flow/pull/2882)\], \[[#3611](https://github.com/bytedance/deer-flow/pull/3611)\])
- **Trace polish** — clean `lead_agent` / custom-agent trace names; `session_id`
 - `user_id` propagated to Langfuse; non-ASCII memory traces no longer escape. 
 (\[[#3101](https://github.com/bytedance/deer-flow/pull/3101)\], \[[#2944](https://github.com/bytedance/deer-flow/pull/2944)\], \[[#3104](https://github.com/bytedance/deer-flow/pull/3104)\])
- **Token-usage tracking on by default**, with refined display modes and usage 
 attributed to the actual models. (\[[#2841](https://github.com/bytedance/deer-flow/pull/2841)\], \[[#2329](https://github.com/bytedance/deer-flow/pull/2329)\], \[[#3658](https://github.com/bytedance/deer-flow/pull/3658)\])
- **Flexible memory & suggestions** — opt out of tiktoken in restricted 
 networks via `memory.token_counting`; make AI follow-up suggestions optional. 
 (\[[#3465](https://github.com/bytedance/deer-flow/pull/3465)\], \[[#3591](https://github.com/bytedance/deer-flow/pull/3591)\])

## 🚀 Performance

- Push thread metadata filters into SQL. (\[[#2865](https://github.com/bytedance/deer-flow/pull/2865)\])
- Index runs by `thread_id` in `RunManager` to eliminate O(n) scans. (\[[#3499](https://github.com/bytedance/deer-flow/pull/3499)\])
- Index messages in `MemoryRunEventStore` to eliminate O(n) scans. (\[[#3531](https://github.com/bytedance/deer-flow/pull/3531)\])
- Cache `Base.to_dict` column reflection per class. (\[[#3654](https://github.com/bytedance/deer-flow/pull/3654)\])
- Speed up `should_ignore_name` in glob/grep sandbox walks. (\[[#3657](https://github.com/bytedance/deer-flow/pull/3657)\])

## 🔒 Security

- Reject symlinked upload destinations on Linux **and** Windows. 
 (\[[#2623](https://github.com/bytedance/deer-flow/pull/2623)\], \[[#2794](https://github.com/bytedance/deer-flow/pull/2794)\])
- Mask sensitive values in MCP config responses; harden the endpoint. 
 (\[[#2667](https://github.com/bytedance/deer-flow/pull/2667)\], \[[#3425](https://github.com/bytedance/deer-flow/pull/3425)\])
- Reject cross-site auth POSTs. (\[[#2740](https://github.com/bytedance/deer-flow/pull/2740)\])
- Cap skill artifact preview decompression (zip-bomb defense). (\[[#2963](https://github.com/bytedance/deer-flow/pull/2963)\])
- Mount the host Docker socket only in aio (DooD) sandbox mode. (\[[#3517](https://github.com/bytedance/deer-flow/pull/3517)\])
- Don't bind-mount host CLI auth dirs by default. (\[[#3521](https://github.com/bytedance/deer-flow/pull/3521)\])

## 🐛 Notable fixes

- **Memory** runs on a persistent event loop instead of a short-lived one 
 `asyncio.run()`; queued updates isolated per agent; wrapped JSON responses 
 parsed correctly. (\[[#2627](https://github.com/bytedance/deer-flow/pull/2627)\], \[[#2941](https://github.com/bytedance/deer-flow/pull/2941)\], \[[#3252](https://github.com/bytedance/deer-flow/pull/3252)\])
- **Runs** hydrate from the persistent store after a gateway restart, return 
 ISO 8601 timestamps, and have an idempotent cancel. (\[[#2989](https://github.com/bytedance/deer-flow/pull/2989)\], \[[#2599](https://github.com/bytedance/deer-flow/pull/2599)\], \[[#3058](https://github.com/bytedance/deer-flow/pull/3058)\])
- **Subagents** isolated from the parent run's checkpointer; timeout terminal 
 state atomic; respect model overrides for tools/middleware. (\[[#3559](https://github.com/bytedance/deer-flow/pull/3559)\], 
 \[[#2583](https://github.com/bytedance/deer-flow/pull/2583)\], \[[#2641](https://github.com/bytedance/deer-flow/pull/2641)\])
- **Sandbox** readiness polling no longer blocks the event loop; 
 `/mnt/user-data` contract enforced at the API boundary; PVC data scoped per 
 user; Windows/Git Bash MSYS path conversion disabled. (\[[#2822](https://github.com/bytedance/deer-flow/pull/2822)\], \[[#2881](https://github.com/bytedance/deer-flow/pull/2881)\], 
 \[[#2973](https://github.com/bytedance/deer-flow/pull/2973)\], \[[#2766](https://github.com/bytedance/deer-flow/pull/2766)\])
- **Auth** auto-generated JWT secrets persist across restarts; setup-status 
 uses cached responses instead of 429. (\[[#2933](https://github.com/bytedance/deer-flow/pull/2933)\], \[[#2915](https://github.com/bytedance/deer-flow/pull/2915)\])
- **Frontend** fixes a swallowed first message, login flicker / resize-observer 
 loop, duplicate optimistic messages, deeply nested list render crashes, and 
 thread isolation on new chats. (\[[#2731](https://github.com/bytedance/deer-flow/pull/2731)\], \[[#2954](https://github.com/bytedance/deer-flow/pull/2954)\], \[[#3002](https://github.com/bytedance/deer-flow/pull/3002)\], \[[#3393](https://github.com/bytedance/deer-flow/issues/3393)\], \[[#3570](https://github.com/bytedance/deer-flow/pull/3570)\], 
 \[[#3508](https://github.com/bytedance/deer-flow/pull/3508)\])
- **Channels** — user-owned IM now requires a bound identity, scopes files, and 
 helper commands to the owner, makes the provider state authoritative, and makes 
 The connect flow is deterministic, backed by shared retry helpers and 
 operational guardrails. (\[[#3578](https://github.com/bytedance/deer-flow/pull/3578)\], \[[#3579](https://github.com/bytedance/deer-flow/pull/3579)\], \[[#3580](https://github.com/bytedance/deer-flow/pull/3580)\], \[[#3581](https://github.com/bytedance/deer-flow/pull/3581)\], \[[#3582](https://github.com/bytedance/deer-flow/pull/3582)\], 
 \[[#3583](https://github.com/bytedance/deer-flow/pull/3583)\], \[[#3584](https://github.com/bytedance/deer-flow/pull/3584)\])
- **Streaming & history** — interrupts propagate through SSE values events for 
 the LangGraph SDK, and base64 image payloads are stripped from streamed and 
 history responses to keep the UI responsive. (\[[#3605](https://github.com/bytedance/deer-flow/pull/3605)\], \[[#3631](https://github.com/bytedance/deer-flow/pull/3631)\], \[[#3535](https://github.com/bytedance/deer-flow/pull/3535)\])
- **Frontend (more)** — the workspace chat list paginates beyond 50 threads, 
 stays interactive when the SSR auth probe can't reach the gateway, and gets a 
 mobile-friendly layout. (\[[#3485](https://github.com/bytedance/deer-flow/pull/3485)\], \[[#3495](https://github.com/bytedance/deer-flow/pull/3495)\], \[[#3646](https://github.com/bytedance/deer-flow/pull/3646)\])

## 📦 Deploy & ops

- **Docker** Gateway defaults to a single worker (multi-worker breakage). 
 (\[[#3475](https://github.com/bytedance/deer-flow/pull/3475)\])
- **Docker** nginx resolves upstream names at request time. (\[[#2717](https://github.com/bytedance/deer-flow/pull/2717)\])
- **Packaging** adds `postgres` extra for store/checkpointer support. (\[[#2584](https://github.com/bytedance/deer-flow/pull/2584)\])
- **Scripts** preserve `uv` extras across `make dev` restarts; clean up local 
 nginx on stop; exclude runtime state from gateway reload. (\[[#2767](https://github.com/bytedance/deer-flow/pull/2767)\], \[[#3005](https://github.com/bytedance/deer-flow/pull/3005)\], 
 \[[#3426](https://github.com/bytedance/deer-flow/pull/3426)\])

## 🙌 Thanks

Huge thanks to the 40 contributors who landed 180 merged PRs in the 2.0.0 milestone, and to everyone who filed issues, tested builds, and shared feedback. DeerFlow 2.0 wouldn't exist without you.

In alphabetical order:

- [@18062706139fcz](https://github.com/18062706139fcz) — Ryker\_Feng
- [@64johnlee](https://github.com/64johnlee) — john lee
- [@airene](https://github.com/airene) — Airene Fang
- [@AnoobFeng](https://github.com/AnoobFeng) — AnoobFeng
- [@chetan655](https://github.com/chetan655) — Chetan Sharma
- [@ech0hol](https://github.com/ech0hol) — Zhipeng Zheng
- [@Eilen6316](https://github.com/Eilen6316) — Eilen Shin
- [@fancyboi999](https://github.com/fancyboi999) — Xinmin Zeng
- [@ggnnggez](https://github.com/ggnnggez) — Nan Gao
- [@greatmengqi](https://github.com/greatmengqi) — greatmengqi
- [@hata33](https://github.com/hata33) — hataa
- [@heart-scalpel](https://github.com/heart-scalpel) — heart-scalpel
- [@he-yufeng](https://github.com/he-yufeng) — Yufeng He
- [@hetaoBackend](https://github.com/hetaoBackend) — DanielWalnut
- [@Hinotoi-agent](https://github.com/Hinotoi-agent) — Hinotobi
- [@Huixin615](https://github.com/Huixin615) — Huixin615
- [@idefav](https://github.com/idefav) — idefav
- [@jinghuan-Chen](https://github.com/jinghuan-Chen) — jinghuan-Chen
- [@Kiteeater](https://github.com/Kiteeater) — KiteEater
- [@kibabsquirrel](https://github.com/kibabsquirrel) — Lawrance\_YXLiao
- [@knight0940](https://github.com/knight0940) — Amorend
- [@Layau-code](https://github.com/Layau-code) — YuJitang
- [@liuchuan01](https://github.com/liuchuan01) — liuchuan01
- [@LittleChenLiya](https://github.com/LittleChenLiya) — Admire
- [@ly-wang19](https://github.com/ly-wang19) — ly-wang19
- [@NewAmorend](https://github.com/NewAmorend) — Amorend
- [@nguyen0096](https://github.com/nguyen0096) — Nguyen DN
- [@p-yf](https://github.com/p-yf) — yangyufan
- [@player0718](https://github.com/player0718) — Lucy Shen
- [@ShenAC-SAC](https://github.com/ShenAC-SAC) — AochenShen99
- [@shenlihust](https://github.com/shenlihust) — 魔力鸟
- [@sunshine-lang](https://github.com/sunshine-lang) — sunsine
- [@stphtt](https://github.com/stphtt) — stphtt
- [@wahajahmed010](https://github.com/wahajahmed010) — Wahaj Ahmed
- [@whhe](https://github.com/whhe) — He Wang
- [@WillemJiang](https://github.com/WillemJiang) — Willem Jiang
- [@xunliu](https://github.com/xunliu) — Xun
- [@yangzheli](https://github.com/yangzheli) — yangzheli
- [@yitang](https://github.com/yitang) — Yi Tang
- [@Yuyi-Ao](https://github.com/Yuyi-Ao) — Yuyi Ao
- [@zengxi](https://github.com/zengxi) — zengxi
- [@zwj110610](https://github.com/zwj110610) — zgenu

See the full author and PR list on the 
[milestone page](https://github.com/bytedance/deer-flow/milestone/1).

### Contributors

- [![@WillemJiang](https://avatars.githubusercontent.com/u/219644?s=64&v=4)](https://github.com/WillemJiang)
- [![@zengxi](https://avatars.githubusercontent.com/u/2630211?s=64&v=4)](https://github.com/zengxi)
- [![@xunliu](https://avatars.githubusercontent.com/u/3677382?s=64&v=4)](https://github.com/xunliu)
- [![@airene](https://avatars.githubusercontent.com/u/4494476?s=64&v=4)](https://github.com/airene)
- [![@yitang](https://avatars.githubusercontent.com/u/6054101?s=64&v=4)](https://github.com/yitang)
- [![@idefav](https://avatars.githubusercontent.com/u/6405415?s=64&v=4)](https://github.com/idefav)
- [![@shenlihust](https://avatars.githubusercontent.com/u/17823347?s=64&v=4)](https://github.com/shenlihust)
- [![@greatmengqi](https://avatars.githubusercontent.com/u/24458013?s=64&v=4)](https://github.com/greatmengqi)
- [![@nguyen0096](https://avatars.githubusercontent.com/u/25027694?s=64&v=4)](https://github.com/nguyen0096)
- [![@stphtt](https://avatars.githubusercontent.com/u/25250133?s=64&v=4)](https://github.com/stphtt)
- [![@whhe](https://avatars.githubusercontent.com/u/27404407?s=64&v=4)](https://github.com/whhe)
- [![@kibabsquirrel](https://avatars.githubusercontent.com/u/32213920?s=64&v=4)](https://github.com/kibabsquirrel)
- [![@he-yufeng](https://avatars.githubusercontent.com/u/40085740?s=64&v=4)](https://github.com/he-yufeng)
- [![@jinghuan-Chen](https://avatars.githubusercontent.com/u/42742857?s=64&v=4)](https://github.com/jinghuan-Chen)
- [![@yangzheli](https://avatars.githubusercontent.com/u/43645580?s=64&v=4)](https://github.com/yangzheli)
- [![@hetaoBackend](https://avatars.githubusercontent.com/u/45447813?s=64&v=4)](https://github.com/hetaoBackend)
- [![@player0718](https://avatars.githubusercontent.com/u/49802413?s=64&v=4)](https://github.com/player0718)
- [![@wahajahmed010](https://avatars.githubusercontent.com/u/57330918?s=64&v=4)](https://github.com/wahajahmed010)
- [![@heart-scalpel](https://avatars.githubusercontent.com/u/61306204?s=64&v=4)](https://github.com/heart-scalpel)
- [![@Yuyi-Ao](https://avatars.githubusercontent.com/u/63177164?s=64&v=4)](https://github.com/Yuyi-Ao)
- [![@LittleChenLiya](https://avatars.githubusercontent.com/u/64821731?s=64&v=4)](https://github.com/LittleChenLiya)
- [![@hata33](https://avatars.githubusercontent.com/u/79907651?s=64&v=4)](https://github.com/hata33)
- [![@liuchuan01](https://avatars.githubusercontent.com/u/80431571?s=64&v=4)](https://github.com/liuchuan01)
- [![@ech0hol](https://avatars.githubusercontent.com/u/87688412?s=64&v=4)](https://github.com/ech0hol)
- [![@ggnnggez](https://avatars.githubusercontent.com/u/88081804?s=64&v=4)](https://github.com/ggnnggez)
- [![@18062706139fcz](https://avatars.githubusercontent.com/u/90562015?s=64&v=4)](https://github.com/18062706139fcz)
- [![@ly-wang19](https://avatars.githubusercontent.com/u/94427531?s=64&v=4)](https://github.com/ly-wang19)
- [![@AnoobFeng](https://avatars.githubusercontent.com/u/109097565?s=64&v=4)](https://github.com/AnoobFeng)
- [![@sunshine-lang](https://avatars.githubusercontent.com/u/135408348?s=64&v=4)](https://github.com/sunshine-lang)
- [![@fancyboi999](https://avatars.githubusercontent.com/u/135568692?s=64&v=4)](https://github.com/fancyboi999)
- [![@Eilen6316](https://avatars.githubusercontent.com/u/136898293?s=64&v=4)](https://github.com/Eilen6316)
- [![@knight0940](https://avatars.githubusercontent.com/u/142649913?s=64&v=4)](https://github.com/knight0940)
- [![@ShenAC-SAC](https://avatars.githubusercontent.com/u/142667174?s=64&v=4)](https://github.com/ShenAC-SAC)
- [![@Kiteeater](https://avatars.githubusercontent.com/u/145987840?s=64&v=4)](https://github.com/Kiteeater)
- [![@chetan655](https://avatars.githubusercontent.com/u/173717093?s=64&v=4)](https://github.com/chetan655)
- [![@p-yf](https://avatars.githubusercontent.com/u/181648048?s=64&v=4)](https://github.com/p-yf)
- [![@zwj110610](https://avatars.githubusercontent.com/u/184498352?s=64&v=4)](https://github.com/zwj110610)
- [![@Huixin615](https://avatars.githubusercontent.com/u/185043954?s=64&v=4)](https://github.com/Huixin615)
- [![@64johnlee](https://avatars.githubusercontent.com/u/208139204?s=64&v=4)](https://github.com/64johnlee)
- [![@Layau-code](https://avatars.githubusercontent.com/u/213606337?s=64&v=4)](https://github.com/Layau-code)
- [![@Hinotoi-agent](https://avatars.githubusercontent.com/u/275430060?s=64&v=4)](https://github.com/Hinotoi-agent)
- [![@NewAmorend](https://avatars.githubusercontent.com/u/281509834?s=64&v=4)](https://github.com/NewAmorend)

WillemJiang, zengxi, and 40 other contributors

Assets 3

Loading

### Uh oh!

There was an error while loading. [Please reload this page]().

 ![tada](https://github.githubassets.com/assets/1f389-36899a2cb781.png) 14 aooohan, ech0hol, airene, Hical61, EmmaHou-Forward, LittleChenLiya, WillemJiang, Plus-L, Yuan-2005-z, Eilen6316, and 4 more reacted with hooray emoji

All reactions

- ![tada](https://github.githubassets.com/assets/1f389-36899a2cb781.png) 14 reactions

14 people reacted

0 [Join discussion](https://github.com/bytedance/deer-flow/discussions/3795)