# Chapter 5 The gap

Release 50 of InterPro indicated that there were 107,165 members of the rhodopsin-like G protein-coupled receptor superfamily (IPR00276). This figure was derived from scanning UniProt version 2015_02 over the relevant diagnostic signatures in PROSITE (G_PROTEIN_RECEPT_FI_1, PS002372), PRINTS (GPRCRHODOPSIN, PR002734) and Pfam (7tm_1, PF00001). Drilling down into the partner databases, however, showed that the Pfam HMM matched 42,866 sequences, the PROSITE pattern had 2,213 true-positive matches, and 4,400 partial matches (6,660 in total) – a combined total short of 107,165. These figures are summarised in Table 5.4.

The situation is further complicated when InterPro 50 introduced a separate rhodopsin-like GPCR superfamily entry (IPR07452) that had 114,321 members, a figure derived from the PROSITE profile G_PROTEIN_RECEPT_FI_2 (PS05026). Visiting the PROSITE profile itself, however, revealed 2,433 true-positive matches, plus an 41 extra hits that hit many families. This diversity of numbers and the similar, yet different, superfamily appears baffling. Why are the numbers and the names different? What does it mean?

Explaining some of the numerical discrepancies is relatively straightforward. InterPro takes its partner database models and scales them against whatever is the current version of UniProtKB; but there is added twist – the way in which InterPro implements its algorithms differs from the way the partners implement them. Stepping aside this, the most important factor is likely to be which version of UniProtKB they used. As mentioned above, for the examples in Table 5.4, the quoted InterPro results were derived from UniProtKB 2015_02; the PROSITE pattern and profile were derived from UniProtKB/Swiss-Prot 2015_02; the PRINTS data, were derived from much older versions of Swiss-Prot (a composite of versions 55.0 and 38, respectively, with sequences tagged as fragments removed); the Pfam HMM was derived from UniProtKB 2012_06. What is clear that the the databases for PRINTS and PROSITE are significantly smaller than the source used by InterPro (note that PROSITE is based

# Table 5.4
Rhodopsin-like GPCRs in InterPro 50 and its source databases.

| G protein-coupled receptor, rhodopsin-like (IPR000276) 107,165 hits | GPCR, rhodopsin-like, 7tm (IPR017452) 114,321 hits |
|---|---|-|
| Pfam | 42,866 | |
| PROSITE pattern | 2,213 | |
| PRINTS | 6,660 | |
| PROSITE profile | | 2,433 (+41) |

> 41http://www.ebi.ac.uk/interpro/entry/IPR000276
42http://prosite.expasy.org/PS00237
43http://www.bioinfo.manchester.ac.uk/cgi-bin/dbdbrowser/PRINTS/DoPRINTS.pl?cmd_a=Display&qua_a=//
Full&fun_a=Code&qs=GPCRHODOPSIN
44http://pfam.xfam.org/family/pf00001
45http://www.ebi.ac.uk/interpro/entry/IPR017452
46http://prosite.expasy.org/PS00262