# Slippy Lab: qualification adaptation for approval

Status: fork, name, and isolation changes only. Everything listed as proposed below remains unimplemented until approval.

## Goal and scope

Help the team reach a well-founded course of action: a finalized term sheet to the client or a reasoned decision to decline. The team understands why the action makes sense, what would change it, and the reasonable alternatives.

Qualification includes enough structuring to support the offer. A draft remains provisional when a material issue is unresolved. Sending anything to a client is a human action in this first version.

The method is general: establish the mandate and constraints; propose promising directions; investigate and model the important uncertainties; challenge the alternatives; revise; converge. The standing question is: **What does the team still need to understand, establish, or choose before it can responsibly act?**

Visible map nodes remain high level. Several reasoning steps, research jobs, and model iterations can happen inside one node. No recursive decision-expansion engine, context registry, mandatory granularity, or predetermined guarantor/allocation strategy.

## Fork and isolation

| Item | Slippy Lab |
|---|---|
| Repository | `https://github.com/balaji-dwa/slippy-lab` |
| Working branch | `codex/qualification-fork` |
| Checkout | `/Users/aakashdwa/Documents/slippy-lab` |
| Upstream | `amosblomqvist/learnharness`, 0.3.8, `3dc88472eea41eed0d5e5f29c2f16f8d063c415b` |
| App/package name | `Slippy Lab` / `slippy-lab` |
| Desktop bundle identifier | `com.slipstream.SlippyLab` |
| macOS desktop profile | `~/Library/Application Support/Slippy Lab` |
| macOS desktop development profile | `~/Library/Application Support/Slippy Lab-dev` |
| Web development | `http://127.0.0.1:3017`; checkout-local `data/` and `auth.json` |
| Updates | Disabled in this fork; publishing metadata points to the fork |
| Local packaging | Publish disabled; upstream Apple signing/notary settings are not used |

The installed `/Applications/LearnHarness.app` and its `~/Library/Application Support/LearnHarness` profile are not modified, copied, linked, or migrated. Sessions, model settings, API keys, subscription credentials, browser profiles, and instance locks remain separate. No real model requests or sign-in are needed for this preparation step.

The original icon, teaching behavior, and learning features still exist. They are intentionally part of the proposal below rather than silently changed during the rename. Internal `LH_` variable names and process-local bridge names can remain where they do not select shared storage or endpoints; wholesale identifier renaming adds no qualification behavior.

Preparation checks: lint, typecheck and production build pass; 197 focused desktop, authentication, identity and release-fixture checks pass under the repository's Node 26 runtime. A direct check of the real shell code verifies separate development/packaged profiles and that the updater is never loaded. The standalone server boots with empty temporary data/auth using Electron's bundled Node; its offline provider checks report zero network attempts. No desktop installer or live qualification session has been tested at this stage. Upstream's four build-tracing warnings remain.

## Proposed feature removal

Each removal includes its callers, settings, contracts, and affected tests. Keep the working conversation and artifact runtime intact.

| Remove from the qualification version | Main locations | Reason / retained equivalent |
|---|---|---|
| Practice sessions and problem/hint/verdict loop | `src/agent/tools/practice.ts`, `prompts/practice/`, `components/practice-cards.tsx`, `components/practice-dock.tsx`; practice branches in agent construction, chat handling, sidebar and contracts | Qualification is not retrieval practice. Keep ordinary conversation and human thinking fields. |
| Graded quizzes, hidden correct answers, answer reveal, confidence percentage rail | Quiz/explain portions of `src/agent/tools.ts`, `src/core/question-core.ts`, `src/core/pending.ts`, `components/question-dock.tsx`, `components/answered-card.tsx`, `components/confidence-rail.tsx` | Adapt the useful question/answer UI into clarifications and tradeoff choices. Preserve ungraded questions and responses. |
| Predict/teach/check sequencing and grading-driven repair | Teaching/probe prompts; question roles in native messages, phase display and contracts | Use clarify, analyze, test, and revise; agent chooses the next useful action without compulsory quizzes. |
| Personal knowledge graph, proposition extraction, linking auditor and extraction coverage | `src/agent/subagents/extraction.ts`, `src/agent/tools/graph.ts`, `src/server/graph.ts`, `src/store/graph.ts`, `app/api/graph/**`, extraction hooks in `chat-handler.ts`, graph settings and components | Remove personal learning memory. Keep session transcripts and the separate per-session plan map. Do not build a replacement deal-memory system for the first test. |
| Knowledge-graph home page, chain table and note-to-proposition import | `components/home.tsx`, `components/graph-view.tsx`, `components/graph-canvas.ts`, `components/chain-table.tsx`, `components/notes-import.tsx` | Start with a mandate and show qualification sessions. Keep reading deal files and PDFs. |
| Learning-specific session controls | Teaching/practice filters, quiz mechanic controls, proposition targets, confidence controls in sidebar/new-chat/settings | A qualification session with the existing model picker, thinking level, cost display and useful preferences. |
| Bundled LearnHarness learning-data skill | `skills/learnharness/**`, `tests/skills/**` | It targets personal learning records, including LearnHarness's installed data path. Do not run or install this inherited skill. Remove it after approval, with its isolated tests. |
| Upstream release operations and updater UI | `.github/workflows/notify-website.yml`, release publishing/signing workflow, `scripts/verify-release.ts`, updater controls/banner and updater-only tests | The lab is tested locally. Updates are already disabled for isolation; deleting the remaining machinery needs approval. Keep local build/boot checks. |

## Keep and adapt

Keep the low-overhead conversation, team thinking fields, transcript/history, model picker and usage display, editable prompts, background job queue, cancellation, local files/PDF readers, per-session map, sandboxed HTML demos, and verification of generated artifacts.

Keep existing provider connections during the first adaptation. Do not rebuild authentication or delete working provider support just to simplify labels. Slippy Lab starts with its own empty profile; configure it separately before live testing.

Adapt research to Exa through the existing `SearchProvider` interface (`src/core/search.ts`, `src/server/search.ts`, key catalog and settings). Add Exa as the route used by qualification; do not invent a new research framework. Existing adapters can remain until there is a reason to remove them.

Adapt the HTML demo builder into a model/simulation builder. Each brief names the question, inputs, assumptions, formulas, controls, and outputs. Check both execution and the relevant calculations; a working demo does not establish that a proposed deal is feasible. Excel integration is deferred; downloadable spreadsheets are not required for the first test.

The existing per-session map represents directions, candidate structures, and major questions. Revise it when findings change the investigation. Preserve the transcript when revising the map. Browsing a node is not evidence that a proposal is validated or approved.

## Proposed document removal and replacement

Git history retains the original documents. Keep required upstream and third-party attribution.

| Current document or asset | Proposed action |
|---|---|
| `README.md` | Replace the retained learning-product marketing and upstream download instructions with Slippy Lab purpose, setup, workflow, isolation, and attribution. |
| `docs/vision.md`, `docs/teaching-methodology.md`, `docs/plan.md` | Remove as active product instructions; replace with a short qualification-method document based on the agreed goal. |
| `docs/probe-teach-split.md` | Rewrite as clarify-to-analysis handoff, with human reasoning and evolving directions. |
| `docs/release-0.3.md`, `docs/archive/architecture-2026-09-08.md` | Remove historical learning-product/release plans. |
| `docs/pi-engine-swap.md` | Remove the completed migration narrative after preserving any live runtime facts in architecture documentation. Keep the working engine. |
| `docs/desktop-release.md` | Replace upstream publishing/signing/update procedures with local lab build and isolation instructions. |
| `docs/architecture.md`, `docs/development.md`, `docs/keyboard.md` | Keep and update to match retained features, ports, names, and the actual qualification workflow. |
| `docs/tool-content-recovery.md`, `docs/compaction-accounting.md` | Keep while their mechanisms remain. The compaction document includes attribution shipped by `electron-builder.yml`; do not remove it as cosmetic cleanup. |
| `docs/assets/knowledge-graph.png`, `docs/assets/teaching-session.png`, `docs/assets/lh_banner_*` | Remove when replacing the README references; defer new artwork. |
| `src/agent/prompts/README.md` | Update prompt assembly, role names and retained fragments alongside the code changes. |
| `LICENSE`, third-party notices and authorship | Retain. Fork attribution must remain accurate. |
| `AGENTS.md` | Retain for now; propose fork-specific guidance separately if needed. Do not silently discard upstream development instructions. |

## Proposed prompt renames and modifications

Paths below are relative to `src/agent/`. These are proposed mappings, not changes already made.

| Existing prompt | Proposed destination | Change in purpose |
|---|---|---|
| `system-prompt.md` | Same file | Replace installing understanding with the qualification goal, governing question, team ownership of judgment, and distinction between sourced facts, assumptions, calculations and preferences. |
| `prompts/prober/10-probe-doctrine.md` | `prompts/clarifier/10-mandate-clarification.md` | Read the mandate and supplied materials; offer preliminary directions; ask what changes the route; capture the team's reasons. Remove learner-level bracketing, binary-search quizzes and misconception scoring. |
| `prompts/teacher/05-method.md` | `prompts/analyst/05-qualification-method.md` | Establish objective and constraints, compare plausible directions, investigate material uncertainties, test and revise, converge. Replace unconditional-truth pedagogy with explicit evidence and assumptions. |
| `prompts/teacher/10-planning.md` | `prompts/analyst/10-analysis-map.md` | Map high-level directions and dependencies. Keep adaptive rewrites; remove curriculum, learner mastery and question tags as progress proof. |
| `prompts/teacher/20-teaching.md` | `prompts/analyst/20-analysis.md` | Develop the analysis in understandable increments, use artifacts, and bring human judgment in when useful. Remove mandatory one-fact/one-quiz cycles. |
| `prompts/teacher/28-predictions.md` | `prompts/analyst/28-hypotheses.md` | State candidate explanations or structures, what would support or weaken them, and choose the next useful test. No compulsory prediction question every turn. |
| `prompts/teacher/30-question-principles.md` | `prompts/analyst/30-challenge.md` | Challenge assumptions, downside cases and alternatives. Human agreement and attractive model output do not verify feasibility. Remove right/wrong grading and distractor craft. |
| `prompts/teacher/40-jobs.md` | `prompts/analyst/40-research.md` | Give researchers specific questions, relevant deal context and needed sources. Use Exa, cite claims, surface gaps and update the analysis on return. Never rely on an unfinished job for a material conclusion. |
| `prompts/teacher/50-demos.md` | `prompts/analyst/50-models.md` | Build scenario instruments with explicit assumptions, formulas, sensitivity controls and financial checks. Use findings in the analysis. |
| No current outcome fragment | `prompts/analyst/60-qualification-outcome.md` | Define convergence: proposed terms or decline, supporting rationale, reasonable alternatives, execution conditions and what changes the recommendation. Material gaps keep the draft provisional. |
| `prompts/shared/10-voice.md` | Same file | Plain professional communication addressed to a team; remove tutoring and learner-correction language. |
| `prompts/shared/15-accuracy.md` | Same file | Retain verification and honest uncertainty. Separate user assertions from established facts and modeled outcomes. |
| `prompts/shared/16-mental-model.md` | `prompts/shared/16-team-thinking.md` | Read the team's full reasoning to discover constraints, beliefs and preferences. Do not treat preferences as external evidence. |
| `prompts/shared/20-question-tools.md` | `prompts/shared/20-team-questions.md` | Clarifications, critiques and consequential choices with thinking fields. Remove hidden answers, grading, distractors and compulsory one-question-per-turn teaching rules. |
| `prompts/shared/25-confidence.md` | Remove | Learning-answer confidence percentages are not estimates of deal feasibility. Express material uncertainty with reasons and implications. |
| `prompts/shared/30-learner-files.md` | `prompts/shared/30-deal-materials.md` | Deal documents, mandate and team-provided materials, targeted reading and citations. |
| `prompts/shared/40-formatting.md` | Same file | Keep useful math, tables and artifact conventions; remove classroom-specific wording. |
| `prompts/practice/00-base.md`, `prompts/practice/10-doctrine.md` | Remove | No practice agent in this qualification version. |

Embedded specialist prompts also need adaptation:

| File | Proposed action |
|---|---|
| `subagents/researcher.ts` | Keep focused cited briefs and gaps; replace teacher/lesson framing with the analytical question and deal context. Exa wiring belongs in the search adapter, not prompt text alone. |
| `subagents/demo-builder.ts` | Rename role/file to model builder with its callers; retain sandbox and run/fix loop, add calculation and sensitivity checks. |
| `subagents/pdf-reader.ts` | Keep targeted extraction and page citations; replace learner/lesson references. |
| `subagents/visual-maker.ts` | Keep precise figures when useful; adapt descriptions and labels without a new architecture. |
| `subagents/extraction.ts` | Remove session extractor, notes extractor and linking-auditor prompts with personal knowledge-graph functionality. |

Rename prompt directories and runtime roles together. Update `teacher-agent.ts`, `prompt-segments.ts`, `src/core/prompt-segments.ts`, model-role settings, phase display, tool descriptions/schemas, prompt settings UI, packaging asset checks and affected tests. Replace `probe_done` with the clarification handoff in that same change; do not leave mismatched prompt names and tool contracts.

Preserve the source order: base, role-specific methodology, shared mechanics. Keep the existing editable-prompt mechanism. Start with a fresh Slippy Lab profile, so no LearnHarness prompt overrides or sessions need migration.

## First test after approval

1. Start a new qualification session with the original UBTC mandate and the agreed goal. Do not preload the team's eventual guarantor or allocation conclusions.
2. Slippy gives an initial analysis and asks a clarification that can change the route. Team thinking is retained in the conversation.
3. It proposes a few high-level directions and an editable map. Further reasoning stays inside those directions.
4. A material uncertainty can trigger an Exa brief, a verified HTML scenario model, a team question, or a revised map. Failures and unknowns remain visible.
5. New information can revise or eliminate a direction without forcing recursive decision expansion.
6. The result is a term-sheet draft or a reasoned decline, with alternatives, dependencies and reversal conditions. Human review establishes whether it is ready to send; nothing is sent automatically.
7. LearnHarness and Slippy Lab can run side by side with separate data, credentials, instance locks and update behavior.

Approval authorizes the proposed feature/document removals and qualification prompt/runtime changes above. It does not authorize deleting LearnHarness data, importing credentials, changing the installed app, publishing a release or sending client communications.
