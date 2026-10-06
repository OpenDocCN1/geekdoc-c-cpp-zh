
## Box 4.7 Visualising protein fingerprints

Protein fingerprints are most easily understood when viewed graphically. For a given fingerprint, a graph is created when the query sequence is plotted along the x-axis, and scores with the constituent fingerprints are plotted on the y-axis. For each motif, a window whose corresponds to the width of the motif is slid along the query sequence, and its identity score is calculated using the frequency matrix derived from the motifs stored in the PRINTS database. Where a window scores above a given threshold (20 per cent identity), a coloured block is shown to mark the location of the match. If we were merely to plot such motif matches linearly, as shown in Figure 4.31, we could not know whether all the motifs had been matched, unless we used some other visual way to depict 'missing motifs'.

![](img/1af42ff402ef4720886c50af0bb8e9b5_144_0.png)

Figure 4.31
Plotting consecutive motifs in a fingerprint.

An alternative is to plot the result of each motif scan separately. For true-positive matches, we expect to see a complete set of blocks running diagonally across the plot, from N- to C-terminus. As shown in Figure 4.32, we can immediately see that the query sequence on the left matches all the fingerprint motifs, while the sequence on the right fails to match motifs 4 and 5.

![](img/1af42ff402ef4720886c50af0bb8e9b5_144_1.png)

Figure 4.32
Plots showing complete (left) and partial (right) fingerprint matches.

Fingerprint graphs like this facilitate rapid visual inspection of query sequences, allowing ready identification of complete matches, and of partial matches that fail to match one or more motifs. This renders fingerprinting a more powerful diagnostic tool than methods that use only single motifs.

## Bioinformatics challenges at the interface of biology and computer science

![](img/1af42ff402ef4720886c50af0bb8e9b5_145_0.png)

![](img/1af42ff402ef4720886c50af0bb8e9b5_145_1.png)

Percentage sequence identity to motif
Residue number

### Figure 4.33

Graphical results of scanning hemoglobin chains from human (left-plot) and the Antarctic dragonfish (Cygnodrace mawsoni) (right-plot) the alpha hemoglobin fingerprint, ALPHAHAEM: the human sequence makes a complete match, the dragonfish sequence a partial match.

The ALPHAHAEM fingerprint identifies several partial matches; the graphical tool, GraphScan¹, provides an elegant element of visualising the quality of the matches, in terms of number of motifs matched, the individual motif scores, the background noise, etc. Figure 4.34 shows another of the partial matches.

Here, the match with a hemoglobin β chain from the paleo-toothed slot (P1426²) – only motifs 4 and 5 are matched, with relatively poor scores. However, if we scan the sequence with a β hemoglobin fingerprint, BETAHAEM (PR00814³), we see a striking complete positive match. This illustrates the power of fingerprints to differentiate between similar sequences from the same family or superfamily (the globin superfamily). By contrast with the consensus expressed, false negatives tends to be less of an absolute limitation for fingerprints, divergent families are more likely to be identified as partial matches. We'd like to be able to capture such outliers as complete matches, the use of frequency metrics limits the overall scoring potential of the method, making fingerprints less sensitive than profile-based approaches.

### Profiles and hidden Markov models

We saw at the start of this section that the main alignment-pattern-recognition methods make use of the sequence information encompassed each single motif, in multiple motifs or complete domains. Techniques in this latter category are profiles and hidden Markov models.

> ¹http://www.bioinf.manchester.ac.uk/cgi-bin/dbbrowser/fingerPRINTScan/GraphScan.cgi
²http://www.uniprot.org/uniprot/P1426
³http://www.bioinf.manchester.ac.uk/cgi-bin/dbbrowser/DoPRINTS.pl?cmd_a=Display&qua_a=/Full&fun=aBETAHAEM

## Chapter 4 Biological sequence analysis

## 127

![](img/1af42ff402ef4720886c50af0bb8e9b5_146_0.png)

HBB_BRATR vs ALPHAHAEM
HBB_BRATR vs BETAHAEM

Figure 4.34

Graphical results of scanning the hemoglobin β chain from the pale-throated three-toed sloth (*Bradypus tridactylus*) against the α hemoglobin fingerprint, ALPHAHAEM (left), which makes it a partial match and BETAHAEM (right), which makes it a complete match.

Profiles were inserted into PROSITE in 1994, in an attempt to offer diagnostic alternatives for some of its weaker patterns (Bairoch and Bucher, 1994). Profiles are essentially complex scoring tables or matrices that encapsulate not only the conserved motifs within sequence alignments, but also the regions in insertions/deletions (*indels*) found to accumulate. The generalised profile syntax is an adaptation from the profile introduced by Griskov et al. (1987). The profile itself encodes alignments as a series of match positions (MI), as that that occur in conserved motifs, and insert positions (I), where additional residues are deleted (Bucher and Bucher, 1994; Bucher, 1996). When traversing an alignment, it is possible to move from a match to another match, or from a match to an insert; or a residue may have been deleted. At each match or insert, there is a match-atch score at match position; there’s a residue-independent deletion score per residue; state transition occurs between any two consecutive steps: e.g., match-insert (MI), match-delete (MD), delete-insert (DI), delete-delete (DD).

Part of PROSITE for the globin superfamily is illustrated in Figure 4.35: this corresponds to the N-terminal half of the alignment shown in Figure 4.28, up to the first gap and including the first motifs of the α hemoglobin fingerprint. Two long match regions are seen, separated by a small insert region. Within the conserved blocks, small inlets are not completely forbidden, but are strongly impeded by deletion and insertion penalties (D=-20, I=-20), and even larger-match, match-delete transition penalties (MI=-210, MD=-210) defined in the DEFAULT line. These strict values are superseded by more permissive values in the gained regions of the alignment (e.g., D=-5, MI=-55, MD=-55), and in the match regions (e.g., D=-6).

The parameters for each match position include a range of position-specific scores, including initiation and termination scores, state-transition scores, insertion/

## Bioinformatics at the interface of biology and computer science

```
/GENERAL_SPEC;ALABET=ABCDEFGHJKMNPQRSTXYZ;LENGTH=154;
/DISJOINT;DEFINITIONS=PROJECT;N=1;M=524;
/NORMALIZATION;FUNCTION=LINEAR;R=0;M=210506;E=E2029003;TEXTS=Nscore;
/CUT_LEVEL;SCORE=524;TYPE=1;
/CUT_OFF;SCORE=353;N=6;SCORE=6;TYPE=7;
/DEFAULT;R=-20;N=18;M=524;M2=210;M3=0;A=1;
/A2;A*=7;N=7;-8,10,13,12,-4,-8,16,24,-4,-6,-10,10,3,4,-10,-D=6;
/M2=20;M3=0;
/A3;A*=11;N=11;-31,2,-6,20,-22,15,16,-10,10,-18,12,-9,11,23,13,-8;D=6;
/A4;A*=17;N=17;-27,30,21,24,-18,13,26,23,36,22,-27,-18,20,16,7,24,-4;
/A5;A*=8;N=5;-38,15,30,15,17,-12,18,19,17,-6,18,19,4,15,-9,18,-31,10,2,124;D=6;
/A6;A*=11;N=10;-36,15,30,17,37,36,-19,25,27,-21,12,2,6,33,10,30,25,16;
/A7;A*=9;N=9;-28,27,22,21,14,17,17,22,22,18,18,14,14,13,14,5;D=6;
/A8;A*=12;N=12;-32,30,21,24,-18,13,26,23,36,22,-27,-18,20,16,7,24,-4;D=6;
/A9;A*=15;N=15;-21,2,6,-5,14,14,18,-9,3,4,17,-9,-6,7,-1,11,1,6,5;D=6;
/A10;A*=18;N=18;-31,16,33,30,30,33,30,36,33,23,23,23,23,34,24,30;D=0;
/A11;A*=21;N=21;-34,27,30,24,24,18,13,26,23,23,13,1,1,1,1,11,15,15,15,16,14;D=6;
/A12;A*=24;N=24;-38,15,30,15,17,-12,18,19,17,-6,18,19,4,15,-9,18,-31,10,2,124;D=6;
/A13;A*=27;N=10;-36,15,30,17,37,36,-19,25,27,-21,12,2,6,33,10,30,25,16;
/A14;A*=30;N=2;-28,27,22,21,14,17,17,22,22,18,18,14,14,13,14,5;D=6;
/A15;A*=33;N=3;-32,30,21,24,-18,13,26,23,36,22,-27,-18,20,16,7,24,-4;D=6;
/A16;A*=36;N=5;-21,2,6,-5,14,14,18,-9,3,4,17,-9,-6,7,-1,11,1,6,5;D=6;
/A17;A*=39;N=3;-31,16,33,30,30,33,30,36,33,23,23,23,23,34,24,30;D=0;
/A18;A*=42;N=3;-34,27,30,24,24,18,13,26,23,23,13,1,1,1,1,11,15,15,15,16,14;D=6;
/A19;A*=45;N=5;-38,15,30,15,17,-12,18,19,17,-6,18,19,4,15,-9,18,-31,10,2,124;D=6;
/A20;A*=48;N=10;-36,15,30,17,37,36,-19,25,27,-21,12,2,6,33,10,30,25,16;
/A21;A*=51;N=2;-28,27,22,21,14,17,17,22,22,18,18,14,14,13,14,5;D=6;
/A22;A*=54;N=3;-32,30,21,24,-18,13,26,23,36,22,-27,-18,20,16,7,24,-4;D=6;
/A23;A*=57;N=5;-21,2,6,-5,14,14,18,-9,3,4,17,-9,-6,7,-1,11,1,6,5;D=6;
/A24;A*=60;N=3;-31,16,33,30,30,33,30,36,33,23,23,23,23,34,24,30;D=0;
/A25;A*=63;N=3;-34,27,30,24,24,18,13,26,23,23,13,1,1,1,1,11,15,15,15,16,14;D=6;
/A26;A*=66;N=5;-38,15,30,15,17,-12,18,19,17,-6,18,19,4,15,-9,18,-31,10,2,124;D=6;
/A27;A*=69;N=10;-36,15,30,17,37,36,-19,25,27,-21,12,2,6,33,10,30,25,16;
/A28;A*=72;N=2;-28,27,22,21,14,17,17,22,22,18,18,14,14,13,14,5;D=6;
/A29;A*=75;N=3;-32,30,21,24,-18,13,26,23,36,22,-27,-18,20,16,7,24,-4;D=6;
/A30;A*=78;N=5;-21,2,6,-5,14,14,18,-9,3,4,17,-9,-6,7,-1,11,1,6,5;D=6;
/A31;A*=81;N=3;-31,16,33,30,30,33,30,36,33,23,23,23,23,34,24,30;D=0;
```

**Figure 4.35** Part of PROSITE profile GLOBIN (PS01033) (that this is one of just representing a protein, a handle that allows the data to be stored and reused).

> http://site.expasy.org/PS01033
