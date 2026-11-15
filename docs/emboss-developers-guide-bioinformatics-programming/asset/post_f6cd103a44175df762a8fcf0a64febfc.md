
/* File exists */
AjBool ajFilenameExists (const AjPStr filename);
/* Exists and is a directory */
AjBool ajFilenameExistsDir (const AjPStr filename);
/* Exists and is executable */
AjBool ajFilenameExistsExec (const AjPStr filename);
/* Exists and is readable */
AjBool ajFilenameExistsRead (const AjPStr filename);
/* Exists and is writeable */
AjBool ajFilenameExistsWrite (const AjPStr filename);

To return the file size call ajFilenameGetSize:

```
ajlong ajFilenameGetSize (const AjPStr name);
```

Functions for setting a string representing a filename have the prefix ajFilenameTrim if they remove the path and/or file extension from the name. The trim functions include:

```
/* Truncates a filename to a basic file name. */
AjBool ajFilenameTrimAll (AjPStr* Pname);
/* Remove directory path and file extension from a file name. */
AjBool ajFilenameTrimPathExt (AjPStr* Pname);
/* Remove directory path (if any) only. */
AjBool ajFilenameTrimPath (AjPStr* Pname);
/* Remove extension (if any) only. */
AjBool ajFilenameTrimExt (AjPStr* Pname);
```

The prefix ajFilenameReplace functions allow the file extension and path to be replaced with some other value. They have the prefix ajFilenameSet if they set the filename in some other way. For example, the filename can also be set to an available temporary filename (with optional path) by calling ajFilenameSetTempname:

```
/* Sets the file extension.*/
AjBool ajFilenameReplaceExtS (AjPStr* Pname, const AjPStr extn);
AjBool ajFilenameReplaceExtC (AjPStr* Pname, const char* extn);
/* Sets the directory path. */
AjBool ajFilenameReplacePathS (AjPStr* Pname, const AjPStr path);
AjBool ajFilenameReplacePathC (AjPStr* Pname, const char* path);
/* Sets name to an available temporary file name with a defined path. */
AjBool ajFilenameSetTempnamePathS (AjPStr* Pfilename, const AjPStr str);
/* Sets name to an available temporary file name. */
AjBool ajFilenameSetTempname (const char** Pname);
```

There are a few functions for manipulating strings representing file paths:

```
/* Changes directory path to one level up. */
AjBool ajDirnameUp (AjPStr* Pname);

/* Add trailing '/' if missing. */
AjBool ajDirnameFix (AjPStr* Path);

/* Checks for valid path, and appends trailing '/' if missing. */
AjBool ajDirnameFixExists (AjPStr* Ppath);

/* Checks for valid path and ensures full path definition is included. */
AjBool ajDirnameFillPath (AjPStr* Ppath);
```

ajDirnameFixExists and ajDirnameFillPath check that the specified path (Ppath) is a valid directory. A trailing / is appended to the path if missing. ajDirnameFillPath will navigate up the directory structure and modify the path if necessary to ensure that the full path definition is included.

## 6.15 Handling application reports

### 6.15.1 Introduction

Applications should use the standard set of report formats (see the EMBOSS User's Guide) for output where possible. Each report defines a content and layout of text in a file. Most of the reports are for describing features, usually short sequence motifs, in a sequence. The sequence motifs, ID codes, sequence position numbers and the corresponding features can be output in a variety of formats. A set of command line qualifiers (Section A.5.3.17, ‘report’) are used to control the data written to the report and set such things as the name and format of the file. Non-printable control characters are not used therefore and so are suitable for viewing on-screen or for printing.

Reports have a consistent look and feel, which helps the end-user and improves interoperation of the applications. In principle an application can use different report formats for different purposes, depending on what the output file will be used for. A human-readable report is required for the end-user whereas a more compact format might be suitable if the output is to be processed by another application. All of the standard sequence feature table formats (see the EMBOSS User's Guide) are also report formats. Other report formats cater for non-sequence information. For a complete list, descriptions and examples of the supported report formats see the EMBOSS User's Guide.

All report formats, excluding the TAB-delimited (excel) one and those using the standard feature table formats, have a block of reference information at the start of the report. This gives:

- The program name
- Date the report was generated
- The output file name
- The ID name of the sequence
- The region of the sequence for which features are being reported
- Some of the parameters and statistics of the report.

The reported data are taken from the report feature table. Different report formats report different values or different tags from the feature table. The tags that might be reported are as follows:

| Tag | Description |
| --- | --- |
| start | Start position of match in sequence |
| end | End position of match in sequence |
| length | Length of match in sequence |
| name | Name of sequence |
| sequence | Sequence of match |
| strand | DNA strand in which feature occurs |
| tagname | Printable name of feature |
| tagvalue | Feature in sequence |
| type | Type of feature |

Finally there is a block of information at the end of the report with summary information.

Internally all reports are held in a very close analogue of the General Feature Format (GFF). This flexible file format holds sequence feature information in a feature table as tag/value pairs. Features can easily be converted to any of the supported report formats (see the EMBOSS User's Guide), and can be selected by using the -rformat built-in qualifier.

GFF has some fields that must exist including:

- A feature type that can be any string but is best specified using the Sequence Ontology (SO) (for example, the EMBOSS antigenic uses 'SO:0001018' as the predicted features are of type 'epitope'. Using SO terms allows some report formats, for example GFF3 or DAS (distributed annotation system), to correctly label features with biological properties. Any unrecognised string is reported as a 'miscellaneous feature' or 'region' by these formats, with the original string retained and reported in the feature tags.
- The sequence itself which may or may not be output depending on the output report format used.
- The start and end positions of the features. GFF requires that the start is before the end, with the strand identifying nucleotide features in the reverse direction.
- A score (in case the program reports a score for the feature).

The score and most other standard GFF tags are set to zero or NULL automatically by the library. You have to explicitly use them (assign values to them) if you need them, otherwise they'll be ignored. To cope with non-standard feature values the AJAX library uses the default '/note' tag. This is transparent to the programmer, unless you select EMBL or another output format in which the '/note' tag is visible.

Any report output files should be defined in the application ACD file and retrieved from within the C source code by a call to ajAcdGetReport. Some programming is required to load the report with data and write it to file as described below.

### 6.15.2 AJAX library files

AJAX library files for handling reports are listed in the table below. Library file documentation, including a complete description of datatypes and functions, is available at: http://emboss.open-bio.org/rel/dev/libs/

| Library file documentation | Description |
| --- | --- |
| ajreport | Application reports |

ajreport.h/c. Defines the AjPReport object and functions for handling of reports. They also contain static data structures and functions for handling reports at a low level. You are unlikely to need the static data structures and functions unless you plan to implement code to support new report formats for EMBOSS. For advice on how to do this ask the EMBOSS developers.

### 6.15.3 AJAX datatypes

For handling application report output files defined in the ACD file use:

- AjPReport Application report (for report ACD datatypes)

### 6.15.4 ACD datatypes

The datatype for handling report output is:

- report Output file for sequence annotation (report)

### 6.15.5 ACD data definition

A typical ACD definition for report output:

```
report: outfile
[
    parameter: "Y"
    rformat: "diffseq"
    taglist: "int:start int:end int:length str:name str:sequence
    str:first_feature str:second_feature"
]
```

#### 6.15.5.1 Parameter name

All data definitions for report output should have standard parameter names (see Appendix A, ACD syntax reference):

- outfile

- *file
