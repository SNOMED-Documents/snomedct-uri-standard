# SNOMED CT URI Space

* [#uris-for-editions-and-versions](./#uris-for-editions-and-versions "mention")
* [#uris-for-components-and-reference-set-members](./#uris-for-components-and-reference-set-members "mention")
* [2.3 Edition and Version-Relative Component URIs](../2%20snomed-ct-uri-space/2.3-Edition-and-Version-Relative-Component-URIs_29951166.html)
* [2.4 URIs for Modules](../2%20snomed-ct-uri-space/2.4-URIs-for-Modules_29951167.html)
* [2.6 URIs for Properties](../2%20snomed-ct-uri-space/2.6-URIs-for-Properties_29951168.html)
* [2.7 URIs for SNOMED Resources](../2%20snomed-ct-uri-space/2.7-URIs-for-SNOMED-Resources_106700321.html)
* [2.7 Comparing URIs for Equality of Reference](../2%20snomed-ct-uri-space/2.7-Comparing-URIs-for-Equality-of-Reference_29951169.html)
* [2.8 URIs for Unpublished Content](../2%20snomed-ct-uri-space/2.8-URIs-for-Unpublished-Content_134520516.html)

## URIs for Editions and Versions

### Background

A SNOMED CT edition logically consists of the complete set of members of one or more modules.[1](https://confluence.ihtsdotools.org/display/DOCURI/2.1+URIs+for+Editions+and+Versions#Footnote1) Since the [module dependency reference set](https://confluence.ihtsdotools.org/display/WIPRELFMT/5.2.4.2+Module+Dependency+Reference+Set) (MDRS) tracks the explicit dependencies between a version of a module and all the versioned modules it depends on, a module identifier[2](https://confluence.ihtsdotools.org/display/DOCURI/2.1+URIs+for+Editions+and+Versions#Footnote2) is a natural identifier for an edition. When combined with a timestamp corresponding to a sourceEffectiveTime appearing in the MDRS, the module identifier can unambiguously identify a version of an edition.

### Form

The URIs that identify unversioned editions (i.e. editions) and versioned editions (i.e. versions) take the following respective forms:

`http://snomed.info/sct/{sctid}`

`http://snomed.info/sct/{sctid}/version/{timestamp}`

Note, while it would be possible to extend this pattern to support multiple root modules, each with their own sourceEffectiveTime, this would introduce non-trivial complexities. For example, the modules they each depend upon may themselves overlap but have different versions (targetEffectiveTime) in which case the implied content would be inconsistent.

### Examples

The following table shows some examples of URIs for editions and versions.

Table 2.1-1: Examples

| **Resource**                              | **URI**                                                    |
| ----------------------------------------- | ---------------------------------------------------------- |
| SNOMED CT International Edition           | http://snomed.info/sct/900000000000207008                  |
| SNOMED CT International Edition, 20130731 | http://snomed.info/sct/900000000000207008/version/20130731 |
| SNOMED CT-AU                              | http://snomed.info/sct/32506021000036107                   |
| SNOMED CT-AU, 31 May 2013                 | http://snomed.info/sct/32506021000036107/version/20130531  |
| SNOMED CT-AU, 30 Nov 2012                 | http://snomed.info/sct/32506021000036107/version/20121130  |
| SNOMED CT-SE                              | http://snomed.info/sct/45991000052106                      |

For a more extensive list of SNOMED CT edition URI examples, please refer to [4.4.2 Edition URI Examples](https://confluence.ihtsdotools.org/display/DOCEXTPG/4.4.2+Edition+URI+Examples)

***

| Footnotes Ref                                                                                               | Notes                                                                                                                                                                                                                                   |
| ----------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [1](https://confluence.ihtsdotools.org/display/DOCURI/2.1+URIs+for+Editions+and+Versions#FootnoteMarker1-0) | While there may be additional files associated with a release, it is only the module content which affects the computable meaning of a concept (i.e. the inferable relationships and subsumption between post coordinated expressions). |
| [2](https://confluence.ihtsdotools.org/display/DOCURI/2.1+URIs+for+Editions+and+Versions#FootnoteMarker2-0) | This is the identifier of the module concept, as would be used in the [module dependency reference set](https://confluence.ihtsdotools.org/display/WIPRELFMT/5.2.4.2+Module+Dependency+Reference+Set).                                  |

***

## URIs for Components and Reference Set Members

### Background

A SNOMED CT component is a concept, description or relationship that conforms with the SNOMED CT logical model. All SNOMED CT components are identified by an SCTID. [1](https://confluence.ihtsdotools.org/display/DOCURI/2.2+URIs+for+Components+and+Reference+Set+Members#Footnote1) .

A SNOMED CT reference set member is a uniquely identified row of a reference set. All reference set members are identified by a UUID (rather than an SCTID).

### Form

URIs for components, based on the corresponding SCTID, take the following form:

`http://snomed.info/id/{sctid}`

URIs for members of a Reference Set, based on the corresponding UUID, take the following form:

`http://snomed.info/id/{uuid}`

For simplicity this document refers to either of the above forms as a _component URI_.

### Examples

The following table shows some examples of URIs for components and reference set members.

Table 2.2-1: Examples

| **Resource**                                                                                          | **URI**                                                                                                                  |
| ----------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| The concept \[ 74400008                                                                               | Appendicitis                                                                                                             |
| The description "Appendicitis" with id=123558018                                                      | [http://snomed.info/id/123558018](http://snomed.info/id/123558018)                                                       |
| The relationship \[ 74400008                                                                          | Appendicitis                                                                                                             |
| The reference set member that defines "Appendicitis" as preferred in the en-US language reference set | [http://snomed.info/id/7c0d7d61-c571-5bf9-9329-fdbfee8747d0](http://snomed.info/id/7c0d7d61-c571-5bf9-9329-fdbfee8747d0) |

| Footnotes Ref                                                                                                              | Notes                                                                                                                                    |
| -------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| [1](https://confluence.ihtsdotools.org/display/DOCURI/2.2+URIs+for+Components+and+Reference+Set+Members#FootnoteMarker1-0) | [3.1.4.2. Component features - Identifiers](https://confluence.ihtsdotools.org/display/WIPTIG/3.1.4.2.+Component+features+-+Identifiers) |

<a href="https://docs.google.com/forms/d/e/1FAIpQLScTmbZIf0UEQwYDkY27EEWBkaiYkHSbR0_9DmFrMLXoQLyL7Q/viewform?usp=pp_url&#x26;entry.1767247133=URI+Standard&#x26;entry.670899847=2%20SNOMED%20CT%20URI%20Space" class="button primary">Provide Feedback</a>
