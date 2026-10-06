# Chapter 5 The gap

certainly no doubt about rhodopsin and its associates – they may share
a 7TM scaffold, but they are not G protein-coupled receptors. Adding to the muddle,
is is acknowledged in the annotation of entry IPR017452, which states that it ‘spans
the transmembrane membrane regions of rhodopsin-like GPCRs. It also identifies some
ceptors, including a number of taste receptors and vomeronal recep-
tors’. Invitably, this has near-consequences, for automatic annotation
pipelines, which have led thousands of UniProt/KB sequences to be
rather ambiguous ‘GPCR, rhodopsin-like, 7TM’ description as a result. This is a classic
illustration of the dangers of blurring protein sequence/structure/boundaries
without reference to the underlying biology.

If the situation for this one GPCR superfamily is confounding, what convo-
olds might we find for other members of the GPCR family? In December 2015, a
search of InterProt with keyword ‘GPCR’ yielded 120 matches, including ‘GPCR,
family 2-like (IPR017983⁸), GPCR, family 2, secretin receptor (IPR002144⁹),
GPCR, family 3, secretin-like (IPR008325⁰), family 2, secretin-like,
estestingly, no overarching ‘GPCR family 2 – given this small sample, we may be
the relationships between the sequences within the wider limit will not be
simple to ascertain.

Part of the problem is that databases have become dependent on automatic
search tools; most not have time to annotate the results in detail to be able
relate them to the underlying biology, especially when families and superfamilies
are large, like the GPCRs. Here once, for example, the class Pfam lists
do not map all to the families listed in PRINTS and PROSITE,
discord between them has resulted in disparities in InterProt, similar to
t one discussed above for rhodopsin-like GPCRs. To understand the evolut-
y relationships for this important group of receptors, we really need to consult
more detailed analyses, such as those of Nordstrom et al. (2009), to put
results on a more solid biological footing.

Before leaving this, there is another important point to note, which relates
to back to our discussion in Section 5.4 nomenclature. InterProt refers to its ‘G
protein-coupled receptor, rhodopsin-like’ entry as a, and to its ‘GPCR, rho-
dopsin-7tm’ entry as a domain. Pfam, on the other, refers to 7tm_1
entry as a family. PRINTS entry to a superfamily, and
Prot refers to the sets of sequences identified by G_PROTEIN_RECEPT-
F_1 and G_PROTEIN_2 pattern and profile entries as families.
Hence, for arguably the same biological concept (the group of sequences that have
himilarity to rhodopsin-like GPCRs), four different databases use three
terms: family, superfamily and domain. And, just to add a bit of nomenclature,
Pfam names the class that encompasses 7tm_1 and the 35 other ‘families’ shown in
Table 5.5, as Family A G protein-coupled receptor-like superfamily’, using
tree different terms within the same concept. Teaching computers what we humans
understand by the term ‘family’ is therefore considerably more difficult than we
might expect.

+   ⁸http://www.ebi.ac.uk/interprot/IPR017983
⁹http://www.ebi.ac.uk/interprot/IPR002144
⁰http://www.ebi.ac.uk/interprot/IPR008325
¹¹http://www.ebi.ac.uk/interprot/IPR017983