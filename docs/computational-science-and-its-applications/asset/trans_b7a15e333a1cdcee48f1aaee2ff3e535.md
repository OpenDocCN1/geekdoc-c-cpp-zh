

- 18. Sashikumaar Ganesan 和 Lutz Tobiska. 具有可溶性表面活性剂的两相流计算的任意拉格朗日-欧拉有限元方法。*Journal of Computational Physics*，231(9):3685–3702，2012。
- 19. Sashikumaar Ganesan 和 Shweta Srivastava. 时变域中对流-扩散问题的 ALE-SUPG 有限元方法：守恒形式。*Applied Mathematics and Computation*，303:128–145，2017。
- 20. Eberhard Bänsch. *Numerical Methods for the Instationary Navier-Stokes Equations with a Free Capillary Surface*。博士论文，Verlag nicht ermittelbar，1998。
- 21. S Ganesan 和 L.Tobiska. 液滴撞击水平表面的有限元模拟。载于 *Proceedings of Algorithm*，第 2005 卷，第 1–11 页。斯洛伐克技术大学，布拉迪斯拉发，2005。
- 22. Gunar Matthies. *Finite Element Methods for Free Boundary Value Problems with Capillary Surfaces*。Shaker，德国亚琛 2002。
- 23. F Nobile. *Numerical Approximation of Fluid Structure Interaction Problems with Application to Haemodynamics*。博士论文，洛桑联邦理工学院，2001。
- 24. Christophe Geuzaine 和 Jean-François Remacle. Gmsh：内置预处理和后处理功能的 3D 有限元网格生成器。*International Journal for Numerical Methods in Engineering*，79(11):1309–1331，2009。
- 25. Hang Si. Tetgen，一个基于 Delaunay 的高质量四面体网格生成器。*ACM Transactions on Mathematical Software (TOMS)*，41(2):11，2015。
- 26. Ulrich Wilbrandt, Clemens Bartsch, Naveed Ahmed, Najib Alia, Felix Anker, Laura Blank, Alfonso Ciaazzo, Sashikumaar Ganesan, Swetlana Giere, Gunar Matthies, 等。ParMooN—基于映射有限元的现代化程序包。*Computers & Mathematics with Applications*，74(1):74–88，2017。
- 27. Patrick Le Tallec 和 Jean Mauro. 大结构位移下的流固耦合。*Computer Methods in Applied Mechanics and Engineering*，190(24–25):3039–3067，2001。
- 28. Frederic J Blom. 应用于活塞问题的整体流固耦合算法。*Computer Methods in Applied Mechanics and Engineering*，167(3–4):369–391，1998。
- 29. EH Van Brummelen, SJ Hulshoff, 和 R De Borst. 流固耦合问题的不相容性下的能量守恒。*Computer Methods in Applied Mechanics and Engineering*，192(25):2727–2748，2003。
- 30. Carlos A Felippa, KC Park, 和 Charbel Farhat. 耦合机械系统的分区分析。*Computer Methods in Applied Mechanics and Engineering*，190(24–25):3247–3270，2001。
- 31. Serge Piperno, Charbel Farhat, 和 Bernard Larrouturou. 瞬态耦合气动弹性问题的分区求解程序 第 I 部分：模型问题、理论和二维应用。*Computer Methods in Applied Mechanics and Engineering*，124(1–2):79–112，1995。
- 32. S Ganesan, V John, G Matthies, R Meesala, S Abdus, 和 U Wilbrandt. 用于偏微分方程计算的面向对象并行有限元方案：设计与实现。载于 *2016 IEEE 23rd International Conference on High Performance Computing Workshops (HiPCW)*，页码 2–11，2016。
- 33. Bing Jie Guo 和 Sverre Steen. 短波中 KVLCC2 附加阻力的评估。*Journal of Hydrodynamics, Series B*，23(6):709–722，2011。

## 11
## DNA—Drug Interaction: Insight from Computer Simulations
Anurag Upadhyaya, Shesh Nath, 和 Sanjay Kumar

## CONTENTS
- 11.1 Introduction................................................................................................................171
- 11.2 A Brief Review of DNA and Its Properties ......................................................................172
- 11.3 Computer Simulations ...................................................................................................175
- 11.4 Atomistic Simulations of DNA Rupture .........................................................................179
- 11.5 Stability of a DNA Aptamer and Its Use as a Drug Delivery Agent ..............................182
- 11.6 Stability of DNA-ICLs against Force and Its Use as an Anti-Tumor Drug ...................184
    - 11.6.1 Rupture of DNA and DNA-ICLs .............................................................................186
    - 11.6.2 Unzipping of DNA and DNA-ICLs.........................................................................188
- 11.7 Conclusions and Future Perspective...............................................................................189
- Acknowledgments................................................................................................................190
- References...........................................................................................................................190

### 11.1 Introduction
核酸在包括细胞分裂（复制）和蛋白质合成（转录和翻译）在内的生物过程中发挥着至关重要的作用。这些过程在正常健康细胞和癌细胞中都会发生。癌细胞的特点是细胞分裂不受控制，这与正常健康细胞分裂不同 [1, 2]。正常细胞表现出受控的细胞分裂，其中与同类细胞的表面接触会停止细胞分裂，这一过程称为接触抑制。癌细胞丧失了这种能力，因此生长迅速。无论细胞分裂是 mitosis 还是 meiosis，DNA 复制的精确拷贝都是必不可少的。DNA 的稳定性很大程度上受其长度、碱基组成、序列以及核苷酸错配的存在影响 [3–8]。它还强烈地受到 pH、温度和溶剂变化以及活细胞中 helicases、polymerases 或 topoisomerases 等蛋白质结合的影响 [7, 9, 10]。

小分子可能与 DNA 发生相互作用或结合 [11]。此类分子的分类取决于其作用机制。广义上讲，DNA 结合分子可分为：(i) 在次要沟槽中组装的沟槽结合剂；(ii) 夹在碱基对之间的嵌入剂；(iii) 与 DNA 反应形成 DNA 烷基化的烷基化剂；以及 (iv) 具有破坏 DNA 链能力的裂解剂。这些类分子具有不同的结构，并以不同的方式与 DNA 相互作用，其主要任务是通过抑制 DNA 复制来阻止癌细胞分裂。然而，它会阻止细胞分裂，而不会区分健康细胞或癌细胞 [12]。因此，它会引起多种其他副作用，例如恶心、腹泻、脱发、血细胞计数低、口腔溃疡等。因此，将药物靶向递送到癌细胞中是提高疗效并通过减少正常细胞的摄取来降低毒性副作用的先决条件。

最近的研究表明，DNA 适配体可作为靶向药物递送的载体 [13–15]。适配体是富含鸟嘌呤(G)的短寡核苷酸（DNA、RNA）分子，可执行特定功能 [16, 17]。这些适配体是通过体外 SELEX（指数富集配体系统进化）过程开发的，以便更好地了解在体内或活细胞中产生的抗体的行为 [16–18]。适配体中最为广泛研究的例子之一存在于真核染色体末端的端粒酶中，在那里它在基因调控中发挥重要作用 [19, 20]。由鸟嘌呤组成的 DNA 环或碱基口袋可以与小分子和蛋白质相互作用，从而增强其稳定性、亲和力和特异性 [21]。例如，腺苷一磷酸（AMP）以八个氢键结合到 DNA 环（称为结合口袋）中，从而增强了适配体的稳定性 [22–24]。它可作为癌症治疗药物的靶点 [25]。它们与靶蛋白的高亲和力和选择性使其成为生物传感器中理想而强大的探针和强效药物 [26–36]。

因此，有必要了解药物-DNA 复合物中涉及的分子间和分子内相互作用的作用。单分子力谱（SMFS）实验提供了研究这些分子力的机会 [2, 6, 37–48]。最初，人们认为 SMFS 实验中检测到的相互作用大多是机械性的，可以通过知道施加力的值来计算。然而，这些实验得出的见解表明，分子相互作用的测量不仅取决于施加力的大小，还取决于力的施加方式和位置 [6, 38–48]。这些实验可用于探索药物-DNA 复合物中相互作用位点产生的局部稳定性。

本章的目的是了解 DNA 在这些分子存在下的构象稳定性，并将其用作药物或药物递送载体。第 11.2 节简要介绍了 DNA 及其性质。第 11.3 节描述了分子动力学（全原子）模拟以及 DNA 所需的力场。第 11.4 节涉及无药物分子存在下 DNA 破裂的原子模拟。第 11.5 节中，我们扩展了我们的方法来研究 DNA 适配体的稳定性和其作为药物递送载体的用途。第 11.6 节重点关注烷基化剂存在下 DNA 的稳定性。如前所述，烷基化剂与 DNA 链形成共价键，被称为交联剂（ICLs）。我们将考虑两种药物，即丝裂霉素 C 和曲贝替定，它们形成 DNA-ICLs，并将其稳定性与无药 DNA 进行比较。本章以第 11.7 节的简要讨论和未来展望结束。

### 11.2 A Brief Review of DNA and Its Properties
细胞内有细胞核，其中含有 DNA（图 11.1）。它是一种被认为是“生命分子”的分子。遗传信息储存在 DNA 中，并用于包括许多病毒在内的生物体的发育和功能 [49–51]。

