# Introduction

## Background

SNOMED CT is a clinical terminology with global scope and a wide range of clinical specialties and requirements. As a result, SNOMED CT artefacts (including concepts, editions and versioned editions) are often referenced by clinical documents, health information standards, health record implementations, and a range of technical artefacts. To support unambiguous references to SNOMED CT resources, a standard approach to the identification of these resources is needed.

The existing SCTID specification allows SNOMED CT components to be identified across time. However, there are other views of a component that are also useful to identify, such as a concept within a specific SNOMED CT edition at a given point in time. Furthermore, there are other SNOMED CT artefacts, such as a SNOMED CT extension module with all its dependent modules, that do not have an SCTID but also need a consistent identification mechanism. This includes specific national editions, such as the Australian release or the Swedish translation.

A number of groups have emphasised the need to come up with an approach that addresses the broad needs of implementers and offers the opportunities for use of a ubiquitous range of services, using the URI (Uniform Resource Identifier) as a common factor in the interfaces. This document describes a URI space that is intended to meet these requirements, to avoid the proliferation of alternative conflicting schemes, and to evolve to meet additional requirements as they emerge.

The URI space defined in this document uses the syntax defined in [_IETF RFC6570 URI Templates_](#user-content-fn-1)[^1] . In addition, principles of good URI design were drawn from the W3C document _Cool URIs for the_ [_Semantic Web_](#user-content-fn-2)[^2], and _Designing URI Sets for the_ [_UK Public Sect&#x6F;_&#x72;](#user-content-fn-3)[^3].

It should be further noted that, consistent with [the advice of Tim Berners-Lee](#user-content-fn-4)[^4], the HTTP scheme is used for these URIs. Furthermore, to be consistent with the W3C's TAG resolution of [_ISSUE-14_](#user-content-fn-5)[^5], since the URIs defined in this document identify _real-world objects_ and not _information resources_, resolving these URIs should **not** result in an HTTP response code of 200 ("OK") but rather, if anything at all, result in an HTTP response code of 303 ("See Other") to redirect to another URI that identifies a representation of the identified component. The intuition here is that it is not possible to return a real-world object (e.g. "The Eiffel Tower"), but only a representation of it (a picture, a geo-location, a Wikipedia page, etc.). Similarly, it is only possible to return a representation of the identified SNOMED CT component, not the component itself. Further discussion around this issue can be found in Section 4.4 [_Choosing between 202 and Hash_](#user-content-fn-6)[^6] of the aforementioned W3C document _Cool URIs for the Semantic Web_.

## Purpose

This document defines a standard format of URIs for identifying various SNOMED CT artefacts, including components and RF2 releases. This includes URIs for formally identifying the SNOMED CT international edition, national editions, and any specific versions thereof. It does not cover mechanisms or URIs for non-SNOMED CT code systems. Nor does it cover RF1-specific artefacts.

This document provides guidance on using the SNOMED CT URI standard in the context of key motivating use cases, including resolvability of the URIs.

## Scope

This document provides a specification for the format and usage of SNOMED CT URIs. Such a URI might identify "A clinical idea to which a unique Concept Identifier has been assigned". However, it does not specify or standardise any aspect of the representation of these things. Appropriate representations may vary greatly depending on use-case requirements and services utilising the URIs specified here are free to make their own choices.&#x20;

This specification relies on the semantics of SNOMED CT modules as defined in the Release Format 2 specification.&#x20;

## Audience

The intended audience of this document includes:

* Technical professionals who are involved in the development or implementation of terminology systems or healthcare information systems that use SNOMED CT, and
* Academics, researchers, and others who are using SNOMED CT in the context of OWL and other Semantic Web technologies.

This standard should be used when it is required to uniquely identify SNOMED CT concepts and other components in contexts where URIs are expected, or where the interpretation of a code as an SCTID may be ambiguous. It should also be used when an unambiguous interoperable (machine-readable) identifier for an edition (or a versioned edition) is required.

## Use Cases

The following use cases have guided the specification detailed in this document:

1. The OWL representation of the stated form of SNOMED CT requires URIs to identify concepts and object properties (i.e. attributes),
2. The CTS2 specification requires all resources to be identified using URIs,
3. Within the HL7 community, there is a need for a consistent mechanism to identify the SNOMED CT code system and versions of SNOMED CT.

While a register of canonical names for each edition could be compiled and maintained, the module system developed for Release Format 2 already provides the required machinery to support unique naming of editions and, in conjunction with a timestamp, specific versions of an edition. Section 3.1.6 Module Identification from the [Release File Specification](http://snomed.org/rfs) says:

_A moduleId field, assigned to each component, helps identify the origin of content and dependencies in a release. This enables Release Centres to compose a unified release from a number of different modules, yet still identify the origin of content within the release. For example, module ids may be used to differentiate SNOMED CT International content, Australian Medicines terminology and Pathology content within the Australian national release._

The module dependency reference set is used to track dependencies between versioned modules. Thus, by tracing the set of module dependencies from a specified versioned module, one is able to identify all the content relevant to that versioned module. Hence, a versioned module can be used to [uniquely identify a versioned edition](#user-content-fn-7)[^7].

## Releases, Editions and Versions

In this document, we use the terms _Release_, _Edition, and Version_ with the following specific meanings:

* **Release**
  * A **release** is a concrete set of files that is published by a release centre (including SNOMED International). This may include any combination of RF2 files, whether full, snapshot, or delta, as well as documentation, cross-map files, alternate identifiers, and so forth. It may even be just the content that is additional to the SNOMED CT International Edition.
* **Edition**
  * An **edition** is the complete logical or conceptual set of terminology components, independent of any specific version. Examples include the SNOMED CT International Edition and the SNOMED CT-AU Edition.
* **Version**
  * A **version** (also known as a **versioned edition**) is the content of an extension's modules and all the modules upon which they depend, on a specific release date. That is, the SNOMED CT content that is conceptually managed within the versioning scheme of RF2, which is based on the moduleId and effectiveTime fields of the release files. In particular, this includes content that pertains specifically to the meaning of concepts and the contents of reference sets. Examples include the 20250101 version of the SNOMED CT International Edition and the 20250531 version of the SNOMED CT-AU Edition.

## Additional Notes

This standard builds upon several other elements of the SNOMED CT ecosystem. In particular, its semantics are dependent on those of RF2 and the module and versioning mechanisms.

This document defines a standard set of identifiers in the form of URIs. To maintain the integrity of the associated URI space, SNOMED International retains ownership of the **snomed.info** DNS domain. While not a requirement of this specification, URIs defined by this specification, with respect to SNOMED CT core, are resolvable through services provided by SNOMED International.

It is important to understand that the URIs in this specification do not identify the representation of an entity, but rather identify the entity itself. [#resolving-snomed-ct-uris](../3-snomed-ct-uris-in-use.md#resolving-snomed-ct-uris "mention") covers this issue in more detail.

***

<a href="https://docs.google.com/forms/d/e/1FAIpQLScTmbZIf0UEQwYDkY27EEWBkaiYkHSbR0_9DmFrMLXoQLyL7Q/viewform?usp=pp_url&#x26;entry.1767247133=URI+Standard&#x26;entry.670899847=1%20Introduction" class="button primary">Provide Feedback</a>

[^1]: [http://tools.ietf.org/html/rfc6570](http://tools.ietf.org/html/rfc6570)

[^2]: Specifically the section _URIs for Real-World Objects_ [http://www.w3.org/TR/cooluris/#semweb](http://www.w3.org/TR/cooluris/#semweb)

[^3]: [http://www.cabinetoffice.gov.uk/sites/default/files/resources/designing-URI-sets-uk-public-sector.pdf](http://www.cabinetoffice.gov.uk/sites/default/files/resources/designing-URI-sets-uk-public-sector.pdf)

[^4]: Linked Data [http://www.w3.org/DesignIssues/LinkedData.html](http://www.w3.org/DesignIssues/LinkedData.html)

[^5]: ISSUE-14 [http://www.w3.org/2001/tag/group/track/issues/14](http://www.w3.org/2001/tag/group/track/issues/14)

[^6]: Choosing between 303 and Hash [www.w3.org/TR/cooluris#choosing](http://www.w3.org/TR/cooluris#choosing)

[^7]: In the case where a release centre has not organized an edition such that it correspond to the transitive contents of a single module, an additional module can be created that depends on all the modules in the edition. This additional module can then be used to identify that edition. Note that it is non-conformant to release only part of a module.
