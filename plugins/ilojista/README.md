# iLojista

Read the device catalog and the funnel stages of a phone and electronics store (loja) on
[iLojista](https://ilojista.com.br). The plugin connects your agent to
`https://api.ilojista.com.br/mcp` and teaches it how to use the tools. The product and its field
descriptions are in Portuguese.

## What's inside

- A skill for reading the store's catalog (`list_catalog_items`) and funnel stages
  (`list_crm_stages`), interpreting centavos, device condition, storage, battery health and
  trade-in values, and handling errors.
- The remote MCP server at `https://api.ilojista.com.br/mcp`. Nothing runs on your machine.
- Manifests for Claude Code and Agent Plugins (ChatGPT, Codex and Cursor).

Both tools are read-only. Neither returns customer contacts or conversations, and neither can
change data in the loja.

## Install

In Claude Code:

```sh
claude plugin marketplace add openwings-ai/plugins
claude plugin install ilojista@openwings-ai
```

In Codex:

```sh
codex plugin marketplace add openwings-ai/plugins
codex plugin add ilojista@openwings-ai
```

## Sign in

In Claude Code, type `/mcp`, choose ilojista and Authenticate. In Codex 0.147 or later, run
`codex mcp login ilojista`. The browser opens `https://app.ilojista.com.br/conectar`. Sign in as
the owner of the loja, check the app's name and return address, and press Conectar.

The app gets its own access key (`ilojista_...`), named after the app, for the loja open in the
console. It appears in `https://app.ilojista.com.br` under Configurações, Integrações, Chaves de
acesso, and counts toward the limit of 10 active keys per loja. Each key can make up to 100 calls
per minute. Delete the key there to disconnect at once. No key needs to be pasted into this
plugin's files.

On a machine with no browser, the skill uses a device code with `client_id=ilojista-agent`. Open
`https://app.ilojista.com.br/conectar/codigo` on another device, check the 8-letter code and
approve it. The code expires in 10 minutes.

## Links

- [API and MCP guide, in Portuguese](https://ilojista.com.br/api)
- [OpenAPI 3.1 contract](https://api.ilojista.com.br/v1/openapi.json)
- [Privacy for AI apps](https://ilojista.com.br/privacy#apps-de-ia)
- [Terms](https://ilojista.com.br/terms)
- Help: [suporte@ilojista.com.br](mailto:suporte@ilojista.com.br)
