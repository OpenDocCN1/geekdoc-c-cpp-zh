extension: "string" ("") Extension of output filename.

features: "boolean" ("N") If set, the sequence output will include feature information either in the same file (if the sequence format supports it) or in a separate file (by default in GFF format).

type: "string" ("") The output sequence type. Although this will default to the type of the first output sequence, it is recommended that a value is always defined to make the output sequence type clear. The sequence type must be a standard sequence type (Section A.7, ‘Sequence types’).

minseqs: "integer" ("1") The minimum number of sequences that are expected in the output file.

maxseqs: "integer" ("INT_MAX") The maximum number of sequences that are expected in the output file.

nullok: "boolean" ("N") If the application can accept a null value for this definition and can run without generating sequence output, the nullok: attribute must be set to "Y". This allows a default value to be omitted or the application to be run with -noFlag on the command line (where Flag is the data definition flag).

nulldefault: "boolean" ("N") The nulldefault: attribute overrides the default name generation, and uses an empty string (no sequence output) as the default for programs where sequence output is only occasionally required. If an empty string is specified on the command line, the standard default value will be generated instead. In combination with the nullok: and missing: attributes, this allows qualifiers to be null by default, and turned on from the command line.

# A.5.3.19.1 Associated qualifiers

The seqoutall datatype has the following associated qualifiers which may be hard-coded as attributes in an ACD file. These qualifiers are described in the EMBOSS User's Guide:

| osformat: "string" ("") | Output seq format |
| osextension: "string" ("") | Filename extension |
| osname: "string" ("") | Base filename |
| osdirectory: "string" ("") | Output directory |
| osdbname: "string" ("") | Database name to add |
| ossingle: "boolean" ("N") | Separate file for each entry |
| oufo: "string" ("") | UFO features |
| oformat: "string" ("") | Features format |
| ofname: "string" ("") | Features filename |
| ofdirectory: "string" ("") | Output directory |

The seqoutall datatype has a datatype-associated command line qualifier (-ossingle) which is often hard-coded as an attribute in an ACD file (see the EMBOSS User's Guide). ossingle: defines the default value for the -ossingle qualifier and can be set to "Y" to direct output to multiple sequence files. For example, the EMBOSS program seqretsplit splits an input sequence input multiple files using this attribute.