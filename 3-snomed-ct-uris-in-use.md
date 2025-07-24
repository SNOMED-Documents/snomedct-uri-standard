# SNOMED CT URIs in Use

* [#resolving-snomed-ct-uris](3-snomed-ct-uris-in-use.md#resolving-snomed-ct-uris "mention")
* [#uri-use-cases](3-snomed-ct-uris-in-use.md#uri-use-cases "mention")

## Resolving SNOMED CT URIs

### Overview

[2-snomed-ct-uri-space.md](2-snomed-ct-uri-space.md "mention") defines a set of URI spaces used to identify various SNOMED CT resources, but it does not discuss **resolving** these URIs. The URIs in the standard use the http scheme and the domain name snomed.info, which SNOMED International owns. This means that SNOMED International is in control of whether or not these URIs, when treated as URLs and resolved, will result in a document being available, a 404 ("Not Found") error, or something else.

### URIs Resolved by SNOMED International

SNOMED International resolves URIs for concepts from the SNOMED CT International Edition (of the form `http://snomed.info/id/{SCTID}`) to the public SNOMED CT browser.

URIs for modelling resources (as described in [#id-2.7urisforsnomedresources-background](2-snomed-ct-uri-space.md#id-2.7urisforsnomedresources-background "mention")) will, by default, be resolved to a HTML representation of the identified entity. To support machine-readability, the HTTP Accept header will be used to perform content negotiation. For example, the value "`application/fhir+json`" may be supplied to request a FHIR representation in JSON syntax. Following FHIR conventions, a suffix of "`?_format=json`" will be interpreted as equivalent to providing an Accept header of "`application/fhir+json`" with maximum priority. This is to facilitate access via web browsers where access to HTTP headers is not normally available.

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

The document ultimately returned by the service might be in JSON or XML or HTML or plain text format and contain information indicating that the SCTID is valid, and refers to a non-extension Concept[^1]. It may also indicate that the service is aware of one or more Editions or Versions in which this Concept is defined. It might further supply the Fully Specified Name for the Concept as given in the Version with the most recent effectiveTime. Note that the exact nature of what the service says about the Concept is up to the service itself. One service may offer a RESTful API that allows detailed querying down to the primitive/fully defined status of a versioned Concept, while another may return a representation of properties of a versioned Concept that then needs to be parsed to determine its primitive/fully defined status.

***

## URI Use Cases

### The Owl Representation of SNOMED CT

The OWL representation of SNOMED CT utilises URIs to identify concepts, the previously implicit grouping role, and the ontology itself (i.e., the set of axioms).

The old pattern used for Concepts was

* `http://www.snomed.org/SCT_{sctid}`

which is now replaced by

* `http://snomed.info/id/{sctid}`

The grouping role URI was

* `http://www.snomed.org/RoleGroup`

and is now

`http://snomed.info/id/609096000`

For the OWL XML representation, the URI was unspecified (the empty string), while for the OWL Functional Syntax representation the URI was (via RDF:about)

* `http://www.snomed.org/sct.owl`

and now includes explicit version information

* `http://snomed.info/sct/{sctid}/version/{timestamp}`

When representing SNOMED CT ontologies using OWL 2, both an ontologyURI and a versionURI should be included using the following forms, respectively[^2] :

* `http://snomed.info/sct/{sctid}`
* `http://snomed.info/sct/{sctid}/version/{timestamp}`

### The CTS2 Specification

The CTS2 specification requires that all resources be identified using URIs. This section lists, where such a thing exists, SNOMED International standard URIs for the resources that require URIs in the CTS2 implementation. This omits URIs for things such as External Code Systems and Value Sets since they are outside the scope of the SNOMED CT URI Standard. Note, however, that a Reference Set is the SNOMED CT mechanism for identifying an arbitrary set of Concepts, which is analogous to a Value Set. Thus the Reference Set URI would be the appropriate thing to use as the Value Set identifier.

<table><thead><tr><th width="150.21484375">Resource</th><th>URI</th><th>Example</th></tr></thead><tbody><tr><td>SNOMED CT Edition</td><td><code>http://snomed.info/sct/{moduleId}</code></td><td><code>http://snomed.info/sct/900000000000207008SNOMED CT International Edition</code></td></tr><tr><td>SNOMED CT Version</td><td><code>http://snomed.info/sct/{moduleId}/version/{effectiveTime}</code></td><td><code>http://snomed.info/sct/900000000000207008/version/20120131SNOMED CT International January 2012 Version</code></td></tr><tr><td>Module</td><td><code>http://snomed.info/module/{moduleId}</code></td><td><code>http://snomed.info/module/900000000000207008SNOMED CT Core Module (only)</code></td></tr><tr><td>A specific release of a Module</td><td><code>http://snomed.info/module/{moduleId}/time/{timestamp}</code></td><td><code>http://snomed.info/module/900000000000207008/time/20120131SNOMED CT Core Module (only) with respect to the timestamp 20120131</code></td></tr><tr><td>SCTID</td><td><code>http://snomed.info/id/{sctid}</code></td><td><code>http://snomed.info/id/449650002</code></td></tr><tr><td>UUID</td><td><code>http://snomed.info/id/{uuid}</code></td><td><code>http://snomed.info/id/00000692-31c5-81a8-2e54b488c824</code></td></tr><tr><td>Table Field</td><td><code>http://snomed.info/field/{table name}.{field name}</code></td><td><code>http://snomed.info/field/Relationship.characteristicTypeId</code></td></tr><tr><td>Map</td><td><code>http://snomed.info/id/{map sctid}</code></td><td><code>http://snomed.info/id/900000000000498005A map is just a reference set in a specific format</code></td></tr><tr><td>Map version</td><td><code>http://snomed.info/sct/{moduleId}/version/{effectiveTime}/id/{map sctid}</code></td><td><code>http://snomed.info/sct/900000000000207008/version/2012013/id/900000000000498005</code></td></tr><tr><td>Refset</td><td><code>http://snomed.info/id/{refset sctid}</code></td><td><code>http://snomed.info/id/900000000000498005</code></td></tr><tr><td>Refset version</td><td><code>http://snomed.info/sct/{moduleId}/version/{effectiveTime}/id/{refset sctid}</code></td><td><code>http://snomed.info/sct/900000000000207008/version/2012013/id/900000000000498005</code></td></tr><tr><td>Role Group</td><td><code>http://snomed.info/id/609096000</code></td><td><code>http://snomed.info/id/609096000</code></td></tr></tbody></table>

### Identifying SNOMED CT Versions in HL7

Traditionally, HL7 has used OIDs to identify Code Systems. The OID for SNOMED CT is 2.16.840.1.113883.6.96. This is the OID that should be used for all versions of SNOMED CT and related terminologies (such as the Australian Medicines Terminology) because it identifies the **system**, i.e., the set of rules for interpreting SCTIDs. Under these rules, any specific SCTID is either defined with respect to a particular SNOMED CT Version, or it is undefined (i.e. not included/mentioned in that version). Furthermore, any given SCTID always identifies the _same thing_ in all versions in which it is defined.

The HL7 specification says: _the interpretation of version strings is defined by the Code System_ (and not by HL7). This means we can use the URI for a Version (versioned Edition) as the version code:

`http://snomed.info/sct/{sctid}/version/{timestamp}`

For example, here is how an element of Data Type CD might appear in a CDA document with:

{% code overflow="wrap" %}
```
<xyz code="78835011000036104" codeSystem="2.16.840.1.113883.6.96" codeSystemName="Australian Medicines Terminology (AMT)" codeSystemVersion= "http://snomed.info/sct/900062011000036108/version/20121231" displayName="GANFORT 0.03% / 0.5% eye drops: solution, 3 mL"/> </xyz>
```
{% endcode %}

### Identifying SNOMED CT Versions in HL7 FHIR

Fast Healthcare Interoperability Resources (FHIR[^3]™) defines a set of 'resources' to represent health and healthcare administration-related information. Rather than OIDs, FHIR uses URIs to identify code systems, typically accompanied by an associated version string. The code system is intended to characterise the set of valid codes, hence the recommended URI to use for this is:

`http://snomed.info/sct`

and the recommended string template to use for the associated version, substituting in the appropriate module sctid and effective time, is:

`http://snomed.info/sct/{sctid}/version/{timestamp}`

***

<a href="https://docs.google.com/forms/d/e/1FAIpQLScTmbZIf0UEQwYDkY27EEWBkaiYkHSbR0_9DmFrMLXoQLyL7Q/viewform?usp=pp_url&#x26;entry.1767247133=URI+Standard&#x26;entry.670899847=3%20SNOMED%20CT%20URIs%20in%20Use" class="button primary">Provide Feedback</a>

[^1]: This information is directly discernable from the SCTID itself.

[^2]: See OWL 2 Web Ontology Language Structural Specification and Functional-Style Syntaxhttp://www.w3.org/TR/owl2-syntax/#Ontology\_IRI\_and\_Version\_IRI&#x20;

[^3]: See [http://hl7.org/fhir](http://hl7.org/fhir)
