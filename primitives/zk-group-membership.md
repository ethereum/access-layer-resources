---
name: zk-group-membership
last_reviewed: 2026-08-19
maturity: production
guarantees: [I-4, I-5]

related:
  requires: []
  composes_with: [oprf]
  alternative_to: []
  see_also: [anonymous-credentials]
---

# ZK group membership

## What it is

A member of a group proves they belong to it, and says something as a member, without revealing which member they are. A scoped nullifier accompanies each signal: unique per identity and per context, it blocks double-use inside a scope while staying uncorrelatable across scopes.

## What it guarantees

I-4: sybil resistance without identity, since being in the group is the whole bar and the group can be built from any admission rule (a deposit, an attestation, a ticket). I-5: per-scope pseudonymity by construction, one identity, unlinkable appearances.

## How it works

1. [user] Generates a private identity and publishes only its commitment.
2. [operator] Admits the commitment into the group's Merkle tree, on chain or off.
3. [user] Proves membership client-side and signals, emitting the scoped nullifier for this context.
4. [contract] Verifies the proof against the group root.
5. [contract] Records the nullifier once per scope; a second use in the same scope fails, a use in another scope is a fresh pseudonym.

## Trust model

Circuit soundness plus the proof system's ceremony carry the cryptography. The real gate is admission: whoever controls who enters the group is the residual issuer, and bootstrapping inclusion without recreating a gatekeeper is the open design question the identity domain states. Once inside, no operator can tell which member signaled.

## Known limits

- The anonymity set is the group; a small or skewed group protects little, and admission timing can fingerprint members.
- Admission centralization is the failure mode to design against: open or multi-source admission keeps the gate from becoming the identity system it replaced.
- Nullifier scope design is where deployments go wrong; a scope too broad links contexts, too narrow re-enables double-use.
- Proving is browser-feasible; this is one of the cheap primitives.
- Post-quantum: proofs are pairing-based today, so a CRQC forges membership; past anonymity survives on hash-based commitments.

## Implementations

[Semaphore](https://github.com/semaphore-protocol/semaphore) (PSE; v4 audited, trusted-setup ceremony completed 2024) with sustained use across [Zupass](https://github.com/proofcarryingdata/zupass) and others; a modified fork underlies a major proof-of-personhood system. Tooling card: [semaphore](../tooling/semaphore.md).

## Further reading

- [Semaphore documentation](https://docs.semaphore.pse.dev/)
- [Semaphore v4 audit](https://semaphore.pse.dev/Semaphore_4.0.0_Audit.pdf), PSE
- [Rate-Limiting Nullifier documentation](https://rate-limiting-nullifier.github.io/rln-docs/), the anonymous rate-limiting extension
- [Zupass](https://github.com/proofcarryingdata/zupass), proof-carrying data in practice
