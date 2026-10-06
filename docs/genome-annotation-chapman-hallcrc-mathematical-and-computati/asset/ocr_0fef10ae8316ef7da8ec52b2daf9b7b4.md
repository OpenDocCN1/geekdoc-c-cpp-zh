# Coding Sequence Prediction ■ 15

and consists of seven nucleotides. The first two nucleotides of the BRE sequence are either G or C, followed by either G or A. The last four nucleotides are CGCC. Transcription factor IIB (TIIB) binds in the major groove of the DNA at the BRE.

# 2.3.4 TATA Box

In prokaryotes, the TATA box is known as the Pribnow box, or the -10 signal, because it is usually centered 10 bases upstream of the start codon. Although there is TATAAT consensus (Pribnow, 1975), it is not universal. More important is that the region is rich in adenine and threonine bonds. Together with the -35 signal, these patterns provide suitability for transcription initiation. It is common to observe multiple candidate start initiation sites, due to the short length and variability of the -10 and -35 signals, therefore the predicted patterns and their putative locations are mostly used to support rather than define the start of the coding sequence.

In eukaryotes, the TATA box is only one of possible initiation factors. Core promoters, such as the initiator element (Inr), the GC box, or the CAAT box can replace or augment the eukaryotic TATA box. Other initiation elements specific to particular genes and tissue types are not generally used for statistical prediction of genes due to their rarity.

# 2.3.5 Ribosomal Binding Site

The Shine–Dalgarno sequence (Shine and Dalgarno, 1975) represents the ribosomal binding site (RBS) in prokaryotes and hence the start of translation. It is usually situated within eight pairs of the start codon. It is specific, determined by the reverse complement of the 16S RNA's 3' end, and may contain mismatches (Schurr et al., 1993). Not every gene necessarily starts with an RBS, but each transcript should. This means that scores for genes in the middle of an operon (also known as polycistronic transcripts) should not be penalized for having one.

In eukaryotes, the ribosomal binding site is referred to as the Kozak sequence (Kozak, 1986). This site does not have as strong a consensus as in prokaryotes (is not derived from the 18S rRNA), and it overlaps rather than precedes the start codon. Because of this overlap, the start codon begins at +1, and the immediate 5' base position is -1. The consensus sequence varies from species to species; therefore proper detection requires a training data set.