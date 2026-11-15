A default value is also set by defining the `default:` global attribute.

**Key attributes** The type of sequence can be restricted by setting the `type:` attribute. The sequence type must be a standard type (Section A.7, ‘Sequence types’). Sequence features (Section 6.9, ‘Handling features’) can be written if the `features:` ACD attribute is set. FASTA format is used by default for the output sequence(s). The format is normally set at the command line but a default may be hard-coded with `osformat:`.

# A.2.3.20 seqoutset

Output file for a set of sequences.

**Data value** The data value is a USA (see the *EMBOSS User’s Guide*) of a sequence output stream on a set of single sequences stored in memory together, to be written to file. For example, the USA might be a database reference or file.

**Default value** The output filename has the format `name.extension` and is constructed from the `name:` and `extension:` attributes. If the `name:` attribute is not defined in the ACD file. It will default to the calculated attribute `name:` of the *first* sequence that is read in. The ACD operation to get this value is `$ (asequence.name)` if the sequence parameter was named `asequence`. A default value is also set by defining the `default:` global attribute.

**Key attributes** The type of sequence can be restricted by setting the `type:` attribute. The sequence type must be a standard type (Section A.7, ‘Sequence types’). Sequence features (Section 6.9, ‘Handling features’) can be written if the `features:` ACD attribute is set. FASTA format is used by default for the output sequence(s). The format is normally set at the command line but a default may be hard-coded with `osformat:`.

# A.2.4 Description of selection ACD datatypes

# A.2.4.1 list

A list of options (text descriptions) with text labels.

The user is presented with a limited list of options they can choose from. The choices can be labelled by any arbitrary text label. The option descriptions are usually more verbose than for the `selection` datatype.

**Data value** The data value is one (or more) of the valid options.

An option is specified by the label text or a non-ambiguous part of the descriptive text itself given after the label. If multiple selections are allowed, the user must supply a comma-separated list of labels (options). For example, the following ACD definition:

```
list: frame [
  standard:"Y"
  help: "Allows selection from a set of reading frames"
  default: "1"
  minimum: "1"
```