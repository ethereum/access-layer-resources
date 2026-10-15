---
name: <tool-slug>
last_reviewed: YYYY-MM-DD

# Maturity of this implementation (not of the underlying primitive):
maturity: research | concept | usable | production

# Optional: primitives this tool gives an app access to. Slugs match
# primitives/<slug>.md and must resolve. Omit when no card applies.
implements: [<primitive-slug>]

# Optional: links on the main branch to the specs in
# ethereum/access-layer-specs for the protocol this tool implements. Omit when there are none.
specs: [<link>]

# Guarantee IDs this tool satisfies when integrated as documented.
guarantees: [W-1, W-3]
---

# <Tool name>

<!-- Scope (decided 2026-08-17): tooling/ covers open source software an
application can integrate: libraries, SDKs, reference implementations, and
self-hostable services. End-user apps get cards only for their integrable
parts. A tool with a paid hosted plan qualifies if the documented integration
path is fully open source and self-hostable; the card states this plainly. -->

## What it implements

One or two sentences: the [primitive](../primitives/) and guarantees this tool delivers, with any deviation from the ideal trust model in one clause. Body target for the whole card: under 250 words.

## Integration guide

A map, never a tutorial: prerequisites in one line, at most four one-line steps, and the canonical docs link. The docs are the guide; this card is the map to them.

## Audit and maturity status

One or two lines, facts only: audits (linked), production evidence, license.

## Maintainer

Who maintains it, the repository, the docs, and the [ethereum.org developer-tools](https://ethereum.org/developers/tools/) page where one exists.
