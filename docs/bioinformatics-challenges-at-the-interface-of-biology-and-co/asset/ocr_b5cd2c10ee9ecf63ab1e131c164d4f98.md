# 5.6 Problems with database entries

Some of the issues we've been discussing in the previous sections are bound up with the constant state of flux of database entries. Our next example is no exception. Consider the following: when we refer to the database entry for the protein designated by AC# Q2329³, to which are we referring? In 1996, the sequence entered the first release of TreMBL with the description, 'Similarity to mammalian μ- and κ-type opioid receptors¹¹. In the years that followed, there were 107 versions of this entry, amongst which the description of the protein changed more than a dozen times. By March 2012, the UnProtKB/TreMBL description line read, 'Protein DMRSR-1', and its sequence had changed in length from 320 to 355 amino acids – a summary of these changes is given in Table 5.3.

A few aspects of the changes shown in Table 5.3 deserve special mention. The first description of the protein was reasonably definitive, asserting that it remained an opioid receptor (a GPCR); over the years, the force of this assertion diminished, changing to 'hypothetical 36.4 kDa protein¹², then to 'putative uncharacterized protein¹³, and more recently to 'protein ZC404.11¹⁴ and 'protein DMRSR-11¹⁵.' But the initial claim that the sequence was an opioid remained in the database for seven years; during this time, it's possible that any subsequent analyses based on that assertion may have led to inappropriate conclusions; the original description had years in which to propagate database entries.

# Table 5.3

Database descriptions and sequence lengths for Q23293.

| Database release | Description | Length |
|---|---|---|
| TreMBL 1 | SIMILARITY TO MAMMALIAN MU- AND KAPPA-TYPE OPIOID RECEPTORS | 320 |
| TreMBL 19 | HYPOTHETICAL 36.4 kDa PROTEIN | 320 |
| TreMBL 21 | Hypothetical 36.4 kDa protein | 320 |
| TreMBL 25 | Hypothetical protein | 320 |
| UnProtKB/TreMBL 2.7/27.7 | Hypothetical protein ZC404.11 | 320 |
| UnProtKB/TreMBL 4.3/29.3 | Hypothetical protein | 320 |
| UnProtKB/TreMBL 12.0/37.0 | Putative uncharacterized protein | 320 |
| UnProtKB/TreMBL 14.0/39 | SubName: Full=Putative uncharacterized protein | 355 |
| UnProtKB/TreMBL 2012_01 | SubName: Full=Protein ZC404.11 | 355 |
| UnProtKB/TreMBL 2012_03 | SubName: Full=Protein DMRSR-11 | 355 |
| UnProtKB/TreMBL 2015_04 | SubName: Full=DMRSR-11 | 355 |
| UnProtKB/TreMBL 2015_05 | SubName: Full=ZC404.11 | 355 |
| UnProtKB/TreMBL 2015_08 | SubName: Full=DMRSR-11 | 355 |
| UnProtKB/TreMBL 2015_11 | SubName: Full=DroMySuppression Receptor related | 355 |

> ⁰http://www.uniprot.org/uniprot/Q23293
¹http://www.uniprot.org/uniprot/Q23293.txt?version=1
¹²http://www.uniprot.org/uniprot/Q23293.txt?version=14
¹³http://www.uniprot.org/uniprot/Q23293.txt?version=45
¹⁴http://www.uniprot.org/uniprot/Q23293.txt?version=74
¹⁵http://www.uniprot.org/uniprot/Q23293.txt?version=77