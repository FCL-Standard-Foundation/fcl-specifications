# Architecture overview

**Non-normative.** This page orients readers to the FCL family of drafts. It does not add requirements. Normative rules live in the specification documents under [`specs/`](../specs/).

## Three instruments, one model

FCL-CORE defines three related **license instruments** that share a common profile envelope, reliance/versioning semantics, prohibited-use handling, attribution/mark discipline, dispute posture, revocation principles, and serialization concepts:

1. **CRL — Catalog Reaction License** — standing permission to react to a fixed catalog of completed works within stated limits.
2. **FCL — Franchise Creative License** — standing permission to create new works using covered elements of a living fictional world (tiers, layers, vertical configurations).
3. **HPL — Human Performance License** — standing permission regarding a natural person’s identity and performance within stated boundaries.

The instruments are independent: permission under one MUST NOT be read as permission under another. See FCL-CORE §2.1.

## Profiles and registries

A **permission profile** is a complete, versioned statement of terms. An effective profile resolves through a **registry entry** and an **Authority Claim**. Registries host current and prior versions; verifiers resolve and evaluate conformance.

Profile changes are intended to apply **prospectively**; historical reliance is evaluated within a **reliance envelope**. Optional **Reliance Receipts** and **Standing Tokens** support evidence and efficient verification as specified in FCL-CORE.

## Human-, legal-, and machine-readable forms

Profiles may exist as legal code, human-readable summary, and machine-readable serialization. They must remain semantically consistent; where they diverge, the legal instrument controls unless applicable law provides otherwise (FCL-CORE §2.3).

## AI usage vs AI training

The **AI Usage Profile** declares how generative AI participated in creating a work. It is distinct from Layer 8 / training-permission statements and from machine-ingestion protocols. A separate draft, **FCL-RSL-BINDING**, addresses binding to RSL where applicable.

## Certification separation

Open specification text (CC BY 4.0) is separate from **certification marks** and program rules. Implementing or publishing profiles does not authorize mark use. See:

- [FCL-REGISTRY-MARK-0.1](../specs/registry-mark/FCL-REGISTRY-MARK-0.1.md)
- [FCL-CERTIFICATION-RULES-0.1](../specs/certification/FCL-CERTIFICATION-RULES-0.1.md)
- [TRADEMARKS.md](../TRADEMARKS.md)

## Independently lawful use

Nothing in the framework converts independently lawful conduct (for example fair use) into licensed-only conduct. See FCL-CORE §1.6.

## Where to read next

| Topic | Document |
|-------|----------|
| Data model, instruments, reliance, conformance | [FCL-CORE-0.1.2](../specs/core/FCL-CORE-0.1.2.md) |
| RSL binding | [FCL-RSL-BINDING-0.1](../specs/rsl-binding/FCL-RSL-BINDING-0.1.md) |
| Registry / mark | [FCL-REGISTRY-MARK-0.1](../specs/registry-mark/FCL-REGISTRY-MARK-0.1.md) |
| Certification rules | [FCL-CERTIFICATION-RULES-0.1](../specs/certification/FCL-CERTIFICATION-RULES-0.1.md) |
| Terms | [terminology.md](terminology.md) |
| Draft status | [document-status.md](document-status.md) |
