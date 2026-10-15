---
name: zk-proof-of-personhood
last_reviewed: 2026-10-06
maturity: usable
implements: [anonymous-credentials]
specs: [https://github.com/ethereum/access-layer-specs/blob/main/specs/5-zk-proof-of-personhood/README.md]
guarantees: [I-1, I-3]
---

# zkID proof of personhood

## What it implements

A document proof under [anonymous-credentials](../primitives/anonymous-credentials.md) for online forums: the user proves possession of a valid issuer-signed X.509 certificate and receives a one-time verified-personhood status without disclosing certificate attributes (I-1). With the physical IC card profile, the key stays on the card and proofs are generated on the user's device (I-3). The mobile-app profile holds the user's key on an issuer-operated signing server and does not meet I-3. A deterministic nullifier blocks a second verification with the same certificate. Verification runs off chain in this version.

## Integration guide

Prerequisite: users holding Taiwan MOICA citizen certificates (MOICA-G2 or G3), and a verifier server. Other issuers need code changes in the verifier.

1. [app] Runs the Go HTTP and gRPC verifier.
2. [user] Generates the two linked proofs (certificate chain and device signature) on mobile or in the browser.
3. [app] Verifies the proofs, checks revocation, and records the nullifier.

Its entry in access-layer-specs is [5/ZK-PROOF-OF-PERSONHOOD](https://github.com/ethereum/access-layer-specs/blob/main/specs/5-zk-proof-of-personhood/README.md), which points to the text in [ethereum/zkID](https://github.com/ethereum/zkID).

## Audit and maturity status

Deployed against two Taiwan MOICA credential profiles (physical IC card and mobile app) with the Ptt forum apps. The circuits have internal security reviews only (latest v3, 2026), no external audit. The code sits in a proof-of-concept folder (`wallet-unit-poc`). MIT; the Go verifier is MIT or Apache-2.0.

## Maintainer

zkID team, with the reference implementation on the [`RSA-X.509-Cert`](https://github.com/ethereum/zkID/tree/RSA-X.509-Cert) branch of ethereum/zkID and the Go verifier at [ethereum/go-zkid-verifier](https://github.com/ethereum/go-zkid-verifier).
