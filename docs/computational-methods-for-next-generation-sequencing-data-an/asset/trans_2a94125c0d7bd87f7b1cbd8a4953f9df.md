

# 表 15.4 算法的平均性能 

| | MT | FS | RMSE | HD |
|---|---|---|---|--|
| 单克隆样本 | | | | |
| ET | 0 | 0.29 | 0.24 | 0.5 |
| KEC | 0 | 0.14 | 0.12 | 0.178571 |
| SHORAH | 0 | 326.43 | 19.18 | 5.267445 |
| kGEM | 0 | 0.86 | 5.9 | 0.928571 |
| 混合样本 | | | | |
| ET | 0 | 0.00 | 0 | |
| KEC | 0.7 | 0.00 | 2.92 | 0 |
| SHORAH | 0.1 | 499.60 | 3.37 | 5.053398 |
| kGEM | 0 | 1.60 | 5.29 | 1.208333 |

MT, 缺失真实单倍型；FS, 错误单倍型；RMSE, 单倍型频率估计的均方误差；HD, 到最近真单倍型的距离，对所有错误单倍型取平均值。

分别为。在单克隆样本的频率估计上，ET 和 KEC 的准确性高于 kGEM。然而，kGEM 的准确性高于 SHORAH。对错误单倍型与其最近真邻居之间的汉明距离分析表明，KEC、ET 和 kGEM 保留的单倍型在遗传上比 SHORAH 获取的更接近单倍型。

因此，所有算法在敏感性上具有可比性，但在特异性和频率估计准确性方面表现出显著差异。需要强调的是，ET 是基于针对特定区域的实验校准参数，而 KEC、SHORAH 和 kGEM 则不依赖于此类估计，更具通用性。然而，ET 的稳健性能表明，对计划在许多研究中使用的扩增子进行误差谱的实证评估是有益的。

# 参考文献

- 1. Hajarizadeh B, Grebly J, Dore GJ. HCV 感染的流行病学和自然史。World J Gastroenterol Nat Rev Gastroenterol Hepatol 2013;10(9):553–562.
- 2. Kilmarx PH. HIV 的全球流行病学。Curr Opin HIV AIDS 2009;4(4):240–246.

# 病毒群体 NGS 测序读取纠错

- 3. Sanjuan R, Nebot MR, Chirico N, Mansky LM, Belshaw R 病毒突变率。J Virol 2010;84(19):9733–9748.
- 4. Domingo E. 病毒准物种的生物学意义。Viral Hepatitis Rep 1996;2:247–261.
- 5. Duarte EA, Novella IS, Weaver SC, Domingo E, Holland JJ. Raina-Hobson S, Clarke DW, Moya A, Elena SF, de la Torre IC. 病毒准物种：对病毒疾病和流行病学的意义。Infect Agents D 1994;3(4):201–214.
- 6. Archer J et al. 病毒多样性高深度序列数据分析：使用 Segmentator II 的下一代测序平台比较。BMC Bioinformatics 2012;13:47.
- 7. Huse M, Huber JA, Morrison HG, Soglin ML, Welch DM. 大规模 DNA 纳米测序的准确性和质量。Genome Biol 2007;8(7):R143.
- 8. Gilles A, Megglez E, Pen N, Ferreira S, Malausa T, Martin J. 45 GS-FL Titanium 纳米测序的准确性和质量评估。BMC Genomics 2011;19(12):245.
- 9. Zagordi O, Daumer M, Beisel C. 病毒准物种的读取长度与覆盖深度的关系。PLoS ONE 2012;7(10):e4746.
- 10. McElroy KC, Luciano F, Thomas T. GenSim: 通用的基于误差的下一代测序数据模拟器。BMC Genomics 2012;13:74.
- 11. Harisendy O et al. 用于靶向测序的下一代测序平台评估。Genome Biol 2009;10(3):R332.
- 12. Quaim M et al. 下一代测序平台：Ion Torrent、Pacific Biosciences 和 Illumina MiSeq 测序器的比较。BMC Genomics 2012;13:341.
- 13. Bragg LM, Stone G, Butter M, Hugholtz P, Tyson GW. 黑暗测序之光：ion torrent PGA 数据中的误差特征。PLoS Comput Biol 2013;9(4):e100301.
- 14. Mardis E. 下一代测序方法的纠错。Rev Hum Human Gen 2008;9:387–402.
- 15. Skums P, Pimitrova D, Vaughan G, Ross L, Forbi J, Yokosawa J, Zelikovsky A, Khudakov Y. 病毒扩增子下一代测序的纠错。BMC Genomics 2012;13:S106.
- 16. Dohm J, Locat C, Bordina T, Himmelbauer. 高通量 DNA 测序超短读取数据中的显著偏差。Nucleic Acids 2008;36(16):e105.
- 17. Campo C, Suks, Pimitrova D, Vaughan G, Forbi J, Theo C-G, Khudakov Y., Lau D. 治疗 48 小时内病毒基因组及其个体细胞内变异性。Clin Pharm Thor 2014;95(6):627–635.
- 19. Luciani F, Alizon S. 快速突变病毒与宿主间的进化动力学：丙肝病毒的案例。PLoS Comput Biol 2009;5(11):e1000565.
- 20. Tazi L, Imamachi H, Hirshield S, Metcalf JA, Orsega S, Perez-Losa M, Posada D, Lane HC, Crandall KA. 分别被 HIV-1 感染。
- 21. Westby M, Lewis M, Whitcomb J, Jenkins M, Shafer R. 感染 HIV-1 的下一代测序。

## NGS 读取数据的计算方法

- 22. Campo C, Suks, Pimitrova D, Vaughan G, Forbi J, Theo C-G, Khudakov Y., Lau D. 混合样本的显著偏差。Nature 2011;18(5).
- 23. Zagori O, Daumer M, Beisel C. 用于混合样本的重构。Bioinformatics 2002;24:609.
- 24. Zagori O, Daumer M, Beisel C. 基于 EM 算法的误差检测。J Comput Biol 2010;17(3).
- 25. Zagori O, Daumer M, Beisel C. 消除比对消除噪声。Bioinformatics 28.
- 26. Quince C, Lanzen A, Davenport R, Hall N, Sloan W. 通过多重比对消除噪声。Nature Methods 2009;6(9).
- 27. Quince C, Lanzen A, Davenport R, Hall N, Sloan W. 消除噪声。Bioinformatics 2011;27.
- 28. Eriksson N, Pachter L, Mitsuya Y, Shafer R, Wang C. 病毒群体的估计。PLoS Comput Biol 2008;4(4).
- 29. Artyomenko A, Gleb O, Ramachander S, Mando I, Campo D, Dimitrova Z, Zelikovsky A. 组合池化的下一代测序计算框架。Bioinformatics 2014.
- 30. Salmera L, Schröder J. 短读取的纠错。Bioinformatics 2011;27(11).
- 31. Pevner T, Tang H, Waterman M. DNA 组装的欧拉路径。Proc Natl Acad Sci U 2001;98(17).
- 32. Chaisson M, Binza D, Pevner P. 使用短双对进行从头组装：长度重要吗？Genome Res 2009;19(2).
- 33. Zhao X, Palmer L, Bonanos R, Micrean C, Fasulo D, Wittenberg ED. 误差检测和模型。J Comput Biol 2010;17(11).
- 35. Yang X, Dorm K, Alurn S. Reptile: 用于短读取纠错的代表性平铺。Bioinformatics 2010;26(20).
- 36. Chaisson M, Pevner PA, Tang H. 短片段组装。Bioinformatics 2004;20(13).
- 37. Butler J, Maccalum I, Kleber M et al. ALLPATHS: 全基因组鸟枪法微读取的从头组装。Genome Res 2008;18(5).
- 39. Comaniciu D, Ramesh V, Meer P. 变带宽均值偏移和数据驱动尺度选择。Proceedings of the 8th International Conference on Computer Vision: 2001. p 438–445.
- 40. Comaniciu D, Meer P. 均值偏移：特征空间分析的稳健方法。IEEE Trans Pattern Anal Mach Intell 2002;24:603–619.
- 42. Mathworks: Matlab. Natick, MA; 2010.

