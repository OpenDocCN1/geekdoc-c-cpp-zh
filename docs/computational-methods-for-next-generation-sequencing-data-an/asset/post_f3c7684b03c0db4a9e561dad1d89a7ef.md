
# TABLE 15.4 Algorithms Performance on Average

| | MT | FS | RMSE | HD |
|---|---|---|---|--|
| Single-clone samples | | | | |
| ET | 0 | 0.29 | 0.24 | 0.5 |
| KEC | 0 | 0.14 | 0.12 | 0.178571 |
| SHORAH | 0 | 326.43 | 19.18 | 5.267445 |
| kGEM | 0 | 0.86 | 5.9 | 0.928571 |
| Mixture samples | | | | |
| ET | 0 | 0.00 | 0 | |
| KEC | 0.7 | 0.00 | 2.92 | 0 |
| SHORAH | 0.1 | 499.60 | 3.37 | 5.053398 |
| kGEM | 0 | 1.60 | 5.29 | 1.208333 |

MT, Missing true haplotypes; FS, false haplotypes; RMSE, mean square error of frequency estimations of haplotypes; HD, average distance to the closest true hapotype, averaged over all false haplotypes.

respectively. The accuracy of frequencies' estimation on single-clone samples was greater for ET and KEC than for kGEM. However, the accuracy of kGEM is greater than SHORAH. Analysis of Hamming distances between false haplotypes and their closest true neighbors shows that haplotypes retained by KEC, ET, and kGEM are genetically closer to true haplotypes than the ones obtained by SHORAH.

Thus, all algorithms are comparable in sensitivity, but showed marked differences in the specificity and accuracy of frequencies' estimation. It should be emphasized that ET is based on experimentally calibrated parameters for the particular region under consideration, while KEC, SHORAH, and kGEM are independent of such estimations and are more universally applicable. However, a solid performance of ET indicates that empirical evaluation of the error profiles for particular amplicons planned to be used in many studies is highly beneficial.

# REFERENCES

- 1. Hajarizadeh B, Grebly J, Dore GJ. Epidemiology and natural history of HCV infection. World J Gastroenterol Nat Rev Gastroenterol Hepatol 2013;10(9):553–562.
- 2. Kilmarx PH. Global epidemiology of HIV. Curr Opin HIV AIDS 2009;4(4):240–246.

# ERROR CORRECTION OF NGS READS FROM VIRAL POPULATIONS

- 3. Sanjuan R, Nebot MR, Chirico N, Mansky LM, Belshaw R Viral mutation rates. J Virol 2010;84(19):9733–9748.
- 4. Domingo E. Biological significance of viral quasispecies. Viral Hepatitis Rep 1996;2:247–261.
- 5. Duarte EA, Novella IS, Weaver SC, Domingo E, Holland JJ. Raina-Hobson S, Clarke DW, Moya A, Elena SF, de la Torre IC, Virus Quasispecies: significance for viral disease and epidemiology. Infect Agents D 1994;3(4):201–214.
- 6. Archer J et al. Analysis of high-depth sequence data for viral diversity: a comparison of next generation sequencing platforms using Segmentator II BMC Bioinformatics 2012;13:47.
- 7. Huse M, Huber JA, Morrison HG, Soglin ML, Welch DM. Accuracy and quality of massively DNA nanopsequencing. Genome Biol 2007;8(7):R143.
- 8. Gilles A, Megglez E, Pen N, Ferreira S, Malausa T, Martin J. Accuracy and quality assessment of 45 GS-FL Titanium nanopsequencing. BMC Genomics 2011;19(12):245.
- 9. Zagordi O, Daumer M, Beisel C. Read length versus depth of coverage for viral quasispecies. PLoS ONE 2012;7(10):e4746.
- 10. McElroy KC, Luciano F, Thomas T. GenSim: general, error-based simulator of next generation sequencing data. BMC Genomics 2012;13:74.
- 11. Harisendy O et al. evaluation of next generation sequencing platforms for targeted sequencing. Genome Biol 2009;10(3):R332.
- 12. Quaim M et al. A tale of next generation sequencing platforms: comparison of Ion Torrent, Pacific Biosciences and Illumina MiSeq sequencers. BMC Genomics 2012;13:341.
- 13. Bragg LM, Stone G, Butter M, Hugholtz P, Tyson GW. Shining a light on dark sequencing: characterizing errors in ion torrent PGA data. PLoS Comput Biol 2013;9(4):e100301.
- 14. Mardis E. Error correction for next generation sequencing methods. Rev Hum Human Gen 2008;9:387–402.
- 15. Skums P, Pimitrova D, Vaughan G, Ross L, Forbi J, Yokosawa J, Zelikovsky A, Khudakov Y. Error correction for next-generation sequencing of viral amplicons. BMC Genomics 2012;13:S106.
- 16. Dohm J, Locat C, Bordina T, Himmelbauer Substantial biases in ultra-short read data from high-throughput DNA sequencing. Nucleic Acids 2008;36(16):e105.
- 17. Campo C, Suks, Pimitrova D, Vaughan G, Forbi J, Theo C-G, Khudakov Y., Lau D. Drug-resistance of a viral genome and its individual intracellular variants during the 48 hours of therapy. Clin Pharm Thor 2014;95(6):627–635.
- 19. Luciani F, Alizon S. The evolutionary dynamics of a rapidly mutating virus and between hosts: the case of hepatitis C virus. PLoS Comput Biol 2009;5(11):e1000565.
- 20. Tazi L, Imamachi H, Hirshield S, Metcalf JA, Orsega S, Perez-Losa M, Posada D, Lane HC, Crandall KA. HIV-1 infected respectively.
- 21. Westby M, Lewis M, Whitcomb J, Pozniak M, Jenkins M, Shafer R, Al5 C. Evaluation of next generation sequencing of HIV-1 infected following treatment. Nature Communications 2010;1(5):10009–2052.

## COMPUTATIONAL METHODS FOR NGS DATA

- 22. Skumps P, Pimitrova D, Vaughan G, Forbi J, Theo C-G, Khudakov Y., Lau D. Numerical detection of mixed sample. Nature Communications 2011;18(5):263.
- 23. Zagori O, P,,,,,,,,... for for.... 22000011:140––609.
- 24. Zagori O, Klein R, Daumer M, Beer N. An efficient error detection and model algorithm. J Comput Biol 2010;17(3):417–428.
- 25. Zagori O, A A,,,,,, N.. novo:. Bioinformatics Bioinformatics. Bioinformatics22221111111111111.
- 26. Quince C, Lanzen A, Davenport R, Hall N, Sloan W. Accurate determination of from. Nature Methods 2009;6(9):639–641.
- 27. Quince C, Lanzen A, Davenport R. Removing noise from. Bioinformatics 2011;28(12):38.
- 28. Eriksson N, Pachter L, Mitsuya Y, Shafer R, Wang C. Viral population estimation by. PLoS Comput Biol 2008;4(4):e1004.
- 29. Artyomenko A,,,,,,,,. kGEM: An EM-based algorithm for local reconstruction. Computational Advances in Bio and Medical Sciences (IEEE), 33rd International.
- 30. Salmera L, Schröder J. Correcting errors in short reads by multiple alignments. Bioinformatics 2011;27(11):1455–1461.
- 31. Pevner T, Tang H, Waterman M. An Eulerian path to DNA assembly. Proc Natl Acad Sci U 2001;98(17):9478–9753.
- 32. Chaisson M, Binza D, Pevner P. De novo assembly with short-paired reads: does the read length matter? Genome Res 2009;19(2):336–346.
- 33. Zhao X, Palmer L, Bonanos R, Micrean C, Fasulo D, Wittenberg ED. An error detection and model algorithm for. J Comput Biol 2010;17(11):1549–1560.
- 34. Skumps P, Artyomenko A, Gleb O, Ramachander S, Mando I, Campo D, Dimitrova Z, Zelikovsky A. Computational framework for next-generation sequencing of heterogeneous viral populations by combinatorial pooling. Bioinformatics. 2014. DOI: 10.1093/bioinformatics/bt726.
- 35. Yang X, Dorm K, Alurn S. Reptile: representative tiling for short read error correction. Bioinformatics 2010;26(20):2526–2553.
- 36. Chaisson M, Pevner PA, Tang H. Fragment assembly with short reads. Bioinformatics 2004;20(13):2067–2074.
- 37. Butler J, Maccalum I, Kleber M et al. ALLPATHS: de novo assembly of whole-genome shotgun microreads. Genome Res 2008;18(5):810–820.
- 39. Comaniciu D, Ramesh V, Meer P. The variable bandwidth mean shift and data-driven scale selection. Proceedings of the 8th International Conference on Computer Vision: 2001. p 438–445.
- 40. Comaniciu D, Meer P. Mean shift: a robust approach toward feature space analysis. IEEE Trans Pattern Anal Mach Intell 2002;24:603–619.
- 42. Mathworks: Matlab. Natick, MA; 2010.
