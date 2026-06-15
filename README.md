# persona-audit

**English** · [中文](README.zh.md) · [日本語](README.ja.md)

**Four fake users read what your tool says to real users — and tell you what makes no sense.**

You're too close to your own product to see where a stranger gets stuck. persona-audit spins up four personas who read *only* your tool's output — never the code, never the docs — and report what they misread, panic at, or can't find.

## What it catches

Point it at, say, the daily digest your app emails users. Four personas read one real digest *cold* — they see only the output, never your code, so they react like a true first-timer:

- **Novice:** "It says *This week: 0* — I thought the app was broken."
- **Veteran:** "*Net change* and *total* are both here and I can't tell which is which."
- **Target user:** "Nothing tells me why I should open this tomorrow."

Three different angles, one shared confusion. The **consensus matrix** — a ranked list of what several personas independently land on — floats that line to the top, and you fix it before it ships. Cross-angle agreement, not a lone nitpick, is the signal you act on.

![The consensus matrix persona-audit produces — findings ranked by how many personas independently hit them](docs/hero-consensus-matrix.png)

> That screenshot is persona-audit run on *this README*: four personas flagged that a tool about "seeing your own blind spots" had no demo of its own. So now it has one — the block you just read.

## Why not just ask Claude to review it?

A plain "review this" prompt tends to follow your wording and tell you what you hoped to hear. persona-audit pins four strangers to fixed identities, lets none of them see your code, and surfaces only what *several of them hit independently* — so it catches the blind spots a single, agreeable pass glides right over.

## When to use

✅ A tool whose engine emits **user-facing text** ships a new version or output — report generators, daily digests, bot push copy, readout tools. *(Yes — a side-project that emails users a daily summary counts.)*
❌ Code review · pure UI/visual QA · interactive-narrative QA.

## Quickstart

```bash
git clone https://github.com/wjameswen888/persona-audit.git
cp -r persona-audit ~/.claude/skills/
```
*(Or paste those two lines to Claude and let it install the skill for you.)*

Then just tell Claude: **"run a persona audit on \<your tool's output>."** It gathers 6–8 real outputs — you point it at where they come from (a demo command, a few pasted samples, or a quick dump script) — runs the four personas, and hands back the ranked matrix in a few minutes. Nothing to configure to start: `LOCAL.md` binds it to your product, but every plug point has a default, so it runs unfilled. It reads output in any language, and runs on the Claude Code you already have — no extra subscription (it does spend tokens, like any longer task).

## How it works

1. **Generate 6–8 real outputs** — cover normal cases, edge data, empty states, and the view users actually see.
2. **Four personas cold-read them** — mirror (your real user), novice (jargon + panic detector), veteran (false-precision detector), and a target for whatever you just shipped.
3. **Consensus matrix** — findings ranked by how many personas independently land on the same thing. A "vote" means several prompt-angles converged — a strong hint to verify first, not proof.
4. **ABCD triage** — **A** fix now (typos, wrong numbers) · **B** real gaps to build · **C** conflicts with a deliberate design choice → *ask the owner before touching it* · **D** out of scope.
5. **Don't-cut list** — what users actually loved, flagged so you don't break it next version.

## Honest about what it is — and how it differs from "synthetic users"

Those tools simulate users to *do research*, and often dress LLM output up as a measurement. persona-audit does the opposite: it audits the text you **already ship**, and it's blunt about its own limits. The four personas share one base model, so a vote means *several angles converged*, not statistical independence — this is a single-person, zero-cost, few-minute **blind-spot scan that produces a candidate list to verify, not data**. Act on cross-angle agreement; confirm before you treat anything as proven.

## Install details

It's a [Claude Code skill](https://docs.claude.com/en/docs/claude-code) — auto-triggers on the phrases in its description (e.g. *"persona audit"*, *"cold-read audit"*, *"audit the output from a user's POV"*). Copy `LOCAL.md.example` → `LOCAL.md` to bind it to your product (gitignored; every plug point has a default, so it runs even unfilled).

## Files

| File | What |
|------|------|
| `SKILL.md` | The method — generic, portable |
| `templates.md` | 4 persona identity blocks + report skeleton + cross-domain adaptation |
| `examples/case-study.md` | A real run, start to finish |
| `LOCAL.md.example` | Template for your private product bindings |

## License

MIT — see [LICENSE](LICENSE).
