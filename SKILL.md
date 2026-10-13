---
name: offer-writer
description: >-
  Writes and reviews customer offer documents in plain, first-read English:
  truthful claims, precise commitments, concrete value, no marketing language.
  Use when the user asks to write, rewrite, or review an RFP response, a
  statement of work (SoW), a proposal, a solution description, an executive
  deck or its markdown source, or an offer email.
metadata:
  author: Anton Zyablov
  version: "1.2.0"
  created: 2026-10-13
---

# Offer writer

Write offer documents that a customer can understand on the first read and sign without surprises.

Readers include executives, procurement, PMO and engineers. Many read English as a second language. Write for all of them.

The writing rules are numbered in priority order. When two rules conflict, the lower number wins.

This skill is not for sales copy. A claim without evidence is a defect, not a style choice.

## Workflow

1. Identify the document type and the readers.
2. Collect the facts from the inputs. When a fact is missing, ask for it or mark it *to confirm*. Do not fill the gap.
3. Draft in the order the reader decides: what they get, what it takes, what is not included. For an executive deck, write the slide titles first and confirm the storyline with the user before writing any slide body.
4. Run the pre-output checks.
5. Deliver in the format the user asks for. Default is Markdown.

When the project defines its own conventions for offer documents, for example in `CLAUDE.md` or `AGENTS.md`, apply them too. On a conflict, the project convention wins.

## Writing rules in priority order

### 1. Truthful claims only

- Every claim traces to an input, to evidence, or to a named source: an RFC with its section, a vendor guide with its release, a named customer input.
- State limits openly. Say what the work proves and what it does not prove.
- Use "guarantee" only for a contractual commitment.
- Do not cite working drafts that can change or disappear.

### 2. Precise commitments

- State in scope, out of scope and optional explicitly.
- Name who supplies what: the customer, the supplier, or a third party.
- Do not use vague verbs for commitments: "support", "assist", "help", "facilitate", "as needed", "where applicable", "best effort".
- Numbers reconcile: totals, effort rows and columns, phase durations against the calendar.
- Show a duration, price or date only where it is committed. Otherwise write *TBD* and say what it depends on.

### 3. Concrete value, no marketing

- Say what the customer gets and what changes for them.
- Do not use: seamless (as an adjective), hitless, zero-impact, non-disruptive, future-proof, best-in-class, world-class, cutting-edge, state-of-the-art, leverage, synergy, holistic.
- Do not use adjectives that carry no fact: "powerful", "robust", "innovative", "unique".

### 4. Recommendations with a reason

Recommendations are allowed. Each one names the reason or the evidence: "We recommend X because Y."

Never justify scope or effort with "because the customer asked". State the value it delivers.

### 5. Customer-facing register

- No repository paths, internal file names or AI-agent names. Name human roles instead, for example "MPLS Core SME".
- No backticks, code formatting or symbols such as ≠ in customer documents.
- Evidence levels in plain bold: **Full**, **Partial**, **Inferred**.
- An abbreviations table expands every acronym, including vendor-specific ones.
- Technical terms are welcome when the reader can act on them or check them: IS-IS, BGP-LU, EVPN-VPWS. Drop a term that only makes the sentence sound expert.

### 6. Passive voice for architecture, active voice for commitments

Describe architectural and technical elements in the passive voice. The element is the subject of the sentence, because the design is the topic, not the person who built it.

- Use the passive voice for what an element is and how it is built, connected, configured or protected. "The route reflectors are deployed in two sites." "Core links are protected by Remote LFA."
- Name the agent with "by" only when the agent is part of the design. "Labels are allocated by the PCE."
- Use the active voice, with a named actor, for commitments, tasks, responsibilities and recommendations. "We run the lab tests." "The customer supplies the configurations."
- Do not use the passive voice to hide who does the work. "The tests will be run" is not a commitment. Name who runs them.
- Do not give a technical element a verb that makes a claim: "ensures", "guarantees", "enables", "delivers". State the design fact instead. "The design ensures resilience" becomes "Each access router is connected to two aggregation routers."
- No impersonal passives: "it is recommended that", "it should be noted that", "it is expected that". Use "We recommend" with a reason (rule 4), or state the fact.

### 7. Language baseline

- One idea per sentence. About 20 words at most.
- Subject and verb first.
- If two sentences need a dash or a semicolon to join them, write two sentences.
- No asides in brackets inside other asides.
- Plain words: "limit", not "ceiling". "Group of routers", not "cohort".
- No labels invented during the work, for example "census", "headroom method", "load-bearing".
- No noun stacks. "Per-forwarding-complex ceiling utilisation band" becomes "how full each forwarding chip is".
- No idioms, metaphors or slogans: "on-ramp", "dressed up as a plan", "off the critical path".
- Use "X, not Y" at most once per section. State the positive fact first.
- Each sentence makes sense on its own. A reference supports the sentence; it does not replace its content.
- Write a sentence only if it gives a fact, a decision or a constraint specific to this offer. Cut standard method, facts the work will discover, and repeats.
- When the user says a passage is unclear, the rewrite is shorter than the original. Fix that passage only.

## Executive decks

Apply the writing rules, plus these. On a conflict, this section wins for slides.

- **Answer first.** The first content slide states the decision asked for, the recommendation and its reason, the cost or effort, and the date. Background comes after.
- **Action titles.** Each title is one sentence that states the conclusion of the slide, about 15 words at most. "Coexistence is not tested at today's network size", not "Lab results".
- **One message per slide.** The body proves the title. Content that does not prove it moves to the appendix.
- **Explicit ask.** The closing slide names the decision, the options with their trade-offs, the cost of doing nothing, the decision owner and the date.
- **Slides travel alone.** Each slide is clear without the presenter. Expand acronyms on the slide. Give a source and date for each number. Mark the status: Draft or Final.
- **Business units.** State numbers in the units an executive decides on: cost, time, risk exposure, customers or services affected. A technical metric appears only with its business consequence, or in the appendix.
- **One set of numbers.** Every number matches the other slides, the SoW and the proposal.
- **Text budget.** About five bullets per slide at most, each a sentence of about 12 words.
- **Charts.** The chart title states the conclusion. Label the data directly. Bar-chart axes start at zero. No 3D or decorative charts.
- **Voice.** Titles and the ask use the active voice and name the consequence for the customer. Architecture detail on body or appendix slides follows rule 6.
- **Speaker notes.** Notes follow the same rules. They can explain a slide but cannot add a claim or commitment the slide does not show. Notes are often forwarded.

## Rewrite of an existing document

Edit the file in place. Do not create a second copy beside it. Keep the meaning. Change only the prose that breaks a rule. Do not change numbers, tables of data, headings or section numbers unless the user asks.

1. Back up the original outside the repository:

   ```bash
   cp <path/to/document.md> /tmp/<document>.orig.md
   ```

2. Edit one passage at a time. Do not regenerate the whole file.
3. Show the changes:

   ```bash
   git diff --no-index --word-diff /tmp/<document>.orig.md <path/to/document.md>
   ```

4. Check for banned words (see rule 3). "Seamless MPLS" as the name of a transport is allowed:

   ```bash
   rg -n -i 'hitless|zero[- ]impact|non-disruptive|future[- ]proof|best[- ]in[- ]class|world[- ]class|cutting[- ]edge|state[- ]of[- ]the[- ]art|leverage|synergy|holistic|seamless' <path/to/document.md>
   ```

5. Check passives that may hide the actor (see rule 6). Each hit names who does the work, or it describes a technical element:

   ```bash
   rg -n -i '\b(will|shall|must|is to|are to) be [a-z]+(ed|en)\b|\bit is (recommended|expected|assumed|noted)\b|\bit should be\b' <path/to/document.md>
   ```

6. In the reply, give the backup path and the diff command. List every claim you removed, so the user can restore it with a source.

## Examples

| Before | After | Rule |
| --- | --- | --- |
| "A price today would be guesses dressed up as a plan." | "We price the migration after the audit and the lab. A price today would be a guess." | 7 |
| "SRv6 is the next-generation foundation for future growth." | "SRv6 replaces the transport the customer runs today." | 3 |
| "We will support the customer during the lab phase." | "We run the lab tests. The customer supplies the lab equipment." | 2 |
| "Score each counter against a confirmed per-forwarding-complex ceiling." | "Until releases and cards are confirmed, report usage as a count only." | 7 |
| "This is the recommended design." | "We recommend this design because it keeps the old transport running during every wave." | 4 |
| "The operator deploys two route reflectors per region." | "Two route reflectors are deployed per region." | 6 |
| "The design ensures that services survive a node failure." | "Each service is dual-homed to two PE routers." | 6 |
| "The configurations will be collected in week 2." | "The customer supplies the configurations in week 2." | 6 |

## Pre-output checks

- [ ] Every claim has a source in the inputs or a named standard.
- [ ] Scope, out of scope, optional items and responsibilities are explicit.
- [ ] No vague commitment verb remains.
- [ ] Numbers reconcile. Durations and prices appear only where committed.
- [ ] No banned marketing word remains.
- [ ] Each recommendation states its reason.
- [ ] No repository path, internal file name, AI-agent name, backtick or ≠ in customer text.
- [ ] Every acronym is expanded.
- [ ] Sentences are about 20 words or fewer, with one idea each.
- [ ] A fluent but non-native engineer can restate each sentence after one read.

For an executive deck, also check:

- [ ] Read alone and in order, the slide titles tell the whole story.
- [ ] Each slide makes sense when forwarded on its own.
- [ ] The ask names a decision, an owner and a date.
