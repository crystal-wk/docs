# Source: https://github.com/bytedance/deer-flow/tree/main/contracts

### Uh oh!

There was an error while loading. [Please reload this page]().

[bytedance](https://github.com/bytedance) / **[deer-flow](https://github.com/bytedance/deer-flow)** Public

- [Notifications](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow) You must be signed in to change notification settings
- [Fork 10.9k](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow)
- [Star 79.8k](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow)

 ## FilesExpand file tree

main

/

# contracts

/

Copy path

## Directory actions

## More options

More options

## Directory actions

## More options

More options

## Latest commit

![MiaoRuidx](https://avatars.githubusercontent.com/u/12540796?v=4&size=40)![WillemJiang](https://avatars.githubusercontent.com/u/219644?v=4&size=40)

[MiaoRuidx](https://github.com/bytedance/deer-flow/commits?author=MiaoRuidx)

and

[WillemJiang](https://github.com/bytedance/deer-flow/commits?author=WillemJiang)

[fix(run): add run event stream contract (](https://github.com/bytedance/deer-flow/commit/f1632cc3511fd614879dcdfdf1f349ae392b746d) [#4342](https://github.com/bytedance/deer-flow/pull/4342) [)](https://github.com/bytedance/deer-flow/commit/f1632cc3511fd614879dcdfdf1f349ae392b746d)

Open commit detailssuccess

Jul 23, 2026

[f1632cc](https://github.com/bytedance/deer-flow/commit/f1632cc3511fd614879dcdfdf1f349ae392b746d) · Jul 23, 2026

## History

[History](https://github.com/bytedance/deer-flow/commits/main/contracts)

Open commit details

History

## FilesExpand file tree

main

/

# contracts

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

[skill\_review](https://github.com/bytedance/deer-flow/tree/main/contracts/skill_review 'skill_review')

 | 

[skill\_review](https://github.com/bytedance/deer-flow/tree/main/contracts/skill_review 'skill_review')

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

[run\_event\_stream\_contract.json](https://github.com/bytedance/deer-flow/blob/main/contracts/run_event_stream_contract.json 'run_event_stream_contract.json')

 | 

[run\_event\_stream\_contract.json](https://github.com/bytedance/deer-flow/blob/main/contracts/run_event_stream_contract.json 'run_event_stream_contract.json')

 | 

[fix(run): add run event stream contract (](https://github.com/bytedance/deer-flow/commit/f1632cc3511fd614879dcdfdf1f349ae392b746d 'fix(run): add run event stream contract (#4342)

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

 | 

Jul 23, 2026

 |
| 

[slash\_skill\_contract.json](https://github.com/bytedance/deer-flow/blob/main/contracts/slash_skill_contract.json 'slash_skill_contract.json')

 | 

[slash\_skill\_contract.json](https://github.com/bytedance/deer-flow/blob/main/contracts/slash_skill_contract.json 'slash_skill_contract.json')

 | 

[feat(frontend): render slash-skill activations as inline chips (](https://github.com/bytedance/deer-flow/commit/c640b52a7d75cc42d3606af7bbaa2fd7ba6e7c80 'feat(frontend): render slash-skill activations as inline chips (#3981)

* feat(frontend): render slash-skill activations as inline chips

Show an explicit `/skill` activation as a compact inline chip in both the
composer and the chat transcript instead of raw slash text.

- Composer: selecting a skill suggestion stores it as a removable chip
 aligned inline with the textarea; the leading `/skill ` prefix is
 reattached only at submit time, so the backend activation protocol is
 unchanged. Backspace on an empty input or the chip's close button clears
 it; history navigation is disabled while a chip is active.
- Transcript: human messages that begin with `/skill` render the skill as a
 read-only chip followed by the task text.
- Add a shared `core/skills/slash.ts` (`parseSlashSkillReference` +
 `resolveSlashSkillDisplay`) mirroring the backend `slash.py` gate, so the
 transcript only shows a chip when the skill actually exists and is enabled.
 This removes a duplicated regex/reserved-name list and keeps display
 semantics consistent with backend activation.

Add unit tests for the shared slash parser and extend the chat e2e to assert
the composer still submits `/skill <task>` after showing a chip.

* chore(frontend): format chat e2e test

* refactor(skills): address slash-skill chip review feedback

Follow-up to the inline slash-skill chip PR, resolving three second-order
review findings:

- Drive the reserved-command set and skill-name grammar from a shared
 contracts/slash_skill_contract.json instead of a hand-copied
 "keep in sync" pair. slash.ts and slash.py now reference the fixture, and
 contract tests on both sides fail CI if either drifts.
- Extract a shared SlashSkillChip so the composer and transcript chips stay
 in lockstep, and normalize the off-scale /8 and /12 opacity steps to the
 standard /10 and /20 tokens.
- Split HumanMessageText into a pure parse gate plus a slash-only subtree
 that owns the useSkills() lookup, so a skill-enabled toggle no longer
 re-renders every plain-text human turn.

Verified: frontend eslint + tsc clean, pnpm test 572 pass (incl. new
slash-contract test); backend slash contract + slash-skills tests 31 pass.

* style(tests): sort slash skill contract imports

* fix(composer): inline the slash-skill text so the chip aligns with input

Address the "composer body layout change" review on #3981 by rendering the
active skill as an inline chip in the same text flow as the prompt, rather
than a separate flex row that drifted the box model across states.

- Render the chip + prompt inside one leading-6 wrapper and edit the prompt
 through a `contentEditable` span, so the chip sits inline with the first
 line and long/multi-line input wraps naturally back to the container edge.
- Align the chip with `align-top`: its h-6 (24px) height matches the text
 line height, so chip and first-line centers coincide exactly (measured
 delta 0), fixing the chip being raised above the baseline.
- Restore the placeholder in chip mode via a `data-empty` CSS `::before`,
 which also gives the empty editable span width so it is no longer treated
 as hidden.
- Widen the IME helper to `HTMLElement` and route the span's keydown/paste
 through the shared skill-suggestion, prompt-history, backspace-to-clear,
 and IME-composition handlers so contentEditable behaves like the textarea.
- Extend chat.spec.ts to drive the inline skill editor instead of the
 textarea after a chip is shown.

* style(frontend): fix composer class order formatting

* fix(composer): break long unbroken input inside the slash-skill row

The inline slash-skill editor wrapped with `break-words`
(overflow-wrap: break-word), which only moves an over-long token to the
next line before breaking it. A long unbroken string therefore started
on the line below the chip, and when the string contained a break
opportunity such as a hyphen the browser wrapped there and pushed the
remaining run to the next line, leaving a wide gap on the right.

Switch to `break-all` (word-break: break-all) so the text fills each
line from the chip and packs tightly regardless of hyphens or CJK.') [#3981](https://github.com/bytedance/deer-flow/pull/3981) [)](https://github.com/bytedance/deer-flow/commit/c640b52a7d75cc42d3606af7bbaa2fd7ba6e7c80 'feat(frontend): render slash-skill activations as inline chips (#3981)

* feat(frontend): render slash-skill activations as inline chips

Show an explicit `/skill` activation as a compact inline chip in both the
composer and the chat transcript instead of raw slash text.

- Composer: selecting a skill suggestion stores it as a removable chip
 aligned inline with the textarea; the leading `/skill ` prefix is
 reattached only at submit time, so the backend activation protocol is
 unchanged. Backspace on an empty input or the chip's close button clears
 it; history navigation is disabled while a chip is active.
- Transcript: human messages that begin with `/skill` render the skill as a
 read-only chip followed by the task text.
- Add a shared `core/skills/slash.ts` (`parseSlashSkillReference` +
 `resolveSlashSkillDisplay`) mirroring the backend `slash.py` gate, so the
 transcript only shows a chip when the skill actually exists and is enabled.
 This removes a duplicated regex/reserved-name list and keeps display
 semantics consistent with backend activation.

Add unit tests for the shared slash parser and extend the chat e2e to assert
the composer still submits `/skill <task>` after showing a chip.

* chore(frontend): format chat e2e test

* refactor(skills): address slash-skill chip review feedback

Follow-up to the inline slash-skill chip PR, resolving three second-order
review findings:

- Drive the reserved-command set and skill-name grammar from a shared
 contracts/slash_skill_contract.json instead of a hand-copied
 "keep in sync" pair. slash.ts and slash.py now reference the fixture, and
 contract tests on both sides fail CI if either drifts.
- Extract a shared SlashSkillChip so the composer and transcript chips stay
 in lockstep, and normalize the off-scale /8 and /12 opacity steps to the
 standard /10 and /20 tokens.
- Split HumanMessageText into a pure parse gate plus a slash-only subtree
 that owns the useSkills() lookup, so a skill-enabled toggle no longer
 re-renders every plain-text human turn.

Verified: frontend eslint + tsc clean, pnpm test 572 pass (incl. new
slash-contract test); backend slash contract + slash-skills tests 31 pass.

* style(tests): sort slash skill contract imports

* fix(composer): inline the slash-skill text so the chip aligns with input

Address the "composer body layout change" review on #3981 by rendering the
active skill as an inline chip in the same text flow as the prompt, rather
than a separate flex row that drifted the box model across states.

- Render the chip + prompt inside one leading-6 wrapper and edit the prompt
 through a `contentEditable` span, so the chip sits inline with the first
 line and long/multi-line input wraps naturally back to the container edge.
- Align the chip with `align-top`: its h-6 (24px) height matches the text
 line height, so chip and first-line centers coincide exactly (measured
 delta 0), fixing the chip being raised above the baseline.
- Restore the placeholder in chip mode via a `data-empty` CSS `::before`,
 which also gives the empty editable span width so it is no longer treated
 as hidden.
- Widen the IME helper to `HTMLElement` and route the span's keydown/paste
 through the shared skill-suggestion, prompt-history, backspace-to-clear,
 and IME-composition handlers so contentEditable behaves like the textarea.
- Extend chat.spec.ts to drive the inline skill editor instead of the
 textarea after a chip is shown.

* style(frontend): fix composer class order formatting

* fix(composer): break long unbroken input inside the slash-skill row

The inline slash-skill editor wrapped with `break-words`
(overflow-wrap: break-word), which only moves an over-long token to the
next line before breaking it. A long unbroken string therefore started
on the line below the chip, and when the string contained a break
opportunity such as a hyphen the browser wrapped there and pushed the
remaining run to the next line, leaving a wide gap on the right.

Switch to `break-all` (word-break: break-all) so the text fills each
line from the chip and packs tightly regardless of hyphens or CJK.')

 | 

Jul 8, 2026

 |
| 

[subagent\_status\_contract.json](https://github.com/bytedance/deer-flow/blob/main/contracts/subagent_status_contract.json 'subagent_status_contract.json')

 | 

[subagent\_status\_contract.json](https://github.com/bytedance/deer-flow/blob/main/contracts/subagent_status_contract.json 'subagent_status_contract.json')

 | 

[fix(subagents): unify guardrail caps on additive stop\_reason + add to…](https://github.com/bytedance/deer-flow/commit/c9fb9768d476e28de0294ac7a23cab9819b93f83 'fix(subagents): unify guardrail caps on additive stop_reason + add token_budget (#3875 Phase 2) (#3980)

Phase 2 of #3875. Two guardrail axes can end a subagent run early — the turn
budget (GraphRecursionError) and the token budget (TokenBudgetMiddleware) —
and both now surface *why* through one additive `subagent_stop_reason` field
instead of a status enum.

This completes and course-corrects Phase 1 (#3949), which shipped the
turn-budget cap as a `max_turns_reached` status enum. The agreed Phase 2
design replaces that enum with an optional `stop_reason` field
(token_capped | turn_capped | loop_capped): a new enum value would break v1
consumers, while an additive field is ignored by older frontends and ledger
readers. `max_turns_reached` and SubagentStatus.MAX_TURNS_REACHED are removed.

- subagents.token_budget config (default enabled, 2,000,000 tokens, warn 0.7)
 with per-agent override; TokenBudgetMiddleware is now attached in
 build_subagent_runtime_middlewares so the cost-ceiling backstop engages for
 every subagent. The hard-stop does not raise — it strips tool_calls and
 lets the run finish with a final answer, recording the cap on a per-run
 consume_stop_reason() accessor.
- executor.py: on normal completion it reads consume_stop_reason() and stamps
 completed + token_capped when the budget fired; on GraphRecursionError it
 recovers the last AIMessage partial (completed + turn_capped) or, if nothing
 usable survived, failed + turn_capped. SubagentResult gains stop_reason.
- status_contract.py / contracts/subagent_status_contract.json (v2) /
 frontend subtask-result.ts: additive subagent_stop_reason field, pinned by
 test_status_values_match_contract / test_stop_reason_values_match_contract.
- task_tool.py + delegation_ledger.py: drop the max_turns_reached paths; the
 ledger captures stop_reason and renders model-facing "capped" guidance so
 the lead reuses a capped completion knowingly.

The 2,000,000-token default is deliberately loose (tighten to taste) — it
would have roughly halved the reported 4.4M burn while leaving legitimate
deep-research runs (max_turns=150) room. Subagent summarization is a follow-up.')

 | 

Jul 8, 2026

 |
| 

View all files

 |