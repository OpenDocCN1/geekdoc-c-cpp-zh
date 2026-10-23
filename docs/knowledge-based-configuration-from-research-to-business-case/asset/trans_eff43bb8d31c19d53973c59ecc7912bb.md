

**表 7.6 将诊断任务表示为优化问题。在此情况下，所有最小冲突集（$CS_1, ..., CS_4$）必须在优化开始前确定（1（0）表示 $c_i$ 是（不是）最小冲突集的一部分）。**

| Conflict Set | $c_1$ | $c_2$ | $c_3$ | $c_4$ | $c_5$ |
|---|---|---|---|---|---|
| $CS_1$ | 1 | 0 | 0 | 1 | 1 |
| $CS_2$ | 1 | 1 | 0 | 0 | 0 |
| $CS_3$ | 1 | 0 | 1 | 0 | 0 |
| $CS_4$ | 0 | 1 | 1 | 0 | 0 |

**表 7.7 由变量 $V = \{v_1, v_2, v_3\}$、dom($v_i$) = {1,2,3} 以及约束 $c_p = conf_1 \lor conf_2 \lor conf_3 \lor conf_4 \in C_{KB}$ 定义的一个简单配置问题。**

| Variables | $conf_1$ | $conf_2$ | $conf_3$ | $conf_4$ |
|---|---|---|---|---|
| $v_1$ | 1 | 3 | 1 | 1 |
| $v_2$ | 2 | 2 | 2 | 2 |
| $v_3$ | 3 | 1 | 2 | 1 |

**表 7.8 示例用户需求 $C_R$ 及其与配置 $conf_1, ..., conf_4$ 的关系（1 = 需求得到支持，0 = 未得到支持）。**

| User Requirements | $conf_1$ | $conf_2$ | $conf_3$ | $conf_4$ |
|---|---|---|---|---|
| $v_1 = 1$ | 1 | 0 | 1 | 1 |
| $v_2 = 1$ | 0 | 0 | 0 | 0 |
| $v_3 = 1$ | 0 | 1 | 0 | 1 |
| $support$ | 1 | 1 | 1 | 2 |

*过滤最小基数诊断。* 我们解释在所有可能配置均已可用的情况下确定最小基数诊断的方法（参见表 7.7 和 7.8）。表 7.7 描述了由一组变量（$V$）、其定义域（dom($v_i$)）以及描述可能配置集合的约束 $c_p$ 定义的配置任务（$c_p = conf_1 \lor conf_2 \lor conf_3 \lor conf_4$）。

基于表 7.7 中包含的信息，我们能够推导出一个*中间表示*，该表示针对每个用户（客户）需求（$\in C_R$）$^6$ 和每个配置（$conf_i$）指示需求是否得到 $conf_i$ 的支持（参见表 7.8）。*support* 值指示

> 6 有关配置任务定义的详细信息，请参见第 6 章。

有多少用户需求得到配置的支持；例如，配置 conf₁ 支持用户需求 v₁ = 1 但不支持其余需求；因此 conf₁ 的支持度为 1。现在应该清楚，我们感兴趣的是针对给定需求集的诊断——必须删除的最小（基数）需求集，以便能够识别出解。

基于中间表示（参见表 7.8），确定例如一个最小基数诊断是直接的。具有最大支持度的配置 confᵢ 也定义了一个最小基数诊断 Δ，因为不存在基数 |Δ′| < |Δ| 的诊断 Δ′（如果存在这种情况，则 Δ 不会具有最大支持值）。在我们的示例中，唯一的最小基数诊断是 Δ = {v₂ = 1}。

## 7.5 结论

在本章中，我们概述了支持基于约束的应用开发中的异常管理，特别是配置器应用开发中的主要概念、技术和算法。这些概念是本书其他章节的基础（参见 Friedrich et al., 2014⁷ 和 Felfernig et al., 2014⁸）。

## 致谢

本章所呈现的工作由奥地利研究促进署资助（拨款编号：827587）。

## 参考文献

Barker, V., O’Connor, D., Bachant, J., Soloway, E., 1989. Expert systems for configuration at Digital: XCON and beyond. Communications of the ACM 32 (3), 298–318.
Chandola, V., Banerjee, A., Kumar, V., 2009. Anomaly Detection: A Survey. ACM Computing Surveys 41 (3), 1–58.
Felfernig, A., Friedrich, G., Jannach, D., Stumptner, M., 2004. Consistency-based diagnosis of configuration knowledge bases. Artificial Intelligence 152 (2), 213–234.
Felfernig, A., Zehentner, C., Blazek, P., 2011. CoreDiag: eliminating redundancy in constraint sets. In: 22nd International Workshop on Principles of Diagnosis (DX’2011), Murnau, Germany, pp. 219–224.
Felfernig, A., Schubert, M., Zehentner, C., 2012. An efficient diagnosis algorithm for inconsistent constraint sets. Artificial Intelligence for Engineering Design, Analysis and Manufacturing (AI EDAM) 26 (1), 53–62.
Felfernig, A., Schippel, S., Leitner, G., Reinfrank, F., Isak, K., Mandl, M., Blazek, P., Ninaus, G., 2013. Automated repair of scoring rules in constraint-based recommender systems. AI Communications 26 (2), 15–27.
Felfernig, A., Reinfrank, F., Ninaus, G., Blazek, P., 2014. Redundancy detection in configuration knowledge. In: Felfernig, A., Hotz, L., Bagley, C., Tiihonen, J. (Eds.), Knowledge-based Configuration – From Research to Business Cases. Morgan Kaufmann Publishers, Waltham, MA, pp. 157–166 (Chapter 12).
Fijany, A., Vatan, F., 2004. New approaches for efficient solution of hitting set problem. In: Winter International Symposium on Information and Communication Technologies. Trinity College Dublin, Cancun, Mexico, pp. 1–6.

⁷第 11 章。
⁸第 12 章。

Fleischanderl, G., Friedrich, G.E., Haselböck, A., Schreiner, H., Stumptner, M., 1998. Configuring large systems using generative constraint satisfaction. IEEE Intelligent Systems 13 (4), 59–68.

Friedrich, G., Jannach, D., Stumptner, M., Zanker, M., 2014. Knowledge engineering for configuration systems. In: Felfernig, A., Hotz, L., Bagley, C., Tiihonen, J. (Eds.), Knowledge-based Configuration – From Research to Business Cases. Morgan Kaufmann Publishers, Waltham, MA, pp. 139–155 (Chapter 11).

Hotz, L., Felfernig, A., Stumptner, M., Ryabokon, A., Bagley, C., Wolter, K., 2014. Configuration knowledge representation and reasoning. In: Felfernig, A., Hotz, L., Bagley, C., Tiihonen, J. (Eds.), Knowledge-based Configuration – From Research to Business Cases. Morgan Kaufmann Publishers, Waltham, MA, pp. 41–72 (Chapter 6).

Jannach, D., 2008. Finding preferred query relaxations in content-based recommenders. In: Chountas, P., Petrounias, I., Kacprzyk, J. (Eds.), Intelligent Techniques and Tools for Novel System Architectures, London, UK, Studies in Computational Intelligence, vol. 109, pp. 81–97.

Junker, U., 2004. QUICKXPLAIN: preferred explanations and relaxations for over-constrained problems. In: McGuinness, D.L., Ferguson, G. (Eds.), 19th International Conference on Artificial Intelligence (AAAI'04). AAAI Press, San Jose, CA, pp. 167–172.

Reiter, R., 1987. A theory of diagnosis from first principles. Artificial Intelligence 32 (1), 57–95.

Schubert, M., Felfernig, A., 2011. BFX: diagnosing conflicting requirements in constraint-based recommendation. International Journal on Artificial Intelligence Tools 20 (2), 297–312.

Schubert, M., Felfernig, A., Mandl, M., 2010. FastXPlain: conflict detection for constraint-based recommendation problems. In: García-Pedrajas, N., Herrera, F., Fyfe, C., Benítez, J., Ali, M. (Eds.), Trends in Applied Intelligent Systems (Proceedings of 23rd International Conference on Industrial Engineering and Other Applications of Applied Intelligent Systems, IEA/AIE 2010). Lecture Notes in Computer Science, vol. 6096. Springer, Cordoba, Spain, pp. 621–630.

## 配置环境的用户界面

Gerhard Leitner*, Alexander Felfernig†, Paul Blazek‡, Florian Reinfank† and Gerald Ninaus†
*Alpen-Adria Universität Klagenfurt, Klagenfurt, Austria
†Graz University of Technology, Graz, Austria
‡cyLEDGE, Vienna, Austria

摘要：配置技术已成功应用于电信、金融服务和汽车等不同领域。配置环境的用户界面在两个主要方面发挥关键作用。首先，配置器应用的用户需要允许高效和直观配置过程的界面。其次，知识工程师和领域专家（配置器应用的开发者）需要提供开发和维护操作智能支持的界面。在本章中，我们讨论在开发配置器终端用户和应用开发者用户界面时应考虑的方面。

## 8.1 引言

配置是大规模定制（Anderson and Pine, 1996; Pine, 1999; 另见 Piller and Blazek, 2014¹）的一项关键技术。它可以定义为设计活动的一种特殊情况，其中产生的工件由预定义的一组组件类型组成，并且与给定的约束集一致（Sabin and Weigel, 1998）。配置环境允许终端用户设计他们自己的个性化产品和服务，以及知识工程师和领域专家开发配置器应用（主要是用户界面和知识库）。对于两类用户，配置环境的 user interface 都发挥关键作用。首先，持久接受和应用的一个主要前提是终端用户能够轻松配置符合其愿望和需求的产品（Ardissono et al., 2003; Falkner et al., 2011）。其次，知识工程师和领域专家需要允许有效开发和维护的技术，这是保持知识库最新不可或缺的前提（Blythe et al., 2001）。对于这两种场景，我们讨论有助于使配置技术应用取得成功的用户界面的属性。

本章的主要贡献如下。我们提供了在开发配置器应用用户界面以及相应知识工程环境用户界面时应考虑的重要标准概述（参见第 8.2 节）。对于这些标准，我们提出了并举例说明了支持技术（参见第 8.3 节）。接下来，我们

> ¹第 9 章。
> ²配置工具和用户界面的概述可在第 V 部分找到。

