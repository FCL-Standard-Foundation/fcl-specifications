Registry and Certification Mark Model

**A model for publishing, resolving, verifying, and displaying permission under the FCL family of standards.**

| **Field**  | **Value**                                                |
|------------|----------------------------------------------------------|
| DOCUMENT   | FCL-REGISTRY-MARK-0.1                                    |
| STATUS     | Draft — published for comment · NO KNOWN IMPLEMENTATIONS |
| DEPENDS ON | FCL-CORE-0.1.2                                           |
| LICENCE    | CC BY 4.0 · royalty-free to implement                    |
| COMMENT    | <info@fclstandard.org>                                   |

Status of This Document

This is a draft companion specification to FCL-CORE.

It defines the registry and certification-mark model used by the FCL family of standards. It does not itself grant rights, determine ownership, adjudicate disputes, or authorize use of an FCL certification mark.

Permission to implement this specification is separate from permission to display any certification mark.

Certification-mark eligibility and use are governed by separately published certification rules.

1\. Purpose

Permission is only useful if it can be found, understood, verified, and relied upon.

The FCL registry model exists to make a published permission profile resolvable over time.

The certification mark exists to tell a person or platform that a work claims standing under that system and to provide a path back to the authoritative record.

The two perform different functions:

**The registry is the source of truth.**

**The mark is a pointer to that truth.**

Neither replaces the underlying legal instrument.

2\. Design principles

A conforming implementation SHOULD follow six principles.

2.1 Terms, not treasure

The registry stores permission information, claims, proofs, identifiers, hashes, and pointers.

It SHOULD NOT become a repository for:

- copyrighted source works;

- voice recordings;

- facial templates;

- motion-capture files;

- model weights;

- raw biometric data; or

- other source material that is unnecessary to resolve permission.

The registry describes rights and permissions.

It does not need custody of the works those rights concern.

2.2 Authority must be visible

A registry MUST identify who published a profile and the basis on which that party claims authority to do so.

Registration is not adjudication.

A registry saying:

*Publisher X claims authority over World Y for these uses.*

is not the same as saying:

*No other party has any rights in World Y.*

The distinction MUST remain visible.

2.3 History must remain resolvable

A creator must be able to determine not only what the profile says today, but what it said when a work was made.

Profile history MUST therefore be immutable and retrievable.

Superseding a profile does not erase it.

2.4 Permission must travel

A creator's standing SHOULD survive movement between conforming platforms.

Permission is attached to the governing profile and work, not to the first platform that recognized it.

2.5 The mark must remain dumb

The certification mark MUST NOT become a miniature license.

It may identify a small fixed set of states, but substantive terms belong in the registry.

This prevents the mark from drifting out of sync with the permission it represents.

2.6 Verification must not imply endorsement

Verification means that the relevant registry records and conformance requirements have been resolved.

It does not mean that the Foundation:

- endorses the creative work;

- considers it official;

- approves its quality;

- agrees with its message;

- warrants that every legal claim is correct; or

- guarantees that no third party has conflicting rights.

3\. Registry objects

A conforming registry MUST be capable of representing the following objects.

3.1 Publisher record

Identifies the person or organization publishing a profile.

Minimum fields:

- publisher_id

- verified name or organizational identity

- verification status

- public contact or resolution endpoint

- administrator identifiers where applicable

- status

The registry MAY permit pseudonymous creator accounts.

A rights holder publishing an authoritative profile MUST have a verifiable legal or organizational identity behind the registry record.

3.2 Subject record

Identifies the thing to which the permission profile applies.

Examples include:

- fictional world;

- franchise;

- character set;

- film catalog;

- music catalog;

- individual work;

- natural person;

- performance identity.

Minimum fields:

- subject_id

- subject type

- public name

- instrument or instruments available

- authoritative profile pointer

- authority-claim pointer

3.3 Authority Claim

An Authority Claim records why the publisher asserts the ability to grant the stated permissions.

Minimum fields:

- authority_claim_id

- publisher_id

- subject_id

- claimed authority type

- scope

- territorial limitation where known

- medium limitation where known

- duration or expiration where known

- evidence status

- known limitations

- current status

Suggested authority types include:

- owner;

- co-owner;

- exclusive licensee;

- non-exclusive licensee with sublicensing authority;

- estate representative;

- authorized agent;

- collective administrator;

- contractual administrator;

- other.

The registry MUST NOT represent an Authority Claim as a judicial determination of title.

3.4 Profile record

A Profile Record contains or resolves to the permission profile defined by FCL-CORE.

Minimum fields:

- profile_id

- instrument

- subject

- publisher

- version

- effective date

- authority claim

- current status

- prior-version pointers

- governing legal instrument pointer

- human-readable summary

- machine-readable representation

3.5 Profile Version Record

Every version MUST have its own immutable record.

Minimum fields:

- profile_id

- profile_version

- effective date

- supersedes

- superseded_by where applicable

- immutable content hash

- machine-readable profile

- human-readable representation

- legal-instrument pointer

- status

A later version MUST NOT overwrite an earlier one.

3.6 Work Registration

A Work Registration identifies a work relying upon an FCL-family profile where registration is required or voluntarily chosen.

Minimum fields:

- registration_id

- creator or registrant identifier

- subject

- instrument

- governing profile version

- tier where applicable

- medium

- use category where applicable

- AI Usage Profile

- likeness-authority pointer where applicable

- registration timestamp

- status

- optional work hash

- provenance pointer where available

The registry SHOULD NOT require custody of the work itself.

3.7 Reliance Receipt

A Reliance Receipt records the profile state available to an unregistered Commons creator at a particular time.

It does not convert Commons use into registration.

It SHOULD contain:

- subject;

- governing profile version;

- tier;

- medium;

- timestamp;

- optional creator identifier;

- optional work hash; and

- registry signature.

3.8 Standing Token

A Standing Token is a short-lived signed representation of selected registry facts.

It exists so that a verifier does not need to make a complete registry round trip for every transaction.

A Standing Token MUST:

- expire;

- identify its issuer;

- point to the governing registry record;

- identify the applicable reliance-envelope version; and

- remain narrower than the underlying permission profile.

It MUST NOT contain the substantive license terms.

4\. Registry states

Profile state and work standing are separate concepts.

A profile MAY be:

- draft

- effective

- superseded

- withdrawn_for_future_use

- disputed

- suspended

- invalidated

A registered work MAY independently be:

- standing

- standing_historical_version

- under_review

- registration_suspended

- registration_invalidated

A profile becoming superseded or withdrawn for future use MUST NOT automatically invalidate works whose reliance envelopes remain valid.

A registry user must be able to distinguish:

*This profile is no longer available for new registrations.*

from:

*Works already created under this version have lost standing.*

Those are not the same state.

5\. Profile lifecycle

5.1 Publication

A profile becomes effective only when:

1.  publisher identity is verified;

2.  an Authority Claim exists;

3.  all required FCL-CORE fields are present;

4.  the effective date has arrived; and

5.  the authoritative registry exposes the profile as effective.

5.2 Revision

A publisher may issue a new version.

The new version MUST:

- identify the version it supersedes;

- receive a new immutable version record;

- state a new effective date; and

- apply prospectively.

5.3 Withdrawal

A publisher may stop accepting future uses under a profile.

Withdrawal MUST NOT delete historical versions.

The registry MUST continue resolving valid reliance envelopes.

5.4 Authority dispute

Where authority is contested, the registry MAY place an Authority Claim or profile into a disputed state.

A disputed state MUST be visible.

The registry MUST NOT silently rewrite historical records.

Procedures for resolving competing authority claims remain a governance matter and are not fully specified here.

6\. Federation

The registry model is intended to support more than one conforming registry operator.

No single commercial platform should be required to become the permanent database of permission for the entire ecosystem.

6.1 Authoritative home

Every profile MUST have one authoritative home registry at a given time.

Other registries MAY:

- index it;

- cache permitted metadata;

- mirror public records;

- query it;

- verify its signatures; or

- provide discovery services.

They MUST NOT silently modify the authoritative profile.

6.2 Portability

Profiles and work registrations SHOULD be portable between conforming registry operators.

Migration MUST preserve:

- identifiers or durable redirects;

- version history;

- reliance envelopes;

- timestamps;

- Authority Claims;

- work registrations; and

- historical resolution.

6.3 Federation identifiers

Identifiers SHOULD be globally resolvable and SHOULD avoid dependence on one vendor's internal database key.

A future version of this specification SHOULD define canonical URI patterns or decentralized identifier requirements.

6.4 Proposed FCL-as-a-Service federation

A future **FCL-as-a-Service (FaaS) federation** may provide shared infrastructure across participating registries, platforms, marketplaces, and rights holders.

Possible FaaS services include:

- permission resolution;

- Standing Token issuance;

- mark verification;

- work-registration portability;

- Reliance Receipts;

- platform compliance APIs;

- commercial-routing instructions;

- authority-claim resolution; and

- enforcement-support workflows.

FaaS does not currently exist and is not required for conformance with this draft.

7\. Certification mark model

The certification mark is the visible trust layer of the FCL system.

Its job is deliberately narrow.

A mark tells a viewer:

*This use claims standing under an identified FCL-family permission record that can be resolved and verified.*

It does not contain the permission itself.

8\. What the mark may communicate

A conforming mark implementation MAY communicate:

- applicable instrument — FCL, CRL, or HPL;

- FCL tier where applicable;

- declared AI Usage Profile;

- certification status; and

- a machine- or human-resolvable pointer.

Examples of display states might include:

**FCL · Commons**

**FCL · Controlled**

**CRL · Licensed**

**HPL · Licensed**

**FCL · Controlled · AI Assisted**

The precise visual system is governed separately.

9\. What the mark must not mean

Displaying an FCL-family certification mark MUST NOT be interpreted as a statement that:

- the work is official;

- the work is canon;

- the Foundation endorses the work;

- the Foundation owns the underlying IP;

- the creator owns the underlying IP;

- the Foundation has independently adjudicated every ownership claim;

- the work is legally immune from challenge;

- the work is free of third-party rights;

- the creative work is factually accurate;

- every statement made in the work is approved by the rights holder; or

- the rights holder has waived rights not expressly included in the governing profile.

10\. Resolution

Every displayed certification mark MUST provide or resolve to an authoritative registry record.

Resolution MAY occur through:

- clickable link;

- QR code;

- embedded metadata;

- platform-native interface;

- API lookup;

- provenance manifest; or

- another conforming mechanism.

The resolved view SHOULD tell a human reader, at minimum:

- what subject is involved;

- which instrument governs;

- who published the profile;

- which profile version governs the work;

- the work's status;

- the applicable tier where relevant;

- the applicable medium;

- declared AI Usage Profile;

- whether likeness authority is separately required;

- whether the profile is current or historical; and

- where the full governing terms can be read.

11\. The mark and historical reliance

A mark displayed on a work created under an older profile version MUST resolve to that work's governing version, not merely to the newest profile.

The registry interface MAY also display the current profile.

It MUST make the distinction clear.

For example:

***This work was created under FCL Profile 1.4 on March 7, 2027. Profile 2.1 is currently in force for new works.***

The historical grant must remain inspectable.

12\. Mark issuance

A certification mark MAY be issued or enabled when a conforming verifier establishes that:

1.  the governing profile exists;

2.  publisher identity has been verified;

3.  an Authority Claim exists;

4.  the claimed use falls within a permitted profile state;

5.  required registration exists where applicable;

6.  the correct reliance-envelope version can be identified;

7.  required identity or likeness permissions resolve where applicable;

8.  required disclosures have been made; and

9.  the implementation satisfies applicable certification-program rules.

Mark issuance does not substitute for the underlying legal grant.

13\. Mark suspension and revocation

Certification-mark status may be suspended or revoked separately from the reliance envelope.

Examples include:

- false certification claims;

- fraudulent registration;

- misuse of the mark;

- failure of a certified verifier to follow program rules;

- unresolved authority fraud;

- material misrepresentation; or

- certification-program violations.

Suspending a mark does not automatically answer whether the underlying creator retains legal permission.

The registry MUST distinguish:

**permission standing**

from:

**certification standing**

A creator may lose authorization to display the certification mark while still possessing rights under an underlying license, depending on the governing legal instrument and circumstances.

14\. Mark misuse

The certification program MAY enforce unauthorized use of its marks separately from enforcement of underlying copyright or other rights.

Examples of misuse include:

- displaying a certification mark without a qualifying registry record;

- fabricating a registry identifier;

- altering a mark to imply a permission state that does not exist;

- displaying a mark after certification has been revoked where continued display is prohibited;

- implying official or canon status through mark presentation; or

- using a confusingly similar mark to falsely claim FCL certification.

Trademark and certification-mark remedies depend on applicable law and the status of the relevant marks.

15\. Verification

A verifier SHOULD be able to answer:

1.  Does the profile exist?

2.  Who published it?

3.  What authority do they claim?

4.  Which version governs this work?

5.  What subject does it cover?

6.  What tier governs the element?

7.  What medium configuration applies?

8.  Is the proposed use permitted?

9.  What AI Usage Profile is declared?

10. Is separate identity or likeness permission required?

11. Does the work have current or historical standing?

12. Is the certification mark valid?

A verifier MUST retrieve substantive terms from the registry or another authoritative mechanism permitted by FCL-CORE.

It MUST NOT infer those terms solely from the visual mark.

16\. Privacy and security

A registry SHOULD minimize the sensitive information it holds.

It SHOULD prefer:

- cryptographic hashes over source-file storage;

- verification assertions over retained identity documents;

- pointers over copied content;

- public keys over shared secrets;

- short-lived tokens over permanent bearer credentials; and

- externally managed payment accounts over custody of funds.

Registries and verifiers MUST address:

- authentication;

- signing-key protection;

- credential compromise;

- key rotation;

- audit logging;

- recovery;

- organizational account control;

- data minimization;

- access control;

- incident response; and

- applicable privacy law.

17\. Relationship to enforcement

The registry and certification mark are not themselves an enforcement system.

They make permission states easier to identify and verify.

Separate implementations may use those permission states as input to:

- publication checks;

- marketplace eligibility;

- monetization decisions;

- payment routing;

- dispute workflows;

- notices;

- enforcement-support tools; or

- other compliance systems.

The proposed FCL-as-a-Service federation may eventually provide common infrastructure supporting those functions.

**The decision to enforce belongs to the rights holder or platform using that information, not to the FCL Standard Foundation.**

Nothing in this specification requires a rights holder to use any particular enforcement mechanism.

18\. Relationship to platforms

A platform integrating the FCL registry model SHOULD be able to:

- resolve profiles;

- verify historical standing;

- validate marks;

- identify applicable profile versions;

- consume Standing Tokens;

- honor Reliance Receipts;

- detect relevant likeness-authority pointers;

- display human-readable terms before publication or sale; and

- preserve portability between conforming services.

A platform MUST NOT represent its own private policy as if it were an FCL permission term.

Platform policy and FCL permission are separate layers.

19\. Conformance

19.1 Conforming registry implementation

A conforming registry:

- verifies publisher identity;

- records Authority Claims;

- preserves immutable profile history;

- resolves current and historical versions;

- supports work registrations;

- supports historical reliance resolution;

- exposes machine-readable profile data;

- distinguishes profile status from work standing;

- distinguishes permission standing from certification standing;

- avoids unnecessary custody of source assets and biometric data; and

- provides resolvable certification-mark records where it participates in certification.

19.2 Conforming mark implementation

A conforming mark implementation:

- resolves to an authoritative registry record;

- does not encode substantive license terms;

- does not imply official status;

- does not imply Foundation endorsement;

- identifies historical reliance correctly;

- identifies instrument and permitted fixed metadata consistently; and

- obeys applicable certification-program rules.

19.3 Conforming verifier

A conforming verifier:

- resolves authoritative registry data;

- recognizes the correct reliance-envelope version;

- distinguishes current profile terms from historical standing;

- validates the certification mark independently of its appearance;

- follows delegated likeness authority;

- recognizes valid Standing Tokens and Reliance Receipts;

- applies prohibited-use rules as required by FCL-CORE; and

- does not silently expand permission beyond the governing record.

20\. What this specification does not settle

The following remain open:

- canonical federated identifier format;

- registry migration protocol;

- conflicting Authority Claims;

- territorial claims;

- partial ownership;

- multi-party approval;

- certification appeals;

- mark suspension procedure;

- certification audit requirements;

- default Standing Token lifetime;

- Reliance Receipt evidentiary standards;

- FaaS federation governance;

- verifier trust roots;

- offline verification;

- canonical QR and link formats;

- certification-mark visual specifications; and

- certification-program economic requirements.

These issues SHOULD be resolved through later drafts and separate certification-program rules rather than hidden inside implementation behavior.

21\. Human-readable registry example

A resolved work might display:

**FCL VERIFIED**

**Work:** *The Clockwork Crown: An Unofficial Adventure*

**World:** *The Brass Kingdom*

**Instrument:** Franchise Creative License

**Tier:** Controlled

**Medium:** Tabletop

**AI Usage:** AI Assisted

**Creator standing:** Valid

**Governing profile:** Version 1.3

**Registered:** June 14, 2027

**Current world profile:** Version 1.6

This work remains governed by Version 1.3 under its reliance envelope.

**Canon status:** Unofficial

**Likeness permissions:** Not implicated

**Publisher:** Example Worlds LLC

**Authority claim:** Verified identity · asserted world owner

\[Read the governing profile\]

The registry view may contain additional information.

The certification mark itself should not.

22\. The architectural boundary

The FCL system separates four functions:

**The rights holder publishes the permission.**

**The registry preserves and resolves it.**

**The verifier checks it.**

**The certification mark points back to it.**

None should quietly become the other.

That separation is what allows permission to remain portable, inspectable, versioned, and usable across platforms.

23\. Comments

This draft is published for comment.

Comments are welcome at:

[**info@fclstandard.org**](mailto:info@fclstandard.org)

Implementers considering a registry, verifier, marketplace integration, or certification-mark implementation are encouraged to make contact before building.

The purpose of publishing the model early is to find architectural defects before anyone depends on them.

Appendix A — Proposed document relationships

The FCL family currently anticipates the following specification structure:

**FCL-CORE**

Defines the common permission model, three instruments, ten layers, tiers, reliance, serialization, and core conformance.

**FCL-RSL-BINDING**

Defines interoperability between the FCL family and Really Simple Licensing / adjacent machine-ingestion signals.

**FCL-REGISTRY-MARK**

Defines registry records, historical resolution, federation behavior, certification-mark semantics, and mark verification.

**FCL-CERTIFICATION-RULES**

Defines who may display the certification marks and under what operational, governance, and economic conditions.

**FCL-FAAS**

Future document defining the proposed FCL-as-a-Service federation and shared platform services.

Appendix B — Change log

v0.1 — Draft

Initial publication.

- Defined registry objects.

- Defined Authority Claims.

- Defined profile and work states.

- Defined federation principles.

- Defined certification-mark semantics.

- Separated permission standing from certification standing.

- Defined historical mark resolution.

- Defined mark issuance, suspension, and misuse concepts.

- Defined platform and verifier responsibilities.

- Identified the proposed FaaS federation as future infrastructure rather than an existing implementation.

- Clarified that enforcement decisions remain with rights holders and platforms rather than the FCL Standard Foundation.

Except where otherwise noted, **FCL-REGISTRY-MARK-0.1** is licensed under the **Creative Commons Attribution 4.0 International License (CC BY 4.0)**.

Copyright © 2026 FCL Standard Foundation.

Implementation of this specification does not confer permission to use any FCL certification mark.

The FCL certification marks are not licensed under CC BY 4.0 and are governed separately by the applicable certification program.
