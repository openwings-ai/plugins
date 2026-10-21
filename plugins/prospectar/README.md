# Prospectar

Read the catalog and the funnel stages of a B2B commercial team (Empresa) on
[Prospectar](https://prospectar.io). The plugin connects your agent to
`https://api.prospectar.io/mcp` and teaches it how to use the tools. The product and its field
descriptions are in Portuguese.

## What's inside

- A skill for reading the Empresa's catalog (`list_catalog_items`) and funnel stages
  (`list_crm_stages`), interpreting `priceLabel`, centavos and meeting durations, and handling
  errors.
- The remote MCP server at `https://api.prospectar.io/mcp`. Nothing runs on your machine.
- Manifests for Claude Code and Agent Plugins (ChatGPT, Codex and Cursor).

Both tools are read-only. Neither returns customer contacts or conversations, and neither can
change data in the Empresa.

## Install

In Claude Code:

```sh
claude plugin marketplace add openwings-ai/plugins
claude plugin install prospectar@openwings-ai
```

In Codex:

```sh
codex plugin marketplace add openwings-ai/plugins
codex plugin add prospectar@openwings-ai
```

## Sign in

In Claude Code, type `/mcp`, choose prospectar and Authenticate. In Codex 0.147 or later, run
`codex mcp login prospectar`. The browser opens `https://app.prospectar.io/conectar`. Sign in as
the owner of the Empresa, check the app's name and return address, and press Conectar.

The app gets its own access key (`prospectar_...`), named after the app, for the Empresa open in
the console. It appears in `https://app.prospectar.io` under Configurações, Integrações, Chaves de
acesso, and counts toward the limit of 10 active keys per Empresa. Each key can make up to 100
calls per minute. Delete the key there to disconnect at once. No key needs to be pasted into this
plugin's files.

On a machine with no browser, the skill uses a device code with `client_id=prospectar-agent`. Open
`https://app.prospectar.io/conectar/codigo` on another device, check the 8-letter code and approve
it. The code expires in 10 minutes.

## Links

- [API and MCP guide, in Portuguese](https://prospectar.io/api)
- [OpenAPI 3.1 contract](https://api.prospectar.io/v1/openapi.json)
- [Privacy for AI apps](https://prospectar.io/privacy#apps-de-ia)
- [Terms](https://prospectar.io/terms)
- Help: [suporte@prospectar.io](mailto:suporte@prospectar.io)
