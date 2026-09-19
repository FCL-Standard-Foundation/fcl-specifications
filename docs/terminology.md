# Terminology

Non-normative glossary derived from **FCL-CORE-0.1.2** (§1.5 and related sections). If this page conflicts with the specification, **the specification controls**.

## Instruments

| Term | Definition (from FCL-CORE) |
|------|----------------------------|
| **CRL** | **Catalog Reaction License** — instrument whose subject is a fixed catalog of completed works; grants permission to react to, comment on, review, criticize, excerpt, compare, or remix within stated limits (§2.1). |
| **FCL** | **Franchise Creative License** — instrument whose subject is a living fictional world; grants permission to create new works using covered elements of that world (§2.1). |
| **HPL** | **Human Performance License** — instrument whose subject is a natural person's identity and performance; grants permission to use or synthesize face, voice, likeness, or motion within stated boundaries (§2.1). |
| **Instrument** | One of the three license types: CRL, FCL, or HPL (§1.5). |

## Core constructs

| Term | Definition (from FCL-CORE §1.5 unless noted) |
|------|-----------------------------------------------|
| **Permission Profile** | A complete, versioned statement of terms published by a rights holder, performer, or authorized administrator. |
| **Registry Entry** | The authoritative, resolvable record hosting a profile, its current version, prior versions, and associated authority information. |
| **Authority Claim** | The registry record describing the identity of the profile publisher, the basis on which that party claims authority to publish permissions, and the asserted scope of that authority. |
| **Reliance Envelope** | The profile version and associated terms against which a work's authorized status is evaluated. |
| **Reliance Receipt** | An optional signed registry record establishing which profile version was effective at a stated time for an otherwise unregistered Commons use (§8.6). |
| **Standing Token** | A time-limited signed assertion allowing a verifier to establish specified facts about a registered work without a registry round trip for every transaction (§8.5). |
| **Certification Mark** | The standard's trustmark indicating that a use resolves to a verified registry entry and an identifiable governing permission state. Distinct from a rights holder's trademarks, logos, and trade dress. |
| **Verifier** | A platform, marketplace, service, or node that resolves FCL-family permissions and evaluates conformance at publication, distribution, registration, or sale. |
| **AI Usage Profile** | A work's declaration of how generative AI participated in its creation (§7). |
| **Vertical Configuration** | Also **row** — a complete permission configuration scoped to a named medium (§5.3). |

## Tiers (FCL element classification)

| Term | Definition (from FCL-CORE §5.1 / §1.5) |
|------|----------------------------------------|
| **Commons** | Elements placed in the Commons lane MAY be used without registration where the governing configuration permits the proposed use. Commons status does not mean unrestricted use. |
| **Controlled** | Elements placed in the Controlled lane require registration or another stated control mechanism whenever use is permitted. Controlled configurations MAY additionally impose reporting, payment, approval, or other stated conditions. |
| **Canon** | Elements placed in the Canon lane are not available under standing FCL permission. |

**Tier** — one of three fixed element classifications: Commons, Controlled, or Canon (§1.5).

## Related terms (FCL-CORE §1.5)

| Term | Definition |
|------|------------|
| **Layer** (also **dial**) | One of ten independent permission dimensions in an FCL profile (§5.2). |

For normative detail, read [FCL-CORE-0.1.2](../specs/core/FCL-CORE-0.1.2.md).
