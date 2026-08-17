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

The skill activates automatically — no restart needed. Invoke it with `/personify`.

Its fully-qualified name is `personify:personify` (that's the form the `/` typeahead lists, since plugin components are namespaced by their plugin). You don't need to type it: the bare `/personify` resolves as long as nothing else installed claims that name. If you ever do hit a clash, `/personify:personify` is unambiguous.

## Install (manual / Claude.ai)

Prefer not to use the plugin system, or want it on Claude.ai?

- **Claude.ai:** zip the `skills/personify/` folder and upload it under **Settings → Capabilities → Skills**.
- **Claude Code (no plugin):** copy `skills/personify/` into `~/.claude/skills/` (personal) or `.claude/skills/` (project).

Installed this way there's no plugin namespace at all — it's just `/personify`.

## Updating

Installed via the plugin system? Refresh the marketplace first, then the plugin — the marketplace holds the version index, so updating the plugin alone won't see a new release:

```bash
claude plugin marketplace update personify-marketplace
claude plugin update personify
```

**Restart Claude Code afterwards** — an updated plugin isn't applied to the running session.

You can also do it from inside Claude Code: run `/plugin` to open the plugin manager and update from there.

To check what you have, run `claude plugin list`, or `claude plugin details personify` for the version and component inventory.

Installed manually? Just replace the folder:

```bash
git pull                                     # in your clone of this repo
cp -r skills/personify ~/.claude/skills/     # overwrite the old copy
```

On Claude.ai, re-zip `skills/personify/` and upload it again under **Settings → Capabilities → Skills**, replacing the existing skill.

### Publishing a new version (maintainers)

`version` is recorded in three files. The first two **must agree**, or the release tag won't validate:

1. Bump `version` in `.claude-plugin/plugin.json`.
2. Bump the matching `version` in the `plugins` entry of `.claude-plugin/marketplace.json`.
3. Update `metadata.version` in `skills/personify/SKILL.md` so manual installs report the right version too.
4. Validate, commit, push, and tag:

```bash
claude plugin validate .
git commit -am "personify v1.1.0"
git push
claude plugin tag --push   # creates and pushes personify--v1.1.0, checking the manifests agree
```

`claude plugin tag` refuses to run on a dirty working tree or an existing tag — commit first, and use `--dry-run` to preview.

Users pick the new version up with the update commands above.

## Usage

Type `/personify` followed by whatever you want done.

```
/personify optimize a slow Postgres query that keeps timing out in production
```

personify replies with a ready-to-paste prompt — a senior Postgres performance engineer, complete with an EXPLAIN-first methodology and the task woven in. Paste it into a fresh AI chat and go.

A few more it handles well:

```
/personify write a firm but polite email to a supplier who shipped the wrong parts twice
/personify launch a waitlist landing page for my new SaaS product   # asks which specialists, then builds a team
/personify write a haiku about autumn                                # returns a lean poet persona, not a bloated one
```

You can also just ask in plain language — "give me a persona for optimizing a slow Postgres query" trips the same skill without the slash command.

Note: personify produces the **prompt**, not the finished work. It sets the AI up to do the task; it doesn't do the task itself.

## How it works

The skill infers the best-fitting expert archetype for your task, fills the role with concrete domain substance and a real working approach, sizes the persona to the task (rich for big ambiguous jobs, tight for small sharp ones), and weaves your instruction in as a closing brief. For tasks that span several disciplines, it pauses to let you choose the specialists and fuses them into a single collaborative prompt.

## License

MIT — see [LICENSE](LICENSE).
