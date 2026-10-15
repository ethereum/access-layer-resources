# Contributing

This repository maps application domains to the CROPS guarantees they can offer users, the primitives behind those guarantees, and the tooling that ships them. [README.md](README.md) explains the structure; [AGENTS.md](AGENTS.md) is the authoritative rule set that this guide summarizes.

## Ground rules

- Descriptive voice: properties and facts, no recommendations, no RFC-2119 keywords (MUST, SHOULD).
- No marketing language. Every adjective must be checkable; the banned vocabulary list lives in [AGENTS.md](AGENTS.md).
- Never name applications in gap descriptions; naming them as factual implementations with source links is fine.
- One concept per file, frontmatter per the `_template.md` of each folder, cross-references by ID and slug rather than restated text.

## Adding a guarantee to a domain page

Guarantees live in `domains/` as `### <ID>: <short name> [<CROPS letters>]` headings; the heading is the declaration. Each block carries five fields: Property, Functions (bracketed list from the page's Functions section), Motivation, Primitives (links to cards, or bare slugs for planned ones; the maintainers track planned cards outside the repository), and Upgrade path.

IDs are permanent: never renumber, never reuse. Reserved letters: W wallet, D defi, P payments, I identity, O oracle, X data-indexing, R rollup, G governance.

## Adding a primitive card

Copy [primitives/_template.md](primitives/_template.md). Maturity rates the primitive itself wherever it runs, not only on Ethereum: `research` (papers only), `concept` (spec, no usable code), `usable` (working implementations, pilots), `production` (sustained real-world use anywhere). Slugs in `related` must resolve to existing files. Post-quantum exposure and its mitigation belong in Known limits. Implementations must link open source code.

## Adding a tooling card

Copy [tooling/_template.md](tooling/_template.md). Scope: open source software an application can integrate (libraries, SDKs, reference implementations, self-hostable services). A tool with a paid hosted plan qualifies if the documented integration path is fully open source and self-hostable, stated plainly on the card. The Integration guide section is the reason this repository exists; keep it current.

## Review flow

- One card or one coherent change per pull request, against `master`.
- Commit messages are single-line conventional commits (`docs: add oracle guarantees`).
- CI runs markdownlint and lychee (link check); both must pass.
- Factual claims are checked against primary sources during review; cite specs and papers, pinned to a version or date where they can move.

## Licensing

This repository is dedicated to the public domain under [CC0 1.0](LICENSE). By contributing, you waive copyright and related rights in your contribution to the fullest extent permitted by law.
