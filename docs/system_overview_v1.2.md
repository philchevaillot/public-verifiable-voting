# Full Specification (v1.2)

Version 1.2 — Verification model and coercion-resistance update

---

## 1. Identity Layer
- Each citizen has a 10-year long-term key pair
- Key is legally bound to the citizen, not the device
- One active trusted device at a time
- Device acts as secure execution environment only

---

## 2. Election Identity
- One temporary election identity per election
- Generated locally at voting time (not pre-generated)
- Derived/blinded and unlinkable across elections
- Authorized by long-term key
- Reusable across sessions for the same election
- Not persistent beyond election lifecycle

---

## 3. Session Model
- Multiple sessions allowed per election
- Same temporary identity reused
- No new identity created on retry
- Identity reconstructable securely during retries

---

## 4. Voting Rules
- One vote → one ballot
- No forks allowed
- One identity per election

---

## 5. Vote Finality
- Vote is final only when included in a published sealed block
- No intermediate state is valid
- App must display: “waiting for publication”

---

## 6. Pending vs Final State
- Pending: submission in progress, internally locked
- Final: published on public ledger
- Pending does NOT consume voting right

---

## 7. Failure Handling
- If interrupted before publication → vote lost
- User must restart from scratch
- No background retry allowed

---

## 8. Duplicate Handling
- If multiple ballots exist:
  - First included in a published sealed block wins
  - Others ignored

---

## 9. Vote Consumption
- Voting right consumed only at final publication

---

## 10. Ballot Structure

Each ballot contains:
- Temporary election identity
- Encrypted vote (vector-based, homomorphic)
- Zero-knowledge proof (ZKP)

---

## 11. Ballot Validity Proof (Mandatory)

ZKP must prove:
- Exactly one valid choice selected
- No multiple selections
- No inflated values
- Valid encoding structure

Proof must be publicly verifiable.

---

## 12. Privacy Model
- No public mapping between identity and vote
- At no point should (temporary ID ↔ vote choice) be derivable, even transiently
- No transferable receipt possible

---

## 13. Verification Right Model

The system retains a voter-specific private verification right, but it is not exposed as a user-controlled ballot-opening mechanism.

### Principles
- A unique verification right exists for each ballot
- It is derived from voter-controlled secret material
- It is associated with the voter’s authorized device and election context
- It is not usable as a general-purpose local reveal tool
- It can only be exercised through the controlled verification architecture

### Purpose
This right exists only to authorize ballot verification under controlled conditions, not to allow unrestricted private decryption by the voter.

---

## 14. Verification Model

Verification is not performed on the voter’s personal device.

Instead:
- the voter device authorizes verification
- ballot reveal occurs only on a certified verification terminal
- the voter device never receives plaintext ballot data

Verification properties:
- one-time verification right per ballot
- consumed at session start
- available only after election closure
- limited to a defined verification window

---

## 15. Controlled Verification Model

After election closure, verification is performed under controlled conditions:

- access through official verification sites or events
- fixed or mobile infrastructure
- single-person access to a private booth
- no bags, accessories, or recording devices
- secure environment similar to controlled facilities

### Verification process
- voter device pairs with a certified terminal
- ballot is displayed only on the terminal
- ballots are revealed one at a time
- verification right is consumed immediately upon session start

### Terminal display behavior
- once revealed, the ballot is displayed for a short predefined duration
- display clears automatically
- no manual pause, replay, extension, or export is allowed

---

## 16. Pairing Model

The pairing mechanism includes:
- signed terminal challenge
- terminal authenticity verification by the phone
- one-time session nonce
- short session lifetime
- explicit user confirmation

The phone proves only:

> possession of a valid, unused verification right

No direct citizen identity data is required at the reveal site.

---

## 17. Verification Token Model

The system uses:
- one verification right per ballot
- storage within the voter application
- controlled re-provisioning mechanism
- possession-based authorization
- validation without identity exposure

The reveal site validates rights, not identity.

---

## 18. Reveal Storage

- reveal payload is protected and only accessible through the controlled verification process
- no direct user-controlled decryption pathway exists
- no reusable or exportable reveal artifact is generated

---

## 19. Coercion Resistance Model

A central objective of the system is to reduce vote buying and coercion risks.

Many verifiable systems allow voters to demonstrate their vote freely, enabling:
- vote buying
- coercion
- external pressure

### Design approach
This system limits transferable proof through:
- post-election-only verification
- limited verification window
- single-use ballot reveal
- controlled environment access
- prohibition of recording or external devices
- terminal-only ballot display
- immediate consumption of verification rights
- automatic clearing of terminal display

### Security objective

> A voter can verify their ballot, but cannot reliably prove their vote to a third party.

### Effect
- buyers cannot easily obtain proof
- sellers cannot easily demonstrate compliance

### Important note
This model improves coercion resistance but does not eliminate coercion entirely.

Its goal is to significantly reduce:
- scalable vote buying
- systematic coercion
- transferable proof of vote

---

## 20. Tally System
- Homomorphic encryption used for aggregation
- Votes combined without decryption

---

## 21. Final Decryption
- Only aggregate results decrypted
- Uses threshold cryptography (multiple key holders)
- No individual ballot decryption possible

---

## 22. Public Verification
- Entire ledger is public
- Anyone can verify:
  - ballot validity (ZKP)
  - tally correctness (ZKP)
- No trust in backend required

---

## 23. Physical vs Digital Voting

The system separates voting into two independent channels.

### Physical voting
- traditional in-person voting process
- identity verification and ballot casting unchanged

### Digital voting
- requires official in-person enrollment
- credential generation before voting

### Shared rule
- a voter may use only one channel

---

## 24. Channel Commitment Rule

The physical voting right is disabled:

> when the voter initiates the official digital enrollment process

This commitment is:
- immediate
- official
- irreversible

Once digital enrollment begins:
- physical voting is permanently blocked
- the voter must complete the digital path
- no fallback to physical voting is allowed

---

## 25. Security Principles
- No hidden states
- No backend trust
- Strict input validation
- System designed to absorb attacks

---

## 26. Infrastructure Principles
- Non-discoverable endpoints
- Layered DDoS resistance (network-level + protocol-level)
- Queue-based processing
- Fast block publication (seconds target)

---

## 27. Device Security
- Requires secure OS environment
- Keys stored in secure hardware
- Non-exportable secrets
- Compromised device → voter must use physical voting fallback or re-enroll according to system policy

---

## 28. Physical Fallback
- User is either digital or physical voter
- Never both simultaneously

---

## 29. Governance Boundary
- System defines technical guarantees only
- Law enforcement, monitoring, and attribution handled by authorities
- Physical and procedural security of controlled verification environments is assumed to be provided by the public operator

---

## 30. System Philosophy
- Full public verifiability
- Strong privacy guarantees
- Minimal trust assumptions
- Constrained, non-transferable verification
- Simplicity and determinism

---

## SUMMARY

A publicly verifiable, privacy-preserving voting system with:
- no single point of trust  
- encrypted and auditable ballots  
- constrained voter verification  
- clear physical/digital channel separation  
- and no transferable proof of vote
