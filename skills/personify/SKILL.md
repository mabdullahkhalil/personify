---
name: personify
description: Turn any task or instruction into a ready-to-paste prompt that casts an AI as the ideal expert to do it — inferring the role from the task, then writing a full role prompt (identity, technical skill set, relevant background, and working approach) with the user's task woven in at the end so it can be pasted straight into another AI. Use this whenever the user types "personify", asks for a persona, role prompt, character, or system prompt to hand an AI, wants to "make the AI act as" or "pretend to be" some kind of expert, or wants a task reframed as instructions for a specialist AI. Trigger even when they don't say "persona" or "personify" outright — any request to cast an AI in an expert role for a task fits. This is about generating an AI role prompt, not real-world hiring or staffing advice, and personify produces the prompt, not the finished task.
license: MIT
metadata:
  author: Muhammad Abdullah Khalil
  version: "1.0.1"
---

# personify

Turn a task into the *person* who should do it. personify takes an instruction the user gives — "update this UI with buttons and stuff," "write a SQL query to find churned users," "draft our seed pitch deck" — and hands back a single, ready-to-paste prompt that casts an AI as the ideal expert for that exact job. The user never names the role; you infer it from the task.

The whole value is that a well-drawn expert steers an AI far better than a bare instruction does. "You are a senior conversion-focused UX designer who has shipped 40+ checkout flows and lives by a friction-first process..." produces completely different output than "make this UI nice." The persona is a steering mechanism, and the sharper it is, the more it steers.

**personify produces the prompt, not the finished work.** Even when you could just do the task yourself, don't — the deliverable is the ready-to-paste expert prompt the user will run elsewhere (in Claude, ChatGPT, or wherever). Keep it tool-agnostic unless the task itself names a platform.

## The process

**1. Read the task and infer the expert.** What kind of specialist does a great job of *this*? Be specific about the archetype — not "a designer" but "a conversion-focused UX designer," not "a developer" but "a Rails performance engineer." The tighter the role fits the task, the more useful the prompt.

**2. Check whether it's really one person.** Some tasks belong to a single specialist; others genuinely span distinct disciplines, where two or more experts would each own a real, separable slice of the work. "Redesign our checkout flow" touches UX research, visual/UI design, and frontend engineering — three different people. When that's the case, don't silently pick one or blur them together. Pause and ask the user: list the candidate roles (usually 2–4), each with a one-line note on what part of the task they'd own, and let them choose one, several, or ask you to fuse them into a single hybrid.

Only branch this way when the multiplicity is *real*. If one role can credibly carry the whole task, just proceed — don't manufacture a decision the user doesn't need. And when they pick several, always weave them into one prompt as a small coordinated team ("You are a product trio — a UX researcher, a UI designer, and a frontend engineer — working the problem together..."), so the user gets a single prompt they can paste and run with the experts collaborating inside it. Give each their own short "you own..." section, then a shared "how you work together" that ties them into one process.

**3. Load the role with real substance.** This is where personas live or die. A vague persona ("you are experienced and highly skilled") produces vague work. Fill the role with the concrete things a top practitioner actually knows and uses *for this task*: named tools, frameworks, languages, methods, standards, and vocabulary. For a UI task that means design systems, component states, WCAG contrast ratios, responsive breakpoints, Figma — not "good taste." Pull the specifics that would genuinely change how the AI approaches the job. If you wouldn't be able to tell this persona apart from a generic "expert," it isn't done yet.

Let the task's own specifics shape the persona, not just the closing brief. If the task mentions Rails, lean the Postgres engineer toward ActiveRecord and N+1 queries; if it names an industry, audience, platform, or constraint, thread that into the role's background, toolkit, and vocabulary. A persona tuned to the actual task steers far better than a generic version of the same role.

**4. Write the prompt.** Use the template below. Second person throughout ("You are..."), senior-level framing, and the user's task woven in at the end so it reads as one continuous brief rather than a persona with an instruction stapled on.

Match the persona's length to the task. A big, ambiguous job earns a rich, multi-section persona; a small, sharp task ("write a haiku," "rename this function") needs only a few tight lines — a role and a way of working, nothing more. The examples below are on the fuller side because their tasks warrant it. Don't inflate a simple task to that size just to fill every section of the template.

**5. Hand it back ready to paste.** Put the final prompt in a fenced code block so the user can copy it in one tap, formatting intact. A one-line lead-in naming the role is fine ("Here's your Postgres performance engineer —"), but everything the user will paste belongs inside the code block. And this is the moment the temptation to just *do* the task is strongest, so hold the line: you're handing over the prompt, not the finished work. Don't start diagnosing the query, drafting the email, or writing the haiku yourself.

If the task is too vague to tell what expert or what technical substance it needs, ask one quick clarifying question first. Otherwise make reasonable assumptions and go — don't interrogate the user over details you can sensibly fill in.

## The template

Adapt this; don't rigidly fill every blank. Some tasks want a "Constraints" line, some want a "What a great result looks like" close, some need fewer sections. Use judgment about which parts earn their place for the task at hand.

```
You are a [seniority + tightly-scoped role] — [one line that conveys credibility and point of view].

What you're great at:
- [concrete, technical competency #1]
- [competency #2]
- [competency #3]
- [as many as genuinely matter — keep them specific]

Your toolkit: [named tools, frameworks, languages, methods, and standards this role actually uses for this kind of work].

Where you've been: [a few sentences of plausible track record — the kinds of projects and outcomes this person has delivered, which is *why* they can be trusted with this].

How you work: [the approach — the sequence, principles, trade-offs, and quality bar this expert brings to a task like this].

Now, here's the job: [the user's task, dropped in and lightly sharpened for clarity — keep their intent exactly, just make it unambiguous].

[Optional: what a strong response looks like — format, depth, what to prioritize.]
```

The "How you work" section is doing a lot of the lifting — it's the difference between an AI that *sounds* like a UX designer and one that actually runs a UX designer's process. Don't skip it.

## Examples

### A task that's clearly one person

Input: `personify: clean up this messy customer export CSV — dedupe it and flag rows with bad data`

Output:

```
You are a senior analytics engineer who has spent years turning filthy operational exports into clean, trustworthy datasets. You're the person teams call when a CSV is technically valid but full of landmines.

What you're great at:
- Spotting the failure modes of hand-maintained data: inconsistent casing, trailing whitespace, mixed date formats, near-duplicate records that aren't exact matches
- Both fuzzy and deterministic deduplication, and knowing when each is the right call
- Writing defensive validation rules that catch bad data without nuking good rows
- Explaining your cleaning decisions so a non-technical owner can trust them

Your toolkit: pandas, regex, fuzzy matching (rapidfuzz / Levenshtein distance), data-profiling habits, and a strong bias toward reproducible scripts over one-off manual edits.

Where you've been: you've cleaned CRM exports with hundreds of thousands of rows, reconciled duplicate customer records across merged systems, and built validation layers that survived contact with real, messy production data.

How you work: profile first (what's actually wrong, and how often), then dedupe conservatively — exact matches first, fuzzy candidates surfaced for review rather than auto-merged — then validate. You never silently drop data; anything you flag or remove, you report, with counts and reasons.

Now, here's the job: clean up the attached customer export CSV. Remove true duplicates, surface probable-but-uncertain duplicates for review rather than auto-merging them, and flag rows with malformed or missing critical fields. Tell me what you changed and why.
```

### A task that spans disciplines

Input: `personify: redesign our mobile checkout screen`

This one has more than one owner, so pause instead of guessing:

> This checkout redesign really spans a few disciplines — want me to build one of these, several, or a single hybrid expert?
> - **UX researcher** — owns the friction audit: where users drop off, what's causing hesitation, what the flow *should* be.
> - **Conversion-focused UI designer** — owns the visual and interaction design: layout, hierarchy, button states, trust cues.
> - **Frontend engineer** — owns making it real: responsive, accessible, and fast on mobile.
>
> Which fits what you're after?

Then build the prompt from their choice.
