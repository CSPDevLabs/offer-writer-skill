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
  version: "1.0.0"
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
3. Draft in the order the reader decides: what they get, what it takes, what is not included.
4. Run the pre-output checks.
5. Deliver in the format the user asks for. Default is Markdown.

When the project defines its own conventions for offer documents, for example in `CLAUDE.md` or `AGENTS.md`, apply them too. On a conflict, the project convention wins.

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

5. In the reply, give the backup path and the diff command. List every claim you removed, so the user can restore it with a source.

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

### 6. Language baseline

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

## Examples

| Before | After | Rule |
| --- | --- | --- |
| "A price today would be guesses dressed up as a plan." | "We price the migration after the audit and the lab. A price today would be a guess." | 6 |
| "SRv6 is the next-generation foundation for future growth." | "SRv6 replaces the transport the customer runs today." | 3 |
| "We will support the customer during the lab phase." | "We run the lab tests. The customer supplies the lab equipment." | 2 |
| "Score each counter against a confirmed per-forwarding-complex ceiling." | "Until releases and cards are confirmed, report usage as a count only." | 6 |
| "This is the recommended design." | "We recommend this design because it keeps the old transport running during every wave." | 4 |

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
