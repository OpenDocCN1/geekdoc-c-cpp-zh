ACD attributes are available to control the length or to provide a regular expression pattern to validate the string if necessary.

# A.2.1.9 toggle

Simple boolean switch for controlling other parameters.

toggle parameters work in the same way as boolean parameters but are intended for use in turning the prompting for other parameters on or off (see Section 4.5, ‘Controlling the prompt’). Typically this is done by using a calculation to determine the value of a standard: or additional: attribute of the data definition that is being controlled. In such cases the toggle parameters are used in the calculated values, and can be placed in the “Required” section of an ACD file even if not themselves defined as standard qualifiers (using the standard: attribute).

**Data value** The data value has a ‘true’ or ‘false’ value which may be specified as follows:

```
"Y"
"yes"
"true"
"N"
"no"
"false"
```

Exactly like boolean parameters, the value will be "Y" if the flag for the parameter is entered on the command line (for example -ToggleOption). If the qualifier is absent from the command line the value will be the default value. The flag can also be prefixed by no (for example -noToggleOption) to force the value to be "N" (false). This is needed if the default value is "Y".

**Default value** A default value is set using the default: global attribute.

**Key attributes** None.

# A.2.2 Description of input ACD datatypes

# A.2.2.1 codon

Codon usage table file.

Codon usage table files are ASCII text files and can be read in several formats including GCG. Codon usage files are distributed in the EMBOSS data directory.

**Data value** The data value is the name of a codon usage table file in the EMBOSS data search path (see the EMBOSS User’s Guide).

**Default value** EMBOSS uses the human codon usage table Ehum.cut provided in the EMBOSS distribution by default but this would typically be overridden by the user. Codon usage tables are species-specific and in some cases specific to a class of genes within a species, so it is useful to be able to set the codon usage table on an application-specific basis. A default value is set using the default: global attribute.

**Key attributes** None.