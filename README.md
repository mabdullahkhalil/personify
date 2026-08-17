# personify

**Turn any task into the *person* who should do it.** Describe what you want done, and personify hands back a ready-to-paste prompt that casts an AI as the ideal expert for that exact job — the right role, a real technical toolkit, a plausible track record, and the way that expert actually works — with your task woven in at the end.

A vague instruction gets vague output. `"You are a senior conversion-focused UX designer who has shipped 40+ checkout flows and works friction-first..."` gets something far better. personify writes that expert for you, automatically, from a one-line description of the task.

## What it does

- **Infers the role from the task** — you never name it. "Optimize a slow Postgres query" summons a database performance engineer; "write a firm supplier email" summons a procurement-comms specialist.
- **Loads it with real substance** — named tools, frameworks, methods, and standards that actually steer the AI, not filler adjectives.
- **Tunes the persona to your specifics** — mention Rails and the Postgres engineer leans into ActiveRecord and N+1; name an industry or constraint and it threads through.
- **Handles multi-discipline work** — when a task genuinely spans specialists (a landing page needs copy + design + frontend), it asks which you want, then fuses your picks into one coordinated team prompt.
- **Hands back a ready-to-paste prompt** — one clean block you drop into Claude, ChatGPT, or any AI, with your task already woven in.

## Install (Claude Code)

Run these two commands in Claude Code, replacing `mabdullahkhalil` with wherever you host this repo:

```
/plugin marketplace add mabdullahkhalil/personify
/plugin install personify@personify-marketplace
```

The skill activates automatically — no restart needed. It registers as `personify:personify`.

## Install (manual / Claude.ai)

Prefer not to use the plugin system, or want it on Claude.ai?

- **Claude.ai:** zip the `skills/personify/` folder and upload it under **Settings → Capabilities → Skills**.
- **Claude Code (no plugin):** copy `skills/personify/` into `~/.claude/skills/` (personal) or `.claude/skills/` (project).

## Usage

Type `personify:` followed by whatever you want done.

```
personify: optimize a slow Postgres query that keeps timing out in production
```

personify replies with a ready-to-paste prompt — a senior Postgres performance engineer, complete with an EXPLAIN-first methodology and the task woven in. Paste it into a fresh AI chat and go.

A few more it handles well:

```
personify: write a firm but polite email to a supplier who shipped the wrong parts twice
personify: launch a waitlist landing page for my new SaaS product   # asks which specialists, then builds a team
personify: write a haiku about autumn                                # returns a lean poet persona, not a bloated one
```

Note: personify produces the **prompt**, not the finished work. It sets the AI up to do the task; it doesn't do the task itself.

## How it works

The skill infers the best-fitting expert archetype for your task, fills the role with concrete domain substance and a real working approach, sizes the persona to the task (rich for big ambiguous jobs, tight for small sharp ones), and weaves your instruction in as a closing brief. For tasks that span several disciplines, it pauses to let you choose the specialists and fuses them into a single collaborative prompt.

## License

MIT — see [LICENSE](LICENSE).
