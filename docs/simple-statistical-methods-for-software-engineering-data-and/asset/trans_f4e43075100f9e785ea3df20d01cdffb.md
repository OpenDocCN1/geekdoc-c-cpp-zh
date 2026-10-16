

![](img/2f042205c6c0e14747f198ed8f9c9f40_177_0.png)

图 A10.2 频率图。

## 复习问题

- 1. 直方图中选择箱数常用的规则是什么？
- 2. 列出从数据中提取直方图的三个目的。
- 3. 双峰直方图是什么意思？
- 4. 直方图特征的元素有哪些？
- 5. 如何从过程数据直方图中判断过程能力？

## 练习

- 1. 使用以下客户满意度数据构建直方图并提取客户满意度的特征。解释该特征。

  4, 5, 3; 5, 4, 5, 5, 4, 3, 4, 5, 3, 4, 5, 3, 2, 3, 2, 4, 1, 4,
  1, 5, 4, 3, 4, 3, 2, 3, 2, 4, 3, 4, 3, 5, 4, 3, 5, 4, 4, 4, 4

- 2. 使用 MS Excel 的数据分析工具直方图构建直方图。不要使用默认的箱选择，指定你自己的箱。
- 3. 如果企业目标是获得至少 3 分的客户满意度评分，之前提到的直方图特征中看到的风险是什么？
- 4. 测试用例返工工作量数据以人小时为单位如下所示：

  16, 16, 2, 5, 7, 8.5, 8, 9, 10, 11, 5

  用这些有限数据绘制直方图并尝试推断测试用例开发过程。

- 5. 软件增强项目中的工作量方差数据如下所示：

  -10, 4, 5, -3, 8, -2, 0, 9, 5, -2, 5, 3, 5, 12

  绘制给定数据的累积曲线图。

## 参考文献

- 1. G. P. Kulk and C. Verhoef, Quantifying requirements volatility effects, *Science of Computer Programming*, 72, 136–175, 2008.
- 2. L. Rosenberg, Applying and interpreting object oriented metrics, *Software Technology Conference*, Utah, April 1998.
- 3. L. R. Beaumont, *Metrics—A Practical Example*, AT&T Bell Laboratories. Available at http://www.humiliationstudies.org/documents/Beaumontmetricsid.pdf.
- 4. H. Barkman, R. Lincke and W. Lowe, *Quantitative Evaluation of Software Quality Metrics in Open-Source Projects*, Software Technology Group, School of Mathematics and Systems Engineering, Sweden. Available at http://www.arisa.se/Files/BLL-09.
- 5. L. Liu, W. Lai, X.-S. Hua and S.-Q. Yang, *Video Histogram: A Novel Video Signature for Efficient Web Video Duplicate Detection*, Department of Computer Science and Technology, Tsinghua University, Microsoft Research, Asia, Springer Verlag Berlin, Heidelberg, 2007.
- 6. M. K. Kowar and S. Yadav, Brain tumor detection and segmentation using histogram thresholding, *International Journal of Engineering and Advanced Technology*, 1(4), 16–20, 2012.
- 7. W. E. Barkman, *In-Process Quality Control for Manufacturing*, CRC Press, New York, 1989.
- 8. T. Weninger and W. H. Hsu, *Web Content Extraction Through Histogram Clustering*, Kansas State University, Manhattan, Annie Conference, November 9–12, St. Louis, Missouri., 2008.
- 9. D. J. Monroe, *The Entitlement Trap*, Juran Institute, Inc., 2009.
- 10. W. Curry, G. Succi, M. Smith, E. Liu and R. Wong, *Empirical Analysis of the Correlation between Amount-of-Reuse Metrics in the C Programming Language*, ACM, New York, 135–140, 1999.

## 生活是一随机变量

费马和帕斯卡为概率论奠定了基础。凭借他们在分赌注问题上的简短而富有成效的合作，他们现在被视为概率论的联合创始人。费马被认为完成了有史以来第一次严格的概率计算。在其中，他被一名职业赌徒问到，为什么如果他押注在掷骰子四次中至少出现一次六点，他长期来看会获胜，而押注在 24 次掷两颗骰子中至少出现一次双六则会输。费马随后在数学上证明了为什么会这样。 (http://en.wikipedia.org/wiki/Problem_of_points)

克里斯蒂安·惠更斯（1657 年）对该主题进行了全面论述。

雅各布·伯努利的《猜测术》（死后出版，1713 年）使概率建立在坚实的数学基础上，展示了如何计算各种复杂概率。

总体而言，结果本质上是随机的；有些对我们有利，有些则不利。过程结果并不总是精确地保持有利，也不会总是变得不利。结果在有利和不利之间随机切换。

> 事件概率的度量是该事件有利情况数与总情况数之比。
>
> 勒内·笛卡尔

概率的发现可以追溯到文艺复兴时期（见框 11.1）。

在有利和不利之间切换的过程称为伯努利过程，以发明者命名。数学上，伯努利过程随机只取两个值，1 和 0。重复抛硬币是一个伯努利过程；我们得到正面或反面，成功或失败，“1 或 0”。每次抛掷都是伯努利试验。伯努利随机变量由瑞士数学家雅各布·伯努利发明（见框 11.2 简要传记）。

随着试验次数的增加，试验结果会收敛到“期望值”。在公平硬币中，成功概率（正面出现的概率）的“期望值”为 0.5。试验次数越多，就越接近成功概率的值。这就是大数定律。利用该定律，我们可以预测稳定的长期行为。伯努利花了 20 多年才发展出足够严格的数学证明。他将其命名为他的黄金定理，但后来普遍被称为伯努利定理。该定理被应用于预测人们在各种机会游戏中期望赢得多少。

从现实事件的足够数据中，我们可以得出成功概率 p，并相信未来可以根据此进行预测。

预测意味着估计两个值：均值和方差（分别表示集中趋势和离散程度）。

在本章中，我们考虑四种分布来描述四种不同的离散模式描述方式。

- 1. 二项分布

  在 n 次试验中恰好得到 k 次成功的概率由以下二项式表达式给出：

  P(X = k) = C_k^n p^k (1 − p)^(n−k)  (11.1)

  其中 n 是试验次数，p 是每次试验的成功概率，k 是在 n 次试验中观察到的成功次数，计算如下：

  Mean = n p  (11.2)

  Variance = n p (1 − p)  (11.3)

  方程 11.1 是广泛上下文的范式。在服务管理中，成功被 arrival 取代，伯努利过程称为 arrival-type 过程。在软件开发过程中，我们更喜欢使用术语 success。系数 C 是二项系数，因此得名二项分布。

  软件开发过程可能由两个组成部分构成：

  - a. 符合大数定律的固有伯努利成分
  - b. 来自虚假噪声因素的影响

  伯努利分布用于统计过程控制。虚假噪声因素必须被识别、分析和消除。例如，在服务水平协议（SLA）合规数据中，可能同时存在这两个成分。如果过程仅限于伯努利类型，则过程被认为处于统计控制之下。（休哈特称这种变异为“共同原因”变异，并将虚假影响归因于特殊原因。）

  方程 11.1 用于离散事件的质量控制。

### 框 11.2 雅各布·伯努利（1654–1705）

> 自然总是倾向于以最简单的方式行动。
>
> 雅各布·伯努利

雅各布·伯努利为概率论奠定了数学基础。伯努利过程以他命名。伯努利家族在数学界是一个知名名字，以其对数学的推进而闻名。原本来自荷兰，雅各布的父亲尼古劳斯·伯努利将他的香料生意搬到了瑞士巴塞尔。雅各布于 1671 年在巴塞尔大学获得哲学硕士学位，1676 年获得神学硕士学位。在攻读硕士学位期间，他还学习数学和天文学。1681 年，雅各布·伯努利遇到了数学家 Hudde。伯努利继续学习数学，并遇到了世界知名的数学家如玻意耳和胡克。

雅各布·伯努利看到了微积分的力量，被认为是微积分之父之一。他还写了一本名为《猜测术》的书，于 1713 年出版（在他去世 8 年后）。

伯努利在卡当的大数定律思想上有所增进。他断言，如果一个可重复的实验在理论上有概率 p 以某种“有利”方式出现，那么对于任何指定的误差范围，该实验若干次重复试验中，有利结果与总结果的比率将落在该误差范围内。通过这一原理，观测数据可用于估计现实世界事件的概率。这就是现在所知的大数定律。有趣的是，当他写这本书时，他将这一思想命名为“黄金定理”。

伯努利获得了若干奖项和/或荣誉。其中一项荣誉是月球上以他命名的陨石坑。在巴黎，有一条以伯努利家族命名的街道。街道名为 Rue Bernoulli。

### 例 11.1：SLA 合规的二项分布

**问题**

根据去年的交付情况，估计在增强项目中满足 SLA 的概率为 90%。求出在当前年计划的 120 次交付中，至少有 10 次满足 SLA 的概率。绘制相关的二项分布。

