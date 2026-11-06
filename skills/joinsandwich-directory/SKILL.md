---
name: joinsandwich-directory
description: Search sandwich-generation caregiving resources, community channels, or estimate long-term care costs via joinsandwich.com.
---

# Sandwich Directory

Every tool named below comes from `https://www.joinsandwich.com/api/mcp`. No account needed.

## Steps

1. **Search** — `search_care_resources` with a city or topic.
2. **Channel** — `get_channel` with an id from search when the user wants details.
3. **Cost** — `calculate_long_term_care_cost` with a state when the user asks for an estimate.

## Rules

- Public directory data only. Estimates are illustrative, not quotes.
- Agents docs: https://joinsandwich.com/agents

## Done when

- Results cite the search/channel/cost tool output.

