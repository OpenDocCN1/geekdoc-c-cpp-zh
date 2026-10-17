
现在，`0 < r < 1` ⇒ `1 − 0 > 1 − r > 1 − 1` ⇒ `0 < R < 1`。当 `0<r<0.5` 时，意见的极性倾向于负面视角，而 `0.5<r<1` 时，极性趋向于正面视角。因此，当 `0< r <0.5⇒ 0.5<R<1` 时，对产品或服务的态度是满意的，而如果 `0.5 < r < 1 ⇒ 0 < R < 0.5`，则意味着评论的态度表明对产品或服务的不满意。

### 25.3 电子商务市场评论的数学案例研究

对于本案例研究，文本数据已从亚马逊客户评论的庞大语料库中提取，用于亚马逊产品：Amazon Fire TV stick、Amazon Fire HD 8 英寸平板电脑和 Amazon Kindle Paper white [22]。然后，数据集被聚类为五个大小相等的子集。每个子集都被转换为标记化文档的数组。每个这样的标记化文档都通过删除文档中出现的非归因词来进行敏感化。随后形成词簇。现在，词簇通过删除不频繁的词等进行过滤。生成词云是该过程的最终结果。响应可以通过云或词袋捕获的词轻松看到。如果用户提供的所有评论中都存在肯定的氛围，那么就可以决定购买已纳入考虑的评论的产品。包含原始数据和过滤后数据的两个词袋进行比较，以可视化分析。

#### 25.3.1 算法

生成词云涉及的步骤如下：

- 1. 数据提取：
  - (i) 提取文本数据
  - (ii) 准备用于标记化的字符串数据
  - (iii) 创建标记化文档的数组
- 2. 数据清洗：
  - (i) 删除停用词，如 "to," "the," "in," "and" 等。
  - (ii) 根据词长删除不必要的长词或短词
- 3. **形成词云：**
  - (i) 使用标记化词开发词袋模型
  - (ii) 通过删除不频繁的词和空文档来清理词袋
  - (iii) 在完成上述文本过滤后，可视化生成的词云
  - (iv) 现在，使用原始文本数据作为输入数据开发词袋模型
- 4. **比较两个词云**

将此原始数据词云与干净标记化数据词云进行比较。

#### 25.3.2 流程图

![](img/81c56bc4b2fca1951aff5e0ab85b66be_398_0.png)

**FIGURE 25.1**

生成词云的工作流程。

### 25.4 结果与讨论

探索表明，可以积累、预处理、模拟和可视化元数据，如图 25.1 所示的逐步程序。它有助于分析客户对品牌或服务的喜好和厌恶。可行的是将数据挖掘和计算语言学审查与电子商务数据相关联，以分析消费者对商品的评论。电子商务网站评论是本研究的文本数据集。各种个人对产品的响应已被用作分析的输入，并研究了产品的整体意见。它捕捉了产品用户的平均情感，并帮助其他潜在买家选择最适合自己的产品。此外，它还提高了市场价值和他们的消费者前景，因此提供的文本是这样的，结果积极地偏向产品。来自零售电子商务的客户反馈是包含大量宝贵商业信息的来源。但，仅知道客户在谈论什么是不够的。还必须了解他们的情感。计算语言学是揭示这些观点的一种方法。表 25.1 显示了缩减分数（R）的重要性。本章计算的缩减分数被证明是有帮助的，因为当 `0.5<R<1` 时，对产品或服务的态度是满意的，而如果 `0<R<0.5`，则意味着评论的态度表明对产品或服务的不满意。对于数据集 1，R 的值为 0.7922，这是一个相当积极的响应。对于数据集 2，R 的值为 0.8383 显示出高度积极的响应。对于数据集 3，R 的值为 0.7805，这是一个相当积极的响应。对于数据集 4，R 的值为 0.8041，这是一个非常积极的响应。对于数据集 5，R 的值为 0.8122，这是一个非常积极的响应。由于 R 的值非常接近 1，这意味着客户对所审查的产品持赞成意见。这证明零售商提供的数据在与其他服务提供商竞争时，描绘了客户或多或少积极的态度。一般来说，讨论的方法适用于虚拟媒体。词云对研究影响深远，因为它有利于看到和理解人们对零售商声称的产品态度的态度。它以字体大小和词频的降序突出显示文本数据中最常出现的词。

通常，零售商利用其从社交媒体跟踪和计算中产生的消费者观念，通过调整营销计划、各种商品和创新。未来工作的一个重要视角可能是完善虚拟媒体

#### TABLE 25.1

显示缩减分数（R）意义的表格

| 数据集 | 干净词数 (C) | 原始词数 (T) | 比率 (r)=(C/T) | 缩减分数 (R)=1-(C/T) | R 的本质 |
|---|---|---|---|---|---|
| Dataset 1 | 305 | 1468 | 0.2078 | 0.7922 | As 0.5<R<1, it shows a fairly positive response |
| Dataset 2 | 178 | 1101 | 0.1617 | 0.8383 | As 0.5<R<1, it shows a highly positive response |
| Dataset 3 | 369 | 1681 | 0.2195 | 0.7805 | As 0.5<R<1, it shows a fairly positive response |
| Dataset 4 | 261 | 1332 | 0.1959 | 0.8041 | As 0.5<R<1, it shows a very positive response |
| Dataset 5 | 243 | 1294 | 0.1878 | 0.8122 | As 0.5<R<1, it shows a very positive response |

跟踪和控制系统，因为思想随着时间的推移而转变。此外，应增加在计算语言学分析和估计中应用无监督技术以丰富企业竞争力和消费者关系的做法。此外，利用这种技术预测销售额可以更加一致和精确。结论是零售商仅记录了产品的肯定评论，作为营销策略的一部分，以提高产品销量，与其他电子商务零售商竞争。

## Acknowledgment

作者感谢 Guru Gobind Singh Indraprastha University 提供财务支持和研究设施。

## References

- 1. Anderson, J.R. and Bower, G.H. 1973. *Human Associative Memory*. Winston, Washington, DC.
- 2. Anderson, S.R. 1982. Where is morphology? *Linguistic Inquiry*. 13:571–612.
- 3. Anderson, S.R. 1985. *Phonology in the Twentieth Century: Theories of Rules and Theories of Representations*. University of Chicago Press, Chicago.
- 4. Anderson, S.R. 1992. *A-Morphous Morphology*. Cambridge University Press, Cambridge.
- 5. Angluin, D. 1992. Computational learning theory: Survey and selected bibliography. *Proceedings of STOC*. 92:351–369.
- 6. Antonelli, G.A. 1999. A directly cautious theory of defeasible consequence for default logic via the notion of general extension. *Artificial Intelligence*. 109(1–2):71–109.
- 7. Aronoff, M. 1976. *Word Formation in Generative Grammar*. MIT Press, Cambridge, Massachusetts.
- 8. Austin, J.L. 1962. *How to Do Things with Words*. Clarendon Press, Oxford.
- 9. Barzilay, R., Elhadad, N., and McKeown, K. 2002. Inferring strategies for sentence ordering in multidocument summarization. *Journal of Artificial Intelligence Research*. 17:35–55.
- 10. Bird, S. and Ellison, T.M. 1994. One-level phonology: Autosegmental representations and rules as finite automata. *Computational Linguistics*. 20(1):55–90.
- 11. Bloch, B. and Trager, G.L. 1942. Outline of linguistic analysis. *Linguistic Society of America*. Waverly Press, Baltimore.
- 12. Chao, Y.R. 1961. Graphic and phonetic aspects of linguistic and mathematical symbols. In: *Structure of Language and Its Mathematical Aspects*, ed. R. Jakobson, 69–82. Linguistic Society of America, Washington, DC.
- 13. Charniak, E. 1993. *Statistical Language Learning*. MIT Press, Cambridge, MA.
- 14. Collins, C., Viegas, F.B., and Wattenberg, M. 2009. Parallel tag clouds to explore and analyze faceted text corpora. *IEEE Symposium on Visual Analytics Science and Technology*, United States, October 2009, 91–98.
- 15. Cui, W., Wu, Y., Liu, S., Wei, F., Zhou, M., and Qu, H. 2010. Context-preserving dynamic word cloud visualization. *IEEE Computer Graphics and Applications*. 30(6):42–53.
- 16. Dumais, S.T. 2004. Latent semantic analysis. *Annual Review of Information Science and Technology*. 38(1):188–230.
- 17. Kornai, A. 2008. *Mathematical Linguistics*. *Advanced Information and Knowledge Processing*. Springer-Verlag, London.
+ 18. Makkonen, J., Myka, H.A., and Salmenkivi, M. 2004. Simple semantics in topic detection and tracking. *Information Retrieval*. 7(3–4):347–368.
+ 19. White, M., Korelsky, T., Cardie, C., Ng, V.D., and Wagstaff, K. 2001. Multidocument summarization via information extraction. *Proceedings of Human Language Technology Conference: (HLT–2001)*, United States, March 2001 1–7.
+ 20. Wu, Y., Provan, T., Wei, F., Liu, S., and Ma, K.L. 2011. Semantic-preserving word clouds by seam carving. *Computer Graphics Forum*. 30(3):741–750.
+ 21. Xie, L., Kennedy, L., Chang, S.F., et al. 2005. Layered dynamic mixture model for pattern discovery in asynchronous multi-modal streams. *IEEE International Conference on Acoustics, Speech, and Signal Processing (ICASSP)*, Massachusetts, December 2005, 1053–1056.
+ 22. Sasikala Alaguwal. 2018. Accessed November 30, 2018. https://www.kaggle.com/sasikala11/amazon-customer-reviews.

Taylor & Francis

Taylor & Francis Group

http://taylorandfrancis.com

## 26

## 使用 ARW 建模系统研究数据同化对印度季风性强降雨事件模拟的影响

Shilpi Kalra, Sushil Kumar, and A. Routray

## 目录

+ 26.1 引言............................................................................... 381
+ 26.2 建模系统 ............................................................................. 382
+ 26.2.1 高级研究 WRF 建模系统 (ARW) ..................................... 382
+ 26.2.2 3DVAR 分析系统 ................................................................... 383
+ 26.3 与强降雨事件相关的天气形势 ........................... 383
+ 26.4 数值试验...................................................................... 384
+ 26.5 结果与讨论 ..................................................................... 384
+ 26.5.1 同化对模型初始场的影响........................................ 384
+ 26.5.1.1 风、温度和比湿对 GTS 观测的验证 ................................................... 385
+ 26.5.1.2 对初始涡度场的影响..................................................... 386
+ 26.5.2 对模型模拟的影响............................................................. 386
+ 26.5.2.1 湿度通量的垂直剖面.......................................... 386
+ 26.5.2.2 强度预测 ................................................................... 387
+ 26.5.2.3 模型模拟降雨............................................................ 389
+ 26.6 结论............................................................................... 389
+ 致谢 ............................................................................... 390
+ 参考文献.................................................................................... 390

### 26.1 引言

数值天气预报 (NWP) 的预报技巧取决于初始条件 (ICs) 的准确性。如果我们知道当前天气状况，即模型的 IC，就可以用地球大气系统的数学模型来预测未来的天气状况。这些数学模型使用基于流体动力学物理原理的基本微分方程。

近几十年来，非静力区域模式已得到发展，能够预测印度季风区极端天气现象相关的强降雨事件 (Routray et al. 2005, 2010; Kalra et al. 2019)。然而，区域模式的预报技巧取决于初始和侧边界条件 (IC 和 BCs)。IC 和 BCs 来自低分辨率全球 NWP 模式的分析或预报。这些 IC 存在一定的局限性，例如分辨率粗糙且对局地中尺度过程的表征不足。因此，同化方法是最有前景的技术之一，通过利用来自不同平台的高空间和时间分辨率观测来提供改进的分析，作为区域模式的 IC (Daley 1991)。数据同化是一种数学技术，通过将观测信息插入模型背景场来创建大气初始状态的最佳估计。
