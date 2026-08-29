# CLAUDE.md

Guidance for Claude Code (and other AI assistants) working in this repository.

## What this repository is right now

**There is no application code in this repo today.** Be aware of that before
you go looking for a src tree, a build, or tests — none exist.

```
.
├── README.md          # empty (a single blank line)
├── index.html         # empty stub (one CRLF, no markup)
└── .claude/           # the only substantive content: vendored Claude Code config
    ├── README.md      # how the vendored plugin is wired up and updated
    ├── settings.json  # registers the local marketplace + enables the plugin
    └── plugins/superpowers/   # unmodified upstream copy (skills + hooks + manifests)
```

No `package.json`, no lockfile, no build tooling, no test runner, no linter, no
CI workflows, no `.gitignore`. There is nothing to install and nothing to run.
Do not invent or assume commands — if a task needs tooling, introduce it
deliberately and say so.

### History and original intent

The repo (`Venkman31/Remove`, originally "HoesforHoes", then "Hose4Hoes") began
as a **single-file static landing page**: a tongue-in-cheek firefighter-themed
dating-site marketing page with hero, "How It Works", "Why Firemen?",
"Features", CTA, and footer sections. It was added in `2f09bfd` and deleted in
`5c62de7` ("Remove index.html file"); `index.html` was later re-added as an
empty stub.

Recover the old page when you need it as a reference:

```sh
git show 2f09bfd:index.html
```

If asked to restore or rebuild the site, follow the conventions the deleted file
established, unless told otherwise:

- One self-contained `index.html` — markup plus an inline `<style>` block, no
  external CSS/JS files, no framework, no build step.
- Theme colors as CSS custom properties on `:root` (`--red`, `--dark`,
  `--light`, `--grey`).
- Google Fonts via `<link>` (Oswald for headings, Inter for body); headings
  uppercase with letter-spacing.
- Mobile-first: `<meta name="viewport" content="width=device-width, initial-scale=1.0">`.
- Plain semantic sections, emoji in headings and buttons, hosted image URLs.

Note: `index.html` currently uses **CRLF** line endings; the old file did too.
Keep that consistent if you edit it, or normalize deliberately.

## The `.claude/` directory — treat as vendored

`.claude/plugins/superpowers/` is an **unmodified copy of upstream**
[obra/superpowers](https://github.com/obra/superpowers) v6.3.0 (tag `v6.3.0`,
commit `b36e082`), MIT licensed. It is vendored so cloud/web sessions — which
start in a fresh container and cannot see locally installed plugins — still get
the skills, offline and with no network fetch.

- **Do not edit files under `.claude/plugins/superpowers/`.** Local fixes are
  lost on the next update and make the vendored copy diverge from upstream.
- To update it, follow the documented procedure in `.claude/README.md` (clone
  the new tag, replace the directory, `claude plugin validate`, then update the
  recorded version/commit there).
- `.claude/settings.json` declares `plugins/superpowers/` as a `directory`
  marketplace named `superpowers-dev` and enables `superpowers@superpowers-dev`.
  If upstream renames its marketplace (see
  `plugins/superpowers/.claude-plugin/marketplace.json`), the key in
  `settings.json` must change to match.

### What the plugin does to your session

A `SessionStart` hook (`hooks/hooks.json` → `hooks/run-hook.cmd session-start`,
matching `startup|clear|compact`) injects the full `using-superpowers` skill
into context at the start of every session. Skills load namespaced, e.g.
`/superpowers:brainstorming`, `/superpowers:test-driven-development`.

Available skills: `brainstorming`, `dispatching-parallel-agents`,
`executing-plans`, `finishing-a-development-branch`, `receiving-code-review`,
`requesting-code-review`, `subagent-driven-development`, `systematic-debugging`,
`test-driven-development`, `using-git-worktrees`, `using-superpowers`,
`verification-before-completion`, `writing-plans`, `writing-skills`.

## Development workflow

The superpowers skills define the expected process. In short:

1. **Check for an applicable skill before acting** — including before
   clarifying questions or exploring files. Announce "Using [skill] to
   [purpose]" and follow it.
2. **Process skills come first, then implementation.** "Let's build X" →
   `superpowers:brainstorming` before writing code. "Fix this bug" →
   `superpowers:systematic-debugging` before proposing a fix.
3. **Multi-step work** → `writing-plans`, then `executing-plans` or
   `subagent-driven-development`.
4. **Writing code** → `test-driven-development` (once a test runner exists;
   this repo has none yet, so adding one is part of the work).
5. **Before claiming done** → `verification-before-completion`: run the
   commands, read the output, then make the claim. Never report success you
   have not observed.
6. **Wrapping up** → `requesting-code-review`, then
   `finishing-a-development-branch`.

Explicit user instructions and this file take precedence over skills; skills
take precedence over default behavior.

## Git conventions

- Default branch: `main`. Work on a feature branch — the established naming is
  `claude/<short-topic>-<id>` (e.g. `claude/claude-md-documentation-ujr0m6`).
- Never commit directly to `main`, and never push to a branch other than the
  one you were assigned.
- Push with `git push -u origin <branch-name>`; on network failure retry with
  backoff (2s, 4s, 8s, 16s).
- Commit messages: short imperative subject describing the change
  ("Vendor superpowers plugin so cloud sessions load it").
- **Do not open a pull request unless explicitly asked.** There is no PR
  template in this repo.
- If the PR for your branch has already merged, restart the branch from the
  latest `main` rather than stacking onto merged history.

## Conventions for new code

Because the repo is a blank slate, whatever you add sets the precedent — so
choose conservatively and document it here:

- Prefer the smallest thing that works. This is a static-site repo; reach for a
  bundler, framework, or package manager only if the task genuinely requires
  one, and mention the tradeoff.
- If you add tooling (package manager, test runner, linter, CI), add a
  `.gitignore` in the same change and update this file with the commands to
  run it.
- Keep secrets out of the repo; there is no ignore file to catch them.
