---
name: <primitive-slug>
last_reviewed: YYYY-MM-DD

# Maturity of the primitive itself, wherever it runs (not only on Ethereum):
#   research   - papers only, no usable implementation
#   concept    - spec exists, no usable code
#   usable     - working implementations, pilots, benchmarks
#   production - sustained real-world use anywhere
maturity: research | concept | usable | production

# Guarantee IDs this primitive can satisfy, defined in domains/.
guarantees: [W-1]

# Typed cross-references to other primitives. Slugs match
# primitives/<slug>.md and must resolve to an existing file.
related:
  requires: []        # hard dependency, cannot work without it
  composes_with: []   # works well together, optional
  alternative_to: []  # competing approach to the same guarantee
  see_also: []        # related for context

# OPTIONAL, for primitives with materially different variants (trust models
# that diverge, e.g. a shared-state primitive with co-SNARK / FHE / TEE
# flavors). Give each variant its own file and list the slugs here; keep this
# file as the aggregator. Delete otherwise.
# variants:
#   - name: "<variant name>"
#     primitive: <variant-slug>
#     summary: "<one-line trust-model difference>"
---

# <Primitive name>

## What it is

First-principles explanation in a few paragraphs. No project names here; implementations belong in [tooling/](../tooling/).

## What it guarantees

The guarantee(s) this primitive provides, referencing the IDs in frontmatter, and the mechanism by which it provides them.

## How it works

Numbered steps (5-8 max), each prefixed with the actor performing it in square brackets: `[user]`, `[wallet]`, `[contract]`, `[relayer]`, `[node]`, `[operator]`.

1. [user] ...
2. [wallet] ...

## Trust model

Who or what must behave honestly for the guarantee to hold, and what breaks when they fail. Honest-majority assumptions, hardware assumptions, liveness assumptions.

## Known limits

Performance costs, anonymity-set considerations, UX costs, and other limits a builder should know before committing. Post-quantum exposure and its mitigation belong here; encrypted or key-revealing data recorded on chain today can be harvested now and decrypted later, so every privacy primitive states what a CRQC breaks and what the migration path is.

## Implementations

Links to [tooling/](../tooling/) cards. Every implementation named here links to its open source code.

## Further reading

Papers and specs, as pinned permalinks.
