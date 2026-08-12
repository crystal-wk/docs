# Source: https://github.com/bytedance/deer-flow/commits/main/contracts

### Uh oh!

There was an error while loading. [Please reload this page]().

[bytedance](https://github.com/bytedance) / **[deer-flow](https://github.com/bytedance/deer-flow)** Public

- [Notifications](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow) You must be signed in to change notification settings
- [Fork 10.9k](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow)
- [Star 79.8k](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow)

 ## Breadcrumbs

History for

on[main](https://github.com/bytedance/deer-flow/tree/main)

## User selector

All users

## Datepicker

All time

## Commit history

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

 View code at this pointBrowse repository at this point

### Commits on Jul 11, 2026

- #### [feat(skills): add skill review quality gate (](https://github.com/bytedance/deer-flow/commit/41658c5ff40f3f1a8a3bffcb8bc58a39117d44e2 'feat(skills): add skill review quality gate (#4037)

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

 Show description for 41658c5

 [![18062706139fcz](https://avatars.githubusercontent.com/u/90562015?v=4&size=32)](https://github.com/18062706139fcz) [18062706139fcz](https://github.com/bytedance/deer-flow/commits?author=18062706139fcz)

 authoredJul 11, 2026

 ·

 11 / 11

 Verified

 [41658c5](https://github.com/bytedance/deer-flow/commit/41658c5ff40f3f1a8a3bffcb8bc58a39117d44e2)View commit details

 Copy full SHA for 41658c5

 View code at this pointBrowse repository at this point

### Commits on Jul 8, 2026

- #### [fix(subagents): unify guardrail caps on additive stop\_reason + add token\_budget (](https://github.com/bytedance/deer-flow/commit/c9fb9768d476e28de0294ac7a23cab9819b93f83 'fix(subagents): unify guardrail caps on additive stop_reason + add token_budget (#3875 Phase 2) (#3980)

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
 deep-research runs (max_turns=150) room. Subagent summarization is a follow-up.') [#3875](https://github.com/bytedance/deer-flow/issues/3875) [Phase 2) (](https://github.com/bytedance/deer-flow/commit/c9fb9768d476e28de0294ac7a23cab9819b93f83 'fix(subagents): unify guardrail caps on additive stop_reason + add token_budget (#3875 Phase 2) (#3980)

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
 deep-research runs (max_turns=150) room. Subagent summarization is a follow-up.') [#3980](https://github.com/bytedance/deer-flow/pull/3980) [)](https://github.com/bytedance/deer-flow/commit/c9fb9768d476e28de0294ac7a23cab9819b93f83 'fix(subagents): unify guardrail caps on additive stop_reason + add token_budget (#3875 Phase 2) (#3980)

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

 Show description for c9fb976

 [![hata33](https://avatars.githubusercontent.com/u/79907651?v=4&size=32)](https://github.com/hata33) [hata33](https://github.com/bytedance/deer-flow/commits?author=hata33)

 authoredJul 8, 2026

 ·

 11 / 11

 Verified

 [c9fb976](https://github.com/bytedance/deer-flow/commit/c9fb9768d476e28de0294ac7a23cab9819b93f83)View commit details

 Copy full SHA for c9fb976

 View code at this pointBrowse repository at this point

- #### [feat(frontend): render slash-skill activations as inline chips (](https://github.com/bytedance/deer-flow/commit/c640b52a7d75cc42d3606af7bbaa2fd7ba6e7c80 'feat(frontend): render slash-skill activations as inline chips (#3981)

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

 Show description for c640b52

 [![18062706139fcz](https://avatars.githubusercontent.com/u/90562015?v=4&size=32)](https://github.com/18062706139fcz) [18062706139fcz](https://github.com/bytedance/deer-flow/commits?author=18062706139fcz)

 authoredJul 8, 2026

 ·

 11 / 11

 Verified

 [c640b52](https://github.com/bytedance/deer-flow/commit/c640b52a7d75cc42d3606af7bbaa2fd7ba6e7c80)View commit details

 Copy full SHA for c640b52

 View code at this pointBrowse repository at this point

### Commits on Jul 5, 2026

- #### [fix(subagents): surface turn-budget cap as MAX\_TURNS\_REACHED with partial result (](https://github.com/bytedance/deer-flow/commit/0664ea224335eacb32c2775dfc79065d9262309f 'fix(subagents): surface turn-budget cap as MAX_TURNS_REACHED with partial result (#3875 Phase 2) (#3949)

 * fix(subagents): surface turn-budget cap as MAX_TURNS_REACHED with partial result (#3875)

 Phase 2 of #3875. When a subagent exhausts its turn budget
 (recursion_limit == max_turns), LangGraph raises
 GraphRecursionError from agent.astream. The generic
 except Exception in _aexecute misclassified it as FAILED and
 discarded the partial work already streamed into final_state, so the
 lead could not tell 'broken subagent' from 'out of budget' and got an
 empty failure.

 Catch GraphRecursionError specifically (before the generic handler)
 and set a distinct SubagentStatus.MAX_TURNS_REACHED terminal status,
 recovering the partial result from the last streamed chunk via a shared
 _extract_final_result helper (refactored out of the normal-completion
 path so both paths render content identically).

 Extend the cross-language status contract so the new value travels on
 additional_kwargs.subagent_status: a capped run is result-bearing, so
 make_subagent_additional_kwargs / read_subagent_result_metadata
 carry subagent_result_brief + subagent_result_sha256 (the
 recovered work, like completed) AND the cap notice on subagent_error
 -- the one status that carries both. task_tool.py returns it via the
 shared _task_result_command; the delegation ledger prefers the
 partial result_brief and renders model-facing guidance (reuse / retry
 tighter / raise max_turns). Frontend collapses max_turns_reached to the
 failed pill with the cap notice on error.

 No agent-loop, runner, or persistence behavior touched; default
 max_turns is unchanged.

 * refactor(subagents): consolidate content-stringify onto shared helper

 Address review feedback on #3949 (willem-bd, copilot-pull-request-reviewer):

 - executor.py: drop the private `_stringify_message_content` — a third
 near-duplicate of `utils/messages.py::message_content_to_text`.
 `_extract_final_result` now delegates to that canonical helper; the
 "No response generated" sentinel is pushed down to the consumer (the
 shared helper returns "" for no-text, matching every other call site).
 - task_tool.py: align the live `task_failed` event's error string with
 the canonical "Reached max_turns=N" used by the logger, the structured
 `error=`, and the executor (was "Reached max turns (N)").

 Behavior for real AIMessage content is unchanged; only atypical edge inputs
 (consecutive bare-string list items; empty content) now match the canonical
 helper that every other call site already uses.

 `extract_response_text` is intentionally left as-is: it filters by OpenAI
 content-block `type`, a different shape with many callers and its own tests.

 Co-Authored-By: Claude <noreply@anthropic.com>

 ---------

 Co-authored-by: Claude <noreply@anthropic.com>') [#3875](https://github.com/bytedance/deer-flow/issues/3875) [Phase 2) (](https://github.com/bytedance/deer-flow/commit/0664ea224335eacb32c2775dfc79065d9262309f 'fix(subagents): surface turn-budget cap as MAX_TURNS_REACHED with partial result (#3875 Phase 2) (#3949)

 * fix(subagents): surface turn-budget cap as MAX_TURNS_REACHED with partial result (#3875)

 Phase 2 of #3875. When a subagent exhausts its turn budget
 (recursion_limit == max_turns), LangGraph raises
 GraphRecursionError from agent.astream. The generic
 except Exception in _aexecute misclassified it as FAILED and
 discarded the partial work already streamed into final_state, so the
 lead could not tell 'broken subagent' from 'out of budget' and got an
 empty failure.

 Catch GraphRecursionError specifically (before the generic handler)
 and set a distinct SubagentStatus.MAX_TURNS_REACHED terminal status,
 recovering the partial result from the last streamed chunk via a shared
 _extract_final_result helper (refactored out of the normal-completion
 path so both paths render content identically).

 Extend the cross-language status contract so the new value travels on
 additional_kwargs.subagent_status: a capped run is result-bearing, so
 make_subagent_additional_kwargs / read_subagent_result_metadata
 carry subagent_result_brief + subagent_result_sha256 (the
 recovered work, like completed) AND the cap notice on subagent_error
 -- the one status that carries both. task_tool.py returns it via the
 shared _task_result_command; the delegation ledger prefers the
 partial result_brief and renders model-facing guidance (reuse / retry
 tighter / raise max_turns). Frontend collapses max_turns_reached to the
 failed pill with the cap notice on error.

 No agent-loop, runner, or persistence behavior touched; default
 max_turns is unchanged.

 * refactor(subagents): consolidate content-stringify onto shared helper

 Address review feedback on #3949 (willem-bd, copilot-pull-request-reviewer):

 - executor.py: drop the private `_stringify_message_content` — a third
 near-duplicate of `utils/messages.py::message_content_to_text`.
 `_extract_final_result` now delegates to that canonical helper; the
 "No response generated" sentinel is pushed down to the consumer (the
 shared helper returns "" for no-text, matching every other call site).
 - task_tool.py: align the live `task_failed` event's error string with
 the canonical "Reached max_turns=N" used by the logger, the structured
 `error=`, and the executor (was "Reached max turns (N)").

 Behavior for real AIMessage content is unchanged; only atypical edge inputs
 (consecutive bare-string list items; empty content) now match the canonical
 helper that every other call site already uses.

 `extract_response_text` is intentionally left as-is: it filters by OpenAI
 content-block `type`, a different shape with many callers and its own tests.

 Co-Authored-By: Claude <noreply@anthropic.com>

 ---------

 Co-authored-by: Claude <noreply@anthropic.com>') [#3949](https://github.com/bytedance/deer-flow/pull/3949) [)](https://github.com/bytedance/deer-flow/commit/0664ea224335eacb32c2775dfc79065d9262309f 'fix(subagents): surface turn-budget cap as MAX_TURNS_REACHED with partial result (#3875 Phase 2) (#3949)

 * fix(subagents): surface turn-budget cap as MAX_TURNS_REACHED with partial result (#3875)

 Phase 2 of #3875. When a subagent exhausts its turn budget
 (recursion_limit == max_turns), LangGraph raises
 GraphRecursionError from agent.astream. The generic
 except Exception in _aexecute misclassified it as FAILED and
 discarded the partial work already streamed into final_state, so the
 lead could not tell 'broken subagent' from 'out of budget' and got an
 empty failure.

 Catch GraphRecursionError specifically (before the generic handler)
 and set a distinct SubagentStatus.MAX_TURNS_REACHED terminal status,
 recovering the partial result from the last streamed chunk via a shared
 _extract_final_result helper (refactored out of the normal-completion
 path so both paths render content identically).

 Extend the cross-language status contract so the new value travels on
 additional_kwargs.subagent_status: a capped run is result-bearing, so
 make_subagent_additional_kwargs / read_subagent_result_metadata
 carry subagent_result_brief + subagent_result_sha256 (the
 recovered work, like completed) AND the cap notice on subagent_error
 -- the one status that carries both. task_tool.py returns it via the
 shared _task_result_command; the delegation ledger prefers the
 partial result_brief and renders model-facing guidance (reuse / retry
 tighter / raise max_turns). Frontend collapses max_turns_reached to the
 failed pill with the cap notice on error.

 No agent-loop, runner, or persistence behavior touched; default
 max_turns is unchanged.

 * refactor(subagents): consolidate content-stringify onto shared helper

 Address review feedback on #3949 (willem-bd, copilot-pull-request-reviewer):

 - executor.py: drop the private `_stringify_message_content` — a third
 near-duplicate of `utils/messages.py::message_content_to_text`.
 `_extract_final_result` now delegates to that canonical helper; the
 "No response generated" sentinel is pushed down to the consumer (the
 shared helper returns "" for no-text, matching every other call site).
 - task_tool.py: align the live `task_failed` event's error string with
 the canonical "Reached max_turns=N" used by the logger, the structured
 `error=`, and the executor (was "Reached max turns (N)").

 Behavior for real AIMessage content is unchanged; only atypical edge inputs
 (consecutive bare-string list items; empty content) now match the canonical
 helper that every other call site already uses.

 `extract_response_text` is intentionally left as-is: it filters by OpenAI
 content-block `type`, a different shape with many callers and its own tests.

 Co-Authored-By: Claude <noreply@anthropic.com>

 ---------

 Co-authored-by: Claude <noreply@anthropic.com>')

 Show description for 0664ea2

 ![hata33](https://avatars.githubusercontent.com/u/79907651?v=4&size=32)![claude](https://avatars.githubusercontent.com/u/81847?v=4&size=32)

 [hata33](https://github.com/bytedance/deer-flow/commits?author=hata33)

 and

 [claude](https://github.com/bytedance/deer-flow/commits?author=claude)

 authoredJul 5, 2026

 ·

 11 / 11

 Verified

 [0664ea2](https://github.com/bytedance/deer-flow/commit/0664ea224335eacb32c2775dfc79065d9262309f)View commit details

 Copy full SHA for 0664ea2

 View code at this pointBrowse repository at this point

### Commits on Jul 4, 2026

- #### [feat: emit structured runtime metadata (follow-up#3887) (](https://github.com/bytedance/deer-flow/commit/66b9e7f21212490cf92fafac137542b9deb06615 'feat: emit structured runtime metadata (follow-up#3887) (#3906)

 * feat: emit structured runtime metadata

 * fix: avoid subagent import cycle in replay gateway

 * fix: preserve legacy subtask result parsing

 * refactor: tighten runtime metadata contracts

 * fix(middleware): keep recovery hint on task exception wrapper content

 The structured-metadata stamp overwrote the wrapper text with the bare
 task-failure message, dropping the model-facing 'Continue with available
 context, or choose an alternative tool.' guidance that every other tool
 exception keeps. Append the shared hint after the formatted message.

 * fix(subagents): require lowercase hex for result_sha256 reader

 Length-only validation accepted any 64-char string; a faulty serializer
 or relaying wrapper could store a non-digest value in the delegation
 ledger. Enforce the producer's hexdigest shape with a fullmatch.

 ---------

 Co-authored-by: Willem Jiang <willem.jiang@gmail.com>') [#3906](https://github.com/bytedance/deer-flow/pull/3906) [)](https://github.com/bytedance/deer-flow/commit/66b9e7f21212490cf92fafac137542b9deb06615 'feat: emit structured runtime metadata (follow-up#3887) (#3906)

 * feat: emit structured runtime metadata

 * fix: avoid subagent import cycle in replay gateway

 * fix: preserve legacy subtask result parsing

 * refactor: tighten runtime metadata contracts

 * fix(middleware): keep recovery hint on task exception wrapper content

 The structured-metadata stamp overwrote the wrapper text with the bare
 task-failure message, dropping the model-facing 'Continue with available
 context, or choose an alternative tool.' guidance that every other tool
 exception keeps. Append the shared hint after the formatted message.

 * fix(subagents): require lowercase hex for result_sha256 reader

 Length-only validation accepted any 64-char string; a faulty serializer
 or relaying wrapper could store a non-digest value in the delegation
 ledger. Enforce the producer's hexdigest shape with a fullmatch.

 ---------

 Co-authored-by: Willem Jiang <willem.jiang@gmail.com>')

 Show description for 66b9e7f

 ![ShenAC-SAC](https://avatars.githubusercontent.com/u/142667174?v=4&size=32)![WillemJiang](https://avatars.githubusercontent.com/u/219644?v=4&size=32)

 [ShenAC-SAC](https://github.com/bytedance/deer-flow/commits?author=ShenAC-SAC)

 and

 [WillemJiang](https://github.com/bytedance/deer-flow/commits?author=WillemJiang)

 authoredJul 4, 2026

 ·

 10 / 10

 Verified

 [66b9e7f](https://github.com/bytedance/deer-flow/commit/66b9e7f21212490cf92fafac137542b9deb06615)View commit details

 Copy full SHA for 66b9e7f

 View code at this pointBrowse repository at this point

### Commits on Jun 7, 2026

- #### [fix(subagent): structured subagent\_status field over text parsing (](https://github.com/bytedance/deer-flow/commit/8d2e55a05f6a23d4318b910b123d182d1adb9638 'fix(subagent): structured subagent_status field over text parsing (#3146) (#3154)

 * fix(subagent): structured subagent_status field over text parsing

 Closes #3146.

 ## Why

 The frontend used to derive subtask card state by string-matching the
 leading text of the `task` tool's result. That contract surface was
 fragile — `#3107` BUG-007 and the `#3131` review both surfaced cases
 where new backend wording (`Task cancelled by user.`,
 `Task polling timed out after N minutes`, `ToolErrorHandlingMiddleware`
 exception wrappers) silently broke the card lifecycle. The frontend
 fallback kept growing more prefixes; any future rewording would break
 it again.

 ## Design

 1. **Backend → frontend contract**: `ToolMessage.additional_kwargs`
 carries `subagent_status` (one of `completed | failed | cancelled |
 timed_out | polling_timed_out`) and an optional `subagent_error`
 blob. The frontend prefers it over parsing `content`.

 2. **Centralised stamping, not 8 sprinkled stamps**: rather than have
 each of `task_tool.py`'s 5 normal-return + 3 pre-execution `Error:`
 paths remember to set `additional_kwargs`, `ToolErrorHandlingMiddleware`
 stamps the field after every task-tool call. Adding a new return
 path in `task_tool.py` cannot now skip the stamp.

 3. **Cross-language contract fixture**: the prefix→status mapping is
 the one piece both sides must agree on. The shared fixture at
 `contracts/subagent_status_contract.json` lists every backend return
 string, the expected status, and what the error substring should
 contain. Backend test (`backend/tests/test_subagent_status_contract.py`)
 and frontend test (`frontend/tests/unit/core/tasks/subtask-result.test.ts`)
 both load that fixture and assert the same cases. A wording drift on
 either side fails the matching language's test.

 4. **Round-trip serialisation pinned**: the round-trip test asserts
 `ToolMessage.model_dump_json()` → `model_validate_json()` preserves
 `additional_kwargs.subagent_status`. Catches the case where a future
 LangChain or Pydantic upgrade silently strips unknown kwargs.

 5. **Frontend status collapse documented**: the backend has five status
 values, the frontend card has three (`completed | failed |
 in_progress`). `cancelled` / `timed_out` / `polling_timed_out` all
 collapse to `failed` with the original status preserved in `error`.
 `parseSubtaskResult` returns `in_progress` for unknown values so a
 backend that ships a new enum variant before the frontend upgrades
 degrades to the legacy prefix fallback instead of getting pinned.

 ## Changes

 Backend:
 - `deerflow.subagents.status_contract` — new module exporting
 `SUBAGENT_STATUS_KEY`, `SUBAGENT_ERROR_KEY`,
 `SUBAGENT_STATUS_VALUES`, `extract_subagent_status(content)`, and
 `make_subagent_additional_kwargs(status, error)`.
 - `ToolErrorHandlingMiddleware`: new `_stamp_task_subagent_status`
 helper centralises the stamp; `wrap_tool_call` / `awrap_tool_call`
 stamp on the success path; `_build_error_message` stamps on the
 wrapper path (carrying `ExcClass: detail` into `subagent_error`).
 Non-task tools are untouched.
 - New tests: `test_subagent_status_contract.py` (19 cases from the
 shared fixture + status-enum / blank-error / unknown-status
 rejection) and `test_tool_error_handling_subagent_stamp.py`
 (middleware integration: terminal-content stamps, non-terminal
 doesn't, non-task tools untouched, async path mirrors sync,
 existing additional_kwargs survive, JSON round-trip preserved).

 Frontend:
 - `parseSubtaskResult(text, additionalKwargs?)` — prefers the
 structured stamp; falls back to the legacy prefix matcher for
 historical threads / unknown future status values.
 - `STRUCTURED_STATUS_TO_SUBTASK` documents the five→three collapse.
 - `message-list.tsx` passes `message.additional_kwargs` through.
 - `subtask-result.test.ts` adds a structured-status block + a
 fixture-driven contract block; legacy prefix tests stay green for
 the fallback path.

 Contract:
 - `contracts/subagent_status_contract.json` — single source of truth
 both languages load. Whitespace variants, varied N for polling
 timeouts, the 3 pre-execution `Error:` returns task_tool produces,
 and the middleware wrapper shape are all in there.

 ## Test plan
 - `make lint` clean (backend + frontend).
 - `pytest tests/test_subagent_status_contract.py
 tests/test_tool_error_handling_subagent_stamp.py` → 37 passed.
 - `pnpm test --run` → 103 passed (was 76, +27 new).

 ## Migration / fallback retirement

 The text-prefix fallback stays in place until backend telemetry shows
 the frontend never hits it for newly produced messages. At that point
 a follow-up PR can drop the prefix branches and keep only the
 structured-status branch.

 Refs: bytedance/deer-flow#3138 (split summary), #3107 (origin), #3131
 (prior prefix-only fix), #3146 (this issue).

 * fix(subtask): back-fill result/error from text when structured status present

 Three follow-ups on the PR #3154 review:

 1. `readStructuredStatus` no longer short-circuits the prefix parse.
 The backend currently stamps only the `subagent_status` enum value;
 the human-facing `result` body and wrapped-error message still live
 in `ToolMessage.content`. Dropping the text parse meant successful
 tasks rendered empty completed pills and wrapped failures lost their
 diagnostic. Now both shapes get composed: structured status wins,
 `result`/`error` come from text when both sides agree, and a lying
 success body under a `failed` stamp is dropped instead of leaking.

 2. Replace the ESM-incompatible `__dirname` fixture lookup in
 subtask-result.test.ts with `fileURLToPath(new URL(..., import.meta.url))`.
 The frontend package is `"type": "module"`, so the previous path
 would have thrown at runtime if anything ever changed under the
 contract directory.

 3. Drop the `$schema` reference from contracts/subagent_status_contract.json
 pointing at a file that doesn't exist in the tree.

 Three new tests cover the structured + text composition: completed
 back-fills the success body, failed back-fills the wrapper text, and
 unrecognised content under a `failed` stamp stays empty rather than
 echoing noise.') [#3146](https://github.com/bytedance/deer-flow/issues/3146) [) (](https://github.com/bytedance/deer-flow/commit/8d2e55a05f6a23d4318b910b123d182d1adb9638 'fix(subagent): structured subagent_status field over text parsing (#3146) (#3154)

 * fix(subagent): structured subagent_status field over text parsing

 Closes #3146.

 ## Why

 The frontend used to derive subtask card state by string-matching the
 leading text of the `task` tool's result. That contract surface was
 fragile — `#3107` BUG-007 and the `#3131` review both surfaced cases
 where new backend wording (`Task cancelled by user.`,
 `Task polling timed out after N minutes`, `ToolErrorHandlingMiddleware`
 exception wrappers) silently broke the card lifecycle. The frontend
 fallback kept growing more prefixes; any future rewording would break
 it again.

 ## Design

 1. **Backend → frontend contract**: `ToolMessage.additional_kwargs`
 carries `subagent_status` (one of `completed | failed | cancelled |
 timed_out | polling_timed_out`) and an optional `subagent_error`
 blob. The frontend prefers it over parsing `content`.

 2. **Centralised stamping, not 8 sprinkled stamps**: rather than have
 each of `task_tool.py`'s 5 normal-return + 3 pre-execution `Error:`
 paths remember to set `additional_kwargs`, `ToolErrorHandlingMiddleware`
 stamps the field after every task-tool call. Adding a new return
 path in `task_tool.py` cannot now skip the stamp.

 3. **Cross-language contract fixture**: the prefix→status mapping is
 the one piece both sides must agree on. The shared fixture at
 `contracts/subagent_status_contract.json` lists every backend return
 string, the expected status, and what the error substring should
 contain. Backend test (`backend/tests/test_subagent_status_contract.py`)
 and frontend test (`frontend/tests/unit/core/tasks/subtask-result.test.ts`)
 both load that fixture and assert the same cases. A wording drift on
 either side fails the matching language's test.

 4. **Round-trip serialisation pinned**: the round-trip test asserts
 `ToolMessage.model_dump_json()` → `model_validate_json()` preserves
 `additional_kwargs.subagent_status`. Catches the case where a future
 LangChain or Pydantic upgrade silently strips unknown kwargs.

 5. **Frontend status collapse documented**: the backend has five status
 values, the frontend card has three (`completed | failed |
 in_progress`). `cancelled` / `timed_out` / `polling_timed_out` all
 collapse to `failed` with the original status preserved in `error`.
 `parseSubtaskResult` returns `in_progress` for unknown values so a
 backend that ships a new enum variant before the frontend upgrades
 degrades to the legacy prefix fallback instead of getting pinned.

 ## Changes

 Backend:
 - `deerflow.subagents.status_contract` — new module exporting
 `SUBAGENT_STATUS_KEY`, `SUBAGENT_ERROR_KEY`,
 `SUBAGENT_STATUS_VALUES`, `extract_subagent_status(content)`, and
 `make_subagent_additional_kwargs(status, error)`.
 - `ToolErrorHandlingMiddleware`: new `_stamp_task_subagent_status`
 helper centralises the stamp; `wrap_tool_call` / `awrap_tool_call`
 stamp on the success path; `_build_error_message` stamps on the
 wrapper path (carrying `ExcClass: detail` into `subagent_error`).
 Non-task tools are untouched.
 - New tests: `test_subagent_status_contract.py` (19 cases from the
 shared fixture + status-enum / blank-error / unknown-status
 rejection) and `test_tool_error_handling_subagent_stamp.py`
 (middleware integration: terminal-content stamps, non-terminal
 doesn't, non-task tools untouched, async path mirrors sync,
 existing additional_kwargs survive, JSON round-trip preserved).

 Frontend:
 - `parseSubtaskResult(text, additionalKwargs?)` — prefers the
 structured stamp; falls back to the legacy prefix matcher for
 historical threads / unknown future status values.
 - `STRUCTURED_STATUS_TO_SUBTASK` documents the five→three collapse.
 - `message-list.tsx` passes `message.additional_kwargs` through.
 - `subtask-result.test.ts` adds a structured-status block + a
 fixture-driven contract block; legacy prefix tests stay green for
 the fallback path.

 Contract:
 - `contracts/subagent_status_contract.json` — single source of truth
 both languages load. Whitespace variants, varied N for polling
 timeouts, the 3 pre-execution `Error:` returns task_tool produces,
 and the middleware wrapper shape are all in there.

 ## Test plan
 - `make lint` clean (backend + frontend).
 - `pytest tests/test_subagent_status_contract.py
 tests/test_tool_error_handling_subagent_stamp.py` → 37 passed.
 - `pnpm test --run` → 103 passed (was 76, +27 new).

 ## Migration / fallback retirement

 The text-prefix fallback stays in place until backend telemetry shows
 the frontend never hits it for newly produced messages. At that point
 a follow-up PR can drop the prefix branches and keep only the
 structured-status branch.

 Refs: bytedance/deer-flow#3138 (split summary), #3107 (origin), #3131
 (prior prefix-only fix), #3146 (this issue).

 * fix(subtask): back-fill result/error from text when structured status present

 Three follow-ups on the PR #3154 review:

 1. `readStructuredStatus` no longer short-circuits the prefix parse.
 The backend currently stamps only the `subagent_status` enum value;
 the human-facing `result` body and wrapped-error message still live
 in `ToolMessage.content`. Dropping the text parse meant successful
 tasks rendered empty completed pills and wrapped failures lost their
 diagnostic. Now both shapes get composed: structured status wins,
 `result`/`error` come from text when both sides agree, and a lying
 success body under a `failed` stamp is dropped instead of leaking.

 2. Replace the ESM-incompatible `__dirname` fixture lookup in
 subtask-result.test.ts with `fileURLToPath(new URL(..., import.meta.url))`.
 The frontend package is `"type": "module"`, so the previous path
 would have thrown at runtime if anything ever changed under the
 contract directory.

 3. Drop the `$schema` reference from contracts/subagent_status_contract.json
 pointing at a file that doesn't exist in the tree.

 Three new tests cover the structured + text composition: completed
 back-fills the success body, failed back-fills the wrapper text, and
 unrecognised content under a `failed` stamp stays empty rather than
 echoing noise.') [#3154](https://github.com/bytedance/deer-flow/pull/3154) [)](https://github.com/bytedance/deer-flow/commit/8d2e55a05f6a23d4318b910b123d182d1adb9638 'fix(subagent): structured subagent_status field over text parsing (#3146) (#3154)

 * fix(subagent): structured subagent_status field over text parsing

 Closes #3146.

 ## Why

 The frontend used to derive subtask card state by string-matching the
 leading text of the `task` tool's result. That contract surface was
 fragile — `#3107` BUG-007 and the `#3131` review both surfaced cases
 where new backend wording (`Task cancelled by user.`,
 `Task polling timed out after N minutes`, `ToolErrorHandlingMiddleware`
 exception wrappers) silently broke the card lifecycle. The frontend
 fallback kept growing more prefixes; any future rewording would break
 it again.

 ## Design

 1. **Backend → frontend contract**: `ToolMessage.additional_kwargs`
 carries `subagent_status` (one of `completed | failed | cancelled |
 timed_out | polling_timed_out`) and an optional `subagent_error`
 blob. The frontend prefers it over parsing `content`.

 2. **Centralised stamping, not 8 sprinkled stamps**: rather than have
 each of `task_tool.py`'s 5 normal-return + 3 pre-execution `Error:`
 paths remember to set `additional_kwargs`, `ToolErrorHandlingMiddleware`
 stamps the field after every task-tool call. Adding a new return
 path in `task_tool.py` cannot now skip the stamp.

 3. **Cross-language contract fixture**: the prefix→status mapping is
 the one piece both sides must agree on. The shared fixture at
 `contracts/subagent_status_contract.json` lists every backend return
 string, the expected status, and what the error substring should
 contain. Backend test (`backend/tests/test_subagent_status_contract.py`)
 and frontend test (`frontend/tests/unit/core/tasks/subtask-result.test.ts`)
 both load that fixture and assert the same cases. A wording drift on
 either side fails the matching language's test.

 4. **Round-trip serialisation pinned**: the round-trip test asserts
 `ToolMessage.model_dump_json()` → `model_validate_json()` preserves
 `additional_kwargs.subagent_status`. Catches the case where a future
 LangChain or Pydantic upgrade silently strips unknown kwargs.

 5. **Frontend status collapse documented**: the backend has five status
 values, the frontend card has three (`completed | failed |
 in_progress`). `cancelled` / `timed_out` / `polling_timed_out` all
 collapse to `failed` with the original status preserved in `error`.
 `parseSubtaskResult` returns `in_progress` for unknown values so a
 backend that ships a new enum variant before the frontend upgrades
 degrades to the legacy prefix fallback instead of getting pinned.

 ## Changes

 Backend:
 - `deerflow.subagents.status_contract` — new module exporting
 `SUBAGENT_STATUS_KEY`, `SUBAGENT_ERROR_KEY`,
 `SUBAGENT_STATUS_VALUES`, `extract_subagent_status(content)`, and
 `make_subagent_additional_kwargs(status, error)`.
 - `ToolErrorHandlingMiddleware`: new `_stamp_task_subagent_status`
 helper centralises the stamp; `wrap_tool_call` / `awrap_tool_call`
 stamp on the success path; `_build_error_message` stamps on the
 wrapper path (carrying `ExcClass: detail` into `subagent_error`).
 Non-task tools are untouched.
 - New tests: `test_subagent_status_contract.py` (19 cases from the
 shared fixture + status-enum / blank-error / unknown-status
 rejection) and `test_tool_error_handling_subagent_stamp.py`
 (middleware integration: terminal-content stamps, non-terminal
 doesn't, non-task tools untouched, async path mirrors sync,
 existing additional_kwargs survive, JSON round-trip preserved).

 Frontend:
 - `parseSubtaskResult(text, additionalKwargs?)` — prefers the
 structured stamp; falls back to the legacy prefix matcher for
 historical threads / unknown future status values.
 - `STRUCTURED_STATUS_TO_SUBTASK` documents the five→three collapse.
 - `message-list.tsx` passes `message.additional_kwargs` through.
 - `subtask-result.test.ts` adds a structured-status block + a
 fixture-driven contract block; legacy prefix tests stay green for
 the fallback path.

 Contract:
 - `contracts/subagent_status_contract.json` — single source of truth
 both languages load. Whitespace variants, varied N for polling
 timeouts, the 3 pre-execution `Error:` returns task_tool produces,
 and the middleware wrapper shape are all in there.

 ## Test plan
 - `make lint` clean (backend + frontend).
 - `pytest tests/test_subagent_status_contract.py
 tests/test_tool_error_handling_subagent_stamp.py` → 37 passed.
 - `pnpm test --run` → 103 passed (was 76, +27 new).

 ## Migration / fallback retirement

 The text-prefix fallback stays in place until backend telemetry shows
 the frontend never hits it for newly produced messages. At that point
 a follow-up PR can drop the prefix branches and keep only the
 structured-status branch.

 Refs: bytedance/deer-flow#3138 (split summary), #3107 (origin), #3131
 (prior prefix-only fix), #3146 (this issue).

 * fix(subtask): back-fill result/error from text when structured status present

 Three follow-ups on the PR #3154 review:

 1. `readStructuredStatus` no longer short-circuits the prefix parse.
 The backend currently stamps only the `subagent_status` enum value;
 the human-facing `result` body and wrapped-error message still live
 in `ToolMessage.content`. Dropping the text parse meant successful
 tasks rendered empty completed pills and wrapped failures lost their
 diagnostic. Now both shapes get composed: structured status wins,
 `result`/`error` come from text when both sides agree, and a lying
 success body under a `failed` stamp is dropped instead of leaking.

 2. Replace the ESM-incompatible `__dirname` fixture lookup in
 subtask-result.test.ts with `fileURLToPath(new URL(..., import.meta.url))`.
 The frontend package is `"type": "module"`, so the previous path
 would have thrown at runtime if anything ever changed under the
 contract directory.

 3. Drop the `$schema` reference from contracts/subagent_status_contract.json
 pointing at a file that doesn't exist in the tree.

 Three new tests cover the structured + text composition: completed
 back-fills the success body, failed back-fills the wrapper text, and
 unrecognised content under a `failed` stamp stays empty rather than
 echoing noise.')

 Show description for 8d2e55a

 [![fancyboi999](https://avatars.githubusercontent.com/u/135568692?v=4&size=32)](https://github.com/fancyboi999) [fancyboi999](https://github.com/bytedance/deer-flow/commits?author=fancyboi999)

 authoredJun 7, 2026

 ·

 8 / 8

 Verified

 [8d2e55a](https://github.com/bytedance/deer-flow/commit/8d2e55a05f6a23d4318b910b123d182d1adb9638)View commit details

 Copy full SHA for 8d2e55a

 View code at this pointBrowse repository at this point

### End of commit history for this file