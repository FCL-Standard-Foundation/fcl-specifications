# FCL-RSL-BINDING-0.1

RSL governs whether a machine may ingest. This governs whether a person may build. Here is the seam.

| **Field** | **Value** |
| --- | --- |
| DOCUMENT | FCL-RSL-BINDING-0.1 |
| STATUS | Draft — published for comment |
| COMPANION TO | FCL-CORE-0.1.2 |
| REQUIRES | No change to RSL. Extension is namespace-safe. |
| SOURCE | Markdown source |

## Contents

1. Purpose
2. The gap, stated plainly
3. What RSL 1.0 specifies
4. What the Human Consent Standard adds
5. Concept correspondence
6. Design constraints
7. The binding
8. Worked examples
9. Where the models genuinely diverge
10. What is not proposed
11. The one request
12. Open questions for reviewers
13. Provenance of this document

## 1. Purpose

RSL 1.0 defines machine-readable licensing terms for automated access to digital assets. RSL Media’s Human Consent Standard extends the model to identity, works, characters, and marks, with a three-state permission model: allowed, allowed with terms, prohibited.

The middle state is declared but its terms are not specified. This document proposes a binding by which those terms may be expressed, using a vocabulary purpose-built for the transaction they describe.

Nothing in this document requires a change to RSL. §7 specifies a binding that works today under XML namespace extension. §11 contains a single optional request, which would improve discoverability but is not required for the binding to function.

This document is written to be checked. Where it characterizes RSL, it cites the normative source. Corrections are welcome and will be published.

## 2. The gap, stated plainly

RSL answers: may an automated client access, index, train on, or infer from this asset, and on what terms?

It does not answer, and does not attempt to answer: may a person create a new work using this material, and what happens to the revenue when they do?

These are different transactions with different counterparties, different units, and different outputs. The first ends with ingestion. The second produces a new work that itself requires standing, attribution, provenance, and often a revenue split among three or more parties.

The Human Consent Standard’s allowed with terms is the point where the second question surfaces inside the RSL model. A rights holder who permits derivative creation “with terms” needs a vocabulary for those terms. FCL-CORE is that vocabulary.

## 3. What RSL 1.0 specifies

Summarized for shared reference. Normative source: rslstandard.org.

An RSL document is XML conforming to XML 1.0, rooted at `rsl` with the namespace https://rslstandard.org/rsl, available as a standalone .xml file, an RSS module using the rsl: prefix, or embedded in HTML via a script element with type `application/rsl+xml`.

A `<content url>` element identifies the governed asset; url must identify an asset governed by the same origin that publishes the document. Each `<content>` carries one or more `<license>` elements containing `<permits>`, `<prohibits>`, `<payment>`, and optionally `<legal>`, `<reporting>`, `<schema>`, and `<copyright>`.

Usage values distinguish ingestion modes independently: ai-train, ai-input, ai-index, ai-use, ai-summarize, search, ai-all, all. Payment types include free, attribution, subscription, purchase, training, crawl, inference, royalty, and use, with `<amount>`, `<standard>`, and `<custom>` children.

Discovery extends the Robots Exclusion Protocol with a License: directive, and is also available via HTTP Link headers, RSS, and Schema.org metadata.

Two protocols support enforcement. The Open License Protocol (OLP) issues license tokens over OAuth 2.0 from a license server designated by the server attribute. The Crawler Authorization Protocol (CAP) validates those tokens at request time, returning 401 or 402 where no valid token is presented and 403 where a valid token does not cover the requested use.

Two properties of the model matter for this binding:

Prohibition narrows permission. Where `<permits>` and `<prohibits>` overlap, prohibition controls. Absence is not permission. A client that cannot obtain a valid RSL document for an asset must treat that asset as unlicensed.

Both principles are preserved unchanged by this binding.

## 4. What the Human Consent Standard adds

The Human Consent Standard extends the model from assets at addresses to four rights areas — Identity, Work, Characters, Marks — applying to the underlying subject wherever it appears, rather than to a resource at a URL. Permission is expressed as allowed, allowed with terms, or prohibited, resolvable through a Human Consent ID.

That shift from address-scoped to subject-scoped is the same move FCL-CORE makes, and it is what makes this binding possible at all. An FCL profile governs a world, a catalog, or a person — none of which has a single canonical URL.

## 5. Concept correspondence

| RSL / HCS | FCL-CORE | RELATIONSHIP |
| --- | --- | --- |
| `<content url>` | subject_id (§3.1) | RSL is origin-scoped; FCL is subject-scoped. See §9.1 |
| Rights area: Identity | HPL (§6) | HPL supplies eras, axes, compensation floor, estate succession, revocation notice |
| Rights area: Work | CRL (§4) | CRL supplies use categories, quantitative limits, revenue and quotation floors |
| Rights area: Characters | FCL (§5) | FCL supplies tiers, canon status, divergent mode, per-medium configuration |
| Rights area: Marks | FCL Layer 4 asset | Reserved asset class within a profile, not a separate instrument |
| allowed | Commons tier below threshold (§5.1) | Use permitted without registration |
| allowed with terms | The entire FCL profile | See §7 |
| prohibited | Canon tier, or prohibited-uses layer (§3.3) | Two distinct FCL states collapse to one RSL state. See §9.2 |
| `<prohibits>` narrows `<permits>` | Prohibited-uses layer overrides every grant (§3.3) | Identical precedence principle |
| Absence ⇒ unlicensed | Silence on a layer ⇒ non-conforming profile (§5.2) | Both reject permissive defaults |
| OLP license token | Standing Token (§8.5) | Same pattern, different claim set. See §7.5 |
| `<payment type="royalty">` | revenue_share, per_unit (§10.6) | Partial correspondence. See §9.3 |
| ai-train prohibition | Layer 8 ai_training | Direct correspondence, independent settings |
| (no equivalent) | Layers 1–3, 5–7, 9 | The derivative-creation vocabulary |
| (no equivalent) | Certification mark, tiers, canon, verticals | See §9 |

## 6. Design constraints

**The binding is constrained as follows:**

No change to RSL is required. The binding must function under RSL 1.0 as published. No change to RSL semantics. No existing element may be given a new meaning. Namespace-safe. Extension elements carry their own namespace; an RSL processor unaware of FCL must be able to ignore them without error. Precedence preserved. RSL prohibitions continue to control. An FCL profile may never widen what RSL prohibits. Round-trippable. A processor must be able to move from an RSL document to the governing FCL profile and back without ambiguity.

## 7. The binding

### 7.1 Extension element

An FCL profile is referenced by a namespaced extension element within `<license>`:

```xml
<rsl xmlns="https://rslstandard.org/rsl" xmlns:fcl="https://fclstandard.org/ns/1.0">
  <content url="/">
    <license>
      <prohibits type="usage">ai-train</prohibits>
      <permits type="usage">search</permits>
      <fcl:profile instrument="fcl" subject="example-world" version="2.0" href="https://registry.fclstandard.org/entry/example-world"/>
    </license>
  </content>
</rsl>
```

The fcl:profile element asserts: derivative creation using this subject is governed by the referenced FCL profile. It makes no assertion about ingestion, which remains governed entirely by `<permits>` and `<prohibits>`.

**Attributes:**

| ATTRIBUTE | REQ. | NOTES |
| --- | --- | --- |
| instrument | MUST | crl \| fcl \| hpl |
| subject | MUST | The FCL subject_id |
| version | SHOULD | Current profile version; absent means resolve current |
| href | MUST | Resolvable registry entry |

An RSL processor that does not recognize the namespace ignores the element and behaves exactly as it does today. This is the whole point of constraint 6.3.

### 7.2 Binding to allowed with terms

Where a Human Consent declaration sets a rights area to allowed with terms, those terms MAY be expressed as an FCL profile:

| RIGHTS AREA | INSTRUMENT | PROFILE SUPPLIES |
| --- | --- | --- |
| Identity | hpl | Era windows, voice/face/motion axes, permitted and prohibited categories, synthetic disclosure, performer share as raisable floor, estate succession, revocation notice |
| Work | crl | Use categories, footage and excerpt limits, quotation and revenue floors, per-category rates |
| Characters | fcl | Tier map, ten layers, canon status, divergent mode, per-medium configurations |
| Marks | fcl (Layer 4) | Asset reservation, logo treatment, mark discipline |

### 7.3 Resolution order

A processor evaluating a request that implicates both ingestion and derivative creation MUST:

Evaluate `<prohibits>` and `<permits>` for the ingestion question. RSL controls entirely. If the request is derivative creation by a person, resolve fcl:profile and evaluate under FCL-CORE §9.3. Enforce the union of both prohibition sets. A permission in either document is narrowed by a prohibition in the other. Where the FCL profile’s likeness layer names another administering party, resolve that layer against the performer’s own entry (FCL-CORE §2.2), regardless of what either the RSL document or the world owner’s profile asserts.

Step 3 is the safety property. Neither document can be used to widen the other.

### 7.4 Reverse direction: FCL to RSL

A conforming FCL registry SHOULD emit an RSL document for any subject with a web-addressable origin, derived as follows:

| FCL STATE | EMITTED RSL |
| --- | --- |
| Layer 8 ai_training: forbidden | `<prohibits type="usage">ai-train</prohibits>` |
| Layer 8 ai_training: permitted | `<permits type="usage">ai-train</permits>` with `<payment>` per profile |
| Commons tier open, no threshold | `<permits type="usage">search</permits>` |
| Prohibited-uses layer (§3.3) | `<legal>` disclosure; not expressible in `<prohibits>` — see §9.4 |
| Any profile | `<fcl:profile>` self-reference |

This is a lossy projection and is labeled as such. It carries the ingestion settings faithfully and the derivative-creation settings by reference only.

### 7.5 Token interoperability

FCL-CORE §8.5 specifies a Standing Token asserting a creator’s registration standing — profile version, tier, medium, AI Usage Profile, likeness authority, departure status — deliberately mirroring OLP’s issuance pattern.

Where an implementation serves both, a single license server SHOULD issue both token types from a common endpoint, distinguished by requested scope. A crawler requests an OLP token; a registered creator requests a Standing Token. The authentication, issuance, and validation machinery is shared.

Two constraints differ and are non-negotiable on the FCL side:

A Standing Token MUST NOT assert the prohibited-uses layer. The verifier enforces that itself, absolutely. A Standing Token MUST NOT carry terms, only pointers by which terms are retrieved live.

## 8. Worked examples

### 8.1 A world owner publishing both

A studio prohibits AI training, permits search, and opens derivative creation under a tiered profile.

```xml
<rsl xmlns="https://rslstandard.org/rsl" xmlns:fcl="https://fclstandard.org/ns/1.0">
  <content url="/" server="https://api.example-studio.com">
    <license>
      <permits type="usage">search</permits>
      <prohibits type="usage">ai-train ai-input</prohibits>
      <fcl:profile instrument="fcl" subject="example-world" version="2.0" href="https://registry.fclstandard.org/entry/example-world"/>
    </license>
  </content>
</rsl>
```

A crawler reads this exactly as it reads any RSL document today. A creator’s publishing platform resolves fcl:profile and learns that background lore is Commons, that four principal characters are Controlled at a stated split, that divergent works must be labeled, and that the likeness layer is administered elsewhere.

### 8.2 Identity: allowed with terms resolving to an HPL

A performer’s consent declaration sets Identity to allowed with terms. The terms:

```xml
<fcl:profile instrument="hpl" subject="performer-identifier" version="1.3" href="https://registry.fclstandard.org/entry/performer-identifier"/>
```

Resolving yields: voice synthesis metered per project for one era; face synthesis forbidden in every era; motion not offered; a raisable compensation floor; synthetic disclosure required without exception; resurrection scenarios closed by default and closed absolutely by the recorded administrator; revocation prospective on ninety days’ notice.

None of that is expressible in a three-state model. All of it is what “with terms” means to the person whose face it is.

### 8.3 Characters: partial permission

A publisher permits derivative creation for background characters and reserves principals:

```xml
<fcl:profile instrument="fcl" subject="example-world" version="1.0" href="https://registry.fclstandard.org/entry/example-world"/>
```

The profile’s tier map does the work the flat state cannot: some characters are Commons, some Controlled, some Canon. A single allowed with terms at the rights-area level resolves to per-element settings underneath.

## 9. Where the models genuinely diverge

Stated because a binding that hides its seams is not a binding.

### 9.1 Scope model

RSL’s `<content url>` is origin-scoped: the url must identify an asset governed by the same origin publishing the document. FCL subjects frequently have no single origin — a fictional world appears across films, books, merchandise, and conventions; a person’s identity has no URL at all. The Human Consent Standard’s move to subject-scoping narrows this gap but does not close it for base RSL. Where a subject has no web-addressable origin, the binding operates through the registry alone and no RSL document is emitted.

### 9.2 State collapse

FCL distinguishes Canon tier (reserved, not licensed under this profile, potentially licensable by separate negotiation) from prohibited uses (never licensable at any price, overriding every grant). Both project to prohibited. The projection is lossy in a direction that matters, and a processor relying only on the RSL projection will not distinguish “ask us” from “never.”

### 9.3 Payment model

free, attribution, and royalty correspond. crawl and inference have no FCL equivalent — they price ingestion events. revenue_share, per_unit, and threshold_gated have no RSL equivalent, because they price outcomes of human creation: a share of what a fan film earned, a per-unit royalty on a sewn patch, a threshold below which nothing is owed. This asymmetry is the gap this document exists to describe. Neither vocabulary is deficient; they price different things.

### 9.4 Prohibited uses

FCL’s prohibited-uses layer (hate_content, sexual_content, political_advertising, deceptive_branding, and others) has no RSL expression, because it constrains what a person may make rather than what a machine may ingest. It projects only into `<legal>` as disclosure, which is weaker than its normative force under FCL-CORE §3.3.

### 9.5 Enforcement

RSL delegates enforcement to CDN partners and to law. FCL adds a certification mark — pending applications, USPTO, filed 6 April 2026 — creating a trademark hook against misuse of the mark itself. This reaches misuse of the mark. It does not reach a party who never uses the mark and never enters either system. Neither standard solves the non-participant.

## 10. What is not proposed

**To be unambiguous:**

No change to RSL’s ingestion vocabulary. ai-train, ai-input, ai-index, search and their semantics are untouched. No competing registry for content ingestion, crawler authorization, or publisher-to-AI-company licensing. That ground is covered. No competing collective licensing body. FCL-CORE §9.4 provides that its custodian sets no operator’s price and takes no share of any operator’s fee. The two funding models are different by design and not in competition. No claim on the Human Consent Registry. The binding treats a Consent ID as authoritative for the consent declaration and supplies vocabulary beneath it. No request for endorsement. This document is published because it seemed more useful published than withheld.

## 11. The one request

Optional, and the binding functions without it.

A normative reference in the Human Consent Standard, of roughly this shape:

Where a rights area is set to allowed with terms, the terms MAY be expressed by reference to an external terms vocabulary. FCL-CORE is one such vocabulary.

The benefit is discoverability: an implementer encountering allowed with terms today has nowhere to look. The reference gives them somewhere. It commits RSL to nothing, since “MAY” and “one such” leave the field open to any other vocabulary that emerges.

If the RSL TSC would prefer to specify its own terms vocabulary rather than reference an external one, this document should be read as prior art and a set of solved problems — particularly the ten-layer independence rule, the vertical-configuration exclusivity rule, and the immutable-version reliance envelope, each of which was arrived at by trying simpler designs and watching them fail. Those are offered freely under CC BY whether or not any binding is adopted.

## 12. Open questions for reviewers

Is `<license>` the right parent for fcl:profile, or does it belong on `<content>`? The former binds terms to a license; the latter to an asset. FCL’s subject-scoping may argue for `<content>`. Should the extension namespace be versioned in the URI, as written, or carry a version attribute? §9.2’s state collapse — is there an existing RSL idiom distinguishing “reserved, negotiable” from “prohibited, absolute”? If so, this document should use it rather than note the loss. Does §7.3’s union-of-prohibitions rule create any conflict with CAP’s 403 semantics? Is the shared-endpoint proposal in §7.5 workable against OLP’s OAuth scope model, or does it require a separate authorization server? Where a subject has no web-addressable origin (§9.1), is there interest in a discovery mechanism at all, or is the registry-only path sufficient?

Question 3 is the one the editor would most like an answer to.

## 13. Provenance of this document

RSL characterizations are drawn from rslstandard.org (specification, file format, robots.txt, crawler authorization, standard licenses, Schema.org, and AI preferences guides), rslcollective.org, and rslmedia.org, as available at the date above. Errors are the editor’s and corrections are welcome at the comment address.

The FCL framework is described at length in a forthcoming book; that book is not required reading for this document and is not offered as an argument. FCL-CORE-0.1.2 is the artifact.

Five certification mark applications — FCL, FCL CANON, FCL CONTROLLED, FCL COMMONS, and HPL — were filed with the USPTO in April 2026 by the FCL Standard Foundation, Serial Nos. 99732430, 99732478, 99751765, 99751799, and 99748332. All are pending examination. Applications are not registrations.

**Except where otherwise noted, FCL-RSL-BINDING-0.1 is licensed under the Creative Commons Attribution 4.0 International License (CC BY 4.0).**

Copyright © 2026 FCL Standard Foundation.

The FCL certification marks are not licensed under CC BY 4.0 and are governed separately.
