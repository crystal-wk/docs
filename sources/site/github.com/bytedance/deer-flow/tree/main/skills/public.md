# Source: https://github.com/bytedance/deer-flow/tree/main/skills/public

### Uh oh!

There was an error while loading. [Please reload this page]().

[bytedance](https://github.com/bytedance) / **[deer-flow](https://github.com/bytedance/deer-flow)** Public

- [Notifications](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow) You must be signed in to change notification settings
- [Fork 10.9k](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow)
- [Star 79.8k](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow)

 ## FilesExpand file tree

main

/

# public

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

[feat(skills): add skill review quality gate (](https://github.com/bytedance/deer-flow/commit/41658c5ff40f3f1a8a3bffcb8bc58a39117d44e2) [#4037](https://github.com/bytedance/deer-flow/pull/4037) [)](https://github.com/bytedance/deer-flow/commit/41658c5ff40f3f1a8a3bffcb8bc58a39117d44e2)

Open commit detailssuccess

Jul 11, 2026

[41658c5](https://github.com/bytedance/deer-flow/commit/41658c5ff40f3f1a8a3bffcb8bc58a39117d44e2) · Jul 11, 2026

## History

[History](https://github.com/bytedance/deer-flow/commits/main/skills/public)

Open commit details

History

## FilesExpand file tree

main

/

# public

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

[..](https://github.com/bytedance/deer-flow/tree/main/skills) |
| 

[academic-paper-review](https://github.com/bytedance/deer-flow/tree/main/skills/public/academic-paper-review 'academic-paper-review')

 | 

[academic-paper-review](https://github.com/bytedance/deer-flow/tree/main/skills/public/academic-paper-review 'academic-paper-review')

 | 

[feat(skills): add academic-paper-review, code-documentation, and news…](https://github.com/bytedance/deer-flow/commit/8bb14fa1a7bf7e6ee0631db4db9168962edbc31f 'feat(skills): add academic-paper-review, code-documentation, and newsletter-generation skills (#1861)

Add three new public skills to enhance DeerFlow's content creation capabilities:

- **academic-paper-review**: Structured peer-review-quality analysis of
 research papers following top-venue review standards (NeurIPS, ICML, ACL).
 Covers methodology assessment, contribution evaluation, literature
 positioning, and constructive feedback with a 3-phase workflow.

- **code-documentation**: Professional documentation generation for software
 projects, including README generation, API reference docs, architecture
 documentation with Mermaid diagrams, and inline code documentation
 supporting Python, TypeScript, Go, Rust, and Java conventions.

- **newsletter-generation**: Curated newsletter creation with research
 workflow, supporting daily digest, weekly roundup, deep-dive, and industry
 briefing formats. Includes audience-specific tone adaptation and
 multi-source content curation.

All skills:
- Follow the existing SKILL.md frontmatter convention (name + description)
- Pass the official _validate_skill_frontmatter() validation
- Use hyphen-case naming consistent with existing skills
- Contain only allowed frontmatter properties
- Include comprehensive examples, quality checklists, and output templates')

 | 

Apr 5, 2026

 |
| 

[bootstrap](https://github.com/bytedance/deer-flow/tree/main/skills/public/bootstrap 'bootstrap')

 | 

[bootstrap](https://github.com/bytedance/deer-flow/tree/main/skills/public/bootstrap 'bootstrap')

 | 

[fix(skills): validate bundled SKILL.md front-matter in CI (](https://github.com/bytedance/deer-flow/commit/b90f219bd179766227a02f8e33cfa57ba5086d66 'fix(skills): validate bundled SKILL.md front-matter in CI (fixes #2443) (#2457)

* fix(skills): validate bundled SKILL.md front-matter in CI (fixes #2443)

Adds a parametrized backend test that runs `_validate_skill_frontmatter`
against every bundled SKILL.md under `skills/public/`, so a broken
front-matter fails CI with a per-skill error message instead of
surfacing as a runtime gateway-load warning.

The new test caught two pre-existing breakages on `main` and fixes them:

* `bootstrap/SKILL.md`: the unquoted description had a second `:` mid-line
 ("Also trigger for updates: ..."), which YAML parses as a nested mapping
 ("mapping values are not allowed here"). Rewrites the description as a
 folded scalar (`>-`), which preserves the original wording (including the
 embedded colon, double quotes, and apostrophes) without further escaping.
 This complements PR #2436 (single-file colon→hyphen patch) with a more
 general convention that survives future edits.

* `chart-visualization/SKILL.md`: used `dependency:` which is not in
 `ALLOWED_FRONTMATTER_PROPERTIES`. Renamed to `compatibility:`, the
 documented field for "Required tools, dependencies" per skill-creator.
 No code reads `dependency` (verified by grep across backend/).

* Apply suggestions from code review

Co-authored-by: Copilot Autofix powered by AI <175728472+Copilot@users.noreply.github.com>

* Fix the lint error

---------

Co-authored-by: Willem Jiang <willem.jiang@gmail.com>
Co-authored-by: Copilot Autofix powered by AI <175728472+Copilot@users.noreply.github.com>')[fixes](https://github.com/bytedance/deer-flow/commit/b90f219bd179766227a02f8e33cfa57ba5086d66 'fix(skills): validate bundled SKILL.md front-matter in CI (fixes #2443) (#2457)

* fix(skills): validate bundled SKILL.md front-matter in CI (fixes #2443)

Adds a parametrized backend test that runs `_validate_skill_frontmatter`
against every bundled SKILL.md under `skills/public/`, so a broken
front-matter fails CI with a per-skill error message instead of
surfacing as a runtime gateway-load warning.

The new test caught two pre-existing breakages on `main` and fixes them:

* `bootstrap/SKILL.md`: the unquoted description had a second `:` mid-line
 ("Also trigger for updates: ..."), which YAML parses as a nested mapping
 ("mapping values are not allowed here"). Rewrites the description as a
 folded scalar (`>-`), which preserves the original wording (including the
 embedded colon, double quotes, and apostrophes) without further escaping.
 This complements PR #2436 (single-file colon→hyphen patch) with a more
 general convention that survives future edits.

* `chart-visualization/SKILL.md`: used `dependency:` which is not in
 `ALLOWED_FRONTMATTER_PROPERTIES`. Renamed to `compatibility:`, the
 documented field for "Required tools, dependencies" per skill-creator.
 No code reads `dependency` (verified by grep across backend/).

* Apply suggestions from code review

Co-authored-by: Copilot Autofix powered by AI <175728472+Copilot@users.noreply.github.com>

* Fix the lint error

---------

Co-authored-by: Willem Jiang <willem.jiang@gmail.com>
Co-authored-by: Copilot Autofix powered by AI <175728472+Copilot@users.noreply.github.com>') [#2443](https://github.com/bytedance/deer-flow/issues/2443) [)…](https://github.com/bytedance/deer-flow/commit/b90f219bd179766227a02f8e33cfa57ba5086d66 'fix(skills): validate bundled SKILL.md front-matter in CI (fixes #2443) (#2457)

* fix(skills): validate bundled SKILL.md front-matter in CI (fixes #2443)

Adds a parametrized backend test that runs `_validate_skill_frontmatter`
against every bundled SKILL.md under `skills/public/`, so a broken
front-matter fails CI with a per-skill error message instead of
surfacing as a runtime gateway-load warning.

The new test caught two pre-existing breakages on `main` and fixes them:

* `bootstrap/SKILL.md`: the unquoted description had a second `:` mid-line
 ("Also trigger for updates: ..."), which YAML parses as a nested mapping
 ("mapping values are not allowed here"). Rewrites the description as a
 folded scalar (`>-`), which preserves the original wording (including the
 embedded colon, double quotes, and apostrophes) without further escaping.
 This complements PR #2436 (single-file colon→hyphen patch) with a more
 general convention that survives future edits.

* `chart-visualization/SKILL.md`: used `dependency:` which is not in
 `ALLOWED_FRONTMATTER_PROPERTIES`. Renamed to `compatibility:`, the
 documented field for "Required tools, dependencies" per skill-creator.
 No code reads `dependency` (verified by grep across backend/).

* Apply suggestions from code review

Co-authored-by: Copilot Autofix powered by AI <175728472+Copilot@users.noreply.github.com>

* Fix the lint error

---------

Co-authored-by: Willem Jiang <willem.jiang@gmail.com>
Co-authored-by: Copilot Autofix powered by AI <175728472+Copilot@users.noreply.github.com>')

 | 

Apr 23, 2026

 |
| 

[chart-visualization](https://github.com/bytedance/deer-flow/tree/main/skills/public/chart-visualization 'chart-visualization')

 | 

[chart-visualization](https://github.com/bytedance/deer-flow/tree/main/skills/public/chart-visualization 'chart-visualization')

 | 

[fix(skills): validate bundled SKILL.md front-matter in CI (](https://github.com/bytedance/deer-flow/commit/b90f219bd179766227a02f8e33cfa57ba5086d66 'fix(skills): validate bundled SKILL.md front-matter in CI (fixes #2443) (#2457)

* fix(skills): validate bundled SKILL.md front-matter in CI (fixes #2443)

Adds a parametrized backend test that runs `_validate_skill_frontmatter`
against every bundled SKILL.md under `skills/public/`, so a broken
front-matter fails CI with a per-skill error message instead of
surfacing as a runtime gateway-load warning.

The new test caught two pre-existing breakages on `main` and fixes them:

* `bootstrap/SKILL.md`: the unquoted description had a second `:` mid-line
 ("Also trigger for updates: ..."), which YAML parses as a nested mapping
 ("mapping values are not allowed here"). Rewrites the description as a
 folded scalar (`>-`), which preserves the original wording (including the
 embedded colon, double quotes, and apostrophes) without further escaping.
 This complements PR #2436 (single-file colon→hyphen patch) with a more
 general convention that survives future edits.

* `chart-visualization/SKILL.md`: used `dependency:` which is not in
 `ALLOWED_FRONTMATTER_PROPERTIES`. Renamed to `compatibility:`, the
 documented field for "Required tools, dependencies" per skill-creator.
 No code reads `dependency` (verified by grep across backend/).

* Apply suggestions from code review

Co-authored-by: Copilot Autofix powered by AI <175728472+Copilot@users.noreply.github.com>

* Fix the lint error

---------

Co-authored-by: Willem Jiang <willem.jiang@gmail.com>
Co-authored-by: Copilot Autofix powered by AI <175728472+Copilot@users.noreply.github.com>')[fixes](https://github.com/bytedance/deer-flow/commit/b90f219bd179766227a02f8e33cfa57ba5086d66 'fix(skills): validate bundled SKILL.md front-matter in CI (fixes #2443) (#2457)

* fix(skills): validate bundled SKILL.md front-matter in CI (fixes #2443)

Adds a parametrized backend test that runs `_validate_skill_frontmatter`
against every bundled SKILL.md under `skills/public/`, so a broken
front-matter fails CI with a per-skill error message instead of
surfacing as a runtime gateway-load warning.

The new test caught two pre-existing breakages on `main` and fixes them:

* `bootstrap/SKILL.md`: the unquoted description had a second `:` mid-line
 ("Also trigger for updates: ..."), which YAML parses as a nested mapping
 ("mapping values are not allowed here"). Rewrites the description as a
 folded scalar (`>-`), which preserves the original wording (including the
 embedded colon, double quotes, and apostrophes) without further escaping.
 This complements PR #2436 (single-file colon→hyphen patch) with a more
 general convention that survives future edits.

* `chart-visualization/SKILL.md`: used `dependency:` which is not in
 `ALLOWED_FRONTMATTER_PROPERTIES`. Renamed to `compatibility:`, the
 documented field for "Required tools, dependencies" per skill-creator.
 No code reads `dependency` (verified by grep across backend/).

* Apply suggestions from code review

Co-authored-by: Copilot Autofix powered by AI <175728472+Copilot@users.noreply.github.com>

* Fix the lint error

---------

Co-authored-by: Willem Jiang <willem.jiang@gmail.com>
Co-authored-by: Copilot Autofix powered by AI <175728472+Copilot@users.noreply.github.com>') [#2443](https://github.com/bytedance/deer-flow/issues/2443) [)…](https://github.com/bytedance/deer-flow/commit/b90f219bd179766227a02f8e33cfa57ba5086d66 'fix(skills): validate bundled SKILL.md front-matter in CI (fixes #2443) (#2457)

* fix(skills): validate bundled SKILL.md front-matter in CI (fixes #2443)

Adds a parametrized backend test that runs `_validate_skill_frontmatter`
against every bundled SKILL.md under `skills/public/`, so a broken
front-matter fails CI with a per-skill error message instead of
surfacing as a runtime gateway-load warning.

The new test caught two pre-existing breakages on `main` and fixes them:

* `bootstrap/SKILL.md`: the unquoted description had a second `:` mid-line
 ("Also trigger for updates: ..."), which YAML parses as a nested mapping
 ("mapping values are not allowed here"). Rewrites the description as a
 folded scalar (`>-`), which preserves the original wording (including the
 embedded colon, double quotes, and apostrophes) without further escaping.
 This complements PR #2436 (single-file colon→hyphen patch) with a more
 general convention that survives future edits.

* `chart-visualization/SKILL.md`: used `dependency:` which is not in
 `ALLOWED_FRONTMATTER_PROPERTIES`. Renamed to `compatibility:`, the
 documented field for "Required tools, dependencies" per skill-creator.
 No code reads `dependency` (verified by grep across backend/).

* Apply suggestions from code review

Co-authored-by: Copilot Autofix powered by AI <175728472+Copilot@users.noreply.github.com>

* Fix the lint error

---------

Co-authored-by: Willem Jiang <willem.jiang@gmail.com>
Co-authored-by: Copilot Autofix powered by AI <175728472+Copilot@users.noreply.github.com>')

 | 

Apr 23, 2026

 |
| 

[claude-to-deerflow](https://github.com/bytedance/deer-flow/tree/main/skills/public/claude-to-deerflow 'claude-to-deerflow')

 | 

[claude-to-deerflow](https://github.com/bytedance/deer-flow/tree/main/skills/public/claude-to-deerflow 'claude-to-deerflow')

 | 

[docs: align runtime docs with gateway mode (](https://github.com/bytedance/deer-flow/commit/84f88b6610e5c6384735e703809bc8b35e33dacb 'docs: align runtime docs with gateway mode (#2868)

Co-authored-by: Willem Jiang <willem.jiang@gmail.com>') [#2868](https://github.com/bytedance/deer-flow/pull/2868) [)](https://github.com/bytedance/deer-flow/commit/84f88b6610e5c6384735e703809bc8b35e33dacb 'docs: align runtime docs with gateway mode (#2868)

Co-authored-by: Willem Jiang <willem.jiang@gmail.com>')

 | 

May 12, 2026

 |
| 

[code-documentation](https://github.com/bytedance/deer-flow/tree/main/skills/public/code-documentation 'code-documentation')

 | 

[code-documentation](https://github.com/bytedance/deer-flow/tree/main/skills/public/code-documentation 'code-documentation')

 | 

[feat(skills): add academic-paper-review, code-documentation, and news…](https://github.com/bytedance/deer-flow/commit/8bb14fa1a7bf7e6ee0631db4db9168962edbc31f 'feat(skills): add academic-paper-review, code-documentation, and newsletter-generation skills (#1861)

Add three new public skills to enhance DeerFlow's content creation capabilities:

- **academic-paper-review**: Structured peer-review-quality analysis of
 research papers following top-venue review standards (NeurIPS, ICML, ACL).
 Covers methodology assessment, contribution evaluation, literature
 positioning, and constructive feedback with a 3-phase workflow.

- **code-documentation**: Professional documentation generation for software
 projects, including README generation, API reference docs, architecture
 documentation with Mermaid diagrams, and inline code documentation
 supporting Python, TypeScript, Go, Rust, and Java conventions.

- **newsletter-generation**: Curated newsletter creation with research
 workflow, supporting daily digest, weekly roundup, deep-dive, and industry
 briefing formats. Includes audience-specific tone adaptation and
 multi-source content curation.

All skills:
- Follow the existing SKILL.md frontmatter convention (name + description)
- Pass the official _validate_skill_frontmatter() validation
- Use hyphen-case naming consistent with existing skills
- Contain only allowed frontmatter properties
- Include comprehensive examples, quality checklists, and output templates')

 | 

Apr 5, 2026

 |
| 

[consulting-analysis](https://github.com/bytedance/deer-flow/tree/main/skills/public/consulting-analysis 'consulting-analysis')

 | 

[consulting-analysis](https://github.com/bytedance/deer-flow/tree/main/skills/public/consulting-analysis 'consulting-analysis')

 | 

[fix(skill): enhance data authenticity protocols and clarify reporting…](https://github.com/bytedance/deer-flow/commit/33595f0bac29df1c4ce20a28762504abd4dcb80d 'fix(skill): enhance data authenticity protocols and clarify reporting guidelines (#905)')

 | 

Feb 25, 2026

 |
| 

[data-analysis](https://github.com/bytedance/deer-flow/tree/main/skills/public/data-analysis 'data-analysis')

 | 

[data-analysis](https://github.com/bytedance/deer-flow/tree/main/skills/public/data-analysis 'data-analysis')

 | 

[fix: remove unnecessary f-string prefixes and unused import (](https://github.com/bytedance/deer-flow/commit/085c13edc7c2b913fd432422c726fce0f2f81d66 'fix: remove unnecessary f-string prefixes and unused import (#2352)

- Remove f-string prefix on 7 strings with no placeholders (F541)
 in analyze.py, aggregate_benchmark.py, run_loop.py, generate_review.py
- Remove unused `os` import in quick_validate.py (F401)

Found by ruff via HUMMBL Arbiter (https://hummbl.io/audit).') [#2352](https://github.com/bytedance/deer-flow/pull/2352) [)](https://github.com/bytedance/deer-flow/commit/085c13edc7c2b913fd432422c726fce0f2f81d66 'fix: remove unnecessary f-string prefixes and unused import (#2352)

- Remove f-string prefix on 7 strings with no placeholders (F541)
 in analyze.py, aggregate_benchmark.py, run_loop.py, generate_review.py
- Remove unused `os` import in quick_validate.py (F401)

Found by ruff via HUMMBL Arbiter (https://hummbl.io/audit).')

 | 

Apr 21, 2026

 |
| 

[deep-research](https://github.com/bytedance/deer-flow/tree/main/skills/public/deep-research 'deep-research')

 | 

[deep-research](https://github.com/bytedance/deer-flow/tree/main/skills/public/deep-research 'deep-research')

 | 

[feat(agent):Supports custom agent and chat experience with refactoring (](https://github.com/bytedance/deer-flow/commit/7de94394d4295182701ffb47e938e7c39b963091 'feat(agent):Supports custom agent and chat experience with refactoring (#957)

* feat: add agent management functionality with creation, editing, and deletion

* feat: enhance agent creation and chat experience

- Added AgentWelcome component to display agent description on new thread creation.
- Improved agent name validation with availability check during agent creation.
- Updated NewAgentPage to handle agent creation flow more effectively, including enhanced error handling and user feedback.
- Refactored chat components to streamline message handling and improve user experience.
- Introduced new bootstrap skill for personalized onboarding conversations, including detailed conversation phases and a structured SOUL.md template.
- Updated localization files to reflect new features and error messages.
- General code cleanup and optimizations across various components and hooks.

* Refactor workspace layout and agent management components

- Updated WorkspaceLayout to use useLayoutEffect for sidebar state initialization.
- Removed unused AgentFormDialog and related edit functionality from AgentCard.
- Introduced ArtifactTrigger component to manage artifact visibility.
- Enhanced ChatBox to handle artifact selection and display.
- Improved message list rendering logic to avoid loading states.
- Updated localization files to remove deprecated keys and add new translations.
- Refined hooks for local settings and thread management to improve performance and clarity.
- Added temporal awareness guidelines to deep research skill documentation.

* feat: refactor chat components and introduce thread management hooks

* feat: improve artifact file detail preview logic and clean up console logs

* feat: refactor lead agent creation logic and improve logging details

* feat: validate agent name format and enhance error handling in agent setup

* feat: simplify thread search query by removing unnecessary metadata

* feat: update query key in useDeleteThread and useRenameThread for consistency

* feat: add isMock parameter to thread and artifact handling for improved testing

* fix: reorder import of setup_agent for consistency in builtins module

* feat: append mock parameter to thread links in CaseStudySection for testing purposes

* fix: update load_agent_soul calls to use cfg.name for improved clarity

* fix: update date format in apply_prompt_template for consistency

* feat: integrate isMock parameter into artifact content loading for enhanced testing

* docs: add license section to SKILL.md for clarity and attribution

* feat(agent): enhance model resolution and agent configuration handling

* chore: remove unused import of _resolve_model_name from agents

* feat(agent): remove unused field

* fix(agent): set default value for requested_model_name in _resolve_model_name function

* feat(agent): update get_available_tools call to handle optional agent_config and improve middleware function signature

---------

Co-authored-by: Willem Jiang <willem.jiang@gmail.com>')

 | 

Mar 3, 2026

 |
| 

[find-skills](https://github.com/bytedance/deer-flow/tree/main/skills/public/find-skills 'find-skills')

 | 

[find-skills](https://github.com/bytedance/deer-flow/tree/main/skills/public/find-skills 'find-skills')

 | 

[feat: add find-skills skill for discovering agent skills](https://github.com/bytedance/deer-flow/commit/f082ef3d87903ba078a36c7cc524d5a362a211ad 'feat: add find-skills skill for discovering agent skills

Co-Authored-By: Claude Opus 4.5 <noreply@anthropic.com>')

 | 

Feb 1, 2026

 |
| 

[frontend-design](https://github.com/bytedance/deer-flow/tree/main/skills/public/frontend-design 'frontend-design')

 | 

[frontend-design](https://github.com/bytedance/deer-flow/tree/main/skills/public/frontend-design 'frontend-design')

 | 

[refactor: refine skills](https://github.com/bytedance/deer-flow/commit/08101aa432917ed04e3d548b2305a7d854e53cac 'refactor: refine skills')

 | 

Jan 21, 2026

 |
| 

[github-deep-research](https://github.com/bytedance/deer-flow/tree/main/skills/public/github-deep-research 'github-deep-research')

 | 

[github-deep-research](https://github.com/bytedance/deer-flow/tree/main/skills/public/github-deep-research 'github-deep-research')

 | 

[feat: Support gitHub PAT configuration for higher github API accessin…](https://github.com/bytedance/deer-flow/commit/6b13f5c9fb052b2efee1e76edc5af91b9244a74d 'feat: Support gitHub PAT configuration for higher github API accessing rate. (#1374)

* feat: Add github PAT configs, allowing larger github API rates.

* Update comment to English for better clarity

* fix: Remove unused config lines in config.example.yaml and unreferenced declarations in app_config. Fix lint issues and update documentation.

* fix: Remove unused imports, and passed the ruff check.

---------

Co-authored-by: Willem Jiang <willem.jiang@gmail.com>')

 | 

Mar 27, 2026

 |
| 

[image-generation](https://github.com/bytedance/deer-flow/tree/main/skills/public/image-generation 'image-generation')

 | 

[image-generation](https://github.com/bytedance/deer-flow/tree/main/skills/public/image-generation 'image-generation')

 | 

[feat: MiniMax provider for image/video/podcast skills + new music-gen…](https://github.com/bytedance/deer-flow/commit/cd5bedaa743832da10ded26e672db8c00085d988 'feat: MiniMax provider for image/video/podcast skills + new music-generation skill (#3437)

* docs(spec): MiniMax integration for generation skills + new music skill

Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>

* docs(plan): MiniMax generation providers implementation plan

Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>

* test(skills): add importlib loader + FakeResp for skill tests

* test(skills): register loaded module in sys.modules; raise requests.HTTPError in FakeResp

* feat(image-generation): add MiniMax provider with env auto-detect

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>

* refactor(image-generation): guard unknown provider, derive ref MIME, strengthen tests

Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>

* feat(video-generation): add MiniMax provider with async poll/download

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>

* refactor(video-generation): surface base_resp errors while polling; add timeout test

* feat(podcast-generation): add MiniMax t2a_v2 provider with env auto-detect

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>

* refactor(podcast-generation): restore TTS credential guard; add volcengine + voice tests

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>

* feat(music-generation): new MiniMax music skill via skill-creator

Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>

* refactor(music-generation): treat empty lyrics as absent; test no-audio-data path

* refactor(skills): add request timeouts to MiniMax network calls

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>

* Potential fix for pull request finding 'Explicit returns mixed with implicit (fall through) returns'

Co-authored-by: Copilot Autofix powered by AI <223894421+github-code-quality[bot]@users.noreply.github.com>

* fix(models): strip inconsistent user-message names for MiniMax chat

DeerFlow middlewares tag user messages with provenance names (user-input, summary, loop_warning); langchain serializes them into the OpenAI-compatible payload and MiniMax rejects mismatched user-message names with "user name must be consistent (2013)". PatchedChatMiniMax now drops the per-message name from user-role messages. Point the config.example MiniMax models at PatchedChatMiniMax so they also get reasoning_content mapping.

Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>

* feat(image-generation): MiniMax sends JSON prompt field, guard 1500-char limit

MiniMax image-01 takes one text string capped at 1500 chars, but the skill was sending the whole structured JSON. The MiniMax provider now extracts the JSON `prompt` field (relying on prompt_optimizer to expand it) and fails fast with a clear error before calling the API when that field exceeds 1500 chars. Authoring stays provider-agnostic; Gemini still receives the full JSON.

Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>

* feat(podcast-generation): per-provider TTS concurrency and retry/backoff

Each TTS provider owns its concurrency internally — MiniMax runs single-threaded to reduce rate-limit failures, Volcengine keeps 4 workers — with automatic retry and backoff on transient HTTP and base_resp errors. No caller-facing concurrency knob.

Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>

* fix(skills): address Copilot review comments on generation skills

- video: add raise_for_status + timeout to the Gemini download/POST/poll calls so non-2xx responses surface as clear HTTP errors instead of JSON/KeyError or hangs
- video: check the task Fail status before the generic base_resp check so the failure keeps its task_id context
- video/image: create the output file parent directory before writing (matching music-generation) so nested output paths do not raise FileNotFoundError
- music: require a non-empty prompt and fail fast with ValueError instead of sending an empty prompt to the API

Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>

* fix(scripts): reclaim dev ports across worktrees in make stop/dev

All deer-flow worktrees (main checkout + linked worktrees) hardcode the same dev ports (8001/3000/2026), so a service started from any worktree must be reclaimable from another. stop_all now resolves the set of worktree roots (DEERFLOW_ROOTS) and treats a process as deer-flow-owned when its open files live under any of them. It also force-kills survivors on 2026 alongside 8001/3000, fixing `make dev` aborting on the nginx port preflight when a prior nginx lingered on 2026.

Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>

* fix(view-image): hide the injected image-context message from the UI

ViewImageMiddleware injects a HumanMessage (text + base64 images) so the vision model can see viewed images, but it was the only internal injector that set neither hide_from_ui nor a hidden name, so it leaked into the chat UI (and IM channels) as a user bubble reading "Here are the images you've viewed:". Mark it with additional_kwargs={"hide_from_ui": True}, matching todo/dynamic_context injections, which the frontend isHiddenFromUIMessage and the channel sender already honor. The model still receives the full content.

Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>

* fix(minimax): mark M2.7 models as text-only (no vision)

MiniMax M2.7 / M2.7-highspeed do not support vision; only M3 does. The
provider config asserted vision support for M2.7 in four places.

- config.example.yaml: 4 M2.7 entries -> supports_vision: false
- backend/docs/CONFIGURATION.md: M2.7 + highspeed -> supports_vision: false
- wizard: add LLMProvider.model_vision_overrides + extra_config_for() so
 selecting an M2.7 model writes supports_vision: false while M3 (default)
 keeps vision; wire it through setup_wizard.py
- tests: M2.7-highspeed fixture -> supports_vision=False; add
 test_minimax_vision_is_per_model

Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>

---------

Co-authored-by: Claude Opus 4.8 (1M context) <noreply@anthropic.com>
Co-authored-by: Willem Jiang <willem.jiang@gmail.com>
Co-authored-by: Copilot Autofix powered by AI <223894421+github-code-quality[bot]@users.noreply.github.com>')

 | 

Jun 8, 2026

 |
| 

[music-generation](https://github.com/bytedance/deer-flow/tree/main/skills/public/music-generation 'music-generation')

 | 

[music-generation](https://github.com/bytedance/deer-flow/tree/main/skills/public/music-generation 'music-generation')

 | 

[feat: MiniMax provider for image/video/podcast skills + new music-gen…](https://github.com/bytedance/deer-flow/commit/cd5bedaa743832da10ded26e672db8c00085d988 'feat: MiniMax provider for image/video/podcast skills + new music-generation skill (#3437)

* docs(spec): MiniMax integration for generation skills + new music skill

Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>

* docs(plan): MiniMax generation providers implementation plan

Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>

* test(skills): add importlib loader + FakeResp for skill tests

* test(skills): register loaded module in sys.modules; raise requests.HTTPError in FakeResp

* feat(image-generation): add MiniMax provider with env auto-detect

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>

* refactor(image-generation): guard unknown provider, derive ref MIME, strengthen tests

Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>

* feat(video-generation): add MiniMax provider with async poll/download

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>

* refactor(video-generation): surface base_resp errors while polling; add timeout test

* feat(podcast-generation): add MiniMax t2a_v2 provider with env auto-detect

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>

* refactor(podcast-generation): restore TTS credential guard; add volcengine + voice tests

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>

* feat(music-generation): new MiniMax music skill via skill-creator

Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>

* refactor(music-generation): treat empty lyrics as absent; test no-audio-data path

* refactor(skills): add request timeouts to MiniMax network calls

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>

* Potential fix for pull request finding 'Explicit returns mixed with implicit (fall through) returns'

Co-authored-by: Copilot Autofix powered by AI <223894421+github-code-quality[bot]@users.noreply.github.com>

* fix(models): strip inconsistent user-message names for MiniMax chat

DeerFlow middlewares tag user messages with provenance names (user-input, summary, loop_warning); langchain serializes them into the OpenAI-compatible payload and MiniMax rejects mismatched user-message names with "user name must be consistent (2013)". PatchedChatMiniMax now drops the per-message name from user-role messages. Point the config.example MiniMax models at PatchedChatMiniMax so they also get reasoning_content mapping.

Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>

* feat(image-generation): MiniMax sends JSON prompt field, guard 1500-char limit

MiniMax image-01 takes one text string capped at 1500 chars, but the skill was sending the whole structured JSON. The MiniMax provider now extracts the JSON `prompt` field (relying on prompt_optimizer to expand it) and fails fast with a clear error before calling the API when that field exceeds 1500 chars. Authoring stays provider-agnostic; Gemini still receives the full JSON.

Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>

* feat(podcast-generation): per-provider TTS concurrency and retry/backoff

Each TTS provider owns its concurrency internally — MiniMax runs single-threaded to reduce rate-limit failures, Volcengine keeps 4 workers — with automatic retry and backoff on transient HTTP and base_resp errors. No caller-facing concurrency knob.

Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>

* fix(skills): address Copilot review comments on generation skills

- video: add raise_for_status + timeout to the Gemini download/POST/poll calls so non-2xx responses surface as clear HTTP errors instead of JSON/KeyError or hangs
- video: check the task Fail status before the generic base_resp check so the failure keeps its task_id context
- video/image: create the output file parent directory before writing (matching music-generation) so nested output paths do not raise FileNotFoundError
- music: require a non-empty prompt and fail fast with ValueError instead of sending an empty prompt to the API

Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>

* fix(scripts): reclaim dev ports across worktrees in make stop/dev

All deer-flow worktrees (main checkout + linked worktrees) hardcode the same dev ports (8001/3000/2026), so a service started from any worktree must be reclaimable from another. stop_all now resolves the set of worktree roots (DEERFLOW_ROOTS) and treats a process as deer-flow-owned when its open files live under any of them. It also force-kills survivors on 2026 alongside 8001/3000, fixing `make dev` aborting on the nginx port preflight when a prior nginx lingered on 2026.

Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>

* fix(view-image): hide the injected image-context message from the UI

ViewImageMiddleware injects a HumanMessage (text + base64 images) so the vision model can see viewed images, but it was the only internal injector that set neither hide_from_ui nor a hidden name, so it leaked into the chat UI (and IM channels) as a user bubble reading "Here are the images you've viewed:". Mark it with additional_kwargs={"hide_from_ui": True}, matching todo/dynamic_context injections, which the frontend isHiddenFromUIMessage and the channel sender already honor. The model still receives the full content.

Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>

* fix(minimax): mark M2.7 models as text-only (no vision)

MiniMax M2.7 / M2.7-highspeed do not support vision; only M3 does. The
provider config asserted vision support for M2.7 in four places.

- config.example.yaml: 4 M2.7 entries -> supports_vision: false
- backend/docs/CONFIGURATION.md: M2.7 + highspeed -> supports_vision: false
- wizard: add LLMProvider.model_vision_overrides + extra_config_for() so
 selecting an M2.7 model writes supports_vision: false while M3 (default)
 keeps vision; wire it through setup_wizard.py
- tests: M2.7-highspeed fixture -> supports_vision=False; add
 test_minimax_vision_is_per_model

Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>

---------

Co-authored-by: Claude Opus 4.8 (1M context) <noreply@anthropic.com>
Co-authored-by: Willem Jiang <willem.jiang@gmail.com>
Co-authored-by: Copilot Autofix powered by AI <223894421+github-code-quality[bot]@users.noreply.github.com>')

 | 

Jun 8, 2026

 |
| 

[newsletter-generation](https://github.com/bytedance/deer-flow/tree/main/skills/public/newsletter-generation 'newsletter-generation')

 | 

[newsletter-generation](https://github.com/bytedance/deer-flow/tree/main/skills/public/newsletter-generation 'newsletter-generation')

 | 

[feat(skills): add academic-paper-review, code-documentation, and news…](https://github.com/bytedance/deer-flow/commit/8bb14fa1a7bf7e6ee0631db4db9168962edbc31f 'feat(skills): add academic-paper-review, code-documentation, and newsletter-generation skills (#1861)

Add three new public skills to enhance DeerFlow's content creation capabilities:

- **academic-paper-review**: Structured peer-review-quality analysis of
 research papers following top-venue review standards (NeurIPS, ICML, ACL).
 Covers methodology assessment, contribution evaluation, literature
 positioning, and constructive feedback with a 3-phase workflow.

- **code-documentation**: Professional documentation generation for software
 projects, including README generation, API reference docs, architecture
 documentation with Mermaid diagrams, and inline code documentation
 supporting Python, TypeScript, Go, Rust, and Java conventions.

- **newsletter-generation**: Curated newsletter creation with research
 workflow, supporting daily digest, weekly roundup, deep-dive, and industry
 briefing formats. Includes audience-specific tone adaptation and
 multi-source content curation.

All skills:
- Follow the existing SKILL.md frontmatter convention (name + description)
- Pass the official _validate_skill_frontmatter() validation
- Use hyphen-case naming consistent with existing skills
- Contain only allowed frontmatter properties
- Include comprehensive examples, quality checklists, and output templates')

 | 

Apr 5, 2026

 |
| 

[podcast-generation](https://github.com/bytedance/deer-flow/tree/main/skills/public/podcast-generation 'podcast-generation')

 | 

[podcast-generation](https://github.com/bytedance/deer-flow/tree/main/skills/public/podcast-generation 'podcast-generation')

 | 

[feat: MiniMax provider for image/video/podcast skills + new music-gen…](https://github.com/bytedance/deer-flow/commit/cd5bedaa743832da10ded26e672db8c00085d988 'feat: MiniMax provider for image/video/podcast skills + new music-generation skill (#3437)

* docs(spec): MiniMax integration for generation skills + new music skill

Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>

* docs(plan): MiniMax generation providers implementation plan

Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>

* test(skills): add importlib loader + FakeResp for skill tests

* test(skills): register loaded module in sys.modules; raise requests.HTTPError in FakeResp

* feat(image-generation): add MiniMax provider with env auto-detect

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>

* refactor(image-generation): guard unknown provider, derive ref MIME, strengthen tests

Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>

* feat(video-generation): add MiniMax provider with async poll/download

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>

* refactor(video-generation): surface base_resp errors while polling; add timeout test

* feat(podcast-generation): add MiniMax t2a_v2 provider with env auto-detect

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>

* refactor(podcast-generation): restore TTS credential guard; add volcengine + voice tests

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>

* feat(music-generation): new MiniMax music skill via skill-creator

Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>

* refactor(music-generation): treat empty lyrics as absent; test no-audio-data path

* refactor(skills): add request timeouts to MiniMax network calls

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>

* Potential fix for pull request finding 'Explicit returns mixed with implicit (fall through) returns'

Co-authored-by: Copilot Autofix powered by AI <223894421+github-code-quality[bot]@users.noreply.github.com>

* fix(models): strip inconsistent user-message names for MiniMax chat

DeerFlow middlewares tag user messages with provenance names (user-input, summary, loop_warning); langchain serializes them into the OpenAI-compatible payload and MiniMax rejects mismatched user-message names with "user name must be consistent (2013)". PatchedChatMiniMax now drops the per-message name from user-role messages. Point the config.example MiniMax models at PatchedChatMiniMax so they also get reasoning_content mapping.

Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>

* feat(image-generation): MiniMax sends JSON prompt field, guard 1500-char limit

MiniMax image-01 takes one text string capped at 1500 chars, but the skill was sending the whole structured JSON. The MiniMax provider now extracts the JSON `prompt` field (relying on prompt_optimizer to expand it) and fails fast with a clear error before calling the API when that field exceeds 1500 chars. Authoring stays provider-agnostic; Gemini still receives the full JSON.

Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>

* feat(podcast-generation): per-provider TTS concurrency and retry/backoff

Each TTS provider owns its concurrency internally — MiniMax runs single-threaded to reduce rate-limit failures, Volcengine keeps 4 workers — with automatic retry and backoff on transient HTTP and base_resp errors. No caller-facing concurrency knob.

Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>

* fix(skills): address Copilot review comments on generation skills

- video: add raise_for_status + timeout to the Gemini download/POST/poll calls so non-2xx responses surface as clear HTTP errors instead of JSON/KeyError or hangs
- video: check the task Fail status before the generic base_resp check so the failure keeps its task_id context
- video/image: create the output file parent directory before writing (matching music-generation) so nested output paths do not raise FileNotFoundError
- music: require a non-empty prompt and fail fast with ValueError instead of sending an empty prompt to the API

Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>

* fix(scripts): reclaim dev ports across worktrees in make stop/dev

All deer-flow worktrees (main checkout + linked worktrees) hardcode the same dev ports (8001/3000/2026), so a service started from any worktree must be reclaimable from another. stop_all now resolves the set of worktree roots (DEERFLOW_ROOTS) and treats a process as deer-flow-owned when its open files live under any of them. It also force-kills survivors on 2026 alongside 8001/3000, fixing `make dev` aborting on the nginx port preflight when a prior nginx lingered on 2026.

Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>

* fix(view-image): hide the injected image-context message from the UI

ViewImageMiddleware injects a HumanMessage (text + base64 images) so the vision model can see viewed images, but it was the only internal injector that set neither hide_from_ui nor a hidden name, so it leaked into the chat UI (and IM channels) as a user bubble reading "Here are the images you've viewed:". Mark it with additional_kwargs={"hide_from_ui": True}, matching todo/dynamic_context injections, which the frontend isHiddenFromUIMessage and the channel sender already honor. The model still receives the full content.

Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>

* fix(minimax): mark M2.7 models as text-only (no vision)

MiniMax M2.7 / M2.7-highspeed do not support vision; only M3 does. The
provider config asserted vision support for M2.7 in four places.

- config.example.yaml: 4 M2.7 entries -> supports_vision: false
- backend/docs/CONFIGURATION.md: M2.7 + highspeed -> supports_vision: false
- wizard: add LLMProvider.model_vision_overrides + extra_config_for() so
 selecting an M2.7 model writes supports_vision: false while M3 (default)
 keeps vision; wire it through setup_wizard.py
- tests: M2.7-highspeed fixture -> supports_vision=False; add
 test_minimax_vision_is_per_model

Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>

---------

Co-authored-by: Claude Opus 4.8 (1M context) <noreply@anthropic.com>
Co-authored-by: Willem Jiang <willem.jiang@gmail.com>
Co-authored-by: Copilot Autofix powered by AI <223894421+github-code-quality[bot]@users.noreply.github.com>')

 | 

Jun 8, 2026

 |
| 

[ppt-generation](https://github.com/bytedance/deer-flow/tree/main/skills/public/ppt-generation 'ppt-generation')

 | 

[ppt-generation](https://github.com/bytedance/deer-flow/tree/main/skills/public/ppt-generation 'ppt-generation')

 | 

[fix: issue 1138 windows encoding (](https://github.com/bytedance/deer-flow/commit/191b60a326f3031298d109dc4e8117ac40a00b23 'fix: issue 1138 windows encoding (#1139)

* fix(windows): use utf-8 for text file operations

* fix(windows): normalize sandbox path masking

* fix(windows): preserve utf-8 handling after backend split') [#1139](https://github.com/bytedance/deer-flow/pull/1139) [)](https://github.com/bytedance/deer-flow/commit/191b60a326f3031298d109dc4e8117ac40a00b23 'fix: issue 1138 windows encoding (#1139)

* fix(windows): use utf-8 for text file operations

* fix(windows): normalize sandbox path masking

* fix(windows): preserve utf-8 handling after backend split')

 | 

Mar 16, 2026

 |
| 

[skill-creator](https://github.com/bytedance/deer-flow/tree/main/skills/public/skill-creator 'skill-creator')

 | 

[skill-creator](https://github.com/bytedance/deer-flow/tree/main/skills/public/skill-creator 'skill-creator')

 | 

[feat(skills): per-user custom skill isolation with sandbox mounting (](https://github.com/bytedance/deer-flow/commit/53a80d3ad1208e3e053c9eefe4cec019a64af595 'feat(skills): per-user custom skill isolation with sandbox mounting (#3889)

* feat(skills): per-user skill isolation (#2905)

Implement user-scoped skill storage that isolates custom skills between
users while sharing public skills globally.

Key changes:
- Add UserScopedSkillStorage class for per-user custom skill directories
- Introduce get_or_new_user_skill_storage() factory with user_id context
- Auth middleware sets effective_user_id for request-scoped storage
- Agent/prompt/middleware now use user-scoped storage and prompt cache
- Sandbox mounts user-scoped skill directories for search/read tools
- Add validate_skill_file_path() to SkillStorage for path security
- Migration script supports --all-users bulk migration
- Frontend: add editable field to Skill type, error check in enableSkill
- All skill categories can be toggled (custom skills default to enabled)
- Update skill-creator SKILL.md with isolation-aware instructions

Tests:
- Add test_user_scoped_skill_storage.py (new)
- Update all existing skill tests for user-scoped storage
- Update sandbox, client, and router tests

* fix(skills): address second-round PR review feedback (#3889)

- P1-1: restrict legacy skill mount to users without custom skills
- P1-2: fail-closed for _is_disabled_skill_path (OSError → return True)
- P2-1: AND-merge global extensions_config skill disabled state
- P2-2: atomic write for _skill_states.json (mkstemp + replace)
- P2-3: normalize X-DeerFlow-Owner-User-Id in trusted boundary
- P2-4: LRU-bounded _enabled_skills_by_config_cache (OrderedDict, maxsize=256)
- P2-5: clear global prompt cache on PUBLIC skill toggle
- P2-6: invalidate skill caches on client.update_skill

* fix(tests): correct tool policy test after merge

* fix(skills): use DEFAULT_SKILLS_CONTAINER_PATH in UserScopedSkillStorage

The "/mnt/skills" literal in UserScopedSkillStorage.__init__ triggers
test_skill_container_path_defaults::test_mnt_skills_literal_is_owned_by_skill_constants_module
on CI. Migrate the default to the existing deerflow.constants constant,
matching the pattern already used by LocalSkillStorage, SkillStorage, and
the durable/tool_error middlewares.

---------

Co-authored-by: Willem Jiang <willem.jiang@gmail.com>') [#…](https://github.com/bytedance/deer-flow/pull/3889)

 | 

Jul 4, 2026

 |
| 

[skill-reviewer](https://github.com/bytedance/deer-flow/tree/main/skills/public/skill-reviewer 'skill-reviewer')

 | 

[skill-reviewer](https://github.com/bytedance/deer-flow/tree/main/skills/public/skill-reviewer 'skill-reviewer')

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

[surprise-me](https://github.com/bytedance/deer-flow/tree/main/skills/public/surprise-me 'surprise-me')

 | 

[surprise-me](https://github.com/bytedance/deer-flow/tree/main/skills/public/surprise-me 'surprise-me')

 | 

[docs: update description for surprise-me skill to enhance clarity](https://github.com/bytedance/deer-flow/commit/60be7ee20de3552aa04bdb5ebbbde092cfabf75f 'docs: update description for surprise-me skill to enhance clarity')

 | 

Feb 7, 2026

 |
| 

[systematic-literature-review](https://github.com/bytedance/deer-flow/tree/main/skills/public/systematic-literature-review 'systematic-literature-review')

 | 

[systematic-literature-review](https://github.com/bytedance/deer-flow/tree/main/skills/public/systematic-literature-review 'systematic-literature-review')

 | 

[test(skills): add evaluation + trigger analysis for systematic-litera…](https://github.com/bytedance/deer-flow/commit/654354c624bfc84ecbb60f1394ca4806590bcbdf 'test(skills): add evaluation + trigger analysis for systematic-literature-review (#2061)

* test(skills): add trigger eval set for systematic-literature-review skill

20 eval queries (10 should-trigger, 10 should-not-trigger) for use with
skill-creator's run_eval.py. Includes real-world SLR queries contributed
by @VANDRANKI (issue #1862 author) and edge cases for routing
disambiguation with academic-paper-review.

* test(skills): add grader expectations for SLR skill evaluation

5 eval cases with 39 expectations covering:
- Standard SLR flow (APA/BibTeX/IEEE format selection)
- Keyword extraction and search behavior
- Subagent dispatch for metadata extraction
- Report structure (themes, convergences, gaps, per-paper annotations)
- Negative case: single-paper routing to academic-paper-review
- Edge case: implicit SLR without explicit keywords

* refactor(skills): shorten SLR description for better trigger rate

Reduce description from 833 to 344 chars. Key changes:
- Lead with "systematic literature review" as primary trigger phrase
- Strengthen single-paper exclusion: "Not for single-paper tasks"
- Remove verbose example patterns that didn't improve routing

Tested with run_eval.py (10 runs/query):
- False positive "best paper on RL": 67% → 20% (improved)
- True positive explicit SLR query: ~30% (unchanged)

Low recall is a routing-layer limitation, not a description issue —
see PR description for full analysis.

* Potential fix for pull request finding

Co-authored-by: Copilot Autofix powered by AI <175728472+Copilot@users.noreply.github.com>

---------

Co-authored-by: Copilot Autofix powered by AI <175728472+Copilot@users.noreply.github.com>')

 | 

Apr 10, 2026

 |
| 

[vercel-deploy-claimable](https://github.com/bytedance/deer-flow/tree/main/skills/public/vercel-deploy-claimable 'vercel-deploy-claimable')

 | 

[vercel-deploy-claimable](https://github.com/bytedance/deer-flow/tree/main/skills/public/vercel-deploy-claimable 'vercel-deploy-claimable')

 | 

[feat: use list of links](https://github.com/bytedance/deer-flow/commit/efd56fdf512667095a6ddeb737c7d953ef91bcf2 'feat: use list of links')

 | 

Feb 2, 2026

 |
| 

[video-generation](https://github.com/bytedance/deer-flow/tree/main/skills/public/video-generation 'video-generation')

 | 

[video-generation](https://github.com/bytedance/deer-flow/tree/main/skills/public/video-generation 'video-generation')

 | 

[feat: MiniMax provider for image/video/podcast skills + new music-gen…](https://github.com/bytedance/deer-flow/commit/cd5bedaa743832da10ded26e672db8c00085d988 'feat: MiniMax provider for image/video/podcast skills + new music-generation skill (#3437)

* docs(spec): MiniMax integration for generation skills + new music skill

Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>

* docs(plan): MiniMax generation providers implementation plan

Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>

* test(skills): add importlib loader + FakeResp for skill tests

* test(skills): register loaded module in sys.modules; raise requests.HTTPError in FakeResp

* feat(image-generation): add MiniMax provider with env auto-detect

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>

* refactor(image-generation): guard unknown provider, derive ref MIME, strengthen tests

Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>

* feat(video-generation): add MiniMax provider with async poll/download

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>

* refactor(video-generation): surface base_resp errors while polling; add timeout test

* feat(podcast-generation): add MiniMax t2a_v2 provider with env auto-detect

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>

* refactor(podcast-generation): restore TTS credential guard; add volcengine + voice tests

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>

* feat(music-generation): new MiniMax music skill via skill-creator

Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>

* refactor(music-generation): treat empty lyrics as absent; test no-audio-data path

* refactor(skills): add request timeouts to MiniMax network calls

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>

* Potential fix for pull request finding 'Explicit returns mixed with implicit (fall through) returns'

Co-authored-by: Copilot Autofix powered by AI <223894421+github-code-quality[bot]@users.noreply.github.com>

* fix(models): strip inconsistent user-message names for MiniMax chat

DeerFlow middlewares tag user messages with provenance names (user-input, summary, loop_warning); langchain serializes them into the OpenAI-compatible payload and MiniMax rejects mismatched user-message names with "user name must be consistent (2013)". PatchedChatMiniMax now drops the per-message name from user-role messages. Point the config.example MiniMax models at PatchedChatMiniMax so they also get reasoning_content mapping.

Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>

* feat(image-generation): MiniMax sends JSON prompt field, guard 1500-char limit

MiniMax image-01 takes one text string capped at 1500 chars, but the skill was sending the whole structured JSON. The MiniMax provider now extracts the JSON `prompt` field (relying on prompt_optimizer to expand it) and fails fast with a clear error before calling the API when that field exceeds 1500 chars. Authoring stays provider-agnostic; Gemini still receives the full JSON.

Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>

* feat(podcast-generation): per-provider TTS concurrency and retry/backoff

Each TTS provider owns its concurrency internally — MiniMax runs single-threaded to reduce rate-limit failures, Volcengine keeps 4 workers — with automatic retry and backoff on transient HTTP and base_resp errors. No caller-facing concurrency knob.

Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>

* fix(skills): address Copilot review comments on generation skills

- video: add raise_for_status + timeout to the Gemini download/POST/poll calls so non-2xx responses surface as clear HTTP errors instead of JSON/KeyError or hangs
- video: check the task Fail status before the generic base_resp check so the failure keeps its task_id context
- video/image: create the output file parent directory before writing (matching music-generation) so nested output paths do not raise FileNotFoundError
- music: require a non-empty prompt and fail fast with ValueError instead of sending an empty prompt to the API

Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>

* fix(scripts): reclaim dev ports across worktrees in make stop/dev

All deer-flow worktrees (main checkout + linked worktrees) hardcode the same dev ports (8001/3000/2026), so a service started from any worktree must be reclaimable from another. stop_all now resolves the set of worktree roots (DEERFLOW_ROOTS) and treats a process as deer-flow-owned when its open files live under any of them. It also force-kills survivors on 2026 alongside 8001/3000, fixing `make dev` aborting on the nginx port preflight when a prior nginx lingered on 2026.

Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>

* fix(view-image): hide the injected image-context message from the UI

ViewImageMiddleware injects a HumanMessage (text + base64 images) so the vision model can see viewed images, but it was the only internal injector that set neither hide_from_ui nor a hidden name, so it leaked into the chat UI (and IM channels) as a user bubble reading "Here are the images you've viewed:". Mark it with additional_kwargs={"hide_from_ui": True}, matching todo/dynamic_context injections, which the frontend isHiddenFromUIMessage and the channel sender already honor. The model still receives the full content.

Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>

* fix(minimax): mark M2.7 models as text-only (no vision)

MiniMax M2.7 / M2.7-highspeed do not support vision; only M3 does. The
provider config asserted vision support for M2.7 in four places.

- config.example.yaml: 4 M2.7 entries -> supports_vision: false
- backend/docs/CONFIGURATION.md: M2.7 + highspeed -> supports_vision: false
- wizard: add LLMProvider.model_vision_overrides + extra_config_for() so
 selecting an M2.7 model writes supports_vision: false while M3 (default)
 keeps vision; wire it through setup_wizard.py
- tests: M2.7-highspeed fixture -> supports_vision=False; add
 test_minimax_vision_is_per_model

Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>

---------

Co-authored-by: Claude Opus 4.8 (1M context) <noreply@anthropic.com>
Co-authored-by: Willem Jiang <willem.jiang@gmail.com>
Co-authored-by: Copilot Autofix powered by AI <223894421+github-code-quality[bot]@users.noreply.github.com>')

 | 

Jun 8, 2026

 |
| 

[web-design-guidelines](https://github.com/bytedance/deer-flow/tree/main/skills/public/web-design-guidelines 'web-design-guidelines')

 | 

[web-design-guidelines](https://github.com/bytedance/deer-flow/tree/main/skills/public/web-design-guidelines 'web-design-guidelines')

 | 

[fix: fix skill md path](https://github.com/bytedance/deer-flow/commit/5888a5ba16276e3ccbaf318cad9d520c5585208a 'fix: fix skill md path')

 | 

Jan 20, 2026

 |
| 

View all files

 |