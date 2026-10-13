# offer-writer skill

An agent skill that writes and reviews customer offer documents: RFP responses, statements of work (SoW), proposals, solution descriptions, executive decks and offer emails. Claims must be truthful, commitments precise, and every sentence clear on the first read. The skill does not write marketing copy.

It is the companion of [technical-writer](https://github.com/CSPDevLabs/technical-writer-skill). Use `technical-writer` for design documents, tech notes, MoPs, runbooks and instructions. Use `offer-writer` for documents that ask a customer to decide or sign. The main difference: `offer-writer` allows recommendations with a reason; `technical-writer` bans them.

**One directory, one skill.** `SKILL.md` is what an agent loads. This README is for people.

The writing rules are in [`SKILL.md`](SKILL.md). See [`LICENSE.txt`](LICENSE.txt) for the package notice.

## Install from GitHub

Node.js is required for `npx`.

```bash
npx skills add CSPDevLabs/offer-writer-skill --skill offer-writer
```

List the skill before installing:

```bash
npx skills add CSPDevLabs/offer-writer-skill --list
```

Use the skill once, without installing it:

```bash
npx skills use CSPDevLabs/offer-writer-skill --skill offer-writer
```

### Cursor

Install into the current project. The skills CLI writes Cursor project skills to `.agents/skills/offer-writer/`.

```bash
npx skills add CSPDevLabs/offer-writer-skill --skill offer-writer -a cursor -y
```

Install for every project on this machine. The CLI writes that copy to `~/.cursor/skills/offer-writer/`.

```bash
npx skills add CSPDevLabs/offer-writer-skill --skill offer-writer -g -a cursor -y
```

A manual copy works too. Keep the directory name `offer-writer`. Cursor reads these locations:

- Project: `.cursor/skills/offer-writer/` or `.agents/skills/offer-writer/`
- User: `~/.cursor/skills/offer-writer/`

### Other agents

Pass `-a` with the agent name from the [skills CLI agent list](https://github.com/vercel-labs/skills), or omit `-a` and pick an agent in the prompt.

```bash
npx skills add CSPDevLabs/offer-writer-skill --skill offer-writer -a claude-code -y
```

A private repository uses the same command. Git, the GitHub CLI, or SSH must already be allowed to clone it.

## Use

Ask for the document in normal language. The agent loads this skill when the request is to write, rewrite, or review an RFP response, a SoW, a proposal, a solution description, an executive deck or its markdown source, or an offer email.

Name the skill when you want it on a task the description might not match:

```text
Use the offer-writer skill. Rewrite the scope section of this SoW.
```

The delivered document is Markdown unless you ask for another format. The skill keeps only claims the inputs support. It marks missing facts *to confirm* instead of filling them. Project conventions in `CLAUDE.md` or `AGENTS.md` take precedence.

For a rewrite of an existing file, the agent copies the original to `/tmp` first, edits the file in place, and checks the result with `git diff --no-index`. The reply gives the diff command and lists every claim it removed.

## Layout

```text
SKILL.md     # agent instructions; higher rules win on a conflict
README.md    # install and use, for people
LICENSE.txt  # package notice
```
