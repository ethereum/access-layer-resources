---
name: anonymous-credentials
last_reviewed: 2026-08-19
maturity: usable
guarantees: [I-1, I-3, I-5]

related:
  requires: []
  composes_with: [oprf, tls-oracles]
  alternative_to: []
  see_also: [zk-group-membership]
---

# Anonymous credentials

## What it is

Anonymous credentials let a holder prove statements about a credential without showing the credential itself. Two flavors exist. Signature schemes designed for it (BBS-class) support blind issuance, selective disclosure, and presentations that cannot be linked to each other. Document proofs go the other way: a zero-knowledge circuit proves predicates over artifacts whose issuer never opted in, a DKIM-signed email or a passport's NFC chip, doing what the issuer would not.

## What it guarantees

I-1: the verifier learns the predicate (over 18, holds the account) and nothing else. I-3: once the credential exists, proving is local; no issuer or API participates per presentation. I-5: multi-show unlinkability where the scheme provides it; document proofs keep an issuer-side link to the source artifact.

## How it works

1. [operator] Issues a signature over attributes, blind where issuance-unlinkability matters, or the signature already exists (email, passport).
2. [user] Holds the credential; nothing registers anywhere.
3. [user] Generates a zero-knowledge proof of the predicate, client-side.
4. [app] Verifies against the issuer's public key; no callback to the issuer.
5. [user] Optionally derives a per-context identifier where double-use must be blocked.

## Trust model

The issuer vouches for claim truth and nothing else: a lying issuer produces valid proofs of false claims. Without blind issuance the issuer knows every attribute it signed, so an issuer-verifier collusion can match presentations to issuance whenever disclosed attributes narrow the candidate set. Disclosed attributes can re-correlate what the cryptography hid: a proof revealing a rare combination is a fingerprint.

## Known limits

- Client-side proving cost is the UX constraint: tens of seconds, up to minutes, for initial document proofs on consumer hardware; follow-up disclosure proofs run in seconds.
- Revocation fights privacy: status checks that call the issuer are tracking; status lists with herd privacy are the mitigation.
- Document proofs break when the source changes formats or signing practices, without notice.
- The standards are in flux: BBS remains pre-RFC, with the base CFRG draft lapsed while the blind-issuance extension stays active, and its W3C integration is a candidate recommendation.
- Post-quantum: pairing-based BBS falls to a CRQC (forged credentials); document proofs fall twice over, through their classical document signatures (RSA, ECDSA) and the classical proof systems they run on, with only the hash commitments inside surviving.

## Implementations

[ZKPassport](https://github.com/zkpassport/circuits) (passport and eID predicates, live apps and SDK) and [zkEmail](https://github.com/zkemail) (email predicates, circuits and SDKs); tooling cards for both pending. Tooling card: [zk-proof-of-personhood](../tooling/zk-proof-of-personhood.md), proof of personhood from X.509 certificates.

## Further reading

- [An efficient system for non-transferable anonymous credentials](https://eprint.iacr.org/2001/019), Camenisch and Lysyanskaya, 2001; the ancestor
- [BBS signature scheme](https://datatracker.ietf.org/doc/draft-irtf-cfrg-bbs-signatures/), IETF CFRG draft
- [Data Integrity BBS cryptosuites](https://www.w3.org/TR/vc-di-bbs/), W3C
- [ZK Email: decentralized identity via email](https://blog.aayushg.com/zkemail/), Aayush Gupta
- [ZKPassport documentation](https://docs.zkpassport.id/), predicate proofs over passports and eIDs
