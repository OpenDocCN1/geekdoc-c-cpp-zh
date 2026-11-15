```
application: ApplicationName
[
   groups: "GroupName1, GroupName2, ... : SubgroupName1, SubgroupName2, ... "
]
```

For example:

```
application: syco
[
   documentation: "Synonymous codon usage Gribsov statistic
   plot"
   groups: "Nucleic:Codon usage, Nucleic:Gene finding"
]
```

Typically just a single group and sub-group is specified. For example, the following ACD file indicates that the application pscan is in the group Protein and sub-group Motifs:

```
application: pscan
[
   documentation: "Scans proteins using PRINTS"
   groups: "Protein:Motifs"
]
```

A single group is also commonly sufficient, for example:

```
application: trimest
[
   documentation: "Trim poly-A tails off EST sequences"
   groups: "Edit"
]
```

# 4.2.4.1 Application group names file (groups.standard)

The application groups have become widely used elsewhere so EMBOSS now uses a standard set of group names which all group names in an ACD file are validated against. The standard is defined in the file: groups.standard which is installed in the same directory as the ACD files, e.g.:

```
.../emboss/emboss/emboss/acdgroups.standard
```

groups.standard contains one line for each valid group : attribute value. Group and sub-group (if specified) are delimited with a ':' (colon) character, and spaces in group or sub-group names are replaced by an underline character ('_'). There is also a short description of what might be expected to be placed in the group. An excerpt from the file is shown below: