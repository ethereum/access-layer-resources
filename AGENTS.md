# Conventions

This repository doubles as LLM context. Every rule below exists to keep it reliable in that role.

## Files

- One concept per file. A file covers exactly one domain, primitive, tool, or spec.
- The folder is the type: `domains/`, `primitives/`, `tooling/`. There is no `type` frontmatter field.
- New files start from their folder's `_template.md`.

## Frontmatter

Shared fields:

```yaml
---
name: <kebab-case-slug, matches filename>
last_reviewed: YYYY-MM-DD
guarantees: [W-1, W-3]   # IDs satisfied (primitives and tooling; not domains)
---
```

Primitives additionally carry `maturity`, typed `related` cross-references, and optional `variants` for primitives whose flavors have diverging trust models. There is no per-card CROPS grading: the repository implies CROPS by design, and a primitive's letters follow from the guarantees it satisfies (decision 2026-08-17, after per-card grading was dropped as an iptf-map holdover). Post-quantum exposure is not frontmatter; it is stated in the card's Known limits section with its mitigation. Tooling carries `maturity`, an optional `implements` list (primitive slugs the tool gives an app access to; slugs must resolve to cards), and an optional `specs` list (links on the `main` branch to the specs in [access-layer-specs](https://github.com/ethereum/access-layer-specs) for the protocol the tool implements; omit when there are none).

Maturity levels, rated for the primitive or tool itself wherever it runs (not only on Ethereum): `research` (papers only), `concept` (spec, no usable code), `usable` (working implementations, pilots, benchmarks), `production` (sustained real-world use anywhere).

Automated checks are markdownlint and lychee (configs at the repo root, run by `.github/workflows/lint.yml`). Structural validation (frontmatter fields, guarantee-ID resolution, slug resolution, no duplicate IDs) is a manual gate at draft time by decision (2026-08-18); do not add custom validation scripts.

## Guarantee IDs and block format

- Domains declare guarantees as `### <ID>:` headings; the heading is the declaration. IDs are one uppercase letter per domain plus a number. Reserved letters: W wallet, D defi, P payments, I identity, O oracle, X data-indexing, R rollup, G governance.
- IDs are permanent. Never renumber. A withdrawn guarantee keeps its ID and is marked withdrawn.
- Primitives and tooling reference guarantees by ID in frontmatter and prose. This is the only cross-reference mechanism; do not restate guarantee text in other files.
- Guarantee blocks are markdown with fixed `- **Field**:` bullets, never YAML frontmatter. Decision recorded 2026-08-17: markdown keeps the blocks readable, diffable, annotatable in review tools, and deep-linkable via heading anchors; the fixed field format keeps them machine-parseable.
- In the Primitives field, mention primitives only as links to existing cards or as bare slugs in inline code. Every bare slug is a planned card; the maintainers track the planned-card list outside the repository. A mention not worth a future card is not a primitive.
- Guarantees carry no maturity rating. Maturity belongs to primitives and tooling (their frontmatter), one rating per path; a guarantee's achievability is narrated in its Upgrade path field and read off the linked cards.

## Cross-references

- Primitive-to-primitive links go in the `related` frontmatter block (`requires`, `composes_with`, `alternative_to`, `see_also`), as slugs matching `primitives/<slug>.md`.
- External references use permalinks pinned to a commit or tag, plus the EIP/ERC number where applicable.

## Voice

- Descriptive. State properties and facts. No RFC-2119 keywords (MUST, SHALL), no recommendations, no endorsements.
- Use terms as defined in [GLOSSARY.md](./GLOSSARY.md); do not invent synonyms.
- Never name specific applications when describing gaps or weaknesses. Upgrade path fields describe routes and categories of behavior; implementations may be named as routes, never shamed as gaps.

## No marketing language

This repository describes; it never sells. Marketing tone destroys the credibility the repository exists to build.

- Banned vocabulary, in any form: seamless, robust, powerful, cutting-edge, state-of-the-art, best-in-class, world-class, industry-leading, leading, next-generation, enterprise-grade, battle-tested, game-changing, revolutionary, groundbreaking, innovative, effortless, blazing, turnkey, holistic, unparalleled, unmatched, premier, ultimate, unprecedented.
- Banned verbs of persuasion: unlock, empower, supercharge, elevate, streamline, transform, revolutionize, harness, leverage (as a verb).
- No superlatives and no unverifiable adjectives. Every adjective must be checkable; if deleting it changes nothing verifiable, delete it.
- Benefits are stated as properties with a mechanism ("queries leave no address-to-IP link because lookups run over PIR"), never as value claims ("gives users peace of mind").
- No exclamation marks, no calls to action, no "just" or "simply".
- Section and field names are plain nouns describing content, never persuasion framing. Precedent: "State of the art" was renamed "Upgrade path" because the name overclaimed.
- The rule applies to everything in the repository, including templates, comments, and commit messages.

## Formatting

- No em-dashes. Use commas, colons, or separate sentences.
- No contrastive constructions of the form "X is not Y, it's Z". Plain declaratives.
- Bold only for structural labels, never for emphasis in prose.

## Before pushing

Check manually (structural validation is a deliberate manual gate; see Frontmatter above): frontmatter matches the template, guarantee IDs resolve to a domain heading, internal links resolve, terminology matches the glossary.
