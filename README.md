# openwings-ai plugins

Plugins for openwings-ai's products. Each one connects your agent to a product's MCP server and
teaches it that product's workflows with a skill.

| Plugin                           | What it does                                                                       |
| -------------------------------- | ---------------------------------------------------------------------------------- |
| [atendime](plugins/atendime)     | Read a service business's catalog and funnel stages on atendi.me.                  |
| [ilojista](plugins/ilojista)     | Read a phone and electronics store's device catalog and funnel stages on iLojista. |
| [prospectar](plugins/prospectar) | Read a B2B commercial team's catalog and funnel stages on Prospectar.              |

## Install

In Claude Code:

```sh
claude plugin marketplace add openwings-ai/plugins
claude plugin install atendime@openwings-ai
```

In Codex:

```sh
codex plugin marketplace add openwings-ai/plugins
codex plugin add atendime@openwings-ai
```

Each plugin's README says how to sign in.

## Build an OpenAI upload

```sh
python3 scripts/export-openai.py atendime
```

This writes `dist/atendime-openai-plugin.zip`. Use another plugin name to build its ZIP, or
`--output <path>` to choose where it goes. The exporter reads the committed plugin files at `HEAD`,
not uncommitted edits. Commit plugin changes before exporting. It never copies untracked files,
environment files or key files.

All current plugins use OAuth remote servers. The ZIP adds OpenAI's
[documented authentication settings](https://developers.openai.com/plugins/build/plugins#configure-mcp-authentication)
to each server: `extensions["com.openai"].auth` selects `oauth` with `client.mode: "cimd"`.
CIMD lets the client identify itself with a metadata document; dynamic client registration stays
available as a fallback. The server supplies the OAuth endpoints through discovery. No client
secret, API key or access token belongs in the ZIP.

The source `mcp.json` stays valid against the published Agent Plugins 1.0 schema. That schema
rejects OpenAI's per-server `extensions` field, so the generated upload is OpenAI-specific, not a
portable MCP config. It keeps the `$schema` marker shown in OpenAI's example. CI checks the upload's
transport fields against the unchanged portable schema and its auth fields against our closed,
docs-derived OAuth profile in `schemas/openai-oauth.schema.json`. This profile checks the settings
we export; it is not an official OpenAI schema or a list of every auth method OpenAI supports.
Local servers and fixed-key configs are not supported by this exporter.

Run the local export check after changing the exporter:

```sh
python3 scripts/check-openai-export.py
```

It checks every plugin's ZIP, unchanged source files, repeatable output and rejected credentials
or unsupported auth settings. It does not run in CI.

## Layout

- `.claude-plugin/marketplace.json` lists the plugins. Claude Code and Codex both read it.
- `plugins/<name>/` holds one plugin: its skills, its MCP server address in `.mcp.json` (Claude)
  and `mcp.json` (Agent Plugins, read by ChatGPT, Codex and Cursor), and a manifest for each
  format.
- `registry/<name>/server.json` lists the plugin's MCP server in the
  [MCP Registry](https://registry.modelcontextprotocol.io).

Both stores ask each plugin for a privacy policy that says what the agent can see, who receives
it, how long it is kept and how to stop it. Each product publishes that section on its own website
(for example, https://atendi.me/privacy#apps-de-ia).

Every push checks the Claude files with `claude plugin validate --strict`, the Agent Plugins files
against the spec's schemas, OpenAI upload packages as described above, and each registry entry with
`mcp-publisher validate`.
