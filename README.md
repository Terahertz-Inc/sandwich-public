# Sandwich

**The platform for the sandwich generation — caring for aging parents while raising kids.**

Sandwich helps families coordinate eldercare, organize what their parents
need, and pay for it without burning out. We also expose our care
directory and family workspace as **agent-callable tools** so AI
assistants like Claude, Cursor, and ChatGPT can answer real questions
about Medicare, Medicaid, long-term care insurance, and the cost of
care in any U.S. state.

🌐 **Marketing site:** [joinsandwich.com](https://www.joinsandwich.com)
👨‍👩‍👧 **Family app:** [app.joinsandwich.com](https://app.joinsandwich.com)
🤖 **Agent integration docs:** [app.joinsandwich.com/agents](https://app.joinsandwich.com/agents)
📦 **MCP Registry:** [`com.joinsandwich/directory`](https://registry.modelcontextprotocol.io/v0.1/servers?search=com.joinsandwich) · [`com.joinsandwich/care-circle`](https://registry.modelcontextprotocol.io/v0.1/servers?search=com.joinsandwich)

---

## What is the sandwich generation?

Adults caring for an aging parent **and** raising children at the same
time. Roughly **1 in 4** Americans aged 40–59 are in this position
([Pew, 2024](https://www.pewresearch.org/social-trends/2024/09/29/the-sandwich-generation/)).
Sandwich is built around the **40-70 rule**: when you turn 40 or your
parents turn 70, it's time to start the conversation about Medicare,
power of attorney, advance directives, and long-term-care plans.

We cover:

- **Legal** — power of attorney, advance directives, guardianship,
  estate planning
- **Financial** — Medicare and Medicaid, long-term care insurance,
  the 5-year Medicaid look-back, IRMAA, RMDs
- **Healthcare** — home care, adult day, assisted living, memory
  care, nursing home, hospice
- **Cost projections** — state-by-state, 1–30 year horizons, custom
  inflation assumptions, sourced from the CareScout 2025 Cost of
  Care Survey
- **Family logistics** — shared calendars, medication tracking,
  caregiver coordination, secure messaging

---

## For AI agents and developers

Sandwich exposes **two MCP servers** registered with the official
[Model Context Protocol Registry](https://registry.modelcontextprotocol.io).
Any MCP-capable agent — Claude Desktop, Claude Code, Cursor, custom
agents — can call them.

### `com.joinsandwich/directory` — public, no auth

Read-only research tools for the 840+ vetted resources and the cost
calculator. Use this when a user asks about Medicare, Medicaid,
nursing-home costs, or any eldercare planning topic.

**Endpoint:** `https://www.joinsandwich.com/api/mcp`
**Auth:** none

| Tool | What it returns |
|---|---|
| `search_care_resources` | Search 840+ channels, guides, reports, glossary terms. |
| `get_channel` | Fetch a specific resource collection by slug. |
| `calculate_long_term_care_cost` | Project total cost by U.S. state, care type, duration, inflation. |

### `com.joinsandwich/care-circle` — authenticated, per-user

Family workspace integration. Read CareEvents (appointments, meds,
visits, notes), list loved ones, inspect tenant context. **HIPAA in
scope** — Bearer API key required, per-key rate-limited, append-only
audit log.

**Endpoint:** `https://app.joinsandwich.com/api/mcp`
**Auth:** Bearer key from `app.joinsandwich.com/settings/mcp-keys`, or
full OAuth 2.1 + PKCE at `app.joinsandwich.com/.well-known/oauth-authorization-server`.

| Tool | What it returns |
|---|---|
| `ping` | Liveness + identity confirmation. |
| `get_user_profile` | Caller's uid, email, workspace. |
| `list_loved_ones` | Care recipients on the caller's workspace. |
| `list_care_events` | Recent care events from Sandwich Pipe. |

### Quick install (Claude Desktop)

```jsonc
// ~/Library/Application Support/Claude/claude_desktop_config.json
{
  "mcpServers": {
    "sandwich-directory": {
      "url": "https://www.joinsandwich.com/api/mcp"
    },
    "sandwich-care-circle": {
      "url": "https://app.joinsandwich.com/api/mcp",
      "headers": {
        "Authorization": "Bearer sk-sand-..."
      }
    }
  }
}
```

Restart Claude Desktop. Mint the Bearer key at
[`/settings/mcp-keys`](https://app.joinsandwich.com/settings/mcp-keys)
after signing in.

Full docs at [**app.joinsandwich.com/agents**](https://app.joinsandwich.com/agents).

---

## Discovery surfaces

- [`/.well-known/mcp/server.json`](https://app.joinsandwich.com/.well-known/mcp/server.json) — RFC-style manifest
- [`/.well-known/oauth-authorization-server`](https://app.joinsandwich.com/.well-known/oauth-authorization-server) — RFC 8414
- [`/.well-known/oauth-protected-resource`](https://app.joinsandwich.com/.well-known/oauth-protected-resource) — RFC 9728
- [`/agents`](https://app.joinsandwich.com/agents) — human-readable connect guide
- [`/agents.json`](https://app.joinsandwich.com/agents.json) — machine-readable manifest
- [`/llms.txt`](https://app.joinsandwich.com/llms.txt) — LLM index

---

## Brand and press

- Company: **Terahertz, Inc.** dba **Sandwich**
- Press inquiries: `hello@joinsandwich.com`
- Logo + brand assets: [joinsandwich.com/press](https://www.joinsandwich.com/press)

If you're writing about the sandwich generation, eldercare cost
inflation, the Medicaid look-back rule, or AI-assisted caregiving,
we're happy to share data and quotes — reach out.

---

## Related repositories

| Repo | What's in it |
|---|---|
| [`Terahertz-Inc/sandwich`](https://github.com/Terahertz-Inc/sandwich) | Public marketing site, content, MCP submission drafts |
| [`Terahertz-Inc/sandwich-platform`](https://github.com/Terahertz-Inc/sandwich-platform) | Application platform (private — HIPAA scope) |

---

## License and use

This README and the public marketing material are released under
[**CC BY 4.0**](https://creativecommons.org/licenses/by/4.0/) —
quote freely with attribution to `joinsandwich.com`.

The Sandwich MCP endpoints are subject to the
[Sandwich Terms of Service](https://www.joinsandwich.com/terms) and
[Privacy Policy](https://www.joinsandwich.com/privacy). Care Circle
data access is governed by a Business Associate Agreement (BAA).

---

## Contact

- Web: [joinsandwich.com](https://www.joinsandwich.com)
- Email: `hello@joinsandwich.com`
- Integrations: `hello@joinsandwich.com` (subject: "MCP / agent")

Built in the US 🇺🇸 for the 11 million Americans caring for an aging
parent and a child at the same time.
