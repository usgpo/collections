Contents



# Regular Expressions Used on FDsys CHRG Text Files

## Star Print Number
```
STARPRINT_P =

   "(\\s*star print\\s*)|(\\s*<star>\\s*)"

   CASE_INSENSITIVE | MULTILINE

```
## Cover Page
```
COVER_PAGE_P =

   "(U\.S\. GOVERNMENT P(RINT|UBLISH)ING OFFICE\r?\n|House of representatives)"

   CASE_INSENSITIVE | PRESERVE_WHITESPACE

COVER_END_P =

   "\b(?:(?:1st|2n?d)\s+Session\s+|Printed (?:for the use|by authority) of(?:\s+the)?\s+){2}[^\n]+"

   CASE_INSENSITIVE

COVER_END2_P =

   "^\s*U\.S\. GOVERNMENT P(RINT|UBLISH)ING OFFICE\s*$"

   CASE_INSENSITIVE | MULTILINE

COVER_END3_P =

   "\s*Printed (?:for the use|by authority) of"

   CASE_INSENSITIVE

COVER_END4_P =

   "-{8,}\r?\n\s*For sale by the (Superintendent of Documents, )?U\.S\. Government P(rint|ublish)ing Office\r?\n|C O N T E N T S"

   CASE_INSENSITIVE

COVER_END5_P =

   "\r?\n\s*Washington, D\.?C\.\r?\n"

   CASE_INSENSITIVE

COVER_END6_P =

   "\r?\n\d{2}-\d{3}"

   CASE_INSENSITIVE

COVER_END7_P =

   "\r?\n\s*-{5,}"

   CASE_INSENSITIVE

COVER_END8_P =

   "House of representatives"

   CASE_INSENSITIVE

// Finding committee names on the cover page

COMMITTEE_P =

   "(^\s*(?:(?:before (?:the|a))|(?:hearing\s+of the))\r?\n\r?\n?[\W\w]+ (?:CONGRESS|SESSION)\r?\n)"

   CASE_INSENSITIVE | MULTILINE | PRESERVE_WHITESPACE

COMMITTEE2_P =

   "(\s+(?:1st|2n?d)\s+Session(?:\s+})?(?:\s+Printed for the use of the)?\s+(?:Commission|Committee)\s+on\s+[^\n]+)"

   CASE_INSENSITIVE | PRESERVE_WHITESPACE

COMMITTEE3_P =

   "\b(congressional\s*-\s*executive\s+commission\s+on\s+china)\b"

   CASE_INSENSITIVE | PRESERVE_WHITESPACE

COMMITTEE4_P =     // pre-match pattern, match pattern, post-match pattern

   "(CONGRESS\s*\n)|(SESSION\s*\n)", "(subcommittee on.+?)(\n\s*){2,}", null

   CASE_INSENSITIVE | DOT_ALL

```

## Title

```

/**

 * Following expression matches a title followed by a . and finished by a

 * sequence of 2 break lines.

 */

TITLE_P =

   // pre-match, match, and post match expressions

   null, "^\\.\r?\n\\s*(.+)", "[=_-]{2,}|(hearing\\s*\n)"

   MULTILINE | DOTALL

TITLE2_P =

   "^\\.(?:\\s+S\\. +Hrg\\. +\\d+-\\d+)?\r?\n\\s*((?:.+\r?\n)*)"

   MULTILINE


```
## Match the first 200 lines

```

LINES200_P =

   "^(?:[^\n]*\n){200}"

```
## Appropriation Title

```
APPROP_TITLE_P =

   "Appropriation"

   CASE_INSENSITIVE

```
## Appropriation Committee

```
APPROP_CMTE_P =

   "Committee on Appropriations"

   CASE_INSENSITIVE

```
## Type

```
/**

 * Matches following entry:

 * Field Hearing Field Briefing

 * Only "H" character is returned as "type".

 */

TYPE_F_P =

   "\n\\s+(F)ield (?:Hearing|Briefing)\r?\n"

   CASE_INSENSITIVE

/**

 * Used to search in coverPage. Matches the following entries:

 * Hearings and Markup Mark up MarkupMarkups Compilation of Markups

 * Only "M" character is returned as "type."

 */

TYPE_M_P =

   "\n\\s+(?:Hearings and |Compilation of )?(M)ark ?ups?"

   CASE_INSENSITIVE

/**

 * Used to search in title only. Matches the following entries:

 * Mark-up on Markup on Markup of

 * Only "M" character is returned as "type."

 */

TYPE_M2_P =

   "(M)ark-?up (?:on|of)"

   CASE_INSENSITIVE

/**

 * Used to search in coverPage only. Matches the following entries:

 *                 Oversight Hearing

 *                 Oversight Hearings

 *                 Oversight and Legislative Hearing

 *                 Oversight and Legislative Hearings

 *                 Oversight Field Hearing Oversight

 *                 Field Hearings

 * Only "O" character is returned as "type."

 */

TYPE_O_P =

   "\n\\s+(O)versight (?:and Legislative |Field )?Hearings?\r?\n"

   CASE_INSENSITIVE

/**

 * Used to search in title only. Matches the following entries:

 * Oversight Hearing

 * Only "O" character is returned as "type."

 */

TYPE_O2_P =

   "^\\s*(?:Annual\\s+)?(O)versight (?:Hearing|of)"

   CASE_INSENSITIVE

/**

 * Used to search in title only. Matches the following entries:

 *                 Authorization

 *                 Authorization on

 *                 Reauthorization

 *                 Reauthorization on

 * Only "AU" character is returned as "type.

 */

TYPE_AU_P =

   "(?:Re)?(au)thorization(?: on)?"

   CASE_INSENSITIVE

/**

 * Used to search in title only. Matches the following entries:

 *                 Treaty on

 *                 Treaty act

 * Only "T" character is returned as "type.

 */

TYPE_T_P =

   "(T)reaty (?:on|act)"

   CASE_INSENSITIVE

```

## Chamber

```
/**

 * Extracting chamber.

 * Matches following text in one single line:

 * "House of representatives" "U.S. House of representatives"

 */

CHAMBER_HOUSE_P =

   "\\s+(HOUSE)(?: OF REPRESENTATIVES)\\s"

   CASE_INSENSITIVE

/**

 * Extracts chamber.

 * Matches following text in one single line:

 * "United States Senate"

 */

CHAMBER_SENATE_P =

   "\\s+(?:UNITED STATES (SENATE)|U.S. (SENATE))\\s"

   CASE_INSENSITIVE

CHAMBER_SENATE2_P =

   " {3,}S\\. +Hrg\\."

   CASE_INSENSITIVE

/**

 * Extracts chamber.

 * Matches following text in one single line:

 * "JOINT COMMITTEE HEARING" "JOINT HEARING"

 */

CHAMBER_JOINT_P =

   "(JOINT) (?:COMMITTEE )?HEARING"

   CASE_INSENSITIVE

CHAMBER_JOINT_CSCE_P =

   "\\bCSCE\\s+\\d+-\\d+-\\d+\\b"

   CASE_INSENSITIVE

```
## Helper Patterns Embedded In Other Regular Expressions

```
DIGITS_RX = "(?:one|two|three|four|five|six|seven|eight|nine)"

TENS_RX = "(?:twen|thir|for|fif|six|seven|eigh|nine)"

ORDS1_RX = "first|second|third|fourth|fifth|sixth|seventh|eighth|ninth"

ORDS2_RX = "eleventh|twelfth|(?:thir|four|fif|six|seven|eigh|nine)teenth"

ORDS3_RX = "tenth|" + TENS_RX + "(?:tieth|ty-(?:" + ORDS1_RX + "))"


```

## Congress, Hearing Number, Part Number

```
/**

 * Extracts congress and chamber number.

 * Gets the "S. Hrg. #-#." First number is Congress. Second is chamber

 * number.

 */

CONGRESS_P =

   "\\s*(S\\. Hrg\\.) (\\d{3})-(\\d+)(?:, Pa?r?t\\.? ([\\dIVX]+\\w?))?\r?\n"

   CASE_INSENSITIVE

```

## Congress Letters

```
/**

 * Extracts numbers in letters in Congress.

 * Matches following expressions:

 * One hundred first congress Two hundred eleventh congress

 */

CONGRESS_PHRASE_P =

   "^\\s*(" + DIGITS_RX + "\\s+HUNDRED\\s+(?:AND\\s+)?(?:" + ORDS1_RX + "|" + ORDS2_RX + "|" + ORDS3_RX + "))\\s+CONGRESS\\s*$"

   CASE_INSENSITIVE | MULTILINE

```

## Congress Original, Congress

```
CONGRESS_NUMBER_P =

   "\n\\s*(\\d{3})TH CONGRESS\r?\n"

   CASE_INSENSITIVE

```

## Congress, Number, Detail

```
/**

 * Extracts the Congress number and serial number.

 * Matches following expressions:

 * Serial #-# Serial Number #-# Serial No. #-# Serial No. #-#, Part 1

 * First number is the Congress number. Second number is the serial number.

 */

SERIAL_P =

   "\\s*Serial (?:Number |No\\. )?(\\d+)-([\\d\\w]+)(?:, Part (\\d))?"

   CASE_INSENSITIVE

```

## Congress, Number

```
/**

 * Extracts the Congress number serial number.

 * Matches following expressions:

 * #-#

 * (#-#)

 * First number is the Congress number. Second number is the serial number.

 */

SERIAL_CITATION_P =

   "\n\\s*\\(?(\\d{3})-([\\d\\w]+)\\)?\r?\n"

   CASE_INSENSITIVE

```

## Numbers

```

/**

 * Extracts the serial numbers as string. Needs post-process functionality.

 * Matches following expressions:

 * Serial Nos. #-#, #-# Serial Nos. #-#, #-#, and #-#

 * First numbers are the Congress number. Second numbers are the serial

 * number.

 */

SERIALS_P =

   "\n\\s*Serial (?:Numbers |Nos\\. )?(?:(?:and )?\\d+-(\\d+)(?:,\\s*)?)+\r?\n"

   CASE_INSENSITIVE


```

## Hearing Number

```
/*

 * To extract number from S. Hrg. 110-161

 */

HRG_NUM_P =

   "(S\\.\\s*Hrg\\.)\\s*\\d+-(\\d+)"

   CASE_INSENSITIVE

HRG_NUM_JCS_P =

 	"\\b(JCS-)(\\d+-\\d+)\\b"

   CASE_INSENSITIVE

HRG_NUM_CSCE_P =

 	"\\b(CSCE)\\s+(\\d+)-(\\d+-\\d+)\\b"

   CASE_INSENSITIVE

SBC_NUM_P =

 	"Small Business Committee Document Number \\d{3}-(\\d{3})"

   CASE_INSENSITIVE

```

## Volume Number

```
VOLUME_P =

 	"\n\r?\n *Volume ([\\dIV]+)"

   CASE_INSENSITIVE

VOL_NUM_P =

   "S\\.\\s*Hrg\\.\\s*\\d+-\\d+\\.?\\s*Vol(?:ume)?\\.?\\s*([\\dIV]+)"

   CASE_INSENSITIVE


```

## Part Number

```
PART_P =

   "\r?\n\\s*Part (\\d)\\s*\r?\n"

   CASE_INSENSITIVE

PART_NUM_P =

   "S\\.\\s*Hrg\\.\\s*\\d+-\\d+\\.?\\s*P(?:ar)?t\\.?\\s*(\\d)"

   CASE_INSENSITIVE

```
## Session

```
/**

 * Extracts if hearing is First or Second Session.

 * Matches text:

 * First Session

 */

SESSION_P =

   "\n\\s*(FIRST|SECOND) SESSION\r?\n"

   CASE_INSENSITIVE


```
## Held Date

```
// Helper Patterns

MONTHS = "(january|february|march|april|may|june|ju?ly|august|october|(?:septm?|nov|dec)embe?r)"

DAYS = "(?:mon|tues|wednes|thurs|fri|satur|sun)day"

/**

 * Extracts held dates.

 * Matches following expressions:

 * January 23, 2007

 * Monday, MARCH 1, 2003

 */

HELD_DATE_P =

   "(?<!ending\\s)" + MONTHS + "*,?\\s*(\\d{1,2})(?:[,; ]+\\s*)(\\d{4})*"

   CASE_INSENSITIVE

HELD_DATE2_P =

   "\n\\s+(?:" + DAYS + "[, ]+)?(" + MONTHS + ".+\\d{4}\\.?\\s*\n)"

   CASE_INSENSITIVE

HELD_DATE3_P =

   "\n\\s+(?:hearing held[\\w\\s,]*)(?:" + DAYS + "[, ]+)?(" + MONTHS + ".+\\d{4}\\.?\\s*\n)"

   CASE_INSENSITIVE

```
## Date

```
/**

 * Patterns in support of finding normalized parts of held dates

 */

HELD_YEAR_P =

   "(\\d{4})"

   CASE_INSENSITIVE

HELD_MONTH_P =

   MONTHS

   CASE_INSENSITIVE | MULTILINE

HELD_DAY_P = // pre-match, match, and post-match patterns

   null, "\\D(\\d{1,2})\\D", MONTHS

   CASE_INSENSITIVE | MULTILINE


```
## Errata

```
/**

 * Matches following entry:

 * ERRATA This errata sheet is being assigned because the original serial

 * number was incorrect. The correct serial number is 106-57.

 */

ERRATA_P =

   "[^\\.]\r?\n *\\[?errata\\]?\r?\n\\s*([^\\.](?:.+\r?\n)*)"

   CASE_INSENSITIVE | MULTILINE

```

## Errata Number

```
ERR_NUM_SP =

   "\\d+err(\\d*)\\."

   CASE_INSENSITIVE

```

## Table Of Contents

```
CONTENTS_P =

   "\n\\s+C *O *N *T *E *N *T *S\\s*[\n\\s]+\\-*"

   CASE_INSENSITIVE

CONTENTS_END_P =

   "\n\\s+\\-{8,}\\s+(?:\\-{2})?\n"

   CASE_INSENSITIVE

CONTENTS_END2_P =

   "\\.{5,}\\s*\\d+\\s*\n"

   CASE_INSENSITIVE

```

## Detecting no text or no graphics

```
NO_TEXT_P =

 	"(?:\\[|<|\\()(text (file |is |of preliminary )?not available( in (tiff|wais)( format)?| refer to pdf)?)(\\]|>|\\))"

	CASE_INSENSITIVE

NO_TEXT2_P =

 	"(?:\\[|<|\\() ?(text available in pdf format only) ?(?:\\]|>|\\))"

   CASE_INSENSITIVE

NO_TEXT3_P =

 	"\n\\s*(This hearing is only available in PDF format)\\."

   CASE_INSENSITIVE

NO_GRAPHICS_P =

 	"(\\[graphic\\] ?\\[tiff omitted\\])"

   CASE_INSENSITIVE

```

## Agency

```
/**

 * Used to search only in title.

 * Matches the following prefix in the title

 * Department of Departments of

 */

AGENCY_TITLE_P =

   "\\.\r?\n\\s*(Departments? of [^\\W]+)"

   CASE_INSENSITIVE

/**

 * Used to search in the coverPage.

 * Matches following prefix in the coverPage

 * Department of <until new brake line>

 */

AGENCY_COVER_P =

   "\n\\s*(Department of [^\n]+)"

   CASE_INSENSITIVE

```

## Fiscal Year

```
FISCAL_YR_P =   // For obtaining the fiscal year from the title

   "(?:Fiscal\\s+year|Appropriations\\s+for)\\s+(\\d{4})"

   CASE_INSENSITIVE

```

## CongHASC, Congress, Number

```
HASC_P =

   "\\[H\\.A\\.S\\.C\\. No\\. (\\d+)-(\\d+)\\]"

   CASE_INSENSITIVE

```

## State Names Patterns

```
STATES_RX =

   "([Aa](labama|laska|rizona|rkansas)|[Cc](alifornia|olorado|onnecticut)|[Dd]elaware|" +
	"[Dd]istrict\\s+[Oo]f\\s+[Cc]olumbia|[Ff]lorida|[Gg]eorgia|[Hh]awaii|[Ii](daho|llinois|ndiana|owa)|" +
	"[Kk](ansas|entucky)|[Ll]ouisiana|[Tt](ennessee|exas)|[Uu]tah|[Vv]ermont|[Oo](hio|klahoma|regon)|" +
	"[Mm](aine|aryland|assachusetts|ichigan|innesota|ississippi|issouri|ontana)|[Nn](ebraska|evada)|" +
	"[Nn]ew\\s+([Hh]ampshire|[Jj]ersey|[Mm]exico|[Yy]ork)|([Ww]est\\s+)?[Vv]irginia|" +
	"([Nn]or|[Ss]ou)th\\s+([Cc]arolina|[Dd]akota)|[Pp]ennsylvania|[Rr]hode\\s+[Ii]sland|" +
	"[Ww](ashington|isconsin|yoming)|North\\s{2,}|South\\s{2,}|West\\s{2,}|New\\s{2,})"

```

## Congress Member Committee

```
SUFFIX_RX = "|[\\.\\(\\)]| (?! )|, ?(?:[JjSs]r|junior|senior|[Ii]{2,3})"

// original, member name, state

STATE_P =

   "(?:\n|  )([A-Z][a-zA-Z'-]*[A-Z]\\.? (?:\\b[A-Z][a-zA-Z'-]*[A-Z]\\b|\\b[A-Z]\\b" + SUFFIX_RX + ")+),\\s*" + STATES_RX

STATE2_P =

   "(?:\n|  )([A-Z][a-zA-Z'-]*[a-z]\\.? (?:\\b[A-Z][a-zA-Z'-]*[a-z]\\b|\\b[A-Z]\\." + SUFFIX_RX + ")+),\\s*" + STATES_RX

```

## Other Hosting Organization

```
HOST_ORG_P =

   "(?:before +(?:the|a))\\s+(.+?)(?:\\s*" + DIGITS_RX + "\\s+hundred)"

   CASE_INSENSITIVE | DOTALL

HOST_ORG2_P =

   "(CONGRESSIONAL-EXECUTIVE COMMISSION ON\\s*[^\n]+)"

   CASE_INSENSITIVE

```

## Get Day, Month, Year from the file name

```
// extract date and addendum number from filename

FILENAME_DATE = "\\d{2}(ja|fe|mr|ap|my|jn|jy|au|se|oc|no|de)\\d{4}\\."

FILENAME_P =

   "((?:" + FILENAME_DATE + ")?[^\\.]+)(?=\\.)"

   CASE_INSENSITIVE

```

## Addendum

```
ADDENDUM_NUMBER_P =    // from file name

   "add(\\d+)"

   CASE_INSENSITIVE

ADDENDUM_P =           // from file content

 		"addendum\\s+(\\d+)\\s+"

   CASE_INSENSITIVE

ADDENDUM_ID_P

	"\n *(\\d{2}-\\d{3}).*?-{50,}"

   DOTALL

```

## Detect Locator file

```

LOCATOR_P =

   "\\a(I\\d)"

```

## Nominee Information

```
// last name, first name, position

NOMINEE_TOC_P =

   "\n\\s*(\\w[\\w\\- ]+?), +([\\w .]+?), +Nominee (.+?)\\.{5,}\\s*\\d+\\s*\n"

   CASE_INSENSITIVE | DOTALL

NOMINEE_TOC2_P =

   "^\\s*([^\n,]+?)\\s+([\\w'-]+),\\s+of\\s+([\\w\\s'-]+),\\s+(to\\s+be\\s+[^\\.]+)\\.+\\s*\\d+\\s*$"

   CASE_INSENSITIVE | MULTILINE

NOMINEE_TOC3_P =

   "\n *([^,\n]+),\\s+([^,]+),\\s+of\\s+(.*?),\\s+nominated\\s+(to\\s+be\\s+[^.]+)\\.+\\s*\\d*\\s*\n"

   CASE_INSENSITIVE | DOTALL

NOMINEE_TITLE_P =

   "Nomination (?:Hearing\\s+)?of +(.+) +(.+?), +of +(.+), +(to be .+)"

   CASE_INSENSITIVE

NOMINEE_TITLE2_P =

   "Nomination (?:Hearing\\s+)?of (?:\\w{2,4}\\. )?(\\w+ (?:\\w\\.)?) ?(.+?),? (to be .+)"

   CASE_INSENSITIVE

NOMINEE_TITLE3_P =

   "Nomination (?:Hearing\\s+)?of ((?:(?:[\\w'-]+|\\w\\.)\\s*)+)\\s+([\\w'-]+)"

   CASE_INSENSITIVE

```

## Witness

```
WITNESS_TOC_END_P =   // end of witness section

		"\n\\.\\s*\n"

WITNESS_P =

   "\n\\s*((?:Statements? of )?WITNESS(?:ES\\:?)?)\\s*(?:\n[a-zA-Z].+?\\:\\s*)?(?=\n)"

   CASE_INSENSITIVE

WITNESS2_P =   // pre-match, match, and post-match patterns

   null, "\n *(\\w.+?)(?:oral (?:statement|testimony))?\\.*\\s+\\d+(?=\\s*\n)", "((?<=\n)\\s*\n[a-zA-Z][^\n]+?\\:\\s*\n)|((?<=\n)\\s*\n {10,40}[a-zA-Z]+[^\n]*)"

   CASE_INSENSITIVE | DOTALL

WITNESS_DELETE_P

   = "(?<=\n) *(Pa(nel|rt) [IVXCM]+|[_\\-]{3,}|(" + DAYS + ", )?" + MONTHS + " \\d{1,2}, +\\d{4})\\s*\n"

```

## Event ID

```
ADDENDUM_EVENT_ID_P =

 	"EventID\\s+(\\d+).*?-{50,}"

   DOTALL | CASE_INSENSITIVE);

URL_EVENT_ID_P =

   "EventID=(\\d+)"

```

## Committee Name

```
CMTE_P =      // pre-match, match, and post-match patterns

   "(of|and|before) the",
	"(?<=\n)\\s+(((special|select|joint|senate|congressional-executive)\\s+)*(committee|caucus|commission)\\s+on.+)",
	"\n\\s+and (?:the|a)\\s*(?:sub)?committee|(?:U\\.S\\.\\s+)?HOUSE OF REPRESENTATIVES|UNITED STATES (SENATE|CONGRESS)|\\[GRAPHIC\\(S\\)"

   CASE_INSENSITIVE | DOTALL

CMTE2_P =      // pre-match, match, and post-match patterns

   null,
	"\n\\s+(committee\\s+on.+)",
	"\n\\s+and (?:the|a)\\s*(?:sub)committee|(?:U\\.S\\.\\s+)?HOUSE OF REPRESENTATIVES|UNITED STATES (SENATE|CONGRESS)"

   CASE_INSENSITIVE | DOTALL

CMTE3_P =      // pre-match, match, and post-match patterns

   "(of|and|before) the", "(?<=\n)\\s+(joint economic committee)\\s+.+", "\n\\s+and the\\s*committee|UNITED STATES"

   CASE_INSENSITIVE | DOTALL

CMTE4_P =      // pre-match, match, and post-match patterns

   "(1st|2n?d)\\s+Session(\\s+})?(\\s+Printed for the use of the)?", "\\s+((?:Committee|Commission)\\s+on[^\n]+\\s+)", "\n"

   CASE_INSENSITIVE | DOTALL

CMTE5_P =

   "(congressional\\s*-\\s*executive\\s+commission\\s+on\\s+china)"

   CASE_INSENSITIVE

CMTE6_P =      // pre-match, match, and post-match patterns

   null, "\n\\s+(committee\\s+on.+)", "(?:U\\.S\\.\\s+)?HOUSE OF REPRESENTATIVES|UNITED STATES (SENATE|CONGRESS)"

   CASE_INSENSITIVE | DOTALL

```

## Subcommittee

```
SUBCMTE_P =      // pre-match, match, and post-match patterns

   "(before|and|with) the", "(.+?subcommittee.*?)(?:of|and|(?:(?:joint )?with)) the\\s*\n", "\n +committee"

   CASE_INSENSITIVE | DOTALL

```

## JacketId

```
File name matches: "\\d{5}([a-zA-Z]+\\w*)?"

File name matches: "\\d+"

# Standard Reference Regular Expressions Used on FDsys CHRG Text Files

```

## Congressional Committees

```

/** 

 * Chamber

*/

CHAMBER_HOUSE_P =

	"\\s+(HOUSE)(?: OF REPRESENTATIVES)\\s"

   CASE_INSENSITIVE

CHAMBER_SENATE_P =

 	"\\s+(?:UNITED STATES (SENATE)|U.S. (SENATE))\\s"

   CASE_INSENSITIVE

CHAMBER_SENATE2_P =

   " {3,}S\\. +Hrg\\."

   CASE_INSENSITIVE

CHAMBER_JOINT_P =

    "(JOINT) +(SELECT|COMMITTEE|HEARING|ECONOMIC)( +COMMITTEE| +HEARING)?"

   CASE_INSENSITIVE

CHAMBER_JOINT_CSCE_P =

	"\\bCSCE\\s+\\d+-\\d+-\\d+\\b"

   CASE_INSENSITIVE

CHAMBER_FALLBACK_P =

   "(?:(Senate)|(House) of Representatives?)"

   CASE_INSENSITIVE

```

## Congress Members (from foundation CongMemberParser)

```

PREFIXES = "(?<!\\()\\b(ms|mr|miss|mrs)\\b"

PREFIXES_P =

   PREFIXES

   CASE_INSENSITIVE

DEL_PREFIXES_P =

   PREFIXES + "\\.?"

   CASE_INSENSITIVE

SUFFIXES = "\\b(jr|ii|iii|iv|sr|junior|senior)\\b"

SUFFIXES_P =

   DEL_SUFFIXES

   CASE_INSENSITIVE

DEL_SUFFIXES_P =

   ",?\\s*" + SUFFIXES + "\\.?"

   CASE_INSENSITIVE

STATE_CODES =

	"AL|AK|AZ|AR|CA|CO|CT|DE|DC|FL|GA|HI|ID|IL|IN|IA|KS|KY|LA|ME|MD|MA|MI|MN|MS|MO|MT|NE|"
	+ "NV|NH|NJ|NM|NY|NC|ND|OH|OK|OR|PA|RI|SC|SD|TN|TX|UT|VT|VA|WA|WV|WI|WY|AS|GU|PR|VI|MP"

STATE_CODE_P

   "\\(\\s*(" + STATE_CODES + ")"

   CASE_INSENSITIVE

STATE_NAME_P =

   "\\bof\\s+(ALA(BAM|SK)A|ARIZONA|"
	+ "(AR)?KANSAS|CALIFORNIA|COLORADO|CONNECTICUT|DELAWARE|DISTRICT\\s*OF\\s*COLUMBIA|FLORIDA|"
	+ "GEORGIA|HAWAII|IDAHO|ILLINOIS|INDIANA|IOWA|KENTUCKY|LOUISIANA|MAINE|MARYLAND|MASSACHUSETTS|"
	+ "MICHIGAN|MINNESOTA|MISS(ISSIPP|OUR)I|MONTANA|NE(BRASK|VAD)A|(WEST\\s*)?VIRGINIA|"
	+ "NEW\\s*(HAMPSHIRE|JERSEY|MEXICO|YORK)|(NOR|SOU)TH\\s*(CAROLIN|DAKOT)A|OHIO|OKLAHOMA|"
	+ "OREGON|PENNSYLVANIA|RHODE\\s*ISLAND|TENNESSEE|TEXAS|UTAH|VERMONT|WASHINGTON|WISCONSIN|"
	+ "WYOMING|AMERICAN\\s*SAMOA|GUAM|PUERTO\\s*RICO|(VIRGIN|NORTHERN\\s*MARIANA)\\s*ISLANDS)"

DEL_STATE_P =

   "(\\([^\\)]*\\)|\\bof\b.*)"

   CASE_INSENSITIVE

NAME_RX = "[\\p{L}][\\p{L}'\\.-]*"

LNF_NAME_P

	"(" + NAME_RX + ")\\s*,\\s*(" + NAME_RX + "\\b)"

   CASE_INSENSITIVE

FNF_NAME_P =

   "(" + NAME_RX + ")\\s+(?:(?:\"|``|'')?" + NAME_RX + "(?:\"|``|'')?\\s+)*(" + NAME_RX + ")"

   CASE_INSENSITIVE

LAST_NAME_ONLY_P =

   "([\\p{L}][\\p{L}'-]*)"

   CASE_INSENSITIVE

```

## Public Laws (from StandardRefParser)

```
LAW_P =

   "(\\bP(?:ublic|rivate|ub|riv|vt)?\\.*\\s*(?:Law|L|R)\\.*)\\s*(?:No[:.])?\\s*(\\d+)[-\\xAD]+\\s*(\\d+)"

   CASE_INSENSITIVE

MULTI_LAW_P =

   "(\\bP(?:ublic|rivate|ub|riv|vt)\\.?\\s*L(?:aws)?\\.?)\\s*(?:Nos?\\.|Numbers?)?(\\s*\\d+[-\\xAD]+\\s*\\d+(?:\\b\\d+[-\\xAD]+\\s*\\d+|,|and|\\s+)+)"

   CASE_INSENSITIVE

MULTI_LAW_NOS_P =

   "(\\d+)[-\\xAD]*\\s*(\\d+)"

```

## United States Code

```
USC = "U\\.?\\s*S\\.?\\s*C(?:\\.|ode)?\\s*"

USC_LONG = "\\s*UNITED\\s*STATES\\s*CODE"

IRC = "\\b(Internal\\s*Revenue\\s*Code)\\b\\s*";

IRC_ONLY =

   IRC

   CASE_INSENSITIVE

/**
 * Matches the following formats: 42 USC 1526 42 U.S.C. 1526 42 U.S.
 * Code 1526 42 US Code 1526. All previous formats plus the following appendix
 * and details 42 USC app. 1526 42 USC appendix 1526 42 USC app. 1526, 1551,
 * 1553, 1555, and 1561
 *
 */
USC_SHORT_P =

 	"(\\d+)\\s*" + USC + "app(?:\\.|endix)\\s*(?:((?:(?:and )?\\d+[a-z]*(?:,\\s*)?)+(?:-[\\w]+)?)((?:\\([\\w]+\\))*\\s*(?:note|et seq\\.)?))"

   CASE_INSENSITIVE

IRC_SHORT_P =

   IRC + "app(?:\\.|endix)\\s*(?:((?:(?:and )?\\d+[a-z]*(?:,\\s*)?)+(?:-[\\w]+)?)((?:\\([\\w]+\\))*\\s*(?:note|et seq\\.)?))"

   CASE_INSENSITIVE

/**
 * Matches following formats: chapter 8 of title 212, United States Code
 * Section 1477 of title 10, United States Code
 */
USC_LONG_P =

   "(?:sections?\\s*(\\w+)\\s*(?:of\\s*))?CHAPTERS?\\s*(\\d+[a-z]*)\\s+of\\s+title\\s+(\\d+)," + USC_LONG

   CASE_INSENSITIVE

IRC_LONG_P

    "(?:sections?\\s*(\\w+)\\s*(?:of\\s*))?CHAPTERS?\\s*(\\d+[a-z]*)\\s+of\\s+the\\s+" + IRC

   CASE_INSENSITIVE

USC_LONG2_P =

 	"CHAPTER\\s*(\\d+[a-z]*)(?:\\s+\\([^\\)]*\\))\\s+of\\s+title\\s+(\\d+)," + USC_LONG

   CASE_INSENSITIVE

IRC_LONG2_P

 	"CHAPTER\\s*(\\d+[a-z]*)(?:\\s+\\([^\\)]*\\))\\s+of\\s+the\\s+" + IRC

   CASE_INSENSITIVE

USC_MULTI_LONG_P =

    "sections?\\s+(.{1,100}?)\\s+of\\s+title\\s+(\\d+)(?:,|\\sof\\s+the)?" + USC_LONG

   CASE_INSENSITIVE | DOTALL

USC_MULTI_SHORT_SECT_P =

   "(\\d+)\\s*" + USC + "(?:sections?|sec\\.?)?\\s*\\xA7?\\s*\\s*((?:\\d[\\w-]*\\b(?:\\(\\w+\\))*(?:\\s+note|\\s+et seq\\.?)?(?!\\s+" + USC + ")|and|through|,|\\s)+)"

   CASE_INSENSITIVE
   
IRC_MULTI_SHORT_SECT_P =

   IRC + "(?:sections?|sec\\.?)?\\s*\\xA7?\\s*\\s*((?:\\d[\\w-]*\\b(?:\\(\\w+\\))*(?:\\s+note|\\s+et seq\\.?)?(?!\\s+" + USC + ")|and|through|,|\\s)+)"

   CASE_INSENSITIVE

USC_MULTI_CHAP_P = 

   "(\\d+)\\s*" + USC + "ch(?:apters?|\\.?)\\s*((?:\\d[\\w-]*\\b(?!\\s+" + USC + ")|and|through|,|\\s)+)"

   CASE_INSENSITIVE

IRC_MULTI_CHAP_P = 

   IRC + "ch(?:apters?|\\.?)\\s*((?:\\d[\\w-]*\\b(?!\\s+" + USC + ")|and|through|,|\\s)+)"

   CASE_INSENSITIVE


// Search patterns in support of processing multisection or multi-chapter UC Code references

USC_SECT_RX = "(?<![\\(])(\\d+[\\w-]*)((?:\\(\\w+\\))*(?:\\s+note|\\s+et seq\\.?)?)";

USC_CHAP_RX = "(?<![\\(])(\\d+[\\w-]*)";

USC_SECT_P = 

   USC_SECT_RX

   CASE_INSENSITIVE

USC_CHAP_P =

   USC_CHAP_RX

   CASE_INSENSITIVE

CONNECTORS_SP =

   "(,|through|and)"

   CASE_INSENSITIVE

SINGLE_SECT_SP =

   USC_SECT_RX

   CASE_INSENSITIVE

SINGLE_CHAP_SP =

   USC_CHAP_RX

   CASE_INSENSITIVE

BRACKETS_SP =

   "(\\(|\\))")

SECT_WORD_SP =

   "\\bsec(tion|\\.)?"

   CASE_INSENSITIVE

CHAP_WORD_SP =

   "\\bch(apter|\\.)?"

   CASE_INSENSITIVE

```

## Statutes at Large

```
statuteAtLargeP =

   "([0-9]+)\\s*STAT\\.\\s*(?:L\\.)?\\s*(\\d+[a-z]*(?:-[0-9]+)?(?: et seq\\.)?)"

   CASE_INSENSITIVE | MULTILINE

```

## Congressional Bills

```
/**
 * Matches following formats: "bill\_type" "volume"
 *
 * Where "bill\_type" could be:
 *
 * House Bill | H. R. | H.R. | HR Senate Bill |
 * S. House Resolution | H.Res. | H. Res | H. Res. | H Res | House Res. | H.
 * Resolution Senate Resolution | Senate Res. | S. Resolution | S.Res. | S.
 * Res | S. Res. House Joint Resolution | H. J. Resolution | H.J. Resolution
 * | H.J.Res. | H. J. Res. | H.J. Res Senate Joint Resolution | S. J.
 * Resolution | S.J. Resolution | S.J.Res. | S. J. Res. | S.J. Res House
 * Concurrent Resolution | H. Con. Resolution | H.Con. Resolution | H. Con
 * Res.| H. Con Res Senate Concurrent Resolution | S. Con. Resolution |
 * S.Con. Resolution | S. Con Res.| S. Con Res
 *
 * And "volume" could be: 1094 949-950 No. 119 23 (107th Congress) 213 of
 * the 107th Congress
 *
 */

BILL_TYPE_RX = "((?:house\\s+|senate\\s+|h\\.?|s\\.?)\\s*(?:bill|(?:joint\\s+|j\\.?|concurrent\\s+|con\\.?)?"
   + "\\s*(?:resolution|res\\.?))|h\\.?\\s*r\\.?|(?<!\\.)s\\.)\\s*(?:No\\.)?\\s*(\\d+)";

BILL_REF_P =
   
   BILL_TYPE_RX + "(?:-\\s*(\\d+))?)\\s*(?:(?:of\\sthe|\\()\\s*(\\d+)(th?|[nr]?d)\\sCONGRESS\\)?)?"

   CASE_INSENSITIVE);

BILL_REF2_P =

    ",?(?:-\\s*(\\d+))?\\s+(?:of\\s+the|\\()?\\s*(?:One\\s+Hundred\\s+([a-z]+)|(One Hundredth))\\s+Congress"

   CASE_INSENSITIVE);

BILL_REF3_P =

   ",?(?:- *(\\d+))? +(?:of +the|\\()? *((?:Seven|Eigh|Nine)(?:ty-(?:[a-z]+)|tieth))\\s+Congress"

	CASE_INSENSITIVE);

BILL_REF4_P =

	BILL_TYPE_RX + "(?:-\\s*(\\d+))?),\\s*(\\d{2,3})-[1-2], +"

   CASE_INSENSITIVE

```

## Congressional Reports

```
PART_OR_VOLUME = "\\s+(\\d+)\\s*-\\s*(\\d+)\\s*(,\\s*((?:Pt\\.|Part|Volume|Vol\\.|and|[0-9])*\\s*(?:Pt\\.|Part|Vol\\.|Volume|[0-9])(\\([^)]+\\)\\s*)))?";

REPORT_NO = "\\.?\\s*R(?:e?pt|eport)\\.?\\s*(?:N(?:umber|o)\\.?)?)"

HOUSE_REPORT_P =

 	"\\b(H(?:ouse)?" + REPORT_NO + PART_OR_VOLUME

   CASE_INSENSITIVE

SENATE_REPORT_P =

 	"\\b(S(?:enate)?" + REPORT_NO + PART_OR_VOLUME

   CASE_INSENSITIVE

EXEC_REPORT_P =

    "(Ex(?:ec(?:utive)?)?" + REPORT_NO + PART_OR_VOLUME

   CASE_INSENSITIVE)

HOUSE_CONF_REPORT_P =

 	"(Conference Report \\(?:H\\. Rept\\.\\))" + PART_OR_VOLUME

   CASE_INSENSITIVE

CONF_REPORT_P =

	"(Conf(?:erence)?" + REPORT_NO + PART_OR_VOLUME

   CASE_INSENSITIVE

```

## Congressional Documents

```
DOC_NUM = "\\.?\\s*Doc(?:ument(?:ation)?)?\\.?\\s*(?:N(?:o|umber)\\.?)?";

HOUSE_DOC = "(H(?:ouse)?" + DOC_NUM + ")";

HOUSE_DOC_P =

   HOUSE_DOC + PART_OR_VOLUME

   CASE_INSENSITIVE

HOUSE_DOC2_P =

   HOUSE_DOC + "(?:\\.?\\s+([\\dA-Z]+),\\s*(?:(\\d+)(?:th|[nr]d|st)\\s*Cong(?:ress)?\\.?))"

   CASE_INSENSITIVE

SENATE_DOC_P =

    "((?:S|Senate)" + DOC_NUM + ")" + PART_OR_VOLUME

   CASE_INSENSITIVE

TREATY_DOC = "((?:(?:Senate)?\\s*T(?:reaty)?)\\.?\\s*" + DOC_NUM + ")";

TREATY_DOC_P =

   TREATY_DOC + PART_OR_VOLUME

   CASE_INSENSITIVE

TREATY_DOC2_P =

   TREATY_DOC + "\\s+(\\d+)-(\\d+)\\s*"

   CASE_INSENSITIVE

```

## Congressional Hearings

```
SENATE_HEARING_P =

 	"(S)(?:enate)?\\.?\\s*(?:Hrg|Hearing)\\.?" + PART_OR_VOLUME

   CASE_INSENSITIVE

```

## Congressional Committee Prints

```
COMMITTEE_PRINT_P =

 	"(S)(?:enate)?\\.?\\s*(?:Prt|Print)\\.?\\s*(?:(?:No|Number)\\.?)?" + PART_OR_VOLUME

   CASE_INSENSITIVE

```

## Code of Federal Regulations

```
CFR_P =

	// number:
	"([1-5]?\\d)\\s*CFR\\s*(Chapters?|Ch\\.|Parts?|Sec\\.|sections?)*\\s*([\\d]+|\\d+|[IVXLCDM]+),?\\s*"
	// detail:
	+ "((?:(?:et (seq|al)\\.)|(?:\\s*(and|through|or|,)\\s+)|(?:(\\d+,?\\s)+)|"
	+ "(?:\\-?\\d+(?:\\.\\d+)?(?:\\(\\w+\\))*)|(?:\\.\\w+(?:\\(\\w+\\))*))+)?",
	CASE_INSENSITIVE

```
