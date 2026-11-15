# A.2.3.13 outmatrixf

Output file for floating point comparison matrix data.

**Data value** The data value is any valid filename.

**Default value** A default value is set using the `default : global attribute`.

**Key attributes** The default data format can be specified by an `oformat : attribute` which the `-oformat` associated qualifier can override.

# A.2.3.14 outproperties

Output file for phylogenetics property data.

**Data value** The data value is any valid filename.

**Default value** A default value is set using the `default : global attribute`.

**Key attributes** The default data format can be specified by an `oformat : attribute` which the `-oformat` associated qualifier can override.

# A.2.3.15 outscop

Output file for SCOP and CATH domain classification information in DCF (domain classification file) format.

DCF (domain classification file) format is a simple ‘clean’ file format for domain classification data. See the documentation for **domainner**, part of the EMBASSY **domainmatrix** package, which generates DCF files from SCOP and CATH file input.

**Data value** The data value is any valid filename.

**Default value** A default value is set using the `default : global attribute`.

**Key attributes** The default data format can be specified by an `oformat : attribute` which the `-oformat` associated qualifier can override.

# A.2.3.16 outtree

Output file for phylogenetic tree data.

**Data value** The data value is any valid filename.

**Default value** The output filename has the format `name.extension` and is constructed from the `name :` and `extension :` attributes. The `extension :` attribute will default to the output file format, and is usually left as the default value. A default value is also set by defining the `default : global attribute`.

**Key attributes** The default data format can be specified by an `oformat : attribute` which the `-oformat` associated qualifier can override.

# A.2.3.17 report

Output file for sequence annotation.

Report data is stored internally as a feature table, so the supported formats (see the _EMBOSS User’s Guide_) include the most common feature formats.