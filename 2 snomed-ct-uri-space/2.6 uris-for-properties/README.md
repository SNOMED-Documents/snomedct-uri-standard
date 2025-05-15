# 2.6 URIs for Properties

# Background

There are a number of additional features of SNOMED CT that do not have SCTIDs or UUIDs, but which still need to be identified. URIs are required to identify these additional features to support use cases such as representing SNOMED CT in OWL (e.g. to identify certain annotations) and referring to SNOMED CT properties (e.g. characteristicTypeId) from other standards (e.g. CTS2). To address these requirements we define a general set of URIs identifying the RF2-based properties of components.

# Form

The URI space for these properties follows the pattern:

http://snomed.info/field/{tableName}.{fieldName}

Valid table names include those described as possible values for the content type element in the File Naming Conventions[1](https://confluence.ihtsdotools.org/display/DOCURI/2.6+URIs+for+Properties#Footnote1 "Footnote: Click here to display the footnote") for RF2. Note, these URIs identify the property itself, not the value or values that may be associated with the property.

# Examples

Table 2.6-1: Examples of URIs for SNOMED CT RF2 properties.

**Resource**| **URI**  
---|---  
The definitionSatusId property in the RF2 concept file| <http://snomed.info/field/concept.definitionStatusId>  
The characteristicTypeId property in the RF2 relationship file| <http://snomed.info/field/relationship.characteristicTypeId>  
The referencedComponentId property in a RF2 simple reference set file| <http://snomed.info/field/refset.referencedComponentId>  
The mapTarget property in a RF2 simple map reference set file| <http://snomed.info/field/sRefset.mapTarget>  
  
* * *

Footnotes Ref | Notes  
---|---  
[1](https://confluence.ihtsdotools.org/display/DOCURI/2.6+URIs+for+Properties#FootnoteMarker1-0 "Footnote: Click to return to reference in text") |  Release File Specification - section [3.3.2 Release File Naming Convention](https://confluence.ihtsdotools.org/display/DOCRELFMT/3.3.2+Release+File+Naming+Convention)
