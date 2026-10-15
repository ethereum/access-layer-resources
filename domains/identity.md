---
name: identity
last_reviewed: 2026-08-17
---

# Identity

Identity applications let users prove things about themselves: names, credentials, attestations, memberships. The risks run in two directions: proofs that reveal more than the verifier needs, and issuers or registries that become chokepoints over who gets to prove anything at all.

## Functions

- Naming
- Issuing credentials and attestations
- Proving claims
- Membership and sybil resistance

## Guarantees

### I-1: Minimal disclosure by construction [P]

- **Property**: A verifier learns exactly the property being proven and nothing else. Where a narrower predicate serves the need (over 18, member of the group, holds a deposit), the app asks for the predicate, never the identity behind it.
- **Functions**: [Proving claims]
- **Motivation**: Every field disclosed outlives the interaction that needed it. A bar checking a birthdate does not need the address printed next to it, and an app that collects full identity for one predicate builds the database that later leaks or gets subpoenaed.
- **Primitives**: [anonymous-credentials](../primitives/anonymous-credentials.md) for selective-disclosure and document-predicate proofs.
- **Upgrade path**: Predicate proofs over existing documents and accounts are usable today; email-based proofs ship as circuits and SDKs, passport and eID proving is in production use, and other national-ID schemes remain pre-production. The design work is naming the narrow predicate before reaching for whole-identity rails.

### I-2: No issuer chokepoint [CR]

- **Property**: Participation never depends on a single issuer's or registry's continued goodwill: the app accepts multiple independent attestation sources by default, supports combining weaker signals, and no issuer can arbitrarily revoke a user's standing.
- **Functions**: [Issuing credentials and attestations, Naming]
- **Motivation**: An identity system with one root issuer is a permission system wearing a different name. Whoever controls issuance controls entry, pricing, and exile, and history says that control gets used.
- **Primitives**: None carded; attestation plurality and combination approaches are design practices.
- **Upgrade path**: Accept several ground truths per claim (document proofs, social-graph attestations, on-chain history) and weight them rather than requiring one.

### I-3: Local, non-custodial proving [S, CR]

- **Property**: Once a credential exists, generating and verifying proofs is local and non-custodial: no ongoing issuer or API involvement, nothing to hand a custodian, nothing an intermediary can switch off.
- **Functions**: [Proving claims]
- **Motivation**: A credential that phones home on every use is a subscription to the issuer's approval. The user's standing lapses the day the API does, and each proof event is logged by a party the verifier never sees.
- **Primitives**: [anonymous-credentials](../primitives/anonymous-credentials.md); client-side proving is practice, no card.
- **Upgrade path**: Client-side proof generation works today for group membership and document predicates. Proving cost on consumer hardware is the friction that pushes apps back toward hosted provers, and hosted proving reintroduces the intermediary.

### I-4: Sybil resistance without identity [P, CR]

- **Property**: Where the need is only sybil resistance or making abuse expensive, the app offers a non-identity path: proof of deposit, proof of stake or holdings, or anonymous membership in a vetted group.
- **Functions**: [Membership and sybil resistance]
- **Motivation**: Demanding official identity for rate-limiting is paying for a fence with a census. The app inherits identity's exclusions (no document, wrong document, revoked document) for a problem a bond would have solved.
- **Primitives**: [zk-group-membership](../primitives/zk-group-membership.md) for anonymous membership with double-use protection; [oprf](../primitives/oprf.md) for anonymous rate-limiting tokens; zero-knowledge deposits are practice, no card.
- **Upgrade path**: Anonymous group membership with double-signaling protection is mature and in sustained use. The open design question is bootstrapping group inclusion without recreating an issuer at the gate.

### I-5: Unlinkable reuse [P]

- **Property**: Presenting the same identity or credential twice, to the same verifier or different ones, yields proofs that cannot be linked to each other. Unlinkability from the issuance event additionally requires blind or hidden issuance; document-based proofs keep an issuer-side link to the source document. Where double-use must be blocked, per-context identifiers prevent it without enabling correlation across contexts.
- **Functions**: [Proving claims, Membership and sybil resistance]
- **Motivation**: A reusable identifier turns every verification into a tracking event. Verifiers who compare notes reconstruct the user's path through services, which is the profile I-1's field-hiding tried to prevent; hiding the fields achieves little if the pattern of use stays visible.
- **Primitives**: [anonymous-credentials](../primitives/anonymous-credentials.md) for multi-show unlinkability; [zk-group-membership](../primitives/zk-group-membership.md) for scoped nullifiers; [oprf](../primitives/oprf.md) where unique per-context identifiers must be issued without the issuer learning them.
- **Upgrade path**: Scoped nullifiers are standard in mature membership protocols. Multi-show unlinkable credential schemes exist and are entering ZK credential stacks; single-show designs that re-issue per use leak usage volume to the issuer, a tradeoff worth stating.

## Ship it

Integration guides by guarantee, added as tooling cards land:

- I-1, I-3: [zk-proof-of-personhood](../tooling/zk-proof-of-personhood.md)
- I-4, I-5: [semaphore](../tooling/semaphore.md)
