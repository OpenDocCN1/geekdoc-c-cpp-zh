
## Bioinformatics challenges at the interface of biology and computer science

compared to ~150,000 structures in the ASD (which is this unfair comparison, as small-molecule structures present fewer obstacles to structure determination than proteins and nucleic acid complexes). Perhaps a more pressing highlighted by the 1977 holdings that the database was beginning to accrue a significant amount of redundancy – by 1992, this was calculated to be ~7-fold (Berman, 2008; Hobohm et al., 1992). This redundancy was an inevitable consequence of the nature of structural research.

Structural studies are immensely valuable. For example, they've shown that the physical similarities shared by some proteins reflect common descent during evolution, during which mutations (substitutions, insertions and/or deletions) have accumulated in their sequences. For distant proteins, such mutations can be extensive, yielding folds in which the numbers and orientations of structures vary considerably, while basic scaffolds nevertheless act to preserve the structural environments of critical functional or active-sites. The diversity and elegance of such protein scaffolds has been captured in a number of fold-classification databases, which are described in more detail in Box 3.1.

### Box 3.1 Structure classification databases

The PDB is highly redundant. This is largely because of the nature of scientific research, which increases our knowledge by repeating detailed analyses of the same system until its intricacies are understood. The earliest protein structures to have been deduced (i.e. from myosin and hemoglobin) have therefore been determined, in order to better resolve their atomic structures and to learn more about the biological and biochemical mechanisms they use to effect their molecular functions.

By rationalising the structural data we have at our disposal, we can begin to put in suitable foundations from which to refine our understanding of structural principles – it turns out that nature use only a limited 'representation' of folds from which to build its portfolio of protein architectures (i.e., the method used is highly redundant too). Some of the systematic approaches to rationalise the structural data have yielded folds (for use in structure prediction and/or data-mining methods) and more comprehensive fold-classification databases, like SCOP and CATH. These groups share common folds and domains; however, in so they use different hierarchical approaches. Let's take a look.

The SCOP (Structural Classification Of Proteins*) hierarchy attempts to classify proteins into evolutionary and structural relationships. This task is complicated by the fact that protein structures are highly diverse; some comprise only single domains, while others are multidomain assemblies (hence, some are classified as individual domains and as multidomain proteins). This isn't an exact instance, of course, and so algorithms for comparing structures can't always capture the complexities completely; SCOP employs both manual and automated methods.

SCOP's hierarchy has three levels: family, superfamily, fold. The boundaries between these may be subjective, but higher levels generally reflect the clearest structural:

- 1. at the family level are proteins that >30% per sequence identity;
- 2. at the superfamily level are proteins that are believed to share a common evolutionary origin based on structural functional characteristics, but rather on moderate sequence identity;
- 3. at the fold level are proteins that have the same organisation of secondary structures, irrespective of their evolutionary origins (i.e. regardless of the mechanisms of divergence or convergence).

> *http://scop2.mrc-lab.cam.ac.uk

## Chapter 3 Biological databases

CATH stands for Class, Architecture, Topology, Homology; its classification strategy differs in several ways from that of SCOP most notably, its hierarchy derives from a domain-based classification and the database is derived largely by manual inspection (with the caveat that manual inspection is necessary when the processes fail). Despite, CATH's hierarchy has five levels:

1. Class describes the secondary-structure content in terms of four broad classes: mainly-α, mainly-β, α-β (containing either α or β elements), and low secondary-structure content;
2. Architecture describes the overall shape of the tertiary using simple descriptive terms like barrel, roll, sandwich, etc., but does not concern the connectivity of the consequent secondary-structure elements (hence, similar architectures may have different topologies);
3. Topology organizes architectures based on the connectivity of secondary structures (hence, proteins at the topology level have the same number and arrangement of secondary structures and the same connectivity);
4. Homology then groups that are more than 35% percent sequence identity, and whose high level of structural and functional similarity suggests evolutionary ancestry, and
5. Sequence follows clusters in those groups that have significant similarity or are identical (e.g., the same protein found in one or more families per homologous group).

By analogy with the EC (Enzyme Classification) system, CATH notation assigns a 4-number (not!) to code each protein domain, which prevents parsing of the database and renders it more attractive for computational manipulation.

Interestingly, SCOP and CATH have been used to estimate the number of unique folds represented by protein in the PDB. As shown in Figure 3.1 for CATH, the RCSB provides-over-year statistics to illustrate the growth of the PDB in terms of the annual number of unique folds contributed to the database (red bars) - cumulative figures are shown in blue. As is apparent from Figure 3.1, no new folds have been made for structures published since 2009, and the cumulative total is now -1,300.

![](img/1af42ff402ef4720886c50af0bb8e9b5_72_0.png)

Figure 3.1

PDB growth statistics.
Source: Protein Data Bank.

This is particularly fascinating from the perspective of the Protein Structure Initiative (PSI), which partly sought to tackle PDB's redundancy issues by targeting novel structures. Nevertheless, the number of unique folds entering the database did not significantly increase in the 8–10 years following the start of the PSI in 2000, and, as we can see, has remained zero since 2009.

> bhttp://www.cathdb.info
http://www.rcsb.org/pdb/statistics/contentGrowthChart.do?content=fold-cath

Structural studies have also revealed that the similarities shared by some proteins reflect convergent evolution from unrelated ancestors, as a result, say, of physical principles that favour particular arrangements and fold topologies. The investigations of these phenomena have driven structural biologists to study the miniae of proteins from many different perspectives. Once elucidated, a structure becomes a kind of starting point from which atomic details may be refined through repeated structure determinations, and new molecular insights gained by replicating the analysis with the protein to its cognate ligand, or with the introduction of a particular mutation, so on. Consequently, with many variations, have been deposited in the PDB. Therefore, as the resource evolved, its contents have been skewed by a handful of well-studied proteins, like hemoglobin, immunoglobins, lysoymes and so on.

Returning to the evolution of the PDB, in 1996, a new database of macromolecular structures was created, the E-MSD (Boutelikakis et al., 2003), at the newly established European Bioinformatics Institute (EBI) in the UK. Building upon PDB data, E-MSD was originally conceived as a pilot study to explore the feasibility of using relational databases to manage structural data more effectively. As it turned out, the prototype database emerging from the pilot was successful in its right, and the E-MSD consequently established as a major EBI resource.

During this period, a concerted effort was made to hasten the pace of knowledge acquisition from structural studies. This was partly motivated by the desire to augment the still-limited number of structures available in the PDB, but also partly to merge the redundancy. The answer was to establish a program of high-throughput X-ray crystallography in a high-profile venture known as the Structure Initiative (Burley et al., 1999). Several feasibility studies had already been launched; coupled with the broad-spanning vision of the PSI (which was gearing up to produce 10,000 new structures over the next ten years), the first indications that coping with high-throughput structure-definition pipelines would require many ways of gathering, storing, distributing and 'servicing' the data to end users.

One of the PDB's responses to this, and to the many challenges that lay ahead, was to form a new management structure. This was embodied in a three-membered Research Collaboration for Bioinformatics (RCSB), a consortium including Rutgers, The State University of New Jersey; the San Diego Supercomputer Center at the University of California; and the Center for Advanced Research in Biotechnology of the National Institute of Standards and Technology (Berman et al., 2000; Berman et al., 2003). With establishment of this consortium, the Brookhaven PDB ceased operations, and the RCSB formally took the helm on 1 July 2009.

With the RCSB in the USA, the E-MSD established in Europe, and a resource (PDB) subsequently announced in Japan (Nakamura et al., 2002), structure-collection efforts had taken on an international dimension. As a result, three repositories were brought together beneath an umbrella organisation as the world-wide Protein Data Bank (wwPDB), to harmonise their activities and maintain a single, publicly available archive of macromolecular data (Berman et al., 2003). By 2009, perhaps to align its nomenclature in a more obvious way with its consortium partners, E-MSD was re-named PDBe (Velankar et al., 2009). Today, the
