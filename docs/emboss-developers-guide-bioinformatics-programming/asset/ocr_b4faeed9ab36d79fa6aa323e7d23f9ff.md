**nullok**: "boolean" ("N") If the application can accept a null value for this definition and can run without sequence input, the nullok : attribute must be set to "Y". This allows a default value to be omitted or the application to be run with -noFlag on the command line (where Flag is the data definition flag).

**nulldefault**: "boolean" ("N") The nulldefault : attribute overrides the default name generation, and uses an empty string (no sequence input) as the default for programs where sequence input is only occasionally required. If an empty string is specified on the command line, the standard default value will be generated instead. In combination with the nullok : and missing : attributes, this allows qualifiers to be null by default, and turned on from the command line.

**minsets**: "integer" ("1") Minimum number of sequence sets to be read. By default, a minimum of one sequence set is acceptable.

**maxsets**: "integer" ("INT_MAX") Maximum number of sequence sets to be read. By default, there is no maximum (other than system-imposed limits on the size of an integer).

**minseqs**: "integer" ("1") Minimum number of sequences to be read. By default, a minimum of one sequence is acceptable.

**maxseqs**: "integer" ("INT_MAX") Maximum number of sequences to be read. By default, there is no maximum.

# ## A.5.2.19.1 Associated qualifiers

The seqsetall datatype has the following associated qualifiers which may be hard-coded as attributes in an ACD file. These qualifiers are described in the EMBOSS User's Guide:

| Attribute | Description |
| :--- | :--- |
| `sbegin: "integer" ("0")` | Start of the sequence to be used |
| `send: "integer" ("0")` | End of the sequence to be used |
| `sreverse: "boolean" ("N")` | Reverse (if DNA) |
| `sask: "boolean" ("N")` | Ask for begin/end/reverse |
| `snucleotide: "boolean" ("N")` | Sequence is nucleotide |
| `sprotein: "boolean" ("N")` | Sequence is protein |
| `slower: "boolean" ("N")` | Make lower-case |
| `supper: "boolean" ("N")` | Make upper-case |
| `sformat: "string" ("")` | Input sequence format |
| `sdbname: "string" ("")` | Database name |
| `sid: "string" ("")` | Entryname |
| `ufo: "string" ("")` | UFO features |
| `fformat: "string" ("")` | Features format |
| `fopenfile: "string" ("")` | Features filename |