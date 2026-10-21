# atendi.me

Read the catalog and the funnel stages of a service business (negócio) on
[atendi.me](https://atendi.me), built for barbershops, clinics, salons and studios in Brazil. The
plugin connects your agent to `https://api.atendi.me/mcp` and teaches it how to use the tools. The
product and its field descriptions are in Portuguese.

## What's inside

- A skill for reading the catalog (`list_catalog_items`) and the funnel stages (`list_crm_stages`),
  interpreting centavos and schedule durations, and handling errors.
- The remote MCP server at `https://api.atendi.me/mcp`. Nothing runs on your machine.
- Manifests for Claude Code and Agent Plugins (ChatGPT, Codex and Cursor).

Both tools are read-only. Neither returns customer contacts or conversations, and neither can
change data in the negócio.

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

## Sign in

In Claude Code, type `/mcp`, choose atendime and Authenticate. In Codex 0.147 or later, run
`codex mcp login atendime`. The browser opens `https://app.atendi.me/conectar`. Sign in as the
owner of the negócio, check the app's name and return address, and press Conectar.

The app gets its own access key (`atendi_...`), named after the app, for the negócio open in the
console. It appears in `https://app.atendi.me` under Configurações, Integrações, Chaves de acesso,
and counts toward the limit of 10 active keys per negócio. Each key can make up to 100 calls per
minute. Delete the key there to disconnect at once. No key needs to be pasted into this plugin's
files.

On a machine with no browser, the skill uses a device code with `client_id=atendime-agent`. Open
`https://app.atendi.me/conectar/codigo` on another device, check the 8-letter code and approve it.
The code expires in 10 minutes.

## Links

- [API and MCP guide, in Portuguese](https://atendi.me/api)
- [OpenAPI 3.1 contract](https://api.atendi.me/v1/openapi.json)
- [Privacy for AI apps](https://atendi.me/privacy#apps-de-ia)
- [Terms](https://atendi.me/terms)
- Help: [suporte@atendi.me](mailto:suporte@atendi.me)
