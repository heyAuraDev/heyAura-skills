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

## Publish to ClawHub

The [publishing workflow](.github/workflows/publish-clawhub.yml) uploads `skills/heyaura` when a stable GitHub release is published. Branch pushes and prereleases do not publish to ClawHub.

The workflow publishes to ClawHub as `@heyaura/heyaura`. The previous slug, `heyaura-portfolio`, redirects to this listing, preserving its version history and existing links.

Before the first release:

1. Choose the ClawHub account or organization that will own the skill and create a publishing token with access to it.
2. Add the token as the GitHub Actions repository secret `CLAWHUB_TOKEN`. Set the repository variable `CLAWHUB_OWNER` to the ClawHub owner handle.
3. Review ClawHub's [MIT-0 publishing terms](https://github.com/openclaw/clawhub/blob/main/docs/skill-format.md#license). Publishing makes the skill bundle free to use, modify, and redistribute without attribution; heyAura API requests still use paid x402.
4. Publish a GitHub release from the intended commit with a tag matching the skill's `package.json` version, initially `v1.0.0`. The workflow sends that version and the release notes to ClawHub.

For later releases, update `skills/heyaura/package.json` and its lockfile version together, commit the changes, and publish the matching `vX.Y.Z` release. Check the Actions run and the ClawHub listing after publishing; an upload can remain under review before it becomes publicly installable.

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
