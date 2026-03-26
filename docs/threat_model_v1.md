# Threat Model (v1)

Version 1 — Aligned with Full Specification v1.2

---

## 1. Purpose

This document defines the security assumptions, attacker model, guarantees, and limitations of the system.

It complements the full specification by clarifying:

- what the system defends against  
- what it does not defend against  
- where trust is placed  
- what risks remain  

---

## 2. System Overview (Security Perspective)

The system is a publicly verifiable voting architecture combining:

- encrypted ballots and public ledger publication  
- homomorphic tally and threshold decryption  
- device-bound, non-exportable verification rights  
- controlled, terminal-based ballot verification  
- stateless, redundant reveal infrastructure  
- minimal, ephemeral consumption enforcement  

---

## 3. Trust Boundaries

### 3.1 Voter Device
- Stores long-term identity key and verification rights  
- Uses hardware-backed secure storage  
- Considered **partially trusted**

Assumptions:
- secure hardware is not trivially extractable  
- device may still be compromised at the application or OS level  

---

### 3.2 Reveal Unit (Verification Terminal)
- Certified hardware with secure/measured boot  
- Provides controlled ballot reveal  
- Stateless between sessions  
- Considered **trusted but auditable**

Trust basis:
- certification process  
- cryptographic identity  
- measured boot and attestation  

Residual risk:
- physical tampering  
- supply-chain compromise  

---

### 3.3 Backend / Verification Infrastructure
- Handles authorization, coordination, and consumption registry  
- Does not require trust for public verification  
- Constrained by minimal data exposure  

---

### 3.4 Key Holders
- Distributed actors holding threshold shares  
- No single entity can decrypt results  
- Trust is **distributed and partial**

---

### 3.5 Physical Verification Environment
- Controlled access (single-person, no recording devices)  
- Enforced by operators  

Assumption:
- environment rules are properly enforced  

---

## 4. Attacker Model

### 4.1 External Network Attacker
Capabilities:
- intercept traffic  
- attempt replay  
- attempt MITM  

Mitigations:
- encryption  
- nonce-based challenges  
- attestation validation  

---

### 4.2 Malicious Client (Compromised Device)
Capabilities:
- modified application  
- bypass UI restrictions  
- attempt replay or duplication  

Mitigations:
- device-bound, non-exportable verification rights  
- reveal requires certified terminal  
- consumption enforced by infrastructure, not client  

---

### 4.3 Cloning / State Duplication Attacker
Capabilities:
- duplicate device state before use  
- attempt parallel verification  

Mitigations:
- hardware-backed storage  
- ephemeral consumption registry  
- atomic check-and-consume enforcement  

---

### 4.4 Malicious Operator / Insider
Capabilities:
- attempt to log or correlate data  
- attempt infrastructure misuse  

Mitigations:
- strict minimal logging policy  
- no identity or vote content stored  
- stateless reveal units  
- distributed trust for decryption  

---

### 4.5 Terminal Tampering Attacker
Capabilities:
- replace or modify reveal unit  
- inject malicious software  

Mitigations:
- certificate-based identity  
- measured boot and attestation  
- backend trust validation  
- per-session verification  

---

### 4.6 Coercion Attacker
Capabilities:
- force voter to reveal vote  
- attempt vote buying  
- attempt recording  

Mitigations:
- no ballot reveal on personal device  
- controlled verification environment  
- brief display and automatic clearing  
- no replay  
- no transferable proof  

Limitation:
- coercion is not eliminated, only made more costly and less scalable  

---

### 4.7 Supply Chain Attacker
Capabilities:
- compromise hardware or firmware before deployment  

Mitigations:
- certification processes  
- measured boot and attestation  

Residual risk:
- cannot be fully eliminated  

---

### 4.8 Denial of Verification Attacker
Capabilities:
- disrupt access to verification infrastructure  
- prevent voters from verifying ballots  

Mitigations:
- redundancy of reveal units  
- multiple verification locations  

Residual risk:
- local or temporary availability disruption  

---

## 5. Security Guarantees

The system is designed to provide:

### ✔ Public Verifiability
Anyone can verify ballot validity and tally correctness without trusting backend systems.

---

### ✔ Ballot Privacy
No identity-to-vote linkage is exposed or derivable from the system.

---

### ✔ Non-Transferable Verification
Voters can verify their ballot but cannot produce durable or replayable proof of their vote.

---

### ✔ Single-Use Verification
Each ballot is designed to be verifiable at most once, enforced through:
- device-bound verification rights  
- coordinated consumption registry  

---

### ✔ No Single Point of Trust
- distributed key custody  
- stateless reveal infrastructure  
- redundant components  

---

### ✔ Bounded Verification Window
Verification is limited to a maximum of one year after election closure.

---

## 6. Non-Goals / Explicit Limitations

The system does not guarantee:

### ❌ Protection against real-time coercion
A voter may still be observed or pressured during verification.

---

### ❌ Protection against fully compromised devices
A device compromised before voting may affect integrity or privacy.

---

### ❌ Elimination of all side-channel leakage
Timing, physical observation, or environmental signals may exist.

---

### ❌ Trustless physical infrastructure
The system depends on proper operation of verification sites and procedures.

---

### ❌ Guarantee of successful verification
A voter may fail to verify their ballot due to:
- device loss  
- missed verification window  
- operational disruption  

---

## 7. Residual Risks

Remaining risks include:

- timing correlation at verification facilities  
- infrastructure misconfiguration  
- legal or governance failure  
- coordinated insider collusion above threshold  
- physical compromise of verification environments  
- temporary inconsistencies in the consumption registry during network partition or partial failure  

---

## 8. Logging and Observability Trade-off

The system enforces minimal logging to preserve privacy.

Implication:
- reduces risk of correlation attacks  
- limits forensic and debugging capabilities  

---

## 9. Security Posture Summary

The system prioritizes:

- public verifiability without backend trust  
- strong ballot privacy  
- constrained, non-transferable verification  
- minimal data exposure  
- distributed trust and stateless critical components  

It is designed to:

> significantly reduce large-scale coercion, vote buying, and systemic manipulation  

while maintaining:

> transparent and independently verifiable election results  

---

## 10. Relationship to Specification

This threat model is aligned with:

- Full Specification v1.2  
- Verification-right lifecycle  
- Terminal trust model  
- Consumption registry design  
- Archival and lifecycle policies  

---

## Summary

The system balances:

- verifiability  
- privacy  
- coercion resistance  

while acknowledging:

- operational dependencies  
- physical-world constraints  
- residual risks inherent to any voting system  
