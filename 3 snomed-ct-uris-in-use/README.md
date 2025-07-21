# SNOMED CT URIs in Use

* [#resolving-snomed-ct-uris](./#resolving-snomed-ct-uris "mention")
* [#uri-use-cases](./#uri-use-cases "mention")

## Resolving SNOMED CT URIs

### Overview

[Section 2](../3%20snomed-ct-uris-in-use/2-SNOMED-CT-URI-Space_29951163.html) defines a set of URI spaces that are used to **identify** a variety of SNOMED CT resources, but it does not discuss **resolving** these URIs. The URIs in the standard use the http scheme and the domain name snomed.info, which is owned by SNOMED International. This means that SNOMED International is in control of whether or not these URIs, when treated as URLs and resolved, will result in a document being available, a 404 ("Not Found") error, or something else.

### URIs Resolved by SNOMED International

SNOMED International resolves URIs for concepts from the SNOMED CT International Edition (of the form [http://snomed.info/id/{SCTID}](http://snomed.info/id/%7BSCTID)) to the public SNOMED CT browser.

URIs for modelling resources (as described in [2.7 URIs for SNOMED Resources](../3%20snomed-ct-uris-in-use/2.7-URIs-for-SNOMED-Resources_106700321.html)) will, by default, be resolved to a HTML representation of the identified entity. To support machine-readability, the HTTP Accept header will be used to perform content negotiation. For example, the value "application/fhir+json" may be supplied to request a FHIR representation in JSON syntax. Following FHIR conventions, a suffix of "?\_format=json" will be interpreted as equivalent to providing an Accept header of "application/fhir+json" with maximum priority. This is to facilitate access via web browsers where access to HTTP headers is not normally available.

### URIs Resolved by Others

A Release Centre or other service providers may also want to support the resolution of other URIs (e.g. those that identify resources that they maintain). A general approach to this involves deploying a resolving service with an endpoint URL such as

* `http://myservice.example.com/`

which is configured to resolve URLs that embed SNOMED CT URIs. Continuing the example, a URL of the following form

* (1) `http://myservice.example.com/?uri=http://snomed.info/{...}`

might be redirected with an HTTP response code of 303 to

* (2) `http://myservice.example.com/snomed/{...}`

which in turn resolves and returns an appropriate document. Conceptually, we can think of the original URL (1) as identifying what the _MyService_ endpoint knows about the identified SNOMED CT resource, and the returned document, identified by the second URL (2), as being a representation of that knowledge.

What might such a document look like? Let us consider the example URL

* `http://myservice.example.com/?uri=http://snomed.info/id/900000000000498005`

The document ultimately returned by the service might be in JSON or XML or HTML or plain text format and contain information indicating that the SCTID is valid, and refers to a non-extension Concept[1](https://confluence.ihtsdotools.org/display/DOCURI/3.1+Resolving+SNOMED+CT+URIs#Footnote1) . It might also indicate that the service knows about one or more Editions or Versions in which this Concept is defined. It might further supply the Fully Specified Name for the Concept as given in the Version with the most recent effectiveTime. Note that the exact nature of what the service says about the Concept is up to the service itself. One service may offer a RESTful API that allows detailed querying down to the primitive/fully defined status of a versioned Concept, while another may return a representation of properties of a versioned Concept that then needs to be parsed to determine its primitive/fully defined status.

***

| Footnotes Ref                                                                                         | Notes                                                           |
| ----------------------------------------------------------------------------------------------------- | --------------------------------------------------------------- |
| [1](https://confluence.ihtsdotools.org/display/DOCURI/3.1+Resolving+SNOMED+CT+URIs#FootnoteMarker1-0) | This information is directly discernable from the SCTID itself. |

***

## URI Use Cases

### The Owl Representation of SNOMED CT

The OWL representation of SNOMED CT makes use of URIs for identifying Concepts, the previously implicit grouping role, and the ontology itself (i.e. the set of axioms).

The old pattern used for Concepts was

`http://www.snomed.org/SCT_{sctid}`

which is now replaced by

`http://snomed.info/id/{sctid}`

The grouping role URI was

`http://www.snomed.org/RoleGroup`

and is now

`http://snomed.info/id/609096000`

For the OWL XML representation, the URI was unspecified (the empty string), while for the OWL Functional Syntax representation the URI was (via RDF:about)

`http://www.snomed.org/sct.owl`

and now includes explicit version information

`http://snomed.info/sct/{sctid}/version/{timestamp}`

When representing SNOMED CT ontologies using OWL 2, both an ontologyURI and a versionURI should be included using the following forms respectively[1](https://confluence.ihtsdotools.org/display/DOCURI/3.2+URI+Use-Cases#Footnote1) :

`http://snomed.info/sct/{sctid}`

`http://snomed.info/sct/{sctid}/version/{timestamp}`

### The CTS2 Specification

The CTS2 specification requires that all resources be identified using URIs. This section lists, where such a thing exists, SNOMED International standard URIs for the resources that require URIs in the CTS2 implementation. This omits URIs for things such as External Code Systems and Value Sets since they are outside the scope of the SNOMED CT URI Standard. Note, however, that a Reference Set is the SNOMED CT mechanism for identifying an arbitrary set of Concepts, which is analogous to a Value Set. Thus the Reference Set URI would be the appropriate thing to use as the Value Set identifier.

| **Resource**                   | **URI**                                                                     | **Example**                                                                                                                   |
| ------------------------------ | --------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| SNOMED CT Edition              | http://snomed.info/sct/{moduleId}                                           | http://snomed.info/sct/900000000000207008SNOMED CT International Edition                                                      |
| SNOMED CT Version              | http://snomed.info/sct/{moduleId}/version/{effectiveTime}                   | http://snomed.info/sct/900000000000207008/version/20120131SNOMED CT International January 2012 Version                        |
| Module                         | http://snomed.info/module/{moduleId}                                        | http://snomed.info/module/900000000000207008SNOMED CT Core Module (only)                                                      |
| A specific release of a Module | http://snomed.info/module/{moduleId}/time/{timestamp}                       | http://snomed.info/module/900000000000207008/time/20120131SNOMED CT Core Module (only) with respect to the timestamp 20120131 |
| SCTID                          | http://snomed.info/id/{sctid}                                               | http://snomed.info/id/449650002                                                                                               |
| UUID                           | http://snomed.info/id/{uuid}                                                | http://snomed.info/id/00000692-31c5-81a8-2e54b488c824                                                                         |
| Table Field                    | http://snomed.info/field/{table name}.{field name}                          | http://snomed.info/field/Relationship.characteristicTypeId                                                                    |
| Map                            | http://snomed.info/id/{map sctid}                                           | http://snomed.info/id/900000000000498005A map is just a reference set in a specific format                                    |
| Map version                    | http://snomed.info/sct/{moduleId}/version/{effectiveTime}/id/{map sctid}    | http://snomed.info/sct/900000000000207008/version/2012013/id/900000000000498005                                               |
| Refset                         | http://snomed.info/id/{refset sctid}                                        | http://snomed.info/id/900000000000498005                                                                                      |
| Refset version                 | http://snomed.info/sct/{moduleId}/version/{effectiveTime}/id/{refset sctid} | http://snomed.info/sct/900000000000207008/version/2012013/id/900000000000498005                                               |
| Role Group                     | http://snomed.info/id/609096000                                             | http://snomed.info/id/609096000                                                                                               |

### Identifying SNOMED CT Versions in HL7

Traditionally, HL7 has used OIDs to identify Code Systems. The OID for SNOMED CT is 2.16.840.1.113883.6.96. This is the OID that should be used for all versions of SNOMED CT and related terminologies (such as the Australian Medicines Terminology) because it identifies the **system** , i.e. the set of rules for interpreting SCTIDs. Under these rules, any specific SCTID is either defined with respect to a particular SNOMED CT Version, or it is undefined (i.e. not included/mentioned in that version). Furthermore, any given SCTID always identifies the _same thing_ in all versions in which it is defined.

The HL7 specification says: _the interpretation of version strings is defined by the Code System_ (and not by HL7). This means we can use the URI for a Version (versioned Edition) as the version code:

http://snomed.info/sct/{sctid}/version/{timestamp}

For example, here is how an element of Data Type CD might appear in a CDA document with:

### Identifying SNOMED CT Versions in HL7 FHIR

Fast Healthcare Interoperability Resources (FHIR™)[2](https://confluence.ihtsdotools.org/display/DOCURI/3.2+URI+Use-Cases#Footnote2) defines a set of 'resources' to represent health and healthcare administration-related information. Rather than OIDs, FHIR uses URIs to identify code systems, usually along with an associated version string. The code system is intended to characterise the set of valid codes, hence the recommended URI to use for this is:

http://snomed.info/sct

and the recommended string template to use for the associated version, substituting in the appropriate module sctid and effective time, is:

http://snomed.info/sct/{sctid}/version/{timestamp}

***

| Footnotes Ref                                                                              | Notes                                                                                                                                                  |
| ------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [1](https://confluence.ihtsdotools.org/display/DOCURI/3.2+URI+Use-Cases#FootnoteMarker1-0) | See OWL 2 Web Ontology Language Structural Specification and Functional-Style Syntaxhttp://www.w3.org/TR/owl2-syntax/#Ontology\_IRI\_and\_Version\_IRI |
| [2](https://confluence.ihtsdotools.org/display/DOCURI/3.2+URI+Use-Cases#FootnoteMarker2-0) | See [http://hl7.org/fhir](http://hl7.org/fhir)                                                                                                         |

<a href="https://docs.google.com/forms/d/e/1FAIpQLScTmbZIf0UEQwYDkY27EEWBkaiYkHSbR0_9DmFrMLXoQLyL7Q/viewform?usp=pp_url&#x26;entry.1767247133=URI+Standard&#x26;entry.670899847=3%20SNOMED%20CT%20URIs%20in%20Use" class="button primary">Provide Feedback</a>
