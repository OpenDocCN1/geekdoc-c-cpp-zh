| snucleotide: "boolean" ("N") | Sequence is nucleotide |
| sprotein: "boolean" ("N") | Sequence is protein |
| slower: "boolean" ("N") | Make lower-case |
| supper: "boolean" ("N") | Make upper-case |
| sformat: "string" ("") | Input sequence format |
| sdbname: "string" ("") | Database name |
| sid: "string" ("") | Entryname |
| ufo: "string" ("") | UFO features |
| fformat: "string" ("") | Features format |
| fopenfile: "string" ("") | Features filename |

# A.5.2.17 seqall

type: "string" ("") Forces the sequence(s) to be of the given type. By default any sequence type is accepted. The type : attribute is normally set so that the accepted input sequence type is clear. The sequence type must be a standard sequence type (Section A.7, ‘Sequence types’).

features: "boolean" ("N") If the features : attribute is set, the sequence input will include feature information either in the same file (if the sequence format supports it) or in a separate file (by default in GFF format).

entry: "boolean" ("N") If set, the sequence input will include the full original text of the input sequence or database entry.

nullok: "boolean" ("N") If the application can accept a null value for this definition and can run without sequence input, the nullok : must be set to "Y". This allows a default value to be omitted or the application to be run with -noFlag on the command line (where Flag is the data definition flag).

minseqs: "integer" ("1") Minimum number of sequences to be read. By default, a minimum of one sequence is acceptable.

maxseqs: "integer" ("INT_MAX") Maximum number of sequences to be read. By default, there is no maximum.

# A.5.2.17.1 Associated qualifiers

The seqall datatype has the following associated qualifiers which may be hard-coded as attributes in an ACD file. These qualifiers are described in the EMBOSS User’s Guide:

| sbegin: "integer" ("0") | Start of the sequence to be used |
| send: "integer" ("0") | End of the sequence to be used |
| sreverse: "boolean" ("N") | Reverse (if DNA) |