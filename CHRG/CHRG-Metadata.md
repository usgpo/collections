# Congressional Hearings (CHRG) Metadata Fields
The below is a listing of metadata fields available through FDsys MODS files for the Congressional Hearings Collection. 

## Package Metadata

| **Entity** | **Description or Constant Value** | **Source** | **Arity** |
| --- | --- | --- | --- |
| Generic Metadata Fields |
| collectionCode | `CHRG` | constant | 1 |
| scope | `fdlp` | constant | 1 |
| governmentAuthor1 | `Congress` | constant | 1 |
| governmentAuthor2 | The chamber responsible for the hearing, or <blank> if both chambers are responsible (i.e. a joint hearing) | parser | 0-1 |
| starprintNumber | Star print number, where available | parser | 0-1 |
| category | `Congressional Committee Materials` | constant | 1 |
| title | Full official title of the hearing. | parser | 1 |
| title/@info | `from-parsing` | parser | 1 |
| subtitle | `<blank>` Manually populated if necessary. | manual | 1 |
| subtitle/@info | `<blank>` Manually populated if necessary. | manual | 1 |
| sourceContentType | `deposited` | constant | 1 |
| packageDigitalOrigin | `born digital` | constant | 1 |
| branch | `legislative` | constant | 1 |
| typeOfResource | `text` | constant | 1 |
| genre | `<genre authority="marcgt">government publication<genre>` | constant | 1 |
| dateIssued |  This is the date when the hearing was held. | parser | 1 |
| dateIngested | Date ingested into FDsys preservation repository. | submission | 1 |
| issuance | `monographic` | constant | 1 |
| language | `eng` | constant | 1 |
| classification | With `@authority="sudocs"`. This is the number is assigned to the hearing by the office of the Superintendent of Documents (SuDoc) of the Government Publishing Office. It is a function of the committee that held the hearing. | parser | 1-n |
| otherIdentifier/[@idStandard="migrated-doc-id"]| The file name of the text file prefixed with `f:`. For example `f:54564.done`. | parser | 1 |
| waisDatabaseName | Examples: `1998\_happ\_tre\_5`,`109\_senate\_hearings` For data migrated from GPO Access. | parser | 0-1 |
| recordSource | `DGPO` | constant | 1 |
| recordCreationDate | Date that the mods.xml is created. | processing | 1 |
| recordChangeDate | Date that the mods.xml is modified. | processing | 1 |
| recordOrigin | `machine generated` | constant | 1 |
| publisher | `U.S. Government Publishing Office` | constant | 1 |
| pageCount | The total page count of the PDF rendition of the hearing. | processing | 1 |
| Collection-Specific Metadata Fields |
| docClass | `HHRG`, `SHRG`, or `JHRG` | parser | 1 |
| accessId | The access identifier for this package, used to uniquely identify this package to the public. Examples:CHRG-110hhrg32001 CHRG-110jhrg32002CHRG-110shrg23001-pt1CHRG-110hhrg32001-vol3CHRG-110hhrg23001-err | parser | 1 |
| type | This is the type of hearing. Available values are: <br>`F`: Field</li><br/><li>`M`: Markup</li><br/><li>`O`: Oversight</li><br/><li>`AU`: Authorization</li><br/><li>`AP`: Appropriation</li><br/><li>`N`: Nomination</li><br/><li>`T`: Treaty</li><br/><li>`G`: General </li></ul> | parser | 1 |
| chamber | Chamber of the hearing's committee. Allowed values are `HOUSE` for House of Representatives, `SENATE` for Senate or `JOINT` for Joint. The fallback value is `JOINT`. | parser | 1 |
| congress | The congress number of the hearing (integer). | parser | 1 |
| session | The session number of the hearing (integer). | parser | 1 |
| number | The hearing number is an integer value for the Senate and could be an alphanumeric value for the House.Example:  S. Hrg. 108-801 | parser | 0-n |
| heldDate | The date value in normalized format YYYY-MM-DD | parser | 0-n |

## Granule Metadata

| **Entity** | **Description or Constant Value** | **Source** | **Arity** |
| --- | --- | --- | --- |
| Generic Metadata Fields  |
| title | The title of the document. | parser | 1 |
| migratedDocId | otherIdentifier/[@idStandard="migrated-doc-id"] | parser | 0-1 |

| **Entity** | **Description or Constant Value** | **Source** | **Arity** |
| --- | --- | --- | --- |
| Granule Collection Specific Metadata |
| granuleClass | One of:  `FIRSTPART`, `OTHERPART`, `ERRATA` | parser | 1 |
| accessId | The access identifier for the granule, used to uniquely identify this granule to the public. | parser | 1 |
| agency | Not all hearings will have this element. Appropriation hearings will have it. (Parent tag) | parser | 0-n |
| agency/name | The name of the agency. | parser | 1 |
| agency/subagency | Reference to a sub agency. | manual | 0-n |
| heading | The textual heading for this segment/portion of the hearing. For example `Part 2`, `Errata`, `Volume III` or even `Volume III, Part 1a`. | parser | 0-1 |
| partNumber | Indicates the segment/portion of the hearing to which the printed material refers. (string), could be `1a`, `1b`, etc. | parser | 0-1 |
| volumeNumber | Indicates the segment/portion of the hearing to which the printed material refers. (integer), could be 1, 2, etc. | parser | 0-1 |
| errataNumber | The number of the errata, or `1` if no errata number is specified. (integer) | parser | 0-1 |
| fiscalyear | This applies to an appropriation hearing for a fiscal year. This value is required if the hearing is an appropriation. Format is YYYY. | parser | 0-1 |
| errata | Errata information on the body of the hearing. The body of this metadata field can be empty since the hearing can be marked with errata but no actual errata text is associated. Otherwise, the parent tag contains the errata text. Hearings without errata data will not have this metadata field. | parser | 0-1 |
| errata/@marked | It is always set to `true` if there is an errata. | constant | 1 |
| nominee | Nominee mentioned on the hearing (parent tag). _Note: Not all hearings have nominees listed._ | parser | 0-n |
| nominee/name | Name of the nominee. | parser | 1 |
| nominee/@state | Two letter abbreviation of the state that the nominee represents (available only for Congress members). | parser | 0-1 |
| nominee/position | The position and organization to which the nominee is being nominated. | parser | 0-1 |
| witness | A witness on the hearing. Not all hearings have witnesses, but if they do, they are usually found on the second page. May also contain the witness' title and associated organization. | parser | 0-n |
| isAppropriation | Indicates the hearing is an appropriation (Boolean).  Must always be true or false (i.e. cannot be missing). | parser | 1 |
| congSerial | A reference to a congressional serial number. (parent tag only)_  Note: These numbers will be extracted only from the cover of the hearing; excluding the body._ | parser | 0-n |
| congSerial/@chamber | Either `H`, `S` or `J`.Note: The type is copied from chamber. | parser | 1 |
| congSerial/@congress | The congress number. (integer) | parser | 1 |
| congSerial/@number | The serial number or letter. | parser | 1 |
| congSerial/@prefix | Optional prefix that can indicate the committee's scope. | parser | 0-1 |
| congSerial/@detail | Additional character that can be used to indicate the alpha component (as a suffix) in the scenario of an alphanumeric value. | parser | 0-1 |
| jacketId | The jacket number, typically a number in the format `41-839`.  _These numbers will be extracted only from the cover of the hearing; excluding the body._ | parser | 1 |
| otherHostingOrg | If not hosted by a committee, then the name of the hosting organization (for example: `Executive Commission on China`) will be stored here. | parser | 0-1 |
| congHASC | House Armed Services Committee Number (parent tag only) | parser | 0-1 |
| congHASC/@congress | Congress number associated to the reference. | parser | 1 |
| congHASC/@number | Number associated to the reference. | parser | 1 |
| congCommittee | A reference to a Congressional committee. (parent tag only) | parser | 0-n |
| congCommittee/@chamber | The chamber to which the committee belongs, either `H`, `S`, or `J`. | parser | 1 |
| congCommittee/@congress | The number of the congress to which this committee reference belongs. | parser | 1 |
| congCommittee/@authorityId | The authority ID of the Congressional committee from authority file. | authority | 0-1 |
| congCommittee/@type | The committee type from authority file, one of `J`, `L`, `O`, `P`, `S`, `T`.  <br/>S=Standing;<br/> L=seLect;<br/>P=sPecial;<br/>J=Joint;<br/>  T=Task force;<br/>O=Other. | authority | 0-1 |
| congCommittee/name | Name of the committee. | parser | 1-n |
| congCommittee/name/@type | Type of name, either `parsed` or `authority-short`. | parser | 1 |
| congCommittee/subCommittee | A reference to a Congressional subcommittee on the hearing's cover. (parent tag only) | parser | 0-n |
| congCommittee/subCommittee/name | The name of the subcommittee. | parser | 1 |
| congCommittee/subCommittee/name/@type | `parsed` | parser | 1 |
| congMember | A reference to a member of congress. (parent tag only) | parser | 0-1 |
| congMember/@chamber | The chamber to which the Congress member belongs at the time the reference was made, either `H` or `S` | parser | 1 |
| congMember/@congress | The Congress number to which this congress member belongs. | parser | 0-1 |
| congMember/@role | The role of the Congress member at the point of the reference. The only allowed value for hearings is `COMMMEMBER` for committee member. | parser | 0-1 |
| congMember/@party | The party affiliation of the Congress member at the time of the reference. One of `D`, `R`, and `I`. | parser | 0-1 |
| congMember/@authorityId | The authority ID of the Congress member from the authority files. | parser | 0-1 |
| congMember/@state | The postal code of the state to which the Congress member belonged at the time of the reference. | parser | 0-1 |
| congMember/@bioGuideId | The BioGuide Id of the Congress member from the authority file.  Example: `L000447`. | parser | 0-1 |
| GCS/congMember/@gpoId | The GPO Id of the Congress member from the authority file.  Example: `5785`. | parser | 0-1 |
| congMember/@houseRefId | The latest House Reference Id of the Congress member from the authority file if available.  Example: `809`. | parser | 0-1 |
| congMember/@chamberIdCode | The latest Chamber Id Code of the Congress member from the authority file if available.  Examples: `HI027701` or `S213`. | parser | 0-1 |
| congMember/name | The Congress member's name. | parser | 1-n |
| congMember/name/@type | The type of name, one of: `parsed`, `authority-fnf` (first-name-first), `authority-lnf` (last-name-first), and `authority-other`.<br/>1. `authority-fnf` will come from `<displayName original="true">`<br/>2. `authority-lnf` will come from `<displayName>` with no original= flag with the latest effective date <br/>3. `authority-other` will come from the authority name pieces, typically just "FirstName LastName" if not already specified.    | parser | 1 |
| **Standard References** |||
| law | A reference to a public or private law. (parent tag only) | parser | 0-n |
| law/@congress | The congress number of the law. (integer) | parser | 1 |
| law/@number | The law number. (without the Congress number) (integer) | parser | 1 |
| law/@isPrivate | Flag indicates the law is private or public. The values are `true` or `false`. | parser | 0-1 |
| USCode | A reference to a section in the United States Code. (parent tag only) | parser | 0-n |
| USCode/@title | The title number of the United States Code being referenced. (integer) For example, the number 10 in "10 U.S.C. 1032" | parser | 1 |
| USCode/section | A United States Code section reference. (parent tag only) | parser | 0-n |
| USCode/section/@number | The number of the United States Code section being referenced. For example, "247b-4a" in "42 U.S.C. 247b-4a". Should be all numbers, letters and dashes in the reference. | parser | 1 |
| USCode/section/@detail | Any section detail which occurs after the first section number. This can include sub-section information or information about a section range. Sample values include "(3)(2)", "note", "et seq." | parser | 0-1 |
| USCode/chapter | References a chapter in the US Code (parent tag only) | parser | 0-n |
| USCode/chapter/@number | The number of the United States Code chapter being referenced as an _Arabic decimal number_. (integer) | parser | 1 |
| USCode/chapter/@detail | Any chapter detail which occurs after the chapter number. | parser | 0-1 |
| USCode/appendix | A reference to an appendix of a title in the U.S. Code.  (parent tag only) | parser | 0-n |
| USCode/appendix/@number | The appendix number of the United States Code referenced. (integer) For example, the number 2078 in "50 U.S.C. App. 2078". | parser | 1 |
| USCode/appendix/@detail | Any appendix detail. May be something like "-1103" to indicate the second half of an appendix number range to be processed in a future release. | parser | 0-1 |
| statuteAtLarge | A reference to a Statute. (parent tag only) | parser | 0-n |
| statuteAtLarge /@volume | The volume number of the Statutes at Large reference; For example, "49" in "49 Stat. 744". | parser | 1 |
| statuteAtLarge/pages | A page or page range. (parent tag only) | parser | 1-n |
| statuteAtLarge/pages/@pages | The page number(s) of a Statute reference; for example, "744" for "49 Stat. 744". The page number can be an integer or a range separated by a dash. This attribute holds the entire page text, for example "13892", "5009-132", or "6320-6540". | parser | 1 |
| bill | A reference to a Congressional bill. (parent tag only) | parser | 0-n |
| bill/@congress | The Congress number which produced the bill. (integer) | parser | 1 |
| bill/@type | The type of bill. One of `HR`, `S`, `HRES`, `SRES`, `HJRES`, `SJRES`, `HCONRES`, or `SCONRES`. | parser | 1 |
| bill/@number | The bill number. (integer) | parser | 1 |
| bill/@context | In case the document is an appropriation hearing (isAppropriation is "true"), all references from the cover must be distinguished from the body of the hearing. Values will be "COVER" or "BODY". | parser | 0-1 |
| congReport | A reference to a Congressional Report (parent tag only) | parser | 0-n |
| congReport/@congress | The Congress number which produced the report. (integer) | parser | 1 |
| congReport/@number | The report number. (integer) | parser | 1 |
| congReport/@type | The type code for the report, one of 'H', 'S', 'CONF', 'H CONF', 'EXEC'. | parser | 1 |
| congReport/@detail | Any detailed reference information, such as "Part I" or "Parts I through IV". | parser | 0-1 |
| congDoc | A reference to a Congressional Document. (parent tag only) | parser | 0-n |
| congDoc/@congress | The Congress number of the Congress who produced the document. (integer) | parser | 1 |
| congDoc/@number | The document number. (integer) | parser | 1 |
| congDoc/@type | The type of Congressional document, one of `H`, `S`, or `STREATY`. | parser | 1 |
| congHearing | A reference to a Congressional hearing (parent tag only).  Note: These references should only be extracted from body of the hearing. | parser | 0-n |
| congHearing/@congress | The number of the Congress which held the hearing. (integer) | parser | 1 |
| congHearing/@type | The type of hearing, `H` or `S`. | parser | 1 |
| congHearing/@number | The hearing number (integer). | parser | 1 |
| congCommPrint | A reference to a Congressional committee print (parent tag only) | parser | 0-n |
| congCommPrint/@type | Either `H` or `S`. | parser | 1 |
| congCommPrint/@number | The committee print number. (integer) | parser | 1 |
| congCommPrint/@congress | The number of the Congress which requested the committee print. (integer) | parser | 1 |
| cfr | Holds all of the part and chapter references for the CFR. (parent tag only) | parser | 0-n |
| cfr/@title | Holds the title number for the CFR. (integer) | parser | 1 |
| cfr/part | A reference to a CFR part. (parent tag only) | parser | 0-n |
| cfr/part/@number | Holds part number for the CFR. (integer) | parser | 1 |
| cfr/part/@detail | Holds other reference information below the part number. (sub-sections and paragraphs within the part) | parser | 0-1 |
| cfr/chapter | A reference to a CFR chapter. (parent tag only) | parser | 0-n |
| cfr/chapter/@number | Holds the chapter number for the CFR (_as a decimal Arabic number_). (integer) | parser | 1 |
| cfr/chapter/@detail | Holds detailed chapter information for the CFR. | parser | 0-1 |



# CHRG MODS Metadata

## CHRG MODS.xml Components

### Component 1:  Metadata elements independent of package or granule

| **MODS Schema Entry** | **MODS entity attributes** | **Entity(ies) & Special Instructions** |
| --- | --- | --- |
| name\* | `type="corporate"` | `<namePart>United States Government Publishing Office</namePart>` <br> `<role>`<br/>```  <roleTerm authority="marcrelator" type="text">publisher</roleTerm>```<br/>```    <roleTerm authority="marcrelator" type="code">pbl</roleTerm>```<br/>`</role>`<br/>`<role>`<br/>```    <roleTerm authority="marcrelator" type="text">distributor</roleTerm>```<br/>```    <roleTerm authority="marcrelator" type="code">dst</roleTerm>```<br/>`</role>`|
| name\* | type="corporate" | `<namePart>United States</namePart>`<br>`<namePart>governmentAuthor1</namePart>`<br/>`<namePart>governmentAuthor2</namePart>`<br/>`<role>`<br/>`<roleTerm authority="marcrelator" type="text">author</roleTerm>`<br/>```    <roleTerm authority="marcrelator"  type="code">aut</roleTerm>```<br/>`</role>`<br/>`<description>Government Organization</description>` |
| typeOfResource\* |   | typeOfResource |
| genre\* |   | genre |
| language/languageTerm\* | type="code" authority="iso639-2b" | language |
| extension/collectionCode\* |   | collectionCode<br/>_Note:  These `<extension>` elements can be in a separate `<extension>` tags or merged with the top-level `<mods>/<extension>` tag._ |
| extension/category\* |   | category |
| extension/waisDatabaseName\* |   | waisDatabaseName |
| extension/branch\* |   | branch |
| extension/dateIngested\* |   | dateIngested |
| extension/starprintNumber |   | starprintNumber |
 
### Component 2:  Metadata elements only for the issue (or package) as a whole 
| **MODS Schema Entry** | **MODS entity attributes** | **Entity(ies) &amp; Special Instructions** |
| --- | --- | --- |
| titleInfo/title | | title |
| titleInfo/title | type="alternative" | title-fallback<br/> 1.When chamber is "S",<br/>title-fallback = congress S. Hrg. number<br/><br/>2.When chamber is "H",<br/>title-fallback = House Hearing, congress Congress<br/><br/>1. 3.When chamber is "J",<br/>title-fallback = Joint Hearing, congress Congress |
| originInfo/publisher\* |   | publisher |
| originInfo/dateIssued\* | encoding="w3cdtf" | dateIssued |
| originInfo/issuance\* |   | issuance |
| originInfo/frequency\* | authority="marcfrequency" | frequency |
| physicalDescription/note\* | type="source content type" | sourceContentType |
| physicalDescription/digitalOrigin\* |   | packageDigitalOrigin |
| physicalDescription/extent\* |   | pageCount p. |
| classification\* |   | classification |
| identifier\* | type="uri" | http://www.gpo.gov/fdsys/pkg/accessId |
| Identifier\* | type="local" | AIP PackageID if is available, otherwise Package Header ID. |
| identifier\* | type="former package identifier" | otherIdentifier[@idStandard='migrated-doc-id'] |
| location/url\* | displayLabel="Content Detail" access="object in context" | http://www.gpo.gov/fdsys/pkg/accessId/content-detail.html |
| location/url\* | displayLabel="PDF rendition" access="raw object" | http://www.gpo.gov/fdsys/pkg/accessId/pdf/accessId.pdf |
| location/url\* | displayLabel="HTML rendition" access="raw object" | http://www.gpo.gov/fdsys/pkg/accessId/html/accessId.html |
| recordInfo/recordContentSource\* | authority="marcorg" | recordSource |
| recordInfo/recordCreationDate\* | encoding="w3cdtf" | recordCreationDate |
| recordInfo/recordChangeDate\* | encoding="w3cdtf" | recordChangeDate |
| recordInfo/recordIdentifier\* | source="recordSource" | accessId |
| recordInfo/recordOrigin\* |   | recordOrigin |
| recordInfo/languageOfCataloging/languageTerm\* | type="code" authority="iso639-2b" | language |
| extension\* |   | \* |

### Component 3:  Granule metadata _only for granules inside of multi-part packages_ 
| **MODS Schema Entry** | **MODS entity attributes** | **Entity(ies) & Special Instructions** |
| --- | --- | --- |
| titleInfo/title |   | title |
| titleInfo/partName |   | heading |
| relatedItem | type="otherFormat" xlink:href= "http://www.gpo.gov/fdsys/pkg/accessId/pdf/accessId.pdf" | @id |
| relatedItem/identifier | type="FDsys Unique ID" | digitalObject/@id |
| identifier | type="uri" | http://www.gpo.gov/fdsys/granule/accessId/accessId |
| identifier | type="former granule identifier" | migratedDocId |
| location/url | displayLabel="Content Detail" access="object in context" | http://www.gpo.gov/fdsys/granule/accessId/accessId/content-detail.html |
| location/url | displayLabel="PDF rendition" access="raw object" | http://www.gpo.gov/fdsys/pkg/accessId/pdf/accessId.pdf |
| location/url | displayLabel="HTML rendition" access="raw object" | http://www.gpo.gov/fdsys/pkg/accessId/html/accessId.html |
| identifier | type="preferred citation" | S. Hrg. congress-number,heading_Note:  This should only be included if docClass = SHRG _ |

###Component 4:  Granule Metadata, _for all types of packages_ (single or multi-part)

| **MODS Schema Entry** | **MODS entity attributes** | **Entity(ies) &** **Special Instructions** |
| --- | --- | --- |
| extension/searchTitle |   | title |
| extension\* |   | \* |
| extension/isNomination |   | If there is one or more nominee elements set this value to "true"; otherwise set value to "false". |
| extension/isErrata |   | If there is an errata element set this value to "true"; otherwise set value to "false". |
| name | type="corporate" | ```<namePart>United States</namePart>```<br/>```<namePart>Congress</namePart>```<br/>```<namePart>congCommittee/@chamber</namePart>```<br/>```<namePart>congCommittee/name</namePart>```<br/>```<namePart>congCommittee/subCommittee/name</namePart>```<br/>```<role>```<br/>```    <roleTerm authority= "marcrelator" type="text">associated name</roleTerm>```<br/>```   <roleTerm authority= "marcrelator" type="code">asn</roleTerm>```<br/>`</role>`<br/>```<description>Government Organization</description>```<br/>_Notes: _<br/>1._Use the [@type='authority-standard'] version of congCommittee/name, if it exists. Otherwise use the [@type='parsed'] version.<br/>2._There are multiple congCommittee_/_subCommittee/name instances; generate a "name" element per instance._<br/>3._Use full name value of congCommittee/@chamber.|
| name | type="corporate" | `<namePart>otherHostingOrg</namePart>`<br/>`<affiliation>congCommittee/@chamber</affiliation>`<br/>`<role>`<br/>```    <roleTerm type="text">referenced by</roleTerm>```<br/>`</role>`<br/>```<description>United States Congressional Organization</description>``` |
| name | type="personal" | `<namePart>congMember/name</namePart>`<br/>`<affiliation>congMember/@chamber </affiliation>`<br/>`<role>`<br/>`    <roleTerm type="text">committee member</roleTerm>`<br/>`</role>`<br/>`<description>United States Congressional Member</description>`<br/>_Notes: <br/>- When available, use the [@type='authority-fnf'] version of congMember/name, otherwise use the [@type='parsed'] version._<br/>- _Generate a separate "name" element for each congMember/name instance._ |
| name | `type="personal"` | ```<namePart>witness</namePart>```<br/>`<role>`<br/>```    <roleTerm authority="marcrelator" type="text">witness</roleTerm>```<br/>```<roleTerm authority="marcrelator" type="code">wit</roleTerm>```<br/>```</role><description>Hearing Witness</description>```<br/>_Note: Generate a separate "name" element for each witness instance._ |
| name | `type="personal"` | ```<namePart>nominee</namePart>```<br/>`<role>`<br/>```<roleTerm type="text">nominee</roleTerm>```<br/>```</role><description>Hearing Nominee</description>```<br/>_Note: Generate a separate "name" element for each nominee instance._ |

**Reference to Jacket Number**

| **MODS Schema Entry** | **MODS entity attributes** | **Entity(ies) &** **Special Instructions** |
| --- | --- | --- |
| relatedItem | `type="isReferencedBy"` |   |
| relatedItem/identifier | `type="Jacket citation"` | congJacket/@number |

**References to H.A.S.C Numbers**

| **MODS Schema Entry** | **MODS entity attributes** | **Entity(ies) &** **Special Instructions** |
| --- | --- | --- |
| relatedItem | `type="isReferencedBy"` |   |
| relatedItem/identifier | `type="HASC citation"` | H.A.S.C No. congHASC/congress-congHASC/number |

## CHRG Standard Reference MODS.xml Components

### Public and Private Laws
_References to the Public and Private Laws_

| MODS Schema Entry | MODS Entity Attributes | Entity(ies) & Special Instructions |
| --- | --- | --- |
| relatedItem/titleInfo/title |   | `United States Public Law law/@congress-law/@number`<br/> or <br/>`United States Private Law law/@congress-law/@number` <br/>_depending on if `isPrivate` is true or not._ |
| relatedItem/identifier        | `type="public law citation"` | Public Law law/@congress-law/@number<br/><br/>_Note:  Multiple law references will result in multiple <identifier> tags_ |
| relatedItem/identifier        | `type="private law citation"` | Private Law law/@congress-law/@number<br/><br/>_Note 1:  Multiple law references will result in multiple <identifier> tags<br/><br/>Note 2:  Use this version if isPrivate is true_ |

### United States Code
_References to the United States Code_

| MODS Schema Entry | MODS Entity Attributes | Entity(ies) & Special Instructions |
| --- | --- | --- |
| relatedItem/titleInfo/title |   | "United States Code" |
| relatedItem/titleInfo/partNumber |   | Title USCode/@title Section USCode/section/@numberUSCode/section/@detail<br/><br/>_Note:  Include multiple <partNumber> tags, one for each U.S.C. section_ |
| relatedItem/titleInfo/partNumber |   | Title USCode/@title Chapter USCode/chapter/@numberUSCode/chapter/@detail<br/><br/>_Note:  Include multiple <partNumber> tags, one for each U.S.C. chapter_ |
| relatedItem/titleInfo/partNumber |   | Title USCode/@title Appendix USCode/appendix/@number<br/><br/>_Note:  Include multiple <partNumber> tags, one for each U.S.C. appendix_ |
| relatedItem/identifier        | `type="USC citation"` | USCode/@title U.S.C. USCode/section/@numberUSCode/section/@detail<br/><br/>_Note:  Multiple titles or sections will result in multiple <identifier> tags_ |
| relatedItem/identifier        | `type="USC citation"` | USCode/@title U.S.C. Chapter USCode/chapter/@numberUSCode/chapter/@detail<br/><br/>_Note:  Multiple titles or chapters will result in multiple <identifier> tags_ |
| relatedItem/identifier        | `type="USC citation"` | USCode/@title U.S.C. App. USCode/appendix/@number<br/><br/>_Note 1:  Multiple titles or appendix entries will result in multiple <identifier> tags_ |

### Statutes At Large
_References to the Statutes At Large_

| MODS Schema Entry | MODS Entity Attributes | Entity(ies) & Special Instructions |
| --- | --- | --- |
| relatedItem/titleInfo/title |   | "United States Statutes At Large" |
| relatedItem/titleInfo/partNumber |   | Volume statuteAtLarge /@volume Page  statuteAtLarge/pages/@pages<br/><br/>_Note:  Include multiple <partNumber> tags, one for each Statute at Large <pages> element_ |
| relatedItem/identifier        | `type="Statute citation"` | statuteAtLarge/@volume Stat. statuteAtLarge/pages/@pages<br/><br/>_Note:  Multiple statuteAtLarge references will result in multiple <identifier> tags_ |

### Congressional Bills
_References to the Congressional Bills_

| MODS Schema Entry | MODS Entity Attributes | Entity(ies) & Special Instructions |
| --- | --- | --- |
| relatedItem | `type="isReferencedBy"` |   |
| relatedItem/titleInfo/title |   | "United States bill/@type bill/@number (bill/@congress suffix Congress)"<br/>_Where:_<br/>- _@type is converted to the full user-friendly name for the bill _<br/>- _The suffix is any of "th", "nd", "rd", or "st" depending on the congress number._ |
| relatedItem/identifier        | `type="congressional bill citation"` | bill/@type bill/@number<br/>_Where:_<br/>- _bill/@type is converted to the abbreviated user-friendly name for the bill._|
| extension/congress |   | bill/@congress |
| extension/context |   | bill/@context |

### Congressional Reports
_References to the Congressional Reports_

| MODS Schema Entry | MODS Entity Attributes | Entity(ies) & Special Instructions |
| --- | --- | --- |
| relatedItem | `type="isReferencedBy"` |   |
| relatedItem/titleInfo/title |   | "United States Congress, congReport/@type Report congReport/@congress-congReport/@number"<br>_Where:_<br/>- congReport/@type_ is converted to the full user-readable name of the report.<br/> |
| relatedItem/identifier        | `type="congressional report citation"` | congReport/@type congReport/@congress-congReport/@number <br/>_Where:<br/>- congReport/@type is converted to the abbreviated user-readable name for the bill._
 |
| extension/context |   | congReport/@context |

### Congressional Documents
_References to the Congressional Documents_

| MODS Schema Entry | MODS Entity Attributes | Entity(ies) & Special Instructions |
| --- | --- | --- |
| relatedItem | `type="isReferencedBy"` |   |
| relatedItem/titleInfo/title |   | "United States congDoc/@type congDoc/@congress-congDoc/@number"<br/>_Where:_<br/>- _@type is converted to the full user-friendly name for the hearing, for example "House Document", "Senate Document", or "Treaty Document" _<br/>- _The suffix is any of "th", "nd", "rd", or "st" depending on the congress number._|
| relatedItem/identifier        | `type="congressional document citation"` | congDoc/@type congDoc/@congress-congDoc/@number <br/>_Where:_<br/>- bill/@type is converted to the abbreviated user-friendly name, specifically "H. Doc.", "S. Doc.", or "Treaty Doc." |
| extension/context |   | congDoc/@context |

### Congressional Hearings
_References to the Congressional Hearings_

| MODS Schema Entry | MODS Entity Attributes | Entity(ies) & Special Instructions |
| --- | --- | --- |
| relatedItem | `type="isReferencedBy"` |   |
| relatedItem/titleInfo/title |   | "United States congHearing/@type congHearing/@congress-congHearing/@number"<br/><br/>_Where:_<br/>- congHearing/@type is converted to the full user-friendly name for the hearing, for example "House Hearing" or "Senate Hearing".<br/>-_The suffix is any of "th", "nd", "rd", or "st" depending on the congress number.|
| relatedItem/identifier        | `type="congressional hearing citation"` | congHearing/@type congHearing/@congress-congHearing/@number <br/>_Where:_<br/>- _congHearing/@type is converted to the abbreviated user-friendly name, specifically "S. Hrg." or "H. Hrg."|

### Congressional Committee Prints
 _References to the Congressional Committee Prints_ 
 
| MODS Schema Entry | MODS Entity Attributes | Entity(ies) & Special Instructions |
| --- | --- | --- |
| relatedItem | `type="isReferencedBy"` |   |
| relatedItem/identifier | `type="congressional committee print citation"` | When congCommPrint/@type = "H":<br/>H. Prt. congCommPrint/@congress-congCommPrint/@number<br/><br/>&nbsp;&nbsp;&nbsp;&nbsp;Example:  H. Prt. 110-20<br/><br/>When congCommPrint/@type = "S":<br/>S. Prt.congCommPrint/@congress-congCommPrint/@number<br/><br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Example:  S. Prt. 106-289 |

### Congress Members

_Note:  `<name>` tags do not indicate referenced documents, therefore there is no `<relatedItem>` tag._

| MODS Schema Entry | MODS Entity Attributes | Entity(ies) & Special Instructions |
| --- | --- | --- |
| name | type="personal" | ```<namePart>congMember/name[@type='authority-fnf']</namePart><affiliation>FullNameofChamber</affiliation>```<br/>`     <role>`<br/>`    <roleTerm authority="marcrelator" type="text">XXXX</roleTerm>`<br/>`    <roleTerm authority="marcrelator" type="code">XXX</roleTerm>`<br/>`</role><description>United States Congress Member</description>`<br/><br/>_NOTE: 1._If the authority name is not present use ```congMember[@role='XXXXXX']/name[@type='parsed']```_<br/>2._Multiple congress members will create multiple `<name>` tags (very rare, but possible)_<br/>3._FullNameofChamber = 'United States Senate' if the congMember/@chamber is `S`, 'United States House of Representatives' if the congMember/@chamber is `H`
 |

### Congressional Committees

_Note: `<name>` tags do not indicate referenced documents; therefore there is no `<relatedItem>` tag._

| MODS Schema Entry | MODS Entity Attributes | Entity(ies) & Special Instructions |
| --- | --- | --- |
| name | type="corporate" | ```<namePart>United States</namePart>```<br/>```<namePart>Congress</namePart>```<br/>```<namePart>congCommittee/@chamber</namePart>```<br/>```<namePart>congCommittee/name[@type='authority-standard']</namePart>```<br/>`<role>`<br/>```    <roleTerm authority= "marcrelator" type="text">associated name</roleTerm>```<br/>```   <roleTerm authority= "marcrelator" type="code">asn</roleTerm>```<br/>`</role>`<br/>```<description>United States Congressional Committee</description>```<br/><br/>_NOTE: _<br/>   1._If the authority name is not present use _congCommittee_/name[@type='parsed'].<br/>2._Use full name value of congCommittee/@chamber _<br/>3. _If congCommittee/@chamber is unknown, leave blank._
 |

### Code of Federal Regulations
_References to the Code of Federal Regulations_

| MODS Schema Entry | MODS Entity Attributes | Entity(ies) & Special Instructions |
| --- | --- | --- |
| relatedItem | `type="isReferencedBy"` | _Note 1:  This is a nested `<relatedItem>` within the granule's `<relatedItem>`_<br/>_Note 2:  This `<relatedItem>` will likely be expanded once the CFR collection has been further defined (at a minimum, one or two URLs will be included)_ |
| relatedItem/titleInfo/title |   | "Code of Federal Regulations" |
| relatedItem/titleInfo/partNumber |   | Title cfr/@title Part cfr/part/@numbercfr/part/@detail<br/>_Note:  Include multiple `<partNumber>` tags, one for each CFR part_ |
| relatedItem/titleInfo/partNumber |   | Title cfr/@title Chapter cfr/chapter/@numbercfr/part/@detail<br/>_Note:  Include multiple `<partNumber>` tags, one for each CFR chapter_ |
| relatedItem/identifier        | `type="CFR citation"` | cfr/@title CFR Part cfr/part/@numbercfr/part/@detail<br.>_Note:  Multiple titles or parts will result in multiple <identifier> tags_ |
| relatedItem/identifier        | `type="CFR citation"` | cfr/@title CFR Chapter cfr/chapter/@numbercfr/part/@detail <br/>Note 1:  Multiple titles or chapters will result in multiple <identifier> tags<br/>Note 2:  Convert chapter to roman numerals_ |
