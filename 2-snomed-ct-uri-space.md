# SNOMED CT URI Space

* [#uris-for-editions-and-versions](2-snomed-ct-uri-space.md#uris-for-editions-and-versions "mention")
* [#uris-for-components-and-reference-set-members](2-snomed-ct-uri-space.md#uris-for-components-and-reference-set-members "mention")
* [#edition-and-version-relative-component-uris](2-snomed-ct-uri-space.md#edition-and-version-relative-component-uris "mention")
* [#uris-for-modules](2-snomed-ct-uri-space.md#uris-for-modules "mention")
* [#id-2.6urisforproperties-background](2-snomed-ct-uri-space.md#id-2.6urisforproperties-background "mention")
* [#id-2.7urisforsnomedresources-background](2-snomed-ct-uri-space.md#id-2.7urisforsnomedresources-background "mention")
* [#comparing-uris-for-equality-of-reference](2-snomed-ct-uri-space.md#comparing-uris-for-equality-of-reference "mention")
* [#uris-for-unpublished-content](2-snomed-ct-uri-space.md#uris-for-unpublished-content "mention")

## URIs for Editions and Versions

### Background

A SNOMED CT edition logically consists of the complete set of members of one or more module[^1]. Since the module dependency reference set (MDRS) tracks the explicit dependencies between a version of a module and all the versioned modules it depends on, a [module identifier](#user-content-fn-2)[^2] is a natural identifier for an edition. When combined with a timestamp corresponding to a `sourceEffectiveTime` appearing in the MDRS, the module identifier can unambiguously identify a version of an edition.

### Form

The URIs that identify unversioned editions (i.e. editions) and versioned editions (i.e. versions) take the following respective forms:

`http://snomed.info/sct/{sctid}`

`http://snomed.info/sct/{sctid}/version/{timestamp}`

Note that while it would be possible to extend this pattern to support multiple root modules, each with its own `sourceEffectiveTime`, this would introduce non-trivial complexities. For example, the modules they each depend upon may themselves overlap but have different versions (`targetEffectiveTime`) in which case the implied content would be inconsistent.

### Examples

The following table shows some examples of URIs for editions and versions.

**Table 2.1: Examples**

<table data-full-width="false"><thead><tr><th width="169.87890625">Resource</th><th>URI</th></tr></thead><tbody><tr><td>SNOMED CT International Edition</td><td><code>http://snomed.info/sct/900000000000207008</code></td></tr><tr><td>SNOMED CT International Edition, 20130731</td><td><code>http://snomed.info/sct/900000000000207008/version/20130731</code></td></tr><tr><td>SNOMED CT-AU</td><td><code>http://snomed.info/sct/32506021000036107</code></td></tr><tr><td>SNOMED CT-AU, 31 May 2013</td><td><code>http://snomed.info/sct/32506021000036107/version/20130531</code></td></tr><tr><td>SNOMED CT-AU, 30 Nov 2012</td><td><code>http://snomed.info/sct/32506021000036107/version/20121130</code></td></tr><tr><td>SNOMED CT-SE</td><td><code>http://snomed.info/sct/45991000052106</code></td></tr></tbody></table>

For a more extensive list of SNOMED CT edition URI examples, please refer to the [Edition URI Examples](https://app.gitbook.com/s/3RKZIWpWFT0ocCgNT16E/4-logical-design/4.4-editions/4.4.2-edition-uri-examples "mention").

***

## URIs for Components and Reference Set Members

### Background

A SNOMED CT component is a concept, description or relationship that conforms with the SNOMED CT logical model. All SNOMED CT components are identified by an SCTID.

A SNOMED CT reference set member is a uniquely identified row of a reference set. All reference set members are identified by a UUID (rather than an SCTID).

### Form

URIs for components, based on the corresponding SCTID, take the following form:

`http://snomed.info/id/{sctid}`

URIs for members of a Reference Set, based on the corresponding UUID, take the following form:

`http://snomed.info/id/{uuid}`

For simplicity this document refers to either of the above forms as a _component URI_.

### Examples

The following table shows some examples of URIs for components and reference set members.

**Table 2.2: Examples**

| Resource                                                                                                       | URI                                                          |
| -------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------ |
| The concept `74400008 \| Appendicitis\|`                                                                       | `http://snomed.info/id/74400008`                             |
| The description "Appendicitis" with id=123558018                                                               | `http://snomed.info/id/123558018`                            |
| The relationship `74400008 \| Appendicitis\|` `363698007 \| Finding site\|` `66754008 \| Appendix structure\|` | `http://snomed.info/id/859910029`                            |
| The reference set member that defines "Appendicitis" as preferred in the en-US language reference set          | `http://snomed.info/id/7c0d7d61-c571-5bf9-9329-fdbfee8747d0` |

***

## Edition and Version-Relative Component URIs

### Background

Edition and version-relative URIs are useful to identify characteristics of components and reference set members that are specific to an edition or version. Conceptually, they build on the idea of what one resource (e.g. the version) says about another (e.g. a component).

### Form

Edition-relative URIs for components take the following form:

`http://snomed.info/sct/{moduleid}/id/{sctid}`

Version-relative URIs for components take the following form:

`http://snomed.info/sct/{moduleid}/version/{time}/id/{sctid}`

Edition-relative URIs for reference set members take the following form:

`http://snomed.info/sct/{moduleid}/id/{uuid}`

Version-relative URIs for reference set members take the following form:

`http://snomed.info/sct/{moduleid}/version/{time}/id/{uuid}`

### Examples

The following table shows some examples of URIs for components in a specific SNOMED CT versioned edition.

T**able 2.3: Examples**

| Resource                                                                                                                             | URI                                                                                                  |
| ------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------- |
| The concept `74400008 \| Appendicitis\|` in SNOMED CT international edition, 31 January 2013                                         | `http://snomed.info/sct/900000000000207008/version/20130131/id/74400008`                             |
| The concept `2771000032106 \| Open reduction of fracture of ankle (procedure)\|` from the 20160930 Australian edition                | `http://snomed.info/sct/32506021000036107/version/20160930/id/2771000032106`                         |
| The November 30th 2012 version of the Australian '_Emergency department findings in presenting problem reference set'_               | `http://snomed.info/sct/32506021000036107/version/20121130/id/32570501000036104`                     |
| The reference set member that defines "Appendicitis" as preferred in the international en-US language reference set, 31 January 2017 | `http://snomed.info/sct/900000000000207008/version/20170131/id/7c0d7d61-c571-5bf9-9329-fdbfee8747d0` |

***

## URIs for Modules

### Background

The [#uris-for-editions-and-versions](2-snomed-ct-uri-space.md#uris-for-editions-and-versions "mention") section defined URIs for editions and versioned editions. These URIs identify the contents of a Module plus all of the Modules it depends on (based on the module version dependencies). However, it is sometimes necessary to simply identify the contents of a single specified module only.

### Form

URIs for modules come in two forms. To identify the contents of a module, independent of any particular point in time, the following form is used:

`http://snomed.info/module/{sctid}`

To identify the contents of a module at a particular point in time, the following form is used:

`http://snomed.info/module/{sctid}/time/{timestamp}`

Note that the timestamp used above is merely referencing a point in time, and does not need to coincide with a version release date.

### Examples

The following table shows some examples of URIs for modules.

Table 2.4-1: Examples

<table><thead><tr><th width="206.94921875">Resource</th><th>URI</th></tr></thead><tbody><tr><td>The SNOMED International core module</td><td><code>http://snomed.info/module/900000000000207008</code></td></tr><tr><td>The SNOMED International core module at March 15 2017</td><td><code>http://snomed.info/module/900000000000207008/time/20170315</code></td></tr></tbody></table>

***

## URIs for Properties <a href="#id-2.6urisforproperties-background" id="id-2.6urisforproperties-background"></a>

### Background <a href="#id-2.6urisforproperties-background" id="id-2.6urisforproperties-background"></a>

There are a number of additional features of SNOMED CT that do not have SCTIDs or UUIDs, but which still need to be identified. URIs are required to identify these additional features to support use cases such as representing SNOMED CT in OWL (e.g. to identify certain annotations) and referring to SNOMED CT properties (e.g. characteristicTypeId) from other standards (e.g. CTS2). To address these requirements we define a general set of URIs identifying the RF2-based properties of components.

### Form <a href="#id-2.6urisforproperties-form" id="id-2.6urisforproperties-form"></a>

The URI space for these properties follows the pattern:

`http://snomed.info/field/{tableName}.{fieldName}`

Valid table names include those described as possible values for the content type element in the File Naming Conventions for RF2. Note, these URIs identify the property itself, not the value or values that may be associated with the property.

### Examples <a href="#id-2.6urisforproperties-examples" id="id-2.6urisforproperties-examples"></a>

**Table 2.6: Examples of URIs for SNOMED CT RF2 properties.**

<table><thead><tr><th width="289.5625">Resource</th><th>URI</th></tr></thead><tbody><tr><td>The definitionSatusId property in the RF2 concept file</td><td><code>http://snomed.info/field/concept.definitionStatusId</code></td></tr><tr><td>The characteristicTypeId property in the RF2 relationship file</td><td><code>http://snomed.info/field/relationship.characteristicTypeId</code></td></tr><tr><td>The referencedComponentId property in a RF2 simple reference set file</td><td><code>http://snomed.info/field/refset.referencedComponentId</code></td></tr><tr><td>The mapTarget property in a RF2 simple map reference set file</td><td><code>http://snomed.info/field/sRefset.mapTarget</code></td></tr></tbody></table>

***

## URIs for SNOMED Resources <a href="#id-2.7urisforsnomedresources-background" id="id-2.7urisforsnomedresources-background"></a>

### Background <a href="#id-2.7urisforsnomedresources-background" id="id-2.7urisforsnomedresources-background"></a>

SNOMED CT can be combined with complementary eHealth standards to create SNOMED-specific resources. When these resources are owned by SNOMED International, they may require a URI. For example, the [HL7 FHIR Specification](https://www.hl7.org/fhir/) uses URIs for various entities, including FHIR resources, profiles and implementation guides. FHIR profiles, which define recommended SNOMED CT bindings, and FHIR implementation guides, which document best practice for implementing a FHIR system using SNOMED CT, require unique SNOMED CT URIs. Similarly, SNOMED-specific modelling resources using other eHealth standards may also require unique SNOMED CT URIs.

### Form <a href="#id-2.7urisforsnomedresources-form" id="id-2.7urisforsnomedresources-form"></a>

The specific URI format used to identify a SNOMED-specific resource will depend on the requirements of the relevant eHealth standard. However, they will all follow the general format:

`http://snomed.info/{eHealthStandard}/{eHealthStandardSpecificURIFormat}`\\

For example, HL7 FHIR modelling resources will use the format:

`http://snomed.info/fhir/{resourceType}/{resourceName}` \\

with resource types including:

* StructureDefinition
* ImplementationGuide

Other standard-specific formats will be defined as required.

### Examples <a href="#id-2.7urisforsnomedresources-examples" id="id-2.7urisforsnomedresources-examples"></a>

The following table shows some examples of URIs for FHIR modelling resources.

**Table 2.7: Examples**

<table><thead><tr><th width="241.3125">Resource Instance</th><th>URI</th></tr></thead><tbody><tr><td>FHIR Profile</td><td><code>http://snomed.info/fhir/StructureDefinition/condition-with-snomed</code></td></tr><tr><td>FHIR Implementation Guide</td><td><code>http://snomed.info/fhir/ImplementationGuide/snomed-ig</code></td></tr></tbody></table>

***

## Comparing URIs for Equality of Reference

Any two URIs from the `http://snomed.info/` URI space identify the same thing if, after syntax-based normalisation as described in section 6.2.2 of [IETF RFC3986 Uniform Resource Identifier (URI): Generic Syntax](#user-content-fn-3)[^3] , they are equal when treated as character strings. The syntax-based normalisation includes case normalization, percent-encoding normalization, and removal of dot-segments. Scheme-based and protocol-based normalisation should not be required since any URIs that would be affected by them (e.g. by including explicit port numbers or trailing slashes) fall outside of the URI space defined by the standard.

## URIs for Unpublished Content

### Background

The URI formats, defined in the previous sections of this document, can be used to identify SNOMED CT content that has been officially published, and may therefore be stored in an Electronic Health Record and exchanged between clinical systems. However, during the process of creating a SNOMED CT release, concepts may exist in a pre-published state. These concepts are considered to be "work in progress" and subject to change or removal, prior to their official publication. For a variety of reasons (including testing, early adoption etc), users may require a way to identify this [unpublished content](#user-content-fn-4)[^4]. Note that the terminology or code system for SNOMED CT will always be specified as `http://snomed.info/sct`, even when the version of this terminology is unpublished, e.g. `http://snomed.info/xsct/900000000000207008`

SNOMED International already uses the X (eXperimental) indicator for alpha & beta releases of International and national editions of SNOMED CT, eg `xSnomedCT_BelgiumExtensionRF2_PREPRODUCTION_20210315T120000Z/Snapshot/Terminology/xsct2_Concept_Snapshot_BE1000172_20210315.txt`.

This additional 'x' is added to make it clear that the contents have not been "officially" published.

### Form <a href="#id-2.8urisforunpublishedcontent-form" id="id-2.8urisforunpublishedcontent-form"></a>

#### Unpublished Editions and Versions <a href="#id-2.8urisforunpublishedcontent-unpublishededitionsandversions" id="id-2.8urisforunpublishedcontent-unpublishededitionsandversions"></a>

The URIs that identify unpublished editions (i.e. the current build) and unpublished versioned editions (i.e. versions) take the following respective forms:

`http://snomed.info/xsct/{moduleId}`

`http://snomed.info/xsct/{moduleId}/version/{timestamp}`

#### Unpublished SNOMED CT Components <a href="#id-2.8urisforunpublishedcontent-unpublishedsnomedctcomponents" id="id-2.8urisforunpublishedcontent-unpublishedsnomedctcomponents"></a>

The URIs that identify components relative to an unpublished edition or version take the following respective forms:

`http://snomed.info/xsct/{moduleId}/id/{sctId}`

`http://snomed.info/xsct/{moduleId}/version/{timestamp}/id/{sctId}`

### Examples <a href="#id-2.8urisforunpublishedcontent-examples" id="id-2.8urisforunpublishedcontent-examples"></a>

The following table shows some examples of URIs for unpublished artefacts.

**Table 2.8: Examples**

<table><thead><tr><th width="300.51953125">Resource</th><th>URI</th></tr></thead><tbody><tr><td>SNOMED CT International Edition, current build</td><td><code>http://snomed.info/xsct/900000000000207008</code></td></tr><tr><td>SNOMED CT International Edition, 20220131 beta release</td><td><code>http://snomed.info/xsct/900000000000207008/version/20220131</code></td></tr><tr><td>The concept <code>1163215007 | Pressure injury|</code> in the current build of the SNOMED CT International Edition</td><td><code>http://snomed.info/xsct/900000000000207008/id/11632150</code>07</td></tr><tr><td>The concept <code>1163215007 | Pressure injury|</code> in the 20220131 beta release of the SNOMED CT International Edition</td><td><code>http://snomed.info/xsct/900000000000207008/version/20220131/id/1163215007</code></td></tr></tbody></table>

For a more extensive list of SNOMED CT edition URI examples, please refer to [Edition URI Examples](https://app.gitbook.com/s/3RKZIWpWFT0ocCgNT16E/4-logical-design/4.4-editions/4.4.2-edition-uri-examples "mention")

<a href="https://docs.google.com/forms/d/e/1FAIpQLScTmbZIf0UEQwYDkY27EEWBkaiYkHSbR0_9DmFrMLXoQLyL7Q/viewform?usp=pp_url&#x26;entry.1767247133=URI+Standard&#x26;entry.670899847=2%20SNOMED%20CT%20URI%20Space" class="button primary">Provide Feedback</a>

[^1]: While there may be additional files associated with a release, it is only the module content which affects the computable meaning of a concept (i.e. the inferable relationships and subsumption between post-coordinated expressions).

[^2]: This is the identifier of the module concept, as would be used in the module dependency reference set.

[^3]: Uniform Resource Identifier (URI): Generic Syntax [http://tools.ietf.org/html/rfc3986#section-6](http://tools.ietf.org/html/rfc3986#section-6)

[^4]: This topic was first raised in the context using SNOMED with the HL7 FHIR specifications, and further detail on the use case is given here URI Proposal: Addition of xsct. This use case only requires the 'version' format of an unpublished substrate to specify the 'version' of the code system - e.g. [http://snomed.info/xsct/900000000000207008/version/20220131](http://snomed.info/xsct/900000000000207008/version/20220131).
