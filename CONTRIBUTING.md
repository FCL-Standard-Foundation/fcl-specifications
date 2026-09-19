# Contributing

Thank you for helping improve the FCL family of specifications. This repository stewards **draft standards documents**. Contributions that change normative meaning are handled carefully.

## Types of contribution

| Type | Description |
|------|-------------|
| **Editorial correction** | Typos, formatting, broken links, non-normative clarity that does not change requirements. |
| **Specification clarification** | Questions or proposed wording that clarify existing intent without changing normative effect. |
| **Technical issue** | Defects, inconsistencies, or missing technical detail in the data model or conformance text. |
| **Interoperability issue** | Conflicts or gaps with adjacent standards, formats, or systems. |
| **Security concern** | Security or privacy issues — prefer private reporting per [SECURITY.md](SECURITY.md) when sensitive. |
| **Proposed vocabulary addition** | New controlled terms or enumerations. |
| **Proposed normative change** | Changes to MUST/SHOULD/MAY requirements, reliance rules, or conformance. |
| **Implementation feedback** | Experience from trial implementations (no endorsement implied). |

Use the GitHub issue templates where possible.

## Editorial vs substantive

**Editorial** changes do not alter normative requirements, conformance criteria, or the legal/operational meaning of a profile field. Examples: spelling, punctuation, cross-reference fixes, non-normative examples that match existing rules.

**Substantive** changes alter (or could reasonably be read to alter) what an implementer, registry, verifier, or rights holder MUST, SHOULD, or MAY do; versioning/reliance semantics; controlled vocabularies with normative effect; or certification/mark rules.

### Process

1. **Substantive proposals MUST go through an issue** (or equivalent tracked discussion) **before** merge.
2. Do **not** silently rewrite normative text via pull request alone.
3. Pull requests that appear substantive may be converted to discussion or closed pending an issue disposition.
4. Editorial fixes may be accepted via PR when clearly non-normative; maintainers may still ask for an issue if scope is unclear.

## Requirements language

Normative keywords in the specifications follow **RFC 2119** and **RFC 8174**: MUST, MUST NOT, REQUIRED, SHALL, SHALL NOT, SHOULD, SHOULD NOT, RECOMMENDED, MAY, and OPTIONAL, when written in all capitals.

## Versioning policy

- **Released versions are immutable.** A published specification version is not silently edited in place.
- **Normative corrections require a new version** (for example a patch or minor draft revision identifier as appropriate to the document’s scheme).
- **Prior versions remain available** for historical reliance and review.
- **Git history is not published version identity.** Commits on a development branch may differ from a tagged release.
- **Tags and releases identify published versions.** Rely on tags/releases (and the document’s own version field), not on the tip of `main` alone, when citing a published snapshot.

See also [docs/document-status.md](docs/document-status.md).

## Conduct

Participation is governed by [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md).

## Contact

General comment: info@fclstandard.org
