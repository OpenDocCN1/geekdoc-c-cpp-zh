# Chapter 7 Representation and meaning

```
...
REMARK 290 CRYSTALLOGRAPHIC SYMMETRY
REMARK 290 SYMMETRY OPERATORS FOR SPACE GROUP: P 21 22 21
REMARK 290 SYMOP SYMMETRY
REMARK 290 NNNMM OPERATOR
REMARK 290 1555 X,Y,Z
REMARK 290 2555 1/2X,-Y,1/2Z
REMARK 290 3555 -1/2X,-Y,1/2Z
REMARK 290 4555 1/2X,Y,-1/2Z
REMARK 290 WHERE NN -> OPERATOR NUMBER
REMARK 290 MM -> TRANSLATION VECTOR
REMARK 290 CRYSTALLOGRAPHIC SYMMETRY TRANSFORMATIONS
REMARK 290 THE FOLLOWING TRANSFORMATIONS OPERATE ON THE ATOM
REMARK 290 RECORDS IN THIS ENTRY TO PRODUCE CRYSTALLOGRAPHIC
REMARK 290 RELATED MOLECULES
REMARK 290 SYMTRY1 1 1.000000 0.000000 0.000000
REMARK 290 SYMTRY2 1 0.000000 0.000000 0.000000
REMARK 290 SYMTRY3 1 0.000000 0.000000 0.000000
REMARK 290 SYMTRY2 2 -1.000000 -0.000000 0.000000
REMARK 290 SYMTRY1 2 1.000000 0.000000 0.000000
REMARK 290 SYMTRY3 2 0.000000 0.000000 0.000000
REMARK 290 SYMTRY1 3 -1.000000 -0.000000 0.000000
REMARK 290 SYMTRY2 3 0.000000 0.000000 0.000000
REMARK 290 SYMTRY3 3 0.000000 0.000000 -1.000000
REMARK 290 SYMTRY1 4 1.000000 0.000000 0.000000
REMARK 290 SYMTRY2 4 0.000000 -1.000000 0.000000
REMARK 290 SYMTRY3 4 0.000000 0.000000 -1.000000
REMARK 290 NULL
```

Figure 7.3

Excerpt from PDB entry 1A08. The crystallographic symmetry operators for this structure are encoded in a block of pseudo-free text. All PDB records contain the same textual description and tabular headings.
://www.rcsb.org/pdb/explore?structure=1a08

with the data that extra columns couldn't be added without breaking the line-length limit. Inevitably, whenever formats had to be extended, almost always meant contravention of the original specification. A good illustration is the inclusion of the crystallographic symmetry operators in the PDB format: the only way to include these additional data without breaking the original format was to embed them in fields originally designed for human-readable, free-text comments (because it was safe to assume that existing parsers for the format wouldn't be trying to interpret the using of 'hack') is shown in Figure 7.3. As a consequence of shoe-horning the symmetry operators into the file in this way, they could safely have ignored the REMARK lines (which, previously, they could safely ignored) to try to determine whether they really contain human-readable comments or instead encode machine-readable data.

# 7.4.1 Design for change

While it's difficult to predict the technologies or scientific needs that might appear in the future of bioinformatics, from past masters and making the most of contemporary techniques, we can take sensible precautions to avoid future problems.