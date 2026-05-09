# Kindling — Agent Instructions

Kindling is a public AI learning site organized around the NVIDIA 5-layer stack (Energy → Chips → Infrastructure → Models → Applications). Built on Mintlify. MDX in git. Auto-deploys on push to `main`.

- **Live site:** https://kindling.birklid.com
- **Repo:** https://github.com/tumbleweedlabs/kindling
- **Local preview:** `PATH="/opt/homebrew/opt/node@22/bin:$PATH" mint dev` (requires Node 22; Node 25+ is unsupported)

---

## Voice and style

- Approachable, polished, honest. Not academic, not hype-driven.
- Second person ("you"), active voice, sentence case for headings.
- No marketing adjectives: no "powerful", "seamless", "robust", "simply", "just".
- Card descriptions: one sentence, factual, no trailing adjectives.
- Prose descriptions: 1–2 paragraphs, specific and accurate.

---

## Terminology

- **Layer** — one of the five NVIDIA stack layers (Energy, Chips, Infrastructure, Models, Applications)
- **Category** — a Library grouping by function (e.g. Finance, Coding, Skills)
- **Tool page** — an internal library page for a specific tool, repo, or article
- **Type** — one of: Open Source, Commercial, Research Paper, Article

---

## Library tool pages

Every item in the library has an internal page at `library/[category]/[slug].mdx`.

### File location

```
library/agents/agent-zero.mdx         → /library/agents/agent-zero
library/coding/opencode.mdx           → /library/coding/opencode
library/finance/trading-agents.mdx    → /library/finance/trading-agents
```

### Frontmatter

```yaml
---
title: "[Tool Name]"
description: "[One sentence — what it is and what makes it notable]"
---
```

### Badge taxonomy

Two badges always appear at the top:

| Badge | Values |
|---|---|
| Type | `Open Source` · `Commercial` · `Research Paper` · `Article` |
| Stack Layer | `Applications Layer` · `Models Layer` · `Infrastructure Layer` · `Chips Layer` · `Energy Layer` |

Badge colour for layer: `color="#F97316"` (Kindling orange).

### Stack layer icons

| Layer | Icon string |
|---|---|
| Applications | `browsers` |
| Models | `brain-circuit` |
| Infrastructure | `server` |
| Chips | `microchip-ai` |
| Energy | `bolt-lightning` |

### Image sourcing

1. **GitHub repos** — use the GitHub social card (no download needed):
   `https://opengraph.githubassets.com/1/[owner]/[repo]`
2. **Commercial tools / websites** — fetch the `og:image` from their homepage
3. **Articles** — no image required; omit the Frame

### Info cards

Use `<CardGroup cols={4}>` for key facts. Standard cards:

| Slot | GitHub repos | Commercial | Article |
|---|---|---|---|
| 1 | Type (Open Source MIT / Apache) | Type (Commercial / Freemium) | Type (Article) |
| 2 | Stack Layer | Stack Layer | Stack Layer |
| 3 | Language | Pricing | Publication |
| 4 | Stars (e.g. 157k+) | API Available: Yes/No | Author |

### Full template

```mdx
---
title: "[Tool Name]"
description: "[One sentence]"
---

<div style={{display: "flex", gap: "8px", marginBottom: "1.5rem", flexWrap: "wrap"}}>
  <Badge>[Type]</Badge>
  <Badge color="#F97316">[Layer] Layer</Badge>
</div>

# [Tool Name]

**[One-sentence bold tagline]**

<Frame>
  <img src="[image URL]" alt="[Tool Name]" />
</Frame>

<CardGroup cols={4}>
  <Card title="Type" icon="code-branch">[Open Source (MIT)]</Card>
  <Card title="Stack Layer" icon="[layer-icon]">[Layer]</Card>
  <Card title="[Stat label]" icon="[icon]">[Value]</Card>
  <Card title="[Stat label]" icon="[icon]">[Value]</Card>
</CardGroup>

## What it is

[1–2 paragraphs. Specific, accurate, no marketing language.]

<Tip>
  **Use this when** [actionable scenario].
</Tip>

## Get started

<CardGroup cols={2}>
  <Card title="[Primary CTA] ↗" icon="globe" href="[URL]">
    [One line: what they'll find there]
  </Card>
  <Card title="GitHub ↗" icon="github" href="[GitHub URL]">
    [One line: source code, issues, contributors]
  </Card>
</CardGroup>

## Related tools

<CardGroup cols={2}>
  <Card title="[Tool]" icon="[icon]" href="/library/[category]/[slug]">
    [One sentence]
  </Card>
</CardGroup>
```

### After creating a tool page

1. **Update the category page** (`library/[category].mdx`): change the card `href` from the external URL to the internal path (e.g. `href="/library/coding/opencode"`).
2. **Update `docs.json`**: add the tool page under its category's nested group (see Navigation section below).

---

## Navigation structure

The LIBRARY tab uses nested groups so tool pages sit under their parent category:

```json
{
  "tab": "LIBRARY",
  "icon": "books",
  "groups": [
    {
      "group": "Library",
      "root": "library/browse",
      "pages": [
        {
          "group": "Coding",
          "root": "library/coding",
          "pages": [
            "library/coding/opencode",
            "library/coding/warp"
          ]
        },
        {
          "group": "Finance",
          "root": "library/finance",
          "pages": [
            "library/finance/alpaca",
            "library/finance/trading-agents"
          ]
        }
      ]
    }
  ]
}
```

Categories without tool pages remain as plain strings in the pages array (no sub-group needed).

---

## docs.json conventions

- `name`: "Kindling by TumbleweedLabs"
- `theme`: "mint"
- `colors.primary`: "#F97316" (orange)
- Never use `mint.json` — always `docs.json`
- Redirects live in the top-level `redirects` array
- Layer tab pages live at `[layer]/overview.mdx`

---

## Mintlify suite skills

The `mintlify-agent-skills` suite is installed:
- `router` — always loaded; routes to the right companion
- `design` — information architecture, nav patterns
- `write` — voice, frontmatter, card description standards
- `create` — site bootstrap
- `maintain` — health checks (`mint broken-links`, `mint validate`)
