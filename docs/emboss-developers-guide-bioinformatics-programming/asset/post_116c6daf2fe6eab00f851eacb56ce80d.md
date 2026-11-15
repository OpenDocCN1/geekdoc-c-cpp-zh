
## Alignments

The align datatype, where used, is typically the primary output and should be defined as a parameter. The first and subsequent alignment outputs should be defined as parameter types, a warning will be generated during ACD processing if they are not. The exception is if the default: or nullok: attributes are set, in which case no warning or error messages are generated as the application can run with a default or without any value for the definition respectively.

## Files

File datatypes, where they are used, are typically the primary input (infile, filelist, directory or dirlist ACD datatypes) or output (outdir ACD datatype) and should be defined as parameters in the same way as for the report datatypes described above.

### 4.3.5.2 User prompting

Attributes are used to provide the text that will be used on the screen to prompt the user for values. Whether a prompt will appear at all depends on whether the option was defined as a parameter or one of the qualifier types (see above) and on the command used to invoke the application (i.e. what options were specified). In some cases, the prompt may or may not appear depending on the value of other inputs. For more information see Section 4.5, ‘Controlling the prompt’. The attributes used are:

```
information: "String"
code: "String"
prompt: "String"
```

Only one of code:, prompt: or information should ever be defined. The use of information: (with a standard name, see below) is preferred. In practice, prompt: is only ever required in the rare cases where the information: string might be misleading.

A default value for the information: string is defined for most common datatypes (see Section 4.3.5.2.1, ‘Standard prompts file (codes.english)’) and should be used. A warning will be generated during ACD processing if either the information: attribute is missing or if the value used is not the standard value (where a standard value is available).

If a non-standard prompt is used, the text given after the information: attribute should conform to certain conventions (Section A.4.4.1, ‘information: "String" ("")’).

In the example below a non-standard prompt is defined for asequence. A warning will be generated if you try to run this:

```
sequence: asequence
[
    standard: "Y"
    information: "Enter filename"
]
```

In the next example, no information: string is specified, therefore the standard prompt of "Read sequence from" (from codes.english) would be used instead:

```
sequence: asequence
[
  standard: "Y"
]
```

### 4.3.5.2.1 Standard prompts file (codes.english)

To provide standard prompts, a default value for the information: string is defined for most common datatypes. The defaults are in the EMBOSS system file codes.english in the application ACD file directory, e.g.:

```
../emboss/emboss/emboss/acd/codes.english
```

Prompts are given on lines beginning with DEF DatatypeName where DatatypeName is the name of the ACD datatype. The file also contains some additional standard prompts for specific instances of individual datatypes, identified by a code (not beginning with DEF). These prompts can be used with the code: attribute, for example code: "GAP".

An excerpt of the file is shown below:

```
#
# This is the EMBOSS coded prompts file. Any messages found here will
# override those in the .acd file, and can be translated into other
# languages. The file extension (default "english") is set by the
# variable "emboss_language"
#
# Messages are referred to by .acd files as code: NAME
#
# DEFXXXX codes are automatically searched for ACD type XXXX if there
# is no information (or prompt) defined in the ACD file of as a
# standard prompt for the ACD type.
#
# HELPXXXX codes are automatically searched for ACD type XXXX if there
# is no help text in the ACD file.
#
# Default prompts: these are used where no prompt for a data type
# has been provided.
DEFALIGN	"Write output alignment to"
DEFREPORT	"Write output report to"
DEFINTEGER	"Enter a number"
DEFFLOAT	"Enter a number"
DEFBOOL	"Yes or No"
.
.
.
# Gap penalties
GAP	"What gap penalty"
GAPEXT	"What gap extension penalty"
```

### 4.3.5.3 Datatype definition

Five global attributes concern the data:

```
knowntype: "String"
default: "Value"
relations: "String"
outputmodifier: "Boolean"
missing: "Boolean"
```

knowntype: describes the type of data and should be defined where the type is not already clear from the datatype itself. It is typically defined for string:, infile:, outfile: and outfileall datatypes but not, for example, for a sequence:.

Valid known type strings are listed in the file knowntypes.standard (The other attributes are used to set a default value (default:), describe relations to other data definitions (relations:), control what fields are written (outputmodifier:) and whether a NULL value can be specified (missing:). A few other values are accepted, for example “ApplicationName output” for an outfile datatype. These are documented with the datatypes (Section A.2, ‘Datatypes’).

### Note

If a value is given that is not a standard known type or other accepted value, a warning message will be generated during ACD processing. The acdvalid utility will check all knowntype values in an ACD file, and report any missing values for data definitions that require a known type.

### 4.3.5.3.1 Application data known types file (knowntypes.standard)

The standard values (known types) are read from the EMBOSS system file knowntypes.standard which can be found in the application ACD file directory:

```
../emboss/emboss/emboss/acd
```

| # Known Types | | |
| --- | --- | --- |
| # Knowntype_string | Type | Comment |
| aaindex_data | file | AAINDEX entry |
| aaindex_database | file | AAINDEX database |
| abi_trace | file | ABI sequencing trace |
| ajint_ajlong_data | file | Standard format info on ajint and ajlong |
| alistat_input | file | HMMER alistat program input |
| alistat_output | file | HMMER alistat program output |
| amino_acid_classification | file | Amino acid chemical classes data |
| . | | |
| . | | |
| . | | |

### 4.3.5.4 Help information and documentation

Every EMBOSS application accepts the global qualifiers `-help` and `-verbose`, the latter used in combination with the former (if at all). When an application is run with `-help`, helpful information is printed to the screen, including all the program parameters and qualifiers with explanatory text alongside.

The attributes below define the text that's used:

```
help: "String"
valid: "String"
expected: "String"
```

help: is usually only defined if a deeper explanation of an application parameter is needed. If `help:` is not defined, the value of the `information:` attribute (if available) or the default help string (see below) will be used instead. The `help:` string must conform to certain conventions (Section A.4.6.1, ‘help: "String" ("")’). `valid:` and `expected:` are used to describe the allowed and expected values for the online documentation. They are not usually required as, in most cases, a reasonable value is obvious from other attributes.

An example where `help:` is helpful:

```
integer: window
[
    standard: "N"
    default: 10
    minimum: 5
    maximum: 100
    information: "Window size"
    help: "Number of residues used to calculate the value for each point"
]
```

### 4.3.5.4.1 Standard help strings file (codes.english)

Default help strings are given for each datatype in the EMBOSS system file `codes.english` file (see Section 4.3.5.2.1, ‘Standard prompts file (`codes.english`)’). They have the general form:

```
HELPDatatypeName
```

where `DatatypeName` is the name of the ACD datatype.

For example:

```
HELPSEQUENCE "Sequence USA"
HELPDIRECTORY "Directory name"
```

### 4.3.5.5 Hints for GUIs

The needed: global attribute indicates whether a parameter is expected to be included in a GUI form. It is used to help GUI developers. Certain datatype-specific attributes, for example button: which can be defined for selection lists, are also used to provide such hints. See Section A.5, ‘Datatype-specific attributes’.

The attribute is defined as follows:

```
needed: "Boolean" ("Y")
```

### 4.3.5.6 For use by SOAPLAB

The following attributes provide metadata for the SOAPLAB project. They are not used by EMBOSS directly and should not appear in standard EMBOSS application ACD files.
The attributes are defined as follows:

```
qualifier: "String"
template: "String"
comment: "String"
```

### 4.3.6 Datatype-specific attributes

Datatype-specific attributes given within an ACD data definition define the characteristics of application options. They control such things as:

- The name and location of input and output files
- Detailed type-checking of inputs to ensure data is as required by the application
- Exactly what data is generated on output
- The appearance and behaviour of the user interface at the command line
- Validation of user input, e.g. to ensure user input is within permissible ranges
- Validation of application output, e.g. to ensure it is as expected
- Suggestions for graphical interfaces.

Datatype-specific attributes are defined for individual datatypes or for groups of related datatypes. The key attributes for each datatype are summarised below. For descriptions of all the available attributes see Section A.5, ‘Datatype-specific attributes’.

### 4.3.6.1 Attributes for simple ACD datatypes

These are used to validate user input.
