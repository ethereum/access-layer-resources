---
name: <domain-slug>
last_reviewed: YYYY-MM-DD
---

# <Domain name>

One paragraph: what applications in this domain do, and why CROPS properties matter to their users.

## Functions

The functions an application in this domain performs. Guarantees attach to these.

- <function 1>
- <function 2>

## Guarantees

One block per guarantee. The `### <ID>:` heading is the guarantee's declaration. IDs are permanent, never renumber. The bullet fields below are a fixed, parseable format; see [AGENTS.md](../AGENTS.md).

### <ID>: <short name> [<CROPS letters>]

- **Property**: the guarantee stated descriptively, in one sentence.
- **Functions**: bracketed list of the functions above this attaches to, e.g. [Network access, Transaction broadcast].
- **Motivation**: concrete end-user motivation. Who is harmed without it, and how.
- **Primitives**: slugs or links only. Link to the card when it exists (`[stealth-addresses](../primitives/stealth-addresses.md)`); use a bare slug in inline code (`` `pir` ``) when it does not; the maintainers track planned cards outside the repository. A mention not worth a future card is not a primitive; describe it in prose in another field.
- **Upgrade path**: light and construction-oriented: how a builder gets from today's default toward the guarantee, which routes exist, how far each goes, and the tradeoffs between them. Name implementations where useful. The problem and its prevalence belong in Motivation, not here. Maturity is not rated here: it lives on the primitive cards, each path its own.

## Ship it

Links to [tooling/](../tooling/) integration guides, listed by the guarantee IDs they satisfy.
