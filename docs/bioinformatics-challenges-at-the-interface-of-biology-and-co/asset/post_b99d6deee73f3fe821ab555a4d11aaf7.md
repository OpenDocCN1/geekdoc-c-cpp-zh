
# Chapter 8 Linking data and scientific literature

309

| TIGR | 2 JANUARY 2000 | AC019018 (gene P40624.1 translation product AA525264) | Putative G protein-coupled receptor | G PROTEIN COUPLED RECEPTOR,G-PROTEIN COUPLED RECEPTOR 2,GCR2 | AT1GG2920 | Submitted April 2011 | TAIR |
|---|---|---|---|---|---|---|---|
| EMBL/Gen | | | | | | | |
| 1 | 01.06.2001 TrEMBL 17.0 | Q9C929 | PUTATIVE G PROTEIN-COUPLED RECEPTOR | Bank/DDBJ | | | |
| 2002 | | | | | | | | |
| 6 | 15.12.2003 UniProtKB/TrEMBL 1/07 | Q9C929 | Putative G protein-coupled receptor | | | | |
| 2004 | | | | | | | | |
| 11 | 01.02.2005 UniProtKB/TrEMBL 4/29.0 | Q9C929-ARATH | Putative G protein-coupled receptor | | | | |
| 2006 | | | | | | | | |
| 2007 | | | | | | | | |
| 2008 | | | | | | | | |
| 35 | 28.07.2009 UniProtKB/TrEMBL 15/64.6 | Q9C929-ARATH | Putative G protein-coupled receptor | | | | | |
| 51 | 28.06.2011 UniProtKB/TrEMBL 2011_07 | Q9C929-ARATH | Putative G protein-coupled receptor | G protein-coupled receptor | F4IEM5-ARATH | 28.06.2011 UniProtKB/TrEMBL 2011_07 | 1 |
| 2012 | | | | | | | | | |
| 68 | 13.11.2013 UniProtKB/TrEMBL 2013_11 | Q9C929-ARATH | Putative G protein-coupled receptor | G-protein coupled receptor 2 | F4IEM5-ARATH | 13.11.2013 UniProtKB/TrEMBL 2013_13 | 23 |
| 11.12.2013 | Merged into GCR2_ARATH (F4IEM) | | | Land-like GCR2 (Alt name: G-protein-coupled receptor 2) | GCR2_ARATH | 11.12.2013 UniProtKB/Swiss-Prot 2013_12 | 24 |
| | | | | Land-like GCR2 (Alt name: G-protein-coupled receptor 2) | GCR2_ARATH | 19.03.2014 UniProtKB/Swiss-Prot 2014_03 | 27 |

![](img/1af42ff402ef4720886c50af0bb8e9b5_328_0.png)

Figure 8.9 The provenance and evolution of the sequence referred to GCR2.

its identifier changed to Q9C929_ARATH. At version 68, the decision was to merge this entry with UniProtKB/Swiss-Prot GCR2_ARATH. Aspects of this convoluted story separates the evolution of Q9C929 from the TAIR mission to the TAIR submission in 2011, and from F4IEM5 from EMBL/GenBank/DDBJ in 2000, until both merged in December 2013.

Interestingly, with GCR2_ARATH represented the 24th revision²⁴ of the progenitor sequence, F4IEM5_ARATH, whose annotation painted a different picture of the identity of GCR2. Let's give it a little further.

Shortly after publication of Li et al. Science article, Illsworth et al. (2008) challenged their results. They demonstrated that the sequence of GCR2 is highly similar to those of lanthionine synthetase (LanC)-like proteins, a divergent family of peptide-modifying enzymes. Strikingly, they showed that the compelling topology of the alleged transmembrane (TM) hydrophicity profile was in result of the seven-fold symmetry

> ²⁴ http://www.uniprot.org/uniprot/F4IEM5.txt?version=24

of the internal helical fold of this protein's globular structure (the-blue regions at the centre of the molecular structures shown in Figure 8.8 (c). Curiously, a simple BLAST search, and/or searches of the main protein databases reveal the relationship with the LanC-like proteins — in consequence, the cross-references to InterPro, Pfam and PRINTS highlighted in red towards the bottom of Figure 8.8 (f).

# Bioinformatics challenges at the interface of biology and computer science

So why didn't Liu et al. perform trivial searches like this? Why were they so convinced GCR2 was a GPCR? Of the answer perhaps lies at the start of their article. That they say:

Only one Arabidopsis putative GPCR protein (GCR1) has been characterized in plants..., and no ligand has been defined for any GPCR. To identify unrecognized GPCR proteins in Arabidopsis, we started by searching the Arabidopsis genome and found a GCR2, GenBank code At1g52920 encoding a putative GPCR [our emphasis].

In fact, At1g52925 is a TAIR accession number, not a GenBank code (the clue is in the letters 'At' at the start of the code). So GCR2 had already been annotated as a possible GPCR, and Liu et al. saw no reason to disagree — presumably, they were motivated to find GCR2 in the earlier discovery of GCR1, and with a ready-made candidate from TAIR, all they had to do was demonstrate protein interaction and involvement in ascorbic acid residues.

Notwithstanding the apparent failure to run a simple BLAST search, the hydropathy plot (Figure 8.8 (d)) generated with the TM prediction server, DAS (Saserzo et al., 1997) Liu used to create their structural Figure S1 A (Figure 8.8 (b)). In particular, the omission of the significance bars in the latter, which in the former, showed that only one of the seven peaks above the significance threshold for TM domains, arguing strongly against this being a membrane protein. Could we speculate that Liu removed the significance bars from the figure, and then buried the result buried in the middle of 20 pages of supplementary data (and it is easy to draw unflattering conclusions).

Now compare the structure of bovine rhodopsin (PDB code 1F8826), that of nysin cyclase (PDB code 2G0D7), a GCR2 homolog from the LanC-like protein family. GCR2 lacks both sequence and structural similarity to GCRs. Nevertheless, the relationship with GCRs continues to be predicted through the sequence data-based bases: as shown in Figure 8.9, in December 2013, the UniProtKB/Swiss-description line changed from 'G-protein [coupled] receptor 2' to the name rather confusing 'Recommended name: LanC-like protein GCR2.
