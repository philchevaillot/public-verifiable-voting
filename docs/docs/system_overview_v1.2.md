# System Overview — v1.2

Public Verifiable Voting System  
Architecture, Verification Model, and Coercion-Resistance Design

---

## Project
**Public Verifiable Voting System**  
Author: Philippe Chevaillot

## Status
This document defines the current architecture, verification model, and system design following the v1.2 updates.

---

## Current Demo State

The browser-based prototype demonstrates:

- client-side ballot encryption using RSA-OAEP  
- public ledger publication of encrypted ballots  
- SHA-256 integrity hashing  
- one ballot per device/session (demo constraint)  
- election-wide verification window (post-close only)  
- single-use ballot verification  
- public tally after election closure  

### Demo limitations

- the RSA private key is intentionally stored in `localStorage`  
- ballot reveal is client-side (for transparency purposes only)  
- verification consumption is stored locally  
- this prototype is designed for clarity and discussion, not production security  

---

## Core System Direction

The project explores a **publicly verifiable, trust-minimized voting architecture** with:

- encrypted ballots  
- public auditability  
- distributed tallying / decryption  
- constrained voter verification  
- strict separation between identity, voting, and verification layers  

---

## Key Concept

The system introduces:

> a **global post-election verification window** combined with a **single-use private verification right**

This design aims to balance:

- auditability  
- ballot secrecy  
- coercion resistance  
- non-transferability of proof  

---

## Physical vs Digital Voting

The system separates voting into two independent channels.

### Physical voting (unchanged)

- voter attends polling station  
- enters voting booth  
- places ballot in envelope  
- presents identity  
- name is crossed from voter list  
- envelope inserted into transparent ballot box  

### Digital voting

- official in-person enrollment  
- credential generation  
- encrypted ballot submission  
- publication to public ledger  
- digital tally and verification logic  

### Shared rule

> A voter may use only one channel.

---

## Channel Commitment Rule

The physical voting right is disabled:

> **when the voter initiates the official digital enrollment process**

This commitment is:

- immediate  
- official  
- irreversible  

Once digital enrollment begins:

- physical voting is permanently blocked  
- the voter must complete the digital path  
- no fallback to physical voting is allowed  

---

## Verification Architecture Direction

Verification is not designed as an unrestricted remote action.

The system evolves toward:

> **controlled, in-person ballot verification**

### Objectives

- limit transferable proof of vote  
- preserve voter privacy  
- maintain individual audit capability  

---

## Controlled Verification Model

After election closure, verification is performed under controlled conditions:

- access through official verification sites or events  
- fixed or mobile infrastructure  
- single-person access to a private booth  
- no bags, accessories, or recording devices  
- secure environment similar to controlled facilities  

### Verification process

- voter device pairs with a certified terminal  
- ballot is displayed only on the terminal  
- plaintext ballot does not return to the phone  
- ballots are revealed one at a time  
- verification right is consumed immediately upon session start  

---

## Pairing Model

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

## Verification Token Model

The system uses:

- one verification right per ballot  
- storage within the voter application  
- controlled re-provisioning mechanism  
- possession-based authorization  
- validation without identity exposure  

---

## Coercion Resistance Model

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
- no plaintext return to the voter’s device  
- immediate consumption of verification rights  

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

## Governance Model

The verification infrastructure is operated by:

> **mixed / audited operators**

This includes:

- public authorities  
- certified independent entities  
- controlled procedures  
- auditability across operators  

---

## Security Position

### Strengths

- public auditability  
- encrypted ballots  
- constrained verification  
- single-use reveal rights  
- non-transferable proof objective  
- strict channel separation  
- privacy boundary at reveal layer  

### Main unresolved challenge

> privacy-preserving enforcement of one-person-one-vote across channels  

This requires a shared eligibility and vote-consumption authority, even if voting and verification remain identity-minimized.

---

## Positioning

This project is no longer only a cryptographic prototype.

It represents:

> an open system design exploring publicly verifiable elections with constrained, non-transferable voter verification

---

## v1.2 Summary

### Demo updates

- one ballot per device/session  
- global post-election verification window  
- single-use verification  

### Architecture updates

- clarified physical vs digital separation  
- defined irreversible digital enrollment  
- introduced controlled in-person verification model  
- formalized possession-based verification  
- added coercion-resistance framework  

---

## Notes

This document reflects the current conceptual and implementation state of the project.

It serves as a reference for:

- README updates  
- diagrams  
- submission materials  
- future development  
