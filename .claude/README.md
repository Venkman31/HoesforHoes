# Vendored Claude Code configuration

This directory makes the [superpowers](https://github.com/obra/superpowers)
skills library available to every Claude Code session that opens this repo —
including cloud/web sessions, which start in a fresh container and cannot see
the plugins installed on your own machine.

## Layout

| Path | What it is |
| --- | --- |
| `settings.json` | Declares the vendored marketplace and enables the plugin |
| `plugins/superpowers/` | Unmodified copy of the upstream plugin (skills + hooks + manifests) |

`settings.json` registers `plugins/superpowers/` as a local `directory`
marketplace and enables `superpowers@superpowers-dev`. Repo-declared plugins are
installed at session start, so nothing is fetched from the network and the
skills work offline.

Skills load namespaced, exactly as they do on a local install — `/superpowers:brainstorming`,
`/superpowers:test-driven-development`, and so on. The bundled `SessionStart`
hook injects the `using-superpowers` skill at the start of each session.

## Vendored version

- Upstream: <https://github.com/obra/superpowers>
- Version: `6.3.0` (tag `v6.3.0`, commit `b36e0829c6d0140e93cfef2ca599b1b07d4a7797`)
- License: MIT — see `plugins/superpowers/LICENSE`

Only the files Claude Code needs are vendored: `.claude-plugin/`, `skills/`,
`hooks/`, and `LICENSE`. Upstream's docs, tests, build scripts, and the
adapters for other agent tools are omitted to keep this repo small.

## Updating

```sh
git clone --depth 1 --branch <new-tag> https://github.com/obra/superpowers.git /tmp/superpowers
rm -rf .claude/plugins/superpowers
mkdir -p .claude/plugins/superpowers
cp -a /tmp/superpowers/{.claude-plugin,skills,hooks,LICENSE} .claude/plugins/superpowers/
claude plugin validate .claude/plugins/superpowers
```

Then update the version and commit recorded above. If upstream ever renames its
marketplace (currently `superpowers-dev`, from
`plugins/superpowers/.claude-plugin/marketplace.json`), update the matching key
in `settings.json` too.
