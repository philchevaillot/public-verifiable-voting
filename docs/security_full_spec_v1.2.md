# Full Specification (v1.2)

Version 1.2 — Verification model, coercion-resistance, and production security

---

## 1. Identity Layer
- Each citizen has a 10-year long-term key pair
- Key is legally bound to the citizen, not the device
- One active trusted device at a time
- The device acts as a secure execution environment only

---

## 2. Election Identity
- One temporary election identity per election
- Generated locally at voting time
- Derived or blinded and unlinkable across elections
- Authorized by the long-term key
- Reusable across sessions within the same election
- Not persistent beyond the election lifecycle

---

## 3. Session Model
- Multiple sessions are allowed
- The same temporary election identity is reused
- No new election identity is created on retry
- Identity reconstruction is secure and deterministic

---

## 4. Voting Rules
- One vote corresponds to one ballot
- No forks are allowed
- One election identity per election

---

## 5. Vote Finality
- A vote is final only when included in a sealed published block
- No intermediate state is valid

---

## 6. Pending vs Final State
- Pending: submission in progress
- Final: published on the public ledger
- Pending state does not consume the voting right

---

## 7. Failure Handling
- If interrupted before publication, the vote is lost
- The voter must restart
- No background retry is allowed

---

## 8. Duplicate Handling
- If multiple ballots exist, the first ballot included in a sealed block wins
- All other ballots are ignored

---

## 9. Vote Consumption
- The voting right is consumed only at final publication

---

## 10. Ballot Structure
Each ballot contains:
- Temporary election identity
- Encrypted vote
- Zero-knowledge proof (ZKP)

---

## 11. Ballot Validity Proof
The ZKP must prove:
- Exactly one valid choice is selected
- No multiple selections are encoded
- Encoding is valid

The proof is publicly verifiable.

---

## 12. Privacy Model
- No public identity-to-vote linkage
- No transferable receipt
- No derivable mapping between identity and vote at any stage

---

## 13. Verification Right Model
- One verification right exists per ballot
- The verification right is created at voting time
- It is device-bound
- It is non-exportable
- It is single-use
- It is non-recoverable
- It is not a standalone user-controlled reveal key

---

## 14. Verification Model
- Verification is available only after election closure
- Verification is time-limited to a maximum of one year
- The voter device authorizes the process but never reveals the ballot
- The voter device never receives plaintext ballot data

---

## 15. Controlled Verification
Verification occurs in certified controlled environments:
- Single-person access
- No recording devices
- Controlled booth or equivalent privacy-preserving structure

### Flow
- Pre-verification outside the reveal chamber
- Ballot selection in an airlock or controlled transition space
- Reveal inside the chamber
- Immediate controlled exit after display cycle

---

## 16. Reveal Unit Architecture
- Reveal units are stateless between sessions
- No persistent ballot or session data is stored
- Units are fully interchangeable
- Availability is provided through horizontal redundancy
- No single unit is critical infrastructure

Each session operates as:
- Fresh trusted state
- Single reveal cycle
- Complete local state destruction after use

---

## 17. Terminal Trust Model
Each reveal unit must prove:
- Identity through an official certificate
- Integrity through measured boot and attestation
- Freshness through a per-session challenge

Validation model:
- The voter device verifies terminal identity and session validity
- Backend infrastructure independently verifies terminal integrity and trust state

---

## 18. Pairing Model
Pairing includes:
- Signed terminal challenge
- One-time nonce
- Short session lifetime

The phone proves only:

> possession of a valid unused verification right

No citizen identity is exposed at the reveal site.

---

## 19. Verification Consumption Registry

### Purpose
- Enforce single-use verification
- Prevent replay across reveal units
- Prevent race conditions

### Model
- Hybrid ephemeral registry
- No single critical node

### Authority
- The client never declares consumption
- The trusted reveal infrastructure is the sole authority for consumption recording

### Trigger
Consumption occurs only when:
- Ballot display completes successfully
- The reveal monitor shuts down

If no ballot is displayed:
- The verification right remains unused

### Minimal stored data
- Opaque verification-right identifier or hash
- State: unused or consumed
- Optional timestamp or event reference

The registry stores:
- No citizen identity
- No vote content

### Lifecycle
- Active only during the one-year verification period
- Decommissioned at archive time

---

## 20. Reveal Execution Model
The reveal model is semi-online:
- Authorization is online
- Reveal runs locally
- Completion is synchronized afterward

The ballot is rendered from local trusted state inside the reveal unit.
No live plaintext ballot transfer occurs during the display cycle.

---

## 21. Reveal Storage
- Reveal data exists only in trusted transient runtime
- No persistent reveal state remains after shutdown
- All local reveal state is destroyed after session completion

---

## 22. Coercion Resistance Model
The system reduces coercion and vote-buying risk through:
- No ballot reveal on the voter’s personal device
- Controlled verification environment
- Brief display duration
- Automatic clearing
- Single-use verification
- No replay
- No exportable proof path

Goal:

> A voter can verify their ballot, but cannot reliably prove it to a third party.

---

## 23. Tally System
- Homomorphic aggregation is used
- No individual ballot decryption occurs during tallying

---

## 24. Final Decryption
- Final aggregate decryption uses threshold cryptography
- Threshold is strict 7-of-10
- Key holders are mixed independent actors
- No full private key reconstruction is allowed

This configuration assumes:
- Strong logistical coordination
- Mandatory participation protocols
- Operational redundancy sufficient to avoid institutional deadlock

---

## 25. Public Verification
Anyone can verify:
- Ballot validity
- Tally correctness

No backend trust is required for public verification.

---

## 26. Physical vs Digital Voting
- Physical and digital voting are strictly separated
- A voter may use only one channel

---

## 27. Channel Commitment
- Entering official digital enrollment disables physical voting
- This commitment is immediate and irreversible

---

## 28. Device Security
- Hardware-backed secure storage is required
- Verification rights are non-exportable
- A lost device permanently destroys any unused current-election verification rights stored on it

---

## 29. Verification Lifecycle
- Verification is available for at most one year after election closure
- The verification right is deleted from the device after successful use
- Client-side deletion is not authoritative
- The authoritative consumption record is maintained by the reveal infrastructure

---

## 30. Election Archival
After one year:
- Verification is permanently disabled
- The election ledger is archived
- The ephemeral consumption registry is decommissioned

No further ballot verification is possible after archival.

---

## 31. Audit Logging
Only minimal operational logging is allowed:
- Terminal or reveal unit identifier
- Timestamp
- Session outcome

The system must never log:
- Citizen identity
- Vote content
- Readable ballot linkage
- Data sufficient to reconstruct who verified what

---

## 32. Security Principles
- No hidden states
- No trust in backend for public verification
- Minimal data exposure
- Stateless critical reveal components

---

## 33. Infrastructure Principles
- Non-discoverable endpoints
- Layered DDoS resistance
- Queue-based processing

---

## 34. Governance Boundary
- The system defines technical guarantees
- Legal enforcement and attribution remain external to the system
- Physical and procedural security of reveal environments is assumed to be provided by authorized operators

---

## 35. Re-enrollment
- Official re-enrollment invalidates the previous device immediately
- The old device is permanently disabled for future system use

---

## 36. Authorized Device Migration
- A voter may migrate their authorized device only through an official migration process
- Migration immediately invalidates the previous device
- No period of dual active authorization is permitted
- Migration preserves long-term identity authorization for future elections
- Current-election verification rights do not migrate
- Any unused current-election verification rights remain bound to the old device and are lost upon migration

---

## 37. System Philosophy
- Public verifiability
- Strong privacy
- Constrained verification
- No transferable proof of vote
- Deterministic behavior
- No single point of trust

---

## Summary
A publicly verifiable voting system with:
- No single point of trust
- Stateless, redundant verification infrastructure
- Strict single-use verification rights
- Controlled, non-transferable ballot verification
- Minimal, ephemeral enforcement of verification consumption
