# Firecrawl by Nova (CIVAI)

Scrape, crawl, and search the web via Firecrawl's official hosted MCP.

**Keywords:** mcp-server, model-context-protocol, nova-by-civai, remote-mcp, streamable-http, civai, cursor, claude-desktop, mcp, firecrawl

Remote **Model Context Protocol (MCP)** server from **Nova by CIVAI**. Connect from **Cursor**, **Claude Desktop**, **Claude Code**, or any MCP client that supports **Streamable HTTP**.

## Links

| Resource | URL |
|----------|-----|
| MCP endpoint | https://nova.civai.co/mcp/agents/mcp-firecrawl |
| Agent page | https://nova.civai.co/agent/mcp-firecrawl |
| API keys | https://nova.civai.co/api-keys |
| Official Registry | `co.civai.nova/mcp-firecrawl` |

## Authentication

Tool discovery (`initialize`, `tools/list`) is open, so you can see every tool before signing up. Calling a tool needs a Nova account, through either of two paths:

1. **OAuth 2.1 (sign in when prompted).** Clients that support MCP OAuth, such as Claude Code, ChatGPT and Codex, open a Nova sign-in on first use. Nothing to configure.
   - Protected resource metadata: https://nova.civai.co/.well-known/oauth-protected-resource/mcp/agents/mcp-firecrawl
   - Authorization server: https://nova.civai.co (metadata at `/.well-known/oauth-authorization-server`)
2. **API key.** For clients without OAuth (Cursor, Cline, scripts), sign in at [nova.civai.co/api-keys](https://nova.civai.co/api-keys), create a programmatic key, and send it as `Authorization: Bearer <key>` or `X-API-Key: <key>`.

## Cursor Marketplace plugin

This repository ships a **Cursor Plugin** manifest (`.cursor-plugin/plugin.json` + root `mcp.json`) for one-click install after marketplace review. Users configure `NOVA_API_KEY` in Cursor **Plugins → Configure** (never commit secrets).

Local test: copy this folder to `~/.cursor/plugins/local/mcp-firecrawl-by-nova`, reload the window, set `NOVA_API_KEY`, verify MCP tools load.

## Cursor (manual MCP)

Add to `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "mcp-firecrawl-by-nova": {
      "url": "https://nova.civai.co/mcp/agents/mcp-firecrawl",
      "headers": {
        "Authorization": "Bearer YOUR_NOVA_API_KEY"
      }
    }
  }
}
```

## Claude Code

Install as a plugin from the Nova marketplace, which prompts for your API key on first enable:

```bash
/plugin marketplace add civai-technologies/nova-catalog-mcp-plugins-by-nova-civai
/plugin install mcp-firecrawl-by-nova --marketplace civai-technologies/nova-catalog-mcp-plugins-by-nova-civai
```

Or add the MCP server directly:

```bash
claude mcp add --transport http mcp-firecrawl-by-nova \
  https://nova.civai.co/mcp/agents/mcp-firecrawl \
  --header "Authorization: Bearer $NOVA_API_KEY"
```

Setting this up on someone's behalf? [`llms-install.md`](./llms-install.md) is written for that.

## Transport

- **Type:** Streamable HTTP (stateless)
- **Auth:** OAuth 2.1, or a Nova API key as `Authorization: Bearer` / `X-API-Key`


## Tools

- `firecrawl_scrape`
- `firecrawl_map`
- `firecrawl_search`
- `alexandria_library_search`
- `alexandria_library_read`
- `firecrawl_save_skill`
- `firecrawl_search_feedback`
- `firecrawl_feedback`
- `firecrawl_crawl`
- `firecrawl_check_crawl_status`
- `firecrawl_agent`
- `firecrawl_agent_status`
- `firecrawl_interact`
- `firecrawl_interact_stop`
- `firecrawl_parse`
- `firecrawl_monitor_create`
- `firecrawl_monitor_list`
- `firecrawl_monitor_get`
- `firecrawl_monitor_update`
- `firecrawl_monitor_delete`
- `firecrawl_monitor_run`
- `firecrawl_monitor_checks`
- `firecrawl_monitor_check`
- `firecrawl_research_search_papers`
- `firecrawl_research_inspect_paper`
- `firecrawl_research_related_papers`
- `firecrawl_research_read_paper`
- `firecrawl_research_lookup_protein`
- `firecrawl_developer_search`
- `firecrawl_gov_search`
- `people_company_search`
- `people_company_enrich`
- `jobs_search`
- `firecrawl_credit_usage`
- `firecrawl_usage_dashboard`
- `firecrawl_recommended_providers`
- `firecrawl_provider_directory`
- `firecrawl_agent_activity`


## Data and usage

- **Where it runs.** The server is hosted by CIVAI on nova.civai.co. Requests and their results are processed on CIVAI's servers under the [Privacy Policy](https://nova.civai.co/privacy) and [Terms](https://nova.civai.co/terms).
- **What an account can run.** Usage depends on the plan of the signed-in Nova account. Current plans and limits are on the [agent page](https://nova.civai.co/agent/mcp-firecrawl).
- **No local install.** Nothing runs on your machine; it cannot work offline.

## About Nova by CIVAI

**Nova by CIVAI** is a platform for running, building, and deploying AI agents. This MCP server exposes **Firecrawl** tools to external MCP hosts without sharing upstream credentials.

| | |
|---|---|
| **Company** | CIVAI TECHNOLOGIES |
| **Creator** | [Kayode Femi Amoo](https://x.com/usecodenaija) |
| **Product** | [Nova by CIVAI](https://nova.civai.co) |

## License

The files in this repository (README, manifests, icon, install guides) are MIT licensed. See [LICENSE](LICENSE).

The MCP server itself is a hosted CIVAI service. Its implementation is proprietary and is not in this repository; the MIT license does not cover it.
