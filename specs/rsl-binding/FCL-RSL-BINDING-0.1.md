FCL-RSL-BINDING-0.1

RSL governs whether a machine may ingest. This governs whether a person may build. Here is the seam.

DOCUMENT

FCL-RSL-BINDING-0.1

**STATUS** Draft — published for comment

COMPANION TO

FCL-CORE-0.1.2

**REQUIRES** No change to RSL. Extension is namespace-safe.

**SOURCE** Markdown source

1\. Purpose

2\. The gap, stated plainly

3\. What RSL 1.0 specifies

4\. What the Human Consent Standard adds

5\. Concept correspondence

6\. Design constraints

7\. The binding

8\. Worked examples

9\. Where the models genuinely diverge

10\. What is not proposed

11\. The one request

12\. Open questions for reviewers

13\. Provenance of this document

1\. Purpose

RSL 1.0 defines machine-readable licensing terms for automated access to digital assets. RSL Media’s Human Consent Standard extends the model to identity, works, characters, and marks, with a three-state permission model: allowed, allowed with terms, prohibited.

The middle state is declared but its terms are not specified. This document proposes a binding by which those terms may be expressed, using a vocabulary purpose-built for the transaction they describe.

Nothing in this document requires a change to RSL. §7 specifies a binding that works today under XML namespace extension. §11 contains a single optional request, which would improve discoverability but is not required for the binding to function.

This document is written to be checked. Where it characterizes RSL, it cites the normative source. Corrections are welcome and will be published.

2\. The gap, stated plainly

RSL answers: may an automated client access, index, train on, or infer from this asset, and on what terms?

It does not answer, and does not attempt to answer: may a person create a new work using this material, and what happens to the revenue when they do?

These are different transactions with different counterparties, different units, and different outputs. The first ends with ingestion. The second produces a new work that itself requires standing, attribution, provenance, and often a revenue split among three or more parties.

The Human Consent Standard’s allowed with terms is the point where the second question surfaces inside the RSL model. A rights holder who permits derivative creation “with terms” needs a vocabulary for those terms. FCL-CORE is that vocabulary.

3\. What RSL 1.0 specifies

Summarized for shared reference. Normative source: rslstandard.org.

An RSL document is XML conforming to XML 1.0, rooted at with the namespace https://rslstandard.org/rsl, available as a standalone .xml file, an RSS module using the rsl: prefix, or embedded in HTML via

**Except where otherwise noted, FCL-RSL-BINDING-0.1 is licensed under the Creative Commons Attribution 4.0 International License (CC BY 4.0).**

Copyright © 2026 FCL Standard Foundation.

The FCL certification marks are not licensed under CC BY 4.0 and are governed separately. 
