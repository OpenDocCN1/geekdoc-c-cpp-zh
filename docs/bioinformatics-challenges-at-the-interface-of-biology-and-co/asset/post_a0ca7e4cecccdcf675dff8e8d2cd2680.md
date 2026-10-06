
## Bioinformatics: charles at the interface of biology and computer science

Such experience would identify any sequence containing exactly these residues at the specified positions (KTYFP). However, a sequence serine in place of threonine at position 2 would not be matched, even though this is a biologically conservative replacement. This is because the outcome of this pattern matching is binary: i.e., a sequence matches the expression or it is counted as a mismatch. This approach gave to the PROSITE ‘pattern’ database, and its simplicity doubtless to its wide appeal.

In the example, the wild cards in the expression lend a degree of flexibility but, in so, reducing its specificity. For relatively long, well-conserved sequence fragments, unlike our α hemoglobin, is unlikely to cause problems. However, the shorter the sequence, and the lower the degree of conservation in the alignment, the greater the risk of identifying sequences that are similar but unrelated to the expression. For example, consider the expression used to characterise the parathyroid hormone (PS00335)⁵, which could be found in the November 2015 release of PROSITE:

In this residue-pattern, most residues are generic (anything goes); when scanned against the November 2015 release of UniProtKB/Swiss-Prot, of 21 matches are found to be false. If we reduce the length of the expression by removing the first two residues, this generates a staggering 724 matches, most of which (707) are false. This demonstrates the importance of ensuring that consensus expressions are sufficiently long to be biologically. Another way to replace wild cards with biologically meaningful residues is examining the types of amino acid residue that could properly align columns and grouping those that share physicochemical properties. Sequence matches are then restricted to those that contains residues in the groups. In this way, the α hemoglobin expression can be re-written using the following notation, specified by the PROSITE syntax:

```
K-TY-F-P-[HJ]-[DN]-[L]-[SA]-H-G-S-X-Q-[IVL]-[KNQ]-G
```

Here, it’s possible to group HQ (anything goes); these groups are broadly similar (to verify that this is true, compare how the PAM 250 and BLOSUM 62 matrices score their respective substitutions). For the remaining two positions in the alignment, however, the observed residues are APTSD and GKDA (columns 14 and 18 respectively). It’s much less obvious that these groups are internally consistent, in terms of shared properties, it’s reasonable to use wild cards for alignment positions, and the specificity of the expression overall will not be significantly sacrificed.

Twenty years ago, when sequence databases were smaller and less diverse than today, simple consensus were able to perform (anything goes); this is no longer across the board, because their diagnostic abilities are being challenged by the size and contents of current sequence databases. A PROSITE pattern whose diagnostic power endured over the years that for rho-ligand GPCRs (PS00237)⁷, as shown:

⁵ http://prositeasy.org/PS00335
⁶ http://prositeasy.org/scanprosite-site-doc.html#pattern_syntax
⁷ http://prositeasy.org/cgi-bin/prosite/get-entry?ID=PS00237

(a) PA [STIMALVC]-[GTAPE]-[EDPRH]-x(2)-LIMVG]-x(2)-LVMFT]-[GSTAN]-[VAS]-[DENI]-R-[FYCH]-x(2)-LIM]. NR RELEASE=20,22654; NR TOTAL=116(116);POSITIVE=115(115);UNKNOWN=0(0);FALSE_POS=1(1);

(b) PA [STGANCDE]-[GTDKPR]-[X]-[LIMVINOGA]-[RK]-[RK]-[LVMFT]-[GSTAN]-[LIMYVSTAC]-[DENI]-R-[FYCWCH]-[PE]-x-[LIM]. NR RELEASE=2015,11,54932; TOTAL=216(222);POSITIVE=1976(1973);UNKNOWN=0(0); FALSE_POS=150(149);FALSE_NEG=449;PARTIAL=32;

### Figure 4.6

PROSITE pattern for rhodopsin-like GPCRs from release 8, November 1991 (a) and 20,120. November 2015 (b). The PA lines show the consensus expression; the NR lines indicate the release of the database that was searched (Swiss-Prot in a), UniProtKB/Swiss-Prot in (b), and numerical results of the search — figures in parentheses indicate the number of proteins in which the matches were found: e.g., 2,126 matches in 2,122 sequences that four proteins match the pattern twice.

in 17 fragment encapsulates the C-terminal TM domain of rhodopsin-like G protein-coupled receptors (GPCRs)—this bears a conserved residue, believed to be the G protein interaction site. Several features are worthy of note. Some alignment positions are degenerate: e.g., originally defined different amino acid residues to conserve, and in the November 2015 alignment up to 12 six wild cards were used in 1991, but only two in 2015 — the remaining four tolerate residue except the two which are in curly brackets. Only one position is conserved.

The database searched in 1991 (Swiss-Prot) contained 22,654; in 2015 (UniProtKB) contained 54,932. In 1991, 115 were correct; in 2015, 1,976 were correct. 116 matches were found in 1991; 222 matches were found in 2015. 1 was false in 1991; 150 were false in 2015. 449 were missed; 32 were partial. 2,126 matches were found in 2,122 sequences that four proteins match the pattern twice. This demonstrates the importance of ensuring that consensus expressions are sufficiently long to be biologically. Another way to replace wild cards with biologically meaningful residues is examining the types of amino acid residue that could properly align columns and grouping those that share physicochemical properties. Sequence matches are then restricted to those that contains residues in the groups. In this way, the α hemoglobin expression can be re-written using the following notation, specified by the PROSITE syntax:

```
K-TY-F-P-[HJ]-[DN]-[L]-[SA]-H-G-S-X-Q-[IVL]-[KNQ]-G
```

Here, it’s possible to group HQ (anything goes); these groups are broadly similar (to verify that this is true, compare how the PAM 250 and BLOSUM 62 matrices score their respective substitutions). For the remaining two positions in the alignment, however, the observed residues are APTSD and GKDA (columns 14 and 18 respectively). It’s much less obvious that these groups are internally consistent, in terms of shared properties, it’s reasonable to use wild cards for alignment positions, and the specificity of the expression overall will not be significantly sacrificed.

Twenty years ago, when sequence databases were smaller and less diverse than today, simple consensus were able to perform (anything goes); this is no longer across the board, because their diagnostic abilities are being challenged by the size and contents of current sequence databases. A PROSITE pattern whose diagnostic power endured over the years that for rho-ligand GPCRs (PS00237)⁷, as shown:

To address some of these issues, PROSITE began to complement some of its weaker patterns withically more powerful profiles (Bairoch and Bucher, 1994). We discuss profiles at the end of the chapter. Before doing so, however, we will explore one other use of consensus expressions. The patterns we've described are family-specific—they are designed to capture the conserved sequence of a protein family, and to use this (usually 15–25 residue) to recognise other members of the same family. But patterns can also be used to pinpoint non-specific features of sequences, such as those that define sugar-attachment sites, glycosylation, phosphorylation or PTM sites, and on. These features are generally much smaller (sometimes only 3–4 residues in typical)—some typical examples are given in Table 4.1. The same syntax as used before: residues within square brackets are allowed at a particular position; those in curly brackets are disallowed at that position; x denotes any residue; and numbers in parentheses indicate the nature of residues the specified type.

The short, non-specific nature of expressions like those in Table 4.1 renders them diagnostically unreliable. In isolation, matches to them are therefore relatively meaningless and can only indicate possible locations of sites, should such functionality

### Box 4.6: Resolving true and false matches

Discriminating true-positive from true-negative sequences with few (or most) true matches or missed sequences. In precision, this means the best resolution between the score distributions of true-positive and true-negative, reducing (or, better, eliminating) the overlap between them. This is important, for sequences within the region of overlap, it can be difficult or impossible to determine which are really correct and which are genuinely false. Statistical approaches are used to assign confidence levels to such matches; however, while the scoring above the threshold may be statistically significant, they are not necessarily relevant. This is a tough sequence analysis cut.

![](img/1af2ff402ef4720886c50af0bb8e9b5_139_0.png)

Figure 4.27: true-positive and true-negative sequences
