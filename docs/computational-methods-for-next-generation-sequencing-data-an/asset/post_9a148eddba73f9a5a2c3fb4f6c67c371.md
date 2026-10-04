
# 48 COMPUTATIONAL METHODS FOR NGS DATA ANALYSIS

![](img/46aec008551cecb3bbf3aac2ee69b926_69_0.png)

![](img/46aec008551cecb3bbf3aac2ee69b926_69_1.png)

![](img/46aec008551cecb3bbf3aac2ee69b926_69_2.png)

Figure 2.13 R products. Shared and unique pathways can be identified using a Venn diagram. (b) Hierarchical clustering or (c) dimensionality reduction methods such as PCA or NMDS can be used to determine the extent to which pathway profiles are shared between environmental samples. The grid visualizations framework ggplot2 can be used to create a wide variety of plots based on the Grammar of Graphics framework. In (b), pathways have been declined to the second level of the MetaCyc hierarchy. The areas of each circle indicate pathway abundance. Please see www.wiley.com/go/Mandoit/NextGenerationSequencing for a color version of this figure.

# ANALYSIS OF ENVIRONMENTAL SEQUENCE INFORMATION USING METAPATHWAYS

when comparing multiple data sets as the number of nonempty sets is 2ⁿ – 1, where n is the total number of sets to compare.

# 2.5.5 Clustering and Relating Samples by Pathways

ORF counts across predicted pathway profiles for multiple samples provides another common analysis mode amenable to hierarchical clustering. A distance or similarity measure is used to iteratively group samples together generating hierarchical groups (Figure 2.13b). A point to consider is the distance measure and data transform being used, environmental data sets often have many zero entries (the-called double-zero problem) and a wide range of observed count data. To deal with these problems, different similarity measures such as Manhattan distance or Bray–Curtis similarity have been adopted to focus on differences of observed nonzero data, the log or square-root transforms are used and measures can be conducted using heust and pvclust packages in R, with bootstrapped samples providing a measure of statistical confidence in resulting cluster groups (46, 95).

Another way to highlight similarity or differences between environmental data sets involves dimensionality reduction techniques such as PCA or non-multidimensional scaling (NMDS) (Figure 2.13c). Intuitively one can think of PCA as being motivated from the fact that all multidimensional data can be viewed as a high-dimensional space. PCA rotates and shifts this ellipse such that the longest axis, the first principal component, aligns with the direction of highest variance in the data, the next components following orthogonally along this first axis. NMDS takes objects in a high-dimensional space while maintaining their relative distances and places them in a lower dimensional space while maintaining their relative distances as much as possible. A number of operational settings needs to be considered when generating PCA and NMDS plots, the details of which are beyond the scope of this chapter. Readers are encouraged to familiarize themselves with ordination and dimensionality reduction techniques described in numerical ecology texts (96–98).

# 2.5.6 Faceting Variables with ggplot2

Finally, another approach to analyzing environmental sequence information is to isolate subsets of pathways in relation to specific physical, chemical, or process variables, a process known as faceting. Two frameworks for doing this in the R statistical environment are ggplot2 and lattice (47, 99), allowing subsets of data to be displayed in small multiple plots based on user-defined variables. ggplot2 in practice is a full-featured and flexible framework based on the principles outlined in the Grammar of Graphics (100), which is able to automatically construct variety of data plots based on drawing primitives, including bar plots, heatmaps, bubble plots, and so on. Readers are encouraged to familiarize themselves with this framework in more detail given its ability to produce publication quality figures.

In this chapter, we presented conceptual and contemporary methods for analysis of environmental sequence information using MetaPathways. Beginning with methods for ORF prediction and annotation using an ever-growing ecosystem of algorithms and reference databases, we described taxonomic and functional gene profiling using the LCA algorithm and MLTreeMap and the construction and exploration of cPGDBs using Pathway Tools before presenting comparative analysis methods in the R statistical design and iterative development of MetaPathways focus a spotlight on Big Data challenges associated with environmental sequence analysis. These include computationally intensive steps related to scalable seed-and-extend searches, data integration across multiple information levels, and interactive visualization of embarrassingly large datasets. We highlighted recent innovations including a grid and cloud distribution system, GUI, and Knowledge engine that integrates millions of functional and taxonomic annotations across multiple samples. Future versions of MetaPathways will be built on distributed computing and interactive visualization themes and append modules for single-cell genomic and population genome assembly and binning. At the same time, parallel improvements to import/export features of Pathway Tools to enhance Cellular Overview and Omics data features enabling more effective metabolic pathway reconstruction and comprehensive community analysis.

# REFERENCES

- 1. Whitman AW, Coleman DC, Wieje WJ. Prokaryotes: the unseen majority. Proc Natl Acad Sci U A 1998;95(12):6578–6583.
2. Falkowski PG, Fencil T, Delong EF. The microbial engines that drive Earth’s biogeochemical cycles. Science 2008;320(5879):1034–1039.
3. Hanson NW, Kamley AK, Altman T, Karp PD, Hallam SJ. Metabolic pathways for the whole community. BMC Genomics 2014;15:619.
4. Delong EF, Preston CM, Ticher R, Hallam SJ, Frigaard N U, Martinez A, Sullivan MB, Edwards R, Brito BR,cosh SW, Karl DM. Community genomics from stratified microbial assemblages in the ocean. Science 2006;311(5760):496–503.
5. Walsh DA, Zaikova E, Howes CS, Song YG, Tortell PD, Hallam SJ. Metagenome of a versatile autotroph from oceanic dead zones. Science 2009;326(5952):578–582.
6. Shi Y, Tyson GW, Willey JP, Delong EF. Integrated metagenomic and metagen analyses of stratified microbial assemblages in the open ocean. ISME J 2011;5(4):999–1013.
7. Fier N, Jackson RB. The diversity of soil bacterial communities. Proc Natl Acad Sci U 2006;103:626–631.
8. Warnecke F, Laughlin P, Ivanova N, Ghemassian M, Richardson T, Stege JT, McHardy A, Djordvic G, Abous N, Sorek R, Kunin V, Dale D, Kirton E, Platt D, Salamov A, Barry K, Mikhail N, Kiev MC, Maton EG, Ottesen EA, Zhang X, Hernández M, Murillo C, Acosta LG, Green DB, Chang C, Rubin EM, Mathur EJ, Robertson DE, Leadbetter RJ. Metagenomic and functional analysis of hidden microbiota of a wood-feeding termite. Nature 2007;450(7169):560–565.
9. Yooseph S, Sutton G, Rush DB, Alpern AL, Williams SJ, Rijmann K, Eisen JA, Heldberg KB, Manning GL, Li W. Global Ocean: expanding the universe of protein families. PLoS Biol 2007;5(3):e16.
10. Tyson GW, Jackman J, Hahn P, Allen EE, Richardson PM, Solovy VV, Rubin EM, Roskar DS. Community structure and metabolism through reconstruction of microbial genomes from the environment. Nature 2004;428(6978):37–43.
11. Turnbaugh J, Ley RE, Hamady M, Fraser CM, Knight R, Gordon JI. The human microbiome project. Nature 2007;449(7164):804–810.
12. Abubacker S, Sega N, Goll J, Schubert AM, Izard J, Cantarel BL, Rodriguez-Mueller B, Zucker J, Thiagarajan M, Henrissat B, White O, Kelley ST, Mete B, Schless PD. Reconstruction for metagenic data and its application to the human microbiome. PLoS Biol 2012;8(6):e10258.
13. Alcalde M, Ferrer M, Plow FJ, Ballester A. Environmental biocatalysis: remediation with novel green processes. Trends Biotechnol 2006;24(6):281–287.
14. Human Microbiome Project Consortium. Structure, function and diversity of the human microbiome. Nature 2012;486(7402):207–214.
15. Cho I, Blaser MJ. The human microbiome: at the interface of health and disease. Nat Genet 2012;13(4):260–270.
16. Taupp M, Mew K, Hallam SJ. The art and design of metagenomic transformations. Curr Opt Biotechnol 2011;22(3):465–472.
17. Kewis M, Armstrong Z, Waldin SA, Withers SJ, Iydomenko K, Budwill K, Moon WW, Elts SD. Biomining active cellulases from a mine bioremediation system. J Biotechnol 2013;16(4):462–471.
18. Strach C, Ring V, Vanisberghe R, Iydomenko K, Budwill K, Hallam SD. Metagenomic scaffolds enable long-term binning transformation. Nat Acad Sci U 2014;111(28):10143–1048.
19. Margues M, Ehm L, Mann W, Atiyah S, Jaders B, Besem BL, Berka J, Braverman Y, YJ, Chen Z, Devell SB, Du L, Fier JM, Godwin WC, He W, Helen S, Hol CH, Irk ZP, Gando S, Alenquer MJ, Jarvis TP, Jarge KB, Kim BJ, Knight JR, Lanza N, Leamon JK, Leifwit MC, Mei L, Li J, Lohman KL, Lu H, Makhiani V, McCabe E, McKenna P, Myers EW, Erickson E, Noble JR, Park BC, Bon RP, Roth KT, Gartis SJ, Janis JF, Simpson SJ, Yoon S, Wang H, Weiner Y, Yu P, Begley RF, Rothberg JM. Genome sequencing in microfactified high-density polycitore reactors. Nature 2005;437(7075):376–380.
20. Qu M, Maizhera I, Smith F, Scallop A, Stephens J, Durbin S, Swardley H, Turner DJ. A large genome center’s improvements to the Illumina sequencing system. Nat Meth-2008;5(12):1005–1010.
21. Leung K, Hahn H, Leave T, Kon KW, Han NW, Pag AP, Lo CC, Chain PS, Hallam SJ, Hansen CL. A programmable droplet-based microfluidic device to multiparameter analysis of single microbes and microbial communities. Natl Sci U S 2012;109(20):7665–7670.
22. Bayley H. Nanotechnology: holes with an edge. Nature 2010;467(7312):164–165.
