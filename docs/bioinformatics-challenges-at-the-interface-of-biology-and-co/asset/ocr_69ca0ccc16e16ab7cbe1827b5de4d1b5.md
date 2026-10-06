# Chapter 3 Biological databases

RCSB remains the 'archive keeper', with sole write-access to the PDB, controlling its contents, and distributing new PDB identifiers (IDs) to all deposition sites.

In November 2015, the PDB holdings^9 amounted to 114,000 structures of these; ~106,600 structures deduced primarily by X-ray diffraction, Magnetic Resonance (NMR) spectroscopy and electron microscopy; the rest were structures of nucleic acids and nucleic acid-protein complexes, and of carbohydrates. This is much larger than the structures deposited in the PDB 44 years earlier; nevertheless, growth of the resource has been slower than might have been predicted in the wake of high-throughput structure determination. In fact, it became apparent that high-throughput studies fought with difficulties, and the experimental pipelines had high attrition rates (Yon and Jothi, 2003); for example, some proteins couldn't be purified in sufficient quantities to use; of those that could be purified, some remained disorderly; and, of those that did crystallise, some poor quality crystals that would produce diffraction patterns. Consequently, the rate of high-throughput structure determination didn't match the original projections, and the initial early years of the PSI produced fewer than 3,000 structures^10.

As you now know, the total figure of ~106,600 protein structures mentioned above includes a considerable amount of redundancy. We can get an index of how much redundancy by clustering PDB's contents by sequence identity. Table 3.3 shows the result of this for the November 2015 holdings. At 30 per cent identity, there are ~24,000 clusters; even at this level, many of the proteins will still have the same fold, because proteins are more conserved than their sequences. More rigorous studies, using the fold-classification databases as benchmarks, show that the number of unique folds in the PDB is currently somewhere between 1,300 and 1,400 (see Box 3.1 for further details).

Even if we consider the full redundant figure, the number of structures is very small relative to the number of known protein sequences — or, to put this another way, the sequence–structure deficit is large (see Figure 3.3). This means that, at the time of writing, there is still no 3D information available for most proteins.

# Table 3.3

Sequence-based redundancy in the PDB*, November 2015,
calculated using the commonly used pairwise alignment algorithm, BLAST (Altschul et al., 1990).

| % identity | # clusters |
| 100 | 63,995 |
| 90 | 42,812 |
| 70 | 37,915 |
| 50 | 32,610 |
| 40 | 28,889 |
| 30 | 24,601 |

> ^9http://www.rcsb.org/pdb/statistics/holdings.do

> ^10https://commons.wikimedia.org/wiki/File:PSI_chart_numStructures-vs-time.PNG