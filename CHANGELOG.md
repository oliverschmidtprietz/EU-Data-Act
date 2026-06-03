# Changelog — eu-data-act

All notable changes to this skill are documented here.

Format: `## [vX.Y] — YYYY-MM-DD`

---

## [v1.3] — 2026-05-31

German DA-DG entry-into-force correction. The v1.2 Germany note hedged that Bundesrat approval and entry into force were still "to be confirmed". They are now confirmed: the **Data Act-Durchführungsgesetz is in force since 30 May 2026**.

- **Status flipped from pending to in-force.** `references/gates/member-state.md` states the DA-DG as settled law: Bundesrat cleared it without objection on 8 May 2026 (1065th session), promulgated in the Bundesgesetzblatt 29 May 2026, in force 30 May 2026. The "should be confirmed before the designation is treated as operative" caveat is removed; BNetzA's competence is now stated as operative.
- **Penalty hedge softened.** "May have moved in passage" (passage complete) becomes "confirm against the published text (BGBl., 29 May 2026)".

No change to method, gates logic, templates, or the BNetzA / BfDI / penalty substance from v1.2. Status-accuracy patch only.

**Status:** reviewed (carried from v1.2).

---

## [v1.2] — 2026-05-31

German implementing-law update. The Member State gate's Germany-specific note now reflects the **Data Act-Durchführungsgesetz (DA-DG)** — *Gesetz zur Durchführung der Verordnung (EU) 2023/2854*.

- **Confirmed competent authority.** `references/gates/member-state.md` upgrades the Germany note from "BNetzA is a *plausible* candidate" to the DA-DG's actual designation: **Bundesnetzagentur (BNetzA)** as the single competent authority for all matters of Data Act implementation (§ 2 DA-DG; Art. 37(1) Data Act), with BfDI retaining the personal-data aspects (Art. 37(3)). The earlier multi-candidate hedge (BNetzA vs. Bundeskartellamt) is resolved.
- **Penalty figures.** Records the DA-DG penalty regime under Art. 40 Data Act: up to €500,000 for general infringements; up to 4 % of EU-generated annual turnover for DMA gatekeepers — flagged "confirm against enacted text" as the figures originate in the Referentenentwurf.
- **Legislative-status discipline preserved.** The note states the status (adopted by the Bundestag 26 March 2026; Bundesrat approval / entry into force to be confirmed) and keeps the warn-only posture: the skill confirms the live designation against the Commission's Art. 37(7) register and German counsel before treating BNetzA's competence as operative. No assertion of non-final law as binding.
- **Cross-reference fix.** The "Member State implementing legislation: not maintained" cross-ref now notes that Germany's DA-DG is the one summarised exception.

No change to method, gates logic, templates, or the house-style linter. Reference-content accuracy update only.

**Status:** reviewed (carried from v1.1).

---

## [v1.1] — 2026-05-25

Output-lint discipline patch. Corrects the v1.0 changelog's misdiagnosis of the house-style linter gap.

- **Diagnosis correction.** The v1.0 changelog claimed `scripts/check_house_style.py` "misses em dashes inside `**bold markdown headers**` and the connector 'Indeed' is missing from the banned list." Re-running the linter against the iteration-1 with-skill outputs that failed grading disproved this: the linter correctly catches all 18 violations in the eval 6 output (including the bold-header em dashes and "Indeed" at line 318) and the 1 em dash in the eval 4 output. The rules were already present in v0.95.
- **Actual root cause.** With-skill subagents ran `python3 scripts/check_house_style.py` with default arguments. The default scans `references/scenarios/` and `templates/` — the skill's own source files, which are clean by construction. The subagents' generated outputs were never passed to the linter and so were never checked.
- **Fix.** `SKILL.md` output discipline gains a ninth required item: lint the output before delivery, with the explicit invocation `python3 scripts/check_house_style.py <path-to-output>`. `references/method/house-style.md` gains a "Verification" subsection that documents the same recipe and calls out the bold-header drift pattern surfaced by the iteration-1 eval.
- **Expected impact.** Closes the last 1.4pp from iteration-1 (evals 4 and 6 lose their single house-style fail). No re-eval scheduled; the operational fix is small and the linter rules themselves are unchanged.

**Status:** reviewed (carried from v1.0).

---

## [v1.0] — 2026-05-25

Phase 8 `/skill-creator` eval pass. Promoted from `pre-review` to `reviewed`.

- **Aggregate eval result.** 132/134 assertions pass with the skill (98.6%) vs 98/134 baseline (73.0%); delta +25.6pp across 8 practitioner-prompt fixtures. With-skill cleared 6 of 8 fixtures at 100%; the remaining two (evals 4 and 6) lost a single house-style assertion each on em-dash usage caught by the grader but missed by the linter.
- **Substantive payoff confirmed.** Eval 0 (circular trap, Art. 4(8) refusal on weak facts): with-skill 17/17 — refused per `ch2-trade-secret-stage-3-refusal.md` Path 2, quoted Recital 31 verbatim with the "serious AND irreparable" conjunction, demanded missing facts. Baseline 11/17 — drafted a partial refusal letter; the word "irreparable" never appears in 27,505 characters of output. The discipline transferred from scaffolding to model behaviour.
- **Discriminating anti-patterns fired as designed.** Eval 1 (sectoral overlay): baseline produced detailed sectoral guidance across Reg. 2018/858, Euro 7, eCall, IDD, IVASS, Italian Law 192/1998 with a "dual-track access strategy" recommendation; with-skill flagged the overlay as warn-only and redirected to specialist counsel.
- **Per-fixture pass rates.** Eval 0 (circular trap) 17/17 vs 11/17; Eval 1 (sectoral overlay) 16/16 vs 10/16; Eval 2 (temporal applicability) 15/15 vs 11/15; Eval 3 (Digital Omnibus) 16/16 vs 12/16; Eval 4 (Art. 15 limb test) 18/19 vs 15/19; Eval 5 (GDPR Case B) 17/17 vs 14/17; Eval 6 (multi-chapter) 16/17 vs 12/17; Eval 7 (Art. 32 cumulative) 17/17 vs 13/17.
- **Cost.** With-skill mean wall-clock 317s and ~111k tokens vs baseline 152s and ~28k tokens — ~2.1× time and ~4× tokens for cold-loading 30k+ words of references. Trade-off is fit-to-send vs fit-for-revision.
- **Known gap (v1.1 patch).** `scripts/check_house_style.py` misses em dashes inside `**bold markdown headers**` and the connector "Indeed" is missing from the banned list. Two with-skill outputs (evals 4 and 6) reported "0 violations" from the linter but the grader caught them. Tightening these patterns closes the last 1.4 percentage points.
- **Eval artefacts.** Workspace at `skills/eu-data-act-workspace/iteration-1/` (not committed per `.gitignore`). Per-fixture `grading.json`, aggregate `benchmark.json` and `benchmark.md`, methodology notes in [docs/2026-05-26-eu-data-act-v1-1-shipped-handoff.md](../../docs/2026-05-26-eu-data-act-v1-1-shipped-handoff.md).

**Status:** reviewed. Eligible for symlinking to `~/.claude/skills/`.

---

## [v0.95] — 2026-05-25

Pre-eval feature-complete. Phases 5, 6, 7, 9 complete; Phase 8 (`/skill-creator` eval loop) pending.

- **Phase 5 — scenario cards (24 total).** Pre-walked applications of the seven-step method for every role × chapter × stage anchor named in the SKILL.md routing table. Each card carries: header (anchor + trigger phrases + adjacent cards), canonical fact pattern, critical disciplines, the seven-step walk, decision point, output skeleton(s) (1–4 paths per card), citations to load, cross-references, drafter notes. Ch II 8 cards, Ch III 2, Ch IV 2, Ch V 3, Ch VI 5, Ch VII 1, cross-chapter 3. The `ch2-trade-secret-stage-3-refusal.md` card is the format prototype; the cross-cards (`cross-gap-analysis`, `cross-gdpr-boundary`, `cross-omnibus-impact`) carry structural adaptations documented at the end of each.
- **Phase 6 — templates (15 + 15 parallel drafter-notes).** Drafting templates for the deliverable types the cards route to. `art4-8-refusal-letter.md` uses the eight-step TSD-gate structure as its spine; the parallel drafter-notes file emphasises that section 5(c) (irreparability) must stand alone (the conjunction discipline). Drafter notes live in `templates/_drafter-notes/` as separate files, not appended to templates.
- **Phase 7 — eval fixtures.** `evals/evals.json` carries 8 practitioner-prompt fixtures spanning the mandated disciplines (circular trap, sectoral overlay, temporal applicability, Digital Omnibus, Ch V Art. 15 limb-by-limb, GDPR Case B, multi-chapter, Art. 32 cumulative conditions). `evals/grading.md` carries per-fixture pass/fail rubric plus cross-fixture quality checks for `/skill-creator` grading.
- **Phase 9 — house-style linter.** `scripts/check_house_style.py` scans scenario cards and templates for banned patterns: em dashes, AI-tic connectors (Furthermore/Moreover/Indeed/...), conclusory padding, preambles, marketing language (robust/best-in-class/leverage as verb/actionable/...), exclamation marks. Exits non-zero on findings. Current state: 0/54.
- **Pending:** Phase 8 (`/skill-creator` eval loop). Once eval passes, version bumps to v1.0 and status changes to `reviewed`.

---

## [v0.9] — 2026-05-22

Initial pre-review baseline. Phases 1–4 of the build complete; Phases 5–9 pending.

- **Architecture (Phase 1).** Anchor: role × chapter × stage. Covers Ch II–VII operatively; Ch VIII gate-only (Arts. 34–35 engaged where they serve Ch VI). Five cross-regime gates: GDPR/ePrivacy, Trade Secrets Directive, DMA gatekeeper exclusion, sectoral lex specialis (warn-only), Member State implementing law (warn-only). English only. Pandoc as eventual renderer. UX: inferential.
- **Source layer (Phase 2).** Verbatim Regulation (EU) 2023/2854 ingested from EUR-Lex 2026-05-15 (119 recitals, 50 articles, 11 chapters). Commission FAQ v1.4 (22 Jan 2026, CC BY 4.0). Digital Omnibus amendments tracker (COM(2025) 833 final). MCTs/SCCs Recommendation pointer. Vehicle Data Guidance pointer. SHA256 manifest. Provenance `_versions.json`. Executable validator (`scripts/validate_sources.py`) at 20/20 checks.
- **Method and gates (Phase 3).** Eight reference files, all reviewed and approved:
  - `references/method/analysis-method.md` — seven-step cognitive flow + cognitive disciplines + output/clarification/refusal rules.
  - `references/method/house-style.md` — voice, length, citation, structure, per-deliverable format.
  - `references/gotchas.md` — 20 numbered failure-mode entries; entries 6–8 are the circular-trap cluster.
  - `references/gates/gdpr-overlay.md` — Art. 1(5) bridge clause, Case A/B, ePrivacy hook, joint controllership, mixed datasets, SA competence.
  - `references/gates/trade-secrets-directive.md` — TSD baseline, three-stage ladder, *serious AND irreparable* conjunction, objective elements, T&O measures, redress, enforcement signals.
  - `references/gates/dma-gatekeeper.md` — Art. 5(3) tripartite exclusion + Art. 6(2)(d), Recital 40 limits, recipient attestation.
  - `references/gates/sectoral-lex-specialis.md` — warn-only catalogue (automotive, MDR/IVDR, DORA, NIS2, CRA, AI Act, eIDAS, energy, agriculture, plus aviation/maritime/rail/telecoms).
  - `references/gates/member-state.md` — warn-only catalogue; every Art. 50 delegating provision enumerated; Germany candidates flagged unverified.
- **SKILL.md router (Phase 4).** 170 lines. Frontmatter trigger-optimised (includes "Datengesetz"). Loading instructions, anchor explanation, 24-row scenario routing table, entry-point UX, output discipline (eight required elements), refusal cases, current-law-vs-proposal discipline, source freshness reminders, validator block.

**Pending (not in this release):**

- Phase 5 — 24 scenario cards under `references/scenarios/`.
- Phase 6 — 15–18 drafting templates with parallel `_drafter-notes/` files.
- Phase 7 — eval fixtures at `evals/evals.json` + grading rubric.
- Phase 8 — `/skill-creator` eval loop; promotion to `reviewed` status.
- Phase 9 — `scripts/check_house_style.py`, finalised README, optional install.sh.

**Status:** pre-review. Not yet symlinked to `~/.claude/skills/`. Not yet validated end-to-end against practitioner prompts.
