---
name: semaphore
last_reviewed: 2026-08-19
maturity: production
implements: [zk-group-membership]
specs: [https://github.com/ethereum/access-layer-specs/blob/main/specs/3-semaphore-v4/README.md]
guarantees: [I-4, I-5]
---

# Semaphore

## What it implements

[zk-group-membership](../primitives/zk-group-membership.md) as contracts and JavaScript packages: anonymous group membership proofs with scoped nullifiers, proving in the browser. Group admission stays the integrator's design decision, which is where the primitive's trust concentrates.

## Integration guide

Prerequisite: a JavaScript app and a group admission rule.

1. [app] Install the `@semaphore-protocol` packages and deploy or reuse a group contract.
2. [user] Generates an identity; the app admits its commitment to the group.
3. [user] Proves membership and signals client-side, with the scope chosen per context.
4. [contract] Verifies and records the nullifier once per scope.

The [documentation](https://docs.semaphore.pse.dev/) is the guide. The protocol is specified in [3/SEMAPHORE-V4](https://github.com/ethereum/access-layer-specs/blob/main/specs/3-semaphore-v4/README.md).

## Audit and maturity status

v4 audited, trusted-setup ceremony completed 2024, sustained use (Zupass and others). MIT. The packages differ from the 3/SEMAPHORE-V4 draft on circuit input names and on how scope and message are hashed, so code built from the spec alone does not interoperate with them (tested 2026-10-06).

## Maintainer

PSE, at [semaphore-protocol/semaphore](https://github.com/semaphore-protocol/semaphore); listed in the [ethereum.org developer tools](https://ethereum.org/developers/tools/).
