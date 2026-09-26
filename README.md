# Claude Code .NET Learning Project Setup

A Claude Code setup for learning .NET the slow way: **Claude teaches, reviews and
tracks decisions — you write every line of code.**

Most Claude Code configurations exist to make it write more code, faster. This one
denies it the ability to write code at all. The point is understanding that
survives a follow-up question, with working code as the evidence rather than the
goal.

Use this repo as a GitHub **template**, once per project.

## How it works

Three mechanisms, each doing a different job:

- **Permissions** (`.claude/settings.json`) — Claude cannot write `.cs`, `.csproj`,
  migrations or `appsettings`, cannot run `git` writes, and cannot scaffold with
  `dotnet new` / `add` / `ef`. Not a request in a prompt; a deny rule. Everything
  else prompts before it runs, so nothing happens that you didn't see first.
- **Output style** (`.claude/output-styles/tutor.md`) — Socratic mode. One question
  at a time, ask before telling, mechanism over syntax, and an explicit escape
  hatch (`JUST TELL ME`) so the flow doesn't become a fight.
- **Docs** (`docs/learning/`) — the project's memory. What binds current work is
  loaded every turn; everything else is read on demand.

## Setup

1. **Use this template** → create your project repo.
2. `cp .devcontainer/.env.example .devcontainer/.env` and set a password.
3. Open in the devcontainer (.NET 10 SDK, SQL Server, Node, egress firewall).
   Swap SQL Server for Postgres in `docker-compose.yml` if that's your stack.
4. Start Claude Code. **If its first reply says `TUTOR-MODE-ACTIVE` is missing,
   stop** — the output style didn't load, and nothing else here is working either.
   Silence means it's fine.
5. Create your integration branch and tag the starting commit, so `/reflect` and
   `/review-as-mentor` have a base to diff against.
6. Fill in `CLAUDE.md`'s per-project block and `docs/learning/master.md`.
7. Draft `docs/learning/current-phase.md`, then run `/plan-review` before writing
   any code.

## The rituals

| Skill | When | What you get |
|---|---|---|
| `/plan-review` | Before starting a phase | Eleven checks on your draft
| `/sync` | End of every session | Conflicts named, docs reconciled, handoff written. |
| `/review-as-mentor <base>` | Phase complete, fresh session | A senior o `reviews/`. |
| `/reflect` | When a session drifts | Five ways reasoning goes wrong, with quotes. |
| `/recall` | Starting cold | Spaced retrieval on decisions you haven't
| `/import-history <phase>` | Once, on an existing project | Cross-checks old docs against real code. |

Start with the first three. Promote the rest to habits only once those feel
automatic — six ceremonies from day one is how setups like this get abandoned.

## Where things live

| File | Holds | Loaded every turn |
|---|---|---|
| `CLAUDE.md` | The working agreement | yes |
| `docs/learning/current-phase.md` | Scope, Done-when + evidence, curren
| `docs/learning/decisions.md` | Constraints, standing checks, decisions | yes |
| `docs/learning/master.md` | Why, roadmap, calibration, process | no |
| `docs/learning/debt.md` | Known-unfixed problems, permanent IDs | no |
| `docs/learning/handoff.md` | Session-to-session state | no |
| `docs/learning/reviews/` | Phase reviews, written by skills | no |
| `docs/learning/archive/` | Pre-harness docs, if any. Never a source of truth | no |
| the source code | What actually exists | — |

The split is by *when you need it*, not by topic. A settled choice goes
`decisions.md`; a known-unfixed problem goes in `debt.md`; they are not
interchangeable.

## The rules that do the work

- **You write all production and test code.** Corrections arrive as diff
  ~10 lines; anything bigger means the design needs discussing instead.
- **Write a prediction before running a command.** Cheapest high-value habit here,
  and the easiest to let slide.
- **Runtime claims need evidence** — test output, a real HTTP response, database
  state, a forced failure. Unverified reasoning gets labelled as such.
- **Docs that disagree get named, never silently reconciled.**
- **Claude's audits are a filter, not a gate.** Internal consistency is not
  correctness.

## Adapting it

The structure is stack-agnostic; the deny lists, devcontainer and review
checklists are .NET. If you add a seventh document, the checklist is: do
`CLAUDE.md` name it, does `settings.json` allow it, does a skill write it, and is
it reachable per turn? Every gap found while building this came from mis
of those four.