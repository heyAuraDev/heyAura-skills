# heyAura Skills

Agent skills for fetching wallet data through heyAura's x402 APIs.

## Available skills

| Skill | Purpose |
| --- | --- |
| [heyAura](skills/heyaura/SKILL.md) | Fetch and summarize an EVM address or ENS name's multichain token balances, USD values, and DeFi positions. |

## Use a skill

Each folder under `skills/` is a self-contained skill. Install the complete folder with your agent's skill installer, including its scripts and supporting files.

The heyAura skill uses Node.js 20 or newer and an x402 payer configured through `HEYAURA_EVM_PRIVATE_KEY` in the agent's environment. Payment terms come from the live API challenge. The skill respects existing explicit spending authorization and asks when a request is not covered.

Example request:

> Use heyAura to show this wallet's assets, value by chain, and DeFi positions: `<wallet-or-ens>`.

### Inspect the endpoint directly

From the repository root:

```sh
npm ci --omit=dev --ignore-scripts --prefix skills/heyaura
node skills/heyaura/scripts/portfolio.mjs inspect --address "<wallet-or-ens>"
```

Inspection does not require a private key and does not sign or pay. It returns the live payment requirements, or a path to saved portfolio data if payment is not required.

See the [skill instructions](skills/heyaura/SKILL.md) for the payment workflow and the [API reference](skills/heyaura/references/portfolio-api.md) for endpoint and response details.

## Repository layout

```text
skills/
  heyaura/
    SKILL.md
    package.json
    package-lock.json
    references/portfolio-api.md
    scripts/portfolio.mjs
```
