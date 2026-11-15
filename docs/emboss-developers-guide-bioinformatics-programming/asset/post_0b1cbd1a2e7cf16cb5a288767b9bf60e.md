
### A.5.3.2.1 Associated qualifiers

The featout datatype has the following associated qualifiers which may be hard-coded as attributes in an ACD file. These qualifiers are described in the EMBOSS User's Guide:

| Attribute | Description |
|---|---|
| oformat: "string" ("") | Output feature format |
| ofopenfile: "string" ("") | Features file name |
| ofextension: "string" ("") | File name extension |
| ofdirectory: "string" ("") | Output directory |
| ofname: "string" ("") | Base filename |
| ofsingle: "boolean" ("N") | Separate file for each entry |

The featout datatype has two associated qualifiers (-oformat and -ofname) which are often hard-coded as attributes in an ACD file (see the EMBOSS User's Guide). oformat: defines the default value for the -oformat qualifier which is the feature format and default file extension. ofname: defines the default value for the -ofname qualifier which is the default base file name

### A.5.3.3 outcodon

- name: "string" ("") Base name of output filename.
- extension: "string" ("") Extension of output filename.
- nullok: "boolean" ("N") If the application can accept a null value for this definition and can run without generating codon output, the nullok: attribute must be set to "Y". This allows a default value to be omitted or the application to be run with -noFlag on the command line (where Flag is the data definition flag).
- nulldefault: "boolean" ("N") The nulldefault: attribute overrides the default name generation, and uses an empty string (no data output) as the default for programs where data output is only occasionally required. If an empty string is specified on the command line, the standard default value will be generated instead. In combination with the nullok: and missing: attributes, this allows qualifiers to be null by default, and turned on from the command line.

### A.5.3.3.1 Associated qualifiers

The outcodon datatype has the following associated qualifiers which may be hard-coded as attributes in an ACD file. These qualifiers are described in the EMBOSS User's Guide:

| Attribute | Description |
|---|---|
| odirectory: "string" ("") | Output directory |
| oformat: "string" ("") | Output format specific to this datatype |

The outcodon datatype has a datatype-associated command line qualifier (-oformat) which is often hard-coded as an attribute in an ACD file (see the EMBOSS User's Guide). oformat: defines the default value for the -oformat qualifier which is the file format.

### A.5.3.4 outcpdb

extension: "string" ("") Extension of output file name. The extension: attribute will default to the output file format.

nullok: "boolean" ("N") If the application can accept a null value for this definition and can run without generating coordinate file output, the nullok: attribute must be set to "Y". This allows a default value to be omitted or the application to be run with -noFlag on the command line (where Flag is the data definition flag).

nulldefault: "boolean" ("N") The nulldefault: attribute overrides the default name generation, and uses an empty string (no data output) as the default for programs where data output is only occasionally required. If an empty string is specified on the command line, the standard default value will be generated instead. In combination with the nullok: and missing: attributes, this allows qualifiers to be null by default, and turned on from the command line.

### A.5.3.4.1 Associated qualifiers

The outcpdb datatype has the following associated qualifiers which may be hard-coded as attributes in an ACD file. These qualifiers are described in the EMBOSS User's Guide:

| Attribute | Description |
|---|---|
| odirectory: "string" ("") | Output directory |
| oformat: "string" ("") | Output format specific to this datatype |

The outcpdb datatype has a datatype-associated command line qualifier (-oformat) which is often hard-coded as an attribute in an ACD file (see the EMBOSS User's Guide). oformat: defines the default value for the -oformat qualifier which is the file format and default file extension.

### A.5.3.5 outdata

type: "string" ("") Defines the output datatype. It is recommended that a value is always defined to make the output datatype clear.

nullok: "boolean" ("N") If the application can accept a null value for this definition and can run without generating formatted data output, the nullok: attribute must be set to "Y". This allows a default value to be omitted or the application to be run with -noFlag on the command line (where Flag is the data definition flag).

nulldefault: "boolean" ("N") The nulldefault: attribute overrides the default name generation, and uses an empty string (no data output) as the default for programs where data output is only occasionally required. If an empty string is specified on the command line, the standard default value will be generated instead. In combination with the nullok: and missing: attributes, this allows qualifiers to be null by default, and turned on from the command line.

### A.5.3.5.1 Associated qualifiers

The outdata datatype has the following associated qualifiers which may be hard-coded as attributes in an ACD file. These qualifiers are described in the EMBOSS User's Guide:

| Attribute | Description |
|---|---|
| odirectory: "string" ("") | Output directory |
| oformat: "string" ("") | Output format specific to this datatype |

The outdata datatype has a datatype-associated command line qualifier (-oformat) which is often hard-coded as an attribute in an ACD file (see the EMBOSS User's Guide). oformat: defines the default value for the -oformat qualifier which is the file format and default file extension.

### A.5.3.6 outdir

- fullpath: "boolean" ("N") If set to "Y" requires the path to be specified in full when passed to the program, although the user may provide a path from the current working directory.

- extension: "string" ("") The default extension for all files written to the directory.

- nullok: "boolean" ("N") If the application can accept a null value for this definition and can run without an output directory, the nullok: attribute must be set to "Y". This allows a default value to be omitted or the application to be run with -noFlag on the command line (where Flag is the data definition flag).

- nulldefault: "boolean" ("N") The nulldefault: attribute overrides the default name generation, and uses an empty string (no data output) as the default for programs where data output is only occasionally required. If an empty string is specified on the command line, the standard default value will be generated instead. In combination with the nullok: and missing: attributes, this allows qualifiers to be null by default, and turned on from the command line.

### A.5.3.6.1 Associated qualifiers

The outdir datatype has no associated qualifiers.

### A.5.3.7 outdiscrete

- nullok: "boolean" ("N") If the application can accept a null value for this definition and can run without generating an output file, the nullok: attribute must be set to "Y". This allows a default value to be omitted or the application to be run with -noFlag on the command line (where Flag is the data definition flag).

- nulldefault: "boolean" ("N") The nulldefault: attribute overrides the default name generation, and uses an empty string (no data output) as the default for programs where data output is only occasionally required. If an empty string is specified on the command line, the standard default value will be generated instead. In combination with the nullok: and missing: attributes, this allows qualifiers to be null by default, and turned on from the command line.

### A.5.3.7.1 Associated qualifiers

The outdiscrete datatype has the following associated qualifiers which may be hard-coded as attributes in an ACD file. These qualifiers are described in the EMBOSS User's Guide:

| Attribute | Description |
|---|---|
| odirectory: "string" ("") | Output directory |
| oformat: "string" ("") | Output format specific to this datatype |

## A.5 DATATYPE-SPECIFIC ATTRIBUTES

The outdiscrete datatype has a datatype-associated command line qualifier (-oformat) which is often hard-coded as an attribute in an ACD file (see the EMBOSS User's Guide). oformat: defines the default value for the -oformat qualifier which is the file format and default file extension.

### A.5.3.8 outdistance

nullok: "boolean" ("N") If the application can accept a null value for this definition and can run without generating a distance matrix file, the nullok: attribute must be set to "Y". This allows a default value to be omitted or the application to be run with -noFlag on the command line (where Flag is the data definition flag).

nulldefault: "boolean" ("N") The nulldefault: attribute overrides the default name generation, and uses an empty string (no data output) as the default for programs where data output is only occasionally required. If an empty string is specified on the command line, the standard default value will be generated instead. In combination with the nullok: and missing: attributes, this allows qualifiers to be null by default, and turned on from the command line.

### A.5.3.8.1 Associated qualifiers

The outdistance datatype has the following associated qualifiers which may be hard-coded as attributes in an ACD file. These qualifiers are described in the EMBOSS User's Guide:

| Attribute | Description |
|---|---|
| odirectory: "string" ("") | Output directory |
| oformat: "string" ("") | Output format specific to this datatype |

The outdistance datatype has a datatype-associated command line qualifier (-oformat) which is often hard-coded as an attribute in an ACD file (see the EMBOSS User's Guide). oformat: defines the default value for the -oformat qualifier which is the file format and default file extension.

### A.5.3.9 outfreq

nullok: "boolean" ("N") If the application can accept a null value for this definition and can run without generating an output frequencies file, the nullok: attribute must be set to "Y". This allows a default value to be omitted or the application to be run with -noFlag on the command line (where Flag is the data definition flag).

nulldefault: "boolean" ("N") The nulldefault: attribute overrides the default name generation, and uses an empty string (no data output) as the default for programs where data output is only occasionally required. If an empty string is specified on the command line, the standard default value will be generated instead. In combination with the nullok: and missing: attributes, this allows qualifiers to be null by default, and turned on from the command line.

### A.5.3.9.1 Associated qualifiers

The outfreq datatype has the following associated qualifiers which may be hard-coded as attributes in an ACD file. These qualifiers are described elsewhere (see the EMBOSS User's Guide):
