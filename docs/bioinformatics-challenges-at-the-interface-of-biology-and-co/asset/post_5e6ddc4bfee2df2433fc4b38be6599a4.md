
# Box 2.4 The process of transcription

Until now, we have talked only in very abstract terms about transcription, the process by which linear strands of RNA are synthesised from single-stranded DNA templates (Figure 2.13 (a)):

The biological event is mediated by an enzyme RNA polymerase. The enzyme binds to one of the two strands of the DNA template, referred to as the template strand, which is temporarily separated from the non-template strand during the process, as shown schematically in Figure 2.13 (b):

![](img/1af42ff402ef4720886c50af0bb8e9b5_50_0.png)

# **Figure 2.13**

- (a) DNA transcription.
- (b) Synthesis of RNA from a DNA template.

https://www.youtube.com/watch?v=WsofH46O6jk
https://www.youtube.com/watch?v=occnB8OtxmQ

The polymerase catalyses the assembly of individual ribonucleotides into a strand of RNA, which complements its DNA template. base pairs (bps) are formed between the template and the RNA strand; however, as the polymerase progresses, the RNA separates from the template, and the two DNA strands re-seat

RNA polymerase proceeds along the template in the 3' to 5' direction; therefore, the RNA is synthesised from 5' to 3'. For the process to work, the polymerase instructs where to start and stop; it gets this information from the DNA template, as shown in (b). The start signal is a short sequence of DNA bases (typically quite variant in genes), termed a promoter. The stop signal, terminator, often takes the form of a specific base sequence that contains a hairpin loop in the RNA structure. This inhibits progression of the polymerase and causes it to dissociate from the template.

Because the new RNA sequence is complementary to its DNA template, it is in fact the same as the non-template strand, but with one difference. When the template base is a C, T or G, the base added to the RNA strand is a G, an A or C, as we might expect. However, when the template base is A, a U is added to the RNA in fact of T. In RNA, we use U rather than T. So, when we think about the DNA sequence of a gene, we usually mean the non-template strand, because it is this sequence that is mimicked by the RNA, and it is this sequence that is subsequently translated into protein.

![](img/1af42ff402ef4720886c50af0bb8e9b5_51_0.png)

### Figure 2.14

Schematic illustration of the structure of mRNA: (a) in prokaryotes, the central coding region is flanked by 5' and 3' untranslated (UTR) regions; (b) in eukaryotes, the central region comprises exons and introns – introns must be excluded to create a functional transcript.

alternating elements exons and introns: exons are parts of a gene sequence that are expressed – i.e., that they are translated; introns are intergenic regions that are destined to be removed from the pre-mRNA, as illustrated in Figure 2.14. As introns are excluded, the ends of their flanking exons are joined together to form a continuous strand in a process called splicing (more details of this process are given in Box 2.5). To add complexity, for a given pre-mRNA, not all of the exons are needed in the final transcript. As a result, a single pre-mRNA can give rise to several different transcripts, or splice forms.

Incredibly, introns were not known before 1977 (Chow et al., 1977; Berget et al., 1977); their discovery was a breakthrough that led it to the award of the Nobel Prize in Physiology and Medicine to Philip Sharp and Robert in 1993. Without doubt, the genome still holds many secrets, and there is still much to discover about how its monotonous four-base code is transformed into the majestic poetry of proteins. Among many remaining mysteries is how splice sites are identified at introns by the boundaries which are known, which signals or sequences to remove. While aspects of the process are known (e.g., characteristic dinucleotides at the introns: guanine-uracil (GU) at the 5' end and adenine-guanine (AG) at the 3' end), the recognition sites are so small (and variable), and the precision of the process so exquisite, it's breath-taking to think how the process is orchestrated in practice; and it's hard to manage how nature does it, how hard it is to deduce the intron-exon structure of a gene computationally – not surprisingly, this is one of the main sources of error in gene prediction. This problem is compounded by the large number of introns in many eukaryotic genes (sometimes up to 20 in a single gene), which further increases the scope for error. Prokaryotes tend to present fewer problems: most of their genes don't contain introns, and their genes are smaller, making sequencing and gene finding much easier; however, there are many more eukaryotic genomes available today.

In eukaryotes, DNA is contained in the nucleus, and transcription and RNA process occur here. The processed mRNA is transported from the nucleus through the nuclear membrane, into the cytoplasm, where translation takes place. So, let's now think about how the chemical code of mRNA is translated into the corresponding protein code.

# Chapter 2 The biological context

# Box 2.5 RNA processing

We mentioned that eukaryotic gene sequences are generally more complex than their prokaryotic counterparts. As we saw, one of the principal differences between them is that eukaryotic sequences containing coding and non-coding regions, termed exons and introns. Therefore, to create a continuous sequence of nucleotides, the molecular machinery must excise the non-coding introns and zip together the exons. The RNA-processing step, known as splicing, is illustrated in Figure 2.15.

The process of splicing is mediated by a molecular 'machine' a complex of proteins and various types of RNA. Like the process of transcription, it makes use of sequences to tell where to start and stop which bits of the sequence to remove. splice signals are typically short, and the spliceosome recognizes them with far greater confidence than we can manage. Some introns can excise themselves from an RNA strand without requiring the spliceosome, such self-splicing introns are rare. The majority of introns in most organisms require the spliceosome and are here referred to as spliceosomal introns. Eukaryotic genes can contain large numbers of introns (e.g., up to 20 in one gene). By contrast, prokaryotic genes are intronless, making them much more tractable to computational analysis. ![](img/1af42ff402ef4720886c50af0bb8e9b5_52_0.png)

Figure 2.15 RNA processing.

https://www.dnalc.com/resources/3d/rna-splicing.html
https://www.youtube.com/watch?v=FVuAw8BG_pQ

## 2.2. The genetic code

The sequence of nucleotide bases in mRNA is read in groups of three: these triplet units are termed codons. As there are three positions and four bases to choose from, there are 64 permutations. Each codon encodes one amino acid; hence, as there are only 20 naturally occurring amino acids, most have more than one codon.

# Bioinformatics challenges at the interface of biology and computer science

| First position | U | C | A | G | Third position |
| :--- | :--- | :--- | :--- | :--- | :--- |
| U | Phe (F) | Ser (S) | Tyr (Y) | Cys (C) |
| | Phe (F) | | Ser (S) | Cys (C) |
| | | Leu (S) | | Stop | Stop |
| | | Leu (S) | Trp (W) | A |
| C | Leu (L) | | His (H) | Arg (R) | U |
| | Leu (P) | | His (H) | Arg (R) | C |
| | Leu (P) | | Glu (Q) | Arg (R) | A |
| | Leu (P) | | Glu (Q) | Arg (R) | G |
| I | Thr (T) | | Asn (N) | Ser (S) | U |
| | Ile (I) | | Asp (N) | Ser (S) | C |
| | Ile (I) | | Lys (K) | Arg (R) | A |
| | Met (M) | | Lys (K) | Arg (R) | G |
| G | Val (V) | Ala (A) | Asp (D) | Gly (G) | U |
| | Val (A) | | Asp (D) | Gly (G) | C |
| | Val (A) | | Glu (E) | Gly (G) | A |
| | | Ala (A) | | Glu (E) | Gly (G) | G |

Figure 2.16

Representations of the standard genetic code used in prokaryotic and the nuclear genomes of most eukaryotes. AUG serves the dual purpose of encoding methionine and indicating the start of the coding region: UAA, UAG and UGA function only as stop codons. The colours are the same as those in Figure 2.10, showing the clustering of amino properties.

How the 64 codons map to amino acids – an assignment known as the genetic code – is shown in Figure 2.16 (left- and right-hand panes). The heart of the table depicted in Figure 2.16 is divided into 16 sections, including the products of four different codons; each section shares the same two bases (e.g., the base in GU). In many cases, four codons encode the same amino acid – *i.e.*, the base in the third position has no difference.

Other sections contain two amino acids, depending on whether the third base is a pyrimidine or a purine. AAY codes *asparagine*, and AAR *lysine* (where Y and R, remember). *Leucine* has three codons, *serine* and *arginine* have six. Two amino acids have a single codon: *tryophan* (UGG) and *methionine* (AUG). Methionine is unique because its codon serves to denote the inclusion of this amino acid when it occurs within a sequence, and to indicate the specific point of the gene coding region; three have stop signals to terminate the coding region; however do not encode amino acids.

Fifty years ago, the genetic code was believed to be the same for all species. However, widespread, it turns out it’s not quite universal. The code depicted in Figure 2.1 applies to most prokaryotic genomes (bacterial and archaeal) and to the nuclear genomes of virtually all eukaryotes. Mitochondrial genomes, the nuclear genomes of some unicellular eukaryotes, and the genomes of some bacteria use different codes; the differences are small, and the bottom line is that the code is generally shared between the three domains of life: archaea, bacteria and eukaryotes.
