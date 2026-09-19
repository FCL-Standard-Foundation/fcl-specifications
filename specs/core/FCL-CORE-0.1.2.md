FCL-CORE-0.1.2

**A data model for advance, conditional permission to create with rights controlled by others.**

| **Field** | **Value**                                                         |
|-----------|-------------------------------------------------------------------|
| DOCUMENT  | FCL-CORE-0.1.2                                                    |
| STATUS    | Draft — published for comment · NO KNOWN IMPLEMENTATIONS          |
| LICENCE   | CC BY 4.0 · royalty-free to implement · no patent claims asserted |
| SOURCE    | Markdown source                                                   |
| COMMENT   | <info@fclstandard.org> — see §14                                  |

Contents

- Status of This Document

  1.  Introduction

  2.  Architecture

  3.  Common elements

  4.  CRL — Catalog Reaction License

  5.  FCL — Franchise Creative License

  6.  HPL — Human Performance License

  7.  The AI Usage Axis

  8.  Serialization

  9.  Conformance

  10. Controlled vocabularies

  11. Security and privacy considerations

  12. Legal effect (non-normative)

  13. Open issues

  14. Comments

- Appendix A — Change log

Status of This Document

This is a draft. It has not been reviewed or adopted by a standards body, has no implementations known to the editor, and will change in response to comment. Section 13 lists known open issues; that list is not exhaustive.

This document specifies a data model and a set of conformance requirements. It does not itself grant rights, provide legal advice, or create enforceable obligations.

A permission profile expressed under this specification derives its legal effect from the underlying license instrument a rights holder or other authorized party executes and publishes, from applicable law, and — where a certification mark is used — from the separately published rules governing that mark.

See §12.

1\. Introduction

1.1 Scope

This specification defines a machine-readable format for expressing advance, conditional permission to create, publish, distribute, or monetize new work using rights controlled by another party.

Its subject is a recurring transaction:

A person wishes to create something using material, identity, or intellectual property controlled by someone else — a fictional world, character, catalog, performance, likeness, or completed work.

Today that transaction has no broadly shared vocabulary.

It may be negotiated bilaterally at costs that exceed the value of the proposed project. It may proceed without permission. It may rely on rights independently supplied by law. Or it may not happen at all.

This specification defines:

- three related license instruments sharing one data model;

- a permission-profile format;

- registry and versioning requirements;

- a reliance model;

- serialization requirements;

- machine-readable discovery mechanisms; and

- conformance requirements for profiles, registries, and verifiers.

The purpose is not to create new rights.

The purpose is to make permission that already can be granted easier to express, discover, interpret, and rely upon.

1.2 What is out of scope

This specification does not define the mechanics of machine ingestion.

It does not specify how an automated system crawls, indexes, obtains model access to, trains on, or performs inference from an asset. Those transactions may be governed by adjacent machine-facing licensing standards.

An FCL profile MAY nevertheless express or reference a rights holder's permission state regarding AI training under Layer 8. That statement describes the rights holder's position. It is not, by itself, a machine-access protocol or authorization credential.

Also out of scope:

- payment rails and settlement networks;

- currency handling;

- tax treatment;

- the visual design of certification marks;

- placement rules beyond what this specification expressly requires;

- the internal procedure of the custodian body;

- adjudication of copyright ownership;

- adjudication of factual disputes; and

- drafting the complete binding legal text of an underlying license instrument.

This specification defines questions the legal instrument must answer. It does not substitute for the legal instrument.

1.3 Relationship to adjacent standards (non-normative)

Several standards address adjacent problems. This specification is intended to complement rather than replace them.

Really Simple Licensing

RSL addresses machine-facing ingestion and licensing signals: whether an automated client may crawl, index, train on, or otherwise ingest an asset, and on what terms.

FCL addresses what a creator may make with rights associated with that material.

The distinction is intentional.

An FCL profile may state:

*AI training prohibited.*

That statement records the rights holder's permission position.

Where machine access is controlled through RSL or another ingestion protocol, the machine must still resolve and comply with that protocol. The FCL statement is not itself authorization to crawl or retrieve source assets.

Likewise, machine authorization under RSL does not imply permission to create derivative or franchise-based works under FCL.

A separate binding document specifies the mapping between RSL and this specification.

Where both apply, neither specification may be interpreted to widen permission the other restricts.

The following non-normative mapping applies to RSL's four declared rights areas:

| **RSL rights area**                                   | **Nearest FCL-family construct** | **Relationship**                                                                                                     |
|-------------------------------------------------------|----------------------------------|----------------------------------------------------------------------------------------------------------------------|
| Identity — name, image, likeness, voice, movement     | HPL (§6)                         | HPL expresses identity and synthesis permissions, temporal windows, compensation terms, succession, and restrictions |
| Work — songs, films, books, art                       | CRL (§4)                         | CRL expresses human reuse, reaction, commentary, excerpt, remix, and monetization conditions                         |
| Characters — fictional characters, depictions, traits | FCL (§5)                         | FCL expresses tiering, canon status, medium-specific permissions, and commercial conditions                          |
| Marks — logos, trademarks, trade dress                | FCL Layer 4 — Asset              | Governed as a protected asset class rather than a separate instrument                                                |

C2PA

C2PA provides content credentials and provenance manifests.

This specification does not define a competing provenance format.

Where a conforming implementation carries provenance, it SHOULD use an established provenance standard such as C2PA and SHOULD NOT invent a parallel format without a demonstrated interoperability need.

Creative Commons

Creative Commons licenses provide standing permission for reuse of a work under standardized terms.

The FCL family addresses a different problem: permission to create, perform, react to, synthesize, or commercially exploit new work involving rights that the licensor continues to control.

The two approaches may coexist.

1.4 Requirements language

The key words MUST, MUST NOT, REQUIRED, SHALL, SHALL NOT, SHOULD, SHOULD NOT, RECOMMENDED, MAY, and OPTIONAL are to be interpreted as described in RFC 2119 and RFC 8174 when, and only when, they appear in all capitals.

1.5 Terminology

**Permission Profile** — a complete, versioned statement of terms published by a rights holder, performer, or authorized administrator.

**Registry Entry** — the authoritative, resolvable record hosting a profile, its current version, prior versions, and associated authority information.

**Instrument** — one of the three license types: CRL, FCL, or HPL.

**Layer**, also **dial** — one of ten independent permission dimensions in an FCL profile (§5.2).

**Tier** — one of three fixed element classifications: Commons, Controlled, or Canon (§5.1).

**Vertical Configuration**, also **row** — a complete permission configuration scoped to a named medium (§5.3).

**AI Usage Profile** — a work's declaration of how generative AI participated in its creation (§7).

**Reliance Envelope** — the profile version and associated terms against which a work's authorized status is evaluated.

**Reliance Receipt** — an optional signed registry record establishing which profile version was effective at a stated time for an otherwise unregistered Commons use (§8.6).

**Authority Claim** — the registry record describing the identity of the profile publisher, the basis on which that party claims authority to publish permissions, and the asserted scope of that authority.

**Certification Mark** — the standard's trustmark indicating that a use resolves to a verified registry entry and an identifiable governing permission state. The certification mark is distinct from a rights holder's trademarks, logos, and trade dress.

**Standing Token** — a time-limited signed assertion allowing a verifier to establish specified facts about a registered work without a registry round trip for every transaction (§8.5).

**Verifier** — a platform, marketplace, service, or node that resolves FCL-family permissions and evaluates conformance at publication, distribution, registration, or sale.

1.6 Independently lawful use

Nothing in this specification converts conduct that is independently lawful into licensed conduct.

Nothing in an FCL, CRL, or HPL profile may be interpreted as narrowing fair use, fair dealing, quotation rights, statutory exceptions, compulsory rights, public-domain status, or any other permission supplied independently by law.

A user relying on an independent legal right is not required by this specification to obtain a license merely because a profile exists.

2\. Architecture

2.1 Three instruments, one model

| **Instrument**                   | **Subject**                                 | **Grants permission to**                                                                 |
|----------------------------------|---------------------------------------------|------------------------------------------------------------------------------------------|
| CRL — Catalog Reaction License   | A fixed catalog of completed works          | React to, comment on, review, criticize, excerpt, compare, or remix within stated limits |
| FCL — Franchise Creative License | A living fictional world                    | Create new works using covered elements of that world                                    |
| HPL — Human Performance License  | A natural person's identity and performance | Use or synthesize face, voice, likeness, or motion within stated boundaries              |

All three share:

- the profile envelope (§3.1);

- reliance and versioning semantics (§3.2);

- prohibited-use handling (§3.3);

- attribution and mark discipline (§3.4);

- dispute posture (§3.5);

- revocation principles (§3.6); and

- common serialization concepts.

The instruments are independent.

A registry entry MAY carry more than one instrument.

Permission under one instrument MUST NOT be construed as permission under another.

2.2 Separation of authority

An HPL profile is administered by the person whose identity is its subject, or by a party legally authorized to act for that person.

Where an FCL profile implicates the likeness layer, the FCL profile MUST be capable of pointing to another party's authority.

A conforming verifier MUST resolve the relevant identity permission against the performer or authorized administrator's own registry entry when one is required.

A profile MUST NOT purport to license rights its publisher does not claim authority to control.

Every effective profile MUST resolve to an Authority Claim maintained by the registry.

An Authority Claim MUST identify:

- the publisher;

- the covered subject;

- the asserted basis of authority;

- the scope of the claimed authority;

- known limitations on that authority; and

- the claim's current status.

A registry's recording of an Authority Claim does not constitute adjudication of title.

See §9.2 and §13.

2.3 Three simultaneous representations

A profile may exist in three representations:

1.  legal code — the binding license instrument;

2.  human-readable summary — prose intended for creators and rights holders; and

3.  machine-readable representation — the serialization defined by this specification.

The three representations MUST be semantically consistent as to permissions, restrictions, conditions, version, and covered subject.

Where they diverge, the legal instrument controls unless applicable law provides otherwise.

A material divergence is a defect and SHOULD be corrected by version update.

3\. Common elements

3.1 Profile envelope

Every profile MUST carry an envelope.

| **Field**                 | **Req.** | **Type** | **Notes**                                            |
|---------------------------|----------|----------|------------------------------------------------------|
| holder_id / registrant_id | MUST     | string   | Verified identity; resolution through registry       |
| subject_id                | MUST     | string   | catalog_id, world_id, or registrant identifier       |
| instrument                | MUST     | enum     | crl \| fcl \| hpl                                    |
| profile_version           | MUST     | string   | See §3.2                                             |
| effective_date            | MUST     | date     | ISO 8601                                             |
| supersedes                | SHOULD   | string   | Prior version; prior version MUST remain retrievable |
| authority_claim           | MUST     | string   | Registry identifier for Authority Claim              |
| jurisdiction_note         | MAY      | string   | Advisory only                                        |
| dispute_contact           | MUST     | string   | See §3.5                                             |

Identity verification is a registry function (§9.2).

A profile whose publisher identity is unverified MUST NOT be served as effective.

3.2 Versioning and the reliance envelope

This is the specification's central reliance guarantee.

Four rules apply:

1.  **Profile changes apply prospectively only.**

2.  **Every prior version MUST remain publicly retrievable.**

3.  **Version history MUST be immutable.**

4.  **A work that relied on a valid version remains governed by that version within its reliance envelope.**

Adding, removing, or amending a vertical configuration is a profile-version change.

Registered works

A registered work MUST be evaluated against the profile version governing that work at registration.

A conforming verifier MUST NOT substitute a later profile version merely because it is currently effective.

Unregistered Commons works

Commons use may occur without registration where the applicable profile permits it.

For an unregistered Commons work, the governing version is the version effective when the work was first publicly released under the profile.

The creator bears responsibility for demonstrating that date if historical reliance becomes material.

A registry SHOULD offer an optional Reliance Receipt (§8.6) allowing a creator to establish the applicable version without converting Commons use into registration.

A verifier MAY accept other reliable evidence of publication date.

Where a creator claims historical reliance but supplies neither a Reliance Receipt nor other evidence sufficient for automated verification, a verifier MAY decline to certify historical-version standing and evaluate the use against the currently effective profile.

Limits of reliance

The reliance envelope protects reliance on a valid grant. It does not create rights the publisher never possessed.

A reliance envelope does not validate:

- fraudulent registration by the profile publisher;

- a grant made without the authority claimed;

- a grant of rights the publisher did not control; or

- fraud by the creator seeking reliance.

The treatment of statutory copyright termination, insolvency, transfer of ownership, partial loss of licensing authority, territorial conflicts, and material post-registration modification of a work remains unresolved.

See §13.

3.3 Safety and prohibited uses

Every profile MUST state a prohibited-use policy.

The policy applies across tiers and media and overrides permission granted elsewhere in the profile.

The baseline controlled vocabulary is defined in §10.1.

A profile MAY add publisher-specific prohibited categories.

Publisher-added prohibitions MAY be added, amended, or removed prospectively through profile versioning.

A change to prohibited-use terms MUST NOT retroactively alter the reliance envelope of an existing work, except where the original grant was invalid under §3.2.

A profile MUST NOT make a prohibited category conditional on revenue merely to convert a prohibited use into a purchasable one.

A conforming verifier MUST apply the prohibited-use policy before evaluating permissions that would otherwise authorize the use.

A verifier is not required by this specification to independently adjudicate contested factual or legal questions such as whether particular speech is defamatory.

Where a use has been authoritatively identified, declared, or established as falling within a prohibited category, the verifier MUST treat that category as controlling.

Layer 10 of the FCL model represents this policy logically. To prevent conflicting copies of the same rule, the normative serialization SHOULD maintain one authoritative profile-wide prohibited-use policy and reference it from resolved configurations.

3.4 Attribution, disclosure, and mark display

Every profile MUST state applicable attribution and disclosure requirements.

| **Field**            | **Req.** | **Notes**                                                                                                  |
|----------------------|----------|------------------------------------------------------------------------------------------------------------|
| attribution_required | MUST     | Form or functional equivalent; where required, MUST identify or link to authoritative registry information |
| unofficial_label     | MUST     | A work MUST NOT falsely present itself as official                                                         |
| mark_display         | MUST     | Whether and where the certification mark may or must appear                                                |

Layer 9 MAY impose additional attribution or disclosure requirements by tier, medium, or use category.

Certification mark discipline

The certification mark asserts a limited fact:

*the marked use resolves to a verified registry entry and an identifiable governing permission state.*

The mark MAY identify:

- instrument;

- tier where applicable; and

- declared AI Usage Profile.

The mark MUST NOT encode the substantive license terms.

The mark MUST NOT be treated as the authoritative source of those terms.

The mark MUST NOT encode medium-specific rules in a way that substitutes for registry resolution.

Terms displayed to a party MUST be retrieved from the authoritative registry record or from an authorized mechanism permitted by this specification, including the historical profile version governing the reliance envelope.

3.5 Dispute posture

| **Field**         | **Req.** | **Notes**                                      |
|-------------------|----------|------------------------------------------------|
| dispute_contact   | MUST     | First response within 14 days RECOMMENDED      |
| dispute_posture   | MUST     | See below                                      |
| boundary_disputes | SHOULD   | Referral to custodian procedure when available |

A compliant creator using a valid grant is a licensee or permitted user in good standing, not a claim pending.

An alleged violation MUST be assessed against the profile version governing that work's reliance envelope.

Where a profile permits Commons use without registration, the same posture applies to unregistered but compliant creators.

Permitted use and registered licensed use are distinct states. Both may carry standing under this specification.

Nothing in this section limits independently lawful use under §1.6.

3.6 Revocation and withdrawal

Revocation or withdrawal of standing permission MUST operate prospectively only, subject to the authority and fraud limitations in §3.2.

A publisher MAY by version update:

- close a category to future use;

- move elements between permission states where this specification permits;

- change conditions;

- withdraw a vertical configuration;

- cease accepting future registrations; or

- cease offering future standing permission.

Those changes do not retroactively invalidate compliant works within an existing reliance envelope.

HPL profiles MUST additionally address notice requirements under §6.6.

3.7 Commercial terms and certification overlays

This specification supports machine-readable commercial terms, including:

- thresholds;

- revenue floors;

- royalty rates;

- revenue shares;

- per-unit charges;

- routing instructions;

- operator fees; and

- other stated compensation terms.

FCL-CORE does not set commercial rates.

Economic requirements imposed as a condition of using an FCL certification mark or participating in a certification program MUST be published separately from this Core Specification.

A certification program MAY impose additional economic or operational rules, including reference configurations or operator-fee ceilings.

Those rules MUST NOT silently alter the permission expressed by an FCL-CORE profile.

Core conformance and certification eligibility are distinct.

See §9.4.

4\. CRL — Catalog Reaction License

4.1 Scope of works

| **Field**        | **Req.** | **Notes**                                                  |
|------------------|----------|------------------------------------------------------------|
| works_covered    | MUST     | Enumerated by registry identifier                          |
| works_excluded   | MUST     | Enumerated; MAY be empty                                   |
| exclusion_terms  | MUST     | Excluded works fully reserved under the CRL grant          |
| scope_limitation | MUST     | States what rights the publisher claims and does not claim |

A catalog holder may not control every right contained within a covered work.

Where known third-party rights materially limit a CRL grant, the affected works MUST be identified or the limitation MUST otherwise be clearly stated.

Nothing in a CRL profile restricts uses independently permitted by law under §1.6.

4.2 Use categories

Controlled vocabulary (§10.2):

reaction · first_time_watching · review · criticism · video_essay · educational_analysis · side_by_side_comparison · parody · fan_edit_remix

Each category MUST be stated as permitted or not permitted under the CRL grant.

Silence is not permission under the profile.

A profile MUST NOT condition permission for review or criticism on whether the creator's opinion is favorable.

4.3 Quantitative limits

| **Field**            | **Req.** | **Type / meaning**                      |
|----------------------|----------|-----------------------------------------|
| footage_ratio        | SHOULD   | Duration per unit of published duration |
| per_work_cap         | SHOULD   | Maximum percentage of one work          |
| max_unbroken_excerpt | SHOULD   | Duration                                |
| trailers             | MAY      | enum                                    |
| stills_and_frames    | MAY      | enum                                    |
| isolated_audio       | MAY      | enum                                    |

4.4 Monetization

| **Field**             | **Req.**                     | **Notes**                                     |
|-----------------------|------------------------------|-----------------------------------------------|
| creator_monetization  | MUST                         | Permitted or not, per category                |
| quotation_floor       | SHOULD                       | Usage below which no profile share is owed    |
| revenue_floor         | SHOULD                       | Earnings below which no profile share is owed |
| above_threshold_rates | MUST if monetized            | Per category                                  |
| routing               | MUST if automatically routed | See §8.4                                      |

Both floor types are RECOMMENDED.

A quotation floor allows a profile to distinguish incidental or limited quotation from more substantial licensed use.

A revenue floor prevents administrative overhead from overwhelming low-value activity.

Neither changes rights supplied independently by law.

5\. FCL — Franchise Creative License

5.1 The tier map

An FCL profile MUST classify covered elements into three fixed tiers:

commons

Elements placed in the Commons lane MAY be used without registration where the governing configuration permits the proposed use.

Commons status does not mean unrestricted use.

The applicable layer and medium configuration still govern what may be done.

controlled

Elements placed in the Controlled lane require registration or another stated control mechanism whenever use is permitted.

Controlled configurations MAY additionally impose reporting, payment, approval, or other stated conditions.

canon

Elements placed in the Canon lane are not available under standing FCL permission.

Use requires permission outside the profile, such as a bespoke license or separate affirmative agreement.

Tier names are fixed and MUST NOT be renamed.

An element's tier is singular and world-level.

Its tier MUST NOT vary by medium.

Vertical configurations determine what actions are allowed in a medium; they do not change the element's lane.

This distinction is intentional:

**the tier identifies how access to the element is governed; the layers identify what may be done with it.**

5.2 The ten layers

A complete FCL profile MUST resolve all ten layers.

A profile silent on a required layer is non-conforming.

| **\#** | **Layer**                | **Key**       |
|--------|--------------------------|---------------|
| 1      | World / lore             | world_lore    |
| 2      | Character                | character     |
| 3      | Canon status             | canon_status  |
| 4      | Asset                    | asset         |
| 5      | Likeness                 | likeness      |
| 6      | Commercial               | commercial    |
| 7      | AI generation            | ai_generation |
| 8      | AI training              | ai_training   |
| 9      | Attribution / disclosure | attribution   |
| 10     | Safety / prohibited uses | prohibited    |

Normative constraints:

1.  Layers are independent.

2.  No setting in one layer implies a setting in another.

3.  Layers 7 and 8 are separate permissions.

4.  A permissive ai_generation setting MUST NOT be construed as permission for AI training.

5.  ai_training records or references the rights holder's training permission state; it is not itself a machine-ingestion authorization protocol.

6.  Layer 5 MUST support administration by a party other than the franchise publisher (§2.2).

7.  Layer 10 overrides permissions granted elsewhere (§3.3).

8.  Layer 10 SHOULD resolve to the profile-wide prohibited-use policy rather than duplicating conflicting copies of that policy.

9.  A profile MAY subdivide a layer more finely than this specification's named settings.

10. A profile MUST NOT collapse two layers into one.

5.3 Vertical configurations

A profile states a world-wide configuration and MAY additionally publish configurations scoped to named media.

The vertical rule is normative:

**A medium without its own vertical configuration is governed by the world-wide configuration.**

**A medium with its own vertical configuration is governed by that configuration.**

Configurations MUST NOT be blended selectively.

A medium-specific configuration MUST resolve the complete applicable tier-and-layer matrix for that medium.

A serialization MAY use references to avoid repeating shared global policy, including the profile-wide prohibited-use policy.

A conforming registry MUST nevertheless be able to serve the resolved configuration as a complete, unambiguous permission state.

Named media (§10.3):

prose · visual_art · merchandise · film_video · audio · comics · tabletop · software_games · stage_performance

5.4 The canon-status layer

Layer 3 answers whether a work created under the profile becomes or may claim official status.

canon_status_of_created_work

MUST be stated.

A work created under standing FCL permission is unofficial unless separately designated as canon by the party authorized to make that designation.

A later designation of a particular work as canon is a separate affirmative act.

It is not a retroactive profile-version change and does not arise automatically from the creator's compliance with the profile.

divergent_mode

OPTIONAL.

Where enabled, the profile permits specified contradiction of established continuity.

When enabled, the profile MUST state:

- labeling requirements;

- disclaimer requirements;

- royalty treatment; and

- approval_gates.

approval_gates MUST be enumerated and exhaustive for purposes of the standing profile.

An unenumerated gate is not a gate under the standing FCL profile.

This does not prevent the parties from entering a separate bespoke agreement.

ecosystem_dial

OPTIONAL and MAY be set by medium.

Values (§10.4):

canon_only · option_held · partner_sought · partner_seated

partner_sought is a public, machine-discoverable signal that the publisher is receptive to formal partnership in the named medium.

A conforming registry SHOULD make this state queryable.

5.5 Registration and verification

| **Field**                | **Req.** | **Notes**                                                |
|--------------------------|----------|----------------------------------------------------------|
| registration             | MUST     | States requirement by tier and use                       |
| registration_granularity | SHOULD   | e.g. per creator, per work, per seller, per use category |
| platform_verification    | MUST     | States what a verifier confirms                          |
| portability              | MUST     | See below                                                |

Portability

FCL permission attaches to the covered subject and governing profile, not to one platform.

A registration valid under one conforming verifier MUST be portable to other conforming verifiers, subject to verification of the same governing registry entry and reliance envelope.

A verifier MUST NOT require a creator to surrender an existing reliance envelope merely because the work moves between platforms.

6\. HPL — Human Performance License

An HPL profile's subject is a natural person.

Its publisher is that person or a recorded party legally authorized to administer the relevant rights.

6.1 Temporal windows

A profile MAY divide the registrant's identity into eras carrying independent settings.

Each era MUST state:

- label;

- scope;

- age range or equivalent descriptor; and

- status.

Era status (§10.7):

open_metered · archival_only · sealed · not_applicable

Child windows

Where identity material exists from the registrant's minority, the default status MUST be sealed.

A sealed child window MUST remain sealed until affirmatively opened by the adult whose identity is at issue, except where applicable law requires otherwise.

An administrator MUST NOT open a sealed child window solely by virtue of administrative status.

6.2 The three axes

| **Axis** | **Key** | **Settings**              |
|----------|---------|---------------------------|
| Voice    | voice   | synthesis status, per era |
| Face     | face    | synthesis status, per era |
| Motion   | motion  | synthesis status, per era |

Each axis MUST be stated per era.

Values include:

forbidden · archival_only · metered_per_project · not_offered

not_offered and forbidden are distinct.

not_offered means the registrant has not placed the axis into the standing licensing program.

forbidden is an affirmative prohibition within the profile.

6.3 Permitted and prohibited categories

permitted_uses MUST be enumerated.

Each permitted-use entry MUST state whether it carries standing permission or requires per-project approval.

prohibited_uses MUST incorporate the applicable §3.3 policy and MUST additionally address:

resurrection_scenarios

For purposes of this specification, a resurrection scenario is a generative depiction of the person in a fictional or simulated event presented as occurring after that person's death.

Default: closed.

6.4 Disclosure

synthetic_disclosure

Every synthetic use permitted under an HPL profile MUST be disclosed as synthetic.

This requirement applies even where the registrant approved the use.

Where provenance is carried, the disclosure SHOULD travel with the work through the provenance record.

digital_double_signal

A licensed synthesis SHOULD be identifiable as a synthesis of a specific person under permission.

It MUST NOT be deliberately misrepresented as a wholly synthetic performer with no human referent where that representation would conceal the licensed human identity underlying the synthesis.

6.5 Compensation

| **Field**           | **Req.**                     | **Notes**                                                     |
|---------------------|------------------------------|---------------------------------------------------------------|
| performer_share     | MUST if metered              | Minimum stated by registrant                                  |
| share_negotiability | MUST                         | Standing share MUST NOT be represented as negotiable downward |
| routing             | MUST if automatically routed | See §8.4                                                      |

Within the standing HPL profile, the performer share functions as a floor the registrant may raise through later versioning.

A separate negotiated agreement may exist outside the standing HPL profile, subject to applicable law and the registrant's rights.

6.6 Estate, succession, revocation, and non-waiver

Estate and succession

Where an administrator is recorded, the profile MUST identify the succession order and scope of that administrator's authority.

Standing restrictions SHOULD tighten rather than expand through succession unless applicable law or an affirmative authorization by the registrant provides otherwise.

An administrator MUST NOT rely solely on administrator status to open a category the registrant expressly prohibited or to unseal a child window.

A profile recorded during life is a statement of licensing posture.

It is not a finding of contemporaneous personal consent to every later use.

Post-death authority and operation depend on applicable law, recorded succession, and the rights involved.

Revocation

Revocation of future standing permission is prospective only except where §3.2 applies.

An HPL profile MUST state notice_days.

Non-waiver

An HPL profile MAY add restrictions or compensation requirements above applicable law, collective bargaining agreements, or preexisting contracts.

An HPL profile MUST NOT purport to waive or reduce statutory rights, collective-bargaining minimums, or preexisting contractual protections where such waiver or reduction is prohibited or not expressly authorized.

Where another applicable legal floor controls, that floor controls.

Requirements concerning minors, guardianship, incapacity, cooling-off periods, and coercion safeguards remain unresolved.

See §13.

7\. The AI Usage Axis

The AI Usage Profile is not an eleventh layer and not a fourth tier.

It answers a different question.

**The FCL layers state what the rights holder permits.**

**The AI Usage Profile states how the creator made the work.**

Every registered work under this standard MUST declare exactly one AI Usage Profile.

| **Value**       | **Meaning**                                                                                                                                    |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| human_only      | No generative AI in the core creative output. Non-generative tooling does not forfeit this classification.                                     |
| ai_assisted     | Core creative work remains human-made; AI may assist with research, outlining, cleanup, translation, accessibility, reference, or scaffolding. |
| ai_collaborated | Generative AI materially contributes to core creative output and is disclosed as a creative tool or collaborator.                              |
| ai_unrestricted | Broad generative use permitted, subject to applicable disclosure, provenance, identity, and prohibited-use rules.                              |

Normative requirements:

- Rights holders state which AI Usage Profiles are accepted by tier and configuration.

- Creators declare one AI Usage Profile per registered work.

- A performer MAY impose a stricter AI Usage Profile for the scope of that performer's identity than the franchise default.

- Where a performer override applies, the verifier MUST resolve it against the relevant identity authority.

- AI Usage Profiles govern generation and creative assistance.

- AI training remains a separate permission under Layer 8.

- Permission to use AI in generating a work MUST NOT be construed as permission to train a model on protected material.

- A declared AI Usage Profile MUST be included in the work's registry record.

- Where provenance is carried, the declared profile SHOULD travel with the work.

Relationship to machine-ingestion authorization

Layer 8 may state or reference the rights holder's AI-training permission posture.

Where an RSL or other machine-ingestion endpoint also governs the asset, the FCL training statement MUST NOT be treated as a substitute for machine authorization.

Where both systems apply, neither may widen a restriction stated by the other.

8\. Serialization

8.1 Format

The normative serialization is JSON.

Media type:

application/fcl+json

An RSL binding for environments where the subject is web-addressable is specified separately.

8.2 Discovery and resolution

A conforming verifier MUST resolve a profile through its authoritative registry entry.

A publisher operating a self-hosted conforming node SHOULD additionally expose:

/.well-known/fcl.json

Where the covered subject is web-addressable, a publisher SHOULD advertise the profile using an established machine-readable licensing discovery mechanism where practical, including:

- a licensing directive;

- an HTTP Link header; or

- embedded document metadata;

pointing to the authoritative registry entry.

Reusing a compatible established discovery path is preferred to creating a new one without interoperability need.

Live resolution

Resolution MUST normally use the authoritative registry state.

A verifier MUST NOT treat an uncontrolled local copy of profile terms as authoritative.

This requirement does not prohibit:

- bounded caching under the conditions below;

- validation through an unexpired Standing Token under §8.5; or

- validation of historical Commons reliance through a Reliance Receipt under §8.6.

Caching is permitted where the verifier can detect or bound staleness.

Default and maximum cache or token lifetimes remain unresolved.

See §13.

8.3 Skeleton

{

"fcl_version": "0.1.2",

"instrument": "fcl",

"envelope": {

"holder_id": "example-holder",

"subject_id": "example-world",

"profile_version": "2.0",

"effective_date": "2026-09-11",

"supersedes": "1.0",

"authority_claim": "authority/example-holder/example-world",

"dispute_contact": "registry-entry"

},

"tiers": {

"commons": {

"elements": \["..."\]

},

"controlled": {

"elements": \["..."\]

},

"canon": {

"elements": \["..."\]

}

},

"configuration": {

"commons": {

"world_lore": "...",

"character": "...",

"canon_status": "unofficial",

"asset": "...",

"likeness": "...",

"commercial": "...",

"ai_generation": "...",

"ai_training": "forbidden",

"attribution": "...",

"prohibited": {

"policy_ref": "#/prohibited"

}

},

"controlled": {

"...": "resolved tier-and-layer configuration"

},

"canon": {

"...": "reserved from standing permission"

}

},

"verticals": {

"rule": "unlisted_media_use_worldwide_configuration; listed_configurations_are_complete",

"merchandise": {

"...": "complete resolved tier-and-layer configuration"

}

},

"ai_usage": {

"accepted_profiles": {

"commons": \[

"human_only",

"ai_assisted",

"ai_collaborated"

\],

"controlled": \[

"human_only",

"ai_assisted"

\]

},

"performer_override": "authoritative_where_applicable"

},

"prohibited": \[

"hate_content",

"sexual_content",

"political_advertising",

"regulated_promotion",

"implied_endorsement",

"deceptive_branding",

"defamation",

"fraud",

"synthetic_performer_misuse"

\],

"commercial": {

"terms": "...",

"routing": "..."

},

"mark": {

"resolves_to": "registry/example-world",

"governing_version": "reliance_envelope"

},

"versioning": {

"changes": "prospective_only",

"history": "immutable",

"prior_versions_retrievable": true

}

}

8.4 Revenue routing

Where a profile provides for automatic routing, a conforming implementation MUST execute the split expressed by the governing entry unless another controlling agreement or applicable law requires otherwise.

A conforming verifier MUST NOT silently alter the profile's routing percentages.

Routing under this specification is non-custodial.

Settlement SHOULD occur on regulated payment infrastructure between the paying party and each receiving party's account.

A conforming implementation MUST NOT require custody of routed funds merely as a condition of implementing this standard.

The profile supplies:

- the split;

- the asserted authority for it;

- the receiving destination or pointer; and

- the governing version.

It does not itself hold money.

Every party receiving a routed share MUST be capable of receiving a statement identifying:

- the earning work;

- registry entry;

- profile version;

- relevant period;

- applicable rate; and

- resulting amount.

Automatic routing applies only to revenue the implementation can observe and attribute.

Revenue arising outside participating infrastructure is outside automatic-routing conformance.

8.5 Proof of standing at runtime

A verifier may need to establish standing without contacting the registry for every publication, sale, view, or transaction.

A conforming registry SHOULD support issuance of a Standing Token to a registered creator.

A Standing Token is a signed assertion that, at time of issue, specified registry facts were true.

| **Claim**          | **Req.**                   | **Notes**                                          |
|--------------------|----------------------------|----------------------------------------------------|
| registration_id    | MUST                       | Registry identifier for the registered work or use |
| subject_id         | MUST                       | Covered subject                                    |
| profile_version    | MUST                       | Governing reliance-envelope version                |
| instrument         | MUST                       | crl \| fcl \| hpl                                  |
| tier               | MUST for FCL               | Applicable tier                                    |
| use_category       | MUST for CRL               | From §10.2                                         |
| medium             | MUST                       | Determines applicable vertical configuration       |
| ai_usage_profile   | MUST                       | Work's declaration under §7                        |
| likeness_authority | MUST if Layer 5 implicated | Pointer to relevant identity authority             |
| issued_at          | MUST                       | Timestamp                                          |
| expires_at         | MUST                       | Timestamp                                          |

A verifier presented with a valid Standing Token MAY treat it as satisfying those conformance checks explicitly represented by the token for the duration of its validity.

Constraints

A Standing Token MUST NOT contain the substantive profile terms.

It carries pointers and claims, not the license itself.

A Standing Token MUST NOT be treated as proof that the work does not violate the prohibited-use policy.

The verifier remains responsible for applying §3.3.

expires_at MUST be present.

Token lifetime bounds the amount of permitted staleness.

A registry MUST provide a mechanism capable of invalidating a token issued for a registration later established to be fraudulent or otherwise outside §3.2.

Token invalidation does not retroactively disturb a valid reliance envelope merely because a profile version later changed.

Where immediate revocation status cannot be checked, token expiry defines the accepted staleness bound.

Default and maximum token lifetimes remain unresolved.

Interoperability note

The Standing Token pattern intentionally resembles established license-server and resource-validation token patterns.

An implementation supporting multiple machine-readable licensing systems SHOULD reuse compatible authentication, signing, and validation infrastructure where practical.

8.6 Reliance Receipts for unregistered Commons use

Commons use may occur without registration.

A creator who wants stronger evidence of historical reliance SHOULD be able to request an optional Reliance Receipt from a conforming registry.

A Reliance Receipt does not register the work.

It does not convert Commons use into Controlled use.

It does not create permission that the profile did not already provide.

It records the profile state available for reliance at a particular time.

A Reliance Receipt SHOULD contain:

| **Claim**       | **Req.** | **Notes**                                                                                      |
|-----------------|----------|------------------------------------------------------------------------------------------------|
| subject_id      | MUST     | Covered world or subject                                                                       |
| profile_version | MUST     | Version effective at receipt issuance                                                          |
| instrument      | MUST     | Normally fcl                                                                                   |
| tier            | MUST     | commons                                                                                        |
| medium          | MUST     | Proposed or declared medium                                                                    |
| issued_at       | MUST     | Registry timestamp                                                                             |
| work_hash       | SHOULD   | Optional content hash or equivalent identifier; registry MUST NOT require source asset custody |
| creator_id      | MAY      | MAY be pseudonymous where compatible with applicable rules                                     |

A Reliance Receipt proves the registry state and timestamp it records.

Where work_hash is present, it also associates that timestamp with the supplied hash.

It does not prove facts the registry did not verify, including the creator's authorship or the legality of every aspect of the work.

9\. Conformance

9.1 Conforming profile

A profile conforms if it:

- carries a complete envelope (§3.1);

- resolves to an Authority Claim;

- states prospective-only versioning with retained history (§3.2);

- states a prohibited-use policy (§3.3);

- states attribution and mark requirements consistent with §3.4;

- states a dispute contact and posture (§3.5);

- complies with revocation rules (§3.6);

- expresses commercial terms in a machine-readable form where commercial terms apply;

- for FCL, sorts covered elements into the three fixed tiers and resolves all ten layers;

- for FCL vertical configurations, states each configuration completely;

- for CRL, enumerates covered and excluded works and states a scope limitation;

- for HPL, states axis settings by era, applies the child-window rule, states non-waiver terms, and states required compensation terms where metered;

- declares accepted AI Usage Profiles where applicable; and

- is registered and served by a conforming registry.

9.2 Conforming registry

A registry conforms if it:

1.  verifies publisher identity before serving a profile as effective;

2.  records an Authority Claim for every effective profile;

3.  records the asserted basis and scope of authority;

4.  provides a mechanism for attaching supporting evidence or verification status to that claim;

5.  does not present the existence of an Authority Claim as a judicial determination of title;

6.  serves the live current profile;

7.  retains and serves every prior version;

8.  enforces immutability of version history;

9.  serves each vertical configuration in resolvable complete form;

10. resolves delegated likeness authority under §2.2;

11. makes required discovery fields queryable;

12. stores no biometric source material as part of ordinary registry operation;

13. stores no copyrighted source asset merely to operate the profile registry;

14. supports historical reliance resolution; and

15. SHOULD support Standing Tokens and Reliance Receipts.

A registry holds terms, claims, proofs, hashes, and pointers.

It is not required by this specification to adjudicate the entire chain of title for every covered work.

The initial Authority Claim model does not resolve partial, conflicting, sublicensed, or territorial claims.

See §13.

9.3 Conforming verifier

A verifier conforms if, where relevant to the transaction, it:

1.  resolves permission against the authoritative registry or a valid mechanism authorized by §8;

2.  evaluates a registered work against its reliance-envelope version;

3.  recognizes a valid Reliance Receipt or other acceptable historical evidence for eligible unregistered Commons use;

4.  validates certification marks against the registry rather than treating the mark itself as license text;

5.  applies the prohibited-use policy before otherwise permissive settings;

6.  confirms that the element tier is compatible with the requested access mechanism;

7.  confirms that the applicable configuration permits the proposed use;

8.  confirms that the declared AI Usage Profile is accepted;

9.  resolves a performer or identity override where required;

10. applies commercial terms and routing exactly as represented by the governing profile where the verifier performs those functions;

11. applies profile changes prospectively only;

12. uses established provenance formats where provenance is carried;

13. does not independently rewrite the governing profile; and

14. refers disputes to the applicable process rather than treating platform policy as a final adjudication of legal validity.

A verifier is not required to perform functions it does not offer.

For example, a verifier that does not process payments is not non-conforming merely because it does not execute revenue routing.

Conformance applies to functions actually implemented.

9.4 Certification overlays

Core conformance and certification eligibility are different states.

An implementation MAY conform to FCL-CORE without being authorized to display an FCL certification mark.

A separately governed certification program MAY impose additional conditions, including:

- operator-fee ceilings;

- reference economic configurations;

- transparency requirements;

- audit requirements;

- service-level requirements;

- governance commitments;

- consumer-protection obligations; and

- mark-display rules.

Such rules MUST be published separately.

Certification rules MUST NOT silently alter the machine-readable permission expressed by the governing profile.

Where certification status matters to an implementation, the registry MAY expose the applicable certification-program identifier and status.

Economic rules previously proposed as part of Core conformance — including any operator-fee ceiling or reference creator-share configuration — belong to the certification program rather than this Core Specification.

10\. Controlled vocabularies

10.1 Prohibited uses

hate_content · sexual_content · political_advertising · regulated_promotion · implied_endorsement · deceptive_branding · defamation · fraud · synthetic_performer_misuse

Vocabularies identify categories.

They do not, by themselves, adjudicate whether particular content legally or factually falls within a category.

10.2 CRL use categories

reaction · first_time_watching · review · criticism · video_essay · educational_analysis · side_by_side_comparison · parody · fan_edit_remix

10.3 Media

prose · visual_art · merchandise · film_video · audio · comics · tabletop · software_games · stage_performance

10.4 Ecosystem dial

canon_only · option_held · partner_sought · partner_seated

10.5 AI Usage Profiles

human_only · ai_assisted · ai_collaborated · ai_unrestricted

10.6 Payment types

free · attribution · royalty · revenue_share · per_unit · threshold_gated

The vocabulary is intended to align with adjacent licensing terminology where the meaning corresponds.

Additional payment types MAY be introduced by version update.

10.7 HPL era status

open_metered · archival_only · sealed · not_applicable

Controlled vocabularies are extensible by specification version update.

Profile changes using newly available vocabulary remain prospective under §3.2.

11\. Security and privacy considerations

Registries should hold rules, not source material.

A conforming registry MUST NOT require storage of biometric source material — including voiceprints, facial templates, or motion-capture source data — merely to publish or resolve an HPL profile.

A conforming registry MUST NOT require custody of copyrighted source assets merely to operate an FCL or CRL registry entry.

The registry SHOULD instead hold:

- terms;

- claims;

- proofs;

- hashes;

- authority records;

- identifiers; and

- pointers.

This reduces security and privacy exposure and avoids making the registry an unnecessary repository of high-value biometric or copyrighted material.

Biometric data may be subject to specialized privacy and biometric-information law, including state, federal, and international requirements depending on jurisdiction and use.

Implementations MUST address applicable requirements concerning:

- data minimization;

- encryption in transit and at rest;

- credential compromise;

- key rotation;

- account recovery;

- organizational accounts;

- incident response;

- retention;

- access control; and

- jurisdiction-specific privacy obligations.

Specific implementation requirements remain unresolved.

HPL registrant data

Identity verification necessarily involves personal data.

Implementations SHOULD minimize the information collected.

They SHOULD prefer verification-by-assertion or trusted verification services over indefinite retention of identity documents where practical.

Retention terms MUST be disclosed before registration.

12\. Legal effect (non-normative)

This specification defines a data model.

It does not itself grant rights.

The enforceability and legal character of a permission expressed through it depend on:

- the underlying license instrument;

- the rights actually held by the publisher;

- applicable law;

- jurisdiction;

- contract formation;

- the conduct of the parties; and

- the specific term at issue.

Nothing in this specification diminishes uses independently permitted by law.

Potential legal mechanisms differ by violation:

| **Violation**                                          | **Potential legal or program mechanism**                               |
|--------------------------------------------------------|------------------------------------------------------------------------|
| Use outside the scope of a valid copyright license     | Copyright                                                              |
| Breach of a contractual promise                        | Contract                                                               |
| Unauthorized display or misuse of a certification mark | Trademark / certification-mark rules                                   |
| Unauthorized synthetic likeness                        | Publicity, privacy, digital-replica, contract, or other applicable law |
| Operator or verifier non-conformance                   | Certification suspension, revocation, contract, or program remedies    |
| Materially false registry claim                        | Potential fraud, contract, mark, or other applicable remedies          |

Whether a particular profile term functions as a condition defining the scope of a copyright license or as a contractual covenant depends on drafting and applicable law.

Implementers drafting binding legal instruments should obtain appropriate legal review.

Quantitative limits, tier boundaries, prohibited uses, reporting requirements, attribution requirements, and administrative duties may not receive identical legal treatment in every jurisdiction.

The certification mark reaches conduct governed by the mark and certification program.

It does not create a general remedy against a party who never uses the mark, never claims certification, and never otherwise enters the system.

Territorial scope, moral rights, statutory termination, text-and-data-mining regimes, publicity rights, digital-replica laws, and collective-bargaining rules may constrain or supersede profile terms.

13\. Open issues

Listed because a draft that hides its gaps is not a useful draft.

1\. Reliance-envelope boundaries

The effect of:

- statutory copyright termination;

- insolvency;

- ownership transfer;

- loss of sublicensing authority;

- territorial change;

- expiration of upstream rights; and

- material post-registration modification of a work

requires further specification.

2\. Multi-party and conflicting rights

The current Authority Claim model can record the asserted source and scope of authority but does not yet resolve:

- partial rights;

- multiple owners;

- split media rights;

- territorial ownership;

- conflicting claims;

- sublicensing chains;

- collective rights;

- music publishing splits;

- film and television rights stacks; or

- competing estate claims.

A richer claim-authority model is required.

3\. Boundary-dispute procedure

Profiles may refer disputes to a custodian process.

A complete procedure has not yet been specified.

4\. Vulnerable registrants

Requirements remain unresolved for:

- minors;

- guardianship;

- incapacity;

- cooling-off periods;

- coercion safeguards; and

- changes in legal capacity.

5\. Standing Token and cache lifetimes

Standing Tokens provide a bounded alternative to per-request registry resolution.

Default and maximum lifetimes remain unspecified.

The same is true for allowed cache intervals.

6\. Reliance Receipts

The basic mechanism is specified in §8.6.

Further work is required concerning:

- standardized content hashes;

- pseudonymous creators;

- lost receipts;

- evidentiary sufficiency;

- post-publication issuance;

- migrations between registries; and

- treatment of substantial revisions to the work.

7\. Security requirements

Specific minimum technical controls for registries, verifiers, signing keys, recovery systems, and incident response are not yet specified.

8\. Conditions versus covenants

This specification describes data fields and policy intent.

It does not resolve the drafting required to make a particular term operate as a copyright-license condition rather than a contractual covenant.

9\. Territoriality

Certification-mark enforcement, copyright scope, moral rights, publicity rights, and statutory exceptions vary by jurisdiction.

A territorial-resolution model remains to be developed.

10\. Conformance test suite

No official test suite currently exists.

11\. Custodian and certification governance

Core governance is specified separately.

Certification-program rules, including economic and operator requirements, require separate publication and public comment.

12\. AI-training interoperability

Layer 8 expresses or references the rights holder's AI-training permission state.

A binding to RSL is specified separately, but precedence, synchronization, conflict reporting, and machine-facing error states require further testing.

13\. Digital-replica legislation

Changes in federal, state, or international digital-replica and synthetic-likeness law may materially affect HPL.

The specification must remain capable of incorporating such legal floors without treating them as waivable profile options.

14\. Comments

This draft is published for comment.

Comments on any section, and particularly on §13, are welcome at:

[**info@fclstandard.org**](mailto:info@fclstandard.org)

Substantive comments received SHOULD be acknowledged and addressed in a published disposition accompanying a later draft.

Implementers considering a trial implementation are encouraged to make contact before building.

The editor would rather change the specification than have an implementation depend on a defect.

Appendix A — Change log

v0.1.2 — draft

Architecture and reliance revision.

- Broadened the specification's scope from "derivative works" to creation involving rights controlled by others.

- Added explicit protection for independently lawful use, including

**License**

Except where otherwise noted, FCL-CORE-0.1.2 is licensed under the Creative Commons Attribution 4.0 International License (CC BY 4.0).

Copyright © 2026 FCL Standard Foundation.

The FCL certification marks are not licensed under CC BY 4.0 and are governed separately.
