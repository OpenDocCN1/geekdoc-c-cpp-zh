# 4.3.3.3.1 Sequence input

For biological sequences input use:

+   - `sequence`: A single sequence for reading
+   - `seqall`: A set of single sequences that are addressed one after another
+   - `seqset`: A set of single sequences that can be used all at the same time
+   - `seqsetall`: One or more sets of single sequences that can be used all at the same time

The data value in all cases is the Uniform Sequence Address (USA) of an input sequence stream. The USA specification is described in the _EMBOSS User's Guide_.

# 4.3.3.3.2 Feature input

For biological sequence features input use:

+   - `features`: Sequence feature annotation in any supported feature format

The data value in all cases is the Uniform Feature Object (UFO) of an input sequence feature stream. The UFO specification is described in the _EMBOSS User's Guide_.

# 4.3.3.3.3 Files and directories

For general input files and directories use:

+   - `directory`: A directory that can be used for input or output
+   - `dirlist`: A list of file names that are read from a directory
+   - `filelist`: A list of input files
+   - `infile`: Non-sequence-related input file

In all cases, the data value is any valid file or directory name.

# 4.3.3.3.4 Data files

For input data files use:

+   - `datafile`: A formatted data file read from the standard EMBOSS data search path
+   - `matrix`: Comparison matrix file (integer values)
+   - `matrixf`: Comparison matrix file (floating point values)

In all cases, the data value is the name of a file in the EMBOSS data search path (see the _EMBOSS User's Guide_).

Typically where a comparison matrix is specified, gap penalties will also be required. These must be specified separately in one or more other data definitions.