# Public Verifiable Voting System

## Overview

This project proposes a publicly verifiable voting system designed to eliminate the need to trust centralized counting authorities while preserving strict vote secrecy.

The system allows any citizen to verify that:
- their vote was recorded
- their vote was counted
- their vote was counted correctly

without ever being able to prove their vote to a third party.

---

## Problem

Modern voting systems face three major challenges:

- Declining public trust in vote counting
- High operational cost of physical voting
- Low participation due to complexity and disengagement

Existing digital solutions often introduce new risks:
- central points of failure
- lack of transparency
- potential coercion or vote selling

---

## Solution

This system introduces a model based on:

- Public ledger for universal verification
- Homomorphic encryption for secure tallying
- Zero-knowledge proofs to ensure ballot validity
- Temporary, unlinkable voter identities
- One-time private vote verification

Key properties:

- No single point of trust
- Full public auditability
- Strong privacy guarantees
- No transferable proof of vote

---

## Key Principles

- One vote → one ballot
- Vote finality only upon public block publication
- First valid published ballot wins
- No intermediate confirmation states
- No backend trust required

---

## Verification Model

Each voter can verify (after results publication):

- their ballot was included
- it contributed to the correct outcome

This is achieved without revealing their identity or enabling coercion.

---

## Current Status

This project is currently at the **architecture and specification stage (V1.1)**.

The goal is to:
- refine the model
- validate assumptions
- explore implementation paths

---

## Notes

This is an open concept intended for discussion, review, and improvement.

Feedback is welcome.