# 2.7 URIs for Language Instances - DO NOT PUBLISH

# Background

When using computable language instances (e.g. SNOMED CT expressions) in electronic health records or other implementations, it may be necessary to identify the literal language string as a URI. This format for SNOMED CT language instances supports these use cases.

# Form

A URI that identifies a literal computable language instance, such as a SNOMED CT expression, expression constraint or template, takes the following form:

[http://snomed.info/{syntaxCode}/{syntaxInstance}](http://snomed.info/%7BsyntaxCode%7D/%7BsyntaxInstance%7D)

To identify a language instance based on a specific version of a language syntax, the following form is used:

[http://snomed.info/{syntaxCode}/syntaxVersion/{syntaxVersionNumber}/{syntaxInstance}](http://snomed.info/%7BsyntaxCode/version/syntaxVersion/syntaxInstance)

To identify a language instance based on a specific SNOMED CT edition or version, the following forms are used:

http://snomed.info/sct/{sctId}/{syntaxCode}/{syntaxInstance[}](http://snomed.info/sct)

[http://snomed.info/sct/{sctId}/version/{timeStamp}/{syntaxCode}/{syntaxInstance}](http://snomed.info/sct/%7BsctId%7D/version/%7BtimeStamp%7D/%7BsyntaxCode%7D/%7BsyntaxInstance%7D)

And to identify a language instance based on a specific SNOMED CT edition or version, **and** a specific version of a language syntax, the following forms are used:

[http://snomed.info/sct/{sctId}/{syntaxCode}/version/{versionNumber}/{syntaxInstance}](http://snomed.info/sct/http://snomed.info/sct/%7BsctId%7D/%7BsyntaxCode%7D/version/%7BversionNumber%7D/%7BsyntaxInstance%7D)

[http://snomed.info/sct/{sctId}/version/{timeStamp}/{syntaxCode}/syntaxVersion/{syntaxVersionNumber}/{syntaxInstance}](http://snomed.info/sct/%7BsctId%7D/version/%7BtimeStamp%7D/%7BsyntaxCode%7D/%7BsyntaxInstance%7D/version/%7BversionNumber%7D/%7BsyntaxInstance%7D)

In each of the forms above, the following replacements must be made:

  * {sctId} is replaced with the identifier of the most dependent module in the relevant SNOMED CT edition,
  * {timeStamp} is replaced with the effectiveTime of the relevant SNOMED CT version,
  * {syntaxCode} is replaced with the codes defined for a [URI for language syntax](2.6-URIs-for-Language-Syntaxes---DO-NOT-PUBLISH_134520518.html) (e.g. scg)
  * {syntaxVersionNumber} is replaced with the version number of the language syntax (e.g. 2.4)
  * {syntaxInstance} is replaced with the specific language string (e.g. an expression).

Please note that URIs using the forms described above identify a literal computable language string. It is therefore possible that two different URIs, which identify _semantically_ equivalent strings, but are not equivalent because they identify different _literal_ strings.

# Percent Encoding

URIs must be converted by the server to replace any unsafe ASCII characters with a "%" followed by the corresponding two hexadecimal digits. This is called [percent encoding](https://tools.ietf.org/html/rfc3986#section-2.1). Due to the special characters that may appear in computable language strings, there are a number of such characters that require percent encoding. These are listed in the table below. For more information please refer to the [Uniform Resource Identifier (URI) Generic Syntax](https://tools.ietf.org/html/rfc3986).

Character| Encoding  
---|---  
SPACE| %20  
!| %21  
"| %22  
#| %23  
$| %24  
%| %25  
&| %26  
'| %27  
(| %28  
)| %29  
*| %2A  
+| %2B  
,| %2C  
/| %2F  
:| %3A  
;| %3B  
<| %3C  
=| %3D  
>| %3E  
?| %3F  
@| %40  
[| %5B  
\| %5C  
]| %5D  
^| %5E  
`| %60  
{| %7B  
|| %7C  
}| %7D  
  
# Examples

The following table shows some examples of URIs for SNOMED CT expressions, constraints and templates. In this table, we include both the human readable and standard ([percent encoded](https://tools.ietf.org/html/rfc3986#section-2.1)) URIs. 

Table 2.7-1: Examples

**Resource**| **URI**  
---|---  
The SNOMED CT Expression  [ 404684003 |Clinical finding|](http://snomed.info/id/404684003 "404684003 | Clinical finding |") : [ 47429007 |Associated with|](http://snomed.info/id/47429007 "47429007 | Associated with |") = [ 267038008 |Edema|](http://snomed.info/id/267038008 "267038008 | Edema |") | Human readable URI

  * [http://snomed.info/scg/404684003|Clinical finding|:47429007|Associated with|=267038008 |Edema|](/pages/createpage.action?spaceKey=DOCURI&title=Clinical+finding&linkCreation=true&fromPageId=134520519)

Standard URI (percent encoded)

  * [http://snomed.info/scg/404684003%7CClinical%20finding%7C%3A47429007%7CAssociated%20with%7C%3D267038008%20%7CEdema%7C](http://snomed.info/scg/404684003%7CClinical%20finding%7C:47429007%7CAssociated%20with%7C=79654002%20%7CEdema%7C)

  
The SNOMED CT Expression Constraint  < [ 404684003 |Clinical finding|](http://snomed.info/id/404684003 "404684003 | Clinical finding |") :< [ 47429007 |Associated with|](http://snomed.info/id/47429007 "47429007 | Associated with |") =< [ 267038008 |Edema|](http://snomed.info/id/267038008 "267038008 | Edema |") | Human readable URI

  * [http://snomed.info/ecl/<404684003 |Clinical finding|:<47429007|Associated with|<267038008|Edema|](/pages/createpage.action?spaceKey=DOCURI&title=Clinical+finding&linkCreation=true&fromPageId=134520519)

Standard URI (percent encoded)

  * [http://snomed.info/ecl/%3C404684003%20%7CClinical%20finding%7C%3A%3C47429007%7CAssociated%20with%7C%3D%3C267038008%7CEdema%7C](http://snomed.info/ecl/%3C404684003%20%7CClinical%20finding%7C:%3C47429007%7CAssociated%20with%7C=%3C79654002%7CEdema%7C)

  
The SNOMED CT Expression Constraint  < [ 404684003 |Clinical finding|](http://snomed.info/id/404684003 "404684003 | Clinical finding |") :< [ 47429007 |Associated with|](http://snomed.info/id/47429007 "47429007 | Associated with |") =< [ 267038008 |Edema|](http://snomed.info/id/267038008 "267038008 | Edema |") using ECL v 2.3| Human readable URI

  * [http://snomed.info/ecl/syntaxVersion/2.3/<404684003 |Clinical finding|:<47429007|Associated with|=<267038008|Edema|](/pages/createpage.action?spaceKey=DOCURI&title=Clinical+finding&linkCreation=true&fromPageId=134520519)

Standard URI (percent encoded)

  * [http://snomed.info/ecl/syntaxVersion/2.3/%3C404684003%20%7CClinical%20finding%7C%3A%3C47429007%7CAssociated%20with%7C%3D%3C267038008%7CEdema%7C](http://snomed.info/ecl/version/2.3/%3C404684003%20%7CClinical%20finding%7C:%3C47429007%7CAssociated%20with%7C=%3C79654002%7CEdema%7C)

  
The SNOMED CT Expression Template  [[+id(< [ 404684003 |Clinical finding|](http://snomed.info/id/404684003 "404684003 | Clinical finding |") )]]: [ 47429007 |Associated with|](http://snomed.info/id/47429007 "47429007 | Associated with |") = [ 267038008 |Edema|](http://snomed.info/id/267038008 "267038008 | Edema |") | Human readable URI

  * [http://snomed.info/etl/[[+id(<404684003|Clinical finding|)]]:47429007|Associated with|=267038008|Edema|](/pages/createpage.action?spaceKey=DOCURI&title=Clinical+finding&linkCreation=true&fromPageId=134520519)

Standard URI (percent encoded)

  * http://snomed.info/etl/%5B%5B%2Bid(%3C404684003%7CClinical%20finding%7C)%5D%5D%3A47429007%7CAssociated%20with%7C%3D267038008%7CEdema%7C  

  
The expression "The expression [ 404684003 |Clinical finding|](http://snomed.info/id/404684003 "404684003 | Clinical finding |") : [ 47429007 |Associated with|](http://snomed.info/id/47429007 "47429007 | Associated with |") = [ 267038008 |Edema|](http://snomed.info/id/267038008 "267038008 | Edema |") using v2.0 of SNOMED CT Compositional Grammar." using v2.0 of SCG| Human readable URI

  * [http://snomed.info/scg/syntaxVersion/2.0/404684003|Clinical finding|:47429007|Associated with|=267038008|Edema|](/pages/createpage.action?spaceKey=DOCURI&title=Clinical+finding&linkCreation=true&fromPageId=134520519)

Standard URI (percent encoded)

  * [http://snomed.info/scg/syntaxVersion/2.0/404684003%7CClinical%20finding%7C%3A47429007%7CAssociated%20with%7C%3D267038008%7CEdema%7C](http://snomed.info/scg/404684003%7CClinical%20finding%7C:47429007%7CAssociated%20with%7C=79654002%7CEdema%7C/syntaxVersion/2.0)

  
The expression [ 404684003 |Clinical finding|](http://snomed.info/id/404684003 "404684003 | Clinical finding |") : [ 47429007 |Associated with|](http://snomed.info/id/47429007 "47429007 | Associated with |") = [ 267038008 |Edema|](http://snomed.info/id/267038008 "267038008 | Edema |") based on the 20180131 international release.| Human readable URI

  * [http://snomed.info/sct/900000000000207008/version/20180131/scg/404684003|Clinical finding|:47429007|Associated with|=267038008|Edema| ](/pages/createpage.action?spaceKey=DOCURI&title=Clinical+finding&linkCreation=true&fromPageId=134520519)

Standard URI (percent encoded)

  * [http://snomed.info/sct/900000000000207008/version/20180131/scg/404684003%7CClinical%20finding%7C%3A47429007%7CAssociated%20with%7C%3D267038008%7CEdema%7C](http://snomed.info/sct/900000000000207008/version/20180131/scg/404684003%7CClinical%20finding%7C:47429007%7CAssociated%20with%7C=79654002%7CEdema%7C)  

  
The expression "The expression constraint < [ 404684003 |Clinical finding|](http://snomed.info/id/404684003 "404684003 | Clinical finding |") :<< [ 47429007 |Associated with|](http://snomed.info/id/47429007 "47429007 | Associated with |") =<< [ 267038008 |Edema|](http://snomed.info/id/267038008 "267038008 | Edema |") based on the 20190731 Australian Edition, using v2.0 of the SNOMED CT Expression Constraint Language." based on the 20160731 international release and using v2.0 of SNOMED CT Compositional Grammar.| Human readable URI

  * [http://snomed.info/sct/32506021000036107/version/20190731/ecl/syntaxVersion/2.0/<404684003|Clinical finding|:<<47429007|Associated with|=<<267038008|Edema|](/pages/createpage.action?spaceKey=DOCURI&title=Clinical+finding&linkCreation=true&fromPageId=134520519)

Standard URI (percent encoded)

  * [http://snomed.info/sct/32506021000036107/version/20190731/ecl/syntaxVersion/2.0/%3C404684003%7CClinical%20finding%7C:%3C%3C47429007%7CAssociated%20with%7C=%3C267038008%7CEdema%7C](http://snomed.info/sct/32506021000036107/version/20190731/ecl/%3C%3C404684003%7CClinical%20finding%7C:%3C%3C47429007%7CAssociated%20with%7C=%3C79654002%7CEdema%7C/syntaxVersion/2.0)  

