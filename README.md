# Access Layer Resources

An open knowledge base for building Ethereum applications with CROPS properties: Censorship Resistance, Open Source and Free, Privacy, and Security.

This repository describes, in first-principles terms, the guarantees a CROPS-aligned application can offer its users, the cryptographic and protocol primitives that provide those guarantees, and the tooling that implements them.

## Who this is for

- **Application builders** (wallets, DEXes, oracles, and other domains): start from your domain page and follow the links.
- **Anyone using an LLM to work on these topics**: the repository is structured as high-quality model context. One concept per file, strict frontmatter, stable cross-reference IDs. See [AGENTS.md](./AGENTS.md).

## How to navigate

1. [domains/](./domains/) is the entry point. Each page decomposes an application domain into its functions and states the desired properties of each function as identified guarantees (for example W-1: network access does not link a user's addresses to their IP).
2. [primitives/](./primitives/) explains the building blocks behind each guarantee: what the primitive is, what it buys in CROPS terms, its trust model and maturity.
3. [tooling/](./tooling/) lists implementations and integration guides, tagged with the guarantee IDs they satisfy; it selects from the broader curated index at [ethereum.org/developers/tools](https://ethereum.org/developers/tools/).

Shared vocabulary is defined once in [GLOSSARY.md](./GLOSSARY.md).

## Scope and stance

This repository is descriptive. It states properties, explains how they can be achieved, and records the available upgrade paths and their maturity. It does not score, certify, or endorse specific applications or vendors.

## Contributing and license

Contributions are welcome; [CONTRIBUTING.md](./CONTRIBUTING.md) covers the format, the voice rules, and the review flow. Everything here is dedicated to the public domain under [CC0 1.0](./LICENSE).
