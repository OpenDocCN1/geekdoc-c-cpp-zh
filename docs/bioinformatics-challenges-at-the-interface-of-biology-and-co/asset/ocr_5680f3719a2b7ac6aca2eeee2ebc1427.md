resolutions varying from 1.5 to 3.0 Å. So when we talk of the ‘structure of myosin’, it’s imperative to be clear which structure we really mean – if we don’t know, a computer will find it very hard to ‘guess’.

# 5.8 Problems with alignments

So far in this chapter, we've been looking at some of the issues relating to nomenclature, database IDs and AC#, database entry versions, and structure variants, and so on. Here we begin to touch on slightly more abstract problems. In the field of protein sequence analysis, a common task is to compare sequences by creating an alignment of some sorts. This stands straightforward, from the necessary input and output formats, to the underlying alignment algorithms, to the ways in which we visualise and interpret the results. Let’s take a closer look.

# 5.8.1 Different methods, different results

Alignments can be made using different software tools, with different algorithms and different input parameters (scoring matrices, gap penalties, etc.); their outputs can be visual in many different ways. What does ‘alignment’ really mean? We can explore this by examining the results in Figure 5.5, which shows alignments of eight receptor sequences: known as GPCRs (OPDS, ACM1, OPRM, C5AR); others are thought to be at same in the time as (GP153, GP162, UL78, Q32393), most likely because they contain hydrophobic, possibly membrane-spanning regions (see Box 5.2). A FASTA-format file containing these sequences was input into three online alignment tools (ClustalW, T-Coffee, Multain) with default parameters, and to a desktop application (MUSCLE) that provides options to align sequences using MUSCLE plugin. The size of the outputs, only part of each alignment is in Figure 5.5.

The first note is that the alignments differ in several respects – here we represent them more-or-less as provided by the programs

The tools used for the purpose of this illustration were fairly randomly – they don’t reflect an endorsement of superiority or inferiority of any one over other. Many other alignment tool exists, either as desktop applications or as online