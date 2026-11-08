
- 8. 估计了组织细胞的平均氧饱和度、开放的毛细血管细胞数量（毛细血管流量），以及上一次迭代中开放和关闭的细胞数量。
- 9. 假设在所有计算实验中，体循环血流的振荡形式保持恒定。
- 10. 当CA进入稳态模式时，记录所有参数。

### 6.2 模拟结果

发现了体循环血流与毛细血管血流之间的四类相互作用，图11：

- a. *稳态*，代谢活动低，毛细血管血流与体循环血流不同步；
- b. *正常动脉血流*——毛细血管血流与体循环血流同步；
- c. *动脉血流显著增加*（例如应激调节）——毛细血管组在收缩期结束前开放和关闭，这可能因局部血管阻力增加而引起流体动力学溢出，并可能损伤微血管内皮；
- d. *动脉血流显著减少*，组织缺氧：由于高浓度血管舒张代谢物导致舒张期动脉压下降，一些毛细血管在收缩期结束时未关闭。

![](img/55ff3770fcfe64effe3c90a4d4692fa6_329_0.png)

图11. 动脉（AF）血流与毛细血管（CF）血流相互作用的类型；组织耗氧量（TOC）的振荡。采用细胞自动机进行模拟。

文献（Lightfoot, 1974）中给出的实验数据证实了关于外周血流与体循环血流之间存在相互作用的假设。从实验数据获得的微动脉和微静脉血流振荡由心脏搏动引起。

### 6.3 心房颤动条件下的模拟

*在本研究步骤中*，我们使用了心房颤动患者的真实数据，图12。假设体循环血流大致与血压振荡成正比。然后我们替换了上一步指出的CA规则。

在这种情况下，当心律和心输出量发生显著变化，且组织代谢活动处于一定水平时，动脉血流与毛细血管血流有可能实现同步，图13。

毛细血管血流与动脉血流同步变化。在接近基础代谢状态下的血流过剩情况（图13a），以及体循环血流高于必要水平时（图13），与图11a、c所示情况相似。

所展示的模拟结果使我们能够推测，毛细血管系统的功能可以与动脉血流的振荡同步。

![](img/55ff3770fcfe64effe3c90a4d4692fa6_330_0.png)

图12. 用于模拟心房颤动的真实患者数据（心电图——ECG和颈动脉脉搏图——CSphG）。

![](img/55ff3770fcfe64effe3c90a4d4692fa6_331_0.png)

![](img/55ff3770fcfe64effe3c90a4d4692fa6_331_1.png)

![](img/55ff3770fcfe64effe3c90a4d4692fa6_331_2.png)

图13. 基于心房颤动真实患者数据的模拟中动脉血流与毛细血管血流的同步。TOS——组织氧饱和度；AF——动脉血流；CF——毛细血管血流。

- Knyzhov G., Nastenko Ye., Maksymenko V., Kravchuk O., Shardukova Yu. The Interactions between Arterial and Capillary Flow Cellular Automaton Simulations of Qualitative Peculiarities.- WC 2009, IFMBE Proceedings 25/IV, - 2009. P. 572-574.// www.springerlink.com
- Lightfoot E. N. Transport phenomena and living systems: biomedical aspects of momentum and mass transport. New York: John Wiley and Sons. 1974. 495 p.
- Little R. C., Little W. C. Physiology of the Heart and Circulation. // Year Book Med. Publ. Inc.- 1989.-379 p.
- Nastenko E., Maksymenko V., Belov Yu., Kravchuk A. Modeling of complex behaviour of the microvascular arterial network with cellular automata // Math. Modeling & Computing in Biology and Medicine. 5th ESMTB Conference 2002. - Ed. By V. Capasso. - MIRIAM. - Italy. - P. 227-234.
- Nastenko E.A., Maksymenko V.B., Palets B.L., Onishchenko V.F., Rysin S.V. The role of central hemodynamics in the regulation of systemic oxygen transport // Yearbook of scientific works of the Association of Cardiovascular Surgeons of Ukraine - V. 8. - 2000. P.142-144. (Rus.)
- Nastenko E.A., Maksymenko V.B., Palets B.L., Rysin S.V. Investigation of the role of peripheral vascular resistance in the optimization of system of oxygen transport in norm and at heart failure. // Yearbook of scientific works of the Association of Cardiovascular Surgeons of Ukraine.-2001. - Vol. 9 - P. 227-231. (Rus.)
- Nastenko E.A. The Use of Cluster Analysis for Partitioning Mixtures of Multidimensional Functional Characteristics of Complex Biomedical Systems.- J. of Automation and Information Sciences.-V.28.-N5-6.-1996.-P.77-83.
- Naylor-Shepherd M.F., Fuchs D.W., Angaran D.M. Oxygen homeostasis: theory, measurement, and therapeutic implications. // DICP, Ann. of Pharmacotherapy.-V.24.-1990.-P.1195-1203.
- Ream A.K., Fogdall R.P. Acute cardiovascular management: anesthesia and intensive care. // Philadelphia-Toronto: J.B. Lippincott Company.- 1982.-940 p.
- Reeder G.D. The biochemistry and physiology of hemoglobin. // Am. Soc. of Extra-Corp. Technol., Inc., AMSECT-Reston.-Virginia.-1986.- 250 p.
- Risk Management: Risk. Sustainable development. Synergetics. - M.: - Science. - 2000.-431 p. (Rus.)
- Rushmer R. F. Cardiovascular Dynamics, 4th edition, Philadelphia, W. B. Saunders Co.-1976.-584 p.
- Samsel R.W., Schumacker P.T. Oxygen delivery to tissues.// Eur. Respir.J., 4.-1981. P.1258-1267.
- Wolfram S. Universality and complexity in cellular automata // Physica D. Vol.1. 1984. P. 91-125.
- Wolfram S. Computation Theory of Cellular Automata. In: Theory and Application of Cellular Automata. World Scientific: Singapore. 1984. P. 189-230.
- Yusupov R.M., Polonnikov R.I. Telemedicine - the new information technologies on the threshold of the XXI century.-St.-1998.-490 p. (Rus.)
- Zweifach B.W. Quantitative studies of microcirculatory structure and function. III. Analysis of pressure distribution in the terminal vascular bed in cat mesentery // Circulation Research, - 1974. - V. 34. - P. 843-857.
- Zweifach B.W., Lipowsky H.H. Quantitative studies of microcirculatory structure and function. III. Microvascular hemodynamics of cat mesentery and rabbit omentum// Circulation Research,-V. 41.- 1977. - P. 380-390.

## 基于细胞自动机的社会模拟：语言转用建模

Francesc S. Beltran¹, Salvador Herrando¹, Violant Estrader², Doris Ferreres²,
Marc-Antoni Adell² and Marcos Ruiz-Soler³
¹巴塞罗那大学，
²瓦伦西亚大学
³马拉加大学
西班牙

### 1. 引言

如今，语言转用（即一个语言使用者群体停止使用其传统语言，并在所有交际场合使用一种新语言）可能在全世界造成语言的大规模灭绝。因此，在这种背景下，社会科学研究的一项重要任务应是深入理解语言转用。然而，在所有社会科学中，对引导个体和群体社会行为的社会变量与行为变量进行建模，历来都很棘手。在这种情况下，社会模拟提供了一种检验假设和构建社会现象模型的工具（例如，见 Gilbert, 1996；Gilbert & Troitzsch, 2005；以及 Goldspink, 2002），尤其是基于细胞自动机理论的技术（Hegselmann, 1996；Hegselmann & Flache, 1998；Nowak & Lewenstein, 1996）。根据这一框架，我们介绍一个细胞自动机的性质，它融合了盖尔语—阿尔瓦尼蒂卡语言转用模型（Sasse, 1992）的一些假设，以及社会心理学领域中关于社会影响动力学的研究发现（Latané, 1981；Nowak et al., 1990）。因此，我们定义了一个细胞自动机，并开展了一组使用该自动机的模拟。我们纳入来自加泰罗尼亚（南欧的一个地区）近期社会语言学研究中的经验数据，以在不同情景下运行该自动机。结果使我们能够突出语言转用中涉及的一些主要因素。最后，我们还讨论基于细胞自动机理论的社会模拟方法如何被证明是理解语言转用的有用工具。

### 2. 语言转用的社会语言学模型

尽管过去有一些语言今天已不再被使用，例如伊特鲁里亚语、埃及语和赫梯语，人们通常称它们为死语言，但一种语言的死亡并不仅仅是古代事件。联合国教科文组织（UNESCO，2003）估计，到本世纪末，目前全世界约6000种语言中，将有超过5100种消失；即约90%的语言将消失。当一种语言消亡时，使用该语言的群体将失去其身份认同的一个主要元素，其文化框架也会因此变得贫乏。其最可能的未来
