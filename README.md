# FCL Standards

Permission at Scale.

This repository holds the open specifications for the **FCL Standard Foundation** advance-permission framework: a machine-readable (and human-readable) way for rights holders to publish standing, conditional permission to create, publish, distribute, or monetize new work using rights they control.

## Instruments

The framework defines three related license instruments that share one data model:

| Instrument | Full name | Subject |
|------------|-----------|---------|
| **CRL** | Catalog Reaction License | A fixed catalog of completed works |
| **FCL** | Franchise Creative License | A living fictional world |
| **HPL** | Human Performance License | A natural person's identity and performance |

These documents are **drafts published for comment**. They have not been adopted as a formal standard. There are no known implementations claimed by this repository.

## Current documents

| Document | Path |
|----------|------|
| FCL-CORE-0.1.2 | [specs/core/FCL-CORE-0.1.2.md](specs/core/FCL-CORE-0.1.2.md) |
| FCL-RSL-BINDING-0.1 | [specs/rsl-binding/FCL-RSL-BINDING-0.1.md](specs/rsl-binding/FCL-RSL-BINDING-0.1.md) |
| FCL-REGISTRY-MARK-0.1 | [specs/registry-mark/FCL-REGISTRY-MARK-0.1.md](specs/registry-mark/FCL-REGISTRY-MARK-0.1.md) |
| FCL-CERTIFICATION-RULES-0.1 | [specs/certification/FCL-CERTIFICATION-RULES-0.1.md](specs/certification/FCL-CERTIFICATION-RULES-0.1.md) |

Supporting notes: [docs/architecture.md](docs/architecture.md), [docs/terminology.md](docs/terminology.md), [docs/document-status.md](docs/document-status.md).

## Status

**Under development.** Specs in this repository are drafts for public comment. They are not adopted standards, do not grant rights by themselves, and do not constitute legal advice. See each document's status header and [docs/document-status.md](docs/document-status.md).

Publication of a draft here does **not** imply product endorsement, vendor certification, or that any particular implementation is conformant or authorized to use FCL marks.

## Principles

- **Permission before creation** — standing terms published in advance, not only negotiated after a work is made.
- **Machine-readable** — profiles serialize so tools and verifiers can resolve terms.
- **Human-readable** — creators and rights holders can understand summaries alongside legal instruments.
- **Rights-holder control** — the rights holder (or authorized administrator) sets and versions the permission profile.
- **Independently lawful uses remain lawful** — fair use, fair dealing, statutory exceptions, public-domain status, and similar permissions are not narrowed by a profile's existence.
- **Prospective versioning** — profile changes apply going forward; historical reliance is preserved within the reliance envelope.
- **Historical reliance** — works that relied on a valid version remain governed by that version within its envelope.
- **Portability** — permission expressions are designed to move across registries and platforms.
- **Separation of permission from certification** — publishing or implementing a profile is distinct from authorization to use certification marks.
- **Vendor neutrality** — the specifications are not tied to a single commercial vendor.
- **Interoperability** — bindings and mappings to adjacent standards (for example RSL) are documented separately where defined.

## Participate

- Open an issue using the templates in [`.github/ISSUE_TEMPLATE/`](.github/ISSUE_TEMPLATE/).
- Read [CONTRIBUTING.md](CONTRIBUTING.md) before proposing normative changes.
- Report security or privacy concerns per [SECURITY.md](SECURITY.md).
- See [GOVERNANCE.md](GOVERNANCE.md) for stewardship context.

## Website

https://www.fclstandard.org

## Contact

info@fclstandard.org

## License and marks

Specification text in this repository is licensed under [CC BY 4.0](LICENSE) except where a file states otherwise. Trademarks, logos, and certification marks are **not** licensed under CC BY 4.0 — see [LICENSING.md](LICENSING.md) and [TRADEMARKS.md](TRADEMARKS.md).
