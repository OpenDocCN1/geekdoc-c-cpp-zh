# De Gruyter 逻辑及其应用丛书：递归论：可定义性的计算方面





## 作者

- Prof. Dr. 钟志达
  新加坡国立大学
  数学系
  10 Lower Kent Ridge Road
  119076 新加坡
  chongct@math.nus.edu.sg

- Prof. Dr. 梁宇
  南京大学
  数学科学研究所
  210093 南京
  中华人民共和国
  yuliang.nju@gmail.com


钟志达将此书献给他已故的父母；
梁宇将此书献给李张。

## 前言

> ... 逻辑关乎可定义性。
> - 杰拉尔德·E·萨克斯 [124]

上面的引文强调了作者的观点：递归论以可定义性概念为基础。虽然从经典上讲，该理论始于图灵对有效可计算性（各种类型对象的）的构想，但它很快便呈现出更广阔的视角。一项基本定理指出，自然数集可计算当且仅当它在一阶算术中是 \(\Delta^1_1\)-可定义的。这为对自然数集及其句法类的一般研究奠定了基础。

关于可定义性的观点并不与计算是递归论核心的事实相冲突。确实，可定义性问题自然转化为关于（可能相对化的）计算的问题，反之亦然。克莱尼将数的 \(\Delta^1_1\)-集刻画为正好是超算术集，而斯佩克特和甘迪的相应定理指出这些正是 \(L_{\omega_1^{CK}}\) 中的所有实数，这便是一个例证。一旦指定了语法（一阶和二阶算术的语言）以及对 \(\omega\) 及其子集的成员进行解释的结构，可定义性便自然而然地占据其位置。已引入工具和构造技术，以研究 \(\omega\)、\(2^\omega\) 乃至 \(2^\omega\) 的幂集或 \(\omega^\omega\) 上句法类的可计算性问题。波斯特的可枚举集问题、实数的 \(\Sigma^1_1\)-集的甘迪基数定理、用超算术刻画 \(\Delta^1_1\)-集、跳算子的可定义性，都是直接的例子。确实，在该领域很难找到与可定义性关系不大的问题。本书的标题正是为了体现这一观点。

编写一本关于递归论、侧重于实数集及其子集计算方面的书籍的想法，是在一段时间内逐渐形成的。该学科由克莱尼创立，他引入了相对于实数及其相关序数的超算术层次概念。它在斯佩克特、甘迪、克雷塞尔和萨克斯手中不断发展。这些正是如今被称为高阶递归论的主要进展。该理论从20世纪50年代开始，近三十年来一直是密集研究的对象，但似乎在20世纪80年代失去了动力。在附录中转载的一次采访中，萨克斯表示：“多年来，我总是倾向于预测递归论即将终结，但每次都错了。”尽管该领域一位创始人做出了相当悲观的宣判，但递归论依然蓬勃发展。然而，自那时起，开拓者们伟大传统中的高阶递归论只偶尔受到关注，尽管在上世纪末，该领域做出了一些非常重要的贡献，例如斯拉曼和伍丁关于超度刚性的定理，并且许多有趣且具有挑战性的问题仍然存在。事实上，萨克斯本人于1998年告别了高阶递归论。今天，该学科没有得到其应有的活力和热情来推进。我们认为这相当不幸，因为其中展现了数理逻辑统一性的精美例证，集合论和模型论的思想和工具被有成效地应用于研究可计算性问题。编写另一本书（继萨克斯的 *高阶递归论* [123]之后）来展示这种相互作用，是一个诱人的提议。最近在图灵度和超度全局理论研究方面的进展，以及高阶随机性作为研究课题的出现，为我们将想法变为现实提供了动力。希望读者在读完后会同意，始于半个多世纪前的推广递归论的事业在数学上是有回报的，并且该学科既富有吸引力又极具挑战性，拥有许多深刻而优雅的定理。

本书包含四个主要部分。前六章构成第一部分，发展 \(\Pi^1_1\)-集的基本理论、可构造宇宙的精细结构理论、解析分层次和集合论。它们为本书其余部分奠定了基础。第二部分侧重于图灵度的结构。在这里，我们讨论与马丁猜想相关的跳算子分类以及 \(\Pi^1_1\)-集的构造，以及度理论独立性结果。我们在第三部分将注意力转向超度。特别是，我们证明了超度结构的刚性及其与二阶算术的双可解释性。我们还包括一章关于基/反基定理以及 \(L\) 中的完美子集。第四部分专门研究高阶随机性，这一主题自然与前三部分涵盖的主题相关联。练习贯穿各章。其中许多旨在补充所涵盖的主题。最具挑战性的练习标有 *。

本书以2009年与杰拉尔德·萨克斯（附录B）的访谈结束。我们认为，用一篇对一位其工作可以说在上世纪显著塑造了递归论（包括经典递归论和高阶递归论）发展的人的致敬来结束本书，是很合适的。

关于先修知识：虽然本书力求涵盖尽可能多的背景材料，但并非旨在成为百科全书。假设读者熟悉基本逻辑和集合论，包括经典递归论、基本集合论（包括强迫法）和算法随机性。许多结果用于证明，有时未明确提及。符合我们的偏好和品味，所呈现的集合论中一些定理的证明明显带有递归论的风格。这些证明不一定是最简单的。我们的目的是通过突出那些不易立即察觉的有效内容，为读者提供对这些定理的不同视角。希望这些能为证明背后的想法提供额外的见解。

前两章的材料紧密遵循萨克斯的 *高阶递归论* [123]。曼斯菲尔德和韦特坎普的专著 *描述集合论的递归方面* [88]也是我们的关键参考书之一。当然，不应忘记提及哈特利·罗杰斯的经典著作 *递归函数与有效可计算性理论*


ity [116]，这本书首次使递归理论对几代逻辑学生变得可理解，并在很大程度上确立了该主题书籍的风格。

在本书中，我们出于对其历史起源的尊重，更倾向于将该学科称为递归理论（recursion theory），而非可计算性理论（computability theory，其另一种常见称呼），尽管全书中两个术语混用。

在手稿准备期间，作者们从同事和学生的评论和建议中受益，其中一些人通读了本书的各个部分。某些章节曾由第二作者在新加坡国立大学的一门研究生课程中使用。我们感谢 Laurent Bienvenu、Peter Cholak、Decheng Ding、Qi Feng、Su Gao、Junle Goh、Noam Greenberg、Wei Li、Yiqun Liu、Yong Liu、Benoit Monin、André Nies、Dilip Raghavan、Gerald Sacks、Richard Shore、Stephen Simpson、Theodore A. Slaman、Frank Stephan、Wei Wang、Yue Yang 和 Jing Zhang 对本项目的关注、想法、建议和/或支持。

最后，就此工作而言，Chong 部分获得 NUS 资助 WBS C140-000-025-00 的支持，而 Yu 部分获得新加坡国立大学、洪堡基金会以及中国国家自然科学基金会（编号 11071114 和 11322112）的支持。我们谨此表示感谢。

Chit Chong 和 Liang Yu
2015年6月15日

## 1 高阶递归理论导论

### 1.1 投影谓词

#### 1.1.1 递归谓词与算术谓词

在 \(\omega\) 上的递归谓词 \(R\) 是一个全递归函数 \(\Phi : \omega \to 2\)，使得 \(R(n) \Leftrightarrow \Phi(n) = 1\)。通过 \(\omega^{<\omega}\) 在 \(\omega\) 上的标准编码，可以定义 \(\omega^{<\omega}\) 上的递归谓词。同样，可以将 \(\omega^n\) 编码在 \(\omega\) 中，以获得 \(\omega\) 上的递归 n 元谓词，以及 \((\omega^{<\omega})^m \times \omega^k\) 上的递归谓词。\(\omega^\omega \times \omega\) 上的算术谓词类定义如下：

**定义 1.1.1.** 一个在 \(\omega^\omega \times \omega\) 上的谓词 \(R(x, n)\) 是 *部分递归* 的，如果存在一个在 \(\omega^{<\omega} \times \omega\) 上的部分递归函数 \(\Phi(\sigma, n)\)，使得

- (i) \((\forall \sigma)(\forall n)(\Phi(\sigma, n) \downarrow \Rightarrow \sigma \prec \tau \rightarrow (\Phi(\tau, n) \downarrow \land \Phi(\sigma, n) = \Phi(\tau, n)))\).

- (ii) 对于任何 \(x \in \omega^\omega\) 和 \(n \in \omega\)，\(R(x, n)\) 当且仅当 \((\exists m)(\Phi(x \mid m, n) \downarrow = 0)\)。

一个在 \(\omega^\omega \times \omega\) 上的谓词 \(R(x, n)\) 是 *递归* 的，如果上述部分递归函数 \(\Phi\) 还满足以下性质：

- (iii) \((\forall y)(\forall n)(\exists m)(\Phi(x \mid m, n) \downarrow)\)。

**备注 1.1.2.** 我们可以同样定义 \((\omega^\omega)^k \times (\omega^{<\omega})^m \times \omega^k\) 上的递归谓词。一般来说，\(\omega^\omega \times \omega\) 上的递归谓词没有有效枚举。

算术谓词的层次 \(\Sigma^0_n\) 通过对 \(n < \omega\) 的归纳定义。

**定义 1.1.3.**

- (i) \(\Sigma^0_1 = P\)（P 是一个部分递归谓词）。

- (ii) 如果 \(\{(x, m) \mid \neg P(x, m)\}\) 是 \(\Sigma^0_1\)，则 \(P\) 是 \(\Pi^0_1\)。

- (iii) 如果存在一个 \(\Pi^0_n\) 谓词 \(R(x, (m, k))\) 使得

\(P(x, m) \Leftrightarrow (\exists k)R(x, (m, k))\)，

则 P 是 \(\Sigma^0_{n+1}\)。

- (iv) 如果 P 既是 \(\Sigma^0_n\) 又是 \(\Pi^0_n\)，则 P 是 \(\Delta^0_n\)。

如果存在某个 n 使得 \(P \in \Sigma^0_n\)，则称谓词 P 是 *算术* 的。

根据经典递归理论的结果，谓词 \(P(x, m)\) 是 \(\Sigma^0_1\) 当且仅当存在一个递归谓词 \(R(x, m, n)\) 使得 \(P(x, m) \Leftrightarrow (\exists n)R(x, m, n)\)。

固定一个满足定义 1.1.1 中性质 (i) 的部分递归函数的有效枚举 \(\{\Phi_e(\sigma, n)\}_{e \in \omega}\)。对于每个实数 x，\(\Phi_e(x \mid m, n)\) 表示在阶段 m 时 \(\Phi_e(x \mid m, n) \downarrow\) 的最小 m 对应的 \(\Phi_e(x \mid m, n)\)。如果不存在这样的 m，则 \(\Phi_e(x, n)\) 未定义。我们称 \(\Phi_e(x, n)\) 为 x-部分递归函数。因此，存在带有神谕 x 的部分递归函数的统一枚举 \(\{\Phi_e(x, n)\}_{e \in \omega}\)。换句话说，谓词 \(P(e, x, n, m) \Leftrightarrow \Phi_e(x, n) \downarrow = m\) 是 \(\Sigma^0_1\)。





以上内容有一个明显的推广，允许在 \(\omega^\omega\) 中使用参数，从而得到相对于一个实数或一组有限实数的 \(\Sigma^0_n\)-谓词类。

### Definition 1.1.4.

- (i) 谓词 \(P^0(y, m)\) 是 \(\Sigma^1_1(\alpha)\)，当且仅当存在一个部分递归谓词 \(R(A, y, m)\)，使得对所有 \(y\) 和 \(m\)，\(P^0(y, m) \leftrightarrow R(\alpha, y, m)\)。
- (ii) \(P^0(y, m)\) 是 \(\Pi^0_n(\alpha)\)，当且仅当 \(\neg P^0(y, m)\) 是 \(\Sigma^0_n(\alpha)\)。
- (iii) \(P^0(y, m)\) 是 \(\Sigma^0_n(\alpha)\)，当且仅当存在一个 \(\Pi^0_n(\alpha)\)-谓词 \(R^0(y, m, k)\)，使得 \(P^0(y, m)\) 当 \((\exists k)R^0(y, m, k)\) 时成立。
- (iv) \(P^0(y, m)\) 是 \(\Delta^0_n(\alpha)\)，当且仅当它既是 \(\Sigma^0_{n+1}(\alpha)\) 也是 \(\Pi^0_{n+1}(\alpha)\)。

给定一组谓词 \(\Gamma\)，我们说集合 \(a \subseteq \omega\)（或 \(P^* \subseteq \omega^\omega\)）是一个 \(\Gamma\)-集，或 \(\Gamma\) 的一个成员，如果存在谓词 \(P(x, m) \in \Gamma\) 使得 \(m \in a \leftrightarrow P(0, m)\)（或 \(x \in P^* \leftrightarrow P(x, 0)\)）。对每个 \(n < \omega\)，令 \(\Sigma^0_n\)、\(\Pi^0_n\) 和 \(\Delta^0_n\) 分别表示 \(\Sigma^0_n\)、\(\Pi^0_n\) 和 \(\Delta^0_n\)-谓词的类。以下引理是众所周知的。证明可参见 [53]。

### Lemma 1.1.5.

- (i) 设 \(n < \omega\)。存在一个 \(\Sigma^0_n\)-集 \(U \subseteq \omega^\omega \times \omega^\omega\)，使得对每个 \(P \in \Sigma^0_n\)，都存在某个 \(y\) 使得 \(P = \{x \mid (x, y) \in U\}\)。
- (ii) 对每个 \(n\)，\(\Sigma^0_n \subset \Delta^0_{n+1} \subset \Sigma^0_{n+1}\) 且 \(\Pi^0_n \subset \Delta^0_{n+1} \subset \Pi^0_{n+1}\)。

在经典递归论中，集合 \(a \subseteq \omega\) 是 \(\Sigma^0_1\) 当且仅当 \(a\) 是 \(\Sigma^0_1(\emptyset')\)。然而，这对于实数集通常不成立。例如，集合 \(\{\emptyset^{(\omega)}\}\) 是 \(\Sigma^0_3\)，但对于任何 \(x \in \omega^\omega\)，它都不是 \(\Sigma^0_1(x)\)（作为单元素集）（参见练习 1.1.5）。

### 1.1.2 解析谓词

### Definition 1.1.6.

- (i) 谓词 \(P(x, m)\) 是 \(\Sigma^1_1\)，如果它是 \(\Sigma^1_1\)；
- (ii) 谓词 \(P(x, m)\) 是 \(\Pi^0_n\)，如果 \(\neg P(x, m)\) 是 \(\Sigma^0_n\)；
- (iii) 谓词 \(P(x, m)\) 是 \(\Sigma^0_{n+1}\)，当且仅当存在一个 \(\Pi^0_n\)-谓词 \(R(x, y, m) \in \omega^\omega \times \omega^\omega \times \omega\)，使得 \(P(x, m)\) 当且仅当 \((\exists y)R(x, y, m)\)。
- (iv) 谓词 \(P(x, m)\) 是 \(\Delta^0_1\)，当且仅当它既是 \(\Pi^0_1\) 也是 \(\Sigma^0_1\)。
- (v) 谓词 \(P\) 是 *解析的*，如果存在某个 \(n\) 使得 \(P \in \Sigma^1_n\)。

如同引理 1.1.5 所示，我们有以下易于验证的事实。

### Lemma 1.1.7.

- (i) 设 \(n < \omega\)。存在一个 \(\Sigma^1_n\)-集 \(U \subseteq \omega^\omega \times \omega^\omega\)，使得对每个 \(P \in \Sigma^1_n\)，都存在某个 \(y\) 使得 \(P = \{x \mid (x, y) \in U\}\)。
- (ii) 对每个 \(n\)，\(\Sigma^1_n \subset \Delta^1_{n+1} \subset \Sigma^1_{n+1}\) 且 \(\Pi^1_n \subset \Delta^1_{n+1} \subset \Pi^1_{n+1}\)。
- (iii) 每个算术集都是 \(\Delta^1_1\)。

关于解析集的更多基本事实可参见 Jech [53]。对 \(\sigma \in \omega^{<\omega}\)，令 \([\sigma]\) 表示 \(\omega^\omega\) 中扩展 \(\sigma\) 的函数集合。我们说函数 \(f : \omega^\omega \to \omega^\omega\) 属于类 \(\Gamma\)，如果 \(\{(x, \sigma) \in \omega^\omega \times \omega^{<\omega} \mid x \in f^{-1}([\sigma])\} \in \Gamma\)。注意，每个 \(\Sigma_1^1\)-函数都是连续的。

以下命题是直接的。

### Proposition 1.1.8.

- (i) 如果 \(f : \omega \to \omega\) 是全函数，则 \(f \in \Sigma_2^0\) 当且仅当 \(f \in \Delta_2^0\)。
- (ii) 函数 \(f : \omega^\omega \to \omega^\omega\) 是 \(\Sigma_1^1\) 当且仅当其图 \(G' = \{(x, y) \mid f(x) = y\}\) 是 \(\Sigma_1^1\)；如果 \(f\) 是 \(\Pi_1^1\)，则 \(G' \in \Pi_1^1\)；如果 \(f\) 是 \(\Delta_1^1\)，则 \(G' \in \Delta_1^1\)。
- (iii) 如果 \(f\) 是全函数，则 \(G'\) 是 \(\Delta_1^1\) 当且仅当 \(f\) 是 \(\Delta_1^1\)。
- (iv) 如果 \(f : \omega^\omega \to \omega^\omega\) 是全函数，则 \(f \in \Sigma_1^1\) 当且仅当 \(f \in \Delta_1^1\)。

证明。(i) 显而易见。对于 (ii)，注意 \((x, y) \in G'\) 当且仅当 \((\forall n)(\forall \sigma \prec x \in f^{-1}([\sigma]))\)。因此，如果 \(f\) 是 \(\Sigma_1^1\)（或 \(\Pi_1^1\)），则 \(G'\) 是 \(\Sigma_1^1\)（或 \(\Pi_1^1\)）。此外，如果 \(G'\) 是 \(\Sigma_1^1\)，则 \(x \in f^{-1}([\sigma])\) 当且仅当 \((\exists y)(\forall \sigma \prec x, (y) \in G')\)。所以 \(f\) 是 \(\Sigma_1^1\) 当且仅当其图 \(G' = \{(x, y) \mid f(x) = y\}\) 是 \(\Sigma_2^1\)。
(iii). 如果 \(f\) 是全函数，则 \(x \in f^{-1}([\sigma])\) 当且仅当 \((\forall y)(\forall \tau \prec x \in f^{-1}([\tau]))\)。
(iv). 如果 \(f\) 是全函数，则 \(x \in f^{-1}([\sigma])\) 当且仅当 \((\forall y)(\forall \sigma \prec x, y) \in G'\)。所以如果 \(G'\) 是 \(\Sigma_n^1\)，则 \(f\) 是 \(\Pi_n^1\)。由 (iii)，\(f\) 是 \(\Delta_n^1\)。

给定 \(\omega^{<\omega}\) 中的 \(\sigma_i\) 和 \(\sigma'_i\)，其中 \(i \le n\)，如果对每个 \(i\) 都有 \(\sigma'_i \subseteq \sigma_i\)，则我们说 \((\sigma'_0, \dots, \sigma'_n)\) 是 \((\sigma_0, \dots, \sigma_n)\) 的子串。假设树 \(T \subseteq \omega^{<\omega} \times \dots \times \omega^{<\omega}\)（\(n\)-重积）具有如下性质：如果 \((\sigma_0, \dots, \sigma_n) \in T\)，则其所有子串都在 \(T\) 中。出于我们的目的，所有树都向下生长，根在顶部。以下树表示定理为 \(\Sigma_1^1\)-实数集提供了有用的图景。

### Proposition 1.1.9.

谓词 \(P(x, m)\) 是 \(\Sigma_1^1\) 当且仅当存在递归树的递归序列 \(\{T_m\}_{m < \omega}\)，使得 \(T_m \subseteq \omega^{<\omega} \times \omega^{<\omega}\) 且

\(P(x, m) \Leftrightarrow (\exists y)(\forall n)(\langle x \mid n, y \mid n \rangle \in T_m).\)

证明。谓词 \(P(x, m)\) 是 \(\Sigma_1^1\) 当且仅当存在一个部分递归函数 \(\Phi(\sigma, \tau, m)\)，它满足定义 1.1.1 的性质 (i)—(iii)，使得 \(P(x, m) \Leftrightarrow (\exists y)(\forall k)(\Phi(x \mid k, y \mid k, m) \downarrow \to \Phi(x \mid k, y \mid k, m) \neq 0)\)。在阶段 \(\max\{|\sigma|, |\tau|\}\) 时，当且仅当 \(\Phi(\sigma, \tau, m) \downarrow\) 或 \(\Phi(\sigma, \tau, m) \neq 0\) 时，将 \((\sigma, \tau)\) 放入 \(T_m\)。我们留给读者验证 \(\{T_m\}_{m \in \omega}\) 满足要求。

### 1.1.3 \(\Sigma_1^1\)-实数集

实数集是 \(\Sigma_1^1\)，当且仅当存在一个 \(\Sigma_1^1\)-谓词 \(P\)（可能带有数参数 \(m\)），使得 \(P(x, m)\) 成立当且仅当 \(x\) 属于该集合。实数集是 \(\Pi_1^1\)，当且仅当其补集是 \(\Sigma_1^1\)。\(\Sigma_1^1\) 和 \(\Pi_1^1\)-实数集在高阶递归论中都扮演着重要角色。在本节中，我们介绍关于这些集合的一些基本事实。

回顾，\( P \subseteq \omega^\omega \) 是完美的，如果它是没有孤立点的闭集。下一定理表明，每个不可数的 \(\Sigma^1_1\)-实数集都具有可称为完美集性质的性质。

### Theorem 1.1.10 (Suslin [162]).

如果 \( P \) 是 \(\Sigma^1_1\) 且不可数，则它包含一个完美子集。

证明。假设 \( P(x) \) 是 \(\Sigma^1_1\)（为简化起见，假定没有定义 \( P \) 的数变量）。我们给出定理 1.1.10 的两个证明。一个是集合论的，另一个是递归论的。

集合论证明。由命题 1.1.9，存在递归树 \( T \subseteq \omega^{<\omega} \times \omega^{<\omega} \)，使得 \( x \in P \) 当且仅当 \( (\exists y)(\forall n)[x \mid y, n) \in T \)。令 \( T' \) 为 \( T \) 的子树，使得

\( (\sigma, \tau) \in T' \iff \{x > \sigma \mid (\exists y > \tau)(\forall n)(\langle x \mid y, n \rangle \in T)\} > \aleph_0 \)。

定义

\( Q = \{x \mid (\exists y)(\forall n)(\langle x \mid y, n \rangle \in T'\} \)。

由于 \( P \) 是不可数的，\( Q \) 非空。显然 \( Q \subseteq P \)。注意，如果 \( (\sigma, \tau) \in T' \)，则存在 \( k \) 和 \( k' \) 使得 \( (\sigma \mid k, \tau \mid k') \in T' \)。我们将证明 \( Q \) 包含一个完美集。通过对 \( n \) 归纳，构造一棵完美树 \( S_0 \) 和一棵树 \( S_1 \)，具有以下性质：

- (i) \( S_1 \subseteq T' \);
- (ii) 令 \( [S_0] \) 表示 \( S_0 \) 中的无限路径集合。则 \( [S_0] \) 包含于 \( \{x \mid (\exists y)(\forall n)(\langle x \mid y, n \rangle \in S_1\}\) 中；
- (iii) \( (\forall(\sigma, \tau) \in S_1)(\{x > \sigma \mid (\exists y > \tau)(\forall n)(\langle x \mid y, n \rangle \in T)\} > \aleph_0) \)。

我们从第 0 层开始，令 \( S_0 \) 和 \( S_1 \) 为空。假设我们在第 \( n+1 \) 层。令 \( \sigma \in S_0 \) 为第 \( n \) 层定义且 \( |\sigma| = n \)。由归纳假设，存在 \( \tau \) 使得 \( (\sigma, \tau) \in S_1 \) 在第 \( n \) 层被定义，且 \( Q_{\sigma, \tau} = \{x > \sigma \mid (\exists y > \tau)(\forall n)(\langle x \mid y, n \rangle \in T)\} \) 是不可数的。

声明。存在 \(\sigma\) 的不兼容扩展 \(\sigma_0, \sigma_1\)，使得 \( Q_{\sigma_0, \tau} \) 和 \( Q_{\sigma_1, \tau} \) 都是不可数的。

如果声明为假，则存在唯一的 \( x > \sigma \)，使得如果 \(\sigma' > \sigma\) 与 \( x \) 不兼容，则 \( Q_{\sigma', \tau} \) 是可数的。但这将意味着 \( Q_{\sigma, \tau} = \{x\} \cup \bigcup_{\sigma' > \sigma, \sigma' \neq x} Q_{\sigma', \tau} \) 是可数的，这与假设矛盾。

按声明固定 \((\sigma_0, \sigma_1)\)。则存在 \(\tau_0, \tau_1 > \tau\)，使得对 \( i = 0, 1 \)，\( |\{x > \sigma_i \mid (\exists y > \tau_i)(\forall n)(\langle x \mid y, n \rangle \in T)\}| > \aleph_0 \)。将 \(\sigma_0\) 和 \(\sigma_1\) 放入 \( S_0 \)，并将 \((\sigma_i, \tau_i)\)，对 \( i = 0, 1 \)，放入 \( S_1 \)。该过程对每个 \(\sigma \in S_0\) 进行。显然 \( S_0 \) 是一棵完美树，且对每个 \( x \) 存在 \( y \) 使得 \( (\forall n)(\langle x \mid y, n \rangle \in S_1 \)。由于 \( S_1 \subseteq T' \subseteq T \)，\( [S_0] \subseteq Q \subseteq P \)。





递归论证明。如上所述，我们有一棵递归树 \( T \subseteq \omega^{<\omega} \times \omega^{<\omega} \)，使得 \( x \in P \) 当且仅当 \( (\exists y)(\forall n)(\langle x \mid n, y \mid n \rangle \in T) \)。我们对树进行如下的康托尔-本迪克森式操作：

在第 0 阶段，令 \( T_0 = T \)。
在极限阶段 \( \alpha \)，令 \( T_\alpha = \bigcap_{\beta < \alpha} T_\beta \)。
在继阶段 \( \alpha + 1 \)，令
\( T_{\alpha+1} = \langle (\sigma, \tau) \in T_\alpha \mid (\exists \sigma_0 > \sigma)(\exists \tau_0 > \tau)(\exists \sigma_1 > \sigma)(\exists \tau_1 > \tau)((\sigma_0, \tau_0) \in T_\alpha \land (\sigma_1, \tau_1) \in T_\alpha \land \sigma_0|\sigma_1) \rangle \)。

观察到对于所有 \( \alpha \ge \beta \)，有 \( T_\alpha \subseteq T_\beta \)。而且，对于任何继序数 \( \alpha + 1 \)，如果 \( T_{\alpha+1} \neq T_\alpha \)，则存在 \( (\sigma_\alpha, \tau_\alpha) \in T_\alpha \setminus T_{\alpha+1} \)。注意，对于任何 \( \alpha \neq \beta \)（若这些已定义），都有 \( (\sigma_\alpha, \tau_\alpha) \neq (\sigma_\beta, \tau_\beta) \)。由于集合 \( \omega^{<\omega} \times \omega^{<\omega} \) 是可数的，存在一个最小可数序数 \( \gamma \)，使得 \( (\sigma_\gamma, \tau_\gamma) \) 不存在。那么 \( T_\gamma = T_{\gamma+1} \)，因此对于任何 \( \alpha \ge \gamma \)，都有 \( T_\gamma = T_\alpha \)。通过将上述集合论证明中的 \( T' \) 替换为 \( T_\gamma \)，我们得出 \( P \) 包含一个完备子集。

### 备注 1.1.11.

- (i) 上述证明提出了两个有趣的问题。首先，所得完备子集的复杂度是什么？由于陈述“\( P \) 是不可数的”在算术中不是二阶可定义的，所定义的完备子集通常既不是 \( \Sigma^1_1 \) 也不是 \( \Pi^1_1 \)。然而，我们将通过更强大的递归论证法稍后证明其复杂度可以被控制（参见练习 1.5.5）。其次，使得 \( T_\gamma = T_{\gamma+1} \) 的最小序数 \( \gamma \) 是什么？我们将稍后给出该序数的计算（参见命题 3.6.10）。

- (ii) 一般来说，并非每个不可数集都具有完备集性质。事实上，“\( \Sigma^1_1 \)-性”是最佳可能的，因为在 ZFC 中不能证明每个 \( \Pi^1_1 \)-集都具有完备集性质（参见推论 4.3.6）。

### 命题 1.1.12. 假设 \( \{P_i\}_{i < \omega} \) 是实数集的一个序列，使得对于任何非空的 \( \Sigma^1_1 \)-集 \( A \) 和 \( i < \omega \)，\( A \cap P_i \) 包含一个非空的 \( \Sigma^1_1 \)-集。令 \( P \) 为 \( \Sigma^1_1 \) 且非空。那么 \( P \cap \bigcap_{i < \omega} P_i \neq \emptyset \)。

证明。根据假设，存在一个非空的 \( \Sigma^1_1 \)-集 \( F_0 \subseteq P \cap P_0 \)。根据命题 1.1.9，存在一棵递归树 \( T \subseteq \omega^{<\omega} \times \omega^{<\omega} \)，使得 \( x \in F_0 \iff (\exists y)(\forall n)(\langle x \mid n, y \mid n \rangle \in T) \)。修正这样一对 \( (x, y) \)，使得 \( (\forall n)(\langle x \mid n, y \mid n \rangle \in T \)。定义 \( \sigma_0 = x \mid 1 \) 和 \( \tau_0 = y \mid 1 \)。注意 \( G_0 = \{x > \sigma_0 \mid (\exists y > \tau_0)(\forall n)(\langle x \mid n, y \mid n \rangle \in T) \} \) 是一个非空的 \( \Sigma^1_1 \)-集。假设通过归纳，对于所有 \( i' \le i \)，一对 \( (\sigma_{i'}, \tau_{i'}) \in T \) 和一个非空的 \( \Sigma^1_1 \)-集 \( G_{i'} \subseteq P_{i'} \) 已被定义，使得

- (1) \( (\forall i' < i)(G_{i'} \supseteq G_{i'+1}) \wedge (\tau_{i'} < \tau_{i'+1}) \)
- (2) \( (\forall i' \le i)(G_{i'} \subseteq P_{i'}) \)
- (3) \( (\forall i' < i)(G_{i'} \supseteq G_{i'+1} \wedge (\forall x \in G_{i'})(x > \sigma_{i'} \wedge (\exists y > \tau_{i'})(\forall n)(\langle x \mid n, y \mid n \rangle \in T)) \)。

由于 \( G_i \) 是 \( \Sigma^1_1 \)，存在一个非空的 \( \Sigma^1_1 \)-集 \( F_{i+1} \subseteq P_{i+1} \cap G_i \)。而且，根据 (3)，每个 \( x \in F_{i+1} \) 都扩展 \( \sigma_i \)，并且存在一个 \( y > \tau_i \)，使得对于所有 \( n \)，\( (\langle x \mid n, y \mid n \rangle \in T \)。修正这样一对 \( (x, y) \)。定义 \( \sigma_{i+1} = x \uparrow (|\sigma_i| + 1) \) 和 \( \tau_{i+1} = y \uparrow (|\tau_i| + 1) \)。令

\(G_{i+1} = \{x \in F_{i+1} \mid x > \sigma_{i+1} \land (\exists y > \tau_{i+1})(\forall n)((x \upharpoonright n, y \upharpoonright n) \in T)\}.\)

那么 \(G_{i+1}\) 是 \(F_{i+1}\) 的一个非空 \(\Sigma^1_1\)-子集，因此也是 \(P_{i+1}\) 的一个非空 \(\Sigma^1_1\)-子集。令 \(x(i) = m\) 当且仅当 \(\sigma_{i+1}(i) = m\)，且 \(y(i) = m\) 当且仅当 \(\tau_{i+1}(i) = m\)。那么对于所有 \(i\)，\(x \in G_i\)，且对于所有 \(n\)，\((x \upharpoonright n, y \upharpoonright n) \in T\)。因此 \(x \in P \cap \bigcap_{n < \omega} P_i\)。

作为命题 1.1.12 的结果，我们可以如下定义甘迪拓扑。

### 定义 1.1.13. \(\omega^\omega\) 上的甘迪拓扑是通过将所有 \(\Sigma^1_1\)-集作为基本开集所生成的拓扑。

命题 1.1.12 蕴含甘迪拓扑满足贝尔范畴定理：可数个稠密开集的交集是稠密的。

### 1.1.4 \(\Pi^1_1\)-实数集

根据命题 1.1.9，我们有以下结论：

### 命题 1.1.14. 谓词 \(P(x, m)\) 是 \(\Pi^1_1\) 当且仅当存在递归树的递归序列 \(T_m \in \omega^{<\omega} \times \omega^{<\omega}\)，使得 \(P(x, m) \leftrightarrow (\forall y)(\exists n)((x \upharpoonright n, y \upharpoonright n) \notin T_m)\)。

对于每个实数 \(x\)，在 \(\omega\) 上定义一个二元关系 \(\le_x\)，使得 \(m \le_x n\) 当且仅当 \(x(<m, n>) = 1\)。定义

\(WF_1 = \{x \in \omega^\omega \mid \le_x \text{ 是一个良基关系}\}.\)

那么 \(x \in WF_1\) 当且仅当

\((\forall f \in \omega^\omega)[(\forall n)(\forall m)(n \ge m \rightarrow f(n) \le f(m)) \rightarrow (\exists m)(\forall n)(\forall k)(n > m \land k > m \rightarrow f(n) = f(k))],\)

因此 \(WF_1\) 是一个 \(\Pi^1_1\)-实数集。修正 \(\omega^{<\omega}\) 的一个标准有效枚举 \(\{\sigma_n\}_{n < \omega}\)。我们说 \(x\) 编码一棵树关系，如果

\(m \le_x n \leftrightarrow \sigma_m \succeq \sigma_n.\)

现在令 \(P\) 成为一个 \(\Pi^1_1\)-实数集，并令 \(T\) 成为一棵递归树，使得 \(x \in P \leftrightarrow (\forall y)(\exists n)((x \upharpoonright n, y \upharpoonright n) \notin T)\)。定义 \(T_x = \{\sigma \mid (|\sigma|, |\sigma|) \in T\}\)。那么 \(x \in P\) 当且仅当 \(T_x\) 是良基的。在字符串上定义克莱尼-布劳尔序 \(<_{KB}\)，使得对于任何 \(\sigma, \tau \in \omega^{<\omega}\)，\(\sigma <_{KB} \tau\) 当且仅当

\(\sigma \succ \tau (\exists i \le \min[|\sigma|, |\tau|])(\sigma \upharpoonright i = \tau \upharpoonright i \land \sigma \upharpoonright i \prec \tau(i)).\)

换句话说，只要 \(\sigma\) 扩展 \(\tau\) 或 \(\sigma\) 在 \(\tau\) 的“左侧”，就有 \(\sigma \prec_{KB} \tau\)。那么对于每个 \(x\)，\(x\) 编码一棵良基树当且仅当 \(x\) 在 \(<_{KB}\) 下编码一个良序。

令 \(T \subseteq \omega^{<\omega} \times \omega^{<\omega}\) 成为一棵见证 \(P\) 是 \(\Pi^1_1\) 的递归树。因此 \(x \in P\) 当且仅当 \((\forall y)(\exists n)[x \mid n, y \mid n] \notin T\)。定义 \(f(x) = z\) 当且仅当 \(z\) 是编码树 \(T_x\) 的唯一实数。显然 \(f\) 是一个定义良好的递归函数。而且，\(P(x)\) 当且仅当 \(f(x) \in \text{WF}_1\)。

定义 \(\text{WO}_1 = \{x \mid x \text{ 编码一个良序}\}\)。

那么 \(x \in \text{WO}_1\) 当且仅当 \(x \in \text{WF}_1 \land (\forall n)(\forall m)(n \le_R m \lor m \le_R n)\)。因此 \(\text{WO}_1\) 是 \(\Pi^1_1\)。那么对于每个 \(\Pi^1_1\)-集 \(P\)，存在一个递归函数 \(f\)，使得 \(x \in P\) 当且仅当 \(f(x) \in \text{WO}_1\)。

令 \(\{R_e\}_{e<\omega}\) 成为递归可枚举（r.e.）二元关系的一个有效枚举。那么集合

\(\text{WF}_0 = \{e \mid R_e \text{ 是良基的}\}\)

是 \(\Pi^1_1\)。令 \(x \subseteq \omega\) 成为一个 \(\Pi^1_1\)-集，并令 \(T \subseteq \omega^{<\omega} \times \omega\) 成为一棵递归树，使得 \(n \in x\) 当且仅当 \((\forall y)(\exists m)[y \mid m, n] \notin T\)。显然存在一个递归函数 \(f\)，使得对于任何 \(n\)，\(T_n = \{\sigma \mid (\sigma, n) \in T\} = R_{f(n)}\)。那么 \(n \in x\) 当且仅当 \(R_{f(n)}\) 是一个良基二元关系。换句话说，\(x\) 对 \(\text{WF}_0\) 多一归约。根据上面相同的论证，每个 \(\Pi^1_1\)-数集都对 \(\Pi^1_1\)-集 \(\text{WO}_0 = \{e \mid R_e \text{ 是一个良序}\}\) 多一归约。

注意 \(\text{WF}_1\) 的序数高度可能高达 \(\omega_1\)。一个有趣的问题是 \(\text{WF}_0\) 的序数高度。换句话说，哪个最小序数不是良基递归树的序数？我们将看到这个序数，记作 \(\omega_1^{\text{CK}}\)，是一个可数序数。

以下命题提供了 \(\Sigma^1_1\)-实数集与 \(\Pi^1_1\)-\(\omega\) 子集之间的一个有趣联系。

### 命题 1.1.15 (Spector [153]). 假设 \(P\) 是一个 \(\Sigma^1_n\)-实数集。那么

- (i) \(\bigcap_{k \in \omega} x\) 是一个 \(\Pi^1_n\)-整数集。

- (ii) 如果 \(P\) 有一个唯一元素 \(x\)，那么 \(x\) 是 \(\Delta^1_n\)。

证明。对于 (i)：\(n \in \bigcap_{k \in \omega} x \iff (\forall x)(P(x) \to n \in x)\)。

对于 (ii)：\(n \in x \iff (\forall y)(P(y) \to n \in y) \leftrightarrow (\exists y)(P(y) \land n \in y)\)。

命题 1.1.15 非常有用。首先，(i) 表明通过取一个 \(\Sigma^1_1\) 条件的交集，可以得到一个 \(\Pi^1_1\)-集。其次，(ii) 在数集与实数集之间提供了一个联系。(ii) 中的唯一实数被称为一个 \(\Sigma^1_n\) 单点。根据 (ii)，每个 \(\Pi^1_n\) 单点都是 \(\Delta^1_{n+1}\)。如我们将看到的（参见命题 1.2.5），这是最佳可能的。一般来说，就单点集而言，数集与实数集之间的联系是薄弱的。例如，将证明一个 \(\Pi^0_2\)-单点本身可能具有比 \(\Pi^0_2\) 复杂得多的定义（另见练习 1.1.5）。





### 1.1.5 相对化

如同在经典递归论中，上述所有结果均可相对化到一个实数 \( x \)。我们使用带波浪号的粗体符号 \( \Sigma_n^0, \Pi_n^0, \Delta_n^0, \Sigma_n^1, \Pi_n^1 \) 和 \( \Delta_n^1 \) 来表示相对化到一个实数的相应集合（数或实数的集合）。如果一个集合属于某个 \( n \) 的 \( \Pi_n^1 \)，则称该集合为*投影集*。

### 1.1.6 练习

**练习 1.1.1.** *证明一个集合* \( P \subseteq 2^\omega \) *是* \( \Delta_1^0 \) *当且仅当它由递归谓词定义。*

**练习 1.1.2.** *证明存在一个* \( \Pi_1^0 \)*-全函数，但它不是* \( \Delta_1^0 \).*。

**练习 1.1.3.** *证明每个闭不可数集合* \( P \subseteq \omega^\omega \) *都可分解为一个可数集合与一个完备集合的并。*

**练习 1.1.4.** *证明每个不可数集合* \( P \subseteq \omega^\omega \) *都可分解为一个可数集合与一个没有孤立点的集合的并。*

**练习 1.1.5.** *证明* \( \emptyset^{(\omega)} \in 2^\omega \) *是一个* \( \Pi_2^0 \)*-单点集，但不是* \( \Pi_1^0(x) \)*-单点集，对于任意* \( x \not\geq_T \emptyset^{(\omega)} \).*。

### 1.2 序数记号

描述性集合论的一个关键目标是在 ZFC 系统内研究实数及实数集合的性质。然而，关于高于 \( \Pi_1^1 \) 层级的复杂性类的许多陈述都与 ZFC 独立。因此，深入研究 \( \Pi_1^1 \)-集合的性质是自然而然的。高阶递归论为此目的提供了理想的平台以及强大的工具。在本节中，我们将介绍递归序数和序数记号的概念，这是分析 \( \Pi_1^1 \)-集合的核心。递归序数允许人们在序数 \( \omega_1^{CK} \) 上进行类似于在 \( \omega_1 \) 上进行跨诱导的有效跨诱导。

#### 1.2.1 Kleene 的 O

令 \( \langle . \rangle : \omega \times \omega \to \omega \) 为一个递归双射。定义一个算术集合 \( P \subseteq 2^\omega \)，使得 \( x \in P \) 当且仅当 \( x \) 满足以下条件：

- (i) \( (1, 2) \in x \);
- (ii) \( (\forall m)(\forall n)((m, n) \in x \to \langle n, 2^n \rangle \in x) \);
- (iii) \( (\forall e)((\forall n)(\Phi_e(n) \downarrow \land (\forall n)(\Phi_e(n), \Phi_e(n+1)) \in x) \to (\forall n)((\Phi_e(n), 3 \cdot 5^e \in x)) \);
- (iv) \( (\forall n)(\forall m)(\forall k)((n, m) \in x \land (m, k) \in x \to \langle n, k \rangle \in x) \).

因此 (i) 蕴含 \(x\) 非空；(ii) 表示 \(x\) 在后继下“封闭”，(iii) 表示它在极限下“封闭”；(iv) 断言 \(x\) 定义了一个传递关系。我们引入以下记法。

### 定义 1.2.1.

\(<_\mathcal{O} = \bigcup_{\beta < \alpha} x\)。\(\mathcal{O} = \{n \mid (\exists m)(n <_\mathcal{O} m)\}\)。

根据命题 1.1.5，\(<_\mathcal{O}\) 是一个 \(\Pi^1_1\)-关系，且 \(\mathcal{O}\) 是 \(\Pi^1_1\)。我们通过归纳定义一个集合 \(a\)：

- 第 0 阶。将 (1, 2) 放入 \(a_0\)。
- 第 \(\beta + 1\) 阶。若在阶 \(\beta\) 时 \((m, n) \in a_\beta\)，则将 \((n, 2^n)\) 和 \((m, 2^n)\) 放入 \(a_{\beta+1}\)。
- 第 \(\lambda\) 阶。对于极限序数 \(\lambda\)。对于每个使得 \(\Phi_e\) 是全函数且 \((\forall n)(\exists \beta < \lambda)((\Phi_e(n), \Phi_e(n+1)) \in a_\beta)\) 的 \(e\)，对每个 \(n\) 将 \((\Phi_e(n), 3 \cdot 5^e)\) 放入 \(a_\lambda\)。此外，若对某些 \(\beta < \lambda\) 有 \((m, \Phi_e(n)) \in a_\beta\)，则 \((m, 3 \cdot 5^e) \in a_\lambda\)。

令 \(a = \bigcup_\beta a_\beta\)。

验证 \(a \in P\) 且对每个 \(x \in P\) 有 \(a \subseteq x\) 是直接的。因此 \(a = <_\mathcal{O}\)。

定义一个函数 \(|\cdot| : \mathcal{O} \mapsto \omega_1\)，使得 \(|1|=0\) 且 \(|n|\) 是存在一个数 \(m\) 使得 \((m, n) \in a_\beta\) 的最小序数 \(\beta\)。若 \(n \in \mathcal{O}\)，则称 \(n\) 是序数 \(|n|\) 的一个记号。若 \(\beta = |n|\) 对某些 \(n \in \mathcal{O}\) 成立，则称序数 \(\beta\) 是可构造的。显然 \(m <_\mathcal{O} n\) 蕴含 \(|m| < |n|\)。因此 \(<_\mathcal{O}\) 是一个良基偏序。

### 定义 1.2.2.

\(\omega_1^{CK} =\) 大于每个 \(n \in \mathcal{O}\) 的 \(|n|\) 的最小序数 \(\alpha\)。

对序数 \(\beta < \omega_1^{CK}\) 进行归纳，可以轻易看出对于每个 \(n \in \mathcal{O}\)，\(\{m \mid m <_\mathcal{O} n\}\) 在 \(<_\mathcal{O}\) 下是一个线性序。

### 注释 1.2.3.

- (i) 一条路径 \(x \subseteq \mathcal{O}\) 是一个集合，使得

\((\forall m, n \in x)(n <_\mathcal{O} m \lor m <_\mathcal{O} n \lor m = n) \land\)
\((\forall m)(\forall n \in x)(m <_\mathcal{O} n \to m \in x)\)。

一个有趣的问题是：每条路径是否都可以扩展为一条序数高度为 \(\omega_1^{CK}\) 的路径。进行有效跨诱导需要这样的路径。然而，这通常不成立。请注意，在低于 \(\omega_1^{CK}\) 的极限阶段 \(\beta\) 处有许多可能的记号选择。如果每条直到 \(\beta\) 的路径都可扩展为一条序数高度为 \(\omega_1^{CK}\) 的路径，那么就会有 \(2^{\aleph_0}\) 多组记号集合。因此，为了获得穿过 \(<_\mathcal{O}\) 的一条路径，必须谨慎选择记号。我们将展示存在一条穿过 \(<_\mathcal{O}\) 的“行为良好”的 \(\Pi^1_1\)-路径。

- (ii) 不难看出，可构造序数的集合构成一个初始段，因此等于 \(\omega_1^{CK}\)。

### 1.2.2 相对化的 O

如同在 § 1.2.1 中，可以将序数记号的概念相对化到任意实数 \(x \in \omega^\omega\)。令 \(\{\Phi_e(x, n)\}_{e<\omega}\) 为带有神谕 \(x\) 的部分递归函数的有效枚举（参见 § 1.1.1）。定义一个算术集合 \(P \subseteq \omega^\omega \times 2^\omega\)，使得 \((x, y) \in P\) 当且仅当 \(y\) 满足以下条件：

- (i) \((1, 2) \in y\);
- (ii) \((\forall m)(\forall n)((m, n) \in y \to (n, 2^n) \in y)\);
- (iii) \((\forall e)(\langle \Phi_e(x, \cdot) \rangle \text{ is total} \land (\forall n)(\Phi_e(x, n), \Phi_e(x, n + 1)) \in y) \to (\forall n)(\langle \Phi_e(x, n), 3 \cdot 5^e \rangle \in y)\)，且
- (iv) \((\forall n)(\forall m)(\forall k)((n, m) \in y \land (m, k) \in y \to (n, k) \in y)\)。

#### 定义 1.2.4.

\(<_{\mathcal{O}}^P = \bigcap_{(x,y)\in P} y\)。\(\mathcal{O}^P = \{n \mid (\exists m)(n <_{\mathcal{O}}^P m)\}\)。

也可以令相对化的 \(a^x = \bigcup_\beta a_\beta^x\)。那么 \(a^x <_{\mathcal{O}}^x\) 且函数 \(|\cdot|_x : \mathcal{O}^x \mapsto \omega_1\) 是一个定义良好的秩函数，使得 \(|1|_x = 0\) 且 \(|n|_x\) 是存在一个数 \(m\) 使得 \((m, n) \in a_\beta^x\) 的最小序数 \(\beta\)。

请注意，\(\mathcal{O}\) 与 \(\mathcal{O}^P\) 之间存在微妙差异：定义 \(\mathcal{O}^P\) 使用了神谕泛函的一个枚举。因此，定义 \(\mathcal{O}^P\) 所使用的索引集合可能与 \(\mathcal{O}\) 的不同，从而在极限阶段产生可能不同的记号。然而，这种差异不影响 \(\mathcal{O}\) 的整体性质。事实上，如果需要，可以将 \(\mathcal{O}\) 重新定义为 \(\mathcal{O}^P\)。

根据命题 1.1.15 的相对化版本，\(<_{\mathcal{O}}^P\) 和 \(\mathcal{O}^P\) 均为 \(\Pi_1^1(x)\)。以下命题立即成立。

#### 命题 1.2.5.

- (i) 集合 \(\{(n, x) \mid n \in \mathcal{O}^x\}\) 和 \(\{((m, n), x) \mid m <_{\mathcal{O}}^x n\}\) 是 \(\Pi_1^1\)。
- (ii) 集合 \(\{(x, y) \mid y = <_{\mathcal{O}}^x\}\) 和 \(\{(x, y) \mid y = \mathcal{O}^x\}\) 是 \(\Pi_1^1\)。

证明。令 \(P\) 为定义 1.2.4 之前定义的实数集合。对于 (i)，\(n \in \mathcal{O}^x\) 当且仅当 \((\exists m)(m, n) \in <_{\mathcal{O}}^x\) 当且仅当 \((\exists m)(\forall y)((x, y) \in P \to (n, m) \in y)\)。

对于 (ii)，请注意 \(y = <_{\mathcal{O}}^x\) 当且仅当 \((x, y) \in P\) 且 \((\forall z)((x, z) \in P \to (\forall n)(n \in y \to n \in z))\)，这属于 \(\Pi_1^1\)。我们将 (ii) 的另一部分留作练习。

命题 1.2.5 有一些有趣的推论。例如，考虑集合 \(\mathcal{O} = \{0\}\)。那么 \(x \in \mathcal{O}\) 当且仅当 \((0, x) \in \{(x, y) \mid y = \mathcal{O}^x\}\)。因此 \(\mathcal{O}\) 是一个 \(\Pi_1^1\)-单点集，其唯一成员仅为 \(\Pi_1^1\)。

如同在 § 1.2.1 中，可以定义 \(x\)-可构造序数的概念，并将最小的非 \(x\)-可构造序数记为 \(\alpha_1^x\)。请注意，在极限阶段，不同的神谕集合 \(x\) 可能为记号使用不同的索引 \(e\)。因此，不同的 \(x\) 可能有不同的 \(\mathcal{O}^x\)。此外，对于具有“足够计算能力”的 \(x\)，可能有 \(\alpha_1^x > \omega_1^{CK}\)。我们将在适当的时候给出该性质的一个刻画。





#### 1.2.3 练习

练习 1.2.1. 完成命题 1.2.5 的证明。

### 1.3 有效超限归纳

#### 1.3.1 递归定理

引入递归序数的动机是为了执行有效超限归纳。在本节中，我们首先回顾以下著名的递归定理（也称为 Kleene 不动点定理），以使其精确化。

#### 定理 1.3.1 (Kleene).
假设 $f : \omega \to \omega$ 是递归的。则存在某个 $e$，使得 $\Phi_{f(e)} = \Phi_e$。

证明. 根据 s-m-n 定理，存在递归函数 $g$，使得对每个 $e$ 都有 $\Phi_{g(e)} = \Phi_{f(e)}$。令 $i'$ 为递归函数 $f \circ g$ 的索引。则 $\Phi_{i}(g(i)) = \Phi_{f(i)} = \Phi_{g(i)}$。

递归定理在经典递归论中研究有效可计算性时是一个强大的工具。在高阶递归论中，它被用于有效超限归纳。以下命题是此类应用的首个例证。

#### 命题 1.3.2 (Sacks [123]).
设 $<_R$ 为 $\omega$ 上的一个具有最小元的序关系。假设 $f$ 是一个递归函数，使得对所有 $e \in \omega$：(i) 对于 $<_R$ 域中的每个 $n$，若对所有 $m <_R n$ 都有 $\Phi_{f(i)}(m)$ 定义，则 $\Phi_e(n)$ 定义；(ii) $\Phi_e(e)$ 在 $<_R$ 的每个最小元上定义。则存在一个索引 $i$，使得 $\Phi_i = \Phi_{f(i)}$ 且 $\Phi_i$ 在 $R$ 的每个良基初始片段上定义。

证明. 根据定理 1.3.1，存在一个 $i$ 使得 $\Phi_i = \Phi_{f(i)}$。根据 (i)，若 $n$ 是一个 $<_R$-最小元，则 $\Phi_i(n)$ 定义。通过简单的归纳并应用 (ii)，$\Phi_i$ 在 $R$ 的每个良基初始片段上定义。

特别地，若 $R$ 是良基的，则 $\Phi_i$ 在 $R$ 的域上定义。注意，命题 1.3.2 中未对 $R$ 的复杂性做任何假设。只要递归函数 $f$ 存在，我们就可以找到这样的索引 $i$。一般来说，需要关于 $R$ 的某些良好性质来保证 $f$ 的存在。

直观地，$\Phi_e$ 是一个关于 $\Phi_e$ 的“一步有效归纳”算子。对于有效超限归纳，需要假设 $\Phi_e$ 本身是由 $f$ 通过另一个函数 $\Phi_{e'}$ 生成的，即 $\Phi_e = \Phi_{f(e')}$。递归定理表明这是可能的。我们将看到命题 1.3.2 在有效超限归纳中的许多应用。在本章中，我们将对其中一些应用给出详细验证。在后续章节中，此类细节将被省略并留给读者。

#### 1.3.2 序数记号上的算子

我们现在在 $\mathcal{O}$ 上定义一个算子 $+_o$。除了要求它在 $\mathcal{O}$ 上封闭（即 \(m \in \mathcal{O}\) 且 \(n \in \mathcal{O}\) 蕴含 \(m +_o n \in \mathcal{O}\)），我们还要求 \(|m| + |n| = |m +_o n|\)。

设 \(g\) 为一个递归函数，使得对所有 \(e, k, m, n\) 都有

$$
\Phi_{g(e,m,n)}(k) = \Phi_e(m, \Phi_n(k))
$$

直观地，\(g\) 是一个用于处理极限阶段归纳的函数。

根据 s-m-n 定理，存在一个递归函数 \(h\)，使得

$$
\Phi_{h(e)}(m, n) = \begin{cases} m & n = 1, \\ 2^{\Phi_e(m,k)} & n = 2^k, \\ 3 \cdot 5^{g(e,m,k)} & n = 3 \cdot 5^k, \\ 7 & \text{否则.} \end{cases}
$$

根据递归定理，存在一个 \(c\) 使得 \(\Phi_{h(c)} = \Phi_c\)。定义

$$
m +_o n = \Phi_c(m, n).
$$

可以直接验证

$$
m +_o n = \begin{cases} m & n = 1, \\ 2^{m+k} & n = 2^k, \\ 3 \cdot 5^{c(m,k)} & n = 3 \cdot 5^k, \\ 7 & \text{否则.} \end{cases}
$$

注意，对所有 \(n\) 都有

$$
\Phi_{g(e,m,k)}(n) = \Phi_e(m, \Phi_k(n)) = m +_o \Phi_k(n)
$$

显然 $+_o$ 是 $\omega \times \omega$ 上的一个递归函数。以下结果通过在 $<_o$ 上归纳证明。

#### 命题 1.3.3.
函数 $+_o$ 满足以下性质：对所有 $m, n$，

- (i) \(m, n \in \mathcal{O} \Leftrightarrow m +_o n \in \mathcal{O}\).
- (ii) \(m, n \in \mathcal{O} \Longrightarrow |m +_o n| = |m| + |n|\).
- (iii) \(m, n \in \mathcal{O} \text{ 且 } n \neq 1 \Longrightarrow m <_o m +_o n\).
- (iv) \(m \in \mathcal{O} \text{ 且 } k <_o n \Leftrightarrow m +_o k <_o m +_o n\).
- (v) \(m \in \mathcal{O} \land n = k \in \mathcal{O} \Leftrightarrow m +_o n = m +_o k \in \mathcal{O}$.

有效超限归纳的一个有趣应用是以下基本结果。

#### 定理 1.3.4 (Kleene [71]).
存在两个递归函数 $f$ 和 $g$，使得对所有 $n \in \omega$，

- (i) $W_{f(n)} = \{m \mid m <_\omega n\}$,
- (ii) $W_{g(n)} = \{(i, j) \mid i <_\omega j <_\omega n\}$.

证明. (i) 根据 s-m-n 定理，存在两个递归函数 $p, q$，使得

$$
W_{p(e, m)} = \{m\} \cup W_{\phi_e(m)},
$$
$$
W_{q(e, m)} = \bigcup \{W_{\phi_i(\phi_e(n))} \mid n \in \omega\}.
$$

修正 $e_0$ 使得 $W_{e_0} = \emptyset$。定义递归函数 $h$ 如下：

$$
\Phi_{h(e)}(n) = \begin{cases} e_0 & n = 1, \\ p(e, k) & n = 2^k, \\ q(e, k) & n = 3 \cdot 5^k, \\ 0 & \text{否则.} \end{cases}
$$

根据递归定理，存在一个常数 $c$ 使得 $\Phi_{h(c)} = \Phi_c$。令 $f = \Phi_c$。

则

$$
f(n) = \begin{cases} e_0 & n = 1, \\ p(c, k) & n = 2^k, \\ q(c, k) & n = 3 \cdot 5^k, \\ 0 & \text{否则.} \end{cases}
$$

显然 $f$ 是全定的，因为 $p$ 和 $q$ 都是全定的。则

$$
W_{f(n)} = \begin{cases} \emptyset & n = 1, \\ \{k\} \cup W_{f(k)} & n = 2^k, \\ \bigcup \{W_{\phi_i(\phi_e(n))} \mid m \in \omega\} & n = 3 \cdot 5^k, \\ 0 & \text{否则.} \end{cases}
$$

简单的归纳表明，对每个 $n \in \omega$ 都有 $W_{f(n)} = \{m \mid m <_\omega n\}$。

(ii) 根据 s-m-n 定理，存在两个函数 $p$ 和 $q$，使得

$$
W_{p(e, m)} = \{(i, j) \mid i \in W_{f(m)}\} \cup W_{\phi_e(m)},
$$
$$
W_{q(e, m)} = \bigcup \{W_{\phi_i(\phi_e(n))} \mid n \in \omega\},
$$

其中 $f$ 如 (i) 所定义。修正 $e_0$ 使得 $W_{e_0} = \emptyset$。令

$$
\Phi_{h(e)}(n) = \begin{cases} e_0 & n = 1, \\ p(e, k) & n = 2^k, \\ q(e, k) & n = 3 \cdot 5^k, \\ 0 & \text{否则.} \end{cases}
$$

根据递归定理，存在一个常数 $c$ 使得 $\Phi_{h(c)} = \Phi_c$。令 $g = \Phi_c$。

故

$$
g(n) = \begin{cases} e_0 & n = 1, \\ p(c, k) & n = 2^k, \\ q(c, k) & n = 3 \cdot 5^k, \\ 0 & \text{否则.} \end{cases}
$$

注意 $g$ 是全定的，因为 $p$ 和 $q$ 都是全定的。则

$$
W_{g(n)} = \begin{cases} \emptyset & n=1, \\ \{\langle i, k \rangle \mid i <_O k\} \cup W_{g(k)} & n=2^k, \\ \bigcup \{W_{g(\phi_i(m))} \mid m \in \omega\} & n=3 \cdot 5^k, \\ W_0 & \text{否则.} \end{cases}
$$

简单的归纳表明，对 $n \in O$ 都有 $W_{g(n)} = \{\langle i, j \rangle \mid i <_O j <_O n\}$。

定理 1.3.4 允许对 $e \in O$ 统一地进行超限归纳。这里我们给出命题 1.3.3 的两个应用。

#### 引理 1.3.5.
存在一个递归函数 $g$，使得对所有 $e$：

- (i) $g(e) \in O \Leftrightarrow W_e \subseteq \emptyset$.
- (ii) 对每个 $n \in W_e$，$g(e) \in O \leftrightarrow |n|_O < |g(e)|$.

证明. 根据 s-m-n 定理，存在一个递归函数 $r$，使得 $\Phi_{r(e)}(0) = 1$ 且 $\Phi_{r(e)}$ 的值域为 $(W_e \setminus \{0\}) \cup \{1\}$。再次根据 s-m-n 定理，存在一个递归函数 $s$，使得 $\Phi_{s(e)}(0) = 1$ 且 $(\forall n)(\Phi_{s(e)}(n+1) = \Phi_{s(e)}(n) \oplus 2^{\Phi_{r(e)}(n+1)})$。定义

$$
g(e) = 3 \cdot 5^{s(e)}.
$$

注意，若 $W_e \subseteq \emptyset$，则根据命题 1.3.3 有 $g(e) \in O$。若 $g(e) \in O$，则对每个 $n$ 都有 $\Phi_{s(e)}(n) \in O$。因此根据命题 1.3.3 有 $W_e \subseteq O$。

假设 $g(e) \in O$ 且 $n \in W_e$。则 $n <_O \Phi_{s(e)}(m) + 2^n = \Phi_{s(e)}(m+1) <_O 3 \cdot 5^{s(e)} = g(e)$，其中 $m$ 是使得 $\Phi_{r(e)}(m+1) = n$ 的最小数。

作为引理 1.3.5 证明的结果，我们有

#### 推论 1.3.6.
存在一个递归函数 $g$，使得对所有 $e$，若 $W_e \subseteq O$ 且 $W_e$ 上的 $<_O$ 是线性的，则 $g(e) \in O$ 且 $(\forall n)(n \in W_e \rightarrow n <_O g(e))$.

推论 1.3.6 可视为一个 $\Sigma^0_1$-有界性原理，即对于 $O$ 的任何可枚举子集，都有一种有效方法来找到其上界。引理 1.3.5 将在定理 1.5.5 中得到显著加强。

### 1.4 递归序数

递归好序的可能序类型是什么？递归好序与构造序数之间有什么联系？本节将回答这些问题。

#### 定义 1.4.1.
若存在一个序类型为 $\beta$ 的递归好序 $R$，则称序数 $\beta$ 是递归的。

#### 引理 1.4.2.
设 $\{R_e\}_{e \in \omega}$ 为偏递归二元关系的一个有效列表。存在一个递归函数 $f$，使得对所有 $e$，



- (i) $R_e$ 是良基的当且仅当 $f(e) \in \mathcal{O}$。
- (ii) 如果 $R_e$ 是良基的，则 $|R_e| \le |f(e)|$，其中 $|R_e|$ 是 $R_e$ 的高度。

证明。由 s-m-n 定理，存在递归函数 $h$ 使得

$R_{h(e,k)}(m,n) \Leftrightarrow R_e(m,n) \land R_e(k,m) \land R_e(n,k)$

对所有 $e, k, m$ 和 $n$ 成立。$R_{h(e,k)}$ 是 $R_e$ 在 $k$ 之前的初始段。其思想是定义一个从 $R_e$ 的域到 $\mathcal{O}$ 的单射、序保持映射。固定引理 1.3.5 中的递归函数 $g$。如果 $k$ 是 $R_e$ 的最小元，则 $k$ 映射到 $\mathcal{O}$ 中由在引理 1.3.5 中应用 $W_{h(e,k)} = \emptyset$ 确定的元素。否则，通过归纳，$R_{h(e,k)}$ 映射到索引为 $e'$ 的递归可枚举集 $W \subset \mathcal{O}$。由引理 1.3.5，$g(e') \in \mathcal{O}$ 且对所有 $n \in W$ 有 $|n| < g(e')$。因此我们可以定义 $f(k) = g(e')$。

我们现在转向正式证明。首先，存在递归函数 $p$ 使得

$W_{p(e)} = \begin{cases} \emptyset & R_e = \emptyset \\ \{ \Phi_c(h(e,k)) \mid k \in \omega \} & \text{Otherwise.} \end{cases}$

因此存在递归函数 $q$ 使得 $\Phi_{q(e)}(e) = g(p(e))$。由递归定理，存在不动点 $c$ 使得 $\Phi_{q(c)} = \Phi_c$。定义

$f(e) = \Phi_c(e)$

和

$p(e) = p(c, e)$。

则

$W_{p(e)} \text{ 良基} = \begin{cases} \emptyset & R_e = \emptyset \\ \{ \Phi_c(h(e,k)) \mid k \in \omega \} = \{ f(h(e,k)) \mid k \in \omega \} & \text{Otherwise.} \end{cases}$

注意 $f(e) = \Phi_c(e) = \Phi_{g(e)}(e) = g(p(c,e)) = g(p(e))$。

现在假设 $R_e$ 是良基的。如果 $R_e$ 为空，则由引理 1.3.5，$W_{p(e)} = \emptyset \subset \mathcal{O}$ 且 $f(e) \in \mathcal{O}$。假设对所有高度 $|R_e| < \alpha$ 的良基关系 $R_e$，(i) 和 (ii) 成立。固定一个高度 $|R_e| = \alpha$ 的良基关系 $R_e$。那么对于 $R_e$ 域中的每个 $k$，有 $|R_{h(e,k)}| < \alpha$。因此 $W_{h(e,k)} \subset \mathcal{O}$ 且 $f(h(e,k)) \in \mathcal{O}$。于是 $W_{p(e)} = \{ f(h(e,k)) \mid k \in \omega \} \subset \mathcal{O}$。由引理 1.3.5，$f(e) = g(p(e)) \in \mathcal{O}$ 且对所有 $n \in W_{p(e)}$ 有 $f(e) > |n|$。因此 $|f(e)| \ge |R_e|$。

假设 $f(e) \in \mathcal{O}$。由引理 1.3.5，$W_{p(e)} \subset \mathcal{O}$ 且对所有 $n$ 有 $|f(e)| > |f(h(e,n))|$。在 $<_{\mathcal{O}}$ 上进行归纳，对所有 $n$，$R_{h(e,n)}$ 是良基的。因此

$R_e = \bigcup_n (R_{h(e,n)} \cup \{ (m,n) \mid R_e(m,n) \land m \in \omega \})$

是良基的。

我们将下一个引理的证明留给读者（练习 1.5.1）：

#### **引理 1.4.3.** 每个偏递归良序 $R$ 同构于一个递归良序。

本节的主要结果如下：

#### 定理 1.4.4 (Kleene [71], Markwald [89]). 一个序数是递归的当且仅当它是构造的。

证明。假设 $R$ 是一个高度为 $|R| = \beta$ 的递归良序。由引理 1.4.2，存在一个构造序数 $\gamma \ge \beta$。因此 $\beta$ 是构造的。反之，如果 $\beta$ 是构造的，则由定理 1.3.4，存在一个高度为 $|R| = \beta$ 的偏递归良序 $R$。由引理 1.4.3，$\beta$ 是递归的。

#### 1.4.1 练习

- 练习 1.4.1. 证明存在一个集合 $x \subseteq O$，其上 $<_O$ 是序类型为 $\omega^2$ 的良序，以及一个偏递归函数 $p : \omega^2 \to \omega$，使得
- (i) 对于任何 $n \in x$，函数 $p_n$（其中 $p_n(i) = p(n, i)$）是全函数；
- (ii) 对于任何 $n <_O m \in x$，$(\exists j)(i > j \to (p_n(i) < p_m(j)))$，且
- (iii) 对于任何递归函数 $f$，存在一个 $n \in x$ 使得 $(\exists i)(\forall j > i)(f(j) < p_n(j))$。

### 1.5 $\Pi^1_1$-完备性和 $\Sigma^1_1$-有界性

#### 1.5.1 $\Pi^1_1$-完备性

#### 定理 1.5.1. $O \in \Pi^1_1$-完备。因此 $O$ 不是 $\Sigma^1_1$。

证明。由引理 1.4.2，Wf 对 $O$ 多一归约。如在 §1.1.4 中讨论，Wf$_0$ 是 $\Pi^1_1$-完备，因此 $O$ 也是。

我们现在考虑实数集。假设 $P(x, n)$ 是 $\Pi^1_1$。通过相对化定理 1.5.1，存在递归函数 $f_P$ 使得对所有 $n$ 和 $x$ 有 $P(x, n) \Leftrightarrow f_P(n) \in O^x$。特别是，一个 $\Pi^1_1$-谓词 $Q(x)$ 是某个 $\Pi^1_1$-谓词 $P$ 的 $P(x, 0)$。因此 $Q(x)$ 当且仅当存在某个递归函数 $f_Q$ 使得 $f_Q(0) \in O^x$。由此可知集合 $C = \{(x, n) \mid n \in O^x\}$ 是 $\Pi^1_1$-通用的。换句话说，对于每个 $\Pi^1_1$-集 $Q$，存在一个数 $n$ 使得 $Q = \{x \mid (x, n) \in C\}$。不难看出 $C$ 不是 $\Sigma^1_1$。我们还可以通过定义 $D = \{0^n1^x \mid n \in O^x\}$ 将 $C$ 编码为 $2^\omega$ 的一个子集。那么 $D$ 是一个 $\Pi^1_1$-完备集。

#### 1.5.2 $\Sigma^1_1$-有界性

下一个推论被称为 $\Sigma^1_1$-有界原理。我们稍后将看到该原理的若干应用。

#### 推论 1.5.2 (Spector [153]). 假设 $x \subseteq O$ 且 $x \in \Sigma^1_1$。那么存在一个 $n \in O$ 使得对所有 $m \in x$ 有 $|m| \le |n|$。

证明。否则，对于每个 \(\beta < \omega_1^{CK}\)，存在一个元素 \(n \in x\) 使得 \(|n| > \beta\)。

由于 \(\mathbb{O}\) 是 \(\Pi^1_1\)，存在递归函数 \(f\) 使得 \(n \in \mathbb{O}\) 蕴含 \(f(n) \in \text{WF}_0\)。

那么 \(n \in \mathbb{O}\) 当且仅当

\((\exists m)(m \in x \land (\exists h \in \omega^\omega)(\forall i)(R_j(f_{i0}(n), j) \rightarrow \langle h(i), h(j) \rangle \in W_{g(m)}))\),

其中 $g$ 如在定理 1.3.4 中定义。因此 $\mathbb{O}$ 是 $\Sigma^1_1$，产生矛盾。

我们现在转向定理 1.5.5。这可以被视为推论 1.5.2 的一个有效版本。

#### 引理 1.5.3. 存在递归函数 \(f\) 使得 \(n \in \mathbb{O} \Leftrightarrow f(n) \in \text{WF}_0 \land |n| < |R_{f(n)}|\)。

证明。由于 \(\mathbb{O}\) 是 \(\Pi^1_1\)，存在递归函数 \(g\) 使得

$n \in \mathbb{O} \Leftrightarrow g(n) \in \text{WF}_0$。

由定理 1.3.4，存在函数 \(h\) 使得 \(n \in \mathbb{O}\) 蕴含 \(R_{s(n)} = (\langle i, j \rangle | \langle i, j \rangle \in W_{k(n)})\)，$h(n) \in \text{WF}_0$ 且 $|n| = |R_{h(n)}|$，其中 $k(n)$ 是定理 1.3.4 中的第二个函数。定义递归函数 \(s\) 使得 $R_{s(m,n)} =$

$R_m \oplus R_n = \{\langle i, j \rangle | (i, j \in \text{Even} \land (\frac{i}{2}, \frac{j}{2}) \in R_m) \lor (i, j \in \text{Odd} \land (\frac{i-1}{2}, \frac{j-1}{2}) \in R_n)\}$。

那么

$(m \in \text{WF}_0 \land n \in \text{WF}_0) \Leftrightarrow (s(m, n) \in \text{WF}_0 \land \max\{|R_m|, |R_n|\} \le |R_{s(m,n)}|)$。

所以 $n \in \mathbb{O} \Leftrightarrow (g(n) \in \text{WF}_0 \land h(n) \in \text{WF}_0) \Leftrightarrow s(g(n), h(n)) \in \text{WF}_0$ 且 $|n| \le |R_{s(g(n), h(n))}|$。现在令 $f(n) = s(g(n), h(n))$。

给定 $\omega$ 上的两个二元 r.e. 关系 $R_i, R_j$，定义递归函数 $t$ 使得 $R_{t(i,j)} = R_i \otimes R_j$，其中

$R_i \otimes R_j = \{(\langle n_1, m_1 \rangle, \langle n_2, m_2 \rangle) | (n_1, n_2) \in R_i \land (m_1, m_2) \in R_j\}$。

很容易验证 $\langle i, j \rangle \in \text{WF}_0 \Leftrightarrow i \in \text{WF}_0 \lor j \in \text{WF}_0$ 且 $\min\{|R_i|, |R_j|\} \le |R_{t(i,j)}|$。我们有以下推论。

#### 推论 1.5.4. 存在递归函数 \(p\) 使得

$(\forall n)(\forall m)(n \in \mathbb{O} \lor m \in \mathbb{O}) \Leftrightarrow p(m, n) \in \mathbb{O}$，

并且如果 $p(m, n) \in \mathbb{O}$ 则

$\min\{|n|, |m|\} \le |p(m, n)|$，

其中对于 $m \notin \mathbb{O}$ 有 $|m| = \infty$。

证明。令 $f_0$ 为引理 1.4.2 中的递归函数 $f$，$f_1$ 为引理 1.5.3 中的递归函数 $f$，并令 $t$ 如上所述。那么函数 $p(i, j) = f_0(\langle t(f_1i, f_1j) \rangle)$ 正是所需的。

给定偏递归函数的标准枚举 $\Phi_e(n, m, y)$，存在 $\Sigma^1_1$-实数的枚举 $\{x_e\}_{e < \omega}$ 使得 $n \in x_e \leftrightarrow (\exists y)(\forall m)(\Phi_e(n, m, y) \downarrow \rightarrow \Phi_e(n, m, y) \neq 0)$。我们有以下 Spector 的 $\Sigma^1_1$ 有界性原理的有效版本。

#### 定理 1.5.5 (Sacks). 存在递归函数 \(\hat{g}\) 使得

$(\forall n)(x_n \subseteq \mathbb{O} \rightarrow \hat{g}(n) \in \mathbb{O} \wedge x_n \subseteq \mathbb{O}_{\hat{g}(n)})$，

其中 $\mathbb{O}_{\hat{g}(n)} = \{m \in \mathbb{O} \mid |m| < |\hat{g}(n)|\}$。

证明。由于集合 $\{m \mid m \notin \Pi^1_1\}$ 在 $\Pi^1_1$ 中，存在递归函数 $h$ 使得 $m \in x_n \leftrightarrow h(m, n) \notin \mathbb{O}$。令 $p$ 为推论 1.5.4 中的函数。定义递归函数 $f$ 使得 $W_{f(n)} = \{p(h(m, n), m) \mid m \in \omega\}$。如果 $x_n \subseteq \mathbb{O}$，则 $W_{f(n)} \subseteq \mathbb{O}$。令 $\hat{g}(n) = 20^{\overline{f(n)}}$，其中 $\overline{g}$ 是引理 1.3.5 中的函数。由引理 1.3.5，$x_n \subseteq \mathbb{O} \implies \hat{g}(n) \in \mathbb{O}$。如果 $\hat{g}(n) \in \mathbb{O}$，则再次由引理 1.3.5，$W_{f(n)} \subseteq \mathbb{O}$。但是对于所有 $m \in x_n$ 有 $h(m, n) \notin \mathbb{O}$。然后由推论 1.5.4，对于所有 $m \in x_n$ 有 $m \in \mathbb{O}$，因此 $x_n \subseteq \mathbb{O}$。此外，如果 $x_n \subseteq \mathbb{O}$，则 $m \in x_n \implies h(m, n) \notin \mathbb{O} \implies |m| \le |p(h(m, n), m)|$。

由定理 1.5.1，每个 $\Pi^1_1$-集对 $\mathbb{O}$ 多一归约。因此我们可以将 $\mathbb{O}$ 视为枚举一个 $\Pi^1_1$-集的阶段（在引入集合 $\mathbb{O}_1$ 后，这一观点将变得更加清晰）。因此，将 $\Pi^1_1$-集视为 $\Sigma^0_1$（即递归可枚举）集的类比是自然的。现在，如果将“有限集”视为其所有成员都在某个阶段 \(\beta < \omega_1^{CK}\) 被枚举的集合，那么 Spector 的有界性原理表明任何 \(\Delta^1_1\)-集都是“有限”的。我们将通过引入可接受集理论来使其精确。

在可定义性方面，人们会预期递归序的可能序类型与 \(\Sigma^1_1$-序之间存在巨大差距。以下观察表明并非如此。

#### 命题 1.5.6. 假设 \(R\) 是 \(\omega\) 上的一个 \(\Sigma^1_1$ 良序关系。那么 $|R| < \omega_1^{CK}$。

证明。假设 $|R| \ge \omega_1^{CK}$。那么 $n \in W\mathbf{f}_0 \leftrightarrow (\exists \beta)(\forall i)(\forall j)(R_\alpha(i, j) \rightarrow R(h(i), h(j)))$。这意味着 $W\mathbf{f}_0$ 是 \(\Sigma^1_1\)，产生矛盾。

#### 注释 1.5.7. 对于实数集，\(\Delta^1_1$-集有一个有界性原理。如在 §1.1.4 中讨论，对于每个实数的 \(\Pi^1_1$-集 \(A\)，存在递归函数 \(f : \omega^\omega \rightarrow \omega^\omega\) 使得 \(x \in A \Rightarrow f(x) \in \mathbf{wO}\)。那么如果 \(A\) 是 \(\Delta^1_1\)，通过与命题 1.5.6 证明中相同的论证，$f(A)$ 的上确界 \(\beta = \sup\{f(x) \mid x \in A\}\) 小于 \(\omega_1^{CK}$。

对于实数的 \(\Sigma^1_1$ 良序，通过与推论 1.5.2 证明中相同的论证，每个这样的良序的序类型都小于 \(\omega_1^{CK}$。





### 1.5.3 练习

练习 1.5.1. 证明一个部分递归良序同构于一个递归良序。

练习 1.5.2. 证明如果 \(x \in \omega^\omega\) 是一个非递归 \(\Pi^0_1\)-单点，那么存在一个 \(z \equiv_T x\) 和一个 \(\Pi^1_1\)-集 \(P \in 2^\omega\)，使得 \(z\) 是 \(P\) 中唯一的非递归实数。

练习 1.5.3 (Jockusch and Soare [60]). 证明如果 \(P \subseteq 2^\omega\) 是一个非空 \(\Pi^0_1\)-集，那么存在一个 \(x \in P\) 使得 \(x' \not\le_T 0'\)。

练习 1.5.4. 证明每个不可数 \(\Pi^0_2\)-集 \(P \subseteq \omega^\omega\) 包含一个完美集 \([T] = \{x \in \omega^\omega \mid (\forall n)[x \upharpoonright n \in T]\}\)，其中 \(T\) 是一个 \(\Sigma^1_1\)-树。

练习 1.5.5. 证明每个不可数 \(\Sigma^1_1\)-集 \(P \subseteq \omega^\omega\) 包含一个完美集 \([T]\)，其中 \(T\) 是一个在 \(\mathcal{O}\) 中递归的树。

## 2 超算术理论

在本章中，我们介绍超算术层次，并证明超算术集的类恰好是 \(\Delta^1_1\)-集的类。因此，超算术层次为分析 \(\Delta^1_1\)-集和 \(\Pi^1_1\)-集提供了合适的框架。这种等价性还允许在 \(\Delta^1_1\)-集上进行超限归纳。

### 2.1 H-集和 \(\Pi^0_2\)-单点

#### 2.1.1 H-集

**定义 2.1.1.**

- 序列 \(\{H_n\}_{n \in O}\) 通过在 \(O\) 上进行超限归纳定义如下。

```
H_1 = \emptyset,
H_{2^n} = (H_n)', \text{the Turing jump of } H_n
H_{3 \cdot 5^e} = \{\langle m, i \rangle \mid m \in H_{|e|_O(i)}\}.
```

- \(\{H_n\}_{n \in O}\) 的一个成员称为 H-集。如果存在 \(n \in O\) 使得 \(y \le_T H_n\)，则称实数 \(y\) 是超算术的。我们用 HYP 表示所有超算术集的集合。

- 同样，对于任意实数 \(x\)，集合 \(H_n^x\) 对所有 \(n \in O^x\) 定义如下：

```
H_1 = x,
H_{2^n} = (H_n^x)',
H_{3 \cdot 5^e} = \{\langle m, i \rangle \mid m \in H_{|e|_O^x(i)}\}.
```

显然 \(n <_O m\) 蕴含 \(H_n <_T H_m\)。事实上，

**引理 2.1.2 (Kleene).** 存在一个递归函数 \(f\)，使得对所有 \(m, n\)，\(n <_O m\) 蕴含 \(H_n = \Phi^0_{f(n,m)}\)。

证明. 令 \(e_0\) 为一个使得 \(x = \Phi^{e_0}_x\) 的索引，并令 \(p, q\) 为递归函数，使得 \(x = \Phi^{e_0}_x \wedge y = \Phi^{e_0}_m\) 蕴含 \(x = \Phi^{p(n,m)}_x\) 且 \(\Phi^{q(m)}(x) = m\)，其中 \(\langle m, n \rangle \in x\)。按定理 1.3.4 的 (i) 固定一个函数 \(g\)。

通过对 \(<_O\) 进行归纳定义 \(f\)。根据递归定理，我们可以假设如果 \(n <_O m\)，则对于所有 \(m' <_O m\)，\(H_n = \Phi^{f(n,m)}_{f(n,m')}\)。如果 \(m = 2^{m'}\) 对某些 \(m' \in O\)，则 \(\Phi^{f(n,m)}_{f(n,m)} = \Phi^{f(n,m')}_{f(n,m')}\)。如果 \(m = 3 \cdot 5^e\) 对某些 \(i\)，则通过递归搜索一对 \(\langle m', k \rangle\) 使得 \(m' = \Phi_1(k)\) 且 \(n \in W^{g(m')}\)，可以定义 \(\Phi^{H_n}_{f(n,m)} = \Phi^{H_{n'}}_{f(n,m')}\)。

引理 2.1.2 对相对化 H-集依然成立。因此存在一个递归函数 \(f\)，使得对所有 \(x\)，如果 \(n <_{O^x} m\) 则 \(H^x_n = \)。

#### 2.1.2 $\Pi^0_2$-单点

设 \(x\) 为满足类 \(\Gamma\) 中某个谓词的唯一实数。则称 \(x\) 为 \(\Gamma\)-单点。我们已经看到每个 \(\Sigma^1_1\)-单点是 \(\Delta^1_1\) 且 \(\emptyset\) 是一个 \(\Pi^1_1\)-单点。在本节中，我们将证明每个 H-集是一个 \(\Pi^0_2\)-单点。

**引理 2.1.3.** 如果 \(x\) 是一个 \(\Pi^0_2\)-单点，那么 \(x'\) 和任何 \(y \equiv_T x\) 都是 \(\Pi^0_2\) 单点。

证明. 设 \(x\) 为谓词 \(R\) 的 \(\Pi^0_2\)-单点。注意对于每个 \(e\)，集合 \(\{y \mid R(\Phi^y_e)\}\) 是 \(\Pi^0_2\)。令 \(e_0\) 为一个使得对所有 \(y\)，\(\Phi^{y}_{e_0} = y\) 的索引。那么谓词 \(Q(y) \Leftrightarrow R(\Phi^{e_0}_y) \wedge (\forall e)(e \in y \rightarrow (\exists s)(\exists \sigma)(\sigma < y \wedge \Phi^{e_0}_{e_0}[s](e)[s] \downarrow))\) 是 \(\Pi^0_2\)。注意 \(x'\) 是使得 \(Q(y)\) 成立的唯一 \(y\)。如果 \(x = \Phi^{e_0}_y\) 且 \(y = \Phi^{e_0}_x\)，那么谓词 \(S(y) \Leftrightarrow R(\Phi^{y}_{e_0}) \wedge (\forall e)(e \in y \rightarrow (\exists s)(\exists \sigma)(\sigma < y \wedge \Phi^{e_0}_{e_0}[s](e)[s] \downarrow = 1))\) 是 \(\Pi^0_2\) 并见证了 \(y\) 的唯一性。

**定理 2.1.4.** 存在一个 \(\Pi^0_2\)-谓词 \(H\)，使得对所有实数 \(y\) 和 \(n \in O^y\)，\((\exists x)(H(x,n,y)) \wedge H(n,H^y_n,n)\)。

因此每个 \(H^y\)-集是一个 \(\Pi^0_2(y)\)-单点。

证明. 根据递归定理，我们可以假设存在一个 \(\Pi^0_2\)-谓词 \(H(n, x, y)\)，使得对每个 \(m' < \omega\)，\(m \in O^y\)，\((H(m', H^m_n, x))\) 已定义且 \(H^m_n\) 是满足 \(H(m', y, x)\) 的唯一实数。如果 \(m = 2 \cdot 5^k\) 对某些 \(k\)，则当且仅当 \((H^m_n)' = H^m_n \wedge H(m', H^m_n, x)\) 时定义 \(H(m, H^m_n, x)\)。如果 \(m = 3 \cdot 5^k\) 对某些 \(k\)，则当且仅当 \((\forall n)(H(k,n,x))\) 时定义 \(H(m, H^m_n, x)\)。

我们指出，定理 2.1.4 中的条件 \(\Pi^0_2\) 不能被 \(\Sigma^0_2\) 取代。不难证明 \(2^\omega\) 中的每个 \(\Sigma^0_2\)-单点都是递归的。另一方面，\(2^\omega\) 中的每个 \(\Pi^0_2\)-单点都与 \(\omega^\omega\) 中的某个 \(\Pi^0_1\)-单点 Turing 等价。

**命题 2.1.15.** 如果 \(x \in 2^\omega\) 是一个 \(\Pi^0_2\)-单点，那么存在一个 \(\Pi^0_1\)-单点 \(T \subseteq \omega^\omega\)，其唯一成员 \(y\) 与 \(x\) Turing 等价。

证明. 假设 \(x \in 2^\omega\) 是一个 \(\Pi^0_2\) 单点。那么存在一个递归谓词 \(R(n, \sigma)\)，使得 \(x\) 是满足 \((\forall n)(\exists m)(R(n, z \mid m))\) 的唯一实数 \(z\)。我们可以假设 \((\forall n)(\forall \sigma)(R(n, \sigma) \rightarrow |\sigma| \ge n)\)。令 \(T\) 为满足以下条件的 \(y\) 的集合：

- 如果 \(y(n) = \sigma\) 则 \(R(n, \sigma)\)；
- \((\forall \tau < y(n))(\neg R(n, \tau))\)，且
- \((\forall k \le n)(y(k) \le y(n) \vee y(n) \le y(k))\)。

那么 \(T\) 是一个 \(\Pi^0_1\) 集。此外，如果 \(y \in T\)，那么对每个 \(n\)，\(y(n)\) 是满足 \(R(n, \sigma)\) 的 \(x\) 的最短初始段 \(\sigma\)。因此，如果 \(y \in T\)，则 \(\bigcup_{n \in \omega} y(n) = x\)。由此可见 \(y\) 是 \(T\) 中的唯一实数。显然 \(y \equiv_T x\)。

#### 2.1.3 练习

练习 2.1.1. 证明每个 \(\Delta^0_2\)-实数 \(x \in 2^\omega\) 是一个 \(\Pi^0_2\)-单点，但存在 \(2^\omega\) 中的一个 \(\Delta^0_3\)-实数不是 \(\Pi^0_3\)-单点。

### 2.2 \(\Delta^1_1\)-性和超算术性

在本节中，我们证明一个基本结果：一个集合是 \(\Delta^1_1\) 当且仅当它是超算术的。

#### 2.2.1 \(\omega\) 的 \(\Delta^1_1\)-子集

**引理 2.2.1.** 以下两个谓词是 \(\Pi^1_1\)：(i) \(n \in O^\vee \land k \in H^y_n\)，(ii) \(n \in O^\vee \land k \notin H^y_n\)。

证明. 注意 \(n \in O^\vee \land k \in H^y_n\) 当且仅当 \(n \in O^\vee \land (\forall z)(H(n, z, y) \rightarrow k \in z)\)，且 \(n \in O^\vee \land k \notin H^y_n\) 当且仅当 \(n \in O^\vee \land (\forall z)(H(n, z, y) \rightarrow k \notin z)\)。根据命题 1.2.5 和定理 2.1.4，两者都是 \(\Pi^1_1\)。

**推论 2.2.2 (Kleene [69]).** (i) 如果 \(x\) 在 \(y\) 中是超算术的，那么 \(x\) 是 \(\Delta^1_1(y)\)。 (ii) 集合 \(\{(x, y) \mid x \in \text{HYP}^y\}\) 是 \(\Pi^1_1\)。

证明. 如果 \(x\) 在 \(y\) 中是超算术的，那么存在一个 \(H^y\)-集 \(H^y_n\) 使得对某些 \(n \in O^\vee\)，\(x \le_T H^y_n\)。因此对某些 \(e\)，\(x = \Phi^{H^y}_e\)。那么以下两个谓词

```
$k \in x \leftrightarrow (\exists \sigma)(\Phi^e_\sigma(k) = 1 \land \sigma \prec H^y_n)$
```

和

```
$k \notin x \leftrightarrow (\exists \sigma)(\Phi^e_\sigma(k) = 0 \land \sigma \prec H^y_n)$
```

根据引理 2.2.1 都是 \(\Pi^1_1(y)\)。

现在 \(x \in \text{HYP}^y \leftrightarrow (\exists n)(\exists e)(n \in O^\vee \land x = \Phi^{H^y}_e) \leftrightarrow (\exists n)(\exists e)(\forall m)(\forall z)(n \in O^\vee \land (H(n, z, y) \rightarrow x = \Phi^z_e))\)，其中 \(H\) 如定理 2.1.4 所示。因此集合 \(\{(x, y) \mid x \in \text{HYP}^y\}\) 是 \(\Pi^1_1\)。

对每个 \(n \in O^\vee\)，定义 \(O^\vee_n = \{m \mid m \in O^\vee \land |m| < |n|\}\)。

**引理 2.2.3.** 以下谓词是 \(\Pi^1_1\)：(i) \(n \in O^\vee \land m \in O^\vee_n\)。 (ii) \(n \in O^\vee \land m \notin O^\vee_n\)。





证明。由定理 1.3.4，定义一个 \(\Sigma^1_1\)-谓词 \(P(x, y)\) 为以下三个句子的合取：

\(x^{[1]} = 0,\)

\((\forall e)(3 \cdot 5^e \in O^y \to x^{[3 \cdot 5^e]} = \bigcup_x x^{[\Phi_e^x(0)]}),\)

和

\((\forall n)(2^n \in O^y \to x^{[2^n]} = \{1\} \cup \{k \mid (\exists j)(k = 2^j \wedge j \in x^{[1]})\} \cup \{k \mid (\exists e)(k = 3 \cdot 5^e \land (\forall j)(\Phi_e^x(j) <_O \Phi_e^x(j+1) \in x^{[1]}))\}).\)

定义一个 \(\Pi^1_1\)-集 \(A = \{(m, n, y) \mid (\forall z)(P(z, y) \to \langle m, n, z \rangle \in z)\}\)。不难看出

\(n \in O^y \land m \in O^y_n \Leftrightarrow \langle m, n, y \rangle \in A.\)

(ii) 的论证类似，留作练习。

### 引理 2.2.4. 存在一个递归函数 g，使得对所有 \(n \in O^y\)，\(O^y_n = \Phi^{H^y_{g(n)}}_{g(n)}\)。

证明。我们证明非相对化版本。由递归定理，我们可以假设对于所有 m <_O n，\(O_m = \Phi^{H_m}_{g(m)}\)。

如果 n = 2^m，定义

\(E = \{e \mid (\forall n)(\Phi_e(n) \downarrow \land \Phi_e(n) \in W_{f(\Phi_e(n+1))})\}\)

其中 f 是定理 1.3.4 中 (i) 的函数。注意 \(E \le_T O^y\)。如果 m \(\neq\) 1 且 m \(\in\) O，则

\(k \in O_{2^m} \Leftrightarrow k = 1 \lor (\exists j)(k = 2^j \wedge j \in O_m) \lor (\exists e)(k = 3 \cdot 5^e \land e \in E \land (\forall j)(\Phi_e(j) \in O_m)).\)

因此 \(O_{2^m}\) 可以通过 \(H_{2^m}\) 由一个 oracle 图灵机计算，其索引可以从 g(m) 有效地得到。将索引设为 g(n)。则 \(O_n = \Phi^{H_{g(n)}}_{g(n)}\)。

如果 n = 3 \(\cdot\) 5^e，则

\(i \in O_n \Leftrightarrow (\exists k)(i \in O_{\Phi_e(k)}) \Leftrightarrow (\exists k)(i \in \Phi^{H_{g(\Phi_e(k))}}_{\Phi_e(k)}).\)

由引理 2.1.2，\(H_{2^e \oplus 0}\) 可以由 \(H_n\)，进而由 \(H_{2^e}\) 一致地计算。因此 \(O_n\) 在 \(H_n\) 上是 \(\Sigma^1_1\)，故在 \(H_{2^e}\) 中是递归的。而且，从 \(H_{2^e}\) 的计算是一致的。因此从 \(H_{2^e}\) 计算 \(O_n\) 的 oracle 图灵机的索引 i 可以有效地得到。设 g(n) = i。则 \(O_n = \Phi^{H_{g(n)}}_{g(n)}\)。

### 推论 2.2.5. 如果 x 是 \(\Delta^1_1(y)\)，则 x 在 y 中是超算术的。

证明。如果 x 是 \(\Delta^1_1(y)\)，则存在递归函数 f 使得 \(n \in x \leftrightarrow f(n) \in O^y\)。集合 \(A = \{f(n) \mid n \in x\}\) 是 \(\Delta^1_1(y)\)。由 Specter 的有界性定理 (1.5.5)，存在一个数 \(m \in O^y\) 使得 \(A \subseteq O^y_m\)。则 \(n \in x \leftrightarrow f(n) \in O^y_m\)。故由引理 2.2.4，\(x \le_T H^y_{2^m}\)。

作为结果，我们有以下由 Kleene 提出的刻画。

### 定理 2.2.6 (Kleene [69]). 一个实数 $x$ 是 $\Delta_1^1(y)$ 当且仅当它在 y 中是超算术的。

以下推论表明 \(\Delta_1^1\)-集强可归约到 H-集。

### 推论 2.2.7. 每个 \(\Delta_1^1\)-实数多一可归约到一个 H-集。

**证明。** 由定理 2.2.6，如果 x 是 \(\Delta_1^1\)，则它对某些 \(n \in \mathcal{O}\) 图灵可归约到 \(H_n\)。则 x 多一可归约到 \(H_{2^n} = (H_n)'\)。

### 2.2.2 \(\Delta_1^1\)-实数集

在定义实数的超算术集概念时，关于一致性存在一个微妙之处。为此，我们通过对 \(\mathcal{O}\) 而非 \(\mathcal{O}^x\) 进行归纳来定义 \(\tilde{H}^x\)-集：

$$\tilde{H}_1^x = x,$$

$$\tilde{H}_{2^x}^x = (\tilde{H}^x)'$$

和

$$\tilde{H}_{3 \cdot 5^e}^x = \langle \langle m, i \rangle \mid m \in \tilde{H}_{\phi_e(i)}^x \rangle.$$

#### 定义 2.2.8. 一个实数集 A 是 *超算术的* 如果存在一个数 \(n \in \mathcal{O}\) 和一个索引 e，使得对所有 x，\(x \in A \Leftrightarrow \phi_e^{\tilde{H}_n^x}(0) \downarrow\)。

因此，如果 A 是超算术的，则存在 n 和 e 使得

$$x \in A \Leftrightarrow (\exists \sigma)(\sigma < \tilde{H}_n^x \land \phi_e^\sigma(0) \downarrow)$$

和

$$x \notin A \Leftrightarrow (\forall \sigma)(\sigma < \tilde{H}_n^x \rightarrow \phi_e^\sigma(0) \uparrow).$$

由此可见，引理 2.2.1 对于这样的 \(\tilde{H}^x\)-集依然成立，因此 A 是 \(\Delta_1^1\)。

反之，假设 A 是 \(\Delta_1^1\)。根据 §1.5.1 的讨论，存在两个数 \(k_0\) 和 \(k_1\) 使得 \(x \in A \Rightarrow k_0 \in \mathcal{O}^x \Rightarrow k_1 \in \mathcal{O}^x\)。通过相对化推论 1.5.4，存在一个递归函数 p 使得对所有 x，\(\min\{|k_0|_x, |k_1|_x\} \le |p(k_0, k_1)|_x\)。令 \(n = 2^{p(k_0, k_1)}\)。注意对于所有 x，\(n \in \mathcal{O}^x\)，因此 \(0 \in \mathcal{O}^x = 0\)。由于引理 2.2.4 依然成立，对于所有 x，\(\mathcal{O}_n^x = \tilde{H}_{\phi(n)}^x\)。因此存在一个递归函数 h 使得对所有 x，\(k_0 \in \mathcal{O}_n^x \Leftrightarrow 0 \in W_{\tilde{H}_{\phi(n)}^x}\)，从而 \(x \in A \Leftrightarrow \phi_{h(n)}^{\tilde{H}_n^x}(0) \downarrow\)。于是我们得到以下结论。

#### 定理 2.2.9. 一个实数集是超算术的当且仅当它是 \(\Delta_1^1\)。

超算术性还为 \(\Delta_1^1\)-实数集的归纳分析提供了一个方案。我们将在引入 §3.8 的分层解析层次后展示如何实现这一点。将在 §2.7 引入的超算术码概念，也将为研究 \(\Delta^1_1\)-实数集提供一个强大工具。下一个命题对 \(|n|_x\) 设定了一个有效界，前提是对所有 x，\(n \in O^x\)。

#### 命题 2.2.10. 如果对所有 x，\(n \in O^x\)，则存在一个递归序数 \(\beta\) 使得对所有 x，\(|n|_x < \beta\)。

证明。如果不成立，\(m \in \text{WF}_0 \Leftrightarrow (\exists j)(\exists x)(\forall i)(\forall j)R_m(i, j) \rightarrow \langle f(i), f(j) \rangle \in W^{g(x)}_m)\)，其中 g 是定理 1.3.4 中 (ii) 的递归函数。所以 \(\text{WF}_0\) 是 \(\Sigma^1_1\)，产生矛盾。

从上述讨论还可得出，\(\omega^x_1 = \omega^{CK}_1\) 当且仅当每个 \(y \le_h x\) 都在某些 \(n \in O\) 的 \(H^x_n\) 中是递归的。

### 2.2.3 \(\Delta_1^1\)-集的参数化

作为上述结果的首个应用，我们展示 \(\Delta_1^1\)-实数的参数化。

#### 命题 2.2.11. 存在一个偏函数 \(D : \omega \times \omega \rightarrow \omega\)，带有一个 \(\Pi^1_1\)-图 \(G^D\)，使得对所有 x，\(x \in \Delta^1_1 \Leftrightarrow (\exists m)(\forall i)(\forall j)(x(i) = j \leftrightarrow (m, i, j) \in D)\)。

证明。定义 \(D = \{\langle n, e, i, j \rangle | n \in O \wedge \Phi^{H}_e \text{ 是全定义的} \wedge \Phi^{H}_e(i) = j\}\)。由定理 2.2.6，对所有 x，\(x \in \Delta^1_1 \Leftrightarrow (\exists m)(\forall i)(\forall j)(x(i) = j \leftrightarrow (m, i, j) \in D)\)。而且，\(\langle n, e, i, j \rangle \in D \Rightarrow n \in O \wedge (\forall z)(H(n, z) \wedge \Phi^z_e \text{ 是全定义的} \rightarrow \Phi^z_e(i) = j)\)，其中 H 如 § 2.1.2 中定义。因此 \(G^D\) 是 \(\Pi^1_1\)。

命题 2.2.11 可用于将某些 \(\Sigma^1_2\)-谓词归约到 \(\Pi^1_1\)。

#### 推论 2.2.12. 对于任何 \(\Pi^1_1\)-谓词 P(x, y)，谓词 Q(y) \(\Leftrightarrow (\exists x \in \Delta^1_1)P(x, y)\) 是 \(\Pi^1_1\)。

证明。由命题 2.2.11，Q(y) \(\Leftrightarrow (\exists x \in \Delta^1_1)P(x, y)\) 等价于

\((\exists m)(\forall i)[\exists j((m, i, j) \in D) \land (\forall x)(\forall i)(\forall j)(x(i) = j \leftrightarrow (m, i, j) \in D) \rightarrow P(x, y)].\)

注意对于每个 m，如果 \((\forall i)(\exists j)((m, i, j) \in D)\)，则谓词 \((m, i, j) \in D\) 是 \(\Delta^1_1\)。因此 Q 是 \(\Pi^1_1\)。

可以将上述命题相对化为陈述“对于任何 \(\Pi^1_1\)-谓词 P(x, y)，谓词 Q(y) \(\Leftrightarrow (\exists x \in \Delta^1_1(y))P(x, y)\) 是 \(\Pi^1_1\)”，这用于推导描述性集合论中的一个经典结果：

#### 推论 2.2.13. 如果函数 \(f : \omega^\omega \rightarrow \omega^\omega\) 是 \(\Delta^1_1\) 且单射，则对于任何 \(\Delta^1_1\)-集 A，f(A) 是 \(\Delta^1_1\)。

证明。如果 f 是 \(\Delta^1_1\) 且全定义的，由命题 1.1.8，\(G^f\) 是 \(\Delta^1_1\)。因此对于任何 y，\(f^{-1}(\{y\})\) 是 \(\Delta^1_1(y)\)。由于 f 是单射，由命题 1.1.15，唯一实数 \(f^{-1}(y)\) 是 \(\Delta^1_1(y)\)。所以 y \(\in\)



$f(A) \Leftrightarrow (\exists x \in \Delta_1^1(y))(y \in A \wedge (x, y) \in G') \Leftrightarrow (\exists x)(x \in A \wedge (x, y) \in G')$. 通过将推论 2.2.12 相对化到 $y$，可以得出 $f(A)$ 是 $\Delta_1^1$。

因此我们得到关于 $\Delta_1^1$-实数集的刻画：

#### 推论 2.2.14. 实数集 $A$ 是 $\Delta_1^1$ 当且仅当存在一个 $\Pi_1^0$-集 $B$ 和一个递归函数 $f : \omega^\omega \to \omega^\omega$，使得 $f(B) = A$ 且 $f$ 在 $B$ 上是一一的。

证明. 若存在一个 $\Pi_1^0$-集 $B$ 和一个一一递归函数 $f : \omega^\omega \to \omega^\omega$ 使得 $f(B) = A$，则根据推论 2.2.13，易知 $A$ 是 $\Delta_1^1$。若 $A = \omega^\omega$ 是 $\Delta_1^1$，则存在递归函数 $g$ 使得 $x \in A \Leftrightarrow g(x) \in \text{WO}_1$，且根据 §1.5.2 的讨论，存在递归良序 $z$ 使得 $x \in A \Leftrightarrow |g(x)| \le |z|$。定义 $P(x, y)$ 当且仅当 $y$ 是从 $\le_{g(x)}$ 到 $\le_z$ 的一个初始段的同构。由于 $z$ 是递归的，$P(x, y)$ 是 $\Pi_1^0$ 且 $x \in A \Leftrightarrow (\exists y)P(x, y)$。故存在递归谓词 $R$ 使得 $P(x, y) \Leftrightarrow (\forall n)(\exists m)R(x, y, n, m)$。通过定义 $\Pi_1^0$-集 $B = \{x_0 \oplus x_1 \oplus x_2 \mid (\forall n)(R(x_1, x_2, n, x_0(n)) \wedge (\forall m < x_0(n))(\neg R(x_1, x_2, n, m)))\}$ 对 $P$ 进行一致化。定义递归函数 $f$，使得若 $x = x_0 \oplus x_1 \oplus x_2$ 则 $f(x) = x_1$。显然 $f$ 在 $B$ 上是一一的。

在某些情况下，推论 2.2.14 使得可以将关于 $\Delta_1^1$-集上的构造归约为关于 $\Pi_1^0$-集上的构造。此外，定理 2.2.9 提供了 $\Delta_1^1$-实数集的参数化。

#### 命题 2.2.15. 存在一个 $\Pi_1^1$-集 $A \subseteq \omega \times \omega^\omega$，具有如下性质：对于任何实数集 $B$，$B$ 是 $\Delta_1^1$ 当且仅当存在一个 $n$ 使得 $B = A_n = \{x \mid (n, x) \in A\}$。

证明. 定义 $A = \{(\langle e, m \rangle, x) \mid m \in \omega \wedge \Phi_e^{B_n(0)} \downarrow \}$。根据定理 2.2.9，$A$ 即为所需。

### 2.2.4 练习

#### 练习 2.2.1. 完成引理 2.2.3 的证明。

#### 练习 2.2.2. 证明对于任何 $n \in \Theta$，存在一个不可数的 $\Pi_1^0$-集 $P \subseteq 2^\omega$，其中每个在 $H_n$ 中递归的实数都是递归的。

#### 练习 2.2.3. 证明存在一个 $B \subseteq \Theta$ 使得 $<_\Theta$ 在 $B$ 上是一个序数类型为 $\omega_1^{CK}$ 的良序。

### 2.3 Spector 唯一性定理

由于 $H$-集是由一个 $\Pi_2^0$-单点过程生成的（参见定理 2.1.4），它们提供了一种在超算术集上进行超限归纳的方法。我们通过指出推论 2.3.2，即 Spector 唯一性定理，来使这一观察精确化，该定理表明在 H-集上的归纳是度理论不变的。

#### 定理 2.3.1 (Spector [153]). 存在一个递归函数 h 使得
$n, m \in O \land |n| \le |m| \implies H_n = \Phi_{h(n,m)}^{H_m}$.

证明. 我们通过对良序 $<_O^2$ 进行归纳来证明这一点：
$(n_1, m_1) < (n_2, m_2) \Rightarrow |n_1| < |n_2| \lor (|n_1| = |n_2| \land |m_1| < |m_2|)$.

需要考虑四种情况。

- (1) $n = 1$. 令 $h(1, m) = c_1$ 使得对所有 $x$ 都有 $\Phi_{c_1}^x = H_1 = \emptyset$.
- (2) $n = 2^{|x|} \land n = 2^i$. 修正一个递归函数 $g$ 使得对于任何 $e, x$ 和 $y$，$x = \Phi_e^y$ 蕴含 $x' = \Phi^{g(e)}$。令 $h(n, m) = g(h(i, j))$.
- (3) $n = 3 \cdot 5^k$. 令 $h(n, m) = c_3$ 使得 $\Phi_{c_3}^{H_m}$ 是集合 $\{(i, j) \mid i \in H_m^{(h(\phi(i),0),m)}\}$ 的特征函数。
- (4) $n = 2^a \land m = 3 \cdot 5^i$. 这是最困难的情况。根据引理 2.2.4，我们可以 $H_m$-递归地搜索一个 $i$ 使得 $n \in O_{\phi(i,0)}$ 且 $O_{\phi(i,0)} = \Phi_{g(h(\phi(i),0))}^{H_m}$。根据引理 2.1.2，存在递归函数 $f$ 使得 $H_{2^{\phi(i,0)}} = \Phi_{f(2^{\phi(i,0)},m)}^{H_m}$。通过归纳，$H_n = \Phi_{h(n, 2^{\phi(i,0)})}^{H_m}$。然后存在一个 $c_4$ 使得 $H_n = \Phi_{h(n, 2^{\phi(i,0)})}^{H_m} = \Phi_{c_4}^{H_m}$。令 $h(n, m) = c_4$.

注意这些情况可以递归地识别。因此 h 是一个递归函数。

因此我们有以下唯一性定理。

#### 推论 2.3.2 (Spector). 如果 $n, m \in O$，那么 $|n| = |m|$ 蕴含 $H_n \equiv_T H_m$.

特别是，对于任何递归序数 $\beta$，“$\beta$-次图灵跳跃”，记作 $\emptyset^{(\beta)}$，可以取为任何满足 $|n| = \beta$ 的 $n \in O$ 的 $H_n$。对于 $\tilde{H}^r$-集存在一个平行结果，其证明与定理 2.3.1 的证明完全相同。我们将其留给读者作为练习。

#### 定理 2.3.3. 存在一个递归函数 h 使得对于任何实数 x，
$n \in O^x \land m \in O \land |n| \le |m| \implies H_n^x = \Phi_{h(n,m)}^{H_m}$.

#### 2.3.1 练习

#### 练习 2.3.1. 证明定理 2.3.3。

### 2.4 超算术可归约性

#### 2.4.1 \( A_1^1 \)-可归约性

定义 2.4.1. \( x \le_{A_1^1} y \) 当且仅当 \( x \) 是 \( \Delta_1^1(y) \)。特别是，如果 $x \le_{A_1^1} y$，则 $x \le_h y$。

命题 2.4.2 (Shoenfield). 如果 \( x \le_{A_1^1} y \) 且 \( y \le_{A_1^1} z \)，那么 \( x \le_{A_1^1} z \)。

证明. 若 $x \le_{A_1^1} y$，则存在 $A_1^1$-谓词 $R$ 使得 $n \in x \Leftrightarrow R(n, y)$。
若 $y \le_{A_1^1} z$，则存在 $A_1^1$-谓词 $S$ 使得 $n \in y \Leftrightarrow S(n, z)$。
则
$n \in x \Leftrightarrow (\exists r)(R(n, r) \land (\forall m)(m \in r \leftrightarrow S(m, z)))$
$\leftrightarrow (\forall r)(\forall m)((m \in r \leftrightarrow S(m, z)) \rightarrow R(n, r))$。
故 $x \le_{A_1^1} z$。

如果 $x \le_{A_1^1} y$ 且 $y \le_{A_1^1} x$，则称实数 $x, y$ 具有相同的 $A_n^1$-度。若 $n = 1$，则我们还说它们具有相同的超度。根据定理 2.2.6，$x \le_h y$ 当且仅当存在 $n \in O^y$ 和 $e$ 使得 $x = \Phi_e^{y_n}$。$x$ 的超跳跃定义为集合 $O^x$。

$h$-归约关系 $x \le_h y$ 提出了引入 $\dot{H}^x$-集的另一个原因。$h$-可归约性的一个问题是，与图灵可归约性的情况不同（在图灵可归约性中，人们考察一个固定的递归可能归约算法列表，与所考虑的集合 $x$ 和 $y$ 无关），没有统一的程序来搜索将 $x$ $h$-归约到 $y$ 的算法。归约取决于 $H^x$-集可以图灵计算的内容，这涉及 $y$ 的序数记法。不同的实数 $y$ 有不同的序数记法。在某些情况下，记法可能显著不同，因为 $\{ \omega_1^y \mid y \in 2^\omega \}$ 在 $\omega_1$ 中无界。使用 $\dot{H}^x$-集绕过了这一困难。若 $\omega_1^y = \omega_1^{y, \text{CK}}$，则由 $\dot{H}^x$-集图灵可计算的集合正是 $A_1^1(y)$-集。因此，虽然这在一般情况下不成立，但对于满足 $\omega_1^y = \omega_1^{y, \text{CK}}$ 的实数 $y$，确实存在一个统一的归约。

#### 2.4.2 超度的偏序

图灵跳跃算子在图灵度上是序保持的。这一性质对于超跳跃算子也成立，它在超度上保持序。

命题 2.4.3. \( x \le_h y \iff O^x \le_m O^y \).

证明. 首先，$O^x$ 是 $\Pi_1^1(x)$。若 $x \le_h y$，则如命题 2.4.2 证明所示，$O^x$ 是 $\Pi_1^1(y)$。根据定理 1.5.1，$O^x \le_m O^y$。
若 $O^x \le_m O^y$，则 $x \le_m O^y$ 且 $\omega \setminus x \le_m O^y$。由于 $\omega \setminus x$ 是 $\Pi_1^1(x)$，$\omega \setminus x \le_m O^x$。则 $\omega \setminus x$ 是 $\Pi_1^1(y)$，这蕴含 $x \le_h y$。





经典递归论中最基本的定理之一是 Friedberg-Mučnik 定理（[28] 和 [109]），它断言存在两个不可比拟的 r.e. 图灵度。由于 $\Pi^1_1$-集被视为更高设置中 r.e. 集的类比，以下结果表明两种可归约性概念之间存在根本差异。

**定理 2.4.4 (Spector [153]).** 如果 $x, y \in \Pi^1_1$ 且 $y \notin \text{HYP}$，则 $x \le_h y$。

证明。我们证明 $\mathcal{O} \le_h y$。根据定理 1.5.1，存在一个递归函数 $f$，使得 $n \in \mathcal{O} \Leftrightarrow f(n) \in \mathcal{O}$。由于 $y \notin \text{HYP}$，根据引理 2.2.4，$\sup\{|f(n)|_y : n \in y\}$ 是 $\omega_1^{CK}$。然后
$n \in \mathcal{O} \Leftrightarrow (\exists m)(m \in y \land n \in \mathcal{O}_{f(m)})$
和
$n \notin \mathcal{O} \Leftrightarrow (\forall m)(m \in y \rightarrow n \notin \mathcal{O}_{f(m)})$。
根据引理 2.2.3，$\mathcal{O} \le_h y$。

**注 2.4.5.** 定理 2.4.4 促使 Kreisel 提出，$h$-归约不是更高递归论中“正确”的归约性概念。这导致在元递归论中引入了元递归归约性的概念。Sacks [118] 表明，存在两个不可比拟的元度的 $\Pi^1_1$-集。

$\omega_1^x$ 与 $x$ 的 $h$-度之间存在紧密联系，如下面的命题所示：

**命题 2.4.6 (Spector [153]).** $x \le_h y \implies \omega_1^x \le \omega_1^y$。

证明。由于 $x \le_h y$，每个 $x$-递归的良序关系 $R \le \omega^2$ 在 $y$ 中都是 $\Delta^1_1$。通过将命题 1.5.6 相对化到 $y$，$R$ 的序类型小于 $\omega_1^y$。因此 $\omega_1^x \le \omega_1^y$。

命题 2.4.6 的逆命题一般不成立。然而，有一个重要的部分结果刻画了 $\omega_1^{CK}$。

**定理 2.4.7 (Sacks).** $\omega_1^x > \omega_1^{CK}$ 当且仅当 $x \ge_h \mathcal{O}$。

我们将证明分解为两个引理，其中以下内容留作练习：

**引理 2.4.8 (Sacks).** 假设 $x \le_T y$。那么存在一个递归函数 $f$，使得 (i) $(\forall n)(\forall m)(n <_O m \rightarrow f(n) < f(m))$，(ii) $(\forall n)(n \in \mathcal{O}^x \rightarrow |n|_x = |f(n)|_y)$。

**引理 2.4.9 (Spector [153]).** (i) $\mathcal{O}^x \le_h y \implies \omega_1^x < \omega_1^y$。(ii) $\omega_1^x < \omega_1^y \land x \le_h y \implies \mathcal{O}^x \le_h y$。

证明。(i) $<_O$ 是 $\Pi^1_1(x)$，因此在 $\mathcal{O}^x$ 中是递归的。因此，根据命题 2.4.6，$\omega_1^x < \omega_1^{\mathcal{O}^x} \le \omega_1^y$。

(ii) 如果 $x \le_h y$，那么对于某些 $e \in \mathcal{O}^y$，有 $x \le_T H_e^y$。令 $f$ 如引理 2.4.8 所示。由于 $\omega_1^x < \omega_1^y$，根据命题 2.4.6，$\omega_1^x < \omega_1^{H_e^y}$。因此存在一个数 $m \in \mathcal{O}^{H_e^y}$，使得对于所有 $i$，$i \in \mathcal{O}^x \leftrightarrow i \in \mathcal{O}_m^{H_e^y}$。因此 $x \le_h H_e^y \le_h y$。

定理 2.4.7 的证明。如果 $\omega_1^x > \omega_1^{CK}$，那么根据引理 2.4.9 的 (ii)，$\mathcal{O} \le_h x$。如果 $\mathcal{O} \le_h x$，那么根据引理 2.4.9 的 (i)，$\omega_1^x > \omega_1^{CK}$。

**推论 2.4.10.** \( x \not\le_h \emptyset \leftrightarrow \mathcal{O}^x \le_h x \not\le_h \emptyset \)。

证明。如果 $\mathcal{O}^x \not\le_h x \not\le_h \emptyset$，那么 $x <_h \emptyset' \not\le_h x \not\le_h \emptyset$。反之，如果 $x \not\le_h \emptyset$，那么根据定理 2.4.7，$\omega_1^x = \omega_1^{CK} < \omega_1^{\mathcal{O}^x}$。根据引理 2.4.9 的 (i)，$\mathcal{O}^x \le_h x \not\le_h \emptyset$。

**推论 2.4.11.** 集合 \(\{x \mid \omega_1^x = \omega_1^{CK}\}\) 是 \(\Sigma_1^1\)。

证明。根据命题 1.2.5，$\mathcal{O}$ 是一个 $\Pi_1^1$-单点。那么 $x \ge_h \mathcal{O}$ 当且仅当 $(\exists n \in \mathcal{O}^x)(\exists e)(\Theta_e^{H_e^x} \in \{\mathcal{O}\})$，这是一个 $\Pi_1^1$-陈述。根据定理 2.4.7，集合 \(\{x \mid \omega_1^x = \omega_1^{CK}\}\) 是 \(\Sigma_1^1\)。

#### 2.4.3 练习

**练习 2.4.1.** _证明引理 2.4.8。_

**练习 2.4.2.** _证明集合_ \(\{x \mid \omega_1^x = \omega_1^{CK}\}\) _是_ \(\Delta_1^1(\emptyset)\)_。*

### 2.5 一些基数定理及其应用

#### 2.5.1 Gandy 基数定理

实数集 \( A \) 是实数集合集合 \(\mathbf{P}\) 的一个 *基数*，如果对于任何非空的 \( P \in \mathbf{P} \)，\( P \cap A \neq \emptyset \)。基数定理在递归论中非常重要。它们用于与其他事物对抗以确定谓词的复杂性。例如，设 \(\{T_i\}_{i \in \omega}\) 是 \( 2^{<\omega} \) 中递归树的有效枚举。索引集 \( N = \{i \mid T_i \text{ 包含一条无限路径}\} \) 看起来是 \(\Sigma_1^1\)。但可以证明，\( 2^{<\omega} \) 中包含无限路径的每个递归树必须包含一个在 \( \emptyset' \) 中递归的无限路径（参见练习 1.5.3）。因此 \( N \) 是一个算术集。

**引理 2.5.1.** 假设 \( T \subseteq \omega^{<\omega} \) 是一棵带有无限路径的递归树。那么存在一条在 \( \emptyset \) 中递归的无限路径 \( x \in [T] \)。

证明。假设 \( T \subseteq \omega^{<\omega} \) 是一棵带有无限路径的递归树。注意集合 \( S = \{ \sigma \in T \mid (\exists y > \sigma)(\forall n)(y \mid n \in T) \} \subseteq T \) 是一个非空的 \(\Sigma^1_1\) 树，没有死端，因此在 \( \emptyset \) 中是递归的。由于 \( T \) 有一条无限路径，\( S \) 也有。因此，\( S \) 中最左边的无限路径 \( x \) 在 \( \emptyset \) 中是递归的。

因此，在 \( \emptyset \) 中递归的实数集合是 \(\omega^{<\omega}\) 中递归树的一个基数，而高算术实数集合则不是：

**命题 2.5.2.** 存在一棵递归树 \( S \subseteq \omega^{<\omega} \)，它有不可数多条无限路径，但没有高算术无限路径。

证明。根据推论 2.2.2，非高算术实数集 \( A \) 是 \(\Sigma^1_1\)。那么存在一棵递归树 \( T \subseteq 2^{<\omega} \times \omega^{<\omega} \)，使得对于任何 \( x \in 2^\omega \)，\( x \in A \) 当且仅当存在一个 \( y \) 满足 \( (\forall n)((x \mid n, y \mid n) \in T) \)。令 \( S \subseteq \omega^{<\omega} \) 为一棵递归树，使得 \( \sigma \in S \) 当且仅当 \( (\sigma_0, \sigma_1) \in T \)，其中对于所有有意义的 \( n \)，\(\sigma_0(n) = \sigma(2n)\) 且 \(\sigma_1(n) = \sigma(2n + 1)\)。那么对于任何无限路径 \( x \in [S] \)，\( x = x_0 \oplus x_1\)，因此 \( x_0 \in A \)。换句话说，\( S \) 中的每条无限路径都图灵计算一个非高算术实数。此外，根据 \( A \) 的定义，每个非高算术实数都在 \( S \) 的某条无限路径中是递归的。因此 \( S \) 包含不可数多条无限路径。

**定理 2.5.3 (Gandy [33]).** 如果 \( A \) 是 \(\Sigma^1_1\) 且非空，那么 \( A \) 包含一个实数 \( x \)，使得 \( \omega_1^x = \omega_1^{CK} \) 且 \( x \le_T \emptyset \)。

证明。根据推论 2.2.2，集合 \( B = \{ x \oplus y \mid y \not\le_h x \wedge x \in A \} \) 也是一个非空的 \(\Sigma^1_1\) 集合。根据引理 2.5.1，存在一个实数 \( x \oplus y \in B \) 且 \( x \oplus y \le_T \emptyset \)。因此 \( x \in A \) 在 \( \emptyset \) 中是递归的。由于 \( y \not\le_h x \)，我们有 \( x \not\ge_h \emptyset \)。根据定理 2.4.7，\( \omega_1^x = \omega_1^{CK} \)。

定理 2.5.3 称为冈迪基数定理。

#### 2.5.2 不可比拟的高度

我们应用冈迪基数定理来构造一对不可比拟的高度。

**引理 2.5.4.** 如果 \( A \) 是一个包含非高算术实数的 \(\Sigma^1_1\)-集，那么 \( A \) 是不可数的。

证明。假设 \( A \) 是一个包含非高算术实数的可数 \(\Sigma^1_1\)-集。那么集合 \( B = \{ x \in A \mid x \not\le_h \emptyset \} \) 是 \( A \) 的一个非空 \(\Sigma^1_1\)-子集。因此存在一棵递归树 \( T \)，使得 \( x \in B \) 当且仅当存在一个 \( y \)，对于每个 \( n \)，\( (x \mid n, y \mid n) \in T \)。令 \( T' = \{ (\sigma, \tau) \mid (\exists x \supset \sigma)(\exists y \supset \tau)(\forall n)((x \mid n, y \mid n) \in T) \} \) 成为 \( T \) 的子树。显然 \( T' \) 是 \(\Sigma^1_1\)-树。此外，对于任何 \( (\sigma, \tau) \in T' \)，存在 \( \sigma_0, \sigma_1 > \sigma \) 和 \( \tau_0, \tau_1 > \tau \)，使得对于 \( i \le 1 \)，\( (\sigma_0, \sigma_1) \in T' \)。否则，\(\Sigma^1_1\)-集 \( \{ x \mid (\exists y)((\forall n)(x \supset \sigma \wedge y \supset \tau, y \in T)) \} \subseteq B \) 包含一个唯一的实数，该实数必须是高算术的，这与 \( B \) 的定义矛盾。因此，模仿定理 11.10 的证明，可以表明 \( B \) 包含一个完美子集。





定理 2.5.5（Spector [155]）。存在实数 $x$ 和 $y$，使得 $x \not\le_h y$ 且 $y \not\le_h x$。事实上，存在一个实数 $x \not\le_h 0$，满足 $\omega_1^x = \omega_1^{CK}$。

证明。令 $A = \{x \mid x \notin \xi_0\}$ 为非空的 $\Sigma^1_1$-集合。根据定理 2.5.3 和推论 2.4.11，集合 $B = \{x \in A \mid \omega_1^x = \omega_1^{CK}\}$ 是非空的 $\Sigma^1_1$-集合。根据引理 2.5.4，$B$ 是不可数的。由于可高算归约到 0 的实数至多有可数个，因此存在实数 $x \in B$ 使得 $x \not\le_h 0$。而且，由于 $\omega_1^x = \omega_1^{CK}$，故 $x \not\le_h 0$。$\square$

应当指出，Spector 对定理 2.5.5 的原始证明与上面给出的证明截然不同。他的证明涉及测度论证法，并且是非构造性的。该思想将在第 14 章（关于更高随机性）中进行探讨。

### 2.5.3 克赖塞尔基定理

**定理 2.5.6** (Kreisel [35])。如果 $x$ 是非高算的，且 $A \subseteq \omega^\omega$ 是非空的 $\Sigma^1_1$-集合，则存在 $y \in A$ 使得 $x \not\le_h y$。

证明。假设 $x$ 是非高算的，且 $A \subseteq \omega^\omega$ 是非空的 $\Sigma^1_1$-集合。根据甘迪基定理 2.5.3，集合 $B = \{z \mid \omega_1^z = \omega_1^{CK} \land z \in A\}$ 是非空的 $\Sigma^1_1$-集合。对于每一对 $(e, n)$（其中 $n \in \omega$），令

$P_{(e,n)} = \{z \mid (\exists i)(\Phi_e^{\tilde{H}_i}(i) \downarrow \lor \Phi_e^{\tilde{H}_i}(i) \downarrow \neq x(i))\}.$

我们声明，对于任何非空的 $\Sigma^1_1$-集合 $C$，都存在非空的 $\Sigma^1_1$-集合 $Q_{(e,n)} \subseteq C \cap P_{(e,n)}$。需考虑三种情况。

- (1) 存在 $z \in C$ 和 $i \in \omega$ 使得 $\Phi_e^{\tilde{H}_i}(i) \uparrow$。则令 $Q_{(e,n)} = \{z \mid (\Phi_e^{\tilde{H}_i}(i) \uparrow \land z \in C)\}$。
- (2) 非情况 (1)，但存在 $z_0, z_1 \in C$ 和 $i \in \omega$ 使得 $\Phi_e^{\tilde{H}_{z_0}}(i) \uparrow \neq \Phi_e^{\tilde{H}_{z_1}}(i)$。则存在 $k \le 1$ 使得 $\Phi_e^{\tilde{H}_k}(i) \neq x(i)$。令 $Q_{(e,n)} = \{z \mid (\Phi_e^{\tilde{H}_z}(i) = \Phi_e^{\tilde{H}_k}(i) \land z \in C)\}$。
- (3) 既非 (1) 也非 (2)。则 $\Sigma^1_1$-集合 $\{u \mid (\exists 2i)(\forall z \in C \land u(i) = \Phi_e^{\tilde{H}_z}(i))\}$ 包含恰好一个实数，该实数必为高算的。令 $Q_{(e,n)} = C$。

根据命题 1.1.12，存在 $y \in B \cap \bigcap_{n < \omega} P_{(e,n)}$。根据 $P_{(e,n)}$ 的定义，$x \neq \Phi_e^{\tilde{H}_y}$。注意 $\omega_1^y = \omega_1^{CK}$。因此，根据定理 2.3.3，我们得出 $x \not\le_h y$。$\square$

定理 2.5.6 表明，高算在某个非高算集合之上的集合锥不包含非空的 $\Sigma^1_1$-子集。特别是，任何非高算集合之上的锥都不是 $\Sigma^1_1$。从模型论角度来看，该定理证明中使用的论证是一类型省略论证。该论证将稍后再次用于构造非标准模型，以通过可构层次 $L$ 刻画高算集合。

### 2.5.4 习题

**习题 2.5.1。** 证明对于任意实数 $z$，集合 $\{(x, 0^x) \mid x \in 2^{\omega}\}$ 不是 $\Sigma_1^1(z)$。

**习题 2.5.2。** 证明存在 $x, y \le_h \mathbf{0}$ 使得 $x \not\le_h y$ 且 $y \not\le_h x$。

**习题 2.5.3。** 证明存在实数序列 $(x_i)_{i < \omega}$ 使得 $x_i <_h x_{i+1} <_h \mathbf{0}$。

**习题 2.5.4** (Slaman [140])。证明不存在 $\Sigma_1^1$-集合 $A \subseteq \omega^\omega$ 使得每个 $\Sigma_1^1$-集合都是 $A$ 的连续单射像。

**习题 2.5.5** (Hjorth [49])。证明每个 $\Sigma_1^1$-集合都是 $\Pi_1^1$-集合 $\{x \in \omega^\omega \mid x \in \omega^\omega\}$ 的连续单射像。

**习题 2.5.6。** 证明任何非空的 $\Sigma_1^1$-集合 $A$ 包含一个元素 $x$，使得 $0^x \le_T \mathbf{0}$。

**习题 2.5.7** (Solovay [152])。给定函数 $f, g: \omega \to \omega$，若对任意 $i < \omega$ 都有 $g(i) \ge f(i)$，则称 $g$ 支配 $f$。证明实数 $x$ 是高算的，当且仅当存在函数 $f \ge_T x$，使得每当 $g$ 支配 $f$ 时都有 $g \ge_T f$。

### 2.6 关于 $\mathbf{O}$ 的更多内容

#### 2.6.1 非标准的 $\mathbf{O}$

我们构造一个与 $\mathbf{O}$ 具有许多共同性质的非标准 $\mathbf{O}$。下面的引理表明，存在一个可枚举集合，其域是 $\mathbf{O}$ 的末端扩展。

**引理 2.6.1。** 存在一个可枚举集合 $x$ 和一个定义在 $x$ 上的可枚举偏序关系 $<_x$，使得

- (i) §1.2.1 中的条件 (i)-(iv) 对 $<_x$ 成立；
- (ii) $\mathbf{O} <_x$；
- (iii) $<_0$ 是 $<_x$ 对 $\mathbf{O}$ 的限制；且
- (iv) 若 $m <_x n$ 且 $n \in \mathbf{O}$，则 $m \in \mathbf{O}$。

证明。我们通过有效跨超归纳构造 $<_x$。定义递归函数 $h$ 如下：

```
\(\Phi_{h(e)}((m, n)) = \left\{ \begin{array}{ll} 1 & m = 1 \wedge n = 2, \ 1 & (\exists k)(\Phi_e((m, k)) = 1 \wedge \Phi_e((k, n)) = 1), \ 1 & (\exists k)(\Phi_e((k, m)) = 1 \wedge n = 2^m), \ 1 & m \neq 1 \wedge n = 3 \cdot 5^d \wedge (\exists k)(\exists j)(\Phi_e((j, m)) = 1 \wedge m = \Phi_d(k)), \ \uparrow & \text{Otherwise.} \end{array} \right.\)
```

根据递归定理，存在常数 \(c\) 使得 \(\Phi_{h(c)} = \Phi_c\)。令 \(g = \Phi_c\) 为偏递归函数。因此

```
\(g((m, n)) = \begin{cases} 1 & m = 1 \wedge n = 2, \\ 1 & (\exists k)(g((m, k)) = 1 \wedge g(k, n) = 1), \\ 1 & (\exists k)(g((k, m)) = 1 \wedge n = 2^m), \\ 1 & m \neq 1 \wedge n = 3 \cdot 5^d \wedge (\exists k)(\exists j)(g((j, m)) = 1 \wedge m = \Phi_d(k)), \\ \uparrow & \text{Otherwise.} \end{cases}\)
```

定义 $m <_x n$ 当且仅当 $g(m, n) = 1$。令 $X = \{m \mid (\exists n)(m <_x n)\}$。可以直接验证，$<_x$ 的域满足 (i)-(iv)。

注意，给定 \(n \in \mathbb{N}\) 时，\(<_x\) 对集合 \(\{m \mid m <_x n\}\) 的限制不一定是线性的。我们引入如下修改。定义 \(z \subseteq x\)，使得 \(i \in z\) 当且仅当 \(i \in x\) 且 \(<_x\) 对 \(\{m \mid m <_x i\}\) 的限制是线性的。那么 \(z\) 是一个算术集。显然，\(<_x\) 对 \(z\) 的限制是一个偏序，\(\emptyset \subset z\)，且条件 (i)-(iv) 对 \(<_x\) 对 \(z\) 的限制成立。

现在，对于任意 \(n \in \mathbb{O}\)，令 \(z_n\) 为高算集合，使得 \(i \in z_n\) 当且仅当 \(i \in \mathbb{O}_{2^{n*}}\)，或存在 \(j \in \mathbb{O}_{2^{n*}}\) 满足 \(j <_l i\) 且 \(i \in z\)。换言之，\(z_n\) 是通过将 \(z\) 中不在 \(\mathbb{O}_{2^{n*}}\) 之上的节点“截断”而得到的。因此，\(z_n\) 将 \(\mathbb{O}_{2^{n*}}\) 作为一个“初始段”。注意，\(<_x\) 对 \(z_n\) 的限制也满足条件 (i)-(iv)。

#### 定义 2.6.2

令 \(\Theta^* = \bigwedge A\)，其中

```
\(A = \{y \mid y \in x \text{ is hyperarithmetic} \wedge \text{Conditions (i)-(iv) in §1.2.1 hold for } <_x \text{ restricted to } y\}.\)
```

记 \(<_{\Theta^*}\) 为 \(<_x\) 对 \(\Theta^*\) 限制得到的序关系。注意，对所有 \(n \in \mathbb{O}\)，都有 \(z_n \in A\)。此外，根据 \(\emptyset\) 的定义，\(\emptyset \subset \Theta^*\)。由于 §1.2.1 中的条件 (i)-(iv) 是算术陈述，根据推论 2.2.2，可知 \(\Theta^*\) 是 \(\Sigma^1_1\)。

#### 2.6.2 穿过 \(\Theta\) 的 \(\Pi^1_1\)-路径

由于 \(\Theta^*\) 是 \(\Sigma^1_1\)，必存在 \(i \in \Theta^* \setminus \mathbb{O}\)。注意，对每个 \(n \in \mathbb{O}\)，都有 \(i \in z_n \setminus \mathbb{O}_n\)。因此，对每个 \(n \in \mathbb{O}\)，存在 \(i_n \in \mathbb{O}_{2^{n*}} \setminus \mathbb{O}_{2^n}\) 使得 \(i_n <_x i\)，从而 \(i_n <_{\Theta^*} i\)。令 \(\Theta^*_i = \{j \mid j <_{\Theta^*} i \land j \in \mathbb{O}\}\)。则 \(j \in \Theta^*_i\) 当且仅当 \(j \in \Theta \land j <_l i\)。故 \(\Theta^*_i \subseteq \mathbb{O}\) 是一个 \(\Pi^1_1\)-集合。

#### 引理 2.6.3

\(<_{\Theta}\) 对 \(\Theta^*_i\) 的限制是一个序类型为 \(\omega^{CK}_1\) 的良序。

证明。显然，\(<_{\Theta}\) 对 \(\Theta^*_i\) 的限制是一个良序。假设 \(<_{\Theta}\) 对 \(\Theta^*_i\) 的限制的序类型小于 \(\omega^{CK}_1\)。则存在 \(n \in \mathbb{O}\) 使得 \(\Theta^*_i \subseteq \mathbb{O}_n\)。于是，对任意 \(k \in \mathbb{O}_{2^{n*}} \setminus \mathbb{O}_{2^n}\)，都有 \(k <_{\Theta^*} j\)。故 \(j \notin z_n\)，产生矛盾。





因此 \(O_1^s \subseteq O\) 是穿过 \(O\) 的一个 \(\Pi_1^1\)-路径，从而得到以下定理。

#### 定理 2.6.4 (Feferman 和 Spector [26])。存在一个 \(\Pi_1^1\)-集合 \(O_1 \subseteq O\)，使得 \(<_O\) 限制在 \(O_1\) 上是序数类型为 \(\omega_1^{CK}\) 的良序。

定理 2.6.4 的证明本质上是模型论的。一个纯递归论的证明可以在 Sacks [123] 中找到。本节的结果也可以一致地相对化。具体来说，存在一个 \(\Sigma_1^1\)-集合 \(\{ (x, O^{x+*}) \mid x \in 2^\omega \}\)，使得对每个 x，\(O^{x+*}\) 是 \(O^x\) 的一个真终端扩展（一个非标准的 \(O^x\)）。

### 2.6.3 穿过 O 的一条正则路径

尽管 O 上的偏序看似复杂，但穿过它的一个 \(\Pi_1^1\)-路径中，每个真初始段都是递归的。这表明在 \(<_O\) 中存在某些隐藏的正则性。

#### 定理 2.6.5 (Jockusch [56])。存在一个集合 \(O \subseteq O\)，使得

- \(<_O\)（定义 1.2.1）是在 O 上的序数类型为 \(\omega_1^{CK}\) 的良序；
- O 是 \(<_O\)-下向闭的，且
- 对于任何 \(n \in O\)，\(\{ m \mid m <_O n \}\) 是递归的。

证明。首先，注意，根据经典递归论中的填充引理，我们可以假设

```
\((\forall m \in O)(\forall n \in O)(n +_O m > \max\{m, n\}).\)
```

根据 s-m-n 定理，存在一个递归函数 \(g_0\)，使得对每个 m，

```
\(\varphi_{g_0(e, m, 0)} = \varphi_e(\varphi_m(0)) \land (\forall n)(\varphi_{g_0(e, m)(n+1)} = \varphi_{g_0(e, m)}(n) +_O \varphi_e(\varphi_m(n+1)).\)
```

定义递归函数 \(h_0\) 如下：

```
\(\varphi_{h_0(e)}(n) = \left\{ \begin{array}{ll} 1 & n = 1, \\ 2^{\varphi_e(k)} & n = 2^k, \\ 3 \cdot 5^{\varphi_e(k)} & n = 3 \cdot 5^k, \\ \uparrow & \text{Otherwise.} \end{array} \right.\)
```

根据递归定理，存在一个常数 c 使得 \(\varphi_{h_0(c)} = \varphi_c\)。那么 \(\varphi_c\) 在 O 上是全定的。注意 \(\varphi_c(1) = 1\)，\(\varphi_c(2^n) = 2^{\varphi_c(n)}\)，并且如果 \(n = 3 \cdot 5^k\)，则 \(\varphi_c(n) = 3 \cdot 5^w\)，其中 \(\varphi_w(n) = \varphi_c(\varphi_c(n))\) 且 \(\varphi_w(j+1) = \varphi_w(j) +_O \varphi_c(\varphi_c(j+1))\)。\(\varphi_c\) 遵循 § 1.2.1 中 (i)-(iv) 设定的格式，并具有额外性质：对于 \(n = 3 \cdot 5^k\)，\(\varphi_c(n)\) 给出一个从 \(\varphi_c\) 递归定义的递归函数的索引 w。因此，直观上可以将其视为 \(\varphi_c\) 值域上的 O 的一个版本。令 \(i \in O^* \setminus O\)。我们声称集合

```
\(O = \{ m \mid (\exists n \in O)(m <_O \varphi_c(n) \land n <_{O^*} i) \}\)
```

是所要求的。我们首先将其作为练习留给读者，以验证

- (1) \(\Phi_e\) 在 \(<_O\) 的意义下是严格递增的；
- (2) 对于每个 \(j_0\) 和 \(m\)，如果 \(\Phi_\omega(j_0) \le_O n <_O \Phi_\omega(j_0 + 1)\)，则存在一个 \(j_1 \in \Theta\) 使得 \(m = \Phi_e(j_0) \vdash_O j_1\)。

由于 \(n <_O m\) 蕴含 \(\Phi_e(n) <_O \Phi_e(m)\)，\(<_O\) 在 O 上是一个良序。注意，对于任何 \(n \in O\)，\(|n| \le |\Phi_e(n)|\)。因此 \(\Phi_e : \{n \in O \mid n <_O \cdot\} \to O\) 是一个嵌入，故 \(<_O\) 在 O 上是序数类型为 \(\omega_1^{CK}\) 的良序。通过在 i 以下的标准序数记号 \(<_O\) 上进行跨越归纳，很容易看出 O 是 \(<_O\)-下向闭的。

根据定理 1.3.4，存在一个递归函数 \(g_1\)，使得对任何 \(n \in O\)，\(W_{g_1(n)} = \{j \mid j <_O n\}\)。我们声称 \(W_{g_1(n)}\) 在限制于 \(n \in O\) 时是递归集合。然后将随之而来，集合 \(\{(j, k) \mid j <_k n <_O n\}\) 也是递归的。

通过有效的跨越归纳与递归定理的应用，我们将定义一个部分递归函数 \(q\)，使得对 \(n \in O\)，\(W_{q(n)} = \omega \setminus W_{g_1(n)}\)。情形 \(n = 2^k\) 且 \(\Phi_e(n) = 2^{\Phi_e(k)}\) 留给读者作为练习（练习 2.6.1）。假设 \(n = 3 \cdot 5^k\) 且 \(\Phi_e(3 \cdot 5^k) = 3 \cdot 5^w\)，其中 w 如前定义，且 e 给定使得对每个 \(j < \omega\)，\(\Phi_e(\Phi_e(j))\) 有定义。首先注意，对 j 的归纳表明 \(\Phi_\omega(j) \ge j\)。如果对于每个 j，\(W_{\Phi_e(\Phi_e(j))} = \omega \setminus W_{g_1(\Phi_e(j))}\)，则我们声称

\(m \in \bigcup_{j < \omega} W_{g_1(\Phi_e(j))} \iff (\exists j_0 \le m)(m \in W_{g_1(\Phi_e(j_0+1))}).\)

该声明从右向左的证明是直接的。对于另一方向，令 \(j_0\) 使得 \(\Phi_\omega(j_0) \le_O m < \Phi_\omega(j_0 + 1)\)。然后根据 (2)，存在一个 \(j_1 \in \Theta\) 使得 \(\Phi_\omega(j_0) \vdash_O j_1 = m\)。这蕴含 \(j_0 \le \Phi_\omega(j_0) \le m\)。由于 \(m \le_O \Phi_\omega(j_0 + 1)\)，我们已证明了该声明。

因此 \(\bigcup_{j < \omega} W_{g_1(\Phi_e(j))} = \omega \setminus \bigcap_{j < \omega} \Phi_\omega(\Phi_e(j))\) 是递归的。现在这个计算是一致的，因此存在一个递归函数 \(g_2\)，使得如果对于每个 j，\(W_{\Phi_e(\Phi_e(j))} = \omega \setminus W_{g_1(\Phi_e(j))}\)，则 \(W_{g_2(e,w)} = \bigcap_{j < \omega} W_{\Phi_e(\Phi_e(j))}\)。令 \(g_3\) 为一个递归函数，使得 \(W_{g_1(e,w)} = W_e \setminus \{w\}\)。回顾，如果 \(\Phi_e(3 \cdot 5^k) = 3 \cdot 5^w \in O\)，则 \(\Phi_\omega(j + 1) = \Phi_\omega(j) \vdash_O \Phi_e(j + 1)\)。令 \(W_{c_1} = \omega\)。

定义递归函数 \(h_1\) 如下：

\(\Phi_{h_1(e)}(n) = \begin{cases} c_1 & n=1, \\ g_3(\Phi_e(m), m) & n=2^m, \\ g_2(e, w) & n=3 \cdot 5^w, \\ \uparrow & \text{Otherwise.} \end{cases}\)

根据递归定理，存在一个 d 使得 \(\Phi_{h_1(d)} = \Phi_d\)。令 \(q = \Phi_d\)。那么 q 即为所需。

### 2.6.4 练习

#### 练习 2.6.1. 完成定理 2.6.5 中情形 \(n = 2^k\) 且 \(\Phi_e(n) = 2^{\Phi_e(k)}\) 的归纳论证。

#### 练习 2.6.2. 证明对于任何 \(i \in O^* \setminus O\)，\(<_O\) 在集合 \(\{j \mid j \in O^* \land j <_O i\}\) 上不是良序。

#### 练习 2.6.3. 证明定理 2.6.5 中的 (1) 和 (2)。

#### 练习 2.6.4. 证明穿过 O 的路径有 \(2^{\aleph_0}\) 条。

#### 练习 2.6.5. 证明不存在部分递归函数 \(p : \omega^2 \to \omega\) 满足练习 14.1 中的性质 (1)-(3)，其中将 x 替换为 \(O_1\)。

### 2.7 集合的编码

在 § 2.2.3 中，介绍了一种 \(\Delta^1_1\)-集合的编码方法。然而，该方法没有提供跟踪 \(\Delta^1_1\)-集合构造的有效方式。在这里，我们讨论超算术编码方法，它作为对实数的 \(\Delta^1_1\) 集合进行归纳分析的有用工具。

#### 2.7.1 Borel 编码

*在本节中，固定 \(\omega^{<\omega}\) 的一个有效枚举* \(\{\sigma_i\}_{i < \omega}\) *。*

对于每个 \(x \in 2^\omega\)，定义 \((x)_n = \{m \mid 2^n \cdot 3^m \in x\}\)。定义实数集的一个序列 \(\{\Sigma_\beta\}_{\beta < \omega_1}\) 如下：

- \(\beta = 0\)：令 \(\Sigma_0 = \{x \in 2^\omega \mid 0\}\)。

- \(\beta > 0\)：令 \(\Sigma_\beta = \{x \in 2^\omega \mid (\forall n)(\exists \gamma < \beta)((x)_n \in \Sigma_\gamma)\}\)。

令 BC = \(\bigcup_{\beta < \omega_1} \Sigma_\beta\) 为 Borel 编码的集合。对于每个 \(x \in\) BC，定义 \(A_x\) 为：

\(x \in \Sigma_0\)：\(A_x = \bigcup_{i \in x} \{ \sigma_i \}\)。

\(\beta > 0\) 且 \(x \in \Sigma_\beta\)：\(A_x = \bigcup_n (2^\omega \setminus A_{(x)_n})\)。

如果 \(\sigma\) 是空字符串，令 \((y)_\sigma = y\)。对于每个 \(\sigma \in \omega^{<\omega}\)，定义

\((y)_\sigma = (\dots ((y)_{\sigma(1)})_{\sigma(2)}) \dots )_{\sigma(|\sigma|)}\)。

给定一个实数 y，我们定义 \(\omega^{<\omega}\) 上的一棵树 \(T' \le_T y\) 如下：

\(\emptyset \in T'\)；

对于任何 \(\sigma \in T'\)，如果 \((y)_\sigma \in \Sigma_0\)，则 \(\sigma\) 在 \(T'\) 中没有扩展。否则，对于每个 n，\(\sigma^\frown n \in T'\)。





### Lemma 2.7.1. $y \in \text{BC}$ 当且仅当 $T^y$ 是良基树。故 $\text{BC}$ 是 $\Pi^1_1$。而且 $y \in \Sigma^y_\beta$ 当且仅当 $|T^y| \le \beta + 1$。

证明。若 $T^y$ 是良基树，则可对 $\sigma \in T^y$ 关于 $\sigma$ 的秩进行归纳，以证明 $(y)_\sigma$ 属于 BC。

若 $y \in \text{BC}$，则对于 $T^y$ 中的任意 $\tau > \sigma$，存在某个 $y < \beta$ 使得 $(y)_\tau \in \Sigma_y$ 且 $(y)_\sigma \ge \Sigma_y$。故 $T^y$ 是一棵良基树。

由于 $T^y \le_T y$ 一致地，且 $y \in \text{BC}$ 当且仅当 $T^y$ 是良基树，我们得出 $\text{BC}$ 是 $\Pi^1_1$。本引理最后一句的验证留给读者。

### 2.7.2 超算术码

超算术码是属于 $\text{HYP} \cap \text{BC}$ 的实数。令 $\text{BC}(\text{HYP})$ 表示超算术码的集合。根据推论 2.2.2 和引理 2.7.1，$\text{BC}(\text{HYP})$ 是 $\Pi^1_1$。

由于 $T^x \le_T x$，若 $x \in \text{BC}(\text{HYP})$，则根据引理 2.7.1 和上述讨论，$|T^x| < \omega^{ck}_1$。故 $\text{BC}(\text{HYP}) \subseteq \Sigma_{\omega^{ck}_1} = \bigcup_{\beta < \omega^{ck}_1} \Sigma_\beta$。

### Theorem 2.7.2 (Kleene [70]). 下列陈述等价：

- (i) 存在某个 $z \in \text{BC} \cap \Delta^1_1$ 使得 $A = A_z$。
- (ii) 存在某个 $z \in \text{BC}(\text{HYP})$ 使得 $A = A_z$。
- (iii) $A$ 是 $\Delta^1_1$。

证明。显然，(i) $\Rightarrow$ (ii)。对于 (ii) $\Rightarrow$ (iii)，假设存在某个 $z \in \text{BC}(\text{HYP})$ 使得 $A = A_z$。我们定义一个 $\Pi^1_1$-关系 $R_z \le \omega^{<\omega} \times \omega^\omega$ 如下。$R_z$ 将从 $T^z$ 解码 $A_z$，并回溯从 $A_z$ 构造 $T^z$ 的步骤：

- (1) $(\forall \tau \notin T^z)(\forall y) \neg R_z(\tau, y)$;
- (2) $(\forall \tau \in T^z)(\forall y)(\tau \text{ 没有扩展} \to (R_z(\tau, y) \leftrightarrow (\exists m)(y \supset \sigma_n \wedge (z)_\tau(n) = 1)));$
- (3) $(\forall \tau \in T^z)((\exists m)(\tau * m \in T^z) \to (\forall y)(R_z(\tau, y) \leftrightarrow (\exists m) \neg R_z(\tau * m, y))).$

显然 $R_z$ 是唯一且定义良好的。此外，对于任意 $z \in \text{BC}$、$m \in \omega$ 和 $y \in \omega^\omega$，$R_z(\emptyset, m, y)$ 当且仅当 $R_{(z)_m}(\emptyset, y)$。我们提出如下主张。

#### 主张. $R_z(\emptyset, y)$ 当且仅当 $y \in A_z$。

主张的证明。我们通过归纳来证明。首先假设 $z \in \Sigma_0$。此时 $T^z$ 仅包含空串，因此根据 (2)，$R_z(\emptyset, y)$ 当且仅当 $y \in A_z$。假设主张对所有 $\Sigma$-码（其中 $y < \beta$）成立。令 $z \in \Sigma_\beta$。若 $R_z(\emptyset, y)$，则根据 (3) 存在某个 $m$ 使得 $\neg R_{(z)_m}(\emptyset, y)$。由归纳假设，$y \notin A_{(z)_m}$，故 $y \in A_z$。反之，若 $y \in A_z$，则存在某个 $m$ 使得 $y \notin A_{(z)_m}$。此时 $(z)_m \in \Sigma_\gamma$ 对某些 $\gamma < \beta$ 成立。由归纳假设，$\neg R_{(z)_m}(\emptyset, y)$。因此根据 (3)，$R_z(\emptyset, y)$，主张得证。

该主张蕴含 $A_z$ 是 $\Pi^1_1(z)$。通过类似论证，可证 $A_z$ 的补集也是 $\Pi^1_1(z)$。故 $A_z$ 是 $\Delta^1_1(z)$。由于 $z \in \text{HYP}$，$A_z$ 是 $\Delta^1_1$。

我们现在证明 (iii) \(\Rightarrow\) (i)。假设 \(A\) 是 \(\Delta^1_1\)。则 \(A\) 和 \(B = \omega^\omega \setminus A\) 都是 \(\Sigma^1_1$。因此存在两个递归树 \(S\) 和 \(T$，使得

\(x \in A \iff (\exists y)(\forall n)(x \upharpoonright n, y \upharpoonright n) \in S$

以及

\(x \in B \iff (\exists y)(\forall n)(x \upharpoonright n, y \upharpoonright n) \in T$。

定义 \(R = S \otimes T$ 如下：

\((\sigma, \tau, v) \in R \iff (\sigma, \tau) \in S \wedge (\sigma, v) \in T$。

定义 \((\sigma, \tau, v) < (\sigma', \tau', v')$ 当且仅当 \(\sigma > \sigma'\)、\(\tau > \tau'\) 且 \(v > v'$。由于 \(A \cap B = \emptyset$，\(R$ 在 \(<\) 下是一棵良基树。我们构造一个超算术码 \(z$，使得 \(B \subseteq A_z$ 且 \(A_z \cap A = \emptyset$。于是 \(A_z = B$。

我们定义一个递归函数 \(h : \omega \to \omega$，使得对于某个 \(c\)，\(\Phi_{h(e)}(n, \emptyset, \emptyset, 0)$ 是 \(A$ 的一个超算术码。

对于满足 \(|\sigma| = |\tau| = |v|$ 的 \((\sigma, \tau, v)$，需考虑三种情况：

- (1) \((\sigma, \tau, v) \notin R$ 且 \((\sigma, v) \in T$。定义 \(\Phi_{h(e)}(0, \sigma, \tau, v) = 0$ 且对于所有 \(n > 0$ 的 \(\Phi_{h(e)}(n, \sigma, \tau, v) = 1$。
- (2) \((\sigma, \tau, v) \notin R$ 且 \((\sigma, v) \notin T$。定义对于所有 \(n$ 的 \(\Phi_{h(e)}(n, \sigma, \tau, v) = 0$。
- (3) \((\sigma, \tau, v) \in R$。对于 \((i, j, k, l)$，我们定义一个由以下四种子情况确定的递归函数 \(g$：

  - 3(i) \(i = k$ 且 \((\sigma' \uparrow i, \tau' \uparrow j, v' \uparrow l) \in R$。定义 \(g(e, i, j, k, l, n) = \Phi_e(n, \sigma' \uparrow i, \tau' \uparrow j, v' \uparrow l)$。
  - 3(ii) \(i \neq k$。定义对于所有 \(n > 0$ 的 \(g(e, i, j, k, l, n) = m$ 且 \(g(e, i, j, k, l, 0) = 0$，其中 \(m$ 是满足 \(0_m = 0^k$ 的码。
  - 3(iii) \(i = k$ 且 \((\sigma' \uparrow i, \tau' \uparrow j) \notin S$。定义对于所有 \(n > 0$ 的 \(g(e, i, j, k, l, n) = 1$ 且 \(g(e, i, j, k, l, 0) = 0$。
  - 3(iv) \(i = k$ 且 \((\sigma' \uparrow i, \tau' \uparrow j) \in S$ 但 \((\sigma' \uparrow i, v' \uparrow l) \notin T$。定义对于所有 \(n$ 的 \(g(e, i, j, k, l, n) = 0$。

直观地，\(g$ 是集合 \(A_{i,j,k,l}$ 的一个超算术码，该集合与 \([S_{(\sigma \uparrow i, \tau \uparrow j)}]$ 不相交但覆盖 \([T_{(\sigma \uparrow i, v \uparrow l)}]$，其中

\([S_{(\sigma \uparrow i, \tau \uparrow j)}] = \{x \supset \sigma \uparrow i \mid (\exists y)(y \supset \tau \uparrow j \wedge (\forall n)((x \upharpoonright n, y \upharpoonright n) \in S)\}$

和

\([T_{(\sigma \uparrow k, v \uparrow l)}] = \{x \supset \sigma \uparrow k \mid (\exists y)(y \supset v \uparrow l \wedge (\forall n)((x \upharpoonright n, y \upharpoonright n) \in T)\}$。

计划是定义 \(\Phi_{h(e)}(n, \sigma, \tau, v)$ 来编码集合 \(C = \bigcup_{k,l} [\bigcup_{i,j} A_{i,j,k,l}]$。于是 \(C \supseteq [T_{(\sigma, v)}]$ 且 \(C \cap [S_{(\sigma, \tau)}] = \emptyset$。定义一个递归函数 \(p^1_k$，使得 \(p^1_k(0) = 1$ 且 \(p^1_k((2^{i,j} \cdot 3^n) \cdot 3^m) = 1$ 当且仅当 \(g(e, i, j, k, l, n) = 1$。于是 \(p^1_k$ 将编码集合 \(\bigcup_{i,j} (\omega^2 \setminus A_{i,j,k,l})$。

定义一个递归函数 \(p^2$，使得 \(p^2(0) = 1$ 且 \(p^2((2^{k,l} \cdot 3^n) \cdot 3^m) = 1$ 当且仅当 \(p^1_k(n) = 1$。于是 \(p^2$ 是 \(\bigcup_k (\omega^\omega \setminus \bigcup_j (\omega^\omega \setminus A_{i,j,k,l})) = \bigcup_k (\bigcap_l A_{i,j,k,l})$ 的一个码。

令 \(\Phi_{h(e)}(n, \tau, v_0, v_1) = 1$ 当且仅当 \(p^2(n) = 1$。根据递归定理，存在一个不动点 \(c$ 使得 \(\Phi_{h(c)} = \Phi_c$。

令 \( z(n) = 1 \iff \Phi_c(n, 0, 0, 0) = 1$。通过在 \(R$ 上沿着 \(<\) 进行的简易超限归纳，可证对于任意 \((\sigma, \tau, v) \in R$，\( z_{(\sigma, \tau, v)} = \{n \mid \Phi_c(n, \sigma, \tau, v) = 1\}$ 是一个递归 Borel 码，使得 \( A_{z_{(\sigma, \tau, v)}} \cong [T_{(\sigma, v)}]$ 且 \( A_{z_{(\sigma, \tau, v)}} \cap [S_{(\sigma, \tau)}] = \emptyset$。特别是，\( z^* = z_{(0, \emptyset, \emptyset)}$ 是一个递归 Borel 码，使得 \( A \cap A_{z^*} = A \cap [S_{0,0}] = \emptyset$ 且 \( [T_{(0,0)}] = B \subseteq A_{z^*}$。因此 \( z^*$ 是 \(B$ 的一个递归 Borel 码。

请注意，上述定理证明了更多内容。回顾（参见 § 1.5.1），存在一个 \( \Pi^1_1$-集合 \( A \subseteq \omega \times \omega^\omega$，使得每个 \( \Sigma^1_1$-集合 \( B$ 都形如 \( B = \neg A_n = \{x \mid (n, x) \notin A\}$ 对某些 \( n$。这些 \( n$ 被称为 \( \Sigma^1_1$-码。于是定理 2.7.2 可加强为：存在一个递归函数 \( f : \omega \times \omega \to \omega^\omega$，使得若 \( m, n$ 是 \( \Sigma^1_1$-码且 \( (2^\omega \setminus A_n) \cap (2^\omega \setminus A_m) = \emptyset$，则 \( f(n, m) \in \text{BC} \cap \Delta^1_1\)，\( (2^\omega \setminus A_{f(n,m)}) \cap (2^\omega \setminus A_n) = \emptyset$，且 \( (2^\omega \setminus A_m) \subseteq (2^\omega \setminus A_{f(n,m)})$。这是一个有效分离定理，是有效描述集合论的核心结果。我们将在后续内容中讨论相关事实。

### Remark 2.7.3. 有人可能会好奇，递归码如何能够编码与超算术码所编码的相同集合。答案在于所使用的归纳步骤数量存在权衡。例如，一个超算术开集可以用超算术码在一步内编码，但任何其递归码都将位于某个 \( \Sigma_\beta$ 中，其中 \( \beta$ 是一个可能很大的递归序数。

我们说 \( A \le \omega^\omega$ 是 \( \Sigma^1_1(\text{HYP})$，若存在某个超算术 \( x \in \Sigma_\beta$ 使得 \( A = A_x$。Louveau [85] 使用 Gandy 强迫法证明了以下结果。

### Theorem 2.7.4 (Louveau [85]). 若 \( A, B \) 是 \( \Sigma^1_1 \) 且被某个 \( x \in \Sigma_\beta \) 的 \( A_x \) 分离，则 \( A \) 可被某个 \( y \in \Sigma_\beta \cap \Delta^1_1 \) 的 \( A_y \) 与 \( B \) 分离。故若 \( A \) 是 \( \Delta^1_1 \) 且 \( \Sigma_\beta \)，则 \( A \) 是 \( \Sigma_\beta(\text{HYP})\)。

定理 2.7.2 给出了实数 \( \Delta^1_1$-集的另一种参数化。

### Corollary 2.7.5. 存在一个 \( \Pi^1_1$-集合 \( A \subseteq \omega \times \omega^\omega$，使得

- \( (\forall n)(A_n = \{y \mid (n, y) \in A\} \in \Delta^1_1)$。
- \( (\forall C)(\exists n)(C \in \Delta^1_1 \to C = A_n)$。

**证明。** 根据命题 2.2.11，存在一个偏函数 \( D : \omega \times \omega \to \omega$，其 \( \Pi^1_1$-图形参数化了 \( \Delta^1_1$-实数。定义 \( (n, y) \in A$ 当且仅当

\( (\forall i)(\exists j)(n, i, j) \in D \land (\forall x)((\forall i)(\forall j)(x(i) = j \leftrightarrow (n, i, j) \in D) \to x \in \text{BC}(\text{HYP}) \land x \in A_x) \)。

注意，若 \( (\forall i)(\exists j)(n, i, j) \in D$ 是 \( \Delta^1_1$。故 \( A$ 是 \( \Pi^1_1$。显然每个 \( A_n^1$-集合 \( C$ 都是某个 \( n$ 的 \( A_n$，且 \( A_n$ 编码了一个属于 \( \text{BC}(\text{HYP})$ 的实数。对每个 \( n$，要么 \( A_n = \emptyset$，要么 \( A_n = A_x$ 对某些 \( x \in \text{BC}(\text{HYP})$。故 \( A$ 符合要求。





### 2.7.3 练习

- 练习 2.7.1. 证明引理 2.4.8。

- 练习 2.7.2. 证明 \( y \in \Sigma_\beta \) 当且仅当 \( |T'| \le \beta + 1 \)。

## 3 可容纳性与可构性

本章从集合论视角介绍了有效可计算性的基本概念。乍看有些抽象，但从可定义性的角度来看，它们是自然而然的。

可容纳结构本质上是一种计算的内模。可构宇宙 \( L \) 通过对 Gödel 算子的超限迭代定义。通过考虑形成可容纳结构的 \( L \) 的适当初始段，我们将看到一个 \( \Pi^1_1 \)-集合在高阶递归理论中如何扮演可枚举（r.e.）集合的角色。

### 3.1 Kripke–Platek 集合论

Kripke–Platek (KP) 集合论由 Kripke [75] 和 Platek [113] 发展而来。KP 是 ZF 公理系统的一个弱化版本，捕捉了集合论环境下有效计算的基本特征。它为超越 \( \omega \) 的领域研究提供了一个自然的平台。

#### 3.1.1 KP

定义 3.1.1. 设 \( \mathscr{L} \) 表示 ZF 的语言。\( \mathscr{L} \) 中的 \( \Delta_0 \)-公式集合是最小的集合 \( X \)，由 \( \mathscr{L} \) 的原子公式组成，并在以下运算下封闭：

- (i) 若 \( \varphi \in X \)，则 \( \neg \varphi \in X \)。
- (ii) 若 \( \varphi, \psi \in X \)，则 \( \{ \varphi \land \psi, \varphi \lor \psi \} \subseteq X \)。
- (iii) 若 \( \varphi \in X \)，则 \( \{ (\forall u \in v)\varphi, (\exists u \in v)\varphi \} \subseteq X \)。

在上述 (iii) 中，公式 \( (\forall u \in v)\varphi \) 或 \( (\exists u \in v)\varphi \) 均称为 *有界公式*。形式为 \( \exists u \in v \) 或 \( \forall u \in v \) 的前缀称为 *有界量词*。\( \Delta_0 \)-公式是递归理论中 *原始递归谓词* 的类比。

定义 3.1.2. 一个 \( \Delta_0 \)-公式也称为 \( \Sigma_0 \)-公式，也称为 \( \Pi_0 \)-公式。一般来说，公式 \( \varphi(u) \) 是 \( \Sigma_{n+1} \)，如果它形式为 \( (\exists v)\psi(u, v) \)，其中 \( \psi \) 是 \( \Pi_n \)-公式。公式 \( \varphi(u) \) 是 \( \Pi_{n+1} \)，如果它形式为 \( (\forall v)\psi(u, v) \)，其中 \( \psi \) 是 \( \Sigma_n \)-公式。

定义 3.1.3. \( \Sigma \)-公式类是最小的类 \( X \)，由 \( \Delta_0 \)-公式组成，并在合取、析取、有界量化下封闭，并且若 \( \varphi \in X \) 则 \( (\exists u)\varphi \in X \)。

\( \Pi \)-公式类是最小的类 \( X' \)，由 \( \Delta_0 \)-公式组成，并在合取、析取、有界量化下封闭，并且若 \( \varphi \in X' \) 则 \( (\forall u)\varphi \in X' \)。

\( \Sigma \)-公式是经典递归理论中递归可枚举谓词的类比。请注意，\( \Sigma_1 \)-公式与 \( \Sigma \)-公式之间存在区别。\( \Sigma_1 \)-公式是 \( \Sigma \)-公式，但反之不一定成立。

### 定义 3.1.4. 理论 KP 由以下公式的全称闭合组成：

- 外延性：\((\forall x)((\forall y)((y \in u \leftrightarrow x \in u) \rightarrow x = y))\)。
- 基础公理：\((\exists x)\varphi(x) \rightarrow (\exists x)(\varphi(x) \land (\forall y \in x)\neg\varphi(y))\)，适用于所有 \(y\) 不自由出现的公式 \(\varphi\)。
- 配对公理：\((\forall x)(\forall y)(\exists z)(x \in z \land y \in z)\)。
- 并集公理：\((\forall x)(\exists y)(\forall u \in x)(\forall v \in u)(v \in y)\)。
- \(\Delta_0\)-分离公理：\((\forall x)(\exists y)(\forall u)(u \in y \leftrightarrow u \in x \land \varphi(u))\)，适用于所有 \(u\) 不自由出现的 \(\Delta_0\)-公式 \(\varphi\)。
- \(\Delta_0\)-收集公理：\((\forall x)(\forall u \in x)(\exists v)\varphi(u, v) \rightarrow (\exists y)(\forall u \in x)(\exists v \in y)\varphi(u, v)\)，适用于所有 \(y\) 不自由出现的 \(\Delta_0\)-公式 \(\varphi\)。

给定一个公式 \(\varphi\)，我们记 \(\varphi^{(w)}\) 为将 \(\varphi\) 中每个无界量词替换为限制于 \(w\) 的有界量词所得的公式。具体而言，将 \(\exists u\) 替换为 \(\exists u \in w\)，将 \(\forall u\) 替换为 \(\forall u \in w\)。显然，若 \(\varphi\) 是 \(\Sigma\)，则 \(\exists w \varphi^{(w)}\) 是 \(\Sigma\)。在 KP 下，每个 \(\Sigma\)-公式都等价于一个 \(\Sigma_1\)-公式，如下列定理所示，该定理通过对公式复杂度进行归纳证明。我们将其留作练习。

### 定理 3.1.5（\(\Sigma\)-反射原理）。设 \(\varphi\) 为一个 \(\Sigma\)-公式。则

\(\text{KP} \vdash \varphi \rightarrow (\exists w) \varphi^{(w)}\)。

因此，该定理断言在 KP 下，对于给定的 \(\Sigma\)-公式，存在一个 \( \Delta_0 \)-可定义集合。事实上，它还说明了更多：

### 定理 3.1.6（\(\Sigma\)-收集原理）。设 \(\varphi\) 为一个 \( \Sigma \)-公式，\( a \) 为一个集合。则

\(\text{KP} \vdash (\forall x \in a)(\exists y) \varphi(x, y) \rightarrow (\exists w)((\forall x \in a)(\exists y \in w) \varphi(x, y) \land (\forall y \in w)(\exists x \in a) \varphi(x, y))\)。

证明。假设 \((\forall x \in a)(\exists y) \varphi(x, y)\)。那么公式 \((\forall x \in a)(\exists y) \varphi(x, y)\) 是 \( \Sigma \)。根据定理 3.1.5，存在一个集合 \( c \)，使得 \((\forall x \in a)(\exists y \in c) \varphi^{(c)}(x, y)\)。定义 \( b = \{y \mid (\exists x \in a) \varphi^{(c)}(x, y)\} \)。根据 \(\Delta_0\)-分离公理，这样的 \( b \) 存在。可以直接验证 \( \varphi^{(c)}(x, y) \) 蕴含 \( \varphi(x, y) \)，因为 \( \varphi(x, y) \) 是 \( \Sigma \)。故 \((\forall y \in b)(\exists x \in a) \varphi(x, y)\)。由于 \((\forall x \in a)(\exists y \in c) \varphi^{(c)}(x, y)\)，我们实际上有 \((\forall x \in a)(\exists y) \varphi^{(c)}(x, y)\)。由此可得 \((\forall x \in a)(\exists y \in b) \varphi^{(c)}(x, y)\)。

### 定理 3.1.7（\(\Delta\)-分离原理）。设 \( a \) 为一个集合。对于任意 \( \Sigma \)-公式 \( \varphi(x) \) 和 \( \Pi \)-公式 \( \psi(x) \)，

\(\text{KP} \vdash (\forall x \in a)(\varphi(x) \leftrightarrow \psi(x)) \rightarrow (\exists w)(\forall x)(x \in w \leftrightarrow x \in a \land \varphi(x))\)。

证明。假设 \((\forall x \in a)(\varphi(x) \leftrightarrow \psi(x))\)。则 \((\forall x \in a)(\varphi(x) \lor \neg \psi(x))\)。注意公式 \( \varphi(x) \lor \neg \psi(x) \) 是 \( \Sigma \)。根据定理 3.1.5，存在一个集合 \( c \)，使得 \((\forall x \in a)(\varphi(x) \lor \neg \psi(x)) \leftrightarrow (\forall x \in a)(\varphi^{(c)}(x) \lor \neg \psi^{(c)}(x))\)。定义 \( b = \{y \mid y \in a \land \varphi^{(c)}(y)\} \)。根据 \(\Delta_0\)-分离公理，这样的 \( b \) 存在。

若 \( y \in b \)，则 \( y \in a \land \varphi^{(c)}(y) \)，进而 \( y \in a \land \varphi(y) \)，因为 \( \varphi(y) \) 是 \( \Sigma \)。若 \( y \in a \land \varphi(y) \)，则 \( y \in a \land \psi(y) \)，进而 \( y \in a \land \psi^{(c)}(y) \)，因为 \( \psi \) 是 \( \Pi \)。

#### 3.1.2 通过 \( \Sigma \)-递归定义

如第 1 章和第 2 章所示，使用有效超限归纳的递归定义是二阶算术中的一个强大工具。我们现在在可容纳集合论的环境下研究递归定义。这可以被视为对 \( \omega^{CK} \) 上递归的推广。

回顾，集合 \( x \) 是传递的，如果 \((\forall y)(\forall z)(y \in x \land z \in y \rightarrow z \in x)\)。注意，公式 "\( x \) 是传递的" 是 \( \Delta_0 \)。

函数 \( f \) 是 \( \Sigma \)，如果存在一个 \( \Sigma \)-公式 \( \varphi \)，使得 \( f(x) = y \leftrightarrow KP \vdash \varphi(x, y) \)。根据定理 3.1.5，\( f \) 由一个 \( \Sigma_1 \)-公式定义。不难看出，若 \( f \) 是 \( \Sigma \)，则对于任意集合 \( u \)，\( KP \vdash (\exists y)(v = f \upharpoonright u) \)，其中 \( f \upharpoonright u = \{(x, y) \mid f(x) = y \land x \in u\} \)。

### 定理 3.1.8。

设 \( G \) 是一个 \( n+2 \) 元 \( \Sigma \)-函数。存在一个 \( n+1 \) 元 \( \Sigma \)-函数 \( F \)，使得

```
KP \vdash F(y, x_1, \dots, x_n) = G(y, x_1, \dots, x_n, \langle z, F, x_1, \dots, x_n \rangle \mid z \in y).
```

证明。为简化起见，假设 \( n = 0 \)。设 \( P(f) \) 为句子：

```
f \text{ is a function } \land \text{Dom}(f) \text{ is transitive } \land
(\forall y \in \text{Dom}(f))(y = G(y, \langle z, f(z) \rangle \mid z \in y)).
```

注意 \( P(f) \) 是一个 \( \Sigma \)-公式。定义

```
Q(y, z) = (\exists f)(P(f) \land f(y) = z),
```

以及

```
F(y) = z \Leftrightarrow Q(y, z).
```

只需证明

```
KP \vdash F \text{ is a function } \land (\forall y)(\exists z)Q(y, z).
```

我们证明 KP \( \vdash (\forall y)(\exists z)Q(y, z) \)。另一个合取式可以用类似的论证来证明。假设 KP 不能证明 \( (\forall y)(\exists z)Q(y, z) \)。那么存在 KP 的一个模型 \( \mathcal{M} = \langle M, \in \rangle \)，使得 \( \mathcal{M} \models (\exists y)(\forall z)\neg Q(y, z) \)。根据基础公理，选择 \( y \) 使得

```
\mathcal{M} \models (\forall z)\neg Q(y, z) \land (\forall y' \in y)(\exists z)Q(y', z).
```





由于 Q(y, z) 是 \(\Sigma_1\)，根据定理 3.1.6，存在 \(v \in M\) 使得

\(M \models (\forall y' \in y)(\exists f \in v)(\exists z'(f(y') = z \land P(f))).\)

因此存在 \(w \in M\) 使得 \(w = \{f \mid f \in v \land P(f)\}\)。

对于任意 \(f_1, f_2 \in w\) 和 \(y' \in \text{Dom}(f_1) \cap \text{Dom}(f_2)\)，我们声称 \(f_1(y') = f_2(y')\)。假设不然。那么再次根据基础公理，存在一个 \(y'\) 使得 \(f_1(y') \neq f_2(y')\)，但对于所有 \(y'' \in y'\)，有 \(f_1(y'') = f_2(y'')\)。然而，

\(f_1(y') = G(y', (\langle y'', f_1(y'') \rangle \mid y'' \in y')) = G(y', (\langle y'', f_2(y'') \rangle \mid y'' \in y')) = f_2(y')\),

这产生矛盾。

现在取 \(f' = \bigcup_{f \in w} f\)。根据定理 3.1.7，\(f \in M\)。显然，Dom(f) 是传递的，因此 P(f) 成立。定义 \(f' = f \cup \{\langle y, G(y, f \upharpoonright y) \rangle\}\)。那么 \(M \models f'(y) = G(y, f \upharpoonright y) \land P(f')\)，从而 \(M \models Q(y, G(y, f' \upharpoonright y))\)。因此 \(M \models (\exists z)Q(y, z)\)，这产生矛盾。

因此 KP ⊢ \((\forall y)(\exists z)Q(y, z)\)。

### 备注 3.1.9.

在定理 3.1.8 中定义类似 G 的函数，通常需要经过一系列简单但繁琐的 \(\Sigma_1\)-归纳步骤。今后我们将把这些步骤的细节留给读者，并简单地称之为“通过 \(\Sigma_1\)-归纳应用定理 3.1.8”。

定理 3.1.8 是可容集理论中的核心结果。它在描述集论中扮演着与有效超限归纳相同的角色。我们通过该定理的一个应用来说明这一点。定义传递闭包算子 TC 为：

\(\text{TC}(\emptyset) = \emptyset\)，且

\(\text{TC}(a) = a \cup \bigcup \{\text{TC}(x) \mid x \in a\}.\)

通过对关系 \(\in\) 进行归纳，可以证明对于任意集合 x，TC(x) 是包含 x 的最小传递集合。问题是该算子在 KP 中是否定义良好。

设 G 为一个 \(\Sigma\)-函数，使得 \(G(\emptyset, y) = \emptyset\) 且 \(G(x, y) = x \cup \bigcup \{y_1 \mid \langle y_0, y_1 \rangle \in y\}\)。那么根据定理 3.1.8，存在一个 \(\Sigma\)-函数 F 使得 \(F(x) = G(x, (\langle y, F(y) \rangle \mid y \in x))\)。不难验证对于每个 x，F(x) = TC(x)。我们有以下推论。

### 推论 3.1.10.

KP ⊢ TC(x) 是一个 \(\Sigma\)-函数。

根据推论 3.1.10，结合定理 3.1.8 的证明，我们有以下定理。

### 定理 3.1.11.

设 G 为一个 n+2 元 \(\Sigma\)-函数。存在一个 n+1 元 \(\Sigma\)-函数 F 使得

\(\text{KP} \vdash F(y, x_1, \dots, x_n) = G(y, x_1, \dots, x_n, (\langle z, F(z, x_1, \dots, x_n) \rangle \mid z \in \text{TC}(y))).\)

设 rk 为一个函数，使得

rk(∅) = 0，且

rk(x) = sup{rk(y) + 1 | y ∈ x}.

根据定理 3.1.8，rk 是从集合到序数的一个 \(\Sigma\)-函数。对于任意集合 x，rk(x) 称为 x 的秩。在进行超限归纳时，秩函数是一个方便的工具。

#### 3.1.3 折叠引理

如果对于所有 y ∈ x 都有 y ⊆ z ⊆ x，则称集合 x 在 z 中是传递的。如果 z = x，即对于所有 y ∈ x 都有 y ⊆ x，则称集合 x 是传递的。使用定理 3.1.8，我们定义一个 \(\Sigma\)-运算 C_x(y) 如下：

C_x(∅) = ∅；

C_x(a) = \{C_x(y) \mid y \in a \cap x\}.

不难验证对于所有 b，C_b(b) 都是传递的。此外，如果 a ⊆ b 且 a 是传递的，那么对于所有 x ∈ a，C_b(x) = x。定义 c_b = \{(x, C_b(x)) \mid x \in b\}。可以将 c_b 视为从 b 到传递集合 C_b(b) 的映射。通常，c_b 不是单射。

如果对于所有 b_1, b_2 ∈ a，(∀x ∈ a)(x ∈ b_1 ↔ x ∈ b_2) → b_1 = b_2，则称集合 a 是外延的。换句话说，如果 a 中的每个集合都由其在 a 中的成员关系确定，则 a 是外延的。显然，任何传递集都是外延的。以下定理表明任何外延集都与一个传递集同构。

### 定理 3.1.12 (Mostowski [108]).

如果 a 是外延的，那么 c_a 是 a 与 C_a(a) 之间的双射。此外，对于所有 x, y ∈ a，x ∈ y 当且仅当 C_a(x) ∈ C_a(y)。

**证明。** 显然 c_a 是从 a 到 C_a(a) 的满射，且 x ∈ y 蕴含 c_a(x) ∈ c_a(y)。我们证明对于所有 x, y ∈ a，c_a(x) ∈ c_a(y) 蕴含 x ∈ y。然后根据 a 的外延性，c_a 是单射。

假设存在 y_0 ∈ a，使得对于所有 rk(y) < rk(y_0) 的 y ∈ a 和 x ∈ a，x ∈ y 当且仅当 c_a(x) ∈ c_a(y)，但存在 x_0 ∈ a 使得 x_0 ∉ y_0 且 c_a(x_0) ∈ c_a(y_0)。因为 c_a(x_0) ∈ c_a(y_0)，存在 z ∈ a∩y_0 使得 c_a(x_0) = c_a(z) = c_a(y_0)。那么 rk(z) < rk(y_0)。然而，这意味着 x_0 = z ∈ y_0，产生矛盾。

#### 3.1.4 可定义性

用 M 表示结构 M 的定义域。

### 定义 3.1.13.

设 F 为语言 L 中的一组公式。

- (i) 给定一个结构 M 和 A ⊆ M，如果存在公式 φ(u, v_0, ..., v_n) ∈ F 和 M 中的有限序列 a_0, ..., a_n，使得 x ∈ A 当且仅当 M ⊨ φ(x, a_0, ..., a_n)，则称 A 在 M 中是 F-可定义的；
- (ii) 如果 \(\mathfrak{M}\) 是一组结构，且对于 \(\mathfrak{M} \in \mathfrak{M}\) 有 \(A_M \subseteq M\)，那么如果存在 \(\mathfrak{F}\) 中的一个无参数公式 \(\varphi(u)\)，使得对于任何 \(\mathfrak{M} \in \mathfrak{M}\)，\(x \in A_{\mathfrak{M}}\) 当且仅当 \(\mathfrak{M} \models \varphi(x)\)，则称 \(\{A_M\}_{\mathfrak{M} \in \mathfrak{M}}\) 在 \(\mathfrak{M}\) 中是 \(\mathfrak{F}\)-一致可定义的。

注意，要使一组结构一致可定义，定义它的公式中不应有参数。

#### 3.1.5 绝对性

### 定义 3.1.14.

给定语言 \(\mathscr{L}\) 中的一组句子 \(\mathfrak{F}\)，如果对于每个 \(\varphi \in \mathfrak{F}\)，\(\mathfrak{M} \models \varphi \Leftrightarrow \mathfrak{N} \models \varphi\)，则称两个 \(\mathscr{L}\)-结构 \(\mathfrak{M}\) 和 \(\mathfrak{N}\) 是 \(\mathfrak{F}\)-初等等价的，记作 \(\mathfrak{M} \equiv_{\mathfrak{F}} \mathfrak{N}\)。

如果 \(\mathfrak{F}\) 是所有句子的集合，则称 \(\mathfrak{M}\) 和 \(\mathfrak{N}\) 是 *初等等价* 的，并记作 \(\mathfrak{M} \equiv \mathfrak{N}\)。

### 定义 3.1.15.

给定一组句子 \(\mathfrak{F}\)，如果对于每个 \(\varphi(\bar{v}) \in \mathfrak{F}\) 和有限序列 \(\bar{a} \in M^{<\omega}\)，\(\mathfrak{M} \models \varphi(\bar{a}) \Leftrightarrow \mathfrak{N} \models \varphi(j(\bar{a}))\)，则称从 \(\mathfrak{M}\) 到 \(\mathfrak{N}\) 的嵌入 \(j\) 是 \(\mathfrak{F}\)-初等的，并记作 \(\mathfrak{M} \prec_j^{\mathfrak{F}} \mathfrak{N}\)。

如果 \(\mathfrak{F}\) 是所有公式的集合，则记作 \(\mathfrak{M} \prec^j \mathfrak{N}\)。如果 \(j\) 是包含映射，则记作 \(\mathfrak{M} < \mathfrak{N}\)，并称 \(\mathfrak{M}\) 是 \(\mathfrak{N}\) 的 *初等子结构*，\(\mathfrak{N}\) 是 \(\mathfrak{M}\) 的 *初等扩展结构*。

### 定义 3.1.16.

给定结构类 \(\mathfrak{M}\) 和公式 \(\varphi(\bar{v})\)，(i) 如果对于 \(\mathfrak{M}\) 中的每一对 \(\mathfrak{M} \subseteq \mathfrak{N}\) 和任何有限序列 \(\bar{a} \in M^{<\omega}\)，\(\mathfrak{M} \models \varphi(\bar{a})\) 蕴含 \(\mathfrak{N} \models \varphi(\bar{a})\)，则称 \(\varphi\) 是 \(\mathfrak{M}\)-向上绝对的；(ii) 如果对于 \(\mathfrak{M}\) 中的每一对 \(\mathfrak{M} \subseteq \mathfrak{N}\) 和任何有限序列 \(\bar{a} \in M^{<\omega}\)，\(\mathfrak{N} \models \varphi(\bar{a})\) 蕴含 \(\mathfrak{M} \models \varphi(\bar{a})\)，则称 \(\varphi(\bar{v})\) 是 \(\mathfrak{M}\)-向下绝对的；(iii) 如果 \(\varphi(\bar{v})\) 既是 \(\mathfrak{M}\)-向上绝对的又是 \(\mathfrak{M}\)-向下绝对的，则称 \(\varphi(\bar{v})\) 是 \(\mathfrak{M}\)-绝对的。

### 命题 3.1.17.

设 \(\mathfrak{M}\) 为传递结构类。(i) 每个 \(\Sigma_0\)-公式都是 \(\mathfrak{M}\)-绝对的；(ii) 每个 \(\Sigma_1\)-公式都是 \(\mathfrak{M}\)-向上绝对的；(iii) 每个 \(\Pi_1\)-公式都是 \(\mathfrak{M}\)-向下绝对的。因此每个 \(\Delta_1\)-公式都是 \(\mathfrak{M}\)-绝对的。

**证明。** 我们通过对 \(\Sigma_0\)-公式的复杂度进行归纳来证明 (i)，并将 (ii) 和 (iii) 留给读者。假设 \(\mathfrak{M} \subseteq \mathfrak{N}\) 且 \(\varphi(a)\) 的形式为 \((\exists u \in a)\psi(u, a)\)，其中 \(\psi(u, a)\) 是某个 \(\Sigma_0\)-公式，且 \(a \in M\)。如果 \(\mathfrak{M} \models \varphi(a)\)，则存在 \(a' \in M\) 使得 \(\mathfrak{M} \models \psi(a', a)\)。因为 \(\mathfrak{M} \subseteq \mathfrak{N}\)，根据归纳假设，\(\mathfrak{N} \models \psi(a', a)\)。如果 \(\mathfrak{N} \models \varphi(a)\)，则存在 \(a' \in N\) 使得 \(\mathfrak{N} \models \psi(a', a)\)。因为 \(a' \in a\) 且 \(a \in M\)，根据传递性，有 \(a' \in M\)。然后根据归纳假设，\(\mathfrak{M} \models \psi(a', a)\)。





关于 KP 的更多事实可参见 [3]。

#### 3.1.6 练习

**练习 3.1.1.** *证明定理 3.1.5.*

**练习 3.1.2.** *完成命题 3.1.17 的证明。*

## 3.2 可容集

集合的宇宙 $V$ 在序数上归纳定义：

```
\( V_0 = \emptyset, \)
\( V_{\beta+1} = \mathscr{P}(V_\beta), \)
\( V_\lambda = \bigcup_{\alpha < \lambda} V_\alpha \text{ when } \lambda \text{ is a limit ordinal, and} \)
\( V = \bigcup_\alpha V_\alpha. \)
```

**定义 3.2.1.** 一个 *可容结构*（或可容集）是 KP 的一个模型 \(\mathfrak{M}\)，形式为 \(\mathfrak{M} = \langle M, \in_M \rangle\)，其中 \(M\) 是 \(V\) 中的传递集，\(\in_M\) 是 \(\in\) 对 \(M\) 的限制。当上下文清晰时，我们常将 \(\in_M\) 简单地写作 \(\in\)。

**定义 3.2.2.** 传递结构 \(\mathfrak{M}\) 的 *序数*，记作 \(o(\mathfrak{M})\)，是不属于 \(M\) 的最小序数。若存在某个可容结构 \(\mathfrak{M}\) 使得 \(\alpha = o(\mathfrak{M})\)，则称序数 \(\alpha\) 为 *可容*。

\(\mathfrak{M}\) 上的关系 \(S \subseteq M^n\) 是 \(\Sigma_n\) 的，当且仅当存在一个 \(\Sigma_n\)-公式 \(\varphi\) 使得

```
\( S(a_1, a_2, \dots, a_n) \Leftrightarrow \mathfrak{M} \vDash \varphi(a_1, a_2, \dots, a_n). \)
```

上述定义中允许使用参数。显然，对于任意 \(a \in M\)，\(a\) 和 \(\{a\}\) 均为 \(\Sigma_1\)。此外，由定理 3.1.5 可知，对于可容的 \(\mathfrak{M}\)，\(\Sigma_1\)-关系在 \(\vee, \wedge, \exists x \in a, \forall x \in a\) 和 \(\exists x\) 下封闭。

#### 3.2.1 最小可容集

**定义 3.2.3.** 一个集合 \(a \in V\) 称为 *遗传有限*，记作 \(a \in \text{HF}\)，若 \(\text{TC}(a)\) 是有限的。

HF 可按如下归纳重新定义：

```
HF(0) = 0,
HF(n + 1) = {a | a ⊆ HF(n)},
HF = ∪_{n<ω} HF(n).
```

因此 HF = V_ω。我们将以下定理留作练习。

### 定理 3.2.4. HF 是最小可容集。

(HF, ε) 是我们遇到的第一个自然的可容集示例。将 n 识别为自然数（在算术中）和 n 识别为有限序数（在集合论中）有一种自然且标准的方法。我们将遵循识别这两个对象的惯例。以下定理突出了递归论与可容论之间的重要联系，并解释了在广义递归论研究中引入可容集的原因。

### 定理 3.2.5. 设 S 是自然数上的一个关系。则 S 是递归可枚举的，当且仅当 S 在 (HF, ε) 上是 Σ1 的。

证明。只需假设 S 是无限的。递归可枚举关系的类是一阶算术语言中在 (ω, +, ·, 0, 1, <) 上 Σ1-可定义的关系类。因此，对于“仅当”部分，只需证明：若 S ⊆ ω 在 (ω, +, ·, 0, 1, <) 上是 Σ1 的，则它在集合论语言中在 (HF, ε) 上也是 Σ1 的。显然，HF 中的序数集，即 ω，在 (HF, ε) 上是 Δ1-可定义的。现在，若 S 由涉及 +, · 的开放公式 φ 定义，则它在集合论语言中由 (HF, ε) 上的 Δ1-公式 φ* 定义，这是常规做法。此外，“u < v”在 (HF, ε) 上可由 “u ∈ v” 定义。因此，任何涉及 +, ·, < 并定义 S 的开放公式，均可在集合论语言中由 (HF, ε) 上的相应 Δ1-公式定义。

对于由集合论语言中的有界公式 φ = (∃i < n) ψ 定义的 S（其中 ψ 为开放公式），令 φ* = (∃u ∈ n) ψ*(u)，其中 ψ* 是与 ψ 对应的 Δ1-公式（注意 φ* 中的 “n” 表示有限序数 n）。对于形式为 φ = (∀i < n) ψ 且 ψ 为开放公式的情况，以显而易见的方式定义 φ*。通过对公式复杂度的归纳，任何由一阶算术语言中的有界公式定义的 S ⊆ ω，均有对应的定义，即通过集合论语言中在 (HF, ε) 上的 Δ1-公式。

现在假设 S = (m | (∃i)ψ(i, m))，其中 ψ 是算术中的有界公式。通过归纳，令 ψ* 为 Δ1，使得 (ω, +, ·, 0, 1, <) ⊨ ψ(n, m) 当且仅当 (HF, ε) ⊨ ψ*(n, m)。则 n ∈ S 当且仅当

```
(HF, ε) ⊨ (∃u)(u is an ordinal ∧ ψ*(u, m)).
```

因此 S 在 (HF, ε) 上是 Σ1 的。

对于另一方向，我们首先定义函数 \( f : \omega \to \text{HF} \) 如下：

```
f(0) = 0,
f(1) = {0},
f(2^{n_1} + 2^{n_2} + \dots + 2^{n_k}) = {f(n_1), f(n_2), \dots, f(n_k)}.
```

可以直接验证 \( f \) 是双射。此外，

- \( f \) 在 \((\text{HF}, \in)\) 上是 \(\Delta_1\) 的。
- 定义 \( f^*(n) = m \) 当且仅当 \( m \) 作为序数是集合 \( f(n) \)。则关系 “\( f(n) = m' \) 是递归的。
- 对于每个 \(\Delta_0\)-公式 \(\varphi\)，集合 \( T_\varphi = \{(n_1, n_2, \dots, n_k) \mid (\text{HF}, \in) \models \varphi(f(n_1), f(n_2), \dots, f(n_k))\} \) 是递归的。

现在若 \( S \) 在 \((\text{HF}, \in)\) 上是 \(\Sigma_1\) 的，则存在一个 \(\Delta_0\)-公式 \(\varphi\)，使得 \( S(m) \) 当且仅当存在 \( u \in \text{HF} \) 使得 \((\text{HF}, \in) \models \varphi(u, m)\)。因此 \( S(m) \) 当且仅当 \((\exists i)(\exists j)(f^*(i) = m \land (i, j) \in T_\varphi)\)。我们得出结论：\( S \) 是一个递归可枚举关系。

由定理 3.2.5 的证明，我们得到以下结果。

**命题 3.2.6.** 对于任意 \( S \subseteq \text{HF} \)，存在 \( x_S \subseteq \omega \)，使得 \( S \) 在 \((\text{HF}, \in, x_S)\) 中是 \(\Delta_1\)-可定义的，且 \( x_S \) 在 \((\text{HF}, \in, S)\) 中是 \(\Delta_1\)-可定义的。

_证明._ 由定理 3.2.5 的证明，存在双射 \( f : \omega \to \text{HF} \)，它在 \((\text{HF}, \in)\) 中是 \(\Delta_1\)-可定义的。定义 \( n \in x_S \) 当且仅当 \( f(n) \in S \)。

从模型论角度看，定理 3.2.5 可被视为 \((\text{HF}, \in)\) 与 \((\omega, \in)\) 之间 \(\Sigma_1\)-公式的双重诠释（参见 [52]）。

#### 3.2.2 练习

**练习 3.2.1.** *证明定理 3.2.4。*

## 3.3 可构性

可构宇宙 \( L \) 由 Gödel [37] 引入，以证明广义连续统假设和选择公理的相容性。Jensen [55] 发展了 \( L \) 的精细结构理论，该理论对高阶递归论产生了深远影响。

#### 3.3.1 可构宇宙

用一元关系符号 \(\dot{A}\) 扩展集合论语言 \(\mathscr{L}\)，并将其记作 \(\mathscr{L}^{\dot{A}}\)。

**定义 3.3.1.** 设 \(A\) 为一个集合。给定集合 \(X\)，若存在 \(\mathscr{L}^{\dot{A}}\) 中的公式 \(\varphi(\mathbf{v})\)，使得在将 \(\dot{A}\) 解释为 \(A \cap X\) 时，有 \(Y = \{y \mid (X, \in, A \cap X) \models \varphi(y)\}\)，则称 \(Y\) 是 *相对于结构* \((X, \in, A \cap X)\) *对 \(A\) 可定义的*，记作 \(Y \in Def^A(X)\)。

通过对序数的递归，定义

\(L_0[A] = 0,\)
\(L_{\beta+1}[A] = Def^A(L_\beta[A]),\)
\(L_\lambda[A] = \bigcup_{\beta<\lambda} L_\beta[A], \text{if } \lambda \text{ is a limit ordinal.}\)

定义 \(L[A] = \bigcup_\beta L_\beta[A]\)，并令 \(L = L[\emptyset]\)。显然 \(L[A]\) 是一个真类。

若 \(x \in L[A]\)，则称 \(x\) 是 \(A\)-可构的。特别是，若 \(A = 0\)，则称 \(x\) 是可构的。\(L\) 的构造在任何可容结构 \(\mathcal{M}\) 上是一致 \(\Sigma_1\)-可定义的，其含义见下述定理（证明略过）。这涉及一个繁琐的编码装置，通过引用定理 3.1.8 可知它是 \(\Sigma_1\)-可定义的。详情见 [22]。

**定理 3.3.2.** 存在一个 \(\Sigma_1\)-公式 \(\varphi(u, v)\)，使得对于任何可容结构 \(\mathcal{M}\) 和序数 \(\beta \in M\)，\(\mathcal{M} \models \varphi(\beta, x)\) 当且仅当 \(x = L_\beta\)。此外，\(L_\beta\) 是满足 \(\mathcal{M} \models \varphi(\beta, x)\) 的唯一集合。因此，\(L_\beta\) 在 \(\mathcal{M}\) 上是一致 \(\Delta_1\)-可定义的。

存在一种通过 Gödel 引入的以下原始递归算符集合生成 \(L\) 的递归论方法：

- (i) \(F_0(x, y) = \{x, y\}.\)
- (ii) \(F_1(x, y) = x \setminus y.\)
- (iii) \(F_2(x, y) = x \times y = \{x, y\}.\)
- (iv) \(F_3(x, y) = \{(u, z, v) \mid z \in x \wedge (u, v) \in y\}.\)
- (v) \(F_4(x, y) = \{(u, v, z) \mid z \in x \wedge (u, v) \in y\}.\)
- (vi) \(F_5(x, y) = \bigcup x.\)
- (vii) \(F_6(x, y) = \{y \mid \exists z(z, y) \in x\}.\)
- (viii) \(F_7(x, y) = \in \cap x \times x.\)
- (ix) \(F_8(x, y) = \{z_1 \mid \exists z_0((z_0, z_1) \in x \wedge z_0 \in y)\}.\)
- (x) \(F_9(x) = A \cap x.\)

令

\(\mathcal{S}^A(U) = U \cup \{U\} \cup \bigcup_{i \le 9} \{z \mid (\exists x \in U \cup \{U\})(\exists y \in U \cup \{U\})(z = F_i(x, y))\}\)

和

\(\mathcal{R}^A(U) = \bigcup_{n < \omega} (\mathcal{S}^A)^n(U).\)





## Define

```
J_0[A] = \emptyset,
J_{\beta+1}[A] = \omega^\omega(J_\beta[A]),
J_\lambda[A] = \bigcup_{\beta<\lambda} J_\beta[A], \text{ if } \lambda \text{ is a limit ordinal.}
J[A] = \bigcup_\beta J_\beta[A]
```

如果 \( A = \emptyset \)，则我们将 \( J \) 写作 \( J[A] \)。直观地，并根据 Jensen [55]，\( J_{\beta+1} \) 是将 \( J_\beta \) 的可定义子集集合在秩中向上“拉伸” \( \omega \) 个层级而不添加新集合的结果。以下命题的证明可见 [22]。

### 命题 3.3.3. 对于所有 \(\beta\),

- \( J_\beta[A] \) 是过渡的。
- 存在一个 \(\Sigma_1\)-公式 \(\varphi(u, w)\)，使得对于任何两个序数 \( v < \beta \)，\( (J_\beta, \in) \models \varphi(v, x) \) 当且仅当 \( x = J_v \);
- 存在一个 \(\Sigma_1\)-公式 \(\varphi_\prec(u, v)\)，使得
  - (i) 对于任何 \(\beta\)，\(\varphi_\prec(u, v)\) 在 \( J_\beta \) 上定义一个良序 \( <_J \);
  - (ii) 对于任何 \( v > \beta \)，如果 \( y \in J_\beta \) 且 \( (J_v, \in) \models \varphi_\prec(x, y) \)，那么 \( x \in J_\beta \) 且 \( (J_\beta, \in) \models \varphi_\prec(x, y) \).
- 定理 3.3.2 对 \( J_\beta \) 依然成立;
- \( J_{\beta+1}[A] \cap \mathscr{P}(J_\beta[A]) = \text{Def}^\omega(J_\beta[A]) \).
- \( L_\beta[A] \subseteq J_\beta[A] \subseteq L_{\omega\beta} \).
- \( J_\beta[A] = L_\beta[A] \) 当且仅当 \( \alpha\beta = \beta \).
- \( L[A] = \bigcup_\beta J_\beta[A] \);
- 定理 3.3.2 对 \( J \) 依然有效。

Gödel 算子为构造 \( L \) 提供了一种算法化的方法。它揭示了对可定义性的引用中隐藏的“黑箱”。基于命题 3.3.3，我们可以将 \( L \) 视为在序数类上通过有效跨诱导获得的，类似于超算术集在 \( \omega_1^{\text{CK}} \) 上的定义方式。这种联系很有用，因为它表明 \( L \) 的初始段可作为一般环境下的计算模型。

### 3.3.2 紧缩与斯科伦化

如果在结构 \( \mathfrak{M} \) 内工作并执行 \( L \) 的逐阶段构造，那么当 \( \mathfrak{M} \) 满足如可接受性等足够强的条件时，对于每个 \( \beta \in M \)，都会得到相同的 \( L_\beta \)。以下定理形式化了这一思想。令 \( (L_\beta)^\mathfrak{M} \) 表示在 \( \mathfrak{M} \) 中构造的 \( L_\beta \)。

### 定理 3.3.4. 设 $\mathcal{M}$ 为 KP 的过渡模型。那么对于每个 $\beta < o(M)$，$L_\beta \in M$ 且 $(L_\beta)^\mathcal{M} = L_\beta$。

**证明.** 根据定理 3.3.2，公式 “$x = L_\beta$” 在 $\mathcal{M}` 上是 $\Delta_1`-可定义的。根据 $\Delta_0`-公式的绝对性，$L_\beta \in M` 且 $(L_\beta)^\mathcal{M} = L_\beta$。

### 推论 3.3.5. 假设 $\mathcal{M}` 是过渡的、可接受的，且 $\mathcal{M} \models \text{“V = L”}$。那么 $M = L_a$，其中 $a = o(\mathcal{M})$。

### 定理 3.3.6. $a` 是可接受的，当且仅当 $(L_a, \in)` 是可接受的。

**证明.** 如果 $(L_a, \in)` 是可接受的，那么 $a` 是可接受的。

如果对于某个可接受的 $\mathcal{M}`，$a = o(\mathcal{M})$，那么根据定理 3.3.4，对于每个 $\beta < a$ 都有 $(L_\beta)^\mathcal{M} = L_\beta$。因此，只需证明 $L_a = \bigcup_{\beta < a}(L_\beta)^\mathcal{M}` 是可接受的。我们验证 $\Delta_0`-收集在 $L_a` 中成立，并将其他性质的验证留给读者。

假设 $(L_a, \in) \models (\forall x \in a)(\exists y)\varphi(x, y)$。根据 $\Delta_0`-公式的绝对性，对于每个 $x \in a$，存在一个（最小的）$\beta < a` 使得

$\mathcal{M} \models (\exists y \in \mathcal{E}) \varphi(x, y).$

那么，定理 3.3.2 和关于 $\Sigma`-收集的定理 3.1.6 蕴含存在一个 $a_0 < a` 使得 $a \in L_{a_0}$，且

$\mathcal{M} \models (\forall x \in a)(\exists \beta < a_0)(\exists y \in L_\beta)\varphi(x, y).$

现在，$\Delta_1`-公式的绝对性给出

$(L_a, \in) \models (\forall x \in a)(\exists y)\varphi(x, y).$

那么如果 $y \in (L_a, \in) \models (\exists x \in a)\varphi(x, y)) \in L_{a_0+1}$ 且包含在 $L_a` 中。

显然，如果 $a = \omega$，那么 $L_a = \text{HF}$。因此，$L_a` 是最小的可接受集合（参见定理 3.2.4）。注意，如果 $a > \omega` 是可接受的，那么 $\omega a = a`。

$L` 的一个基本性质是以下被称为紧缩的性质：

### 定理 3.3.7. 假设 $\beta > 0` 且 $(X, \in) \prec_{\Sigma_1} (J_\beta, \in)$。那么对于某些 $\gamma \le \beta`，$(X, \in) \cong (J_\gamma, \in)$。而且，对于每个 $x \in X`，$\pi(x) \supseteq x`。

**证明.** 假设 $(X, \in) \prec_{\Sigma_1} (J_\beta, \in)$。那么 $(X, \in)` 是良基的，并满足外延公理。根据定理 3.1.12，存在一个过渡集合 $M` 使得

$\pi : (X, \in) \cong (M, \in).$

我们声称 $M = J_\gamma$，其中 $\gamma = \sup(\pi[\delta]) \in \delta \cap \text{On}$。

显然，$\langle M, \in \rangle \prec_{\Sigma_1}^{\Sigma_1} \langle J_\beta, \in \rangle` 且 $M` 是过渡的。根据命题 3.3.3，存在一个 $\Sigma_0`-公式 $\varphi(x, \delta, s)`，使得对于任何 $x \in J_\delta` 和 $\delta < \beta`，$(J_\beta, \in) \models \exists \exists \varphi(x, \delta, s)` 当且仅当 $x = J_\delta$。由于 $M` 是过渡的，通过对 $\delta < \gamma` 的归纳，我们证明对于任何 $\delta < \gamma` 都有 $J_\delta \in M`。因此 $J_\gamma \subseteq M`。

显然 $J_0 = \emptyset \in M`。如果 $\delta > 0`，那么 $\pi^{1+\delta}(\beta) < \beta`。那么 $(J_\beta, \in) \models (\exists x)(\exists s)\varphi(x, \pi^{-1}(\delta), s)`，因此 $(M, \in) \models (\exists x)(\exists s)\varphi(x, \delta, s)`。令 $x \in M` 和 $s \in M` 使得 $(M, \in) \models \varphi(x, \delta, s)`。根据 $\varphi(x, \delta, s)` 的绝对性，任何包含 $x, s` 和 $\delta` 的可接受结构 $\aleph` 都满足 $\varphi(x, \delta, s)`。根据命题 3.3.3，$J_\delta \ni x \in M`。

此外，对于任何 $x \in M`，存在一个 $\delta < \beta` 使得 $\pi^{-1}(x) \in J_\delta`。因此 $(J_\beta, \in) \models (\exists \delta)(\exists y)[(\exists s)\pi^{-1}(x) \in y \wedge \varphi(y, \delta, s)]`。那么 $(M, \in) \models (\exists \delta)(\exists y)[(\exists s)x \in y \wedge \varphi(y, \delta, s)]`。再次根据命题 3.3.3，对于某些 $\delta' < \gamma`，有 $x \in J_{\delta'}`。我们得出 $J_\gamma \supseteq M`，因此 $J_\gamma = M`。

假设对于某些 $x \in X`，有 $x <_{J_\beta} \pi(x)`。取 $x_0` 为这样的 $<_{J_\beta}`-最小集合。由于 $\pi(x_0) \in J_\beta`，所以 $x_0 \in J_\beta`，因此存在一个 $x_1 \in X` 使得 $\pi(x_1) = x_0`。如果 $x_0 <_{J_\beta} x_1`，那么 $\pi(x_0) <_{J_\beta} \pi(x_1) = x_0`，这与假设 $x_0 <_{J_\beta} \pi(x_0)` 矛盾。所以 $x_1 <_{J_\beta} \pi(x_1) = x_0`，这与选择 $x_0` 为 $<_{J_\beta}`-最小反例相矛盾。

紧缩定理（3.3.7）的一个直接后果是 $V = L` 蕴含连续统假设。我们将证明留作练习。

### 推论 3.3.8. $2^\omega \cap L = 2^\omega \cap L_\alpha$。

在可构性理论中，另一个重要工具是使用斯科伦函数。如果一个关系或函数在 $\aleph` 上是 $\Sigma_n`-可定义的（可能带有参数），则称其为 $\Sigma_n(\aleph)`-可定义的。

### 定义 3.3.9. 给定一个结构 $\mathfrak{M}`，$\aleph` 的一个 $\Sigma_n`-斯科伦函数是一个带有参数 $p \in M` 的 $\Sigma_n(\aleph)`-可定义函数 $h : \omega \times M \to M`，使得对于任何在 $\aleph` 上带有参数 $p, x \in M` 且是 $\Sigma_n`-可定义的 $A \subseteq M`，存在一个 $i \in \omega` 使得 $h(i, x) \in A$。

因此，一个 $\Sigma_n`-斯科伦函数是 $\Sigma_n`-集合的一个 $\Sigma_n`-可定义选择函数。

### 命题 3.3.10. 假设 $a > 0` 是可接受的，且 $h` 是 $(J_a, \in)` 的一个 $\Sigma_n`-斯科伦函数。那么

- (i) 对于任何 $x \in J_a`，$x \in \text{Range}(h(\omega \times \{x\}))` 且 $(\text{Range}(h(\omega \times \{x\})), \in) \prec_{\Sigma_n} (J_a, \in)`；
- (ii) 如果 $q \in J_a` 且 $X \subseteq J_a` 在有序对下封闭，那么 $X \cup \{q\} \subseteq \text{Range}(h(\omega \times (X \cup \{q\})))` 且 $(\text{Range}(h(\omega \times (X \cup \{q\}))), \in) \prec_{\Sigma_n} (J_a, \in)`。

证明。注意 (i) 验证起来很简单，是模型论中的一个标准事实。对于 (ii)，由于 $X` 在有序对下封闭，用于在 $\text{Range}(h(\omega \times (X \cup \{q\})))` 中定义有序序列的来自 $X` 的任何有限序列都可以由单个参数编码。因此，证明 $(\text{Range}(h(\omega \times (X \cup \{q\}))), \in) \prec_{\Sigma_n} (J_a, \in)` 是常规的。

我们指出，$\Sigma_n`-斯科伦函数的存在并非平凡事实。在模型论中，为结构 $\mathfrak{M}` 定义斯科伦函数需要对 $M` 进行良序。然而，在可构宇宙 $L` 中，存在一个一致的 $\Sigma_1`-可定义斯科伦函数。





命题 3.3.11. 存在一个 \(\Sigma_1\)-公式 \(\varphi(x, y, i, z)\)，使得对于任何序数 \(\alpha\)，函数

\(h_\alpha(i, x) = y \leftrightarrow \langle J_\alpha, \in \rangle \models (\exists z)\varphi(x, y, i, z)\)

是 \(\langle J_\alpha, \in \rangle\) 的一个 \(\Sigma_1\)-Skolem 函数。

**证明.** 由命题 3.3.3，存在一个 \(\Sigma_1\)-公式 \(\varphi(u, v)\)，它为任何可接受的 \(\alpha\) 定义了 \(J_\alpha\) 上的良序 \(<_J\)。显然存在所有 \(\Sigma_0\)-公式的 \(\Sigma_1\)-枚举 \(\langle \varphi_i(u, v, w) \rangle\)。换句话说，存在一个 \(\Sigma_1\)-公式 \(\varphi(x, y, i, z)\)，使得 \(\langle J_\alpha, \in \rangle \models \varphi(x, y, i, z) \leftrightarrow \langle J_\alpha, \in \rangle \models \varphi_i(x, y, z)\)。定义 \(h_\alpha(i, x)\) 为 \(y\)，使得 \(\langle y_0, y_1 \rangle\) 是满足 \(\langle J_\alpha, \in \rangle \models \varphi_i(y_0, y_1, x)\) 的 \(<_J\)-最小对。由命题 3.3.3，\(h_\alpha(i, x)\) 是 \(\Sigma_1\)-可定义的。

由 \(\alpha\) 的可接受性，使用一些可以在 [22] 中找到的繁琐编码论证，可以证明关系 \(h_\alpha(i, x) = y\) 是一致 \(\Sigma_1\) 的。令 \(h_\alpha(i, x) = y\) 当且仅当存在 \(y_0, y_1\) 使得 \(\langle J_\alpha, \in \rangle \models \varphi(y_0, y_1, x)\)，并且存在 \(z = \langle z_0, z_1 \rangle\) 使得 \(\langle z_0, z_1 \rangle <_J \langle y_0, y_1 \rangle\)，并且对于任何对 \(\langle z_0, z_1 \rangle \in J_\alpha\)，\(\langle J_\alpha, \in \rangle \models \neg \varphi(z_0, z_1, x)\)。由于 \(z\) 对任何可接受的 \(\alpha\) 都是一致 \(\Delta_1\)-可定义的，我们有 \(h_\alpha(i, x)\) 对任何可接受的 \(\alpha\) 都是一致 \(\Sigma_1\)-可定义的。

如果 \(\alpha\) 是可接受的，我们称 \(\Sigma_1\)-Skolem 函数 \(h_\alpha\) 为 \(\alpha\) 的规范 \(\Sigma_1\)-Skolem 函数。

命题 3.3.12. 如果 \(\alpha > \omega\) 是可接受的，则 \(\alpha \ge \omega_1^{CK}\)。

**证明.** 假设 \(\alpha\) 是可接受的且 \(\omega < \alpha < \omega_1^{CK}\)。由定理 3.3.6，\(L_\alpha\) 是可接受的。由定理 13.4，存在一个递归函数 \(f\)，使得对于每个 \(n \in \omega\)，\(f(n) = \langle \{i, j\} | i <_J j < n \rangle\)。固定一个数 \(n \in \omega\) 使得 \(|n| = \alpha\)。那么 \(W_{f(n)}\) 的序类型是 \(\alpha\)，且由定理 3.2.5，\(W_{f(n)} \in L_{\omega+1} \subseteq L_\alpha\)。由 \(\Sigma\)-归纳，存在一个 \(\Sigma_1\) 序保持双射 \(g : W_{f(n)} \to \alpha\)。由于 \(W_{f(n)} \in L_\alpha\)，由 \(\alpha\) 的可接受性，\(\alpha \in L_\alpha\)。这产生矛盾。

#### 3.3.3 练习

- 练习 3.3.1. 证明 \(\langle L_{\omega_1}, \in \rangle = \text{KP} + \text{"V = L"}\)。

- 练习 3.3.2. 证明推论 3.3.8。

- 练习 3.3.3 (Putnam [115]). 证明对于任何可数序数 \(\alpha\)，存在一个可数序数 \(\beta\) 使得 \(L_{\beta+1} \models L_\beta \models 2^\omega = 0\)。

## 3.4 投影与主代码

为了使本章保持在合理长度内且证明更简单，我们呈现 Jensen [55] 中结果的较弱版本。尽管如此，关键思想提取自 [55]，且结果对于递归论应用是充分的。

#### 3.4.1 投影

**定义 3.4.1.** 设 \(\alpha > 0\) 且 \(n \ge 1\)。\(\alpha\) 的 \(\Sigma_n\)-projectum \(\rho_\alpha^n\) 是使得存在一个 \(\Sigma_1(J_\alpha)\)-可定义函数 \(f\) 将 \(J_\rho\) 的一个子集映射到 \(J_\alpha\) 上的最小序数 \(\rho\)。

显然对于任何 \(n \ge 1\)，\(\rho_\alpha^n\) 存在。在上述定义中可以将 \(J_\rho\) 替换为 \(\omega\rho\)。为了证明这一点，我们需要以下读者自行证明的引理：

**引理 3.4.2.** 设 \(\alpha > 0\)。对于每个 \(1 \le \gamma \le \omega\alpha\)，存在一个 \(\Sigma_1(J_\alpha)\)-可定义的双射，它在 \(\omega\alpha\) 与 \(\gamma \times \omega\alpha\) 之间。

**命题 3.4.3.** 设 \(\alpha > 0\)。存在一个 \(\Sigma_1(J_\alpha)\)-可定义函数，它从 \(\omega\alpha\) 映射到 \(J_\alpha\) 上。

**证明.** 令 \(f_0 = (f^0, f^1)\) 为由引理 3.4.2 保证（设 \(\gamma = \omega\alpha\)）通过 \(<_{J_\alpha}\)-最小参数 \(p \in J_\alpha\) 定义的 \(\omega\alpha\) 与 \((\omega\alpha)^2\) 之间的双射。对 \(\gamma < \omega\alpha\) 定义 \(f_{n+1}(\gamma) = (f^0(\gamma), f_n(f^1(\gamma)))\)。容易验证 \(f_n\) 是带参数 \(p\) 的 \(\Sigma_1(J_\alpha)\)-可定义函数，并且是在 \(\omega\alpha\) 与 \((\omega\alpha)^{n+2}\) 之间的双射。令 \(h_\alpha\) 为 \(J_\alpha\) 的规范 \(\Sigma_1\)-Skolem 函数。设 \(X = h_\alpha(\omega \times (\omega\alpha \times p))\)。注意对于每个 \(n < \omega\) 和 \(y < \omega\alpha\)，存在一个 \(i_n\) 使得 \(f_p(y) = h_\alpha(i_n, \langle p, y \rangle)\)。因此对于每个 \(\chi < \omega\alpha\)，\(\chi \in X\)。由命题 3.3.10，\((X, \in) \prec_{\Sigma_1} (J_\alpha, \in)\)。由定理 3.3.7，存在 \(\beta \le \alpha\) 和同构 \(\pi : (X, \in) \cong (J_\beta, \in)\)。而且，\(\pi(p) \le_{J_\alpha} p\)。由于对于每个 \(\chi < \omega\alpha\)，\(\chi \in X\)，我们有 \(\pi\beta = \alpha\) 且对于每个 \(\gamma < \omega\alpha\)，\(\pi(\gamma) = \gamma\)。因此 \(\pi^{-1} : (J_\alpha, \in) \xrightarrow{\Sigma_1} (J_\alpha, \in)\) 且 \(\pi^{-1}(f_0) = f_0\)。所以 \(f_0\) 也由 \((J_\alpha, \in)\) 中的 \(\pi(p)\) 定义。根据对 \(p\) 的假设，\(p \le_{J_\alpha} \pi(p)\) 从而 \(p = \pi(p)\)。那么对于任何 \(x \in X\)，存在 \(i < \omega\) 和 \(\gamma < \omega\alpha\) 使得 \(x = h_\alpha(i, \langle \gamma, p \rangle) = h_\alpha(\pi(i), \langle \pi(\gamma), \pi(p) \rangle) = \pi(x)\)，这蕴含 \(X = J_\alpha\)。注意 \(h_\alpha\) 不一定是全函数。令 \(\varphi(u, i, v, w, s)\) 为一个 \(\Sigma_0\)-公式，使得 \(h_\alpha(i, \gamma, p) = x\) 当且仅当 \((J_\alpha, \in) \models (\exists y)\varphi(i, \gamma, p, x, y)\)。然后由命题 3.3.11 的证明，存在一个全 \(\Sigma_1\)-函数 \(h'(i, \gamma_1, \gamma_2) = \begin{cases} x & (J_\alpha, \in) \models (\exists n \in \omega)(\exists y \in J_\omega \cup S^{(\alpha)}(J_\rho))\varphi(i, \gamma_1, p, \gamma_2, y), \\ 0 & \text{Otherwise.} \end{cases}\) 令 \(h(\gamma) = h'(f_1(\gamma))\) 对 \(\gamma < \omega\alpha\)。

应用命题 3.4.3，我们有：

**命题 3.4.4.** \(\alpha\) 是可接受的当且仅当不存在将 \(\alpha\) 映射到 \(\omega\alpha\) 上的 \(\Sigma_1(J_\alpha)\)-可定义函数。

下一个引理是 \(\rho_\alpha^1\) 的一个刻画。

**引理 3.4.5.** 假设 \(\alpha > 0\) 且 \(\rho = \rho_\alpha^1\)。那么对于任何 \(\gamma < \rho\) 和任何 \(\Sigma_1(J_\alpha)\)-可定义的 \(A \subseteq J_\gamma\)，有 \(A \in J_\rho\)。

**证明.** 如果 \(\rho = 1\)，则结论立即成立。假设 \(\rho > 1\)。那么 \(\rho\) 是极限序数。令 \(\gamma < \rho\) 且 \(A \subseteq J_\gamma\)。令 \(h_\alpha\) 为 \(J_\alpha\) 的规范 \(\Sigma_1\)-Skolem 函数。固定 \(p \in J_\alpha\) 使得 \(A\) 是带参数 \(p\) 的 \(\Sigma_1(J_\alpha)\)-可定义的。令 \(X = h_\alpha(\omega \times \{p\})\)。那么 \((X, \in) \prec_\Sigma (J_\alpha, \in)\)。由定理 3.3.7，存在 \(\beta \le \rho\) 使得 \(\pi : (X, \in) \cong (J_\beta, \in)\) 是同构。注意对于所有 \(x \in J_\gamma\)，\(\pi(x) = x\)，因为 \(\gamma\) 是传递的。因此对于所有 \(x \in A\)，\(\pi(x) = x\)。所以 \(A\) 也是带参数 \(\pi(p) \in J_\beta\) 在 \(J_\rho\) 中的 \(\Sigma_1\)-可定义的。我们声称 \(\beta < \rho\)。否则，令 \(f\) 为将 \(J_\rho\) 的一个子集映射到 \(J_\alpha\) 上的 \(\Sigma_1(J_\alpha)\) 函数。那么 \(f \circ \pi \circ h_\alpha\) 是 \(\Sigma_1(J_\alpha)\) 且将 \(\omega \times (J_\gamma \times \{p\})\) 的一个子集映射到 \(J_\alpha\) 上。但是 \(\omega \times J_\gamma \times \{p\} \in J_{\gamma+2} \subseteq J_\rho\)，因此它将 \(J_{\gamma+2}\) 的一个子集映射到 \(J_\alpha\) 上，这与 \(\rho\) 的选择矛盾。

**引理 3.4.6.** 设 \(\alpha > 0\) 且 \(\rho = \rho_\alpha^+\)。那么存在一个 \(A \subseteq J_\rho\)，它是 \(\Sigma_1(J_\alpha)\)-可定义的且 \(A \notin J_\alpha\)。

**证明.** 令 \(f\) 为将 \(J_\rho\) 的一个子集映射到 \(J_\alpha\) 上的 \(\Sigma_1(J_\alpha)\)-可定义函数。那么 \(f\) 限制在 \(J_\rho\) 上的定义域是 \(\Sigma_1(J_\alpha)\) 且不是 \(J_\alpha\) 的元素，由可接受性。

引理 3.4.5 和引理 3.4.6 得出 \(\rho_\alpha^+\) 的以下刻画：

**定理 3.4.7.** 设 \(\alpha > 0\)。那么 \(\rho_\alpha^+\) 是使得存在一个 \(\Sigma_1(J_\alpha)\) 集合 \(A \subseteq J_\rho\) 且 \(A \notin J_\alpha\) 的最小序数 \(\rho\)。

现在假设 \(x \subseteq \omega\) 是带参数 \(p\) 的 \(\Sigma_1(J_\alpha)\)-可定义的且 \(x \notin J_\alpha\)。令 \(X = h_\alpha(\omega \times \{p\})\)。我们可以将 \(\omega \times J_1\) 识别为 \(J_1\)。因此 \(X = H(1 \times \{p\})\) 对于某个 \(\Sigma_1\)-函数 \(H\)。那么 \((X, \in) \prec_\Sigma (J_\alpha, \in)\)。由传递坍缩，存在 \(\beta \le \alpha\) 使得 \(\pi : (X, \in) \cong (J_\beta, \in)\)。由于 \(x \subseteq J_1\)，对于所有 \(n \in \omega\)，\(\pi(n) = n\)。因此 \(x\) 是带参数 \(\pi(p)\) 的 \(\Sigma_1(J_\beta)\)-可定义的。如果 \(\beta < \alpha\)，那么 \(x \in J_\alpha\)，这产生矛盾。因此 \(\beta = \alpha\)。现在 \(\pi\) 是 \(\Sigma_1(J_\alpha)\)-可定义的，所以 \(\pi \circ h\) 是 \(\Sigma_1(J_\alpha)\)-可定义的且将一个集合 \(y \subseteq J_1\) 映射到 \(J_\alpha\) 上。由于 \(J_1 \simeq \text{HF}\)，由命题 3.2.6，我们可以假设 \(y\) 是一个实数。因此对于任何可接受的 \(\alpha\)，如果 \(J_{\alpha+1} \backslash J_\alpha\) 包含一个 \(\Sigma_1(J_\alpha)\)-可定义的实数，那么它包含一个实数 "coding \(J_\alpha\)"。

**注释 3.4.8.** 定理 3.4.7 对于 \(n \ge 1\) 依然成立。然而，证明需要的不仅仅是对上述内容的直接推广。主要困难在于对于 \(n \ge 2\) 不存在规范的 \(\Sigma_n\)-Skolem 函数。为了克服这一困难，引入了对 \(J_\alpha\) 的更精细分析。详情见 Jensen [55]。

#### 3.4.2 主代码

**定义 3.4.9.** 给定一个序数 \(\alpha\) 和 \(n \ge 0\)，\(J_\alpha\) 的一个 \(\Sigma_n\)-master code 是一个 \(\Sigma_n(J_\alpha)\)-可定义集合 \(A \subseteq J_\rho\)，使得对于任何 \(m \ge 1\)，任何 \(\Sigma_{n+m}(J_\alpha)\)-可定义的集合 \(B \subseteq J_\rho\) 在 \((J_\rho, \in, A)\) 中是 \(\Sigma_m\)-可定义的。

在递归论的背景下，主代码的概念有一种诠释。首先假设 \(\alpha = 1\) 并且因此 \(\rho_1^1 = 1\)。那么 \(J_\alpha = J_\rho = \text{HF}\)。令 \(A \subseteq \text{HF}\) 为一个 \(\Sigma_1\)-master code。由命题 3.2.6，存在一个实数 \(x\) 使得 \(x\) 在



(HF, \(\epsilon\), A) 和 A 是 (HF, \(\epsilon\), x) 中 \(\Delta_1\)-可定义的。由定理 3.2.5，(HF, \(\epsilon\), x) 中每个 \(\Sigma_1\)-可定义实是在 x 中递归可枚举的。因此，(HF, \(\epsilon\)) 中每个 \(\Sigma_2\)-可定义实是 (HF, \(\epsilon\), A) 中 \(\Sigma_1\)-可定义的，并且也是在 x 中递归可枚举的。因此，\(\Sigma_1\)-主码正是那些递归可枚举且完备的实数（因此与 \(\emptyset'\) 图灵等价）。一般来说，在 \(\langle J_1, \epsilon \rangle\) 中是 \(\Sigma_n\)-主码的实数是 \(\Sigma_n\)-完备的，因此与 \(\emptyset^{(n)}\) 图灵等价。我们可以因此将主码视为集合论意义上的图灵跳跃。其次，假设 \(\rho_2^\alpha = 1\)。\(\langle J_\alpha, \epsilon \rangle\) 的一个 \(\Sigma_1\)-主码是一个集合 \(A \in HF\)，使得每个 \(\Sigma_2(J_\alpha)\)-可定义实是 (HF, \(\epsilon\), A) 中 \(\Sigma_1\) 的。再次由命题 3.2.6 和定理 3.2.5，每个 \(\Sigma_2(J_\alpha)\)-可定义实是在某个 \(\Sigma_1(J_\alpha)\)-可定义实 x 中递归可枚举的。特别是，每个实 \(x \in J_\alpha\) 在 x 中是递归的。因此，如果 \(\alpha\) 远大于 \(\rho_2^\alpha\)，则实 x 在计算能力上必须非常强大。历史上，\(\rho = 1\) 的主码概念最初由 Boolos 和 Putnam [8] 引入，当时他们研究了可构造宇宙中实数的图灵度。我们现在表明，对于任何可接受序数 \(\alpha\)，\(\Sigma_1\)-主码都存在。

### 定理 3.4.10. 设 \(\alpha > 0\)。存在 \(\langle J_\alpha, \epsilon \rangle\) 的一个 \(\Sigma_1\)-主码，即一个 \(\Sigma_1(J_\alpha)\)-可定义的 \(A \subseteq J_{\rho_\alpha^\alpha}\)，使得对于任何 \(B \in J_{\rho_\alpha^\alpha}\)，如果 \(B\) 是 \(\Sigma_{m+1}(J_\alpha)\)-可定义的，那么它在 \(\langle J_{\rho_\alpha^\alpha}, \epsilon, A \rangle\) 中是 \(\Sigma_m\)-可定义的。

证明。为简化起见，我们只证明 m = 1 的情况。假设 \(f\) 是带参数 p 的 \(\Sigma_1(J_\alpha)\)-可定义的，将 \(\rho_2^\alpha\) 的一个子集映射到 \(\alpha\) 上。修正带参数 p 的 \(\Sigma_1\)-公式的一个 \(\Delta_1\)-枚举 \(\langle \varphi_i(x, p) \rangle_{i < \omega}\)。令
\[
A = \{\langle i, x \rangle \mid i < \omega \land x \in J_{\rho_\alpha^\alpha} \land \langle J_\alpha, \epsilon \rangle \models \varphi_i(x, p)\}.
\]

显然，A 在 \(\langle J_\alpha, \epsilon \rangle\) 上是 \(\Sigma_1\)-可定义的。现在假设 \(B \in J_{\rho_\alpha^\alpha}\) 在 \(\langle J_\alpha, \epsilon \rangle\) 上是 \(\Sigma_2\)-可定义的。那么存在一个 \(\Sigma_1(J_\alpha)\)-公式 \(\varphi(u, v, w)\)，使得
\[
x \in B \Leftrightarrow \langle J_\alpha, \epsilon \rangle \models (\exists y) \neg \varphi(x, u, v, s),
\]

其中 s 是 \(J_\alpha\) 中的一个参数。由于 f 是满射，存在 \(s_0 \in J_{\rho_\alpha^\alpha}\) 使得 \(f(s_0) = s\)。则
\[
x \in B \Leftrightarrow (\exists y \in J_{\rho_\alpha^\alpha})(\langle J_\alpha, \epsilon \rangle \models \neg \varphi(x, f(y), f(s_0))).
\]

由于 f 是带参数 p 的 \(\Sigma_1(J_\alpha)\)-可定义的，存在一个索引 i，使得对 x, y \(\in J_{\rho_\alpha^\alpha}\)，
\[
\langle J_\alpha, \epsilon \rangle \models \neg \varphi(x, y, s_0, p) \Leftrightarrow \langle J_\alpha, \epsilon \rangle \models \neg \varphi(x, f(y), f(s_0)).
\]

因此
\[
x \in B \Leftrightarrow (\exists y \in J_{\rho_\alpha^\alpha})((i, x, y, s_0) \notin A \Leftrightarrow (\exists y)((i, x, y, s_0)) \notin A).
\]
故 B 在 \(\langle J_{\rho_\alpha^\alpha}, \epsilon, A \rangle\) 上是 \(\Sigma_1\)-可定义的。\(\square\)

例如，\(0'\) 是一个 \(\Sigma_1(J_1)\)-主码，因为它满足定理 3.4.10 中描述的性质。Jensen [55] 证明了以下一般结果：

### 定理 3.4.11. 对于任何序数 \(\alpha > 0\) 和 \(n > 0\)，存在一个 \(\Sigma_n(J_\alpha)\)-主码 \(A \subset J_{\rho^p_\alpha}\)。而且，\(\rho^p_\alpha\) 是最小的序数 \(\gamma\)，使得存在一个不在 \(J_\alpha\) 中的 \(\Sigma_n(J_\alpha) A \subseteq \omega \gamma\)。

\(\Sigma_n\)-主码在递归理论中对应于 \(0^{(\alpha n)}\)。等式 \(0^{(\alpha n+m)} = (0^{(\alpha n)})^{(m)}\) 在精细结构理论中有一个自然的类比。详情见 [55]。

### 3.4.3 练习

- **练习 3.4.1.** 证明引理 3.4.2。

- **练习 3.4.2.** 证明命题 3.4.4。

- **练习 3.4.3.** 证明存在一个可数可接受序数 \(\alpha > \omega\)，使得 \(\rho^1_\alpha = \alpha\)。

## 3.5 \(\omega\)-模型

#### 定义 3.5.1. 一个结构 \(\mathfrak{M}\) 是 \(\omega\)-模型，如果 \(\omega^\mathfrak{M} = \omega\)。

\(\omega\)-模型在递归理论和描述性集合论中被广泛使用。\(\omega\)-模型中一个主要关注点是其标准部分。

### 定义 3.5.2. 设 \(\mathfrak{M} = \langle M, E \rangle\) 为一个结构，且 \(M_1 \subseteq M\)。如果对于每个 \(x \in M_1\)，\(yEx\) 且 \(y \in M\) 蕴含 \(y \in M_1\)，则称 \(M_1\) 是 \(E\)-闭的。\(\mathfrak{M}\) 的标准部分是 \(M\) 中极大的 \(E\)-闭良好基子集。

显然，如果 \(M_1 \subseteq M\) 是 \(E\)-闭的，那么对于任何 \(\Sigma_0\)-公式 \(\varphi(v)\) 和 \(x \in M_1\)，\(\langle M, E \rangle \models \varphi(x)\) 当且仅当 \(\langle M_1, E \rangle \models \varphi(x)\)。

### 引理 3.5.3. 假设 \(\mathfrak{M} \models \text{KP}\)。那么 \(x\) 属于 \(M\) 的标准部分，当且仅当 \(\text{rk}(x)\)（即 \(x\) 的秩）属于 \(\mathfrak{M}\) 的标准部分。

**证明。** 由于 \(\mathfrak{M} \models \text{KP}\)，根据 \(\Sigma\)-归纳定理（3.1.8），秩函数 rk 是 \(\Delta_1\)-可定义的。

如果 \(x\) 属于 \(M\) 的标准部分，那么通过对 \(x\) 的秩进行归纳，可以直接验证 rk\((x)\) 也属于标准部分。

如果 \(x\) 不属于 \(M\) 的标准部分，那么在 \(M\) 中存在一个下降序列 \(\langle x_n \rangle_{n < \omega}\)，使得对每个 \(n\) 都有 \(x_{n+1} E x_n\)，且对每个 \(n\) 都有 \(x_0 \text{rk}(x_n) \text{Erk}(x_n)\)，并且 \(\text{rk}(x_0) \text{Erk}(x)\) 也不属于 \(M\) 的标准部分。

### 引理 3.5.4. 假设 \(\mathfrak{M} \models \text{KP}\) 且 \(M_1 \subseteq M\) 是 \(M\) 的标准部分。那么 \(\langle M_1, E \rangle \models \text{KP}\)。

**证明。** 由于 \(M_1 \subseteq M\) 是 \(E\)-闭的，外延公理在 \(\mathfrak{M}_1 = \langle M_1, E \rangle\) 中成立。\(\mathfrak{M}_1\) 满足基础公理，因为 \(M_1\) 是 \(M\) 的标准部分。同样，可以直接验证配对、并集和 \(\Delta_0\)-理解公理在 \(\mathcal{M}_1\) 中成立。我们证明 \(\mathcal{M}_1 \models \Delta_0\)-收集。

假设 \(\varphi(u, v)\) 是一个 \(\Delta_0\)-公式，且 \(a \in M_1\) 使得

\(\langle M_1, E \rangle \models (\forall x Ea)(\exists y)\varphi(x, y).\)

由于 \(\varphi(u, v)\) 是 \(\Delta_0\) 且 \(M_1\) 是 M 的 E-闭子集，我们有

\(\langle M, E \rangle \models (\forall x Ea)(\exists y)\varphi(x, y).\)

现在 \(\langle M, E \rangle \models \text{KP}\) 意味着存在 \(b \in M\) 使得

\(\langle M, E \rangle \models (\forall x Ea)(\exists y E b)\varphi(x, y).\)

由引理 3.5.3，存在 \(b_0\) 使得 \(\text{rk}(b_0) = a_0\) 是 \(\mathcal{M}\) 中满足 \(\varphi\) 的收集公理的最小序数。如果 \(a_0 \in M_1\)，则由引理 3.5.3，\(b_0 \in M_1\)，证毕。否则，\(a_0 \in M \setminus M_1\)。但此时存在一个非标准的 \(a_1 E a_0\)，使得对每个 \(x E a\)，存在 \(M_1\) 中的 \(y E b_0\)，使得 \(\text{rk}(y) E a_1\) 且 \(\langle M, E \rangle \models \varphi(x, y)\)。注意 \(\varphi(x, y) \land \text{rk}(y) E a_1\) 是一个 \(\Sigma\)-公式，且

\(\langle M, E \rangle \models (\forall x Ea)(\exists y)(\varphi(x, y) \land \text{rk}(y) E a_1).\)

由 \(\Sigma\)-收集定理（3.1.6），存在 \(b_1 \in M\) 使得

\(\langle M, E \rangle \models (\forall x Ea)(\exists y E b_1)(\varphi(x, y) \land \text{rk}(y) E a_1).\)

定义

\(c = [y \mid y E b_1 \land \langle M, E \rangle \models \text{rk}(y) E a_1 \land \exists x E a (\varphi(x, y))].\)

由定理 3.1.6，\(c \in M\)。

那么 \(\text{rk}(c) E a_0\) 且 \(a_0 = \text{rk}(b_0)\)。由于 \(a_0\) 是 \(\mathcal{M}\) 中满足 \(\varphi\) 的收集公理的最小序数，我们得到矛盾。\(\square\)

### 命题 3.5.5. 设 \(\mathcal{M} \models \text{KP}\) 是一个 \(\omega\)-模型。那么 \(L_{\omega_1^{CK}} \in M\)。

证明。设 \(M_1 \le M\) 为 M 的标准部分。由引理 3.5.4，\(\langle M_1, E \rangle \models \text{KP}\)。因此 \(\langle M_1, E \rangle\) 也是 KP 的一个 \(\omega\)-模型。由于 \(\omega_1^u(u) \in M_1\)，由 \(\Delta_0\)-分离，每个递归集合都属于 \(\langle M_1, E \rangle\)。由 \(\Sigma\)-归纳，\(\omega_1^{CK} \in M_1\)。设 \(\pi : \langle M_1, E \rangle \to \langle N, \in \rangle\) 为坍塌映射。那么 \(\langle N, \in \rangle\) 是可接受的，因此 \(\omega_1^{CK} \le N\)。由定理 3.3.4，\(L_{\omega_1^{CK}} \in N\)。我们通过对 \(\beta < \omega_1^{CK}\) 进行归纳来证明 \(\pi^{-1} L_{\omega_1^{CK}}\) 是恒等映射。

注意，由命题 3.3.3 存在一个 \(\Delta_1\)-公式 \(\varphi(u, v)\)，使得对任何序数 \(\beta < \omega_1^{CK}\)，\(\langle N, \in \rangle \models \varphi(\beta, x)\) 当且仅当 \(x = J_\beta\)。而且，

\(\langle N, \in \rangle \models \varphi(\beta, J_\beta) \land (\forall x E J_\beta)(\exists y \in \beta)(\forall y)(x \in y \leftrightarrow \varphi(y, y)).\)

我们通过归纳证明，对每个 \(\gamma < \omega_1^{CK}\)，\(\pi^{-1}(J_\gamma) = J_\gamma\)。





由于 \(\omega_1^{CK} \le M_1\)，对于任意 \(\beta < \omega_1^{CK}\)，都有 \(\pi(\beta) = \beta\)。因此对于 \(x \in J_1\)，有 \(\pi(x) = x\)。由于 \((N, \in) \models \phi(1, x)\) 当且仅当 \(x = f_1\)，所以 \((M_1, E) \models \phi(1, x)\) 当且仅当 \(x = f_1\)。故 \(\pi^{-1}(J_1) = J_1\)。

对于后继序数 \(\beta + 1\)，\(\pi\) 显然保留 Gödel 原始递归算子。因此 \(\text{Rang}(\pi^{-1} J_{\beta+1}) = J_{\beta+1}\)。由于 \((N, \in) \models \phi(\beta + 1, x)\) 当且仅当 \(x = J_{\beta+1}\)，所以 \((M_1, E) \models \phi(\beta + 1, x)\) 当且仅当 \(x = J_{\beta+1}\)。故 \(\pi^{-1}(J_{\beta+1}) = J_{\beta+1}\)。

现在假设 \(\beta < \omega_1^{CK}\) 是极限序数。通过归纳，若 \(\gamma < \beta\)，则 \((M_1, E) \models \phi(\gamma, x)\) 当且仅当 \(x = J_\gamma\)。令 \(z = \pi^{-1}(J_\beta)\)。由于 \(\pi^{-1}(\beta) = \beta\)，我们有

\((M_1, E) \models \phi(\beta, z) \wedge (\forall x Ez)(\exists y Ey)(\exists y Xy) \wedge \phi(\gamma, y).\)

因此 \(z = J_\beta\)。由 \(J_{\omega_1^{CK}}\) 的传递性，可得出 \(\pi^{-1} \restriction L_{\omega_1^{CK}}\) 是恒等映射，从而 \(L_{\omega_1^{CK}} \in M\)。

### 3.5.1 习题

习题 3.5.1. 证明，若 \((M, E) \models KP\) 是一个非标准 \(\omega\)-模型，则对于任意非标准序数 \(\alpha \in M\)，存在一个集合 \(A \subseteq \beta \mid (M, E) \models \beta E \alpha)\)，使得 \((Q, <)\) 与 \((A, E)\) 同构，其中 \(Q\) 是有理数集。

## 3.6 结构编码

#### 3.6.1 编码语言

给定一个可数语言 \(\mathscr{L}\)，有许多方法可以用一组数字对其进行编码。我们想要的是一种“良好”的编码方案。在许多情况下，可以用递归集 \(\mathscr{L}' \subseteq \omega\) 对语言 \(\mathscr{L}\) 进行编码。这样可编码的语言称为递归语言。例如，算术的一阶语言和 Zermelo–Fraenkel 集合论语言都是递归的。此外，在递归语言中，良构公式集和句子集都是递归的。我们可以有效地将每个公式 \(\varphi\) 与其 Gödel 数 \(\ulcorner \varphi \urcorner\) 关联。我们说，理论 \(T\) 是递归的，如果其对应的 Gödel 数集 \(T' = \{ \ulcorner \varphi \urcorner \mid \varphi \in T \}\) 是递归的。本书中考虑的理论，如 KP、ZFC，都是递归的。在 Gödel 数编码下，证明序列被识别为有限数字序列，因此可视为 \(\omega\) 的有限子集。此外，若 \(\mathscr{L}\) 和 \(T\) 均为递归的，则 \(T\) 中的证明集也是递归的。由此可知，\(T\) 的定理句子集是递归可枚举的。

#### 3.6.2 编码结构

给定递归语言 \(\mathscr{L}\)，可以将其与递归集 \(\dot{\mathscr{L}}\) 关联，并用自然数集 \(\omega\) 以及在 \(\omega\) 上定义的 \(\dot{\mathscr{L}}\) 中的关系来对 \(\mathscr{L}\) 中的可数结构进行编码，使得得到的结构与原结构同构。若 \(\mathfrak{M} = (M, R_0, \dots, R_n)\) 是可数的，则 \(\mathfrak{M}\) 的一个编码 \(\ulcorner M \urcorner = (\omega, \dot{R}_0, \dots, \dot{R}_n)\) 是满足 \(\mathfrak{M} \cong \dot{\mathfrak{M}}\) 的结构。若所有关系 \(R_0, \dots, R_n\) 都是递归的，则称结构 \(\ulcorner M \urcorner\) 为递归的。然而，递归结构非常少。

令 \(\mathscr{L}\) 为递归语言，\(\mathfrak{M}\) 为由 \(\ulcorner \mathfrak{M} \urcorner\) 编码的结构。对于 \(\dot{\mathscr{L}}\) 中与 \(\mathscr{L}\) 中公式 \(\varphi(u)\) 对应的公式 \(\dot{\varphi}(u)\)，我们可以计算集合 \(A = \{m \in \omega \mid \ulcorner m \urcorner \vDash \dot{\varphi}(m)\}\) 的复杂度。计算复杂度的步骤如下：递归地解码 \(\dot{\varphi}(u)\) 以得到公式 \(\varphi(u)\)。然后 \(A\) 的复杂度即为 \(\varphi(u)\) 的复杂度。例如，假设 \(\mathscr{L}\) 是集合论语言，且 \(\dot{\varphi}(u)\) 对应公式 \(\varphi(w): (\forall u)(\forall v)(u \in v \land v \in w \rightarrow u \in w)\)（“$w$ 是传递的”）。则集合

\(\{m \mid (\omega, \dot{\in}) \vDash (\forall i)(\forall j)(i \dot{\in} j \land j \dot{\in} m \rightarrow i \dot{\in} m)\}\)

是 \(\Pi_1(\dot{\in})\)。

一般而言，给定带有关系符号 \(R_0, \dots, R_n\) 的语言 \(\mathscr{L}\)、一个结构以及公式 \(\varphi \in \mathscr{L}\)，集合 \(\{m \in \omega \mid \ulcorner M \urcorner \vDash \varphi(m)\}\) 在 \(\dot{R}_0 \oplus \cdots \oplus \dot{R}_n\) 中是算术的。此外，这种编码是一致的。因此，若 \(\{\varphi_i\}_{i < \omega}\) 是递归的，则集合 \(\{(i, m) \mid \ulcorner M \urcorner \vDash \dot{\varphi}_i(m)\}\) 可通过索引为 \(e\) 的算法在 \((\dot{R}_0 \oplus \cdots \oplus \dot{R}_n)^{(\omega)}\) 中 Turing 可计算。特别是，存在一个 \(e\)，使得若 \(\{\varphi_i\}_{i < \omega}\) 是句子的递归集，则 \(\ulcorner M \urcorner \vDash \dot{\varphi}_i\) 当且仅当 \(\dot{\varphi}_e^{(R_0 \oplus \cdots \oplus R_n)^{(i)}}(i) = 1\)。作为结果，我们有以下结论：

### **命题 3.6.1.**

给定递归理论 \(T\)，集合 \(\{\ulcorner M \urcorner \mid \forall \varphi(\varphi \in T \rightarrow \ulcorner M \urcorner \vDash \varphi)\}\) 是 \(\Delta_1^1\)。

例如，\(\{\ulcorner M \urcorner \mid \ulcorner M \urcorner \vDash \text{KP} + \text{"V = L"}\}\) 是 \(\Delta_1^1\)（为简单起见，此处不区分 KP+V = L 及其在 \(\ulcorner M \urcorner\) 中解释的对应句子）。

### 3.6.3 编码 \(\omega\)- 模型和良基模型

我们现在使用集合论语言，并用 "\(E\)" 代替符号 \(\dot{\in}\)。当然，集合论的最佳模型是那些良基模型。

### **命题 3.6.2.**

\(\langle E \mid (\omega, E) \text{ 编码一个良基模型} \rangle\) 是 \(\Pi_1^1\)。

证明。\((\omega, E)\) 编码一个良基模型，当且仅当不存在函数 \(f : \omega \to \omega\)，使得对于任意对 \((i, j)\)，\(i < j\) 当且仅当 \((\omega, E) \models f(j)Ef(i)\)。\(\square\)

编码良基模型是一件复杂的事情，尽管这类模型是集合论的“真正模型”。次佳选择是编码 \(\omega\)-模型。研究 \(\omega\)-模型的原因在于，在考虑此类模型中的实数或实数集时，可以确保所涉及的“自然数”是标准数。

### **命题 3.6.3.**

\(\{E \mid (\omega, E) \text{ 编码一个 } \omega\text{-模型}\}\) 是 \(\Delta^1_1\)。

证明。\((\omega, E)\) 编码一个 \(\omega\)-模型，当且仅当存在 \(m \in \omega\) 和单射 \(f : \omega \to \omega\)，使得

- (i) \((\omega, E) \models \text{‘}m \text{ 是一个无限序数’}\)；
- (ii) \(f\) 是 \(\omega\) 与 \([k \mid kEm]\) 之间的双射；且
- (iii) 对于任意对 \((i, j)\)，\(i < j\) 当且仅当 \((\omega, E) \models f(i)Ef(j) \land f(j)Em\)。

因此集合 \(\{E \mid (\omega, E) \text{ 是一个 } \omega\text{-模型}\}\) 是 \(\Sigma^1_1\)。

另一方面，\((\omega, E)\) 编码一个 \(\omega\)-模型，当且仅当存在 \(m \in \omega\)，使得

- (iv) \((\omega, E) \models \text{‘}m \text{ 是一个无限序数’}\)；
- (v) 对于从 \(\omega\) 到 \([k \mid kEm]\) 的每个单射 \(f\)，存在一对 \((i, j)\)，使得 \(i < j\) 且 \((\omega, E) \models f(i)Ef(j)\)；且
- (vi) 对于从 \(\omega\) 到 \([k \mid kEm]\) 的每个保序函数 \(f\) 以及任意满足 \((\omega, E) \models kEm\) 的 \(k\)，存在一个 \(j\)，使得 \((\omega, E) \models kEf(j)\)。

因此 \(\{E \mid (\omega, E) \text{ 是一个 } \omega\text{-模型}\}\) 也是 \(\Pi^1_1\)，故为 \(\Delta^1_1\)。\(\square\)

### **命题 3.6.4.**

- (i) 集合 \(\langle \omega, \omega_E, \emptyset \rangle = \langle \langle n, n_E \rangle \mid n_E \text{ 在 } \ulcorner \mathcal{M} \urcorner \text{ 中编码 } n \rangle\) 是算术的；
- (ii) 假设 \(\ulcorner \mathcal{M} \urcorner = \langle \omega, E \rangle\) 编码一个 \(\omega\)-模型 M。则对于任意实数 \(x \in \mathcal{M}\)，\(x\) 在 E 中是算术的；
- (iii) 若 \(m\) 在 \(\ulcorner \mathcal{M} \urcorner\) 中编码 \(w\)，且 \(f : \omega \to [k \mid k \in \ulcorner \mathcal{M} \urcorner]\) 是保序双射，则每个实数 \(x \in \mathcal{M}\) 在 \(f \oplus E\) 中是递归的。

证明。(i) \(\langle n, m, E \rangle \in \langle \omega, \omega_E, \emptyset \rangle\) 当且仅当存在有限序列 \(\langle k_j \rangle_{j \in \mathbb{Z}^n}\)，使得

- \(k_n = m \cap \ulcorner \mathcal{M} \urcorner\)；
- 对于任意 \(j < n\)，\(\ulcorner \mathcal{M} \urcorner \models k_j E k_{j+1} \land (\forall k) (k E k_{j+1} \to k E k_j \lor k = k_j)\)；且
- 对于所有 \(j < n\)，\(\ulcorner \mathcal{M} \urcorner \models k E k_j\)。

故 \((\omega, \omega_E, E)\) 是算术的。

(ii) 给定 \(x \in \mathcal{M}\)，在 \(\ulcorner \mathcal{M} \urcorner\) 中对 \(x\) 进行编码。则对于任意 \(n\)，\(n \in x\) 当且仅当 \((n, n_E) \in \langle \omega, \omega_E, \emptyset \rangle\) 且 \(\ulcorner \mathcal{M} \urcorner \models n_E E m\)。因此 \(x\) 在 E 中是算术的。

(iii) 对于 \(x \in \mathcal{M}\)，令 \(n\) 在 \(\ulcorner \mathcal{M} \urcorner\) 中编码 \(x\)。则对于任意 \(i\)，\(i \in x\) 当且仅当 \(\ulcorner \mathcal{M} \urcorner \models f(i) E n\)，故 \(x \le_T E \oplus f\)。





根据命题 3.6.4 的 (iii)，如果 $f$ 是递归的，那么 $\mathfrak{M}$ 中的每个实数在 $E$ 中都是递归的。如果存在这样的递归 $f$，我们说 $\langle \omega, E \rangle$ 是一个良好编码的 $\omega$-模型。

**命题 3.6.5.** 如果 $\langle \omega, E \rangle$ 编码了一个 $\omega$-模型，那么存在一个良好编码的 $\omega$-模型 $\langle \omega, E_0 \rangle \equiv \langle \omega, E \rangle$。而且，集合 $E \mid \{ \langle \alpha, E \rangle \text{ 是一个良好编码的 } \omega\text{-模型} \}$ 是 $\Delta^1_1$。

证明。假设 $\langle \omega, E \rangle$ 编码了一个 $\omega$-模型，且 $m$ 在 $\langle \omega, E \rangle$ 中编码了 $\omega$。不失一般性，我们可以假设 $\{ k \mid \langle k, E \rangle \in K m \}$ 是无限的。设 $f : \omega \to \{ k \mid \langle \omega, E \rangle \equiv k E m \}$ 为序保持双射。设 $g : \omega \to \omega$ 为任意双射，使得对每个 $n$ 都有 $g(2n) = f(n)$。现在定义 $j E_0 i$ 当且仅当 $g(i) E g(j)$。那么 $g : \langle \omega, E \rangle \equiv \langle \omega, E_0 \rangle$。显然，$n E_0^{CK} 1(m)$ 当且仅当 $n$ 是偶数。设 $h(n) = 2n$。那么 $h$ 是递归的，且 $h : \omega \to \{ i \mid \langle \omega, E_0 \rangle \equiv i E_0^{CK} 1(m) \}$ 是序保持双射。因此 $\langle \omega, E_0 \rangle$ 是一个良好编码的 $\omega$-模型。

我们将命题 3.6.5 第二部分的证明留给读者。

从以上可以看出，假设一个 $\omega$-模型 $\langle \omega, E \rangle$ 总是良好编码的是无害的。

### 3.6.4 第二个最小可接受序数

之前结果的一个应用得出

**引理 3.6.6.** $\omega_1^{CK}$ 是第二个最小可接受序数。

证明。设 $\alpha$ 为第二个最小可接受序数。根据命题 3.3.12，$\alpha \ge \omega_1^{CK}$。设 $\mathscr{X} = \{ E \mid \langle \omega, E \rangle \text{ 良好编码了一个 KP 的 } \omega\text{-模型} \}$。根据命题 3.6.5，$\mathscr{X}$ 是一个 $\Delta^1_1$-集。根据甘地基定理 (2.5.3)，存在一个 $E \in \mathscr{X}$ 使得 $\omega_1^E = \omega_1^{CK}$。设 $\langle M_1, \in \rangle$ 为由 $\langle \omega, E \rangle$ 编码的 $\omega$-模型，$M_1$ 为其标准部分。根据引理 3.5.4，$\langle M_1, \in \rangle \models \text{KP}$。我们声称，对于任何 $\beta \in M_1$，都有 $\beta < \omega_1^{CK}$。假设此为假。设 $m \in \omega$ 为一个在 $\langle \omega, E \rangle$ 中编码 $\omega_1^{CK}$ 的实数。那么集合

$\{ \langle i, j \rangle \mid \langle \omega, E \rangle \models i E j \land j E m \}$

是一个 $E$-递归的良序，序类型为 $\omega_1^{CK}$，这与 $\omega_1^E = \omega_1^{CK}$ 矛盾。因此 $o(M_1) = \omega_1^{CK}$，故 $\alpha = \omega_1^{CK}$。因此 $\omega_1^{CK}$ 是第二个最小可接受序数。

根据定理 3.3.6 和引理 3.6.6，我们有

**推论 3.6.7.** $L_{\omega_1^{CK}}$ 是可接受的。

**定理 3.6.8.** 一个实数 $x$ 是高算实数，当且仅当 $x \in L_{\omega_1^{CK}}$。

证明。要证明每个高算实数都属于 $L_{\omega_1^{CK}}$，只需证明对于任何 $n \in \omega$，$H_n \in L_{\omega_1^{CK}}$。根据命题 2.1.5，$H_n$ 可图灵归约到某个 $\Pi^0_1$-单点 $f_n \in \omega^\omega$。因此，只需证明 $f_n \in L_{\omega_1^{CK}}$。

由于 $f_n$ 是一个 $\Pi^0_1$-单点，存在一个递归树 $T_n$，使得 $f_n$ 是 $T$ 中唯一的无限路径。那么对于每个 $m \in \omega$ 和 $\sigma \in \omega^{<\omega} \setminus \{ f_n \mid m \}$，$T_\sigma = \{ \tau \in T_n \mid \tau > \sigma \}$ 是良基的。由于 $L^K_{\omega_1^{CK}}$ 是可接受的，存在一个在 $L^K_{\omega_1^{CK}}$ 中的 $h_\sigma : T_\sigma \to \omega_1^{CK}$，使得对 $T_\sigma$ 中任何 $r_1 >_T r_0$，都有 $h_\sigma(r_1) < h_\sigma(r_0)$。因此存在一个 $\beta_\sigma \in \omega_1^{CK}$ 使得 $h_\sigma \in L_{\beta_\sigma}$。由于 $\omega_1^{CK} \setminus f_n \mid m \in L_{\alpha_\beta}$，根据定理 3.3.2 和 $\Sigma$-收集定理 (3.1.6)，存在一个 $\beta^m < \omega_1^{CK}$ 使得对所有 $\sigma \in \omega^m \setminus f_n \mid m$ 都有 $\beta_\sigma < \beta_m$。再次根据定理 3.1.6，存在一个 $\beta < \omega_1^{CK}$ 作为所有 $\beta_m$ 的上界。那么 $\sigma < f_n$ 当且仅当

$\langle L_\beta, \in \rangle \models (\forall \tau \in \omega^{<\omega})(\exists \beta)(\exists \gamma)(\forall r_1, r_2 \in T_\sigma)(h : T_\tau \to \gamma \wedge r_2 >_T r_1 \to h(r_2) < h(r_1)).$

因此 $f_n \in L_{\beta+1} \subset L^K_{\omega_1^{CK}}$。

假设 $x \in L^K_{\omega_1^{CK}}$。由于 $L^K_{\omega_1^{CK}}$ 是可接受的，我们有 $\omega_1^x = \omega_1^{CK}$。假设 $x$ 不是高算的。定义

$\mathscr{X} = \{E \mid \langle \omega, E \rangle \text{ 良好编码了一个 KP 的 } \omega\text{-模型}\}.$

根据命题 3.6.5，$\mathscr{X}$ 是一个 $\Delta^1_1$-集。根据克莱斯尔基定理 (2.5.6)，存在一个 $E_0 \in \mathscr{X}$，使得 $\omega_1^{E_0} = \omega_1^{CK}$ 且 $x \notin E_0$。设 $\langle M, \in \rangle$ 为由 $\langle \omega, E_0 \rangle$ 编码的 $\omega$-模型，并设 $M_1$ 为 $M$ 的标准部分。那么每个 $z \in M_1$ 的实数在 $E_0$ 中都是递归的。因此 $x \notin M_1$。根据命题 3.5.5，$L^K_{\omega_1^x} \subset M_1$。因此 $x \notin L^K_{\omega_1^x}$。

这给出了高算实数集的模型论刻画：

**推论 3.6.9.** 一个实数 $x$ 是高算的，当且仅当它属于 KP 的每个 $\omega$-模型。

**证明。** 根据定理 3.6.8，$x$ 是高算的，当且仅当 $x \in L^K_{\omega_1^x}$。根据定理 3.5.5 和推论 3.6.7，$x \in L^K_{\omega_1^x}$ 当且仅当 $x$ 属于 KP 的每个 $\omega$-模型。

### 3.6.5 再论 Cantor-Bendixson 构造

我们现在回到定理 1.1.10 的递归论证明，并计算使得 $T_{\gamma+1} = T_\gamma$ 的最小序数 $\gamma$。

**命题 3.6.10.** 假设 $T \subset \omega^{<\omega}$ 是一个具有不可数多条无限路径的递归树。那么存在一个 $\Sigma_1(L_{\omega_1^{CK}})$-函数 $f : \omega_1^{CK} \to L_{\omega_1^{CK}}$，使得对任何 $\gamma_1 < \gamma_2 < \omega_1^{CK}$，都有 $f(\gamma_2) = T_{\gamma_2} \subseteq f(\gamma_1) = T_{\gamma_1} \subseteq T$，且 $\cap_{\gamma < \omega_1^{CK}} T_\gamma$ 是 $T$ 的一个完美子树。

证明。由于 $T$ 是递归的，我们有 $T \in L_{\omega+1}$。根据定理 3.1.8，存在一个 $\Sigma_1(L_{\omega_1^{CK}})$-函数 $f : \omega_1^{CK} \to L^K_{\omega_1^{CK}}$，使得

- $f(0) = T$;
- 对于任何 $\gamma < \omega_1^{CK}$，$f(\gamma + 1) = T_{\gamma+1} = \{\sigma \in T_\gamma \mid (\exists \tau_0, \tau_1 > \sigma)(\tau_0, \tau_1 \in T_\gamma \wedge \tau_0 \perp_T \tau_1)\} \subseteq f(\gamma)$;
- 如果 $\gamma$ 是极限序数，则 $f(\gamma) = T_\gamma = \cap_{\beta < \gamma} T_\beta$。

首先注意，对于每个 $\gamma < \omega_1^{CK}$，都有 $|[T_\gamma] \setminus [T_{\gamma+1}]| \le \aleph_0$，因此 $[T_{\omega_1^{CK}}] \neq \emptyset$。我们声称 $T_{\omega_1^{CK}} = \cap_{\gamma < \omega_1^{CK}} T_\gamma \subseteq T$ 是一棵完美树。首先注意，给定 $\sigma \in T_{\omega_1^{CK}}$，存在一个 $\tau > \sigma$ 使得 $\tau \in T_{\omega_1^{CK}}$。否则，设 $g_0(n)$ 为使得 $\sigma^\frown n \notin T_\gamma$ 的最小序数 $\gamma < \omega_1^{CK}$。那么 $g_0$ 是一个全函数，且在 $L_{\omega_1^{CK}}$ 中是 $\Sigma_1$ 的。根据 $\omega_1^{CK}$ 的可接受性（推论 3.6.7），存在一个序数 $\beta < \omega_1^{CK}$ 使得对所有 $n$ 都有 $g_0(n) < \beta$。那么 $\sigma \notin T_{\beta+1}$，这产生矛盾。

现在假设 $\sigma \in T_{\omega_1^{CK}}$ 是一条孤立路径，即 $[\sigma] \cap [T_{\omega_1^{CK}}]$ 包含恰好一条路径。设 $h_0(n)$ 为使得 $[\{\tau \in T \mid T_\gamma \wedge \tau \supset \sigma \mid [\sigma] = [\sigma] \mid n\}] = 1$ 的最小序数 $\gamma < \omega_1^{CK}$。那么 $h_0$ 是一个全函数，且在 $L_{\omega_1^{CK}}$ 中是 $\Sigma_1$ 的。再次根据推论 3.6.7，存在一个序数 $\beta < \omega_1^{CK}$ 使得对所有 $n$ 都有 $h_0(n) < \beta$。那么对于任何 $\tau_0, \tau_1 > \sigma$，如果 $\tau_0, \tau_1 \in T_\beta$，则 $\tau_0$ 和 $\tau_1$ 兼容。所以 $\sigma \notin T_{\beta+1}$，这产生矛盾。

### 3.6.6 练习

- 练习 3.6.1. 完成命题 3.6.5 的证明。
- 练习 3.6.2. 相对化并证明 § 3.6.4 中的结果。
- 练习 3.6.3. 证明存在一个具有不可数多条无限路径的递归树 $T$（如命题 3.6.10 所述），使得对每个 $\gamma < \omega_1^{CK}$，$T_\gamma$ 不是一棵完美树。
- 练习 3.6.4. 假设 $R_0$ 和 $R_1$ 编码了 $\omega$ 的良序关系，且 $R_0$ 的序类型不大于 $R_1$ 的序类型。证明存在一个序保持函数 $f \le_H R_0 \oplus R_1$，它将 $R_0$ 嵌入到 $R_1$ 的一个初始段上。
- 练习 3.6.5. 给定一个高算实数 $x$，证明存在两个递归良序 $R_0 \cong R_1$ 的 $\omega$，使得不存在在 $x$ 中递归的 $R_0$ 和 $R_1$ 之间的同构。
- 练习 3.6.6. 不使用克莱斯尔基定理，给出定理 3.6.8 的直接证明。

## 3.7 Spector–Gandy 定理

#### 3.7.1 第一版

定理 3.7.1 (斯佩克特 [156], 甘地 [34])。$x \in 2^\omega$ 是 $\Pi^1_1$，当且仅当存在一个 $\Sigma_1$-公式 $\varphi(u)$，使得 $n \in x \iff (L_{\omega_1^{CK}}, \in) \models \varphi(n)$。

证明。假设 $x \in 2^\omega$ 是 $\Pi^1_1$。根据命题 1.1.14，存在一个递归树 $T \subseteq \omega \times \omega^{<\omega}$ 和一个递归函数 $f$，使得 $n \in x$ 当且仅当 $f(n) = [\sigma \mid (f(n), \sigma) \in T]$ 是一棵良基树。由于 $T$ 是递归的，我们有 $T \in L_{\omega_1^{CK}}$。给定 $n$，我们说 $g : T_{f(n)} \to \gamma$ 是序保持的，如果 $\sigma \succ \tau$ 蕴含 $g(\sigma) < g(\tau)$。根据推论 3.6.7，



$L_{\omega_1^{CK}}^x$ 是可接受的。因此，根据定理 3.1.8，存在一个序数 $\gamma < \omega_1^{CK}$ 和一个序保持函数 $g : T_{[n]} \to \gamma$。

令 $\varphi(n)$ 为陈述

$(\exists y)(\exists g)(y \text{ 是一个序数 } \wedge g \text{ 是从 } T_{[n]} \text{ 到 } y \text{ 的一个序保持函数})$。

换句话说，$n \in x \Rightarrow (L_{\omega_1^{CK}}^x, \in) \models \varphi(n)$。另一方面，如果 $(L_{\omega_1^{CK}}^x, \in) \models \varphi(n)$，那么 $T_{[n]}$ 是良基的。因此 $n \in x$。

对于逆方向，假设存在一个 $\Sigma_1$-公式 $\varphi(u)$，使得 $n \in x \Leftrightarrow (L_{\omega_1^{CK}}^x, \in) \models \varphi(n)$。由于 $\varphi(u)$ 是 $\Sigma_1$，根据命题 3.5.5，$(L_{\omega_1^{CK}}^x, \in) \models \varphi(n)$ 当且仅当对于任何 $E$，如果 $(\omega, E)$ 对 KP 的一个 $\omega$-模型进行编码，那么 $(\omega, E) \models \varphi[n_E]$，其中 $n_E$ 表示在 $(\omega, E)$ 中对 $n$ 进行编码的数。根据命题 3.6.3，$x \in \Pi_1^1$。

尽管 [107] 中有评论称“Spector–Gandy 定理没有很多应用，但它无疑是有效理论的一颗明珠”，它仍然是一个主要结果，并在高递归理论中有重要应用。例如，该定理允许人们为结构 $(L_{\omega_1^{CK}}^x, \in)$ 发展一个健壮的计算理论，包括实现优先级方法来研究 $\Pi_1^1$-集的元度。

定理 3.7.1 的一个推广，将结果提升到实数集，如下所示。

### Corollary 3.7.2. 对于任何实数 $y$，集合 $A \subseteq 2^\omega$ 是 $\Pi_1^1(y)$ 当且仅当存在一个 $\Sigma_1$-公式 $\varphi(u, v)$，使得 $x \in A \Leftrightarrow (L_{\omega_1^{CK}}[x \oplus y], \in) \models \varphi(x, y)$。

应当指出，如果在 Corollary 3.7.2 中将 $2^\omega$ 替换为 $\omega^\omega$，则该推论中的陈述仍然有效。

### 3.7.2 第二版

令 $0^*$ 如 § 2.6 中所定义。固定一个数 $i \in 0^* \setminus 0$。然后，根据同一节中的结果，集合 $0_i^* = \{j \mid j <_{0^*} i\}$ 是一个 r.e. 集，使得 $0_i^* \cap 0$ 是 $0^*$ 的一个初始段，序类型为 $\omega_1^{CK}$。根据引理 2.2.4，存在一个递归函数 $g$，使得如果 $n \in 0$，则 $0_n = \Phi_{g(n)}^{0_i^*}$。

对于任何实数 $z$ 和 $n \in \omega$，令 $(z)_n = \{m \mid 2^n 3^m \in z\}$。令 $A(n, z)$ 为如下定义的算术谓词：存在一个 $m <_{0^*} i$，使得

- (1) $(z)_i = \emptyset$;
- (2) $(\forall j)((j \prec_{0^*} 2^n) \to (z)_j = ((z)_j)')$;
- (3) $(\forall y)(3^{x+5} \prec_{0^*} 2^n \to (\forall k)((z)_{y,3} s^* = (z)_{\varphi(x, k)})$;
- (4) $n \in \Phi_{g(m)}^{(2)_m}$，且
- (5) $(\forall j)((j \prec_{0^*} 2^n) \to (z)_j \le_T (z)_{2^n})$。

粗略地说，$A(n, z)$ 表示存在一个 $m <_{0^*} i$，使得 $z$ 沿着集合 $\{j \mid j \prec_{0^*} m\}$ 对图灵跳跃进行迭代编码，且 $n \in 0_m = \Phi_{g(m)}^{(2)_m}$。那么对于任何 $n \in 0_i^* \cap 0$，$(z)_n = H_n$。

### Theorem 3.7.3 (Spector [156], Gandy [34]). $x \in 2^\omega$ 是 $\Pi_1^1$ 当且仅当存在一个算术谓词 $B(n, z)$，使得 $n \in x \leftrightarrow (\exists z \in A_1^x)(B(n, z))$。

证明。根据 Corollary 2.2.12，如果存在一个算术谓词 $B(n, z)$，使得 $n \in x \leftrightarrow (\exists z \in A_1^x)(B(n, z))$，那么 $x$ 属于 $\Pi_1^1$。

假设 $x$ 是 $\Pi_1^1$。那么存在一个递归函数 $f$，使得 $n \in x \leftrightarrow f(n) \in \emptyset$。令 $A(n, z)$ 如前定义。如果 $n \in x$，则 $f(n) \in \emptyset_{(m)}$。令 $m <_{0^*} i$ 在 $\emptyset$ 中，使得 $|m| > f(n)$。令 $z$ 为一个实数，使得对于任何 $j \le \omega^2$，$\langle z \rangle_j = H_j$，而对于其他的 $j$，$\langle z \rangle_0 = \emptyset$。那么 $f(n) \in \emptyset_m = \varphi_{(m)}^{(\omega^2)m}$。显然 $z$ 是高算实数。因此 $n \in x$ 蕴含存在一个满足 $A(f(n), z)$ 的高算实数 $z$。

现在假设 $z$ 是高算的且 $A(f(n), z)$。那么存在一个 $m <_{0^*} i$，具有性质 (1)–(5)。我们声称 $m \in \emptyset$。否则，对于任何 $k \in \emptyset$，$H_k \le_T (z)_{2^{k+m}}$，这与 $z$ 是高算的事实矛盾。因此 $f(n) \in \emptyset_m = \varphi_{(m)}^{(\omega^2)m}$，从而 $n \in x$。令 $B(n, z)$ 为 $A(f(n), z)$。那么 $n \in x$ 当且仅当存在一个高算实数 $z$，使得 $B(n, z)$。

我们将证明下面定理 3.7.3 到实数集的推广留给读者：

### Corollary 3.7.4. $A \subseteq 2^\omega$ 是 $\Pi_1^1(y)$ 当且仅当存在一个算术谓词 $B$，使得 $x \in A \leftrightarrow (\exists z \le_h x \oplus y)(B(x, z, y))$。

定理 3.7.3 表明，如果我们将 $\Pi_1^1$-集视为 r.e. 集，那么高算实数就是有限集的类比。特别是，存在自然数的无限集是“有限”的。这与经典观念有所不同，经典观念中无限集永远不是“有限”的。

如 § 3.7.1 中所述，Gandy–Specter 定理提供了一种有效的——因此也是递归论的——方式来枚举 $\Pi_1^1$-集的元素。枚举是在 $L_{\omega_1^x}$ 中通过小于 $\omega_1^{CK}$ 的序数进行的。

对于 $\Pi_1^1$-实数集，情况更为棘手。Corollary 3.7.2 表明，集合 $A \subseteq 2^\omega$ 是 $\Pi_1^1$ 当且仅当存在一个 $\Sigma_1^1$-公式 $\varphi(u)$，使得 $x \in A \leftrightarrow (L_{\omega_1^x}[x], \in) \models \varphi(x)$（而不是 $(L_{\omega_1}, \in) \models \varphi(x)$）。这使得分析 $\Pi_1^1$-实数集成为一个更微妙的命题。对于每个实数 $x$，必须在 $L_{\omega_1^x}[x]$ 内工作以寻找 $\Sigma_1^1$-公式 $\varphi(u)$ 的解。这种缺乏一致性的问题在希望选择满足 $\varphi$ 的最早阶段枚举的 $x$ 时会出现。在 Gandy–Specter 定理第二版（3.7.3）的情况下，枚举 $\Pi_1^1$-实数集的相应程序是“枚举” $H^x$-集以计算一个证人 $z$。在这里，我们面临与第一版类似的问题，即没有统一的方式来执行这个程序。下面我们给出一个例子来说明如何解决这种困难。

### Definition 3.7.5. 集合 $A \subseteq 2^\omega$ 上的范数是一个函数 $\varphi : A \to \alpha$，其中 $\alpha$ 为某个序数。

范数是描述性集合论中最重要的对象之一。集合 $A$ 上的范数充当 $A$ 的“枚举函数”。

### Proposition 3.7.6. 令 \( A \subseteq 2^\omega \) 为 \( \Pi_1^1 \)。存在 \( A \) 上的一个范数 \( \phi \)、一个 \( \Pi_1^1 \)-关系 \( P(x, y) \) 和一个 \( \Sigma_1^1 \)-关系 \( Q(x, y) \)，使得对于任何 \( y \in A \)，\( (\forall x)(x \in A \land \phi(x) \le \phi(y) \rightarrow (P(x, y) \rightarrow Q(x, y))) \)。

*证明.* 由于 \( A \) 是 \( \Pi_1^1 \)，根据 Corollary 3.7.4，存在一个算术谓词 \( B(x, z) \)，使得 \( x \in A \Leftrightarrow (\exists z \in O^\times) B(x, z) \)。如果 \( x \in A \)，选择 \( n \in O^\times \) 使得 \( |n|_x \) 最小且对于某些 \( e \)，\( B(x, \phi_{n_1}^H) \) 成立。令 \( p(x) \) 如下：

- 1. \( (\exists n_0 \in O^\times)(\exists e)(B(x, \phi_{n_0}^H) \land (\forall m \in O_{n_0}^y)(\neg e)(B(x, \phi_{m_1}^H)) \);
- 2. \( (\exists n_1 \in O^\times)(\exists e)(B(y, \phi_{n_1}^H) \land (\forall m \in O_{n_1}^y)(\neg e)(B(y, \phi_{m_1}^H)) \)，且
- 3. 存在一个从 \( \{m \mid m <_{O^\times} n_0\} \) 到 \( \{m \mid m <_{O^\times} n_1\} \) 的初始段的同构。

子句 (3) 是 \( \Pi_1^1 \) 的，因为同构（如果存在的话）必须在 \( x \oplus y \) 中是高算的。

通过对 §2.6 中结果进行相对化，存在一个 \( \Sigma_1^1 \)-集 \( \{(x, O^{+,*}) \mid x \in 2^\omega\} \subseteq 2^\omega \times \omega \)，使得 \( <_{O^\times} \) 是 \( O^{+,*} \) 上的一个二元关系，具有以下性质：

- (i) \( O^\times \subseteq O^{+,*} \);
- (ii) \( <_{O^\times} \) 是 \( <_{O^\times} \) 对 \( O^\times \) 的限制；
- (iii) 对于任何 $n$，$n \in O^\times$ 当且仅当 $<_{O^\times}$ 对 $\{m \mid m <_{O^\times} n\}$ 的限制是一个良序。

令 \( Q(x, y) \) 为公式

```
\( (\forall n \in O^\times)(\exists e_0)(B(y, \phi_{n_0}^H) \rightarrow (\exists m \in O^{+,*})(\exists f)(\exists e_1) \)
\( (f : \{j \mid j <_{O^\times} m\} \rightarrow \{j \mid j \in O_{n_1}^y\} \text{ is order preserving } \land B(x, \phi_{e_1}^H)) \)。
```

现在很容易看出，如果 \( y \in A \)，那么 \( (\forall x)(x \in A \land \phi(x) \le \phi(y)) \) 当且仅当 \( P(x, y) \)，并且当且仅当 \( Q(x, y) \)。

命题 3.7.6 本质上表明，如果 \( y \) 属于 \( A \)，那么枚举到 \( A \) 中的实数集合在“$y$ 被枚举之前”是 \( \Delta_1^1(y) \)。

### 3.7.3 一个应用

我们应用 Spector-Gandy 定理来研究 \( \Sigma_1^1 \)-实数集。对于每个序数 \( \alpha < \omega_1 \)，令 \( r_\alpha \) 为对 \( \omega \) 的一个序类型为 \( \alpha \) 的良序进行编码的实数。在接下来的两个引理中，如果 \( \alpha \) 不是可数可接受序数，则令 \( R_\alpha = \emptyset \)（因为对于任何 \( x \in \omega \)，\( \omega_1^x \) 都是可接受的）。

### Lemma 3.7.7. 对于任何 \( \alpha < \omega_1 \)，集合 \( R_\alpha = \{x \mid \omega_1^x = \alpha\} \) 是 \( \Delta_1^1(r_\alpha) \)。

*证明.* 对于任何 $n$，令 $|n|_{r_\alpha}$ 为 $n$ 在序 $r_\alpha$ 下的阶。那么 $x \in R_\alpha$ 当且仅当

- \( (\forall n \in O^\times)(\exists f) \text{ 是 } \{m \mid m <_{O^\times} n\} \text{ 到 } r_\alpha \text{ 的一个嵌入} \land \)
- \( (\exists g)(\exists i \in O^{+,*})(g \text{ 是从 } r_\alpha \text{ 到 } O_i^{+,*} \text{ 的一个初始段的同构映射}) \)。





因此 $R_a$ 是 $\Sigma^1_1(r_a)$。令 $r'_a \le_T r_a$ 成为 $\omega$ 的一个序类型为 $\alpha + 1$ 的良序。则 $x \in R_a$ 当且仅当

- (vf) $(\forall n \in O^{r_a*})(f$ 不是 $r_a^*$ 到 $O^{r_a*}$ 的嵌入) $\wedge$
- (vn) $(\exists m \in O^{r_a*})(\exists g$ 是 $(m \mid m <_{r_a} n)$ 到 $(i \mid i \prec_\omega m)$ 的初始段的同构)。

根据练习 3.6.4，上述表达式中的 $g$ 可以取为相对 $r_a \oplus [i \prec_\omega m]$ 的超算术，而后者又相对 $r_a \oplus x$ 是超算术的。因此 $R_a$ 也是 $\Pi^1_1(r_a)$，从而是 $\Delta^1_1(r_a)$。

### Lemma 3.7.8.

对于任意 $\alpha < \omega_1$，关系 $C_\alpha(x, y) \Leftrightarrow y \le_B x \wedge x \in R_a$ 是 $\Delta^1_1(r_a)$。

### Proof.

根据推论 2.2.2 和引理 3.7.7，$C_a$ 是 $\Pi^1_1(r_a)$。

我们证明 $C_a$ 是 $\Sigma^1_1(r_a)$。现在 $y \le_B x$ 当且仅当存在一个 $n \in O^{r_a}$ 使得 $y \le_T H_n^a$，且根据前一引理，后者成立当且仅当存在一个 $n \in O^{r_a*}$ 和一个 $f : [m \mid m <_{\omega^*} n] \to \omega$，使得对所有 $i <_{\omega^*} j$，$(f(i), f(j)) \in r_a$。于是 $y \le_B x$ 是 $\Sigma^1_1(r_a)$。因此 $C_a$ 是 $\Sigma^1_1(r_a)$。

### Lemma 3.7.9.

- (i) 每个 $\Pi^1_1$-实数集是 $\aleph_1$ 个博雷尔集的并。
- (ii) 每个 $\Sigma^1_1$-实数集是 $\aleph_1$ 个博雷尔集的并。

### Proof.

(i) 假设 $A \in \omega^\omega$ 是 $\Pi^1_1$。根据推论 3.7.4，存在一个算术谓词 $A(x, z)$，使得 $x \in A \Leftrightarrow (\exists z \le_B x)\Sigma(x, z)$。对任意 $\alpha < \omega_1$，令 $A_\alpha = A \cap R_\alpha$。则 $A_\alpha$ 是 $\Pi^1_1(r_\alpha)$。根据引理 3.7.8，$A_\alpha$ 也是 $\Sigma^1_1(r_\alpha)$。因此 $A_\alpha$ 是 $\Delta^1_1(r_\alpha)$，从而是博雷尔集。

(ii) 假设 $A \subseteq 2^\omega$ 是 $\Sigma^1_1$。则存在一个 $\Pi^0_2$ 集合 $B \subseteq \omega^\omega \times 2^\omega$，使得 $x \in A$ 当且仅当 $(\exists \beta)B(f, x)$。对 $\alpha < \omega_1$，令 $A_\alpha = A \cap R_\alpha$。根据引理 3.7.7，$A_\alpha$ 是 $\Sigma^1_1(r_\alpha)$。

根据甘迪基数定理 2.5.3，$x \in A$ 当且仅当 $(\exists f <_B O^{r_\alpha}) B(f, x)$。由于 $\omega_1^{f*_1} > \omega_1^r$，我们有 $x \notin r_\alpha$。将推论 2.4.10 的证明相对化到 $r_\alpha$ 得到 $O^{r_\alpha} \le_B x \oplus r_\alpha$。我们得出结论，$A_\alpha$ 是 $\Pi^1_1(r_\alpha)$，从而是 $\Delta^1_1(r_\alpha)$。

### Corollary 3.7.10 (Lusin [86]).

每个 $\Pi^1_1$-实数集是可测的。

### Proof.

遵循引理 3.7.9 的记号，对每个 $n \in \omega$ 和 $\alpha < \omega_1$，令 $D_{n, \alpha} = \{x \mid n \in O^{r_\alpha*} \wedge ([m \mid m <_{\omega^*} n, l <_{\omega^*}) \equiv r_\alpha\}$。

则 $D_{n, \alpha}$ 是 $\Sigma^1_1(r_\alpha)$。根据引理 3.7.8 的证明和练习 3.6.4，

$D_{n, \alpha} = \{x \mid n \in O^{r_\alpha} \wedge ([m \mid m <_{\omega^*} n, l <_{\omega^*}) \equiv r_\alpha\}$

且是 $\Pi^1_1(r_\alpha)$。因此 $D_{n, \alpha}$ 是博雷尔集。注意当 $\alpha \neq \beta$ 时，$D_{n, \alpha} \cap D_{n, \beta} = \emptyset$。故对任意 $n$，存在一个 $\alpha_n < \omega_1$，使得当 $\beta \geq \alpha_n$ 时 $\mu(D_{\beta, n}) = 0$。令 $\alpha_\omega < \omega_1$ 为这些 $\alpha_n$ 的一个上界。

现在假设 $A$ 是 $\Pi^1_1$。则对任意 $\alpha > \alpha_\omega$，$x \in A_\alpha$ 蕴含存在一个 $n$ 使得 $x \in D_{n, \alpha_\omega}$。换句话说，$\bigcup_{\alpha > \alpha_\omega} A_\alpha \subseteq \bigcup_n D_{n, \alpha_\omega}$。根据 $\alpha_\omega$ 的选取，\(\mu(\bigcup_{n<\omega} A_n) = 0\)。但 \(\bigcup_{n<\omega} A_n\) 是一个可测的博雷尔集。我们得出结论，\(A = \bigcup_{\alpha<\omega} A_\alpha\) 是可测的。

我们将在第 14 章计算 \(\alpha_\omega\) 的值。

### Theorem 3.7.11 (Sierpinski [135]). 每个 \(\Sigma^1_2\)-实数集是 \(\omega_1\) 个博雷尔集的并。

### Proof.

假设 \(A \subseteq 2^\omega\) 是 \(\Sigma^1_2\)。则存在一个 \(\Pi^1_1\)-集合 \(B \subseteq \omega^\omega\)，使得 \(x \in A\) 当且仅当 \((\exists f \in \omega^\omega) B(f, x)\)。根据引理 3.7.9 的 (i)，存在一个博雷尔集的 \(\omega_1\)-序列 \(\{B_\alpha\}_{\alpha<\omega_1}\)，使得 \(\bigcup_{\alpha<\omega_1} B_\alpha = B\)。则对每个 \(\alpha < \omega_1\)，\(C_\alpha = \{x \mid (\exists f \in \omega^\omega) B_\alpha(f, x)\}\) 是 \(\Sigma^1_1\)。显然 \(A = \bigcup_{\alpha<\omega_1} C_\alpha\)。通过将引理 3.7.9 的 (ii) 相对化，每个 \(C_\alpha\) 是 \(\omega_1\) 个博雷尔集的并。因此 \(A\) 是 \(\omega_1\) 个博雷尔集的并。

### Corollary 3.7.12. 每个势大于 \(\aleph_1\) 的 \(\Sigma^1_2\)-实数集都有一个完美子集。

### Proof.

根据定理 3.7.11，每个 \(\Sigma^1_2\)-实数集 \(A\) 都是 \(\aleph_1\) 个博雷尔集的并。如果 \(A\) 的势大于 \(\aleph_1\)，则其中一个博雷尔集是不可数的，因而有一个完美子集。

### 3.7.4 练习

### Exercise 3.7.1. 以下是定理 2.4.7 的另一个证明。

- (i) 证明 \(\emptyset\) 在 \(L_{\omega_1^{CK}}\) 上是 \(\Sigma_1\)-可定义的；
- (ii) 证明对任意实数 \(x\) 和 \(y\)，\(x \le_T y\) 当且仅当 \(x \in L_{\omega_1^y}[y]\)，从而 \(\emptyset \le_B y\) 当且仅当 \(\omega_1^x < \omega_1^y\)。

### Exercise 3.7.2. 证明存在一个实数序列 \(\{x_n\}_{n<\omega}\)，使得对每个 \(n\)，\(x_n \ge_T x_{n+1}^T\)。

### Exercise 3.7.3. 证明如果 \(\{x_n\}_{n<\omega}\) 是如上序列，则对每个 \(n\)，\(x_n\) 不是超算术的。

### Exercise 3.7.4. 使用 Spector–Gandy 定理（3.7.1）的第一个版本来证明定理 3.7.11。

### Exercise 3.7.5. 证明如果 \(x\) 是一个实数，使得每个非空的 \(\Pi^0_1\) 集合 \(A \subseteq \omega^\omega\) 都有一个相对 \(x\) 超算术的元素，则 \(x \ge_T \emptyset\)。

### Exercise 3.7.6. 证明集合 \(\{(x, y) \mid x_0^y > \omega_1^x\}\) 是 \(\Pi^1_1\) 但不是 \(\Sigma^1_1\)。

### Exercise 3.7.7. 假设 \(\mathsf{MA} + 2^{\aleph_0} > \aleph_1\)（参见定义 6.1.5）。证明每个 \(\Sigma^1_2\)-集合是可测的。

## 4 \(\Pi^1_1\)-集合的理论

\(\Pi^1_1\)-实数集被赋予了丰富的结构性质，包括那些从可构造宇宙 \(L\) 的角度来看最易理解的性质。本章对这类集合进行更深入的分析，以阐明这一点。

### 4.1 一个 \(\Pi^1_1\)-基数定理

#### 4.1.1 \(\Pi^1_1\)-集合的树表示

回顾，给定一个 \(\Pi^1_1\)-集合 \(A \subseteq 2^\omega\)，存在一个递归谓词 \(P \subseteq 2^{<\omega} \times \omega^\omega\)，使得 \(x \in A\) 当且仅当 \((\forall f)(\exists n) \neg P(x \mid n \mid f \mid n)\)。换句话说，\(x \in A\) 当且仅当 \(x\)-递归树 \(T_x = \{\sigma \mid (\forall \tau)(\tau \subseteq \sigma \rightarrow P(x \mid |\tau|, \tau))\}\) 在 Kleene-Brouwer 序下是良基的。那么存在一个函数 \(p_x : T_x \rightarrow \omega_1^\omega\)，其中 \(p_x \in L_{\omega_1^x}[x]\)，使得 \(p_x\) 在 Kleene-Brouwer 序下是序保持的。

现在令 \(T \subseteq 2^{<\omega} \times \omega_1^{<\omega}\) 成为一个集合，使得 \((\sigma, p) \in T\) 当且仅当 \(p\) 是从 \(\{\tau \mid \tau \subseteq [\sigma]^{|\sigma|}\} \wedge (\forall \tau')( \tau' \subseteq \tau \rightarrow P(\sigma \mid [\tau'], \tau'))\) 到 \(\omega_1\) 的一个序保持的有限函数。定义 \((\sigma', p') \geqslant (\sigma, p)\) 当且仅当 \(\sigma' \supseteq \sigma\) 且 \(p'\) 扩展 \(p\)。那么 \(T\) 在 \(>\) 下是一棵树。因此 \(x \in A\) 当且仅当存在一个 \(f : T_x \rightarrow \omega_1\) 使得 \((x, f)\) 是 \(T\) 中的一条无限路径，这当且仅当存在一个 \(f : T_x \rightarrow \omega_1\) 且 \(f \in L_{\omega_1^x}[x]\) 使得 \((x, f)\) 是 \(T\) 中的一条无限路径。

树表示的优势在于 \(x\) 的伴随路径存在于 \(L_{\omega_1^x}[x]\) 中。

- 给定 \((\sigma, p), (\sigma', p') \in 2^{<\omega} \times \omega_1^{<\omega}\)，我们说 \((\sigma', p') \prec_l (\sigma, p)\) 如果
  - 要么 \((\sigma', p') \prec (\sigma, p)\)，或
  - 存在一个 \(i\) 使得 \(\sigma'(i) < \sigma(i)\) 且对所有 \(j < i\)，\(\sigma'(j) = \sigma(j)\)，或
  - 存在一个 \(v \in \omega^{<\omega}\) 使得 \(p'(v) < p(v)\) 且对所有 \(v' \prec_{KB} v\)，\(v \in \text{Dom}(p) \Rightarrow p'(v') = p(v')\)。

\(T\) 中的一条无限路径 \((x, f)\) 是 *最左路径* 如果在 \(\{(\sigma, p) \mid (\sigma, p) \prec_l (x \mid [n], f \mid \text{Dom}(p))\}\) 中不存在无限路径。

### Lemma 4.1.1. 假设 \((x, f)\) 是 \(T\) 的最左路径。则 \(f \in L_{\omega_1^x}[x]\)。

### Proof.

假设 \((x, f)\) 是 \(T\) 的最左路径。则 \(f\) 是从 \(x\)-递归树 \(T_x = \{\sigma \mid P(x \mid |\sigma|, o)\}\) 到 \(\omega_1^x\) 的一个初始段的唯一序保持函数。由于 \(L_{\omega_1^x}[x]\) 是可接受的，根据 \(\Sigma\)-归纳定理（3.18），我们有 \(f \in L_{\omega_1^x}[x]\)。




### 4.1.2 可构基定理

定理 4.1.2 (Gupasari [42])。如果 \( A \subseteq 2^\omega \) 是一个非空的 \( \Pi^1_1 \)-集，那么存在 \( x \in A \) 使得 \( x \in L_{\omega_1^x} \)。

证明。令 T 为 A 的树表示，(x, f) 为其最左路径。我们声称 \( x \in L_{\omega_1^x} \)。根据引理 4.1.1，\( f \in L_{\omega_1^x}[x] \)。因此存在一个序数 \( \alpha_0 < \omega_1^x \) 使得 Rang(f) = \( \alpha_0 \)。我们通过在 T 中到处将 \( \omega_1 \) 替换为 \( \alpha_0 \) 来定义树 \( T^{\alpha_0} \)。显然，对于某个 \( \gamma_0 < \omega_1^x \)，\( T^{\alpha_0} \in L_{\omega_1}[x] \)，且 (x, f) 是 \( T^{\alpha_0} \) 中的一条无限路径。此外，对于任意 \( (\sigma, p) < (x \upharpoonright |\sigma|, f \upharpoonright \text{Dom}(p)) \)，\( T^{\alpha_0}_{(\sigma, p)} = \{\sigma', \tau' \in T^{\alpha_0} \mid (\sigma', p') > (\sigma, p)\} \) 中没有无限路径。否则，任何这样的无限路径也将在 T 中，并且位于 (x, f) 的左侧，这与 (x, f) 在 T 中的选择相矛盾。那么，对于任意 \( (\sigma, p) < (x \upharpoonright |\sigma|, f \upharpoonright \text{Dom}(p)) \)，存在序数 \( \alpha_{(\sigma, p)} < \omega_1^x \)、\( \beta_{(\sigma, p)} < \alpha_{(\sigma, p)} \) 和一个函数 \( g_{(\sigma, p)} \in L_{\alpha_{(\sigma, p)}} \)，使得 \( g_{(\sigma, p)} \) 是从 \( T^{\alpha_0}_{(\sigma, p)} \) 到 \( \beta_{(\sigma, p)} \) 的序保持函数。此外，从 \( (\sigma, p) < (x \upharpoonright |\sigma|, f \upharpoonright \text{Dom}(p)) \) 到 \( \alpha_{(\sigma, p)} < \omega_1^x \) 的函数在 \( L_{\omega_1^x}[x] \) 中是 \( \Sigma_1 \) 的。由于集合 \( \{(\sigma, p), T^{\alpha_0}_{(\sigma, p)} \mid (\sigma, p) < (x \upharpoonright |\sigma|, f \upharpoonright \text{Dom}(p))\} \) 是 \( L_{\omega_1^x}[x] \) 的一个元素，存在一个 \( \gamma < \omega_1^x \) 它界定了任何 \( \alpha_{(\sigma, p)} \)，其中 \( (\sigma, p) < (x \upharpoonright |\sigma|, f \upharpoonright \text{Dom}(p)) \)。我们可以假设 \( \gamma > \alpha_0 \)。现在在 \( L_\gamma \) 中工作，我们按如下方式定义一条无限路径：\( (o_0, p_0) = 0 \)。\( (o_{i+1}, p_{i+1}) > (o_i, p_i) \) 在 \( T^{\alpha_0} \) 中长度为 i + 1，使得 (1) 对于所有不扩展 \( (o_{i+1}, p_{i+1}) \) 的 \( (\sigma, p) < (o_{i+1}, p_{i+1}) \)，存在一个序保持函数 \( g_{(\sigma, p)} \in L_\gamma \) 从 \( T^{\alpha_0}_{(\sigma, p)} \) 到一个序数 \( \beta_{(\sigma, p)} < \gamma \)，并且 (2) 不存在序保持函数 \( g \in L_\gamma \) 从 \( T^{\alpha_0}_{(o_{i+1}, p_{i+1})} \) 到任何序数 \( \beta < \gamma \)。根据 \( \gamma \) 的假设，我们有 \( \bigcup_{i < \omega} (o_i, p_i) = (x, f) \)。显然，序列 \( \{(o_i, p_i)\}_{i < \omega} \) 是 \( L_{\gamma + \omega} \) 的一个元素。因此 \( (x, f) \in L_{\gamma + \omega} \subseteq L_{\omega_1^x} \)，所以 \( x \in L_{\omega_1^x} \)。

作为定理 4.1.2 的直接推论，

推论 4.1.3。如果 x 是一个 \( \Pi^1_1 \)-单点，那么 \( x \in L_{\omega_1^x} \)。

### 4.1.3 练习

练习 4.1.1. 使用定理 4.1.2 证明命题 4.2.5。

练习 4.1.2. 证明存在非可构实数当且仅当存在一个不包含可构实数的非空 \( \Pi^1_1 \)-集。

## 4.2 $\Pi^1_1$-一致化

#### 4.2.1 一致化 $\Pi^1_1$-关系

给定一个关系 $R \subseteq 2^\omega \times 2^\omega$，如果对于任意 x 和 y，$R_0(x, y)$ 蕴含 $R(x, y)$，并且对于任意 x，如果存在 y 使得 $R(x, y)$，则存在唯一的 y 使得 $R_0(x, y)$，则称关系 $R_0$ 是 R 的一致化。R 的一致化实际上是 R 的一个选择函数。

定理 4.2.1 (Kondo [74] 和 Addison [1])。假设 $R \subseteq 2^\omega \times 2^\omega$ 是 $\Pi^1_1$。那么存在一个一致化 R 的 $\Pi^1_1$-关系 $R_0$。

证明。假设 $R \subseteq 2^\omega \times 2^\omega$ 是 $\Pi^1_1$。根据推论 3.7.2，存在一个 $\Sigma_0$-公式 $\varphi(u, v, w)$ 使得

$(x, y) \in R \leftrightarrow (L_{\omega_1^{xy}}[x \oplus y], \in) \models (\exists w)\varphi(x, y, w).$

定义 $R_0 \subseteq 2^\omega \times 2^\omega$ 使得 $(x, y) \in R_0$ 当且仅当
- (i) $y \in L_{\omega_1^{xy}}[x]$;
- (ii) $(\exists w \in L_{\omega_1^{xy}}[x])((L_{\omega_1^{xy}}[x], \in) \models \varphi(x, y, w))$；以及
- (iii) $(L_{\omega_1^{xy}}[x], \in) \models (\forall z \forall w')(w' <_{L[x]} (y, w) \rightarrow \neg\varphi(x, z, w'))$。

根据定理 4.1.2，如果存在 y 使得 $(x, y) \in R$，则存在一个 y 使得 $R_0(x, y)$。根据 $R_0$ 的定义，$R_0$ 一致化 R。注意上述 (i) 和 (ii) 都是 $\Sigma_1$-陈述。根据命题 3.3.3，(iii) 也是一个 $\Sigma_1$-陈述。根据推论 3.7.2，$R_0$ 是一个 $\Pi^1_1$-关系。

现在我们来讨论 $\Pi^1_1$ 一致化定理（4.2.1）的一些有趣应用：

命题 4.2.2. 给定 $\Pi^1_1$-集 $A_0$ 和 $B_0$，存在不相交的 $\Pi^1_1$-集 $A_1 \subseteq A_0, B_1 \subseteq B_0$，使得 $A_0 \cup B_0 = A_1 \cup B_1$。

证明。令 $R \subseteq 2^\omega \times 2^\omega$ 为一个 $\Pi^1_1$-关系，使得 $(x, i) \in R$ 当且仅当要么 $i = 0$ 且 $x \in A_0$，要么 $i = 1$ 且 $x \in B_0$。根据定理 4.2.1，存在一个一致化 R 的 $\Pi^1_1$-关系 $R_0$。定义 $x \in A_1$ 当且仅当 $(x, 0) \in R_0$，且 $x \in B_1$ 当且仅当 $(x, 1) \in R_0$。那么 $A_1, B_1$ 即为所需集合。

推论 4.2.3. 给定不相交的 $\Sigma^1_1$-集 $A_0, B_0$，存在不相交的 $\Delta^1_1$-集 $A_1, B_1$，使得 $A_0 \subseteq A_1, B_0 \subseteq B_1$ 且 $A_1 \cup B_1 = 2^\omega$。

证明。假设意味着 $2^\omega \setminus A_0$ 和 $2^\omega \setminus B_0$ 是 $\Pi^1_1$。根据命题 4.2.2，存在两个 $\Pi^1_1$-集 $A_1 \supseteq B_0, B_1 \supseteq A_0$，使得 $A_1$ 和 $B_1$ 不相交且 $A_1 \cup B_1 = 2^\omega$。因此这些集合是 $\Delta^1_1$。

#### 4.2.2 Kreisel 紧性定理

Kreisel 的紧性定理是模型论中紧性定理推广到 \(L_{\omega_1\omega}\)-逻辑的结果。在此背景下，“递归可枚举”是 \(\Pi^1_1\)，“有限”是 \(\Delta^1_1\)。它是 \(\Pi^1_1$-一致化定理的一个显著应用。

**定理 4.2.4** (Kreisel)。令 \(A \subseteq \omega^2\) 为一个 \(\Pi^1_1$-集，使得对于每个 \(n\)，\(A_n = \{x \mid (n, x) \in A\}\) 是 \(\Delta^1_1$。令 \(z \in \Pi^1_1$。如果对于每个超算术的 \(y \subseteq z\)，\(\bigcap_{n \in \omega} A_n \neq \emptyset\)，那么 \(\bigcap_{n \in \omega} A_n \neq \emptyset$。

证明。假设不成立。那么 \(z\) 是真正的 \(\Pi^1_1$ 且 \(\bigcap_{n \in \omega} A_n = \emptyset$。那么对于每个 \(x\)，存在一个 \(n\) 使得 \(x \notin A_n$。定义一个 \(\Pi^1_1$-关系 \(R \subseteq 2^{<\omega} \times \omega$ 使得 \(R(x, n) \Leftrightarrow n \in 2^\omega \times A_n$。根据一致化定理（4.2.1），存在一个全函数 \(\Pi^1_1$-函数 \(f$ 一致化 \(R$。那么集合 \(y = \{n \mid (\exists x)(f(x) = n)\}$ 包含于 \(z$ 且是 \(\Sigma^1_1$。如果 \(x \in \bigcap_{n \in \omega} A_n$，那么 \(f(x) \in \omega \setminus y$。但没有 \(m \in \omega \setminus y$ 属于 \(f[2^\omega]$。因此 \(\bigcap_{n \in \omega} A_n = \emptyset$。根据推论 4.2.3 限制于 \(\omega$ 上，存在一个 \(\Delta^1_1$-实数 \(y_0$ 使得 \(y \subseteq y_0 \subseteq z$。那么 \(\bigcap_{n \in \omega} A_n = \emptyset$，这是一个矛盾。

定理 4.2.4 由 Barwise [3] 进一步推广到可数可接受集，作为无穷逻辑的一个紧性定理。

#### 4.2.3 \(\Pi^1_1$-单点

**命题 4.2.5.** 每个非空的实数 \(\Pi^1_1$-集包含一个 \(\Pi^1_1$-单点。

证明。假设 \(A \subseteq 2^\omega\) 是 \(\Pi^1_1$ 且非空。令 \((n, x) \in R$ 当且仅当 \(x \in A$。那么 \(R$ 是一个 \(\Pi^1_1$-关系。根据定理 4.2.1，存在一个一致化 \(R$ 的 \(\Pi^1_1$-关系 \(R_0$。那么唯一的实数 \(x$ 使得 \((0, x) \in R_0$ 是一个 \(\Pi^1_1$-单点。

根据命题 4.2.5，我们知道每个非空的 \(\Pi^1_1$-集包含一个 \(\Pi^1_1$-单点。

**命题 4.2.6.** 集合 \(\{x \mid x \text{ 是一个 } \Pi^1_1\text{-单点}\}\) 是 \(\Pi^1_1$。

证明。令 \(P \subseteq \omega \times 2^\omega$ 为一个通用的 \(\Pi^1_1$-集。根据命题 4.2.5，存在一个一致化 \(P$ 的 \(\Pi^1_1$-集 \(P_0 \subseteq P$。令 \(A = \{x \mid (\exists n)(n, x) \in P_0\}\)。那么 \(A$ 是一个 \(\Pi^1_1$ 集，恰好包含所有的 \(\Pi^1_1$-单点。

由于只有可数个 \(\Pi^1_1$-单点，存在一个可数的 \(\Pi^1_1$-集作为实数 \(\Pi^1_1$-集的基。这给出了 \(\Sigma^1_2$-集的以下基结果。

**推论 4.2.7.** 每个非空的实数 \(\Sigma^1_2$-集包含一个 \(\Delta^1_2$-元素。

证明。假设 \(A$ 是一个非空的实数 \(\Sigma^1_2$-集。那么 \(x \in A$ 当且仅当对于某些 \(\Pi^1_1$-关系 \(B\)，\((\exists y)B(x, y)$。根据命题 4.2.5，存在一个 \(\Pi^1_1$-单点，因此是一个 \(\Delta^1_2$-实数，\((x_0, y_0)$ 使得 \(B(x_0, y_0)$。那么 \(x_0 \in A$ 是 \(\Delta^1_2$。




根据推论 4.2.7 的证明，我们有关于 \(\Delta^1_2\)-实数的以下刻画。

**推论 4.2.8.** _实数 x 是_ \(\Delta^1_2\) _当且仅当 x 可在某个_ \(\Pi^1_1\)_-单子中递归。因此，_ \(\Delta^1_2\)_-实数的集合是_ \(\Sigma^1_2\) _。_

**推论 4.2.9** (肖恩菲尔德 [129])**.** (i) _如果_ \(A \subseteq 2^\omega\) _非空且为_ \(\Sigma^1_2\) _，则存在_ \(x \in A \cap L\) _可在某个_ \(\Pi^1_1\)_-单子中递归。_
(ii) _每个_ \(\Delta^1_2\)_-实数都是可构的。_

_证明._ (i) 如果 \(A \subseteq 2^\omega\) 是非空 \(\Sigma^1_2\)-集，则存在 \(\Pi^1_1\)-集 \(B \subseteq 2^\omega \times 2^\omega\)，使得 \(x \in A\) 当且仅当存在 _y_ 使得 _B_(_x_, _y_)。根据命题 4.2.25，存在 \(\Pi^1_1\)-单子 _B_(_x_<sub>0</sub>, _y_<sub>0</sub>)。根据推论 4.1.3，\((x_0, y_0) \in L\)。因此 \(x_0 \in A\) 是可在 \(\Pi^1_1\)-单子 \(x_0 \oplus y_0\) 中递归的可构实数。
(ii) 直接由 (i) 得出，因为每个 \(\Delta^1_2\)-实数都是 \(\Sigma^1_2\)-单子。\(\square\)

推论 4.2.9 (i) 在文献中被称为 _肖恩菲尔德绝对性引理_。集合论中有许多这样的应用。例如，给定一个 \(\Sigma^1_2\)-谓词 _P_，则 \((L, \varepsilon) \models P\) 当且仅当 \(\langle V, \varepsilon \rangle \models P\)。

### 4.2.4 练习

**练习 4.2.1.** _证明存在一个_ \(\Sigma^1_1\)_-关系_ \(R \subseteq 2^\omega \times 2^\omega\) _，该关系不能由任何_ \(\Sigma^1_1\)_-关系一致化。_

**练习 4.2.2.** _证明不存在_ \(\Pi^1_1\)_-集_ \(x \subseteq \emptyset\) _，其中_ \(<_\omega\) _限制到 x 上是序数类型为_ \(\omega_1^{CK}\) _的良序，并且存在一个部分递归函数_ \(p : \omega^2 \to \omega\) _满足练习 1.4.1 的性质_ (i)_-_(iii) _。_

**练习 4.2.3.** _从定理 4.2.1 证明定理 4.1.2。_

## 4.3 刻画稀疏 \(\Pi^1_1\)-集

如果一个集合不包含任何完美子集，则称其为 _稀疏_。存在关于 \(\Pi^1_1\)-稀疏集的可构性方面的优美刻画。

#### 4.3.1 最大稀疏 \(\Pi^1_1\)-集

令 \(\mathbb{C} = \{x \mid x \in L_{\omega_1}\}\)。

**引理 4.3.1.** \(\mathbb{C}\) _是一个稀疏_ \(\Pi^1_1\)_-集。_

_证明._ \(x \in L_{\omega_1}\) 当且仅当 \((L_{\omega_1}[x], \in) \models (\exists \beta)(x \in L_\beta)\)。根据定理 3.3.2 和推论 3.7.2，C 是 \(\Pi^1_1\)。假设 \(\mathcal{C}\) 不是稀疏的。令

\(B = \{T \in 2^{<\omega} \mid T \text{ 是一个完美树，其中每条无限路径都属于 } \mathcal{C}\}.\)

那么 \(B\) 是一个 \(\Pi^1_1\)-集。根据定理 4.1.2，存在 \(T \in B\) 使得 \(T \in L_{\omega_1}\)。通过将甘迪基数定理 (2.5.3) 相对化到 \(T\)，存在一个实数 \(x \in [T] \subseteq \mathcal{C}\)，使得 \(x \not\le_h T\) 且 \(\omega_1^x \le \omega_1^{x \oplus T} = \omega_1^T\)。因此 \(x \notin L_{\omega_1}\)，矛盾。

**引理 4.3.2** (曼斯菲尔德 [87], 索洛维 [149]). 设 \(A \subseteq 2^\omega\) 为 \(\Pi^1_1\)。如果存在 \(x \in A\) 使得 \(x \notin L_{\omega_1}\)，则存在一个完美树 \(T \in L\)，其所有无限路径都属于 \(A\)。

**证明.** 令 \(\mathcal{C}\) 如前定义。假设 \(A \subseteq 2^\omega\) 是 \(\Pi^1_1\) 且存在 \(x \in A \setminus \mathcal{C}\)。令 \(\alpha_0\) 为最小序数 \(\alpha\)，使得存在 \(x \in A \setminus \mathcal{C}\) 使得 \(\alpha = \alpha_1^x\)。

令 \(T_0\) 为 \(A\) 的树表示，\(T_0^\alpha\) 按定理 4.1.2 证明中定义。由于 \(\mathcal{C}\) 是 \(\Pi^1_1\)-集，存在递归树 \(T_1 \subseteq 2^{<\omega} \times \omega^{<\omega}\)，使得 \(x \notin \mathcal{C}\) 当且仅当 \((\exists y)((x, y) \in [T_1])\)。现在令 \(T_2 \subseteq 2^{<\omega} \times \omega^{<\omega} \times 2^{<\omega}\) 为如下定义的树：\((\sigma, p, \tau) \in T_2\) 当且仅当 \((\sigma, p) \in T_0^\alpha\) 且 \((\sigma, \tau) \in T_1\)。根据假设，\(T_2\) 中存在无限路径 \((x, f, y)\)。

我们声明，对于任何 \((\sigma, p, \tau) \in T_2\)，如果 \(T_{2, (\sigma, p, \tau)} = \{(\sigma', p', \tau') \in T_2 \mid (\sigma', p', \tau') \succ (\sigma, p, \tau)\}\) 中存在无限路径，则存在 \(T_{2, (\sigma, p, \tau)}\) 中的 \((\sigma_0, p_0, \tau_0)\) 和 \((\sigma_1, p_1, \tau_1)\)，其中 \(\sigma_0\) 和 \(\sigma_1\) 不兼容，使得 \(T_{2, (\sigma_0, p_0, \tau_0)}\) 和 \(T_{2, (\sigma_1, p_1, \tau_1)}\) 都有无限路径。否则，选取 \(T_2\) 中一个使得此命题不成立的 \((\sigma, p, \tau)\)。那么 \(T_{2, (\sigma, p, \tau)}\) 中存在无限路径 \((x, f, y)\)。注意 \(\omega_1^x \ge \alpha_0\)。根据假设，对于任何 \(\sigma' \succ \sigma\) 且不是 \(x\) 的初始段，树

\(T_{2, \sigma'} = \{(\sigma'', p'', \tau'') \in T_{2, (\sigma, p, \tau)} \mid \sigma' \succ \sigma\}\)

是良基的。然后，与定理 4.1.2 证明相同，存在 \(\gamma < \omega_1^x\) 使得集合 \(\{\sigma' \mid (\exists \sigma'', p'', \tau'') \in T_{2, (\sigma, p, \tau)}\, \sigma' \subseteq \sigma''\}\) 属于 \(L_\gamma\)。因此 \(x \in L_{\gamma+1} \subseteq L_{\omega_1}\)，这与 \(x \notin \mathcal{C}\) 矛盾。

根据该声明，可以执行定理 1.1.10 的第一个构造以获得一个完美树，其所有路径都属于 \(A\)。因此集合 \(\{T \mid T \text{ 是完美的且 } [T] \subseteq A\}\) 是一个非空 \(\Pi^1_1\)-集。根据定理 4.1.2，存在完美树 \(T \in L\) 使得 \([T] \subseteq A\)。

根据引理 4.3.1 和引理 4.3.2，我们有关于最大稀疏 \(\Pi^1_1\)-集的以下刻画。

**定理 4.3.3.** \(\mathcal{C}\) 是最大稀疏 \(\Pi^1_1\)-集。

#### 4.3.2 \(\mathcal{C}\) 的一些性质

由于每个实数的 \(\Pi^1_1\)-集都包含一个 \(x \in \mathcal{C}\)，且该 \(x\) 也是 \(\Pi^1_1\)-单子，人们可能会问 \(\mathcal{C}\) 中的每个实数是否都是 \(\Pi^1_1\)-单子。这是错误的，因为 \(\mathcal{C}\) 在 \(L\) 中是不可数的。

**命题 4.3.4.** 对于任何实数 \(x \in L\)，存在 \(z \in \mathbb{C}\) 使得 \(z \geq_T x\)。

证明. 令 \(x \in L\)。根据推论 3.3.8，存在 \(a < (\omega_1)^L\) 使得 \(x \in L_{a+1} \setminus L_a\)。那么对于某些 \(n\)，\(x\) 是 \(\Sigma_n(L_{a+1})\)。根据定理 3.4.11，存在实数 \(z \in L_{a+1} \setminus L_a\)，它是 \(\Sigma_n\)-主代码。因此 \(\rho_a^L = \omega\)。根据 \(\Sigma_n\)-主代码的定义，存在 \(a\) 的 \(z\)-递归良序。换句话说，\(\omega_1^x > a\)。因此 \(z \in L_{\omega_1^x}\) 且 \(x \leq_T z\)。

**命题 4.3.5.** 存在 \(x \in \mathbb{C}\)，使得其中每个 \(\Pi^1_1\)-单子都是递归的。

证明. 根据命题 4.1.3，每个 \(\Pi^1_1\)-单子都在 \(L\) 中。由于 \((L, \in) \vDash \text{ZFC}\)，陈述 "只有可数个 \(\Pi^1_1\)-单子" 在 \(L\) 中为真。因此存在实数 \(y \in L\)，使得 \(L\) 中的每个 \(\Pi^1_1\)-单子在 \(y\) 中都是递归的。根据命题 4.3.4，存在 \(z \in \mathbb{C}\) 使得 \(y \leq_T z\)。

**推论 4.3.6.** (i) \(\mathbb{C}\) 是最大可数 \(\Pi^1_1\)-实数集当且仅当 \((\omega_1)^L < \omega_1\)。 (ii) 存在不可数稀疏 \(\Pi^1_1\)-集当且仅当 \((\omega_1)^L = \omega_1\)。

证明. (i) 根据命题 4.3.4，如果 \(\mathbb{C}\) 是可数的，则 \(L \cap 2^\omega\) 是可数的。因此 \((\omega_1)^L\) 是可数的。假设 \((\omega_1)^L\) 是可数的。那么根据命题 4.3.2，每个可数 \(\Pi^1_1\)-实数集都是 \(\mathbb{C}\) 的子集。根据推论 3.3.8，\(\mathbb{C}\) 是可数的。 (ii) 由 (i) 得出。

#### 4.3.3 练习

**练习 4.3.1.** 证明如果 \(\omega_1 = (\omega_1)^L\)，则不存在最大可数 \(\Pi^1_1\)-实数集。

## 4.4 \(\Sigma^1_2\)-集

实数的 \(\Sigma^1_2\)-集和 \(\Pi^1_2\)-集在多个方面相似。我们在此列举其中一些。

**推论 4.4.1.** \(2^\omega \cap L\) 是 \(\Sigma^1_2\)。

证明. 根据命题 4.3.4，\(x \in L\) 当且仅当存在 \(y \in \mathbb{C}\) 使得 \(y \geq_T x\)。

**命题 4.4.2.** \(x \leq_L y\) 是 \(\Sigma^1_2\)-关系。

证明. \(x \leq_L y\) 当且仅当 \(x, y \in L\) 且存在二元关系 \(E \subseteq \omega\)，使得

- \((\omega, E)\) 是良基的；
- \((\omega, E) \models V = L + \text{KP}\)；
- \((\omega, E) \models x \leq_L y\)。

因此关系 \(x \leq_L y\) 是 \(\Sigma^1_2\)。





以下是针对 \(\Sigma^1_2\)-集的 Spector–Gandy 定理的类比。

### 命题 4.4.3.
一个集合 \(A \subseteq 2^\omega\) 是 \(\Sigma^1_2\) 当且仅当存在一个 \(\Sigma_1\)-公式 \(\varphi\) 使得

\[
x \in A \Leftrightarrow \langle L[x], \in \rangle \vDash \varphi \Leftrightarrow \langle L_{(\omega_1)^x}[x], \in \rangle \vDash \varphi.
\]

证明. 假设 \(A \subseteq 2^\omega\) 是 \(\Sigma^1_2\)。那么存在一个 \(\Pi^1_1\)-关系 \(B \subseteq 2^\omega \times 2^\omega\) 使得

\[
x \in A \Leftrightarrow (\exists y) B(x, y).
\]

根据推论 3.7.2，存在一个 \(\Sigma_1\)-公式 \(\psi\) 使得

\[
B(x, y) \Leftrightarrow \langle L_{(\omega_1)^x}[x, y], \in \rangle \vDash \psi.
\]

由于对每个 \(x\)，\(B_x = \{y \mid B(x, y)\}\) 是 \(\Pi^1_1(x)\)，通过相对化定理 4.1.2，存在一个 \(y \in B_x\) 使得 \(y \in L_{(\omega_1)^x}[x]\)。

因此

\[
x \in A \Leftrightarrow (\exists y)(y \in L_{(\omega_1)^x}[x] \land \langle L_{(\omega_1)^x}[x], \in \rangle \vDash \psi).
\]

现在令 \(\varphi\) 为

\[
(\exists \beta)(\exists \alpha > \omega)(\alpha \text{ is the least admissible ordinal such that}
\]

\[
y \in L_\alpha[x] \land \langle L_\alpha[x], \in \rangle \vDash \psi).
\]

根据定理 3.3.2，\(\varphi\) 是 \(\Sigma_1\)。根据上述讨论，\(x \in A\) 当且仅当 \(\langle L[x], \in \rangle \vDash \varphi\) 当且仅当 \(\langle L_{(\omega_1)^x}[x], \in \rangle \vDash \varphi\)。

对于逆方向，假设存在一个 \(\Sigma_1\)-公式 \(\varphi\) 使得 \(x \in A \Leftrightarrow \langle L[x], \in \rangle \vDash \varphi\)。那么对于每个 \(x\)，存在一个基数 \(\alpha\) 使得 \(x \in A \Leftrightarrow \langle L_\alpha[x], \in \rangle \vDash \varphi\)。

根据凝聚定理（3.3.7），存在一个可数可接受序数 \(\alpha\) 使得 \(x \in A \Leftrightarrow \langle L_\alpha[x], \in \rangle \vDash \varphi\)。由于 \(\varphi\) 是 \(\Sigma_1\)，我们有 \(x \in A \Leftrightarrow \langle L[x], \in \rangle \vDash \varphi \Leftrightarrow \langle L_{(\omega_1)^x}[x], \in \rangle \vDash \varphi\)。

根据定理 3.3.4，\(\langle L_{(\omega_1)^x}[x], \in \rangle \vDash \varphi\) 当且仅当存在一个可数传递良基模型 \(\langle M, \in \rangle \vDash \text{KP} + \text{“}V = L[x]\text{”} + \varphi\)。因此 \(\langle L_{(\omega_1)^x}[x], \in \rangle \vDash \varphi\) 当且仅当

\[
(\exists E)(\langle \omega, E \rangle \text{ codes a wellfounded transitive model } \land \langle \omega, E \rangle \vDash \text{KP} + \text{“}V = L[x]\text{”} + \varphi).
\]

根据命题 3.6.2，集合 \(\{x \mid \langle L_{(\omega_1)^x}[x], \in \rangle \vDash \varphi\} = \{x \mid \langle L[x], \in \rangle \vDash \varphi\}\) 是 \(\Sigma^1_2\)。

因此可以将 \(L_{\omega_1}\) 视为 \(\Sigma^1_2\)-集所基于的结构。从某种意义上说，\(\Sigma^1_2\)-性划定了递归理论与集合论之间的边界。在 ZFC 内，无法将前几节的结果推广到超越 \(\Sigma^1_2\) 的层次。为此需要额外的集合论假设。如何实现这一点是描述集合论的一个主要课题。从这个角度看，高阶递归理论作为研究超越 \(\Sigma^1_2\) 层次的描述集合论的一个跳板。令

\[
\delta^1_2 = \text{supremum of the } \Delta^1_2 \text{ well-orderings of } \omega,
\]

和

\[
\delta = \min\{\alpha \mid L \setminus L_\alpha \text{ contains no } \Pi^1_1\text{-singleton}\}.
\]

### 命题 4.4.4. \(\delta = \delta^1_2\).

证明. 如果 \(\alpha < \delta\)，那么存在一个 \(\Pi^1_1\)-单点 \(x \in L_\delta \setminus L_\alpha\)。由于 \(x \in L_{\omega_1^x}\) 且 \(\omega_1^x\) 是一个 \(\Pi^1_1(x)\) 良序，\(\alpha < \omega_1^x < \delta^1_2\)。故 \(\delta \le \delta^1_2\)。

如果 \(\alpha < \delta^1_2\)，那么存在一个类型为 \(\alpha\) 的 \(\Delta^1_2\) 良序关系 \(R \subseteq \omega \times \omega\)。那么存在算术关系 \(S, T \subseteq (\omega^\omega)^2 \times \omega^2\) 使得

\[
R(n, m) \Leftrightarrow (\exists f)(\forall g)S(f, g, n, m),
\]

和

\[
\neg R(n, m) \Leftrightarrow (\exists f)(\forall g)T(f, g, n, m).
\]

定义 \(\Pi^1_1\)-集

\[
R_0 = \{\langle h, (n, m) \rangle \mid h(0) = 0 \land (\exists f)(\forall g)(S(f, g, n, m) \land (\forall n)(f(n) = h(n+1)))\}.
\]

和

\[
R_1 = \{\langle h, (n, m) \rangle \mid h(0) = 1 \land (\exists f)(\forall g)(T(f, g, n, m) \land (\forall n)(f(n) = h(n+1)))\}.
\]

根据 \(\Pi^1_1\)-一致化定理（4.2.1），这两个关系可以由部分 \(\Pi^1_1\)-函数 \(p_{R_0}\) 和 \(p_{R_1} : \omega \to \omega^\omega\) 统一。令 \(p = p_{R_0} \cup p_{R_1}\)。那么 \(p\) 是一个全态 \(\Pi^1_1\)-函数，可以视为一个 \(\Pi^1_1\)-单点。那么 \(R\) 在 \(p\) 中是算术的，因此 \(\alpha < \omega_1^p < \delta\)。故 \(\delta^1_2 = \delta\)。

这给出了针对 \(\Sigma^1_2\)-集的 Spector–Gandy 定理的一个更精细版本：

### 命题 4.4.5. 一个实数 \(x\) 是 \(\Sigma^1_2\) 当且仅当 \(x\) 可以在 \(\langle L_{\delta^1_2}, \in \rangle\) 上以 \(\Sigma_1\) 方式定义。

证明. 假设 \(x\) 是 \(\Sigma^1_2\)。那么存在一个 \(\Sigma_0\)-公式 \(\varphi(n, y)\) 使得

\[
n \in x \Leftrightarrow (\exists y)(\langle L_{\delta^1_2}[y], \in \rangle \vDash \varphi(n, s, y)).
\]

根据推论 4.2.9 和命题 4.4.4，我们有

\[
n \in x \Leftrightarrow \langle L_{\delta^1_2}, \in \rangle \vDash (\exists s)(\exists y)[s \in L_{\omega_1^y}[y] \land \varphi(n, s, y)].
\]

假设 \(\langle L_{\delta^1_2}, \in \rangle \vDash (\exists s)(\exists y)[s \in L_{\omega_1^y}[y] \land \varphi(n, s, y)]\) 并修正这样的一个实数 \(y\)。那么 \(\langle L_{\omega_1^y}[y], \in \rangle \vDash (\exists s)\varphi(n, s, y)\)。故 \(n \in x\)。因此 \(x\) 可以在 \(\langle L_{\delta^1_2}, \in \rangle\) 上以 \(\Sigma_1\) 方式定义。

反之，假设 \(x\) 可以通过公式 \(\varphi(n)\) 在 \(\langle L_{\delta^1_2}, \in \rangle\) 上以 \(\Sigma_1\) 方式定义。根据命题 4.4.4，\(n \in x\) 当且仅当存在一个 \(z \in L_{\omega_1^x}\) 使得 \(\langle L_{\omega_1^x}[x], \in \rangle \vDash \varphi(n)\)。因此 \(x\) 是 \(\Sigma^1_2\)。

可以以显而易见的方式相对化 "$\Delta^1_2$-性" 并在 \(y\) 中定义关系 "$x$ 是 $\Delta^1_2$"，从而引入 \(\Delta^1_2\)-度的概念。令 \(\delta^{1,x}_2\) 为所有在 \(x\) 中是 \(\Delta^1_2\) 的 \(\omega\) 的良序的上确界。以下结果从强意义上说，Post 问题对 \(\Delta^1_2\)-度有否定解。

### 命题 4.4.6.

- (i) 如果 \(x\) 是可构的且不是 \(\Delta^1_2\)，那么 \(\delta^{1,x}_2 > \delta^1_2\)。
- (ii) 假设 \(V = L\)。那么 \(\le_{\Delta^1_2}\) 是 \(\Delta^1_2\)-度的一个良序，其序类型为 \(\omega_1\)。而且，如果 \(x <_{\Delta^1_2} y\)，那么 \(\delta^{1,x}_2 < \delta^{1,y}_2\)。

证明. (i) 令 \(A = \{r \mid r \text{ codes a well-ordering of } \omega \land x \in L_{|r|}\}\)，其中 \(|r|\) 表示 \(r\) 作为良序的序类型。那么 \(A\) 是 \(\Delta^1_2(x)\)。令 \(r \in A\)。由于 \(x\) 不是 \(\Delta^1_2\)，我们必须有 \(|r| > \delta^1_2\)。故 \(\delta^{1,x}_2 > \delta^1_2\)。

(ii) 如果 \(V = L\)，那么根据命题 4.4.2，\(\le_L\) 是实数的一个 \(\Delta^1_2\) 良序。假设 \(x \le_L y\)。那么根据 (i) 的证明，存在一个 \(\Delta^1_2(y)\)-实数 \(r\) 对 \(\omega\) 的良序进行编码，使得 \(y \in L_{|r|}\) 并且因此 \(x \in L_{|r|}\)。那么 \(x \in L_{\omega_1^x}\) 并且因此 \(x \le_{\Delta^1_2} y\)。所以 \(x \le_{\Delta^1_2} y\)。因此 \(\le_{\Delta^1_2}\) 是 \(\Delta^1_2\)-度的一个良序，其序类型为 \(\omega_1\)。如果 \(x <_{\Delta^1_2} y\)，那么通过与 (i) 中相同的论证但相对化到 \(y\)，我们有 \(\delta^{1,x}_2 < \delta^{1,y}_2\)。

命题 4.4.6 表明，虽然 \(L\) 是高算术理论的一个合适基模型，但对于 \(\Delta^1_2\)-理论来说则不那么合适，因为 \(\le_{\Delta^1_2}\) 关系的良序使得相应的度的结构相对简单，因此不那么有趣。

### 4.4.1 练习

- 练习 4.4.1 (Solovay [149] 和 Mansfield [87]). 证明每个包含不可构实数的 \(\Sigma^1_2\)-实数集都有一个完美子集。

- 练习 4.4.2. \(2^\omega \cap L\) 是最大的可数 \(\Sigma^1_2\)-实数集当且仅当 \((\omega_1)^x < \omega_1\)。

- 练习 4.4.3. 如果 \(\omega_1 = (\omega_1)^x\)，那么不存在最大的可数 \(\Sigma^1_2\)-实数集。

- 练习 4.4.4. 证明存在一个实数 \(x\) 和一个非空 \(\Pi^1_2\)-集 \(P \subseteq 2^\omega\) 使得 \(\delta^{1,x}_2 > \delta^1_2\) 但不存在实数 \(z \in P\) 使得 \(z \le_{\Delta^1_2} x\)。

- 练习 4.4.5. 假设 \(\mathcal{L}\) 是一个可数语言且 \(T\) 是 \(\mathcal{L}\) 的一个一致理论。那么 \(T\) 至初等等价要么有 \(\le \aleph_0\) 个，要么有 \(2^{\aleph_0}\) 个可数模型。





## 5 递归论强迫法

虽然科恩最初是出于集合论考虑引入强迫法，但该方法很快由费弗曼 [25] 改编用于研究递归论问题（事实上，在 1950 年代证明的关于图灵度结构的波斯特和克莱尼定理中，人们确实可以察觉到科恩强迫法的痕迹）。这里我们研究三种经典的强迫法示例（分别由科恩、萨克斯和斯蒂尔提出）及其在递归论中的应用。事实证明，分层解析层次为这一目的提供了理想的平台。

### 5.1 分层解析层次

#### 5.1.1 结构 $\mathfrak{A}(\omega_1^{CK}, x)$

分层解析层次由克莱尼 [72] 引入，其上的强迫构造可追溯至科恩 [18] 并由费弗曼 [25] 继续发展。它可以被视为在二阶算术语言中定义的可构层次的类比，用于研究高算术理论。

- 层次的语言，记作 $\mathscr{L}(\omega_1^{CK}, x)$，由以下内容组成：
  - 数变量：$i, j, k, m, n, \dots$
  - 数字：$0, 1, 2, \dots$
  - 集合常量：$\dot{x}, \dot{y}, \dots$
  - 分层集合变量：$x^\beta, y^\beta, \dots$（其中 $\beta < \omega_1^{CK}$）
  - 未分层集合变量：$x, y, \dots$
  - 函数和关系符号：$+, \dots$（乘法）、$'$（后继）和 $\epsilon$。

该语言中的公式以通常的方式通过归纳定义。正如人们所料，分层集合变量的存在意味着 $\mathscr{L}(\omega_1^{CK}, x)$ 没有递归编码。相反，编码是在可数可容集 $L_{\omega_1^{CK}}$ 中进行的。首先，根据定理 2.6.4，选择一条通过 $\mathsf{O}$ 的 $\Pi^1_1$-路径 $\mathsf{O}_1$。用数 $(2, n)$ 编码分层集合变量 $x^\beta$，其中 $n \in \mathsf{O}_1$ 且 $|n| = \beta$。其他符号以递归方式编码。这样一来，公式就在 $L_{\omega_1^{CK}}$ 中被编码。如果一个公式的所有集合变量都是分层的，则称该公式是 *分层的*。如果分层公式 $\varphi$ 满足以下条件，则称其秩至多为 $\beta$：

- 对于任何 $\gamma_i$，如果 $x^i$ 是 $\varphi$ 中出现的自由变量，则 $\gamma \le \beta$；
- 对于任何 $\gamma_i$，如果 $x^i$ 是 $\varphi$ 中出现的受限变量，则 $\gamma < \beta$。

请注意：

- 公式的 Gödel 数集合是 $\Pi^1_1$；
- 秩至多为 $\beta$ 的分层公式的 Gödel 数集合在 $\mathsf{O}_1$ 中 $\beta$ 的唯一记法下一致可枚举。

根据定理 1.3.4，存在一个递归函数 $h$，使得对于 $n \in O_1$，$W_{h(n)}$ 是秩至多为 $|n|$ 的分层公式的 Gödel 数集合。

我们现在定义结构 $\mathcal{A}(\omega_1^{CK}, x) = \bigcup_{\beta < \omega_1^{CK}} \mathcal{A}(\beta, x)$，其中 $x$ 是一个解释 $x$ 的实数。$\mathcal{A}(\omega_1^{CK}, x)$ 是一组以类似于哥德尔 $L$ 的方式定义的实数的集合。该构造在 $\omega_1^{CK}$ 个阶段中完成。任何分层集合变量 $x^\rho$ 都应由 $\bigcup_{y < \beta} \mathcal{A}(y, x)$ 中的一个实数来解释。以此为约定，对于秩至多为 $\beta$ 的分层公式 $\varphi$，满足关系 $\bigcup_{y < \beta} \mathcal{A}(y, x) \models \varphi$ 是明确定义的。我们通过对递归序数进行归纳来定义 $\mathcal{A}(\omega_1^{CK}, x)$，如下：

$\mathcal{A}(0, x) = \{x\} \cup \omega$.

假设 $\beta > 0$ 且对于所有 $y < \beta$，$\mathcal{A}(y, x)$ 已定义。给定一个秩至多为 $\beta$ 且唯一自由变量为 $n$ 的分层公式 $\varphi(n)$，令

$i \in Z_\varphi \Leftrightarrow \bigcup_{y < \beta} \mathcal{A}(y, x) \models \varphi(i)$.

令 $B$ 为这样的 $\varphi$ 对应的实数 $z_\varphi$ 的集合。设

$\mathcal{A}(\beta, x) = \bigcup_{y < \beta} \mathcal{A}(y, x) \cup B$.

因此，在阶段 $\beta$ 构造的实数正是由早期阶段构造的实数算术定义的那些实数。

对于公式 $\varphi$，满足关系 $\mathcal{A}(\omega_1^{CK}, x) \models \varphi$ 通过归纳定义：

- 如果 $\varphi$ 是秩至多为 $\beta$ 的分层公式，则 $\mathcal{A}(\omega_1^{CK}, x) \models \varphi$ 当且仅当 $\bigcup_{y < \beta} \mathcal{A}(y, x) \models \varphi$；
- 如果 $\varphi$ 是 $(\exists z)\varphi(z)$，则 $\mathcal{A}(\omega_1^{CK}, x) \models \varphi$ 当且仅当存在一个 $\beta < \omega_1^{CK}$ 和一个 $z^\beta$，使得 $z^\beta \in \mathcal{A}(\omega_1^{CK}, x)$ 且 $\mathcal{A}(\omega_1^{CK}, x) \models \varphi(z^\beta)$；
- 如果 $\varphi$ 是 $\neg \psi$，则 $\mathcal{A}(\omega_1^{CK}, x) \models \varphi$ 当且仅当 $\mathcal{A}(\omega_1^{CK}, x) \not\models \psi$。

$\mathcal{L}(\omega_1^{CK}, x)$ 中的一个句子 $\varphi$ 是 $\Sigma_1^1$ 的，当且仅当它是分层的，或形如 $(\exists x_1)\cdots(\exists x_n)\psi$，其中 $\psi$ 是某个没有被量词约束的未分层集合变量的公式。不难看出，$\Sigma_1^1$-句子的 Gödel 数集合是 $\Pi_1^1$。令 “$\varphi$” 为公式 $\varphi$ 的代码。

**定理 5.1.1.** 集合 $\{(x, \text{“}\varphi\text{”}) \mid \varphi \text{ 是 } \Sigma_1^1 \land \mathcal{A}(\omega_1^{CK}, x) \models \varphi\}$ 是 $\Pi_1^1$。

*证明.* 通过 $\Sigma$-归纳（定理 3.1.8）和 $\mathcal{A}(\omega_1^{CK}, x)$ 的定义，存在一个 $\Sigma_1$-公式 $\psi(u)$，使得 $(L_\omega[x], x) \models \psi(u^{\text{“}\varphi\text{”}})$ 当且仅当 $\varphi$ 是分层的 $\land \mathcal{A}(\omega_1^{CK}, x) \models \varphi$。因此，根据 Spector-Gandy 定理（3.2.2），集合 $\{(x, \text{“}\varphi\text{”}) \mid \varphi \text{ 是分层的} \land \mathcal{A}(\omega_1^{CK}, x) \models \varphi\}$ 是 $\Pi_1^1$。现在，如果 $\varphi$ 是形如 $(\exists z)\varphi(z)$ 的形式，则 $\mathcal{A}(\omega_1^{CK}, x) \models (\exists z)\varphi(z)$ 当且仅当存在一个 $n \in O_1$，使得 $\mathcal{A}(\omega_1^{CK}, x) \models (\exists z|n)\varphi(z^{\omega[n]})$。由此可见，集合 $\{(x, \text{“}\varphi\text{”}) \mid \varphi \text{ 是 } \Sigma_1^1 \land \mathcal{A}(\omega_1^{CK}, x) \models \varphi\}$ 是 $\Pi_1^1$。

**推论 5.1.2.** 对于 $\beta < \omega_1^{CK}$，集合 $\{(x, \text{“}\varphi\text{”}) \mid \text{rank}(\varphi) \text{ 至多为 } \beta \land \mathcal{A}(\omega_1^{CK}, x) \models \varphi\}$ 是 $\Delta_1^1$。

*证明.* 请注意，集合 $\{\ulcorner \varphi \urcorner \mid \text{rank}(\varphi) \text{ 至多为 } \beta\}$ 是可枚举的，因此是 $\Delta_1^1$。根据定理 5.1.1，集合 $\{(x, \ulcorner \varphi \urcorner) \mid \text{rank}(\varphi) \text{ 至多为 } \beta \land \mathfrak{A}(\omega_1^{CK}, \mathbf{x}) \models \varphi\}$ 和 $\{(x, \ulcorner \varphi \urcorner) \mid \text{rank}(\varphi) \text{ 至多为 } \beta \land \mathfrak{A}(\omega_1^{CK}, \mathbf{x}) \models \neg \varphi\}$ 均为 $\Pi_1^1$，因此也是 $\Delta_1^1$。

#### 5.1.2 刻画 $\mathfrak{A}(\omega_1^{CK}, \mathbf{x})$

**命题 5.1.3.** 对于任意实数 $z$，$z \in \mathfrak{A}(\omega_1^{CK}, \mathbf{x})$ 当且仅当存在一个 $m \in \mathbb{O}$，使得 $z \le_T H_m^x$。

*证明.* 假设 $z \in \mathfrak{A}(\omega_1^{CK}, \mathbf{x})$。那么存在一个分层公式 $\varphi(n)$，使得 \( n \in z \Leftrightarrow \mathfrak{A}(\omega_1^{CK}, \mathbf{x}) \models \varphi(n) \)。

根据推论 5.1.2，集合 \( C = \{\langle x, n \rangle \mid \mathfrak{A}(\omega_1^{CK}, \mathbf{x}) \models \varphi(n)\} \) 是 $\Delta_1^1$。根据 $\Pi_1^1$-一致化定理（4.2.1），存在一个全态的 $\Pi_1^1$ 且因此也是 $\Delta_1^1$ 的函数 \( f : 2^\omega \to \omega \)，使得 $f(x) = m$ 当且仅当 $m \in O^x$ 且 \( (\exists \beta)(\forall n)(n, x \in C \leftrightarrow \mathfrak{A}_m^{f(x)}(n) = 1) \)。根据相对化的 $\Sigma_1^1$-有界性（推论 1.5.2），存在一个序数 \( \beta < \omega_1^{CK} \)，使得对所有 $x$ 都有 \( f(x)|_x \le \beta \)。因此，如果 $z \in \mathfrak{A}(\omega_1^{CK}, \mathbf{x})$，那么存在一个 $m \in \mathbb{O}$，使得 $z \le_T H_m^x$。

反之，假设存在一个 $m \in \mathbb{O}$，使得 $z \le_T H_m^x$。只需证明 \( H_m^x \in \mathfrak{A}(m|1+2, \mathbf{x}) \)。我们通过对 $|m|$ 进行归纳来证明这一点。

假设 $m = 2^n$。那么 \( H_m \in \mathfrak{A}(m|1+x) \)。所以 \( H_m^x \in \mathfrak{A}(m|1+2, \mathbf{x}) \)。

假设 $m = 3 \cdot 5^n$ 且对于所有 $n < m$ 都有 \( H_n^x \in \mathfrak{A}(\omega_1^{CK}, \mathbf{x}) $。那么 $i \in H_m^x$ 当且仅当

\(\mathfrak{A}(m|1+x) \equiv (\exists m'(\exists \beta)[\exists \beta](\hat{H}(f_C(\mathbf{l}), z^{m'|\mathbf{l}}, \mathbf{x}) \wedge \mathbf{l} = \langle j, l \rangle \wedge j \ge z^{m'}])\)。

因此 \( H_m^x \in \mathfrak{A}(m|1+2, \mathbf{x}) \)。

定理 2.3.3 和命题 5.1.3 立即给出以下结论

**推论 5.1.4.** 假设 \( \omega_1^x = \omega_1^{CK} \)。那么对于任意 $z$，$z \in \mathfrak{A}(\omega_1^{CK}, \mathbf{x})$ 当且仅当 $z \le_h x$。特别是，$z$ 是高算术的当且仅当 $z \in \mathfrak{A}(\omega_1^{CK}, \emptyset)$。

#### 5.1.3 $\Delta_1^1$-理解公理

$\Delta_1^1$-理解公理方案陈述如下：

\( (\forall n)((\exists z)\varphi(n, z) \to (\forall z)\psi(n, z)) \to (\exists y)(\forall n)(n \in y \leftrightarrow (\exists z)\varphi(n, z)) \)。

其中 $\varphi(n, z)$ 和 $\psi(n, z)$ 均为算术公式。在强迫构造中，在 $\mathfrak{A}(\omega_1^{CK}, \mathbf{x})$ 中满足 $\Delta_1^1$-理解公理用于保证 $\omega_1^x = \omega_1^{CK}$，如下列定理所示。

**定理 5.1.5.** \(\omega_1^x = \omega_1^{CK}\) 当且仅当 $\mathfrak{A}(\omega_1^{CK}, \mathbf{x})$ 满足 $\Delta_1^1$-理解公理。




证明。如果 \(\omega_1^\alpha = \omega_1^{CK}\)，则由推论 5.1.4，对于任意实数 \(z\)，\(z \in \mathfrak{A}(\omega_1^{CK}, x)\) 当且仅当 \(z \le_h x\)。现在假设 \(\mathfrak{A}(\omega_1^{CK}, x) \vDash (\forall n)((\exists z)\varphi(n, z) \leftrightarrow (\forall z)\psi(n, z))\)。那么对于每个 \(n\)，令 \(f(n)\) 为 \(\mathfrak{A}(\omega_1^{CK}, x) \vDash (\exists z^{[m]})(\varphi(n, z^{[m]})) \lor \neg\psi(n, z^{[m]}))\) 这样的 \(<_{\mathcal{O}^*}\)-最小 \(m \in \mathcal{O}^*\)。\(f\) 是一个全的 \(\Pi_1^1\) 函数，因而也是 \(\Delta_1^1\) 函数。由此可知存在 \(n_0 \in \omega\) 使得对所有 \(n\) 都有 \(f(n) < n_0\)。令 \(y\) 为一个实数，使得 \(n \in y\) 当且仅当 \(\mathfrak{A}(\omega_1^{CK}, x) \vDash \exists z^{[n_0]}(\varphi(n, z^{[n_0]}))\)。那么 \(y \in \mathfrak{A}(\omega_1^{CK}, x)\) 且

\(\mathfrak{A}(\omega_1^{CK}, x) \vDash n \in y \leftrightarrow (\exists z)\varphi(n, z)\)。

假设 \(\mathfrak{A}(\omega_1^{CK}, x)\) 满足 \(\Delta_1^1\)-理解公理。为求矛盾，假设 \(\omega_1^\alpha > \omega_1^{CK}\)。令 \(n \in \mathcal{O}^*\) 满足 \(n = 3 \cdot 5^e\) 且 \(|n|_k = \omega_1^{CK}\)。注意对于 \(m <_{\mathcal{O}^*} n\)，有 \(H_m^\alpha \in \mathfrak{A}(\omega_1^{CK}, x)\)。令 \(\varphi(n, z)\) 为

\((\exists m)(\exists i)[\hat{H}(\hat{\varphi}_{e(m)}^x(m), z, x) \wedge n = \langle m, i \rangle \wedge i \in z]\)。

如果 \(m <_{\mathcal{O}^*} n\)，则 \(\hat{H}_{\varphi^{[m]}}^x\) 是唯一满足 \(\hat{H}(\hat{\varphi}_{e(m)}^x(m), z, x)\) 的实数 \(z\)。因此

\(\mathfrak{A}(\omega_1^{CK}, x) \vDash (\forall n)((\exists z)\varphi(n, z) \leftrightarrow (\forall z)((\exists i)(\langle m, i \rangle = n \wedge i \in z) \to \neg\varphi(n, z))\)。

然后由 \(\Delta_1^1\)-理解，存在 \(y \in \mathfrak{A}(\omega_1^{CK}, x)\) 使得

\(\mathfrak{A}(\omega_1^{CK}, x) \vDash (\forall n)(n \in y \leftrightarrow (\exists z)\varphi(n, z))\)。

由于对于 \(m <_{\mathcal{O}^*} n\) 有 \(\hat{H}_{\varphi^{[m]}}^x \in \mathfrak{A}(\omega_1^{CK}, x)\)，故 \(y = \hat{H}_n^x\)，这与命题 5.1.3 矛盾。

### 注 5.1.16.
上述结果可以推广。例如，可以引入语言 \(\mathscr{L}(\omega_1^x, x, z)\)，定义结构 \(\mathfrak{A}(\omega_1^x, x, z)\)，并表明上述所有结果均成立。那么 \(\{(x, \ulcorner p \urcorner, z) \mid p \in \Sigma_1^x \wedge \mathfrak{A}(\omega_1^x, x, z) \vDash p\} \Pi_1^1\)。此外，\(\mathfrak{A}(\omega_1^x, z)\) 满足 \(\Delta_1^1\)-理解当且仅当 \(\mathfrak{A}(\omega_1^x, x, z)\) 正好是相对于 \(x \oplus z\) 高算术的实数的集合，当且仅当 \(\omega_1^{x \oplus x} = \omega_1^x\)。

#### 5.1.4 练习

### 练习 5.1.1.
证明 \(\mathfrak{A}(\omega_1^{CK}, \emptyset)\) 是满足 \(\Delta_1^1\)-理解公理的最小 \(\omega\)-模型。

### 5.2 科恩强迫

科恩最初的强迫概念是定义在类似于解析分层次结构上的结构之上的，尽管集合论的后续发展已走上不同的道路。对于高算术理论，这个层次是研究强迫最自然的环境。

我们在此考虑的强迫条件集合 \(\mathcal{P}\) 相对简单，例如有限二进制串或高算术编码的完备集。强迫关系 \(\Vdash\) 是一个二元关系，是 \(\mathcal{P} \times \{\varphi \mid \varphi \text{ 是 } \mathcal{L}(\omega_1^{CK}, x) \text{ 中的公式}\}\) 的子集。目标是使 \(\Vdash\) 的定义尽可能简单。例如，当被强迫的公式 \(\varphi\) 是分级的时为高算术，或当 \(\varphi\) 是 \(\Sigma^1_1\) 时为 \(\Pi^1_1\)。通用集 \(x\) 将是通过一组两两兼容条件的并或交运算得到的实数。模型 \(\mathfrak{A}(\omega_1^{CK}, x)\) 于是是 \(\mathfrak{A}(\omega_1^{CK}, \omega)\) 的通用扩展。我们总是使 \(\mathfrak{A}(\omega_1^{CK}, x)\) 满足 \(\Delta^1_1\)-理解，从而 \(\omega_1^x = \omega_1^{CK}\)。有了这一点，就可以构造具有规定性质的通用 \(x\)。

#### 5.2.1 科恩强迫

科恩条件 \(p\) 是一个有限字符串 \(\sigma \in 2^{<\omega}\)，可以将其与基本开集 \([\sigma]\) 识别。定义偏序 \(\le\) 使得 \(p \le q\) 当且仅当 \(p \supseteq q\)。

给定公式 \(\varphi(x)\) 和 \(\psi(n)\)，用 \(\varphi(x \mid \psi)\) 表示将 \(\varphi\) 中每个 \(n \in x\) 的出现替换为 \(\psi(n)\)，并将每个 \(n \notin x\) 的出现替换为 \(\neg\psi(n)\) 所得的公式。

对于句子 \(\varphi \in \mathcal{L}(\omega_1^{CK}, x)\)，通过对 \(\varphi\) 的复杂度进行归纳定义 \(p \Vdash \varphi\)：

- \(p \Vdash \check{n} \in x\) 当且仅当 \(p(n) = 1\)；
- \(p \Vdash t_1 = t_2\) 当且仅当 \(\mathfrak{A}(\omega_1^{CK}, 0) \models t_1 = t_2\)，其中 \(t_1, t_2\) 是仅涉及数字和算术运算的项；
- \(p \Vdash t \in x\) 当且仅当存在某个 \(n\) 使得 \(\mathfrak{A}(\omega_1^{CK}, 0) \models t = \check{n}\) 且 \(p \Vdash \check{n} \in x\)，其中 \(t\) 是仅涉及数字和算术运算的项；
- \(p \Vdash (\exists n)\psi(n)\) 当且仅当存在 \(n \in \omega\) 使得 \(p \Vdash \psi(\check{n})\)；
- \(p \Vdash (\exists \beta < \omega_2^{CK})\dot{\varphi}\) 当且仅当存在秩至多为 \(\beta\) 的分级公式 \(\psi(\check{n})\) 使得 \(p \Vdash \varphi(\dot{\omega}\beta \mid \psi)\)；
- \(p \Vdash (\exists \beta)\dot{\varphi}\) 当且仅当存在 \(\beta < \omega_1^{CK}\) 使得 \(p \Vdash (\exists \beta < \omega_2^{CK})\varphi(\dot{\omega}\beta)\)；
- \(p \Vdash \varphi \lor \psi\) 当且仅当 \(p \Vdash \varphi\) 且 \(p \Vdash \psi\)；
- \(p \Vdash \neg \varphi\) 当且仅当 \(\forall q \le p (q \not\Vdash \varphi)\)。

以下基本事实易于验证。

### 命题 5.2.1.
对于任意公式 \(\varphi\)，
(i) \((\neg p) \Vdash \neg \varphi\);
(ii) \((\forall p)(\exists q \le p)(q \Vdash \varphi \lor q \Vdash \neg \varphi)\);
(iii) \((\forall p)(\forall q \le p)(p \Vdash \varphi \to q \Vdash \varphi)\)。

### 定理 5.2.2.
集合 \(\{(p, \ulcorner \varphi \urcorner) \mid p \Vdash \varphi \land \varphi \text{ 是 } \Pi^1_1\}\) 是 \(\Pi^1_1\)。

证明。注意 \(\Sigma^1_1\)-句子的集合是 \(\Pi^1_1\)，且如果 \((\exists x)\theta(x)\) 是 \(\Sigma^1_1\) 且 \(\theta(x)\) 是算术的，那么 \(p \Vdash (\exists x)\theta(x)\) 当且仅当存在 \(n \in \omega\) 使得 \(p \Vdash \theta(\check{n})\)。由 \(\Sigma\)-归纳定理 (3.1.8) 和强迫的定义，存在集合论语言中的 \(\Sigma^1_1\) 公式 \(\psi(u, v)\)，使得对于 \(\Sigma^1_1\)-句子 \(\varphi\)，\((L_{\omega_1^{CK}}, \in) \models \psi(p, \ulcorner \varphi \urcorner)\) 当且仅当 \(p \Vdash \varphi\)。由 Spector–Gandy 定理 (3.7.1)，集合 \(\{(p, \ulcorner \varphi \urcorner) \mid p \Vdash \varphi \text{ 或 } p \Vdash \neg \varphi\}\) 是 \(\Pi^1_1\)。

集合 \(D \subseteq 2^{<\omega}\) 称为稠密的，如果对于任意 \(p \in 2^{<\omega}\)，存在 \(q \in D\) 使得 \(q \le p\)。给定句子 \(\varphi\)，令 \(D_p = \{p \mid p \Vdash \varphi \lor p \Vdash \neg \varphi\}\)。下一个引理由命题 5.2.1 的 (ii) 得出。

### 引理 5.2.3.
给定公式 \(\varphi\)，\(D_p\) 是稠密的。

实数 \(x\) 是科恩通用的，如果对于任意句子 \(\varphi\)，存在 \(n\) 使得 \(x \Vdash \check{n} \Vdash \varphi\) 或 \(x \Vdash \check{n} \Vdash \neg \varphi\)。由引理 5.2.3 和对公式哥德尔数集合的归纳，很容易证明存在科恩通用实数。下一个定理表明，对于通用实数，强迫等于真理。

### 定理 5.2.4.
假设 \(x\) 是科恩通用的。那么对于任意句子 \(\varphi\)，\(\mathfrak{A}(\omega_1^{CK}, x) \models \varphi\) 当且仅当存在 \(n\) 使得 \(x \Vdash \check{n} \Vdash \varphi\)。

证明。定理的任一方向都可以通过对公式复杂度的归纳来证明。我们展示非平凡情况，即 \(\varphi\) 形如 \(\neg \psi\)。

假设存在 \(n\) 使得 \(x \Vdash \check{n} \Vdash \neg \psi\)。我们声称 \(\mathfrak{A}(\omega_1^{CK}, x) \models \neg \psi\)。否则，由归纳，存在 \(m\) 使得 \(x \Vdash \check{m} \Vdash \psi\)。由引理 5.2.1，\(x \Vdash \check{(m+n)} \Vdash \psi \land \neg \psi\)，这与引理 5.2.1 矛盾。故 \(\mathfrak{A}(\omega_1^{CK}, x) \models \neg \psi\)，即 \(\mathfrak{A}(\omega_1^{CK}, x) \models \varphi\)。

假设 \(\mathfrak{A}(\omega_1^{CK}, x) \models \neg \psi\)。由归纳，对于任意 \(n\) 都有 \(x \Vdash \check{n} \Vdash \psi\)。由于 \(x\) 是科恩通用的，存在 \(m\) 使得 \(x \Vdash \check{m} \Vdash \psi\) 或 \(x \Vdash \check{m} \Vdash \neg \psi\)。故 \(x \Vdash \check{m} \Vdash \neg \psi\)。

### 定理 5.2.5.
如果 \(x\) 是科恩通用的，那么 \(\mathfrak{A}(\omega_1^{CK}, x)\) 满足 \(\Delta^1_1\)-理解。

证明。假设 \(x\) 是科恩通用的，且

\(\mathfrak{A}(\omega_1^{CK}, x) \models (\forall n)(\exists z)\varphi(n, z) \leftrightarrow (\forall z)(\psi(n, z))\)。

其中 \(\varphi(n, z)\) 和 \(\psi(n, z)\) 均为算术公式。那么

\(\mathfrak{A}(\omega_1^{CK}, x) \models (\forall n)(\exists z)(\varphi(n, z) \lor \neg \psi(n, z))\)。

由定理 5.2.4，存在 \(p < x\) 使得

\(p \Vdash (\forall n)(\exists z)(\varphi(n, z) \lor \neg \psi(n, z))\)。

由强迫的定义，

\((\forall q \le p)(q \Vdash (\forall n)(\exists z)(\varphi(n, z) \lor \neg \psi(n, z)))\)。

故

\((\forall q \le p)(\forall n)(q \Vdash (\exists z)(\varphi(n, z) \lor \neg \psi(n, z)))\)。

因此

\((\forall q \le p)(\forall n)(\exists r \le q)(r \Vdash (\exists z)(\varphi(n, z) \lor \neg \psi(n, z)))\)。




根据 \(\Pi_1^1\)-一致化定理（4.2.1），存在一个全定义的 \(\Pi_1^1\) 因而也是 \(\Delta_1^1\)-函数 \(f : \{q \mid q \le p\} \times \omega \to \omega\)，使得 \(f(q, n) = m\) 当且仅当 \(m \in O_1\)，并且存在 \(r \le q\) 使得 \(r \Vdash (\exists z^{[\omega]})(\varphi(n, z^{[n]}) \lor \psi(n, z^{[n]})).\) 令 \(S\) 为 \(f\) 的值域。

根据定理 5.2.2，\(f\) 是一个定义良好的 \(\Pi_1^1\)-函数。由于 \(f\) 在其定义域上是全定义的，故它是 \(\Delta_1^1\)。根据推论 1.5.2，存在 \(n_0 \in O_1\)，使得对任意 \(m \in S\)，都有 \(m <_O n_0\)。则

\((\forall q \le p)(\forall n)(\exists r \le q)(r \Vdash (\exists z^{[\omega]})(\varphi(n, z^{[n_0]}) \lor \neg \psi(n, z^{[n_0]})).\)

故

\((\forall n)(\forall q \le p)(q \Vdash \neg (\exists z^{[n_0]})(\varphi(n, z^{[n_0]}) \lor \neg \psi(n, z^{[n_0]})).\)

且

\((\forall n)p \Vdash \neg (\exists z^{[n_0]})(\varphi(n, z^{[n_0]}) \lor \neg \psi(n, z^{[n_0]})).\)

由于 \(x > p\)，根据定理 5.2.4，

\(\mathfrak{A}(\omega_1^{\text{CK}}, x) \Vdash (\forall n)(\exists z^{[n_0]})(\varphi(n, z^{[n_0]}) \lor \neg \psi(n, z^{[n_0]})).\)

令 \(y\) 满足 \(n \in y\) 当且仅当 \(\mathfrak{A}(\omega_1^{\text{CK}}, x) \Vdash (\exists z^{[n_0]})(\varphi(n, z^{[n_0]}).\) 则 \(y \in \mathfrak{A}(\omega_1^{\text{CK}}, x).\) 现在若 \(n \in y,\) 则 \(\mathfrak{A}(\omega_1^{\text{CK}}, x) \Vdash (\exists z)(\varphi(n, z).\) 若 \(n \notin y,\) 则 \(\mathfrak{A}(\omega_1^{\text{CK}}, x) \Vdash (\exists z^{[n_0]})(\neg \psi(n, z^{[n_0]}).\) 然后根据假设，\(\mathfrak{A}(\omega_1^{\text{CK}}, x) \Vdash (\forall z) \neg \varphi(n, z).\) 因此 \(\mathfrak{A}(\omega_1^{\text{CK}}, x)\) 满足 \(\Delta_1^1\)-理解公理。

推论 5.2.6. 若 \(x\) 是 Cohen 通用的，则

- (i) \(\omega_1^x = \omega_1^{\text{CK}}.\)
- (ii) 对任意实数 \(y \le_{sh} x,\) 存在 \(n \in O\) 使得 \(y \le_T x \oplus H_n.\)

证明. 定理 5.2.5 和定理 5.1.5 直接蕴含 (i).

对于 (ii)，假设 \(y \le_{sh} x.\) 则根据推论 5.1.4 和 (i)，\(y \in \mathfrak{A}(\omega_1^{\text{CK}}, x).\) 根据定理 5.2.4，存在一个分级公式 \(\varphi\)，使得对任意 \(k\)，\(y(k) = 1 \Leftrightarrow (\exists m)(x \mid m \Vdash \varphi(k))\) 且 \(y(k) = 0 \Leftrightarrow (\exists m)(x \mid m \Vdash \neg \varphi(k)).\) 根据定理 5.2.2，

\(R(p, k, i) \equiv (i \wedge 1 \wedge p \Vdash \varphi(k)) \vee (i = 0 \wedge p \Vdash \neg \varphi(k))\)

是 \(\Pi_1^1\). 由于 \(O\) 是 \(\Pi_1^1\)-完全的（定理 1.5.1），存在递归函数 \(f : 2^{<\omega} \times \omega \times 2 \to \omega\)，使得 \(f(p, k, i) \in O\) 当且仅当 \(R(p, k, i)\) 成立。

定义 \(R^* \subseteq \omega \times 2 \times \omega\) 使得 \(R^*(k, i, n)\) 当且仅当 \(n \in O\) 且存在 \(m\) 使得 \(f(x \mid m, k, i) = n.\) 则 \(R^*\) 是 \(\Pi_1^1(x).\) 根据定理 4.2.1，存在一个全定义的 \(\Pi_1^1(x)\)，因而也是 \(\Delta_1^1(x)\)，函数 \(h : \omega \to 2 \times \omega\) 对 \(R^*\) 进行一致化。因此 Range(\(h\)) 是一个 \(\Delta_1^1(x)\)-集合。根据 (i) 和推论 1.5.2，存在 \(n_0 \in O\) 使得 Range(\(h\)) \(\subseteq 2 \times O_{n_0}.\) 因此对任意 \(k\)，\(y(k) = 1 \Leftrightarrow (\exists m)(f(x \mid m, k, 1) \in O_{n_0}),\) 且 \(y(k) = 0 \Leftrightarrow (\exists m)(f(x \mid m, k, 0) \in O_{n_0}).\) 由此可见 \(y \le_T x \oplus O_{n_0},\) 因而存在 \(n \in O\) 使得 \(y \le_T x \oplus H_n.\)

从拓扑角度看，Cohen 通用实数是指与所有可定义稠密开集相交的实数。因此，这样的实数集是非第一类的。在第 14 章中，我们将基于非零测度性质发展出一种平行的强制概念。

#### 5.2.2 超度的应用

我们现在使用 Cohen 强制来研究超度的结构。

**命题 5.2.7.** 若 _z_ 不是超算术的，则存在 _x_ 使得 \(x \not\le_h z\) 且 \(x \not\ge_h z\).

**证明.** 假设 _z_ 不是超算术的。固定在 _z_ 中超算术的实数枚举 \(\{z_i\}_{i<\omega}\) 和所有公式的枚举 \(\{\varphi_i\}_{i<\omega}.\)

我们定义一组条件序列 \(\emptyset = p_0 \ge p_1 \ge \cdots\) 如下：

假设 _p<sub>i</sub>_ 已定义。在第 _i_ + 1 阶段，首先令 \(q_i^1 \le p_i\) 使得存在 _j_ 与 \(q_i^1(j) \neq z(i)\)。然后令 \(q_i^1 \le q_i^0\) 使得 \(q_i^1 \in D_{\varphi_i}\)。根据引理 5.2.3，这是可能的。

检查 \(\varphi_i(n, k)\) 是否为分级公式，以及是否对所有 _n_，都存在 \(r \le q_i^1\) 和 _k_ 使得 \(r \Vdash \varphi_i(n, k)\)。若不存在，令 _p_<sub>_i_+1</sub> = \(q_i^1\) 并进入下一阶段。否则，检查是否对所有 _n_ 和 \(r \le q_i^1\)，若 \(r \Vdash \varphi_i(n, k)\) 则 _k_ 唯一。若如此，令 _p_<sub>_i_+1</sub> = \(q_i^1\) 并进入下一阶段。若不然，令 \(p_{i+1} \le q_i^1\) 使得存在 _n_ 与 \(p_{i+1} \Vdash \varphi_i(n, k)\) 对某些 \(k \neq z(n)\)。

令 \(x = \bigcup_{i<\omega} p_i\)。则 _x_ 是 Cohen 通用的且 \(x \not\le_h z\)。根据推论 5.2.6，\(\omega_1^x = \omega_1^{CK}\)。若 \(x \ge_h z\)，则根据推论 5.1.4，枚举列表中存在一个分级公式 \(\varphi_i(n, k)\)，使得 _z_(_n_) = _k_ 当且仅当 \(\mathfrak{A}(\omega_1^{CK}, x) \Vdash \varphi_i(n, k)\)。根据定理 5.2.4，对每个 _n_，都存在 _k_ 和 _m_ 使得 \(x \mid m \Vdash \varphi_i(n, k)\)。然后根据第 _i_ + 1 阶段的构造，必然对每个 _n_ 和 \(r \le q_i^1\)，存在唯一的 _k_ 满足 \(r \Vdash \varphi_i(n, k)\)。定义 _z_(_n_) = _k_ 当且仅当存在 \(r \le q_i^1\) 使得 \(r \Vdash \varphi_i(n, k)\)。根据定理 5.2.2，_z_ 是 \(\Pi_1^1\) 因而超算术。但 \(z = \hat{z}\)，矛盾。

因此 \(x \not\le_h z\) 且 \(x \not\ge_h z\).

#### 5.2.3 练习

- **练习 5.2.1.** 证明存在 Cohen 通用的 \(x \le_T O^{(\alpha)}\)。
- **练习 5.2.2.** 证明存在实数序列 \(\{x_i\}_{i<\omega}\)，使得对每个 _j_，\(x_j \not\le_h (\{i, n\} \mid n \in x_i \wedge i \neq j)\)。
- **练习 5.2.3.** 证明任何可数偏序集可嵌入超度集合。
- **练习 5.2.4.** 证明作为偏序集的超度的 \(\Sigma_1\)-理论是可判定的。
- **练习 5.2.5.** 证明对任何非超算术 _x_，集合 \(\{y \mid y \not\le_h x \wedge y \not\ge_h x\}\) 是非第一类的。

## 5.3 Sacks 强制

Gandy 和 Sacks [36] 在构造具有最小超度的集合时引入了在解析分层上使用完美集进行强制的概念。然而，完美集强制的起源可追溯至 Spector 关于存在最小 Turing 度的证明 [154]。正如将要看到的，构造最小超度要复杂得多，因为这需要对强制关系 \(\Vdash\) 的复杂性进行详细分析。

#### 5.3.1 解析分层上的完美集强制

令 \(\mathscr{S}\) 为超算术完美集的集合。每个 \(S \in \mathscr{S}\) 都是 Sacks 强制的一个条件。给定两个条件 \(S, T \in \mathscr{S}\)，若 \(S \subseteq T\)，则称 \(S \le T\)。

令 \(\varphi\) 为解析分层语言 \(\mathscr{L}(\omega_1^{CK}, x)\) 中的一个句子。

定义 \(T \Vdash \varphi\) 如下。

- 若 \(\varphi\) 是分级的，则当 \((\forall x \in T)(\exists \alpha(\omega_1^{CK}, x) = \varphi)\) 时，\(T \Vdash \varphi\)；
- 若 \(\varphi(y)\) 是非分级的且存在某个 \(\beta\) 使得 \(T \Vdash \varphi(y \mid \beta)\)，则 \(T \Vdash (\exists y^\beta)\varphi(y)\)；
- \(T \Vdash (\exists y)\varphi(y)\) 当且仅当存在某个 \(\beta < \omega_1^{CK}\) 使得 \(T \Vdash (\exists y^\beta)\varphi(y^\beta)\)；
- 若 \(\varphi(n)\) 是非分级的且存在某个数 _m_ 使得 \(T \Vdash \varphi(\bar{n})\)，则 \(T \Vdash (\exists n)\varphi(n)\)；
- 若 \(\varphi\) 和 \(\psi\) 都是非分级的，且 \(T \Vdash \varphi\) 与 \(T \Vdash \psi\)，则 \(T \Vdash \varphi \land \psi\)；
- 若 \(\varphi\) 是非分级的且 \((\forall S)(S \le T \rightarrow \neg S \Vdash \varphi)\)，则 \(T \Vdash \neg \varphi\)。

需要注意的是，虽然 Cohen 强制对分级句子的定义是通过对句子复杂度进行归纳给出的，但 Sacks 强制的定义是直接给出的。这立即蕴含以下结论。

**引理 5.3.1.** 若 \(T \Vdash \varphi\) 且 \(S \le T\)，则 \(S \Vdash \varphi\).

根据定理 5.1.1 和强制定义，有

**引理 5.3.2.** 集合 \(\{(T, \ulcorner \varphi \urcorner) \mid \varphi \text{ 是 } \Sigma_1^1 \wedge T \Vdash \varphi\}\)

是 \(\Pi_1^1\).

**引理 5.3.3.** (融合引理) 令 \(T\) 为一个条件，\(((i, \varphi_i))_{i < \omega}\) 为一组 \(\Sigma_1^1\) 公式的超算术集合。假设 \((\forall i)(\forall y \in T)(\exists S \le T)(S \Vdash \varphi_i)\)。

则 \((\exists S \le T)(\forall i)(S \Vdash \varphi_i)\).

证明. 使用记号 \(P \Vdash n = \{ \tau \in 2^{<\omega} \mid \tau \in P \}\)，定义 \(\mathfrak{R}\) 为

\(\mathfrak{R}(i, \alpha, R, P) \Leftrightarrow \alpha \in R \wedge P \subseteq R \wedge P \Vdash |\alpha| = \{ \tau \mid \tau < \alpha \} \wedge P \Vdash \varphi_i.\)





注意，$\mathcal{P}$ 是一个 $\Pi^0_1$-关系。那么 $\mathcal{X}$ 可以由一个部分 $\Pi^0_1$-函数 $F : \omega 2^{<\omega} \times \mathscr{S} \to \mathscr{S}$ 一致化。根据假设，对于任何 $R \le T$，$\sigma \in R$ 和 $i \in \omega$，$F(R, i, \sigma)$ 有定义。利用 $F$，一个高算族 $\{P_\sigma \mid \sigma \in 2^{<\omega}\}$ 通过对 $\sigma$ 的递归定义：

$P_0 \vDash T.$

如果 $\sigma \notin P_\sigma$，令 $P_{\sigma 0} = P_{\sigma 1} = \emptyset$。否则，令 $P_{\sigma 0}$ 和 $P_{\sigma 1}$ 为比 $P_\sigma$ 更强的（即包含于 $P_\sigma$ 中的）不相容条件，且 $P_{\sigma 0} \vDash [0]$，$P_{\sigma 1} \vDash [1] = [\sigma] = \{\tau \mid \tau \prec \sigma\}$，使得 $P_{\sigma 0}, P_{\sigma 1} \vDash \lambda_{\sigma \sqcup \rho} \varphi_\rho$。

令 $Q = \bigcup_{\sigma \in P_\sigma} P_\sigma$。那么 $Q \in \mathscr{S}$。

对于每个 $i$ 和 $\sigma \in 2^{i+1}$，要么 $P_\sigma = \emptyset$，要么 $P_\sigma \Vdash \varphi_i$。假设 $\varphi_i$ 的形式为 $(\exists \beta^i)(z)$，其中 $\psi(z)$ 是有秩的。那么当 $P_\sigma \neq \emptyset$ 时，对某些 $\beta_\sigma$，有 $P_\sigma \Vdash (\exists \beta^i)\psi(z^{\beta_\sigma})$。令 $\beta = \bigcup_{\sigma \in 2^{i+1}} \beta_\sigma$。根据强制关系的定义，有 $Q \Vdash (\exists \beta^i)\psi(z^\beta)$。

$\text{故 } (\exists \beta^i)(\varphi_i(z^\beta))$。

因此，对于每个 $i$，有 $Q \Vdash \varphi_i$。

#### Lemma 5.3.4. 对于任何句子 $\varphi$ 和条件 $T$，存在一个 $S \le T$，使得要么 $S \Vdash \varphi$，要么 $S \Vdash \neg \varphi$。

Proof. 如果 $\varphi$ 是无秩的，则该引理直接由定义得出。对于秩为 $\beta$ 的 $\varphi$，我们通过对 $\beta$ 进行归纳来证明该引理。不失一般性，假设 $\varphi$ 的形式为 $(\exists \beta^i)\psi(x^\beta)$，其中 $\psi$ 的秩小于 $\beta$。令 $\{\dot{\varphi}_i(n)\}_{i < \omega}$ 成为所有秩至多为 $\beta$ 且唯一自由变量为 $n$ 的公式的高算枚举。如果存在一个 $i$ 和 $S \le T$ 使得 $S \Vdash \psi(x^\beta \mid \dot{\varphi}_i)$，则证毕。否则，根据 Lemma 5.3.3 和归纳假设，存在一个 $S \le T$，使得对每个 $i$ 都有 $S \Vdash \neg \psi(x^\beta \mid \dot{\varphi}_i)$。那么 $S \Vdash \neg \varphi$。

### 5.3.2 Sacks 泛型实数

一个集合 $D \subseteq \mathscr{S}$ 称为稠密的，如果对于任何条件 $T$，存在一个 $S \in D$ 使得 $S \le T$。一个实数 $x$ 称为 Sacks 泛型的，如果对于任何在 $\emptyset$ 中可算的稠密集合 $D \subseteq \mathscr{S}$，存在一个条件 $T \in \mathscr{S}$ 使得 $x \in [T]$。注意，根据 Lemma 5.3.2 和 Lemma 5.3.4，对于任何句子 $\varphi$，集合 $D_p = \{T \in \mathscr{S} \mid T \Vdash p \text{ 或 } T \Vdash \neg p\}$ 是稠密且在 $\emptyset$ 中可算的。

#### Lemma 5.3.5. 设 $x$ 为 Sacks 泛型且 $x \in [T_0] \cap [T_1]$。那么存在一个 $T \le T_0 \cap T_1$ 使得 $x \in [T]$。

Proof. 令 $i \in \{0, 1\}$。由于 $T_i$ 是高算的，存在一个有秩公式 $\varphi_i$ 使得

$(\forall \sigma)(\sigma \in T_i \leftrightarrow \mathfrak{A}(\omega_1^{\text{CK}}) \models \varphi_i(\sigma))$。

因此，对于 $i < 2$，

$(\forall i < 2)(z \in [T_i] \leftrightarrow \mathfrak{A}(\omega_1^{\text{CK}}, z) \vDash (\forall n)\varphi_i(z \upharpoonright n))$。

由于 \( x \in [T_0] \cap [T_1] \)，

\(\mathfrak{A}(\omega_1^{\text{CK}}, x) \vDash (\forall n)\varphi_0(x \upharpoonright n) \wedge (\forall n)\varphi_1(x \upharpoonright n)\)。

根据 $x$ 的泛型性和有秩公式的强制定义，存在一个条件 $T$ 使得 $x \in [T]$ 且

\( T \vDash (\forall n)\varphi_0(\dot{x} \upharpoonright n) \wedge (\forall n)\varphi_1(\dot{x} \upharpoonright n)\)。

这意味着

\((\forall z)(z \in [T] \Rightarrow \mathfrak{A}(\omega_1^{\text{CK}}, z) \vDash (\forall n)\varphi_0(z \upharpoonright n) \wedge (\forall n)\varphi_1(z \upharpoonright n))\)

因此 $T \le T_0, T_1$。

#### Lemma 5.3.6. 假设 $x$ 是 Sacks 泛型的。那么对于任何句子 $\varphi$，

\(\mathfrak{A}(\omega_1^{\text{CK}}, x) \vDash \varphi \Rightarrow (\exists T)(x \in [T] \land T \Vdash \varphi)\)。

Proof. 如果 $\varphi$ 是有秩的，则根据强制定义，$(\exists T)(x \in [T] \land T \Vdash \varphi)$ 蕴含 \(\mathfrak{A}(\omega_1^{\text{CK}}, x) \vDash \varphi\)。反之，假设 \(\mathfrak{A}(\omega_1^{\text{CK}}, x) \vDash \varphi\)。$x$ 的泛型性蕴含存在一个条件 $T$ 使得 $x \in [T]$ 且要么 $T \Vdash \varphi$，要么 $T \Vdash \neg \varphi$。然后再次根据强制定义，$T \Vdash \varphi$。

如果 $\varphi$ 是无秩的，则可以像在 Theorem 5.2.4 中所做的那样，通过对 $\varphi$ 的复杂性进行归纳来证明该引理。与 Cohen 强制的唯一区别在于当 $\varphi$ 是两个句子的合取时，但这可以通过应用 Lemma 5.5.35 来解决。

#### Lemma 5.3.7. 如果 $x$ 是 Sacks 泛型的，那么 \(\mathfrak{A}(\omega_1^{\text{CK}}, x)\) 满足 \(\Delta_1^1\)-理解公理，因而 \(\omega_1^x = \omega_1^{\text{CK}}\)。

Proof. 假设

\(\mathfrak{A}(\omega_1^{\text{CK}}, x) \vDash (\forall n)(\exists z)\varphi(n, z) \leftrightarrow (\forall z)\psi(n, z),\)

其中 \(\varphi(n, z)\) 和 \(\psi(n, z)\) 都是可算的。

因此

\(\mathfrak{A}(\omega_1^{\text{CK}}, x) \vDash (\forall n)(\exists z)(\varphi(n, z) \vee \neg \psi(n, z))\)。

令 $T$ 为一个条件，使得

\( T \Vdash (\forall n)(\exists z)(\varphi(n, z) \vee \neg \psi(n, z))\)。

根据强制定义，

\((\forall S \le T)(\neg S \Vdash (\exists n)(\neg \exists z)(\varphi(n, z) \vee \neg \psi(n, z)))\)。

因此

\((\forall S \le T)(\forall n)(\neg S \Vdash \neg \exists z(\varphi(n, z) \vee \neg \psi(n, z)))\)，

蕴含

\((\forall P \le T)(\forall n)(\exists S \le P)(S \Vdash \exists z(\varphi(n, z) \vee \neg \psi(n, z)))\)。

根据 Lemma 5.3.3，

\((\exists S \le T)(\forall n)(S \Vdash \exists z(\varphi(n, z) \lor \neg \psi(n, z)))\)。

根据 Lemma 5.3.2，定义一个 \(\Pi^1_1$-关系 \(R \subseteq \omega \times \omega\)，使得 \(R(n, m)\) 当且仅当
\(m \in O_1 \land S \Vdash (\exists z^{|m|})(\varphi(n, z^{|m|}) \lor \neg \psi(n, z^{|m|}))\)。

根据 Theorem 4.2.1，存在一个全态 \(\Pi^1_1$ 因而也是 \(\Delta^1_1$ 的函数 $f$ 一致化 $R$。根据 Corollary 1.5.2，存在一个 $m_0 \in O_1$，使得对任何 $n$，都有 $f(n) \le m_0$，因此
\((\forall n)(S \Vdash (\exists z^{|m_0|})(\varphi(n, z^{|m_0|}) \lor \neg \psi(n, z^{|m_0|})))\)。

因此，对于任何满足 \(T \Vdash (\forall n)(\exists z)(\varphi(n, z) \lor \neg \psi(n, z))\) 的条件 $T$，存在一个 $S \le T$ 和 \(\beta < \omega_1^{\text{CK}}\)，使得
\((\forall n)(S \Vdash (\exists z^\beta)(\varphi(n, z^\beta) \lor \neg \psi(n, z^\beta)))\)。

令

\(\mathcal{D} = \{S \mid S \Vdash \neg(\forall n)(\exists z)(\varphi(n, z) \lor \neg \psi(n, z)) \lor (\exists \beta < \omega_1^{\text{CK}})(S \Vdash (\forall n)(\exists z^\beta)(\varphi(n, z^\beta) \lor \neg \psi(n, z^\beta)))\}\)。

那么 \(\mathcal{D}$ 是一个在 $\mathcal{O}$ 中可算的稠密条件集合。根据 $x$ 的泛型性，存在一个 $T \in \mathcal{D}$ 使得 $x \in [T]$。根据 Lemma 5.3.6 和假设，$T \Vdash \neg(\forall n)(\exists z)(\varphi(n, z) \lor \neg \psi(n, z))$。因此
\(T \Vdash (\forall n)(\exists z^\beta)(\varphi(n, z^\beta) \lor \neg \psi(n, z^\beta))\)

对某些 \(\beta < \omega_1^{\text{CK}}\)。根据强制定义，
\(\mathfrak{A}(\omega_1^{\text{CK}}, x) \vDash (\forall n)(\exists z^\beta)(\varphi(n, z^\beta) \lor \neg \psi(n, z^\beta))\)。

因此，如同 Theorem 5.2.5 的证明中那样，\(\mathfrak{A}(\omega_1^{\text{CK}}, x)\) 满足 \(\Delta^1_1$ 理解公理。

### Theorem 5.3.8 (Gandy 和 Sacks [36]). 假设 $x$ 是 Sacks 泛型的且 $y \le_h x$ 不是高算的。那么 $x \le_h y$，即 $x$ 是一个最小超度的集合。

**Proof.** 假设 $y \le_h x$ 不是高算的。根据 Corollary 5.1.4 和 Lemma 5.3.7，存在一个有秩公式 $\varphi$ 使得
\((\forall n)(y(n) = i \Rightarrow \mathfrak{A}(\omega_1^{\text{CK}}, x) \vDash \varphi(n, i))\)。
根据 Lemma 5.3.6，令 $T$ 为一个条件，使得 $x \in [T]$ 且
\(T \Vdash (\forall n)(\exists i)(i < 2 \land \varphi(n, i))\)。

### Claim. 对于任何 $S \le T$，存在 $Q_i \le S$（$i < 2$）和一个 $n$，使得 $Q_i \Vdash \varphi(\bar{n}, i)$。否则，固定一个 $S$，使得对所有 $Q_i$ 和所有 $n$，都不存在 $Q_0 \Vdash \varphi(\bar{n}, 0)$ 和 $Q_1 \Vdash \varphi(\bar{n}, 1)$ 的情况。那么
\(n \in y \Leftrightarrow (\exists Q \le S)Q \Vdash \varphi(\bar{n}, 0)\)
且
\(n \notin y \Leftrightarrow (\exists Q \le S)Q \Vdash \varphi(\bar{n}, 1)\)，
根据 Lemma 5.3.2 蕴含 $y$ 是高算的，这与假设矛盾。





根据主张和引理 5.3.3，可以定义一个条件 \( S \le T \)，使得

\( (\forall \sigma, \sigma' \in S)(\exists m)(\exists j < 2)(\sigma \upharpoonright j' \to S \cap \sigma \upharpoonright j \neq \varphi(m, j) \land S \cap \sigma \upharpoonright j' \neq \varphi(m, 1 - j)). \)

此外，存在一个高算术函数 \( f \)，将 \( (\sigma, \sigma') \) 映射到适当的 \( (m, j, 1 - j) \)。

\( D_\varphi = \{S \mid S \Vdash \neg(\forall n)(\exists l < 2)\varphi(n, i) \text{ or } S \text{ satisfies } (*)\}.\)

那么 \( D_\varphi \) 是在 \( \mathcal{O} \) 中的一个稠密算术集合。根据对 \( x \) 的假设，存在一个 \( S \in D_\varphi \)，使得 \( x \in [S] \) 且 \( S \) 满足 (*)。在 \( S \) 上定义的函数 \( f \) 有效地分离了 \( [S] \) 中的实数，因此 \( x \) 在 \( y \# f \) 中是递归的。由于 \( f \) 是高算术的，我们得出 \( x \le_h y \).

### 5.3.3 最小超度的 \(\Sigma^1_1\) 集

设 \( \varphi \) 为分级的，且

\( \hat{D}_\varphi = \{S \mid S \Vdash \neg(\forall n)(\exists l < 2)\varphi(n, i) \text{ or } (\forall n)(\exists l < 2)S \Vdash \varphi(n, i) \text{ or } S \text{ satisfies } (*) \text{ defined in the proof of Theorem 5.3.8}.\}\)

若对任意分级的 \( \varphi(n, i) \)，存在一个条件 \( S \in \hat{D}_\varphi \) 使得 \( x \in [S] \)，则称 \( x \) 为弱萨克斯通用。注意集合 \(\{S \mid \forall n,i \, S \in \hat{D}_\varphi \}\) 是 \(\Pi^1_1\)。根据定理 5.3.8 的证明，\(\hat{D}_\varphi\) 对每个分级的 \( \varphi(n, i) \) 都是稠密的。此外，通过定理 5.3.8 的证明，我们有以下引理。

### 引理 5.3.9. 设 \( x \) 为弱萨克斯通用且 \( n \in \mathcal{O} \). 若 \( 0 <_n y \le_T H_n^x \)，则 \( x \le_h y \).

设 \(\{\varphi_\beta\}_{\beta < \omega_1^{ck}}\) 为所有分级句子的 \(\Sigma^1_1(L_{\omega_1^{ck}}(x))\)-枚举。根据融合引理 (5.3.3) 和定理 5.3.8，我们可以通过归纳定义条件集合的 \(\Sigma^1_1(L_{\omega_1^{ck}})\)-枚举 \(\{\mathscr{I}_\beta\}_{\beta < \omega_1^{ck}}\)，使得对任意 \(\gamma < \beta < \omega_1^{ck}\),

- (i) \( (\forall S \in \mathscr{I}_\gamma)(S_0 \in \mathscr{I}_\beta \to S_0 \le S \cap [t_S(0)] \wedge S_1 \le S \cap [t_S(1)]) \), where \( t_S \) is the natural homeomorphic map from \( 2^{<\omega} \) to \( S \);
- (i) 对任意 \( S \in \mathscr{I}_\gamma \)，若 \( S_0 \in \mathscr{I}_\beta \)，则 \( S_0 \le S \cap [t_S(0)] \) 且 \( S_1 \le S \cap [t_S(1)] \)，其中 \( t_S \) 是从 \( 2^{<\omega} \) 到 \( S \) 的自然同胚映射；
- (ii) \( (\forall S \in \mathscr{I}_\beta)(\exists n)(\exists \sigma \in S)(\forall \tau \in S)([S] \subseteq \bigcup_{\sigma \in S}[S_\tau]) \), and
- (ii) 对任意 \( S \in \mathscr{I}_\beta \)，存在 \( n \) 和 \( \sigma \in S \)，使得对任意 \( \tau \in S \)，\([S] \subseteq \bigcup_{\sigma \in S}[S_\tau]\)；以及
- (iii) \( (\forall S \in \mathscr{I}_\beta)(\forall \alpha \in 2^{n+1})(S \cap [t_S(\alpha)] \in \hat{D}_{\varphi_\beta}) \).
- (iii) 对任意 \( S \in \mathscr{I}_\beta \) 和 \( \alpha \in 2^{n+1} \)，\( S \cap [t_S(\alpha)] \in \hat{D}_{\varphi_\beta} \).

设 \(\mathscr{I}_0 = \{2^{<\omega}\}\). 在阶段 \(\beta + 1\)，对任意 \( S \in \mathscr{I}_\beta \)，根据 \(\hat{D}_{\varphi_\beta}\) 的稠密性，令 \( S_0, S_1 \in \hat{D}_{\varphi_\beta} \) 为满足 \( S_0 \le S \cap [t_S(0)] \) 和 \( S_1 \le S \cap [t_S(1)] \) 的 \( <_l \)-最小条件对。令 \( S_0, S_1 \in \mathscr{I}_{\beta+1} \).

在极限阶段 \(\lambda\)，令 \(\{\beta_i\}_{i < \omega}\) 为极限为 \(\lambda\) 的 \( <_l \)-最小递增 \(\omega\)-序数序列。对 \(\beta < \lambda\)，令 \(\beta_i\) 为满足 \(\beta \le \beta_i\) 的最小 \( i \). 根据归纳假设，不难看出存在一个 \( <_l \)-最小融合序列 \(\{S_\alpha\}_{\alpha \in 2^{<\omega}}\)，使得

- - \( S_0 = S \);
- - \( S_0 = S \)；
- - \( (\forall n)(\forall \alpha \in 2^{n+1})(S_\alpha \in \mathscr{I}_{\beta_{|\alpha|}}). \)
- - 对任意 \( n \) 和 \( \alpha \in 2^{n+1} \)，\( S_\alpha \in \mathscr{I}_{\beta_{|\alpha|}} \).

设 \( T = \bigcap_{n<\omega} \bigcup_{n<\omega} S_n \). 将 \( T \cap [\tau_T(0)] \) 和 \( T \cap [\tau_T(1)] \) 放入 \( \mathscr{S}_A \). 留给读者验证 \(\{\mathscr{S}_\beta\}_{\beta < \alpha^{CK}_1}\) 满足 (i)-(iii). 以下是 (iii) 的直接推论。

### **引理 5.3.10.** 若对任意 \( \beta < \omega_1^{CK} \)，存在一个条件 \( S_p \in \mathscr{S}_\beta \) 使得 \( x \in [S_p] \)，则 \( x \) 是弱萨克斯通用.

现在令

\( A = \{(n, x) \mid (\exists S)(x \in [S] \land S \in \mathscr{S}_{\langle n \rangle} \land n \in \omega\} \).

由于每个 \( S \in \mathscr{S}_\beta \) 都是高算术的，根据推论 2.2.12，\( A \) 是 \( \Pi^1_1 \). 此外，对任意 \( n \)，\( A_n = \{x \mid (n, x) \in A\} \) 是 \( \Delta^1_1 \).

### **引理 5.3.11.** \( \bigcap_{n \in \mathcal{O}_1} A_n \) 是一个不可数的 \( \Sigma^1_1 \) 集.

**证明.** 显然 \( \bigcap_{n \in \mathcal{O}_1} A_n \) 是 \( \Sigma^1_1 \). 根据 \(\{\mathscr{S}_\beta\}_{\beta < \alpha^{CK}_1}\) 的定义，对任意 \( n \in \mathcal{O}_1 \)，\( \bigcap_{m < n} A_m \neq \emptyset \). 因此对任意 \( A'_1 \supseteq \mathcal{O}_1 \cap \bigcap_{n \in \mathcal{O}_1} A_n \neq \emptyset \). 根据克雷塞尔紧性定理 (4.2.4)，\( \bigcap_{n \in \mathcal{O}_1} A_n \) 非空。由于该集合的任何元素都不是高算术的，根据引理 2.5.4，它是不可数的。

### **定理 5.3.12** (Simpson [138]). 存在一个不可数的最小超度的 \( \Sigma^1_1 \) 集.

**证明.** 令 \( M = \{x \mid x \notin HYP \land x \in \bigcap_{n \in \mathcal{O}_1} A_n \land \omega^x_1 = \omega_1^{CK}\} \). 那么 \( M \) 是 \( \Sigma^1_1 \) 且根据引理 5.3.11 和甘迪基础定理 (2.5.3)，\( M \) 非空。根据引理 2.5.4，\( M \) 是不可数的。根据引理 5.3.9，每个 \( x \in M \) 都是最小超度.

通过相对化定理 5.3.12 的证明（参见 [138]），可以证明存在一个 \( \Sigma^1_1 \) 集 \( M \subseteq 2^\omega \times 2^\omega \)，使得对任意 \( x \)，存在一个 \( y \) 使得 \( (x, y) \in M \)，且对任意 \( (x, y) \in M \)，\( y \) 的超度是 \( x \) 的超度的最小覆盖。

### 5.3.4 练习

### **练习 5.3.1** (Sacks [123]). 证明 \( x \) 是萨克斯通用当且仅当对每个句子 \( \varphi \)，存在一个 \( S \in D_\varphi \) 使得 \( x \in [S] \).

### **练习 5.3.2** (Simpson [138]). 证明存在两个最小超度的实数 \( x, y \)，使得 \( x \oplus y \geq_T 0 \).

### **练习 5.3.3.** 证明没有弱萨克斯通用实数是高算术的.

### **练习 5.3.4.** 设 \( X \) 为分级句子的 \( \Pi^1_1 \) 集。假设若 \( A \subseteq X \) 是 \( \Delta^1_1 \)，则存在一个 \( x \) 使得 \( \mathfrak{A}(\omega_1^{CK}, x) \) 是 \( A \) 的模型。证明存在一个 \( x \) 使得 \( \mathfrak{A}(\omega_1^{CK}, x) \) 是 \( X \) 的模型.

### **练习 5.3.5** (Simpson [138]). 若存在一个 \( x \) 使得 \( 2^\omega = L(x) \cap 2^\omega \)，则对任意 \( z \)，存在一个 \( y \geq_T z \)，其超度不是任何超度的最小覆盖。

## 5.4 可容序数的刻画

通过相对化推论 3.6.7 的证明，可以证明对任意 \( x \)，\(\omega_1^x\) 是一个可容序数。其逆命题由 Sacks [122] 证明：每个大于 \(\omega\) 的可容序数 \(\alpha\) 都是某个 \( x \) 的 \(\omega_1^x\). 他的证明还产生了一个 \( x \)，使得没有 \( y <_h x \) 满足 \(\omega_1^y = \alpha\). 我们使用 Steel [158] 引入的强迫法概念，证明一个较弱的结果，即存在某个 \( x \) 使得 \(\alpha = \omega_1^x\). 在本节余下部分，设 \(\alpha\) 为大于 \(\omega\) 的可容序数。

### 5.4.1 广义分支解析层次

设 \(\mathfrak{L}(\alpha, x)\) 为由以下部分组成的语言：

- 数变量: $i, j, k, m, n, \dots$
- 数字: $0, \bar{1}, \bar{2}, \dots$
- 常量: $x, y, \dots$
- 分级集变量: $x^\gamma, y^\gamma, \dots$ 其中 \(\gamma < \alpha\)
- 未分级集变量: $x, y, \dots$
- 运算和关系: $+, \cdot, (\text{times}), / (\text{successor})$ 和 $\in$.

公式通过归纳定义。数论项的集合是在数字和数变量上关于 $+, \cdot$ 封闭的项的集合。原子公式是形式为 $t = s$ 和 $t \in x$ 的公式，其中 \(t\) 和 \(s\) 是数论项。其他公式以常规方式生成。若公式的所有集变量都是分级的，则称该公式为 *分级*。若分级公式 \(\varphi\) 满足

- - 对任意 \(\beta\)，若 \(x^\beta\) 是 \(\varphi\) 中出现的自由变量，则 \(\beta \le \gamma\);
- - 对任意 \(\beta\)，若 \(x^\beta\) 是 \(\varphi\) 中出现的约束变量，则 \(\beta < \gamma\).

通过对 \(L_\alpha\) 进行 \(\Sigma\)-归纳，我们有

- - 公式的集合在 \(L_\alpha\) 中是 \(\Sigma_1\);
- - 集合 \(\{(\gamma, \varphi) \mid \varphi \text{ 是秩至多为 } \gamma \text{ 的分级公式}\}\) 在 \(L_\alpha\) 中是 \(\Delta_1\).

给定 \(x\)，现在定义结构 \(\mathfrak{A}(\alpha, x) = \bigcup_{\beta < \alpha} \mathfrak{A}(\beta, x)\)，其中 \(x\) 将符号 \(\dot{x}\) 解释为实数的可数汇集的可数并集。在构造过程中，分级变量 \(x^\gamma\) 将被解释为 \(\bigcup_{\beta < \gamma} \mathfrak{A}(\beta, x)\) 中的一个实数。对于秩至多为 \(\gamma\) 的分级公式 \(\varphi\)，满足关系 \(\bigcup_{\beta < \gamma} \mathfrak{A}(\beta, x) \models \varphi\) 是定义良好的。\(\mathfrak{A}(\alpha, x)\) 通过对小于 \(\alpha\) 的序数进行归纳构造：

- - \(\gamma = 0\): \(\mathfrak{A}(\gamma, x) = t(\gamma) \cup \omega\).
- - \(\gamma > 0\): 假设对所有 \(\beta < \gamma\)，\(\mathfrak{A}(\beta, x)\) 已定义。对于秩至多为 \(\gamma\) 且 \(n\) 为唯一自由变量的分级公式 \(\varphi(n)\)，令

```
$i \in z_\varphi \Leftrightarrow \bigcup_{\beta < \gamma} \mathfrak{A}(\beta, x) \models \varphi(i).$
```



令 B 为这样的 z_p 的集合。设

```
\mathfrak{A}(\gamma, x) = \bigcup_{\beta < \gamma} \mathfrak{A}(\beta, x) \cup B.
```

满足关系 \(\mathfrak{A}(\alpha, x) \vDash \varphi\) 归纳定义如下：

- 若 \(\varphi\) 的秩至多为 \(\gamma\)，则 \(\mathfrak{A}(\alpha, x) \vDash \varphi\) 当且仅当 \(\bigcup_{\beta < \gamma} \mathfrak{A}(\beta, x) \vDash \varphi\)；
- 若 \(\varphi\) 为 \((\exists z)\varphi(z)\)，则 \(\mathfrak{A}(\alpha, x) \vDash \varphi\) 当且仅当存在 \(\gamma < \alpha\) 和 \(z^\gamma\) 使得 \(z^\gamma \in \mathfrak{A}(\alpha, x)\) 且 \(\mathfrak{A}(\alpha, x) \vDash \varphi(z^\gamma)\)；
- 若 \(\varphi\) 为 \(\neg \psi\)，则 \(\mathfrak{A}(\alpha, x) \vDash \varphi\) 当且仅当 \(\mathfrak{A}(\alpha, x) \not\vDash \psi\)。

以下结果的证明留给读者。

### 定理 5.4.1. 若 \(\omega_1^x \ge \alpha\)，则集合 \(\{ (x, \varphi) \mid \varphi \text{ is ranked } \land \mathfrak{A}(\alpha, x) \vDash \varphi \}\) 在 \(L_{\omega_1^x}[x]\) 中是 \(\Delta_1\)。

### 定理 5.4.2. 假设 \(\omega_1^x \ge \alpha\)。则 \(\omega_1^x = \alpha\) 当且仅当 \(\mathfrak{A}(\alpha, x)\) 满足 \(\Delta_1^1\)-理解公理。

### 5.4.2 Steel 强迫

Steel 强迫是一种强迫概念，其条件为带标记的有限树 \(p\)，具有以下性质：

- \(p = (t, h)\)，其中 \(t \subseteq \omega^{<\omega}\) 且 \(h : \tilde{t} \to \alpha \cup \{\infty\}\) 是一个函数，满足 \(h(t) = \infty\) 且 \((\forall \sigma, \tau \in \text{Dom}(h))(\sigma \to_T \tau \Rightarrow h(\sigma) < h(\tau))\)。我们采用约定：对所有 \(\beta < \alpha\)，\(\infty > \beta\)；
- \(p = (\tilde{t}_p, h_p) < q = (\tilde{t}_q, h_q)\) 当且仅当 \(\tilde{t}_q\) 是 \(\tilde{t}_p\) 的子树且 \(h_p \restriction \tilde{t}_q = h_q\)。

固定 \(\omega^{<\omega}\) 的一个递归编码，使得 \(\omega^{<\omega}\) 中的字符串与自然数相识别。由于泛集实数意图为一棵树，我们也用 T 代替 \(\dot{x}\)。
给定句子 \(\varphi \in \mathcal{L}(\alpha, \mathcal{T})\)，通过对 \(\varphi\) 的复杂度进行归纳，定义 \(p = (t_p, h_p) \Vdash \varphi\)：

- \(p \Vdash \sigma \in \dot{T}\) 当且仅当 \(\sigma = \emptyset \lor (\sigma \restriction |\sigma| - 1) \in \tilde{t}_p \land h_p(\sigma \restriction (|\sigma| - 1)) > 0\)；
- \(p \Vdash t_1 = t_2\) 当且仅当 \(\mathfrak{A}(\alpha, 0) \vDash t_1 = t_2\)，其中 \(t_1, t_2\) 为数论项；
- \(p \Vdash t \in \dot{T}\) 当且仅当存在 \(\sigma\) 使得 \(\mathfrak{A}(\alpha, 0) \vDash t = \sigma\) 且 \(p \Vdash \dot{\sigma} \in \dot{T}\)，其中 \(t\) 为数论项；
- \(p \Vdash (\exists n)\varphi(n)\) 当且仅当存在 \(n \in \omega\) 使得 \(p \Vdash \varphi(\bar{n})\)；
- \(p \Vdash (\exists z^\gamma)\varphi(z^\gamma)\) 当且仅当存在秩至多为 \(\gamma\) 的已秩公式 \(\psi(\bar{\eta})\) 使得 \(p \Vdash \varphi(\bar{\eta})\)；
- \(p \Vdash (\exists z)\varphi(z)\) 当且仅当存在 \(\gamma < \alpha\) 使得 \(p \Vdash (\exists z^\gamma)\varphi(z^\gamma)\)；
- \(p \Vdash \varphi \land \psi\) 当且仅当 \(p \Vdash \varphi\) 且 \(p \Vdash \psi\)；
- \(p \Vdash \neg \varphi\) 当且仅当 \((\forall q \le p)(\neg q \Vdash \varphi)\)。

以下基本事实直接从强迫的定义得出。

### 命题 5.4.3. 对于 $p \Vdash \text{sentence } \varphi$，

- (i) $(\forall p)(p \Vdash \varphi \lor \psi \Vdash \neg \varphi)\)；
- (ii) $(\forall p)(\exists q \leq p)(q \Vdash \varphi \lor q \Vdash \neg \phi)\)；
- (iii) $(\forall p)(\forall q \leq p)(p \Vdash \varphi \Rightarrow q \Vdash \varphi)\)。

对上述定义的 $\Vdash$ 的复杂度进行分析并非易事。困难在于，Steel 强迫不同于 Cohen 强迫，本质上是一种“类强迫”。由于标记，强迫条件遍及整个 $L_\alpha$。这使得语句 "$p \Vdash \neg \varphi$" 的复杂度更难确定。因此，我们的主要努力是处理这个问题。

### 定义 5.4.4. 假设 $p, q$ 是条件且 $\gamma < \alpha$。那么 $\text{Ret}(\gamma, p, q)$（即由 $p$ 对 $q$ 进行的重标记）当且仅当：

- $t_p = t_q\)；
- $(\forall o)((h_p(o) < \gamma \lor h_q(o) = 0 \lor h_q(o) = 0) \rightarrow h_p(o) = h_q(o))\)，且
- $(\forall o)(h_p(o) \geq \gamma \rightarrow h_q(o) \geq \gamma)\)。

我们将使用重标记，用更简单的条件来简化复杂条件，同时保持强迫关系。

### 引理 5.4.5. 若 $\gamma_0 < \gamma_1 < \alpha$ 且 $\text{Ret}(\gamma_1, p, q)$，则

$(\forall p_1 \leq p)(\exists q_1 \leq q)\text{Ret}(\gamma_0, p_1, q_1)\)。

### 证明.

考虑 $\gamma_0$ 和 $\gamma_1$ 的原因是为重标记预留一些空间。假设 $\gamma_0 < \gamma_1 < \alpha$ 且 $\text{Ret}(\gamma_1, p, q)\)。令 $p_1 \leq p\)。定义 $q_1$ 如下：

- 令 $t_{q_1} = t_p\)，且
- 情况 (1) \(\sigma \in t_q\) 且 \(h_q(\sigma) < \omega \gamma_0\)。令 \(h_{q_1}(\sigma) = h_q(\sigma)\)；
- 情况 (2) 否则。令 \(h_{q_1}(\sigma) = \omega \gamma_0 + t_{q_1, \sigma}\)，其中 \(t_{q_1, \sigma} = \{ \tau \geq \sigma \mid \tau \restriction t_{q_1} \}\)。
- 留给读者验证 \(q_1\) 符合要求。

不难看出，存在一个双射 \(\Delta_1(L_\alpha)\)-函数 \(f : \{ \varphi \mid \varphi \text{ is ranked} \} \to \alpha\)，使得若 \(\varphi\) 的秩小于 \(\psi\) 的秩，则 \(f(\varphi) < f(\psi)\)。

### 引理 5.4.6. 若 \(f(\varphi) = \gamma\) 且 \(\text{Ret}(\gamma, p, q)\)，则 \(p \Vdash \varphi \leftrightarrow q \Vdash \varphi\)。

### 证明.

我们通过对序数进行归纳来证明该引理。唯一非平凡的情况是 \(\varphi\) 形如 \(\neg \psi\) 且 \(f(\psi) < f(\varphi)\)。假设 \(\text{Ret}(\gamma, p, q)\) 且 \(f(\varphi) = \gamma\)。若 \(p \Vdash \neg \varphi\) 但 \(q \not\Vdash \neg \varphi\)，则 \((\exists p_1 \leq p)(p_1 \Vdash \varphi)\) 但 \((\exists q_1 \leq q)(q_1 \Vdash \neg \varphi)\)。由引理 5.4.5，存在 \(p_2 \leq p\) 使得 \(\text{Ret}(\gamma_1, p_2, q_1)\) 且 \(f(\psi) = \gamma_1 < \gamma\)。由归纳假设，\(p_2 \Vdash \varphi\)，矛盾。故 \(p \Vdash \neg \varphi \leftrightarrow q \Vdash \neg \varphi\)。类似论证表明 \(q \Vdash \varphi \to p \Vdash \varphi\)。

### 定理 5.4.7. 集合 \((\{p, \ulcorner \varphi \urcorner \} \mid p \Vdash \varphi \land \varphi \text{ is ranked})\) 是 \(\Delta_1(L_\alpha)\)。

证明. 假设 \(f(\psi) = \gamma\)。对任意条件 \(p\)，\(p \Vdash \neg \phi\) 当且仅当 \((\forall q \le p)(q \not\Vdash \phi)\)。修正条件 \(q \le p\) 并定义 \(q'\) 使得 \(t_{q'} = t_q\) 且情况 (1) \(t \in t_p\) 或 \(h_q(\sigma) > \omega_\gamma\)。令 \(h_{q'}(\sigma) = h_q(\sigma)\)；情况 (2) 否则。令 \(h_{q'}(\sigma) = \omega_\gamma + t_{q,\sigma}\)，其中 \(t_{q,\sigma} = \{\tau \ge \sigma \mid \tau \in t_q\}\)。故 \(\text{Ret}(\omega_\gamma, q, q')\) 成立。由引理 5.4.6，\(q \Vdash \phi \Leftrightarrow q' \Vdash \phi\)。因此

\((\forall q \le p)(\text{Range}(h_q) \subseteq \cup_{\sigma \in t_q} h_p(\sigma) + \omega \cdot (\gamma + 1)) \to q \Vdash \phi\)。

定理现在通过应用 \(\Sigma\)-归纳定理 (3.1.8) 得证。

令 \(\{D_i\}_{i<\omega}\) 为在 \((L_\alpha, \in)\) 上可定义的所有条件稠密集的枚举。则存在一个序列 \(\{p_i\}_{i<\omega}\)，使得 \(p_0 \ge p_1 \ge \cdots\) 且对每个 \(i\) 有 \(p_i \in D_i\)。令 \(T = \bigcup_{i<\omega} p_i\)，\(h = \bigcup_{i<\omega} h_{p_i}\)。以下引理是直接的。

### 引理 5.4.8. 对任意 \(\gamma < \alpha\)，

- 集合 \(D_0^\gamma = \{p \mid (\exists \sigma)(\sigma \in t_p \land h_p(\sigma) = \gamma)\}\) 是稠密的。
- 集合 \(D_1^\gamma = \{p \mid (\forall \sigma)(\sigma \in t_p \land h_p(\sigma) > \gamma \to (\exists \tau > \sigma)(\tau \in t_p \land h_p(\tau) = \gamma))\}\) 是稠密的。

### 引理 5.4.9. \(\omega_1^T \ge \alpha\).

证明. 由引理 5.4.8，对任意 \(\gamma < \alpha\)，存在 \(\sigma \in T\) 使得 \(h(\sigma) = \gamma\)。通过对 \(\gamma\) 进行归纳，可以直接验证子树 \(T_\sigma = \{\tau \in T \mid \tau \ge \sigma\}\) 在 Kleene-Brouwer 序下是良序的，序类型至少为 \(\gamma\)。故 \(\omega_1^T \ge \alpha\)。

以下强迫引理通过常规论证证明，留给读者。

### 引理 5.4.10. 对任意句子 \(\phi\)，\(\mathfrak{A}(\alpha, T) \models \phi\) 当且仅当存在 \(p\) 使得 \(t_p \subseteq T\) 且 \(p \Vdash \phi\)。

### 引理 5.4.11. \(\mathfrak{A}(\alpha, T)\) 满足 \(\Delta_1^1\)-理解公理。

证明. 令 \(\phi\) 和 \(\psi\) 为算术公式，使得

\(\mathfrak{A}(\alpha, T) \models (\forall n)((\exists z)\phi(n, z) \to (\forall z)\psi(n, z))\)。

则

\(\mathfrak{A}(\alpha, T) \models (\forall n)(\exists z)(\phi(n, z) \lor \neg \psi(n, z))\)。

如同在定理 5.2.5 的证明中，存在 \(p\) 使得 \(t_p \subseteq T\) 且

\((\forall q \le p)(\forall n)((\exists r \le q)(r \Vdash (\exists z)\phi(n, z) \lor \neg \psi(n, z)))\)。

故

\((\forall q \le p)(\forall n)((\exists r \le q)(\exists r')(r \Vdash (\exists z)\phi(n, z') \lor \neg \psi(n, z')))\)。

由引理 5.4.6 和引理 5.4.5，在 \(L_\alpha\) 中存在一个递增序列 \(\gamma_0 < \gamma_1 < \cdots\) 使得



- (i) Range($h_p$) $\supseteq y_0 \cup \{\infty\}$;
- (ii) 对于任意 $m$，$f((\exists z^{>n})(\varphi(n, z^{>n}) \lor \neg \psi(n, z^{>n})) < \gamma_{m+1}$，并且对于任意 $n$ 以及 $L_{\gamma_{m+1}}$ 中的 $p_n \le p$，存在一个 $q_n \le p_n$ 且 $q_n \in L_{\gamma_{m+1}}$，使得 $q_n \Vdash (\exists z^{>n+1})(\varphi(n, z^{>n+1}) \lor \neg \psi(n, z^{>n+1}))$，且
- (iii) 对于每个 $m$，$\gamma_{m+1} = \omega \gamma_{m+1}$。

令 $\beta = \bigcup_{m < \omega} \gamma_m = \omega \beta$。则 $\beta < \alpha$。我们声称

$p \Vdash (\forall n)((\exists z^\beta)(\varphi(n, z^\beta) \lor \neg \psi(n, z^\beta))$。

强制关系等价于

$(\forall n)(\forall q \le p)(\exists r \le q)(q \Vdash (\exists z^\beta)(\varphi(n, z^\beta) \lor \neg \psi(n, z^\beta))).$

给定 $n$ 和 $q \le p$，令 $q'$ 为一个条件，使得 $t'_{q'} = t_q$ 且当 $h_q(\alpha) < \beta$ 时 $h_{q'}(\alpha) = h_q(\alpha)$，否则 $h_{q'}(\alpha) = \infty$。由 (i)，$q' \le p$ 且对于某个 $m$，$q' \in L_{\gamma_m}$。由 (ii)，存在一个条件 $r' \in L_p$ 使得 $r' \le q'$ 且

$r' \Vdash (\exists z^{\gamma_m})(\varphi(n, z^{\gamma_m}) \lor \neg \psi(n, z^{\gamma_m})).$

由 (iii)，Ret$(\omega\beta, q, q')$ 成立且

$\omega \cdot f((\exists z^{\gamma_m})(\varphi(n, z^{\gamma_m}) \lor \neg \psi(n, z^{\gamma_m}))) < \beta.$

由引理 5.4.5 和引理 5.4.6，存在一个条件 $r \le q$ 使得

$r \Vdash (\exists z^\beta)(\varphi(n, z^{\gamma_m}) \lor \neg \psi(n, z^{\gamma_m})).$

因此

$r \Vdash (\exists z^\beta)(\varphi(n, z^\beta) \lor \neg \psi(n, z^\beta)).$

由引理 5.4.10，

$\mathfrak{A}(\alpha, T) \Vdash (\forall n)(\exists z^\beta)(\varphi(n, z^\beta) \lor \neg \psi(n, z^\beta)).$

令 $y$ 满足 $y \in \dot{y}$ 当且仅当 $\mathfrak{A}(\alpha, T) \Vdash (\exists z^\beta)\varphi(n, z^\beta)$。则 $y \in \mathfrak{A}(\alpha, T)$，因此 $\mathfrak{A}(\alpha^{<\omega}, T)$ 满足 $\Delta_1^\xi$-理解公理。$\square$

总之，我们有以下结论：

### **定理 5.4.12** (Sacks [122]). 对于任何可数可接受序数 $\alpha > \omega$，存在一个实数 $x$ 使得 $\omega_1^x = \alpha$。

### **注释 5.4.13.** 在文献中，有若干个定理 5.4.12 的证明。Sacks 最初的证明采用完备集强制法，并给出了更强的结论。第二个证明由 Friedman 和 Jensen [31] 提出，通过应用 Barwise 紧致性定理 [3]。第三个证明尚未发表，由 Jensen [54] 提出，使用了一类 Lévy 折叠运算，可视为 Steel 强制的变体。

### 5.4.3 练习

- 练习 5.4.1. 证明对于任何满足 \( x \notin L_{\omega_1^x} \) 的 x，存在一个 y 使得 \( y \ge_h x \)、\( y \notin_h x \) 且 \( \omega_1^x = \omega_1^y \)。

- 练习 5.4.2. 证明 \( x \in L_{\omega_1^x} \) 当且仅当对于所有 y，\( \omega_1^y \ge \omega_1^x \) 蕴含 \( y \ge_h x \)。

- 练习 5.4.3. 令 \( \alpha_n \) 为第 n 个可接受序数。则 \( \bigcup_{n<\omega} \alpha_n \) 不是可接受的。

- 练习 5.4.4 (Chong [11]). 假设 \( y > \omega \) 是一个序数，使得 \( J_{y+1} \backslash J_y \cap 2^\omega \neq \emptyset \)。则对于任何可接受序数 \( \alpha < \gamma^+ \)，其中 \( \gamma^+ \) 是大于 y 的最小可接受序数，存在一个 x \( \in J_y \backslash J_y \) 使得 \( \omega_1^x = \alpha \)。

- 练习 5.4.5 (Jensen [54]). 假设 \( \alpha \) 是可接受序数的可数极限。则存在一个集合 \( A \subseteq \alpha \)，使得对于任何可接受的 \( \beta < \alpha \)，\(\langle L_\beta[A], \epsilon, A \cap L_\beta[A] \rangle\) 是可接受的，且 \(\langle L_\alpha[A], \epsilon, A \cap L_\beta[A] \rangle \models \text{\texttt{"$\beta$ is countable"}}\)。

- 练习 5.4.6 (Jensen [54]). 假设 \( \omega < \alpha_0 < \cdots < \alpha_n \) 是一组可数可接受序数的有限序列。证明存在一个 x，使得对于任何 \( i \le n \)，\( \alpha_i \) 是 L[x] 中第 i + 1 个可数可接受序数。

## 6 集合论

本章回顾具有递归论应用的集合论结果。其中一些结果将不作证明，以供日后参考。

### 6.1 集合论强制法

强制法的技术在第 5 章的递归论背景下讨论过。Cohen [18] 中提出的该方法的原始版本与 § 5.2 中发展的方法非常相似。这里我们遵循 Shoenfield [130] 引入的非分层强制法（关于该主题的优秀论述见 Kunen [78]）。

#### 6.1.1 强制法与泛化性

令 M = (M, ∈) 为 ZFC 的一个可数传递模型，令 P = (P, ≤) 为 M 中的一个偏序。元素 p ∈ P 称为一个条件。给定两个条件 p, q ∈ P，如果 p ≤ q，则我们说 q 比 p 更强。D ⊆ P 是稠密的，如果对于任何 p ∈ P，存在 q ∈ D 使得 q ≤ p。

滤子 F ⊆ P 是一个非空集合，使得

- (∀p)(∀q)(q ≤ p ∈ P → p ∈ F);
- (∀p)(∀q)((∃r) ∈ F ∧ q ≤ r → r ∈ F ∧ r ≤ p ∧ r ≤ q).

泛化集 G ⊆ P 是一个与每个稠密集相交的滤子。一般来说，泛化集不属于 M，除非是非常特殊的偏序。如果 G ∉ M，则存在 ZFC 的一个模型 M[G] = (M[G], ∈)，使得 M ∪ {G} ⊆ M[G] 且 o(M) = o(M[G])。其定义如下。

首先，M 中的 P-名通过归纳定义：

- ∅ 是一个 P-名；
- 如果 τ ⊆ P-名集合 × P，则 τ 是一个 P-名。

我们用 M^P 表示 P-名的类。注意 M^P ⊂ M 且不是 M 的元素。假设 G 是泛化的。通过归纳定义 val(τ, G)：

- 如果 τ 不是 P-名，则 val(τ, G) = τ；
- 否则，val(τ, G) = {val(σ, G) | (σ, p) ∈ τ ∧ p ∈ G}.

令

```
M[G] = {val(τ, G) | τ ∈ M}.
```

因此，M[G] 中的每个元素 x 都有一个对应的 P-名。我们用 ẋ 表示 x 的 P-名。对于任何 a ∈ M，我们通过 a 的秩进行归纳，用 ȧ 表示 ⟨⟨ḃ, p⟩ | b ∈ a ∧ p ∈ P⟩。由于对于任何 \(a \in M\)，\(\text{val}(\tilde{a}, G) = a\)，我们有 \(M \subseteq M[G]\)。此外，\(\tilde{G} = \{(\check{p}, p) \mid p \in \mathbf{P}\}\) 是一个 \(\mathbf{P}\)-名，且 \(\text{val}(\tilde{G}, G) = G\)。因此 \(G \in M[G]\)。\(\langle M[G], \in \rangle\) 是 ZFC 的一个传递模型，且 \(o(M) = o(M[G])\)。

**定义 6.1.11.** 给定一个条件 \(p \in \mathbf{P}\) 和一个公式 \(\varphi(\tau_0, \dots, \tau_n)\)，其中 \(\tau_0, \dots, \tau_n \in M^\mathbf{P}\)，我们说 \(p\) *强制* \(\varphi(\tau_0, \dots, \tau_n)\)，或 \(p \Vdash \varphi(\tau_0, \dots, \tau_n)\)，当且仅当对于任何包含 p 的泛化集 G，\(\langle M[G], \in \rangle \models \varphi(\text{val}(\tau_0, G), \dots, \text{val}(\tau_n, G))\)。

**定理 6.1.2.** (i) 类 \(\langle p, \varphi, (\tau_0, \dots, \tau_n) \rangle \mid p \Vdash \varphi(\tau_0, \dots, \tau_n)\rangle\) 在 \(\mathfrak{M}\) 中可定义；(ii) 对于每个泛化集 G 和公式 \(\varphi(\tau_0, \dots, \tau_n)\)，其中 \(\tau_0, \dots, \tau_n \in M^\mathbf{P}\)，\(\langle M[G], \in \rangle \models \varphi(\text{val}(\tau_0, G), \dots, \text{val}(\tau_n, G)) \Leftrightarrow (\exists p \in G)(p \Vdash \varphi(\tau_0, \dots, \tau_n))\)。

定理 6.1.2 与 §5.2 中 \(\Vdash\) 的定义（见 [78]）结合起来并不令人惊讶。关于强制关系的以下事实是标准的。

**命题 6.1.3.** 对于任何公式 \(\varphi\)、条件 \(p\) 和 \(\mathbf{P}\)-名 \(\tau_0, \dots, \tau_n\)，(i) \(q \le p \land p \Vdash \varphi \implies q \Vdash \varphi\)；(ii) \(p \Vdash \varphi \land \psi\) 当且仅当 \(p \Vdash \varphi\) 且 \(p \Vdash \psi\)；(iii) \(p \Vdash \neg \varphi\) 当且仅当 \((\forall q \le p) q \not\Vdash \varphi\)；(iv) 集合 \(\{p \mid p \Vdash \neg \varphi \lor p \Vdash \varphi\}\) 是稠密的；(v) \(p \Vdash (\exists x)\varphi(x)\) 当且仅当集合 \(\{q \mid q \le p \text{ 且 } \exists \tau (q \Vdash \varphi(\tau))\}\) 是稠密的；(vi) \(p \Vdash (\exists x)\varphi(x)\) 当且仅当存在一个 \(\mathbf{P}\)-名 \(\tau \in M^\mathbf{P}\) 使得 \(p \Vdash \varphi(\tau)\)。

#### 6.1.2 \(\kappa\)-链条件与 Martin 公理

给定一个偏序 \(\mathbf{P} = (\mathbf{P}, \le)\)，集合 \(A \subseteq \mathbf{P}\) 是一个 *反链*，如果对于 A 中的 \(p \neq q\)，不存在满足 \(r \le p\) 和 \(r \le q\) 的 \(r\)。\(\mathbf{P}\) 满足 \(\kappa\)-*链条件*，或 \(\kappa\)-c.c.，如果在 \(\mathfrak{M}\) 中 \(\mathbf{P}\) 的每个反链的基数小于 \(\kappa\)。特别是，\(\omega_1\)-c.c. 称为可数链条件，或 c.c.c. 链条件限制了泛化扩展中函数的可能取值。事实上，链条件被用作泛化扩展中基数保持的基本工具。例如，如果 \(\mathbf{P} = (\mathbf{P}, \le)\) 满足 c.c.c. 且 \(f : \omega \to (\omega_1)^{\mathbf{M}}\) 是某个泛化集 G 下 \(\mathbf{M}[G]\) 中的一个函数，那么对于每个 \(n < \omega\)，集合 \(A_n = \{(\alpha, \omega_1)^{\mathbf{M}} \mid (\exists p)(p \Vdash f(\check{n}) = \check{\alpha})\} \in \mathbf{M}\) 在 \(\mathfrak{M}\) 中是可数的，因此 \(\bigcup_n A_n \in \mathbf{M}\) 在 \(\mathfrak{M}\) 中也是可数的。因此 \(\mathbf{P}\) 不会折叠 \((\omega_1)^{\mathbf{M}}\)。

**引理 6.1.14.** 如果 \(\mathbf{P}\) *满足* \(\kappa\)*-链条件*，则对于任何泛化集 G，\((\kappa)^{\mathbf{M}} = (\kappa)^{\mathbf{M}[G]}\)。

**定义 6.1.5** (Martin 公理 [90]). 令 \(\kappa\) 为一个基数。\(\text{MA}_\kappa\) 断言对于任何 c.c.c. 偏序 \(\mathbf{P} = (\mathbf{P}, \le)\) 和任何 \(\kappa\)-序列的稠密集 \(\{D_\alpha\}_{\alpha < \kappa}\)，存在一个滤子 \(G \subseteq \mathbf{P}\) 与每个 \(D_\alpha\) 相交。我们用 \(\text{MA}\) 表示 \((\forall \kappa < 2^{\aleph_0})\text{MA}_\kappa\)。





显然 $\mathrm{MA}_{\aleph_0}$ 是 ZFC 的一个定理。已知如果 ZFC 是自洽的，那么 ZFC + MA 也是自洽的。$\kappa$-链条件也用于计算幂集的基数。

### 6.1.3 $\kappa$-closedness

### 引理 6.1.6.
假设 $\kappa > \aleph_0$ 是正则基数，且 $\mathbb{P} = (\mathbf{P}, \le)$ 在 $\mathcal{M}$ 中满足 $\kappa$-c.c.，且 $|\mathcal{P}| = \lambda$。那么对于任何正则基数 $\eta \in M$ 和通用集 $G$，$\mathcal{M}[G] \models 2^\lambda \le ((\lambda^\kappa)^\eta)^M$。

**证明（草图）。** 每个 $x \in M[G] \cap 2^\lambda$ 对应一个 $\mathbb{P}$-名 $\dot{x} \in \eta \times \mathscr{P}(\mathbf{P})$。此外，我们可以假设对于任何 $\gamma < \eta$，$|\{p : (\dot{\gamma}, p) \in \dot{x}\}|$ 是一个反链。在 $\mathcal{M}$ 中有 $\lambda^\kappa$ 个反链。因此，这样的 $\mathbb{P}$-名最多有 $(\lambda^\kappa)^\eta$ 个。换句话说，$\mathcal{M}[G] \models 2^\lambda \le ((\lambda^\kappa)^\eta)^M$（详细证明见 [78]）。

$\mathbb{P}$ 中的两个条件 $p$ 和 $q$ 如果 $p \le q$ 或 $q \le p$，则称为相容。给定一个基数 $\kappa$，如果对于任何长度 $\nu < \kappa$ 的相容条件序列 $\langle p_\alpha \rangle_{\alpha < \nu}$，存在一个 $q$ 使得对每个 $\alpha < \nu$ 都有 $q \le p_\alpha$，则称 $\mathbb{P}$ 具有 $\kappa$-闭性质（在 $\mathcal{M}$ 中）。满足 $\kappa$-闭性质是保持基数的另一种基本工具。

### 引理 6.1.7.
如果 $\mathbb{P}$ 具有 $\kappa$-闭性质且 $A \in M$ 与 $|A| < \kappa$，那么在通用扩展 $\mathcal{M}[G]$ 中任何定义域为 $A$ 的函数 $f$ 都属于 $\mathcal{M}$。

由此可知，$\kappa$-闭性质保持所有不大于 $\kappa$ 的基数。

### 6.1.4 Product forcing

### 定义 6.1.18.
设 $I$ 为索引集，对于 $i \in I$，设 $\mathbb{P}_i = (\mathbf{P}_i, \le_i)$ 为一个强迫概念。设 $C \subseteq \mathscr{P}(I)$。$C$-积强迫 $\mathbb{P} = (\mathbf{P}, \le)$ 是一个偏序，对每个 $p \in \mathbf{P}$ 满足以下条件：

- 存在 $J \in C$ 使得 $p(i)$ 定义当且仅当 $i \in J$ 且 $p(i) \in \mathbf{P}_i$；
- 在 $\mathbf{P}$ 中，$q \le p$ 当且仅当对于任何 $i \in I$，$p(i)$ 已定义蕴含 $q(i)$ 已定义且 $q(i) \le_i p(i)$。

如果 $C$ 是 $I$ 的所有有限子集的集合，则 $\mathbb{P}$ 称为有限支持的积强迫。如果 $C$ 是 $I$ 的所有可数子集的集合，则 $\mathbb{P}$ 是可数支持的积强迫。$I$ 常取为序数。

设 $I$ 为序数 $\gamma$。如果 $C = I$，我们称 $\mathbb{P}$ 简单为 $\langle \mathbb{P}_\alpha \rangle_{\alpha < \gamma}$ 的积。那么 $C$-积强迫 $\mathbb{P} = \Pi_{\alpha < \gamma} \mathbb{P}_\alpha$ 可分解为 $\Pi_{\alpha < \beta} \mathbb{P}_\alpha \times \Pi_{\beta \le \alpha < \gamma} \mathbb{P}_\alpha$。换句话说，$\mathbb{P} \cong \Pi_{\alpha < \beta} \mathbb{P}_\alpha \times \Pi_{\beta \le \alpha < \gamma} \mathbb{P}_\alpha$。

### 定理 6.1.19.
假设 $\mathbb{P} = (\mathbf{P}, \le_P)$ 和 $\mathbb{Q} = (\mathbf{Q}, \le_Q)$ 是两个强迫概念。设 $\mathbb{P} \times \mathbb{Q}$ 为 $\mathbb{P}$ 和 $\mathbb{Q}$ 的积。那么对于任何集合 $G \subseteq \mathbf{P} \times \mathbf{Q}$，$G$ 是 $\mathcal{M}$ 上的通用集当且仅当 $G = G_1 \times G_2$，其中 $G_1 \subseteq \mathbf{P}$ 是 $\mathcal{M}$ 上的通用集且 $G_2$ 是 $\mathcal{M}[G_1]$ 上的通用集。此外，$\mathcal{M}[G] = \mathcal{M}[G_1][G_2]$。

一般来说，c.c.c. 性质在积强迫下不被保持。以下更强的性质解决了这一限制。

### 定义 6.1.10.
如果一个强迫概念的每个不可数条件集都有一个互相相容的不可数子集，则称其具有性质 (K)。

下一个定理出自 Jech [53]。

### 定理 6.1.11.
- (i) 设 $\gamma \ge 0$ 为序数，并假设对于每个 $\alpha < \gamma$，$\mathbb{P}_\alpha$ 具有性质 (K)。那么有限支持的积强迫 $\mathbb{P} = \Pi_{\alpha < \gamma} \mathbb{P}_\alpha$ 具有性质 (K)；
- (ii) 假设 $\kappa \ge \aleph_1$，$\kappa^\omega = \kappa$，且对于每个 $i \in I$ 有 $|\mathbf{P}_i| \le \kappa$。那么可数支持的积强迫 $\Pi_{i \in I} \mathbf{P}_i$ 满足 $\kappa^+$-c.c.。

### 6.1.5 Iterated forcing

积强迫不太适合对模型的构建进行精细调整。由 Solovay 和 Tennenbaum [147] 引入的迭代强迫概念在这方面提供了更多的“灵活性”。给定一个序数 $\alpha$，设 $I \subseteq \mathscr{P}(\alpha)$ 为一个理想，使得 $\{0\} \in I$。我们通过对 $\beta$ 进行归纳，定义带有支持 $I$ 的序数 $\beta \le \alpha$ 上的迭代强迫 $\mathbb{P}_\beta = (\mathbf{P}_\beta, \dot{\mathbb{Q}}_\gamma, \gamma \le \beta, I)$。

### 定义 6.1.12.
对于 $\beta = 0$，$\mathbb{P}_0 = (\mathbf{P}_0, \dot{\mathbb{Q}}_0, 0, I)$ 满足

- $\dot{\mathbb{Q}}_0$ 是一个强迫概念；
- $p \in \mathbf{P}_0$ 当且仅当 $p$ 是一个函数，使得 $\mathrm{Dom}(p) = \{0\}$ 且 $p(0) \in \dot{\mathbb{Q}}_0$。

对于 $\beta = \xi + 1$，强迫条件 $p \in \mathbf{P}_\beta$ 是一个定义域属于 $I$ 的偏函数，使得

- $p \restriction \xi \in \mathbf{P}_\xi$；
- $\dot{\mathbb{Q}}_\beta$ 是一个 $\mathbf{P}_\xi$-名；
- 如果 $\beta \in \mathrm{Dom}(p)$，则 $p \restriction \xi \Vdash p(\beta) \in \dot{\mathbb{Q}}_\beta$。

如果 $q \in \mathbf{P}_\beta$，定义 $p \le_\beta q$ 当 $p \restriction \xi \le q \restriction \xi$ 且 $p \restriction \xi \Vdash p(\beta) \le q(\beta)$。

如果 $\beta$ 是极限序数，则强迫条件 $p \in \mathbf{P}_\beta$ 是一个定义域属于 $I$ 的偏函数，使得

- 对每个 $\xi < \beta$，$p \restriction \xi \in \mathbf{P}_\xi$；
- $\{\xi < \beta \mid \xi \in \mathrm{Dom}(p)\} \in I$。

如果 $q \in \mathbf{P}_\beta$，定义 $p \le_\beta q$ 当且仅当对每个 $\xi < \beta$ 都有 $p \restriction \xi \le q \restriction \xi$。

最有用的两个迭代强迫概念是基于有限支持和可数支持定义的那些。

### 命题 6.1.13.
设 $\alpha$ 为无穷序数。假设 $\mathcal{M} \vDash \text{ZFC} \wedge \text{``}\kappa > \omega \text{ is regular''}$，$I = \{s \mid s \subseteq \alpha \wedge |s| < \aleph_0\}$，并设 $\mathbb{P}_\alpha = (\mathbf{P}_\alpha, \le_{\mathbb{P}_\alpha}, I)$。如果对于每个 $p$ 和 $\beta \le \alpha$，$p \Vdash \text{``}\dot{\mathbb{Q}}_\beta \text{ satisfies c.c.c.''}$，那么对于每个 $\beta \le \alpha$，$\mathbb{P}_\beta$ 在 $\mathcal{M}$ 中满足 c.c.c.。

### 注释 6.1.14.
当 $I$ 是可数支持时，类似的结论对正当强迫也成立。证明可见 [53]。

### 6.1.6 Embeddings and isomorphisms

### 定义 6.1.15.
一个从 $(\mathbf{P}, \le)$ 到 $(\mathbf{Q}, \le)$ 的函数 $f$ 是稠密嵌入，如果
- $(\forall p_0)(\forall p_1)(p_0 \le p_1 \rightarrow f(p_0) \le f(p_1))$；
- $(\forall p_0)(\forall p_1)(p_0 \parallel p_1 \rightarrow f(p_0) \parallel f(p_1))$；
- Range($f$) 是 $\mathbf{Q}$ 的一个稠密子集。

一个从 $(\mathbf{P}, \le)$ 到 $(\mathbf{Q}, \le)$ 的函数 $f$ 是同构，如果 $f$ 是双射且 $(\forall p_0)(\forall p_1)(p_0 \le p_1 \leftrightarrow f(p_0) \le f(p_1))$。显然，每个同构都是稠密嵌入。

### 定义 6.1.16.
假设 $f : \mathbf{P} \to \mathbf{Q}$。对于任何 $\tau \in M^{\mathbf{P}}$，递归地定义由 $f$ 诱导的 $\tau$ 的相应 $\mathbb{Q}$-名 $f_*(\tau)$ 为
$f_*(\tau) = \{(f_*(\sigma), f(p)) \mid (\sigma, p) \in \tau\}$。

这允许证明以下命题。

### 命题 6.1.17.
设 $\mathcal{M} \vDash \text{ZFC}$，设 $f : \mathbf{P} = (\mathbf{P}, \le) \to \mathbf{Q} = (\mathbf{Q}, \le)$ 为稠密嵌入。
- (i) 如果 $H$ 是 $\mathcal{M}$ 上的 $\mathbb{Q}$-通用集，则 $f^{-1}(H)$ 是 $\mathcal{M}$ 上的 $\mathbb{P}$-通用集且 $M[f^{-1}(H)] \subseteq M[H]$。
- (ii) 对于任何公式 $\varphi(v_0, \dots, v_n)$，
  $p \Vdash \varphi(\tau_0, \dots, \tau_n) \leftrightarrow f(p) \Vdash \varphi(f_*(\tau_0), \dots, f_*(\tau_n))$。

### 6.1.7 Exercise

### 练习 6.1.1.
证明命题 6.1.17。

## 6.2 Some examples of forcing

### 6.2.1 Cohen forcing

### 定义 6.2.1.
Cohen 强迫 $\mathbb{C} = (2^{<\omega}, \le)$ 是一个强迫概念，使得对于任何 $p, q \in 2^{<\omega}$，$q \le p$ 当且仅当 $q \supseteq p$。





由于 \(2^{<\omega}\) 可数，以下结论表明 Cohen 扩张下基数被保留：

### 命题 6.2.2. Cohen 强迫满足性质 (K)。

给定 Cohen 通用集 \(G\)，集合 \(g = \bigcup_{p \in G} \check{p}\) 被称为 Cohen 实数。接下来的两个结果在 [78] 中被证明。

### 命题 6.2.3. 假设 \(g = g_1 \times g_2\)。那么 \(g\) 是 \(M\) 上的 Cohen 实数，当且仅当 \(g_1\) 是 \(M\) 上的 Cohen 实数，且 \(g_2\) 是 \(M[g_1]\) 上的 Cohen 实数。

### 命题 6.2.4. 假设 \(\kappa \ge \omega\) 且 \(S \in M\)。令 \(\mathbb{P}\) 为长度为 \(\kappa\) 的乘积 Cohen 强迫概念，并令 \(G\) 为通用集。那么对于 \(M[G]\) 中的任何 \(A \subseteq S\)，存在 \(\alpha \le \min\{\kappa, |S|^M\}\) 使得 \(A \in M[G \cap \mathbb{P}_{<\alpha}]\)，其中 \(\mathbb{P}_{<\alpha} = \Pi_{\gamma < \alpha} 2^{<\omega}\)。

### 6.2.2 随机强迫

随机强迫由 Solovay [150] 引入，用于构造 ZF + DC 的一个模型，其中每个实数集都是勒贝格可测的。

### 定义 6.2.5. 令 \(\mu\) 表示勒贝格测度。随机强迫 \(\mathbb{R} = (\mathbf{T}, \le)\) 是一种强迫概念，其中

- 每个 \(T \in \mathbf{T}\) 都是 \(2^{<\omega}\) 的子树，且满足 \(\mu([T]) > 0\)；
- \(T_1 \le T_2\) 当且仅当 \(T_1 \subseteq T_2\)。

### 命题 6.2.6. 随机强迫满足 c.c.c。

证明。假设存在一个不可数反链 \(\{T_\alpha\}_{\alpha < \omega_1}\)。那么对于 \(\alpha \neq \beta < \omega_1\)，\(\mu([T_\alpha] \cap [T_\beta]) = 0\)。令 \(S_\alpha = [T_\alpha] \setminus \bigcup_{\beta < \alpha} [T_\beta]\)。那么 \(\{S_\alpha\}_{\alpha < \omega_1}\) 是一组两两不相连的博雷尔集的不可数序列，且对每个 \(\alpha < \omega_1\) 满足 \(\mu(S_\alpha) > 0\)。令 \(n\) 使得集合 \(R_n = \{S_\alpha \mid \mu(S_\alpha) > \frac{1}{n}\}\) 是不可数的。那么 \(1 = \mu(2^\omega) \ge \mu(\bigcup_{S \in R_n} S_\alpha) = \infty\)，这产生了矛盾。

如果实数 \(x\) 是 \(\mathbb{R}\)-通用的，则称其为随机实数。

### 6.2.3 基数坍缩

令 \(\kappa\) 为一个基数。存在一种强迫概念，它坍缩 \(\kappa\) 以下的所有基数，同时保留 \(\kappa\)：令 \(\mathbb{P}(\kappa) = (\kappa^{<\omega}, \le)\)，对于 \(p, q \in \kappa^{<\omega}\)，定义 \(q \le p\) 当且仅当 \(q \supseteq p\)。那么 \(\mathbb{P}(\kappa)\) 满足 \(\kappa^+\)-c.c。此外，对于任何通用滤子 \(G\)，函数 \(g = \bigcup_{p \in G} p\) 将 \(\omega\) 映射到 \(\kappa\)。因此我们有

### 命题 6.2.7. 假设 \(\kappa \ge \omega_1\) 是一个基数。那么

- (i) \(\mathbb{P}(\kappa)\) 满足 \(\kappa^+\)-c.c；
- (ii) 如果 \(G\) 是通用的，那么 \(\kappa^+ = (\omega_1)^{M[G]}\)。

注意 \(\mathbb{P}(\kappa)\) 仅保留后继基数 \(\kappa^+\)。下一种强迫概念允许保留正则极限基数。

### 定义 6.2.8. 令 \(\kappa \ge \omega\) 为一个基数。为 \(\kappa\) 定义 Lévy 强迫 \(\mathbb{L}(\kappa) = (\mathbb{L}_\kappa, \le)\)，如下：

- \(p \in \mathbb{L}_\kappa\) 当且仅当 \(p\) 是一个从 \(\kappa \times \omega\) 的子集映射到 \(\kappa\) 的有限函数，使得对于任何 \(\alpha < \kappa\) 和 \(n < \omega\)，若 \(p(\alpha, n)\) 有定义，则 \(p(\alpha, n) < \alpha\)。
- 对于任何 \(p, q \in \mathbb{L}_\kappa\)，\(q \le p\) 当且仅当 \(q \supseteq p\)。

\(\mathbb{L}(\kappa)\) 可以被视为长度为 \(\kappa\) 且具有有限支持的乘积强迫，其中在每个 \(\alpha < \kappa\) 处，强迫作用将 \(\alpha\) 坍缩到 \(\omega\)。

### 命题 6.2.9. 令 \(\kappa \ge \omega\) 为一个正则基数，并令 \(G\) 为 \(\mathbb{L}(\kappa)\)-通用。那么 \(\kappa = (\omega_1)^{M[G]}\)。

证明。显然，对于任何 \(\alpha < \kappa\)，\(G(\alpha) = \bigcup_{n \le p \in G} p(\alpha, n)\) 将 \(\omega\) 映射到 \(\alpha\)。因此 \(M[G] \models \kappa \le \omega_1\)。我们证明 \(\mathbb{L}(\kappa)\) 满足 c.c.c。

假设 \(A \subseteq \mathbb{L}_\kappa\) 是一个基数为 \(\kappa\) 的反链。不失一般性，我们可以假设存在 \(n^*\) 使得对于每个 \(p \in A\)，\(|\text{Dom}(p)| = n^*\)。我们声称存在 \(\alpha < \kappa\) 使得 \(A_\alpha = \{p \in A \mid (\exists n)(\alpha, n) \in \text{Dom}(p)\}\) 的基数为 \(\kappa\)。否则，存在 \(p, q \in A\) 具有不相交的定义域，使得 \(p\) 和 \(q\) 相容，这产生矛盾。因此，令 \(\alpha_0\) 为使得 \(A_\alpha\) 基数为 \(\kappa\) 的最小 \(\alpha\)。令 \(B_{\alpha_0} = \{p \in A_{\alpha_0} \mid (\forall \beta < \alpha_0)(\forall n)(\beta, n) \in \text{Dom}(p)\}\)。根据对 \(\alpha_0\) 的假设，\(|B_{\alpha_0}| = \kappa\)。

由于 \(|B_{\alpha_0}| = \kappa\) 且 \(|\alpha_0| < \kappa\)，我们可以假设对于任何 \(p, q \in B_{\alpha_0}\)，\(\{(\alpha_0, n) \mid (\alpha_0, n) \in \text{Dom}(p)\} = \{(\alpha_0, n) \mid (\alpha_0, n) \in \text{Dom}(q)\}\)。此外，由于一般情况下 \(p(\alpha, n) < \alpha\)，我们甚至可以假设对于任何 \(p, q \in B_{\alpha_0}\)，\((\alpha_0, n) \in \text{Dom}(p)\) 蕴含 \(p(\alpha_0, n) = q(\alpha_0, n)\)。

然后，与 \(\alpha_0\) 的相同论证，存在 \(\alpha_1 > \alpha_0\)，它是大于 \(\alpha_0\) 的最小序数，使得 \(B_{\alpha_0} \ge A_{\alpha_1}\) 且后者大小为 \(\kappa\)。令 \(B_{\alpha_1} = A_{\alpha_1} \cap \{p \mid (\forall \beta)(\forall n)(\alpha_0 < \beta < \alpha_1 \rightarrow (\beta, n) \notin \text{Dom}(p))\}\)。那么 \(|B_{\alpha_1}| = \kappa\)。

因此，如前所述，我们可以定义一组序数 \(\alpha_0 < \alpha_1 < \dots < \alpha_\kappa\) 和一组集合 \(B_{\alpha_0} \ge B_{\alpha_1} \ge \dots \ge B_{\alpha_\kappa}\)，使得 \(|B_{\alpha_\kappa}| = \kappa\) 且对于所有 \(p \in B_{\alpha_\kappa}\)，\(\text{Dom}(p) = \{\alpha_0, \dots, \alpha_\kappa\}\)。那么 \(|B_{\alpha_\kappa}| \le |\alpha_\kappa|^\omega < \kappa\)，这产生矛盾。

### 6.2.4 Sacks 强迫

完美集强迫由 Spector [154] 引入，用于构造一个最小 Turing 度的集合。该方法由 Sacks 推广，并应用于超算术和集合论设置，分别产生最小超度和最小可构度的集合 [121]。

### 定义 6.2.10. Sacks 强迫是一种强迫概念 \(\mathbb{S} = (\mathbf{T}, \le)\)，使得

- \(\mathbf{T}\) 是 \(\subseteq 2^{<\omega}\) 的完美树的集合；
- 对于任何 \(T_1, T_2 \in \mathbf{T}\)，\(T_1 \le T_2\) 当且仅当 \(T_1 \subseteq T_2\)。

Sacks 通用实数是与每个完美集的稠密集相交的实数。下面的定理表明这样的实数具有“最小性质”。

### 定理 6.2.11 (Sacks [121]). 假设 \(g\) 是 ZFC 模型 \(\mathcal{M}\) 上的 Sacks 通用实数，且 \(x \in \mathbf{M}[g] \setminus \mathbf{M}\) 是一个实数。那么存在实数 \(z_0, z_1 \in \mathbf{M}\)，使得 \(x \oplus z_0 \ge_T g\) 和 \(x \le_T z_1 \oplus g\)。

证明。假设 \(g\) 是由通用滤子 \(G\) 产生的 Sacks 通用实数，并令 \(x \in \mathbf{M}[g] \setminus \mathbf{M}\)。根据定理 6.1.2，存在一个条件 \(T^0\)，使得 \(T^0 \in G\)（即 \(g \in [T^0]\)）且

```
$T^0 \Vdash \dot{x} \notin \check{\mathbf{M}} \wedge \dot{x} \in 2^\omega$.
```

令 \(T^1 \le T^0\)。通过归纳定义函数 \(T : 2^{<\omega} \to T^1\)、条件序列 \(\{T_\sigma\}_{\sigma \in 2^{<\omega}}\) 和数 \(n_\sigma\)，如下：

令 \(T(0) = 0\) 和 \(T_0 = T^1\)。

假设 \(\sigma \in 2^{<\omega}\)，\(T(\sigma)\) 已定义且 \(T_\sigma \subseteq T^1\)。那么 \(T_\sigma \Vdash \dot{x} \notin \check{\mathbf{M}} \wedge \dot{x} \in 2^{n_\sigma}\)，并且存在 \(n_\sigma > |\sigma|\) 以及条件 \(T_0, T_1 \subseteq T_\sigma \cap [T(\sigma)]\)，使得 \(T_0 \Vdash \dot{x}(\dot{n}_\sigma) = 0\) 和 \(T_1 \Vdash \dot{x}(\dot{n}_\sigma) = 1\)，其中 \([T(\sigma)]\) 是扩展 \(T(\sigma)\) 的字符串集合。

那么存在 \(\tau > T(\sigma)\) 和 \(i \in \{0, 1\}\)，使得 \(\tau \in T_\sigma\)，\([\tau'] \cap [T_0] \neq \emptyset\) 且 \([\tau' \cap (1-i)] \cap [T_1] \neq \emptyset\)。令 \(T(\sigma') = \tau'\)，\(T_{\sigma'} = \tau' \cap [T_i] \cap T_i\) 对于 \(i \in \{0, 1\}\)。那么 \(T_{\sigma'} \Vdash \dot{x}(\dot{n}_\sigma) = 0\) 和 \(T_{\sigma' \cap (1-i)} \Vdash \dot{x}(\dot{n}_\sigma) = 1\)。

令 \(T^2 = \{\tau \mid (\exists \sigma)(T(\sigma) > \tau)\} \subseteq T^1\)。那么对于任何 \(\sigma\)，\(T^2 \cap [T(\sigma)] \le T_\sigma\)。因此

```
$(\forall \sigma)(\forall i < 2)(T^2 \cap [T(\sigma' \cap i)] \Vdash \dot{x}(\dot{n}_\sigma) = i)$.
```

令

```
D = \{T^2 \mid (T(\sigma) \Vdash_T T^2 \Vdash_T T \notin [T^0] \lor
(\exists(n_\sigma)_{\sigma \in 2^{<\omega}})(\exists \forall)(T : 2^{<\omega} \to 2^{<\omega}(\forall \sigma)(\forall \tau)(i < 2)(\exists j < 2)
(T^2 = \{\tau \mid (\exists \sigma)(\tau < T(\sigma))\} \land
(\sigma < \tau \mapsto T_\sigma \le T_\tau) \land (n_\sigma > |\sigma|) \land
(T^2 \cap [T(\sigma' \cap i)] \Vdash \dot{x}(\dot{n}_\sigma) = \dot{j} \wedge T^2 \cap [T(\sigma' \cap (1-i))] \Vdash \dot{x}(\dot{n}_\sigma) = \dot{1-\dot{j}})\}.
```

显然 \(D\) 是一个稠密集。因此存在 \(T^2 \in D \cap G\)。此外，存在序列 \(\{n_\sigma\}_{\sigma \in 2^{<\omega}}\) 和序保持映射 \(T : 2^{<\omega} \to 2^{<\omega}\)，使得

- \(T^2 = \{\tau \mid (\exists \sigma)(\tau < T(\sigma))\}\)；
- 对于所有 \(\sigma\)，\(n_\sigma > |\sigma|\)；
- 对于所有 \(\sigma\)、\(i < 2\)，存在 \(j < 2\) 使得 \(T^2 \cap [T(\sigma' \cap i)] \Vdash \dot{x}(\dot{n}_\sigma) = \dot{j}\) 且 \(T^2 \cap [T(\sigma' \cap (1-i))] \Vdash \dot{x}(\dot{n}_\sigma) = \dot{1-\dot{j}}\)。

令

```
$z_0 = \{(\sigma, T(\sigma' \cap i), n_\sigma, j) \mid \sigma \in 2^{<\omega} \wedge i \in 2 \wedge j \in 2 \wedge T^2 \cap [T(\sigma' \cap i)] \Vdash \dot{x}(\dot{n}_\sigma) = \dot{j}\}.
```



那么 \( z_0 \in M \) 可以被编码为一个实数。

注意 \( g \in [T]^2 \)。由于 \( x \in M[g] \)，要计算给定 \( n \) 的 \( g \restriction n \)，搜索一个 \( |\tau| \ge n \) 和一个 \( \sigma \)，使得对于任何 \( k \le |\tau| \)，存在唯一的 \( n_{0k} \) 和 \( n_{1k} < \tau k \)，使得 \( (\sigma \upharpoonright k, \tau_k, n_{0k}, n_{1k}) \in j_0 \) 当且仅当 \( x(n_{0k}) = j \)。那么 \( \tau \cap n = g \restriction n \)。因此 \( g \le_T \sigma \times \tau_0 \)。

要看到存在一个实数 \( z_1 \in M \) 使得 \( g \Vdash z_1 \ge_T x \)，假设

对于某个 \( \tau \in 2^\omega \)。令 \( z_1 = ((\sigma \circ \tau) \cap T^2 [(T \circ \tau)] \models x \neq \dot{\tau} \} \)。那么 \( x \le z_1 \Vdash g \)。

定理 6.2.11 证明中的方法是典型的所谓融合构造。这种构造线允许在 \( M \) 中找到一个融合序列 \( \langle T_\alpha \rangle_{\alpha < 2^\omega} \)，对于该序列存在 \( M \) 中的一个条件 \( T^2 \)，它是 \( \langle T_\alpha \rangle_{\alpha < 2^\omega} \) 的交集，使得 \( (\forall \alpha)(\forall i < 2)(T^2 \cap [T(\sigma(i))] \models x(\dot{n}_\alpha) = \dot{i}) \)。这个“分裂性质”有助于从 \( x \) 和实数 \( z \) 中解码 \( G \)。

### 推论 6.2.12. 如果 \( g \) 是 \( M = (M, \in) \) 上的萨克斯泛化，那么 \( M[g] \) 中每个可数序数集都是 \( M \) 中某个可数集的子集，且 \( (2^{\aleph_0})^{M[g]} = (2^{\aleph_0})^M \)。

因此萨克斯强迫保持 \( \aleph_1 \)。然而，已知萨克斯强迫可能使基数坍塌（参见 [6]）。

### 6.2.5 破坏选择公理

一般来说，没有通过 ZFC 过渡模型的强迫扩展直接破坏选择公理（AC）的方法。人们引入一个中间模型来实现这一点。

### 定义 6.2.13.

- 一个集合 \( X \) 在 \( M \) 中是序数可定义的，记作 \( X \in \text{OD}^M \)，如果存在一个公式 \( \varphi(x, v_0, \dots, v_n) \) 连同 \( M \) 中的序数 \( a_0, \dots, a_n, \beta \)，使得 \( a \in X \Leftrightarrow V_\beta^M \models \varphi(a, a_0, \dots, a_n) \)，其中 \( V_\beta^M \) 是 \( M \) 中秩小于 \( \beta \) 的集合的集合。

- \( X \) 在 \( M \) 中是遗传序数可定义的，记作 \( X \in \text{HOD}^M \)，如果 \( \text{TC}(\{X\}) \subset \text{OD}^M \)。

如果 \( M \) 是 ZFC 的过渡模型，那么 \( (\text{HOD}^M)^\in \) 是 ZFC 的过渡模型（参见 [53]）。

这一概念可以通过定义 \( \text{OD}(A)^M \) 和 \( \text{HOD}(A)^M \) 推广到更广泛的类。如果 \( M \) 是 ZFC 的过渡模型且 \( A \in M \)，那么 \( (\text{HOD}(A)^M, \in) \) 是 ZF 的过渡模型（参见 [53]）。我们使用 \( \text{HOD}(A)^M \) 来获得一个破坏 AC 的模型。

### 定义 6.2.14. 设 \( A \in M \)。

- 一个集合 \( X \) 在 \( M \) 中相对于 \( A \) 是序数可定义的，记作 \( X \in \text{OD}(A)^M \)，如果存在序数 \( a_0, \dots, a_n \)、元素 \( a_0, \dots, a_m \in A \) 以及扩展语言中的公式 \( \varphi(x, a_0, \dots, a_n, a_0, \dots, a_m, A) \)，在结构 \( \langle M, A, a_0, \dots, a_m, \in \rangle \) 中定义 \( X \)。

- 一个集合 \( X \) 属于 \( \text{HOD}(A)^M \)，如果 \( \text{TC}(\{X\}) \subset \text{OD}(A)^M \)。

### 定理 6.2.15. 假设 $\mathcal{M} \models V = L$。设 $\mathbb{P} = \Pi_{\alpha < \omega} C$ 为具有有限支持的积科恩强迫概念，并设 $G$ 为一个 $\mathbb{P}$-泛化滤子。如果 $A = \{g \in (\exists i)(\forall j)(g(j) = \bigcup_{p \in G} p(i)(j))$，那么在 $N = \text{HOD}(\text{TC}(\{A\}))^{\mathcal{M}[G]}$ 中不存在实数的良序。

证明. 假设存在 $N$ 中的双射 $F : 2^\omega \to A$，对某些 $\alpha \in \text{ON}$。我们可以将 $G$ 与泛化实数的 $\omega$-序列 $\langle (i, j) \mid g(j) \rangle = \bigcup_{p \in G} p(i)(j) \rangle$ 识别。

令

$\hat{A} = \langle (\dot{G}_i, p) \mid i < \omega \land p \in \mathbf{P} \rangle,$

其中 $G_i = (\forall j)(\exists p)(p \in G \land G_i(j) = (p(i)(j)))$。显然 $\text{val}(A, \dot{G}) = A$。那么存在一个公式 $\phi(x, v, \vec{a}, \vec{a}, A)$，通过 $A$、序数 $\vec{a}$ 和 $\vec{a} \in A^{<\omega}$ 定义 $F(x) = v$。令 $\phi_1(x, v, \vec{a}, \vec{a}, A)$ 为

$x$ 是使得 $\phi_0(x, v, \vec{a}, \vec{a}, A)$ 成立的唯一实数。

那么对于任何实数 $x \in M[G]$，存在一个 $v < \omega_1$ 使得

$\mathcal{M}[G] \models \phi_1(x, v, \vec{a}, \vec{a}, A).$

设 $n$ 为最小的数，使得 $\vec{a} \in \mathcal{M}[G_{<n}]$，其中 $G_{<n} = \langle (i, j) \mid i < n \land (\forall j)(\exists p)(p \in G \land (p(i)(j)) = 1) \rangle$。那么 $G_n \in N$，因此

$\mathcal{M}[G] \models \phi_1(G_n, v, \vec{a}, \vec{a}, A)$

对某些 $v < a$。

因此存在条件 $p \in G$ 使得

$p \Vdash \phi_1(G_n, \vec{v}, \vec{a}, \vec{a}, \vec{A}).$

设 $m > n$ 为不在 $\text{Dom}(p)$ 中的最小数。设 $\pi : \omega \to \omega$ 为仅交换 $m$ 与 $n$ 的 $\omega$ 的排列。那么 $\pi$ 诱导 $\mathbb{P}$ 的一个自同构 $\tilde{\pi}$：对于每个 $p \in \mathbf{P}$，

$\text{Dom}(\tilde{\pi}(p)) = \{\pi(i) \mid i \in \text{Dom}(p)\}$

且

$(\tilde{\pi}(p))(\pi(i)) = p(i).$

显然 $\tilde{\pi}(\dot{v}) = \dot{v}$，$\tilde{\pi}(\dot{\vec{a}}) = \dot{\vec{a}}$，$\tilde{\pi}(\dot{\vec{a}}) = \dot{\vec{a}}$，$\tilde{\pi}(\dot{A}) = A$。而且，$p$ 与 $\tilde{\pi}(p)$ 相容。因此存在 $q \in \mathbf{P}$ 使得 $q \le p, \tilde{\pi}(p)$。那么

$q \Vdash \phi_1(G_m, \vec{v}, \vec{a}, \vec{a}, \vec{A})$

且

$q \Vdash \phi_1(G_m, \vec{v}, \vec{a}, \vec{a}, \vec{A}).$

这意味着 $q \Vdash G_n = G_m$，这是一个矛盾。

### 6.2.6 练习

### 练习 6.2.1. 证明如果 ZF 是相容的，那么 ZF+“存在一个无限实数集 \( A \)，其所有子集要么在 \( A \) 中是有限的，要么在 \( A \) 中是余有限的”也是相容的。

### 练习 6.2.2. 证明萨克斯强迫不满足 c.c.c.

### 练习 6.2.3. 证明如果 \( g \) 是 $M \models \text{ZFC}$ 上的实数科恩泛化，那么对于任何实数 $x \in M[g] \setminus M$，存在 $z \in M$ 使得 $x \le_T g \oplus z$。

### 练习 6.2.4. 证明如果 \( g \) 是 $M \models \text{ZFC}$ 上的实数科恩泛化，那么 $M[g]$ 中每个解析实数都是 $M$ 的元素。

### 练习 6.2.5 (Levy [84]). 证明如果 \( g \) 是 $L$ 上的实数科恩泛化，那么 \( (\text{HOD})^{L[g]} = L \)。

## 6.3 \(\Pi^1_1\)-集的基数刻画

在本节中，我们展示了马丁公理在马丁和索洛韦 [90] 的 \(\Pi^1_1\)-集刻画中的一个应用。

### 6.3.1 几乎不相交强迫

### 定义 6.3.1. 实数集 \( A \subseteq 2^\omega \) 是 *几乎不相交* 的，如果对于任何 \( x \in A \)，\( |x| = \infty$，且对于任何 \( x \neq y \in A \)，\( x \cap y \) 是有限的。

以下强迫概念由西尔弗引入。

### 定义 6.3.2. 给定索引集 \( I \)、几乎不相交集 \( A = \{x_i\}_{i \in I} \) 和 \( X \subset I \)，\(\mathbb{P} = (\mathbb{P}, \le)\) 是与 \( A \) 和 \( X \) 对应的 *几乎不相交强迫*，如果每个 \( p \in \mathbb{P} \) 都是从 \( \omega \) 到 2 的部分函数，使得

- \( (\forall i \in X)(|\text{Dom}(p) \cap x_i| < \infty) \); and
- \( |\{n \mid p(n) = 1\}| < \infty \).

我们写 \( p \le q \) 如果 \( p \supseteq q \)。

### 引理 6.3.3. 给定索引集 \( I \) 上的几乎不相交集 \( A = \{x_i\}_{i \in I} \) 和 \( X \subset I \)，与 \( A \) 和 \( X \) 对应的几乎不相交强迫是 c.c.c。

**Proof.** 给定两个条件 \( p \) 和 \( q \)，\( p$ 与 $q$ 不相容当且仅当 \(\{n \mid p(n) = 1\} \neq \{n \mid q(n) = 1\}\)。由于 \( \omega \) 只有可数多个有限子集，引理立即成立。\(\square\)





### 6.3.2 Martin–Solovay 的刻画

### 引理 6.3.4.

(i) 对每个 \(i \in I\)，\(D_{0,i} = \{p \in \mathbf{P} \mid x_i \subseteq \text{Dom}(p)\}\) 是稠密的。(ii) 对每个 \(i \in X\) 和 \(i \in \omega\)，\(D_{1,i} = \{p \in \mathbf{P} \mid |\{n \in x_i \mid p(n) = 1\}| > i\}\) 是稠密的。

**证明.** (i) 显而易见。要看到 (ii)，给定任意条件 \(p\)，我们有 \(|\text{Dom}(p) \cap x_i| < \infty\)。然后只需将 \(p\) 扩展到一个条件 \(q\)，使得 \(|\{n \in x_i \mid q(n) = 1\}| > i\)。

### 定理 6.3.5.

如果 \(G\) 是一个与所有 \(D_{0,i}\) 和 \(D_{1,i}\) 对所有 \(i \in I\) 相遇的通用集，那么通用集 \(g = \bigcup_{p \in G} p\) 是一个实数，使得对于任何 \(i \in I, x \in X\) 仅当 \(g \cap x_i\) 是无限的。

**证明.** 设 \(G\) 是一个与所有 \(D_{0,i}\) 和 \(D_{1,i}\) 对所有 \(i \in I\) 相遇的通用集。如果 \(i \in X\)，则由引理 6.3.4 的 (ii)，\(x_i \cap g\) 是无限的。如果 \(i \notin X\)，则由引理 6.3.4 的 (i)，对某些 \(p \in G\) 有 \(x_i \subseteq \text{Dom}(p)\)。但 \(|\{n \mid p(n) = 1\}| < \infty\)，因此 \(x_i \cap g\) 是有限的。

因此，近乎不相交强迫产生一个实数 \(g\)，它通过一个近乎不相交集 \(A\) 编码一个大集 \(X\)。

### 引理 6.3.6.

假设 \(\text{MA}_{\aleph_1}\) 并假设对于某些 \(x \in 2^\omega\) 有 \((\omega_1)^{L[x]} = \omega_1\)。如果 \(B \subseteq 2^\omega\) 的基数为 \(\aleph_1\)，那么 \(B\) 是 \(\Pi^1_1\)。

**证明.** 我们假设对于任何 \(x \in B\) 有 \(x(0) = 1\)。

由于 \((\omega_1)^{L[x]} = \omega_1\)，令 \(C = \{z \mid z(0) = 0 \wedge z \in L_{\omega_1^{L[x]}}[z \oplus x]\}\)。那么 \(C\) 是一个基数为 \(\aleph_1\) 的 \(\Pi^1_1\) 集。

设 \(f : \omega \to 2^\omega\) 为一个递归双射。定义

\(T = \{t \in 2^{<\omega} \mid (\exists \tau \in 2^{<\omega})(\forall n < |t|)(t(n) = 1 \mapsto f(n) \prec \tau)\}.\)

注意 \(T\) 是一个近乎不相交集树。而且 \(T\) 是一个递归完美树，并且存在一个递归同态 \(h : 2^\omega \to [T]\)。还要注意，任何 \(x \in [T]\) 在其每个无限子集中都是递归的。令 \(C_0 = \{y \mid (\exists x \in C)(h(x) = y)\}\) 和 \(B_0 = \{y \mid (\exists x \in B)(h(x) = y)\}\)。假设 \(p_0, p_1, \dots\) 是素数的递归枚举。令

- \(B_0 = \{x_a\}_{a < \aleph_1},\)
- \(C_0 = \{y_a\}_{a < \aleph_1},\)
- \(B_1 = \{x_{a,n} \mid (\forall i \in \omega)(x_{a,n}(i) = 1 \leftrightarrow (\exists j)(i \text{ is the } p_n^j\text{-th element of } x_a))\}\)

和

\(C_1 = \{y_{a,n} \mid (\forall i \in \omega)(y_{a,n}(i) = 1 \leftrightarrow (\exists j)(i \text{ is the } p_n^j\text{-th element of } y_a))\}.\)

令 \(B = B_0 \cup C_0\)。那么 \(A\) 是近乎不相交的，且 \(x \in C_1\) 仅当

- (i) 存在一个 \(z \le_T x\) 和一个 \(n \in \omega\) 使得 \(z \in C_0\)，且
- (ii) \((\forall i \in \omega)(x(i) = 1 \leftrightarrow (\exists j)(i \text{ is the } p_n^j\text{-th element of } z))\)。

那么 \(C_1\) 是 \(\Pi_1^1\)。由 \(\text{MA}_{\aleph_1}\)、引理 6.3.3 和定理 6.3.5，存在一个实数 \(g\) 使得对于任何 \(\alpha < \aleph_1\) 和 \(n \in \omega\)，

- 1. \(g \cap \chi_{\alpha, 2n+1}\) 是无限的仅当 \(n \notin \chi_\alpha\)；且
- 2. \(g \cap \chi_{\alpha, 2n+2}\) 是无限的仅当 \(n \in \chi_\alpha\)。

设 \(h_0\) 为一个函数，使得 \(h_0(x, n) = i\)（如果 \((\exists j)(i\) 是 \(x\) 的 \(p_j^i\)-th 元素)）。注意 \(h_0(x_\alpha, n) = \chi_{\alpha, n}\) 和 \(h_0(y_\alpha, n) = y_{\alpha, n}\)。

令 \(h_1(x) = \{n \mid h_0(x, 2n + 1) \cap g\} = \text{co}\infty\) 和 \(h_2(x) = \{n \mid h_0(x, 2n + 2) \cap g\} = \text{co}\infty\)。

那么对于任何 \(x \in 2^\omega\)，\(x \in B_0 \leftrightarrow h_1(x) \in C_0 \land h_2(h_1(x)) = x\)，

这表明 \(B\) 是 \(\Pi_1^1\)。

### 定理 6.3.7 (Martin 和 Solovay [90]).

假设 \(\text{MA}_{\aleph_1}\)。那么对于某些 \(x \in 2^\omega\) 有 \((\omega_1)^{[L[x]]} = \omega_1\) 当且仅当每个基数为 \(\aleph_1\) 的 \(2^\omega\) 的子集是 \(\Pi_1^1\)。

**证明.**

假设对于所有 \(x \in 2^\omega\) 有 \((\omega_1)^{[L[x]]} < \omega_1\)。令 \(A = \{x_\alpha\}_{\alpha < \omega_1}\) 为图灵度的最大链。那么 \(A\) 的基数为 \(\aleph_1\) 且不包含完美子集。由此可知，对于任何实数 \(x\)，\(A\) 必须包含一个在 \(L[x]\) 中不可构造的实数。如果 \(A\) 是某些 \(x_0\) 的 \(\Pi_1^1(x_0)\)，则由引理 4.3.2，\(A\) 包含一个完美子集，这是矛盾。

反之，假设对于某些 \(x \in 2^\omega\) 有 \((\omega_1)^{[L[x]]} = \omega_1\)。由引理 6.3.6，每个基数为 \(\aleph_1\) 的 \(2^\omega\) 的子集是 \(\Pi_1^1\)。

### 注记 6.3.8.

定理 6.3.7 可以被视为一个超越递归理论“极限”的结果，在该理论中，通常先证明一个定理的浅色版本，然后将其相对化为深色版本。然而，在这种情况下，定理 6.3.7 没有浅色版本。

定理 6.3.7 的一个直接后果（见练习 6.3.3）是，如果 \(\text{MA}_{\aleph_1}\) 成立，那么对于某些 \(x \in 2^\omega\) 有 \((\omega_1)^{[L[x]]} = \omega_1\) 当且仅当每个 \(\aleph_1\) 个博雷尔集的并是 \(\Sigma_2^1\)。与此形成对比的是，Harrington [44] 证明了对于任何基数 \(\kappa < 2^{\aleph_0}\)，存在一个 ZFC 的模型，其中任何 \(\kappa\) 个博雷尔集的并是 \(\Pi_2^1\)。

### 6.3.3 练习

### 练习 6.3.1 (Martin 和 Solovay [90]).

假设 MA。证明对于任何 \(X \subset 2^{\aleph_0}\) 且 \(|X| < 2^{\aleph_0}\)，存在一个实数 \(g\) 使得 \(L[g] = L[X]\)。

### 练习 6.3.2 (Martin 和 Solovay [90]).

假设 MA。证明对于任何 \(\kappa < 2^{\aleph_0}\) 有 \(2^\kappa = 2^{\aleph_0}\)。

### 练习 6.3.3 (Martin 和 Solovay [90]).

假设 \(\text{MA}_{\aleph_1}\)。证明对于某些 \(x \in 2^\omega\) 有 \((\omega_1)^{[L[x]]} = \omega_1\) 当且仅当每个 \(\aleph_1\) 个博雷尔集的并是 \(\Sigma_2^1\)。

### 练习 6.3.4 (Harrington [44]).

如果 \(\mathcal{M} \in \text{ZFC} + \omega_1 = \omega_1^L\) 且 \(A \subset 2^\omega\) 在 \(\mathcal{M}\) 中，那么存在 \(\mathcal{M}\) 的一个 c.c.c. 扩展 \(\mathcal{N}\)，其中 \(A\) 是 \(\Pi_2^1\)。

## 6.4 大基数

尽管对于集合论有一套相当全面的公理，但已知有相当多的重要数学问题独立于 ZF。为了研究这些问题，引入了额外的假设，其中涉及大基数概念的假设。我们在这里讨论其中一些。

### 6.4.1 不可达基数

### 定义 6.4.1.

- 一个基数 \(\kappa\) 是 *不可达的* 如果 \(\kappa\) 是正则的，并且对于每个基数 \(\nu < \kappa\)，\(2^\nu < \kappa\)；
- 一个基数 \(\kappa\) 是 *弱不可达的* 如果 \(\kappa\) 是一个正则极限基数。

我们这里只考虑 \(\kappa > \omega\)。存在一个不可达基数的假设是最弱的大基数公理。如果 \(\kappa\) 是不可达的，那么 ZFC \(\vdash\) "\((V_\kappa, \in) \vDash\) ZFC"。换句话说，ZFC + "\(\exists \kappa (\kappa \text{ 是不可达的})\)" 蕴含 ZFC 是相容的。由哥德尔第二不完备定理，ZFC + "ZFC 是相容的" 不蕴含 "ZFC + \(\exists \kappa (\kappa \text{ 是不可达的})\)" 的相容性。这意味着，不能通过假设存在 ZFC 的模型来构造 "ZFC + \(\exists \kappa (\kappa \text{ 是不可达的})\)" 的模型。

乍一看，不可达基数的概念似乎与实数集的结构无关。相当令人惊讶的是，两者有着密切的联系，如下例所示。

### 命题 6.4.2 (Solovay [149]).

如果不存在不可数的 \(\Pi^1_1\)-稀疏集，那么 \(\omega_1\) 在 \(L\) 中是不可达的。

**证明.** 显然 \(\omega_1\) 在 \(L\) 中是正则的。由于 \((L, \epsilon) \vDash\) GCH，只需证明 \(\omega_1\) 在 \(L\) 中是一个极限基数。

假设不是。那么存在一个可数序数 \(\gamma < \omega_1\) 使得 \((L, \epsilon) \vDash \omega_1 = \gamma^+ = 2^\gamma\)。由于 \(\gamma\) 是可数的，存在一个 \(x\) 计算出 \(\omega\) 的一个良序，其序类型为 \(\gamma\)。那么 \((L[x], \epsilon) \vDash 2^\omega = \omega_1\)。将角 corollary 4.3.6 的证明相对化到 \(x\)，我们得到 \(\{z \mid z \in L_{\omega_1^{CK}}[x]\}\) 是一个不可数的 \(\Pi^1_1(x)\)-稀疏集，矛盾。

命题 6.4.2 涉及描述集合论中的经典主题，即不可数可定义实数集的完美子集的存在性。它指出，要求所有 \(\Pi^1_1\)-集都是“良好行为”的，至少需要诉诸不可达基数的存在。这种情况可以从逆数学的角度来看待，逆数学是一个研究在“普通数学”中证明定理所必需且充分的集合存在公理的方案。在当前语境中，人们关心的是集合论公理，这些公理是相对于 ZF 或 ZFC 的相容性，在描述集合论中建立一个陈述的相容性所必需且充分的。更精确地说，给定描述集合论中的这样一个陈述 \(\varphi\)



理论，是否存在一个大基数公理 \(\psi\) 使得 ZFC \(+\varphi\)（或 ZF \(+\varphi\)）的相容性当且仅当 ZFC \(+\psi\) 的相容性成立？当这成立时，我们说 \(\varphi\) 与 \(\psi\) 相容性等价。索洛维（Solovay）的下一个结果体现了这一点。

### 提议 6.4.3 (Solovay [149]). 每个不可数 \(\Pi^1_1\)-集都有完美子集这一命题与不可达基数的存在性在相容性意义上等价。

证明。根据提议 6.4.2，每个不可数 \(\Pi^1_1\)-集都有完美子集这一命题蕴含 \(\omega_1\) 在 L 中是不可达的。因此在 ZFC 下，该命题的相容性蕴含不可达基数存在性的相容性。

现在假设在 ZFC 的过渡模型 \(\mathfrak{M}\) 中存在一个不可达基数 \(\kappa\)。在 \(\mathfrak{M}\) 上固定一个 L(\(\kappa\))-通用集 \(G\)。根据提议 6.2.9，\(\kappa = (\omega_1)^{\mathfrak{M}[G]}\)。令 \(x \in \mathfrak{M}[G]\)。那么存在一串条件 \(\cdots \le p_n \le \cdots \le p_0\)，使得对于任意 \(n\)，\(p_n \in G\) 强制 \(x(n)\) 的值。由于 \(\kappa = (\omega_1)^{\mathfrak{M}[G]}\)，存在一个正则基数 \(\eta < \kappa\)，使得对每个 \(n\) 都有 \(p_n \in \mathbf{L}(\eta)\)，从而 \(x \in \mathfrak{M}[G \cap \mathbf{L}(\eta)]\)。因此 \((\omega_1)^{L[x]} \le (\omega_1)^{\mathfrak{M}[G \cap \mathbf{L}(\eta)]} < \kappa < \omega_1\)。换句话说，

\(\mathfrak{M}[G] \models \text{"}(\omega_1)^{L[x]} < \omega_1\text{"}.\)

将角 corollary 4.3.6 的证明相对化到 x，我们得出最大的 \(\Pi^1_1(x)\)-稀疏集 \(\{z \mid z \in L_{\omega_1^{x+}}[x]\}\) 是可数的。那么

\(\mathfrak{M}[G] \models \text{"Every uncountable } \Pi^1_1\text{-set has a perfect subset".}\)

### 6.4.2 可测基数

对于给定的无限基数 \(\kappa\)，将 \(\mathscr{P}(\kappa)\) 视为在 \(\subseteq\) 下的偏序集。

### 定义 6.4.4.

- 一个集合 \(A \subseteq \mathscr{P}(\kappa)\) 是 \(\kappa\) 上的超滤子，如果它是一个滤子，并且对于任何 \(a \subseteq \kappa\)，要么 \(a \in A\)，要么 \(\kappa \setminus a \in A\);
- 一个滤子 \(A\) 是非主的，如果对于任何 \(a \in A\)，存在 \(b \in A\) 使得 \(a \not\subseteq b\);
- 令 \(\eta \le \kappa\) 为一个基数。一个滤子 \(A\) 是 \(\eta\)-完备的，如果对于任何 \(\beta < \eta\) 和 \(A\) 中的任何序列 \(\{a_\alpha\}_{\alpha < \beta}\)，\(\cap_{\alpha < \beta} a_\alpha \in A\)。

\(\kappa\) 上的一个 \(\kappa\)-完备非主超滤子 \(A\) 在 \(\mathscr{P}(\kappa)\) 上诱导出一个 \(\kappa\)-可加零一测度 \(\mu\)，定义方式为：对于任何 \(a \subseteq \kappa\)，\(\mu(a) = 1\) 当且仅当 \(a \in A\)。在 ZFC 下构造 \(\omega\) 上的一个 \(\omega\)-完备非主超滤子 \(A\) 并不困难。然而，对于 \(\kappa > \omega\)，在同一公理系统中无法证明 \(\kappa\) 上的 \(\kappa\)-完备非主超滤子 \(A\) 存在。

### 定义 6.4.5. 我们说 \(\kappa > \omega\) 是可测的，如果存在 \(\kappa\) 上的一个 \(\kappa\)-完备非主超滤子 \(A\)。

可以证明，每个可测基数都是不可达的（参见 [53]）。可测基数的存在性是一个非常强的大基数假设。尽管它是集合论中的一个主要概念，但本书中证明的结果没有一个需要这个假设。

### 6.4.3 \(0^\#\)

与可测基数相比，\(0^\#\) 是一个相对较小的大基数。尽管如此，它在可定义性研究中扮演着重要角色。根据 Slaman（哥德尔讲座，2001），“\(0^\#\) 是递归理论家进入集合论的通行证”。以一种相当引人注目的方式，\(0^\#\) 的定义比迄今考虑过的大基数的定义更为复杂。

### 定义 6.4.6. 假设

- (i) 对于任意一对不可数基数 \(\eta < \kappa\)，\((L_\eta, \in) \prec (L_\kappa, \in)\);
- (ii) 存在一个包含所有不可数基数的序数的唯一闭无界类 \(I\)，使得对于任何基数 \(\kappa > \omega\)，
  - (a) \(|I \cap \kappa| = \kappa\);
  - (b) 对于任何 \(\psi(v_0, \dots, v_k)\)，以及 \(I \cap \kappa\) 中的任意两个递增序列 \(\gamma_0^0 < \dots < \gamma_k^0\) 和 \(\gamma_1^1 < \dots < \gamma_k^1\)，都有 \((L_\kappa, \in) \vDash \psi(\gamma_0^0, \dots, \gamma_k^0) \Leftrightarrow (L_\kappa, \in) \vDash \psi(\gamma_1^1, \dots, \gamma_k^1)\);
  - (c) 每个元素 \(a \in L_\kappa\) 都可以在 \((L_\kappa, \in)\) 中用 \(I \cap \kappa\) 中的参数定义。

那么 \(n \in 0^\#\) 当且仅当 \(n\) 是一个公式 \(\varphi\) 的 Gödel 数，使得 \((L_{\aleph_\omega}, \in) \vDash \varphi(\aleph_1, \dots, \aleph_{m+1})\)。

术语 \(0^\#\) 由 Solovay 引入。Gaifman [32] 证明 \(0^\#\) 的存在性可从可测基数的存在性推出。Silver [137] 在假设存在 Ramsey 基数的情况下得出了相同结论，已知 Ramsey 基数比可测基数弱。Solovay [148] 证明 \(0^\#\) 是一个非可构的 \(\Delta_2^1\)-整数集。由于每个 \(\Delta_2^1\)-实数都属于 \(L\)（角 corollary 4.2.9 (iii)），这在大基数假设下给出了实数可构性的最优界 \(\Delta_2^1\)。

尽管 \(0^\#\) 的定义在集合论语言中看起来是不可定义的，但它可以从模型论角度重新表述。这使得 Silver 能够证明 \(0^\#\) 是一个 \(\Pi_2^1\)-单点集，因此也是 \(\Delta_2^1\)，\(0^\#\) 很可能是与 \(V = L\) 不兼容的最弱大基数公理。

### 提议 6.4.7. 如果 \(0^\#\) 存在，那么每个可构实数在 \(0^\#\) 中是递归的。因此只有可数多个可构实数。

证明。假设 \(0^\#\) 存在且 \(x\) 是可构的。由于 \(x \in L_{\omega_1}\)，根据定义 6.4.6 (ii)，存在一个公式 \(\varphi_v(v, u_1, \dots, u_m)\) 和 \(I \cap L_{\omega_1}\) 中的一个递增序列 \(i_1, \dots, i_m\)，使得对于任意 \(n < \omega\)，\(n \in x\) 当且仅当 \((L_{\omega_1}, \in) \vDash \varphi_x(n, i_1, \dots, i_m)\)。

对于每个 \(n\)，令 \(\varphi_n(v)\) 为定义 \(n\) 的公式，使得

$$(\exists v_0) \cdots (\exists v_n)(\forall v)(\varphi_n(v_0) \land v_1 = v_0 \cup \{v_0\} \land v_2 = v_1 \cup \{v_1\} \land \dots \land v_n = v_{n-1} \cup \{v_{n-1}\} \land v = v_n).$$

那么

$$n \in x \Leftrightarrow (L_{\omega_1}, \in) \models (\exists v)(\varphi_n(v) \land \varphi_x(v, i_1, \dots, i_m)).$$

根据定义 6.4.6 (i) 和 (ii),

$$n \in x \Leftrightarrow (L_{\aleph_\omega}, \in) \models (\exists v)(\varphi_n(v) \land \varphi_x(v, \aleph_1, \dots, \aleph_m)).$$

显然集合 \(\{(\exists v)(\varphi_n(v) \land \varphi_x(v, u_1, \dots, u_m)) \mid n < \omega\}\) 是递归的，并且

$$n \in x \Leftrightarrow \ulcorner (\exists v)(\varphi_n(v) \land \varphi_x(v, u_1, \dots, u_m)) \urcorner \in 0^\sharp.$$

因此 \(x \le_T 0^\sharp\)。

提议 6.4.7 蕴含 \(0^\sharp\) 具有极高的计算能力。从递归论角度看，可以将 \(0^\sharp\) 视为 #-算子下 \(\emptyset\) 的“跳跃”。

尽管 \(0^\sharp\) 在 \(L\) 中压缩了基数，但它的缺失则由 Jensen 杰出的覆盖引理（Covering Lemma）呈现出截然不同的图景。

### 定理 6.4.8 (Jensen [21]). 如果 \(0^\sharp\) 不存在，那么每个不可数序数集都包含在一个同基数的可构集中。

## 6.5 确定性公理

在本书中，我们的重点主要放在低层次可定义的实数集上，例如 \(\Pi^1_1\) 或 \(\Sigma^1_2\) 这样的集合。要“更进一步”，人们诉诸于游戏和策略的使用，它们是确定性公理的核心。事实证明，这个公理的核心是一个大基数公理。

### 6.5.1 游戏和策略

令 \(A \subseteq \omega^\omega\)。一个具有完备信息的无限游戏 \(G_A\) 有两名玩家，分别标记为 I 和 II。游戏由两名玩家交替选择自然数进行，并在 \(\omega\) 多步后结束。每个游戏生成一个实数 \(x = (n_0, m_0, \dots, n_i, m_i, \dots) \in \omega^\omega\)，其中 \(n_i\) 和 \(m_i\) 分别是 I 和 II 在步骤 i 中选择的数字。如果 \(x \in A\)，则 I 获胜。否则，II 获胜。

### 定义 6.5.1.

给定一个集合 \(A \subseteq \omega^\omega\)，如果对于每个 \(g \in \omega^\omega\)，实数 \(\vec{\sigma} * g = (n_0, g(0), \dots, n_i, g(n_i), \dots) \in A\)，其中 \(n_0 = \vec{\sigma}(0)\) 且对于 \(i > 0\) 有 \(n_i = \vec{\sigma}(\langle n_0, g(0), \dots, n_{i-1}, g(i-1) \rangle)\)，则 I 对游戏 \(G_A\) 有一个获胜策略 \(\vec{\sigma} : \omega^{<\omega} \to \omega\)。字符串



(n_0, m_0, ..., n_i) 被称为 I 在第 i 步遵循 \tilde{\sigma} 进行的对局。II 对于博弈 G_A 拥有获胜策略 \tilde{\tau} : ^\omega \omega \to \omega，当且仅当对于每个 f \in ^\omega \omega，实数 f * \tilde{\tau} = (f(0), m_0, ..., f(i), m_i, ...) \notin A，其中 m_0 = \tilde{\tau}(f(0)) 且对 i > 0 有 m_i = \tilde{\tau}(f(0), m_0, ..., f(i))。字符串 f(0), m_0, ..., m_i 被称为 II 在第 i 步遵循 \tilde{\tau} 进行的对局。如果两名玩家中的任意一名拥有获胜策略，则称 G_A 是确定的。

### 定义 6.5.2. 确定性公理 (AD) 断言，对于任意 A \in ^\omega \omega，I 或 II 中的一方对 G_A 拥有获胜策略。

不难看出 AC 与 AD 相矛盾。然而，只要 A 是简单定义的，G_A 就是确定的。

### 命题 6.5.3. 如果 A 是闭集，则 G_A 是确定的。

证明. 由于 A 是闭集，存在一棵树 T \subseteq ^{<\omega} \omega 使得 A = [T]。假设 II 没有获胜策略。我们定义一个 I-获胜策略 \tilde{\sigma} 如下：

令 \tilde{\sigma}(0) 为一个 n_0，使得 II 在 G_{T[(n_0)]} 上没有获胜策略，其中 T_{(n_0)} = \{ \tau \in T | n_0 \le \tau \}，且 n_0 是长度为 1、在 0 处的值为 n_0 的字符串。注意，根据 II 没有获胜策略的假设，n_0 存在。

通过归纳假设 \tilde{\sigma} 已定义于长度不超过 i - 1 的序列，且 II 在 G_{T[(n_0, m_0, ..., n_{i-1})]} 上没有获胜策略，其中

T_{(n_0, m_0, ..., n_{i-1})} = \{ \tau \in T | (n_0, m_0, ..., n_{i-1}) \le \tau \},

对于 I 遵循 \tilde{\sigma} 进行的序列 (n_0, m_0, ..., m_i)。那么存在一个 n_i，使得 II 在 G_{T[(n_0, m_0, ..., m_i)]} 上没有获胜策略，其中

T_{(n_0, m_0, ..., m_i, n_i)} = \{ \tau \in T | (n_0, m_0, ..., m_{i-1}, n_i) \le \tau \}.

令

\tilde{\sigma}((n_0, m_0, ..., m_{i-1})) = n_i.

那么对于任意 g \in ^\omega \omega 和数字 k，\tilde{\sigma} * g \upharpoonright k \in T。因此 \tilde{\sigma} * g \notin A，因为 A 是闭集。

并非总是成立：若 G_A 确定，则 G_{^\omega \omega \setminus A} 也确定（参见练习 6.5.1）。然而，下一命题表明，当 A 是闭集时，这个补集性质成立。

### 命题 6.5.4. 假设 \Gamma \subseteq \mathscr{P}(^\omega \omega)，使得对于任意 A \in \Gamma 和字符串 \sigma \in ^{<\omega} \omega，集合 A_\sigma = \{ x | ^\sigma x \in A \} \in \Gamma。如果对于每个 A \in \Gamma，G_A 都是确定的，那么对于每个 A \in \Gamma，G_{^\omega \omega \setminus A} 也是确定的。

证明. 假设 A \in \Gamma。注意，对于任意 n，A_n = \{ x | ^n x \in A \} \in \Gamma，因此 G_{A_n} 是确定的。

情况 (1) 存在一个 n_0，使得玩家 II 对 G_{A_{n_0}} 拥有获胜策略 \tilde{\tau}。令 \tilde{\sigma}(0) = n_0。对于任意字符串 (n_0, m_0, ..., m_i)，令 \tilde{\sigma}((n_0, m_0, ..., m_i)) 为 \tilde{\tau}(m_0, ..., m_i)。那么 \tilde{\sigma} 是玩家 I 对 G_{^\omega \omega \setminus A} 的获胜策略。

情况 (2) 否则。那么对于每个 n，玩家 I 对 G_{A_n} 拥有获胜策略 \tilde{\sigma}_n。定义 \tilde{\tau}，使得对于每个 n，\tilde{\tau}(n) = \tilde{\sigma}_n(0)，并且对于任意字符串 (n_0, m_0, ..., n_i)，\tilde{\tau}(n_0, m_0, ..., n_i) = \tilde{\sigma}_{n_i}(m_0, ..., n_j)。那么 \tilde{\tau} 是 II 对博弈 G_{\omega^\omega \setminus A} 的获胜策略。

在 ZF 中可证的确定性的最优结果归功于马丁。这里的最优意味着，任何更强的版本本质上都是一个大基数公理。令 DC 表示依赖选择公理：

### 定理 6.5.5 (Martin [93]). ZF + DC “每个博雷尔集都是确定的”。

### 定理 6.5.6 (Martin [92] 和 Harrington [45]). \( \Pi^1_1 \)-确定性与 \( 0^\sharp \) 的存在等价。

关于 AD 的状况更为复杂。详细讨论将涉及 Woodin 基数的概念，我们在此不予定义。尽管如此，伍丁、马丁和斯蒂尔已经证明 ZF + AD 与 ZFC + “存在无穷多个 Woodin 基数” 相对相容。伍丁还证明了以下内容：

- **定理 6.5.7** (Woodin). 以下各项等价：
- (i) ZF + DC + \( \Delta_2^1 \)-确定性是相容的；
- (ii) ZF + DC + 分析确定性是相容的；
- (iii) ZFC + “存在一个 Woodin 基数” 是相容的。

伍丁以及马丁和斯蒂尔 [95] 还在射影层次结构中（称为射影确定性）提供了确定性的逐层分析。

### 6.5.2 练习

### 练习 6.5.1. 假设 ZFC。证明存在一个集合 \( A \)，使得 \( G_A \) 是确定的，但 \( G_{\omega^\omega \setminus A} \) 不是。

## 6.6 确定性的递归论方面

从递归论的角度研究确定性是由马丁发起的。一个自然的起点是分析获胜策略的复杂性。

### 6.6.1 获胜策略的基础定理

如果 \( A \) 是 \( \Pi^1_1 \)，那么集合 \( \{\hat{\sigma} \mid (\forall g)((\hat{\sigma} * g \in A))\} \) 和 \( \{\hat{\tau} \mid (\forall f)(f * \hat{\tau} \in A)\} \) 都是 \( \Pi^1_1 \)。根据推论 4.2.7，I 或 II 中的一方存在一个 \( \Delta^1_1 \)-获胜策略。然而，即使对于 \( \Pi^1_2 \)-集，也无法显著改进上界。

### 定理 6.6.1 (Blass [7]). 假设 \( A \) 是 \( \Pi^1_1 \)。如果 I 对 \( G_A \) 有获胜策略，那么 I 有一个在 \( O \) 中递归的获胜策略；如果 II 对 \( G_A \) 有获胜策略，那么 II 有一个超算术的获胜策略。

证明. 由于 \( A \) 是 \( \Pi^1_1 \)，存在一棵递归树 \( T \subseteq \omega^{<\omega} \) 使得 \( A = [T] \)。假设 I 有获胜策略。那么集合

\( B = \{\hat{\sigma} \mid (\forall i)(\forall \sigma \in \omega^i)((\hat{\sigma} \text{ 是 I 遵循 } \hat{\sigma} \text{ 在第 } i \text{ 步进行的对局}) \to (\exists x)(\sigma \frown x \in A))\} \)

是一个非空的 \( \Sigma^1_1 \)-集。根据 Gandy 基础定理 (2.5.3)，存在一个 \( \hat{\sigma}_0 \le_T O \) 在 B 中。显然 \( \hat{\sigma}_0 \) 是玩家 I 的获胜策略。

现在假设 I 没有获胜策略。令 \( n \in \omega^* \setminus 0 \)。那么 \( \Omega^1_n = \{m \mid m \le_{\sigma^*} n\} \) 是一个递归可枚举集（r.e. 集），在 r.e. 线性序关系 \( <_{\sigma^*} \) 下具有一个序类型为 \( \sigma^1_{CK} \) 的初始段。定义一个从 \( \omega^{<\omega} \) 到 \( \Omega^1_n \) 的函数的算术集 C 如下：\( f \in C \) 当且仅当对于任意 \( \sigma \),

(i) 如果 \( |\sigma| \le |T| \)，则 \( f(\sigma) \) 未定义；
(ii) 如果 \( |\sigma| \cap |T| = \emptyset \)，则 \( f(\sigma) = 1 \)；
(iii) 假设 \( \sigma \) 不满足 (i) 或 (ii)。(a) 如果 \( |\sigma| \) 是偶数，则当 \( i = \sup\{k \mid k = f(\sigma^i)\} \) 存在时（sup 在 \( <_{\sigma^*} \) 的意义下），\( f(\sigma) = 2^i \)；否则，\( f(\sigma) \) 未定义。(b) 如果 \( |\sigma| \) 是奇数，则当 \( i = \inf\{k \mid k = f(\sigma^m)\} \) 存在时（inf 在 \( <_{\sigma^*} \) 的意义下），\( f(\sigma) = 2^i \)；否则，\( f(\sigma) \) 未定义。

由于 \( \Omega \cap O^1_\alpha \) 是 \( \Omega^1_n \) 的最大良序段，对于任意 \( f \in C \) 和 \( \sigma \)，如果 \( f(\sigma) \) 已定义，则 \( f(\sigma) \in O \)。

**主张 1.** 假设 \( \sigma \) 满足 (iii)(a)。如果对于任意 m，存在一个超算术部分函数 \( f_m \in C \) 使得 \( f_m(\sigma^m) \) 已定义，那么存在一个超算术部分函数 \( f \in C \) 使得 \( f(\sigma) \) 已定义。

主张 1 的证明. 定义一个 \( \Pi^1_1 \)-关系 \( R \subseteq \omega \times (\omega \times \omega) \) 如下：\( (m, (e, i)) \in R \) 当且仅当 \( i \in O \) 且 \( \emptyset_e^O \in C \)，使得 \( \emptyset_e^O(\sigma^m) \) 已定义。根据定理 4.21，存在一个 \( \Pi^1_1 \)-函数 \( g : \omega \to \omega \times \omega \) 一致化 R。根据假设，g 是全函数，因此是超算术的。

定义 f 为一个超算术函数，使得对于任意 m 和 \( r \ge \sigma^m \)，\( f(r) = \Phi_{g(m)}^{H_{r_1}}(r) \)，其中 \( g(m) = (m_0, m_1) \)。显然 \( f \in C \)。此外，由于 f 是超算术的，\( \sup\{k \mid k = f(\sigma^m)\} \) 存在，因此 \( f(\sigma) \) 已定义。

**主张 2.** 存在一个超算术的 \( g \in C \)，使得 g(0) 已定义。





主张2的证明。假设不然。我们为I在$G_A$中对弈获得如下获胜策略$\tilde{\sigma}$：

根据主张1，存在一个$m$，使得不存在超算术函数$f \in C$使得$f(m)$有定义。令$\tilde{\sigma}(0) = m$。注意，根据(iii)，对于任何超算术$f \in C$和数字$j$，$f(m^j)$未定义。

对$k$进行归纳，对于I遵循$\tilde{\sigma}$在第$k$步的任何对弈$(i_0, j_0, \dots, i_k)$，不存在超算术$f \in C$使得$f((i_0, j_0, \dots, i_k))$有定义。那么对于任何$j_k$和任何超算术$f \in C$，$f((i_0, j_0, \dots, i_k, j_k))$未定义。根据主张1，存在一个$i_{k+1}$，使得不存在超算术函数$f_{i_{k+1}} \in C$使得$f_{i_{k+1}}((i_0, j_0, \dots, i_k, j_k, i_{k+1}))$有定义。令$\tilde{\sigma}((i_0, j_0, \dots, i_k, j_k)) = i_{k+1}$。那么$\tilde{\sigma}$是I的获胜策略，与假设矛盾。

因此存在超算术函数$g \in C$使得$g(0) \in \mathcal{O}$。我们为II定义超算术策略$\tilde{\tau}_g$如下：对于每个$n$，令$\tilde{\tau}_g(n) = m$，其中$g(m) <_{\mathcal{O}} g(0)$。对于每个$k$和长度为偶数的$a \in \omega^{<\omega}$，令$\tilde{\tau}_g(a * k) = m$，其中$(a * k * m) <_{\mathcal{O}} g(a)$（如果存在）。

我们声称$\tilde{\tau}_g$是II的获胜策略。要看到这一点，对于任何$h \in \omega^\omega$，对于任何使得$g(h * \tilde{\tau}_g \upharpoonright 2k) > 1$的$k$，都有$g(h * \tilde{\tau}_g \upharpoonright 2k + 2) <_{\mathcal{O}} g(h * \tilde{\tau}_g \upharpoonright 2k)$。由于$g(0) \in \mathcal{O}$，存在一个$k$使得$g(h * \tilde{\tau}_g \upharpoonright 2k) = 1$。因此$h * \tilde{\tau}_g \in \omega^\omega \setminus A$。

关于解析层级的一个一般基础定理是以下由Moschovakis提出的第三周期性定理。

### 定理 6.6.2 (Moschovakis [107]).

- (i) 假设每个$\Sigma^1_{2n}$-集都是确定的。如果I对$G_A$有获胜策略，其中$A$是$\Sigma^1_{2n}$，那么I有一个$\Delta^1_{2n+1}$-获胜策略。

- (ii) 假设每个$\Delta^1_{2n}$-集都是确定的。如果I对$G_A$有获胜策略，其中$A$是$\Pi^1_{2n+1}$，那么I有一个$\Delta^1_{2n+2}$-获胜策略。

### 6.6.2 图灵度的圆锥

一组图灵度$\mathbf{A}$是一个圆锥，如果存在一个$\mathbf{z}$使得$\mathbf{A} = \{\mathbf{x} \mid \mathbf{x} \ge \mathbf{z}\}$。我们称$\mathbf{z}$为$\mathbf{A}$的底。

### 提议 6.6.3. 假设ZF + AD。对于任何图灵度集合$\mathbf{A}$，$\mathbf{A}$或其补集包含一个图灵度圆锥。

### 证明。

令$A = (\mathbf{x} \mid \mathbf{x} \in \mathbf{A})$。假设I对$G_A$有获胜策略$\tilde{\sigma}$。那么对于任何$g \ge_T \tilde{\sigma}$，$h * g \equiv_T g$。因此$g \in A$。故$\mathbf{A}$包含一个图灵度圆锥。

如果II对$G_A$有获胜策略$\tilde{\tau}$，则通过相同的论证，$\mathbf{A}$的补集包含一个图灵度圆锥。

尽管提议6.6.3的证明看起来简单直接，但它揭示了一个显著的事实：图灵度的全局结构可能对集合论假设敏感。

### 定义 6.6.4.

- \( A \in \omega^\omega \) 是终沓的，如果对于每个$x$，存在一个$y \in A$使得$y \ge_T x$。
- 树\( T \in \omega^{<\omega} \) 是尖的，如果\( T \) 是完美的，并且对于任何\( x \in [T] \)，\( x \ge_T T \)。
- 尖树\( T \) 是一致尖的，如果存在一个\( e \) 使得对于任何\( x \in [T] \)，\( T = \Phi^e_x \)。

### 提议 6.6.5 (Martin [91]).

ZF + DC + AD 蕴含每个终沓实数集都有一个一致尖子树。

### 证明。

假设\( A \subseteq \omega^\omega \)是终沓的。令\( B \subseteq \omega^\omega \)使得\( z = x \oplus y \in B \)当且仅当以下之一成立：

- \( x \notin_T y \)；或
- \( x \le_T y \) 且 \( y \notin A \)。

根据AD，\( G_B \) 是确定的。假设II有获胜策略 \( \dot{\sigma} \)。令\( y \in A \) 使得\( y \ge_T \dot{\tau} \)。那么对于某些\( x \le_T y \)，\( \dot{\sigma} * y = y \oplus x \)。因此 \( \dot{\sigma} * y \notin B \)。

故II有获胜策略 \( \dot{\tau} \)。令\( T_0 \subseteq 2^{<\omega} \) 为一个一致尖树，使得\( T_0 \models \dot{\tau} \)（参见练习6.6.1）。定义\( T_1 \) 使得\( (n_0, \dots, n_i) \in T_1 \) 当且仅当存在有限字符串\( (m_0, \dots, m_i) \in T_0 \) 使得\( (m_0, n_0, \dots, m_i, n_i) \) 是II在第\( i \) 步遵循 \( \dot{\tau} \) 的一次对弈。显然 \( T_1 \le_T \dot{\tau} \)。由于 \( \dot{\tau} \) 是II的获胜策略，对于任何\( y \in [T_1] \)，存在一个\( x \in [T_0] \) 使得\( y = x \oplus \dot{\tau} \) 且 \( \dot{\tau} * x \le_T y \)。此外 \( T_1 \) 是一棵完美树：每个\( \tau = (m_0, \dots, n_i) \in T_1 \)，它是某个\( \sigma = (m_0, \dots, m_i) \in T_0 \) 的像（即II在第\( i \) 步遵循 \( \dot{\tau} \) 的对弈 \( (m_0, n_0, \dots, m_i, n_i) \)），在\( T_1 \) 中都有一对（直接的）不兼容扩展 \( \tau_1 \) 和 \( \tau_2 \)，使得存在 \( x_1, x_2 >_T x \) 且 \( x_1 * \dot{\tau} >_T \tau_1 \) 和 \( x_2 * \dot{\tau} >_T \tau_2 \)，因为否则存在唯一的\( y \) 使得对于 \( [T_0] \) 中任何 \( x >_T \sigma \)，\( x \le_T \tau * \dot{\tau} = y \)，这将意味着存在不可数多个在\( y \) 中递归的实数，这与事实矛盾。我们得出结论：\( T_1 \) 是\( A \) 的一个尖子树。

我们遵循[58]中的想法构造\( T_1 \) 的一个子树 \( T_2 \)，使得 \( T_2 \) 是一致尖的。定义一棵树序列 \( T_1 = T_1^{-1} \supseteq T_1^0 \supseteq T_1^1 \dots \)，它们在 \( T_1 \) 中是递归的，如下：

### 第 \( e \) 阶段：

情况 (I)。存在一个 \( n \) 使得对于某些 \( \sigma \in T_e^{<e-1} \)，\( \Phi_e^e(n) \downarrow T_1(n) \)。令 \( T_e^e = \{ \tau \mid \tau \in T_1^{e-1} \wedge (\tau \ge_T \sigma \lor \tau \subseteq \sigma) \} \) 并进入下一阶段。

情况 (II)。否则。

子情况 (i) \( (\forall n)(\forall \sigma \in T_e^{<e-1})(\exists \tau > \sigma)(\tau \in T_e^{<e-1} \wedge \Phi_e^\tau(n)[|\tau|]) \)。在这种情况下，定义一棵 \( T_1 \)-递归完美树 \( T_e^e \subseteq T_1^{e-1} \) 并不困难，使得对于每个 \( x \in [T_e^e] \)，都有 \( \Phi_e^x = T_1 \)。在此情况下，终止构造，因为 \( T_1^e \le_T T_1 \) 且 \( T_1^e \) 是一棵一致尖树。

子情况 (ii) 否则。那么存在 \( n_0 \) 和 \( a_0 \in T_1^{<i} \) 使得对于 \( T_1^{<i-1} \) 中每个 \( \tau \ge \sigma_0 \)，\( \Phi_e^\sigma(n)[|\tau|] \downarrow \)。令 \( T_1^i = \{ \tau \mid \tau \in T_1^{<i-1} \wedge (\tau \ge \sigma_0 \lor \tau \le \sigma) \} \)。进入下一阶段。

如果构造在任何阶段 \( e \) 都不终止，那么存在一个实数 \( x \in \cap_e [T_1^e] \)。根据序列 \( \{T_1^i\} \) 的定义，我们有 \( \Phi_e^\sigma \neq T_1 \)，这与 \( T_1 \) 是一棵尖树的事实矛盾。因此构造必须在某个阶段 \( e \) 终止，其中子情况 (i) 成立。令 \( T_2 = T_1^e \)。

### 6.6.3 练习

### 练习 6.6.1.

证明对于任何实数 \(z\)，存在一棵一致尖树 \(T \le 2^{<\omega}\) 使得 \(T \equiv_T z\)。

### 6.6.4 图灵确定性

### 定义 6.6.6.

- 图灵确定性 (TD) 陈述：任何图灵度集合要么包含一个圆锥，要么与一个圆锥不相交。
- 如果 \(\Gamma\) 是图灵度集合的一个类，那么 \(\Gamma\)-图灵确定性 陈述：\(\Gamma\) 中的每个集合要么包含一个圆锥，要么与一个圆锥不相交。

图灵确定性在描述集合论中起着重要作用，如以下未给出证明的定理所示：

### 定理 6.6.7 (Harrington [45]).

ZFC+\(\Sigma_1^1\)-确定性 是相容的，当且仅当 ZFC+\(\Sigma_1^1\)-图灵确定性 是相容的。

### 定理 6.6.8 (Woodin).

- (i) 对于任何 \(n \ge 2\)，ZFC + \(\Sigma_n^1\)-确定性 是相容的，当且仅当 ZFC + \(\Sigma_n^1\)-图灵确定性 是相容的。

- (ii) ZF + DC + AD 是相容的，当且仅当 ZF + DC + TD 是相容的。

### 6.6.5 Martin猜想

一个函数 \(F : 2^\omega \to 2^\omega\) 在一个圆锥（实数的圆锥）\(C = \{ x \mid x \ge_T z \}\) 上是度不变的，对于某些 \(z\)，如果 \(C \) 中任何 \(x, y \ge_T z\) 且具有相同的图灵度，则满足 \(F(x) \equiv_T F(y)\)。如果对于 \(x \in C\) 有 \(F(x) \ge_T x\)，则称 \(F\) 在一个圆锥上是递增的。如果 \(F\) 和 \(G\) 在一个圆锥上是度不变的，当对于所有 \(x \in C\) 有 \(F(x) \le_T G(x)\) 时，写作 \(F \le_M G\)。Martin 提出了以下猜想。

### 猜想 6.6.9.

假设 ZF + AD + DC。





- 1. 每个在锥上不递增的度不变函数在锥上是常数；
- 2. \(\le_M\) 对在锥上递增的度不变函数进行良序。而且，如果 \(F\) 的 \(\le_M\)-阶是 \(\alpha\)，则 \(F'\) 的 \(\le_M\)-阶是 \(\alpha + 1\)，其中 \(F'(x) = (F(x))'\)，即 \(F(x)\) 的图灵跳跃。

马丁猜想是递归理论中最深刻的猜想之一。基本上它说，唯一的“自然不可解问题”是停机问题。我们将在第7章中详细讨论这个话题。

## 6.6.6 练习

- 练习 6.6.2 (Blass [7])。证明对于任何超算术实数 \(x\)，存在一个 \(\Pi^0_1\)-集 \(A\)，使得 \(\Pi\) 对 \(G_A\) 有获胜策略，但没有在 \(x\) 中递归的获胜策略。

- 练习 6.6.3。假设 \(A\) 是一个 \(\Pi^1_1\)-集，使得对于任何图灵度 \(\mathbf{x}\)，\(\mathbf{x} \cap A \neq \emptyset\)。那么存在一个指示树 \(T\) 使得 \([T] \subseteq A\)。

- 练习 6.6.4 (Blass [7])。证明存在一个 \(\Pi^0_1\)-集 \(A\)，使得 \(\Pi\) 有获胜策略，但对 \(G_A\) 没有超算术获胜策略。

- 练习 6.6.5。证明存在一个图灵度 \(\mathbf{a}\) 使得
  \((\mathscr{P}(\le \mathbf{a}), \le) \equiv (\mathscr{P}(\le \mathbf{b}), \le)\)
  对于任何图灵度 \(\mathbf{b} \ge \mathbf{a}\)，其中 \(\mathscr{P}(\le \mathbf{a}) = \{ \mathbf{c} \mid \mathbf{c} \le \mathbf{a} \}\)。

- 练习 6.6.6。假设 \(\mathbf{b} \ge \mathbf{a}\)，ZF + PD。证明存在一个图灵度 \(\mathbf{a}\) 使得
  \((\mathscr{P}(\ge \mathbf{a}), \le) \equiv (\mathscr{P}(\ge \mathbf{b}), \le)\) 对于任何图灵度 \(\mathbf{b} \ge \mathbf{a}\)，其中 \(\mathscr{P}(\ge \mathbf{a}) = \{ \mathbf{c} \mid \mathbf{c} \ge \mathbf{a} \}\)。

- 练习 6.6.7 (Jockusch and Soare [59])。证明 \((\mathscr{A}, \le) \not\equiv (\mathscr{P}, \le)\)，其中 \(\mathscr{A}\) 是算术集的图灵度集合。

- 练习 6.6.8。假设 ZFC。证明存在一个函数序列 \(\{f_n\}_{n < \omega}\) 使得对所有 \(n\) 都有 \(f_{n+1} \le_M f_n\)。

- 练习 6.6.9 (Simpson [138])。假设 ZF + \(\Pi^1_1\)-确定性。证明存在一个 \(x\) 使得对于任何 \(y \ge x\)，\(y\) 的超度是最小覆盖。

- *练习 6.6.10 (Harrington and Kechris [46])。设 \(P \subseteq 2^\omega\) 是一个 \(\Pi^0_1\)-集，关于超算术集的图灵度是终沓的，即，对于任何 \(x \in \text{HYP}\) 存在 \(y \in P\) 使得 \(y \ge_T x\)。证明任何 \(x \ge_T 0\) 都与任何 \(y \in P\) 图灵等价。*

## 7 跳算子分类

图灵跳算子 \(x \mapsto x'\) 是度不变的，即，如果 \(x \equiv_T y\) 则 \(x' \equiv_T y'\)。度不变性是该算子的一个基本性质，它促使引入了马丁猜想（§ 6.6.5）。在本章中，我们讨论一个更强的性质，称为 _均匀度不变性_，并给出满足该性质的函数分类。

### 7.1 均匀度不变函数

**定义 7.1.1。**
- 如果 \(e = (e_0, e_1)\)，我们说 \(x\) 通过 \(e\) 与 \(y\) 图灵等价（\(x \equiv_T y\) via \(e\)）如果 \(x = \Phi_{e_0}^y\) 且 \(y = \Phi_{e_1}^x\)；
- 一个函数 \(F : 2^\omega \to 2^\omega\) 在以 \(z\) 为基的锥 \(C = \{x \mid x \ge_T z\}\) 上是 _均匀度不变_ 的，如果存在一个函数 \(t : \omega \to \omega\) 使得对于任何 \(x, y \ge_T z\) 且 \(x\) 通过 \(e\) 与 \(y\) 图灵等价，都有 \(F(x)\) 通过 \(t(e)\) 与 \(F(y)\) 图灵等价。

注意在上述定义中，\(t(e)\) 的值与实数 \(x, y\) 无关。

1967年，Sacks 对于 Post 问题的一般解，提出了关于存在度不变函数 \(x \mapsto W^x\) 的猜想。该猜想与马丁猜想相矛盾，因为后者断言任何这样的函数至少必须和跳算子一样强：

**猜想 7.1.2 (Sacks [119])。** _存在一个_ \(\Sigma^1_1\)_-谓词_ \(W \subseteq 2^\omega \times \omega\) _使得，如果_ \(W^x = \{n \mid W(x, n)\}\)_，则_ \(x <_T W^x < x'\) _并且对于任何_ \(y \equiv_T x\)_，_ \(W^x \equiv_T W^y\)。

1975年，Lachlan [80] 证明该猜想对均匀度不变的 \(W\) 不成立。

#### 7.1.1 非递增均匀度不变函数

均匀度不变函数在 ZF + DC + AD 下表现良好。下面的定理表明，一个均匀度不变函数要么在锥上是常数，要么在锥上是递增的。

**定理 7.1.3 (Slaman and Steel [142])。** _假设_ ZF + DC + AD_。如果 F 是均匀度不变的且在锥上不递增，则 F 在锥上是常数。_

我们将定理 7.1.3 的证明分解为一系列引理。设 \(F\) 是通过 \(\leq a\) 均匀度不变的，且在锥上不递增。

**引理 7.1.4。** _假设_ ZF+DC+AD_。如果 F 是均匀度不变的且在锥上非递增，则在锥上 \(F(x) <_T x$。_

证明。假设 \(F\) 是均匀度不变的且在锥上不递增。那么集合 \(\{x \mid F(x) \not\ge_T x\}\) 在图灵度中是终沓的。根据命题 6.6.5，存在一个指示树 \(T\) 使得 \(F\) 在 \(T\) 上通过一个函数 \(\iota : \omega \to \omega\) 均匀度不变，并且对于任何 \(x \in [T]\)，\(F(x) \not\ge_T x\)。

给定 \(x\)，令 \(x^\iota(i) = 2(x_i + 1)\) 对于 \(i < \omega\)。设 \(A \subseteq \omega^\omega\) 使得 \(x = x_0 \oplus x_1 \in A\) 当且仅当以下条件之一成立：\(x_1^\iota \not\ge_T 2^\omega$ 或
- \(x_0^\iota \in 2^\omega\)；
- 对某些 \(e, n < \omega\)，\(x_0(i) = \langle e, n \rangle\)；
- 要么 \(x_0 \not\le_T x_1$ 或 \(F(x_0^\iota)(n) = 0 \leftrightarrow x_1(x_1(0)) \neq 0$，并且
- \(x_0^\iota \in [T] \wedge \Phi_e^{x_0^\iota} = x_1$。

考虑由 I 和 II 进行的双人博弈 \(\mathcal{G}_A$，两者像往常一样交替选择数字。根据 AD，I 或 II 对 \(\mathcal{G}_A$ 拥有获胜策略。假设 I 拥有一个获胜策略 \(\delta$。我们将证明在 \(T \oplus \delta$ 之上的锥上 \(x \le_T F(x)$，这将导致矛盾。

令 \(z_0 \ge_T T \oplus \delta$ 且对于 \(m < \omega\)，\(x_1^m = m \frown z_0$。令 \(x_0^m$ 为 I 在 \([T]$ 中作为对 II 下 \(x_1^m$ 的回应而下出的实数，即 \(\delta(x_1^m) = \langle e_0, n_0 \rangle \frown x_0^m$，其中 \(\langle e_0, n_0 \rangle$ 编码了数对 \(e_0, n_0$，且 \(\delta(0) = \langle e_0, n_0 \rangle$ 是 \(\delta$ 规定的第一步。由于 I 获胜，对每个 \(m\) 都有 \(x^m = x_0^m \oplus x_1^m \in A$。因为 \(x_1^m \ge_T \delta$，所以 \(x_1^m \ge_T x_0^m$。于是对每个 \(m\)，
\(F(x_0^m)^+(n_0) = 0 \leftrightarrow x_1^m(m) = 1.\)

由于 \(\Phi_{e_0}^{(x_0^m)^+} = x_1^m$ 且 \(x_1^m = m \frown z_0$，存在一个 \(i$ 使得对每个 \(m\) 都有 \(\Phi_i^{(x_0^m)^+} = (x_0^{m+1})^+$。类似地，存在一个 \(j$ 使得对每个 \(m\) 都有 \(\Phi_j^{(x_0^m)^+} = (x_0^m)^+$。因此 \((x_0^m)^+ \equiv_T (x_0^{m+1})^+$ 通过 \(\langle i, j \rangle$，于是 \(F((x_0^m)^+) \equiv_T F((x_0^{m+1})^+)$ 通过 \(t(i, j) = \langle i', j' \rangle$。由于 \(F$ 是度不变的且 \(z_0 \equiv_T x_0^m \equiv_T (x_0^m)^+$，存在某个 \(k$ 使得 \(\Phi_k^{(x_0^m)} = F((x_0^m)^+)$。令 \(l_m = F((x_0^m)^+)(n_0)$。注意 \(F((x_0^m)^+) = \Phi_k^{F(z_0)}$ 且 \(F((x_0^{m+1})^+) = \Phi_k^{F((x_0^m)^+)}$。所以 \(\{l_m\}_{m \in \omega}$ 是 \(F(z_0)$-递归的。注意 \(z_0(m) = x_1^{m+1}(m+1) = 1 - l_{m+1}$。因此 \(z_0 \le_T F(z_0)$，矛盾。

因此 II 拥有一个获胜策略 \(\tilde{\tau}$。我们将证明在 \(T \oplus \tilde{\tau}$ 之上的锥上 \(F(x) <_T x$。固定一个实数 \(x_0 \in [T]$ 使得 \(x_0 \ge_T T \oplus \tilde{\tau}$。根据相对于 \(x_0$ 的递归定理，存在一个 \(e_0$ 使得对每个 \(n, m$ 都有 \(\tilde{\tau}((e_0, n)^\frown x_0)(m) = \Phi_{e_0}^{e_0}(\langle n, m \rangle)$。对每个 \(n$，令 \(x_1^n = \tilde{\tau}((e_0, n)^\frown x_0)$。由于 II 获胜，必有 \(x_0 \le_T x_1^n$ 且 \(F(x_0^n)(n) = x_1^n(x_1^n(0))$。于是
\(F(x_0^n)(n) = x_1^n(x_1^n(0)) = \Phi_{e_0}^{e_0}(\langle n, x_0^n(e_0(n, 0)) \rangle)\)
因此 \(F(x_0) \le_T x_0$。由于 \(F$ 是度不变的，我们得出在锥上 \(F(x) <_T x$。

根据引理 7.1.4，固定一个 \(x_0$ 使得在锥 \(\{x \mid x \ge_T x_0\}\) 上 \(F(x) <_T x$。那么存在一个 \(e_0$ 使得集合 \(C = \{x \mid \Phi_{e_0}^x = F(x) \wedge x \ge_T x_0\}\) 是终沓的。根据命题 6.6.5，存在一个完美树 \(T_0$ 和一个数 \(i$ 使得 \([T_0] \subseteq C$ 并且对于每个 \(x \in [T_0]$ 都有 \(T_0 = \Phi_i^x$。





引理 7.1.5. 存在一棵完美树 \( T_1 \subseteq T_0 \)，使得 \( T_1 \le_T T_0 \) 且 \( F \) 在 \( [T_1] \) 上要么是单射，要么是常数。

证明. 如果存在 \( \sigma \in T_0 \) 使得对所有 \( x, y \in [T_0] \cap [\sigma] \) 都有 \( \Phi^\sigma_{e_0}(x) = \Phi^\sigma_{e_0}(y) \)，则令 \( T_1 = T_0 \cap \{ \tau \in 2^{<\omega} \mid \tau \supset \sigma \} \)。显然 \( F \) 在 \( [T_1] \) 上是常数。否则，\( T_0 \)-递归地找到一棵完美子树 \( T_1 \subseteq T_0 \)，使得 \( F \) 在 \( [T_1] \) 上是单射。\(\square\)

根据引理 7.1.5，我们可以假设 \( F \) 在 \( T_0 \) 上是单射。令

```
\( S_0 = \{ \tau \in 2^{<\omega} \mid (\exists \sigma \in T_0)(\forall n \le |\tau|)(\tau(n) = \Phi^\sigma_{e_0}(n)) \} \)。
```

那么 \( S_0 \) 是一棵 \( T_0 \)-递归的完美树，使得 \( \Phi_{e_0} \) 是从 \( [T_0] \) 到 \( [S_0] \) 的同胚映射。

由于 \( T_0 \) 是完美的，令 \( p : 2^{<\omega} \to T_0 \) 为一个保序的、\( T_0 \)-递归的双射。那么 \( p \) 可视为从 \( 2^\omega \) 到 \( [T_0] \) 的同胚映射。令 \( \pi : 2^{<\omega} \to 2^{<\omega} \) 为一个递归函数，使得对任意 \( \sigma \) 和 \( i < 2 \)，若 \( \sigma^\frown i \neq \emptyset \) 且存在某个 \( j < |\sigma| \) 使得 \( \sigma(j) = 1 \)，则 \( p(\sigma^\frown i) = p(\sigma)^\frown i \)；否则 \( \pi(\sigma^\frown i) = \sigma^\frown (1-i) \)。通过令 \( \pi(\alpha) = (\bigcup_n \pi(\alpha \upharpoonright n)) \)，\( \pi \) 可视为从 \( 2^\omega \) 到 \( 2^\omega \) 的同胚映射。令

```
\( p_0 = p \circ \pi \circ p^{-1} \)。
```

那么 \( p_0 \) 是从 \( T_0 \) 到 \( T_0 \) 的同胚映射。我们将验证以下引理留给读者。

引理 7.1.6. 对任意 \( \sigma \)，\( \{\pi^{(n)}(\alpha)\}_{n \in 2^{<\omega}} \) 是 \( 2^{|\sigma|} \) 的一个排列。

令 \( p_1 = F \circ p_0 \circ F^{-1} \) 为从 \( [S_0] \) 到 \( [S_0] \) 的同胚映射，并固定一个 \( x_0 \in [T_0] \)。由于 \( T_0 \) 是一致指示的，存在一对 \( (i_0, j_0) \) 使得对任意 \( n \)，\( p_1^{(n)}(x_0) \equiv p_1^{(n+1)}(x_0) \) 通过 \( (i_0, j_0) \)。那么 \( F(p_0^{(n)}(x_0)) \equiv F(p_0^{(n+1)}(x_0)) \) 通过 \( (i_1, j_1) = \ell((i_0, j_0)) \)。注意对任意 \( n \)，\( F(p_0^{(n)}(x_0)) = p_1^{(n)}(F(x_0)) \)。因此实数 \( \Phi_{e_0}^{p}(p_1^{(n)}(F(x_0))) \) 在 \( p_1^{(n)}(x_0) = F(x_0) \) 中是递归的。

给定一棵完美树 \( T \) 和一个数 \( n \)，我们说一棵有限树 \( S \subseteq T \) 对 \( T \) 的 \( 2^n \) 副本进行编码，如果

- \( S \) 同构于 \( 2^n \);
- 对任意 \( \tau \in T \setminus S \)，存在一个终端节点 \( \sigma \in S \) 使得 \( \tau \supset \sigma \)。

引理 7.1.7. \( S_0 \) 在 \( F(x_0) \) 中是递归的。

证明. 注意我们可以将 \( F : [T_0] \to [S_0] \) 视为一个同胚映射。因此对任意 \( \sigma \)，存在一个 \( m \) 使得 \( p^{-1}(F^{-1}((F(x_0) \upharpoonright m))) \) 的长度为 \( 2^{|\sigma|} \)。根据引理 7.1.6，\( \{\pi^{(n)}(p^{-1}(F^{-1}((F(x_0) \upharpoonright m))))\}_{n \in 2^{<\omega}} \) 是 \( 2^{|\sigma|} \) 的一个排列。由于 \( F \) 和 \( p \) 都是同胚映射，有限树

```
\( S_0^{[\sigma]} = \{ \tau \mid (\exists n < 2^{|\sigma|})(\tau \le p_1^{(n)}(F(x_0) \upharpoonright m)) \} \)。
```

对 \( S_0 \) 的 \( 2^{|\sigma|} \) 副本进行编码。

因此 \( \sigma \in S_0 \) 当且仅当 \( \sigma \in S_0^{[\sigma]} \)。显然 \( S_0^{[\sigma]} \) 可以从 \( \{p_1^{(n)}(F(x_0))\}_{n \in 2^{<\omega}} \) 中有效计算得到。故 \( S_0 \le_T F(x_0) \)。\(\square\)

这表明 \( S_0 \) 是一棵指示树。那么存在一个 \( x_1 \in [S_0] \) 使得 \( T_0 \oplus S_0 \le_T x_1 \)。由于 \( \Phi_{e_0} \) 是从 \( T_0 \) 到 \( S_0 \) 的同胚映射，不难看出唯一的实数 \( y \in [T_0] \) 使得 \( \Phi_{e_0}^y = x_1 \) 在 \( x_1 \) 中是递归的。换句话说，\( F(y) = x_1 \ge_T y \)，这产生了一个矛盾。

#### 7.1.2 练习

练习 7.1.1. 证明引理 7.1.6。

### 7.2 一致度不变函数上的马丁猜想

本节讨论的结果归功于 Steel [159]。

引理 7.2.1. 假设 ZF + AD + DC。那么 \( \le_M \) 是在一致度不变且递增的函数集合上的一个线性序。

证明. 假设 \( F \) 和 \( G \) 是通过 \( t \) 在锥 \( \{x \mid x \ge_T z_0\} \) 上的一致度不变递增函数。定义集合 \( A \subseteq \omega^\omega \)，使得 \( x_0 \oplus x_1 \in A \) 当且仅当要么 \( x_1^i \notin 2^\omega \)，要么

- \( x_0^i \in 2^\omega \);
- \( \Phi_{e_0}^{x_0^i} = x_1^i\)，其中 \( x_0(0) = \langle e_0, n_0 \rangle\)，且
- 要么 \( \Phi_{e_1}^{x_1^i} \notin x_0^i \)，要么 \( n_0 \in F(x_0^i) \leftrightarrow n_1 \notin G(x_1^i) \)，其中 \( x_1(0) = \langle e_1, n_1 \rangle\)。

考虑由 I 和 II 在 \( A \) 上进行的两人博弈 \( \mathcal{G}_A \)，I 的第一步走 \( \langle e_0, n_0 \rangle \)。假设 I 对 \( \mathcal{G}_A \) 有一个获胜策略 \( \hat{\sigma} \)。固定一个实数 \( y \ge_T \hat{\sigma} \oplus z_0 \oplus t \)。根据相对于 \( y \) 的递归定理，对任意数 \( m \)，存在一个 \( e_1^m \) 使得 \( \Phi_{e_1^m} = (\delta(\overline{x_1^m})) \)，其中 \( x_1^m = (\langle e_1^m, m \rangle)^\frown y \)。注意函数 \( m \mapsto e_1^m \) 是递归的。令 \( x_0^m = \delta(\overline{x_1^m}) \) 和 \( x_0^m(0) = \langle e_0^m, n_0^m \rangle \)。注意函数 \( m \mapsto \langle e_0^m, n_0^m \rangle \) 是 \( y \)-递归的（实际上是一个常函数）。由于 \( \hat{\sigma} \) 是 I 的获胜策略，\( \Phi_{e_0^m}^{x_0^m} = y \) 且

\( n_0^m \in F(x_0^m) \leftrightarrow m \notin G(x_1^m) = G(y) \)。

注意 \( x_1^m \equiv_T y \) 通过 \( \langle e_0^m, e_1^m \rangle \)，因此我们有 \( F(x_0^m) \equiv_T F(y) \) 通过 \( \langle e_0^m, e_1^m \rangle = (i_0^m, i_1^m) \)。由于 \( F(y) \ge_T y \)，\( t \le_T y \) 且 \( m \mapsto \langle e_0^m, e_1^m \rangle \) 是 \( y \)-递归的，函数 \( m \mapsto (i_0^m, i_1^m) \) 是 \( F(y) \)-递归的。那么对任意 \( m \)，我们可以 \( F(y) \)-递归地找到 \( n_0^m \) 和 \( i_1^m \) 使得 \( \Phi_{i_1^m}^{F(y)}(n_0^m) = F(x_0^m)(n_0^m) = 1 - G(y)(m) \)。故 \( G(y) \le_T F(y) \)，从而 \( G \le_M F \)。

如果 II 有一个获胜策略，则通过类似的论证可以证明 \( F \le_M G \)。

给定 \( x \) 和 \( y \)，我们说 \( x \equiv_M y \) 通过 \( (e_0, e_1) \)，如果存在两个递归函数 \( \Phi_{e_0} \) 和 \( \Phi_{e_1} \) 使得对任意 \( n \)，

- \( n \in y \Leftrightarrow \Phi_{e_0}(n) \downarrow \in x \); 且
- \( n \in x \Leftrightarrow \Phi_{e_1}(n) \downarrow \in y \)。

引理 7.2.2. 假设 ZF+AD+DC。如果 \( F \) 和 \( G \) 是通过 \( t \) 的一致度不变递增函数且 \( F <_M G \)，那么 \( F' \le_M G \)。

证明. 假设 \( F <_M G \) 在锥 \([x \mid x \ge_T z_0]\) 上，但 \( F' \not\le_M G \)。令 \( p : 2^{<\omega} \to \omega \) 为一个递归双射，并对任意 \( x \)，令 \( G_1(x) = y \)，其中

\( y = \{n \mid (\forall m)(p(G(x) \mid m) \neq n)\} \)。

那么对每个 \( x \)，\( G_1(x) \equiv_T G(x) \)。而且，由于 \( G \) 是一致度不变的，\( G_1 \) 也是。

我们应用与引理 7.2.1 中相同的方法。定义 \( A \subseteq \omega^\omega \)，使得 \( x_0 \oplus x_1 \in A \) 当且仅当要么 \( x_1^t \notin 2^\omega \)，要么

- \( x_0^t \in 2^\omega \);
- \( \Phi_{e_1}^{x_0^t} = x_1^t \)，其中 \( x_0(0) = \langle e_0, n_0 \rangle\)，且
- 要么 \( \Phi_{e_1}^{x_1^t} \neq x_0^t \)，要么 \( n_0 \in F'(x_0^t) \Leftrightarrow n_1 \notin G_1(x_1^t) \)，其中 \( x_1(0) = \langle e_1, n_1 \rangle\)。

两名玩家 I 和 II 进行博弈 \( \mathcal{G}_A \)。如同在引理 7.2.1 中，如果 II 对 \( \mathcal{G}_A \) 有一个获胜策略，那么 \( F' \le_M G_1 \)，这与假设矛盾。

因此 I 对 \( \mathcal{G}_A \) 有一个获胜策略 \( \vartheta \)。固定 \( y \ge_T \vartheta \oplus z_0 \oplus t \)。根据相对于 \( y \) 的递归定理，对每个 \( m \) 存在一个 \( e_1^m \) 使得 \( \Phi_{e_1^m} = (\delta(x_1^m))' \)，其中 \( x_1^m = (e_1^m, m)^\frown y \)。注意函数 \( m \mapsto e_1^m \) 是递归的。令 \( x_0^m = \delta(x_1^m) \) 和 \( x_0^m(0) = \langle e_0^m, n_0^m \rangle \)。函数 \( m \mapsto (e_0^m, n_0^m) \) 是 \( y \)-递归的。由于 \( \vartheta \) 是 I 的获胜策略，\( \Phi_{e_0^m}^{x_1^m} = y \) 且

\( n_0^m \in F'(x_0^m) \Leftrightarrow m \notin G_1(x_1^m) = G_1(y) \)。

注意 \( x_0^m \equiv_T y \) 通过 \( (e_0^m, e_1^m) \)。那么我们有 \( F(x_0^m) \equiv_T F(y) \) 通过 \( t(e_0^m, e_1^m) = (i_0^m, i_1^m) \)。由于 \( t \le_T y \) 且 \( m \mapsto (e_0^m, e_1^m) \) 是 \( y \)-递归的，函数 \( m \mapsto (i_0^m, i_1^m) \) 也是 \( y \)-递归的。因此存在一个 \( y \)-递归函数 \( m \mapsto (j_0^m, j_1^m) \) 使得 \( F'(x_0^m) \equiv_T F(y) \) 通过 \( (j_0^m, j_1^m) \)。于是对任意 \( m \)，可以 \( y \)-递归地找到 \( x_0^m \) 和一个 \( j_1^m \) 使得

\( F'(y)(\Phi_{j_1^m}(n_0^m)) = F'(x_0^m)(n_0^m) = 1 - G_1(y)(m) \)。

由于 \( F(y) \ge_T y \)，集合 \( E_1 = \{m \mid F'(y)(\Phi_{j_1^m}(n_0^m)) = 1\} \) 是无限的且是 \( F(y) \)-可枚举的。令 \( E_2 \subseteq E_1 \) 为无限的 \( F(y) \)-递归集合。那么对任意 \( m \in E_2 \)，存在一个 \( n_m \) 使得 \( p^{-1}(m) = G_1(y) \downarrow n_m \)。故 \( G(y) \le_T F(y) \)，从而 \( G \le_M F \)，这与假设矛盾。

我们得出结论 \( F' \le_M G \)。





现在假设存在一个 \(\le_M\)-序列 \(\langle F_n \rangle_{n<\omega}\)，使得对每个 \(n\)，(a) \(F_n\) 通过 \(t_n\) 是一致度不变的，且 (b) \(F_{n+1} \le_M F_n\) 在锥 \(\{x \mid x \ge_T z_n\}\) 上。

令 \(z = \Phi_{n<\omega} z_n\) 且 \(\langle t_n, e_0, e_1 \rangle = t_\infty(e_0, e_1)\)。对每个 \(n\)，我们为对 \((F_{n+1}, F_n)\) 定义集合 \(A_n\) 和 \(B_n\)，分别为 Lemma 7.2.1 和 Lemma 7.2.2 中对应的集合 \(A\)。然后对每个 \(n\)，I 对 \(G_n\) 具有获胜策略 \(\delta_n\)，其中 \(y = z \oplus t \oplus (\Phi_{n<\omega} \delta_n) \oplus (\Phi_{n<\omega} \bar{\delta}_n)\)。然后如同在 Lemma 7.2.1 的证明中一样，存在一个 y-算术关系 \(P(x_0, x_1)\)，使得对任意 \(n\)，\(F_{n+1}(y)\) 是使得 \(P(x, F_n(y))\) 成立的唯一实数 \(x\)。注意，由 Lemma 7.2.2，对每个 \(n\)，\(F_{n+1}(y) \le_T F_n(y)\)。

### 提议 7.2.3 (Steel [157])

令 \(R \subseteq 2^\omega \times 2^\omega\) 为一个算术关系。如果 \(\langle x_n \rangle_{n<\omega}\) 是一串实数，使得 \(x_{n+1}\) 是满足 \(R(y, x_n)\) 的唯一 \(y\)，则存在某个 \(n\)，使得 \(x'_{n+1} \le_T x_n\)。

证明。假设为了矛盾，对每个 \(n\) 都有 \(x'_{n+1} \le_T x_n\)。定义

\(P(x, i, j) \Leftrightarrow (\exists k > j + 1)(\exists \sigma \in \omega^{<\omega})(|\sigma| = j + 1 \wedge \Phi_e^{(x)}(i) = x \wedge (\forall k' < k)R(\Phi_{\sigma(k')}^{\sigma(k+1)}, \Phi_{\sigma(k)}^{\sigma(k)}) \wedge (\exists e)(\Phi_e^x(i) = 0 \wedge \Phi_e^x = (\Phi_{\sigma(k)}^{\sigma(j+1)})).\)

根据对序列 \(\langle x_n \rangle_{n<\omega}\) 的假设，对任意 \(n\) 我们有

\((\forall i)(\forall j)(P(x_n, i, j) \Leftrightarrow (\exists k > j + 1)(i \notin (x_{n+k})^{(j+1)})).\)

由于 \(P\) 是算术的，存在 \(m\) 和 \(e\) 使得

\(P(x, i, j) \Leftrightarrow \Phi_e^{(m)}(i, j) = 1.\)

那么对任意 \(n, i, j\)，

\(\Phi_e^{(x_n)}(i, j) = 1 \Leftrightarrow (\exists k > j + 1)(i \notin (x_{n+k})^{(j+1)}).\)

令 \(j = m\)，存在一个 \(e_0\) 使得对每个 \(i\)，

\(\Phi_{e_0}^{(x_n)}(i) = 1 \Leftrightarrow \Phi_e^{(x_n)}(i, m) = 1 \Leftrightarrow (\exists k > m + 1)(i \notin (x_{n+k})^{(m+1)}).\)

当 \(i = e_0\) 时，对任意 \(n\) 我们有

\(e_0 \in (x_n)^{(m+1)} \Leftrightarrow (\exists k > m + 1)(e_0 \notin (x_{n+k})^{(m+1)}).\)

因此 \(e_0 \in (x_0)^{(m+1)}\) 当且仅当 \((\exists k > m + 1)(e_0 \notin (x_k)^{(m+1)})\)，且 \(e_0 \in (x_{k_0})^{(m+1)}\) 当且仅当 \((\exists k > m + 1)(e_0 \notin (x_{k_0+k})^{(m+1)})\)。于是 \(e_0 \in (x_0)^{(m+1)}\) 当且仅当 \(e_0 \in (x_{k_0+k})^{(m+1)}\)。再次由上述等价式，\(e_0 \in (x_0)^{(m+1)}\) 当且仅当 \(e_0 \notin (x_0)^{(m+1)}\)，这产生了矛盾。

将提议 7.2.3 相对化到 \(y\)，存在一个 \(n\) 使得 \(F_{n+1}(y)' \not\le_T F_n(y)\)，这与我们对序列 \(\langle F_n \rangle_{n<\omega}\) 的假设以及 Lemma 7.2.2 相矛盾。因此我们有：

### 引理 7.2.4

假设 ZF + AD + DC，在一致度不变函数上的偏序 \(\le_M\) 是良序。

综上所述，我们有以下定理。

### 定理 7.2.5 (Steel [159], Slaman and Steel [142])

假设 ZF + AD + DC，马丁猜想（6.6.9）对一致度不变函数成立。

### 注释 7.2.6

H. Friedman [30] 证明存在一个超算术谓词 R 和一串 \(\{x_n\}_{n<\omega}\)，使得 \(x'_{n+1} \le_T x_n\) 且 \(x_{n+1}\) 是满足 \(R(y, x_n)\) 的唯一 y。

#### 7.2.1 练习

- 练习 7.2.1. 证明存在一个算术谓词 P，使得对任意 n > 0，存在一串 \(\{x_i\}_{i \le n}\) 满足：(i) 对任意 i < n，\(x'_{i+1} \le_T x_i\)，(ii) \(P(x_{i+1}, x_i)\) 且 (iii) 若 \(P(x, y)\) 则 \(y = x_{i+1}\)。

- 练习 7.2.2. 证明存在一个算术谓词 R 和一个 \(<_h\)-降序列 \(\{x_n\}_{n<\omega}\)，使得对任意 n，\(x_{n+1}\) 是满足 \(R(y, x_n)\) 的唯一实数 y。

## 7.3 Posner–Robinson 定理

### 7.3.1 原始 Posner–Robinson 定理

### 定理 7.3.1 (Posner and Robinson [114])

对任意非递归 \(x \le_T 0'\)，存在一个 g 使得 \(x \oplus g \equiv_T g' \equiv_T 0'\)。

因此给定一个非递归的 \(\Delta^0_2\)-实数 x，定理 7.3.1 说明存在一个相对于它 x 是其图灵跳的 g。

证明。为了证明这一点，我们使用 Jockusch 和 Shore [57] 的方法。固定 \(x >_T 0\) 为 \(\Delta^0_2\)。我们可以假设 x 不是递归可枚举的。对每个 e，考虑以下陈述：

\((\forall \alpha \in 2^\omega)(\exists n)(n \in x \wedge (\forall \tau \supseteq \sigma \supseteq 0^n1)(\Phi_e^\tau(e)[s] \uparrow) \vee (n \notin x \wedge (\exists \tau \supseteq \sigma \supseteq 0^n1)(\Phi_e^\tau(e)[s] \downarrow)).\)

由于 x 不是递归可枚举的，\((\sharp_e)\) 对每个 e 都成立。我们通过归纳构造 g。

步骤 0：定义 \(g_0 = \emptyset\)。

步骤 s + 1：

- 子步骤 1. 定义 \(g(s, 1) = g_s^\frown 0'(s)\)。

- 子步骤 2. 找到最小的 n，使得以下之一成立

  \((n \in x \wedge \forall \tau \supseteq g(s, 1)^\frown 0^n 1)(\Phi_s^\tau(s)[s] \uparrow)\)

  或

  \((n \notin x \wedge (\exists \tau \supseteq g(s, 1)^\frown 0^n 1)(\Phi_s^\tau(s)[s] \downarrow)).\)

由 \((t_s)\)，这样的 n 存在。在第一种情况下，定义 \(g_{s+1} = g(s, 1) \ulcorner 0^s 1 \urcorner\)。在第二种情况下，选择字典序最小的 \(\tau\) 使得 \(\tau \supseteq g(s, 1) \ulcorner 0^s 1 \urcorner (\Phi_s^\tau(s)[|\tau|] \downarrow)\)。定义 \(g_{s+1} = \tau \ulcorner 1 \urcorner\)。

令 \(g = \bigcup_{s < \omega} g_s\)。注意该构造是一致 \(x \oplus \emptyset'\)-递归的。因此 \(\emptyset' \geqslant_T x \oplus \emptyset'\)。我们将证明 \(0'(s)\) 和 \(g_s\) 是一致 \(g \oplus x\)-递归的。假设我们已计算出 \(g_s\) 和 \(0'(s)\)。那么 \(0'(s + 1) = g(|g_s| + 1)\)。要计算 \(g_{s+1}\)，搜索唯一的 n 使得 \((g \upharpoonright |g_s| + 1) \ulcorner 0^s 1 \urcorner < g\)。根据构造，以下之一成立

- (1) \(n < s\) 或
- (2) \(n \notin x\) 且存在一个 \(\tau \supseteq (g \upharpoonright |g_s| + 1) \ulcorner 0^s 1 \urcorner\) 使得 \(\tau < g\) 且 \(\Phi_s^\tau(s)[|\tau|] \downarrow\)。

若 (1) 成立，则 \(g(s+1) = \langle g \upharpoonright |g_s| + 1 \rangle \ulcorner 0^s 1 \urcorner\)。若 (2) 成立，则存在唯一的 \(\tau \supseteq (g \upharpoonright |g_s| + 1) \ulcorner 0^s 1 \urcorner\) 使得 \(\tau < g\) 且 \(\Phi_s^\tau(s)[|\tau|] \downarrow\)。由此 \(g_{s+1} = \tau\)。因此 \(\emptyset' \geqslant_T g \oplus x\)。

要证明 \(g' \leq_T g \oplus \emptyset'\)，观察到对每个 e 存在一个 n 使得以下之一成立：\(\Phi_e^{g \oplus \emptyset'}(e) \downarrow\) 或对任意 \(\tau > g \upharpoonright n\) 有 \(\Phi_e^\tau(e) \downarrow\)。利用这一点，可以立即验证 \(g' \leq_T g \oplus \emptyset'\)。\(\square\)

#### 7.3.2 一个超限 Posner-Robinson 定理

定理 7.3.1 可以以多种不同的方式迭代到超限。以下是第一个版本。

### 定理 7.3.2 (Slaman and Steel [142])

令 \(0 < b < \omega_1^{CK}\) 且令 z 为一个实数，使得对每个 \(y < b\) 都有 \(0^{(y)} <_T z\)。则存在一个 g 使得 \(g \oplus z \equiv_T g^{(b)}\)。

本节其余部分专门用于证明定理 7.3.2。

令 \(a \in \mathcal{O}\)。第一步是引入一个由 \(|a|\) 索引的算术谓词枚举。由定理 1.3.4，集合 \(\{b \mid b <_O a\}\) 是递归可枚举的。应用递归定理，我们可以假设存在一个部分递归函数 \(\Phi : a^2 \to \omega\) 使得对每个 \(b <_O a\)，\(\{\Phi(b, i)\}_{i < \omega}\) 是 "\(\Sigma_b^0\)-谓词" 的 Gödel 数集合的一个枚举。为了简化记号，我们将谓词与其 Gödel 数识别。

我们通过归纳引入 \(\Sigma_b^0\) 谓词的一个枚举。\(\Sigma_1^0\)-谓词的枚举是标准的。如果 \(b = 2^e \in \mathcal{O}\) 且 \(b <_O a\)，则谓词 \(P(x, n)\) 是第 \(i\) 个 \(\Sigma_b^0\)-谓词，或 \(P(x, n) = P_{\Phi(b, i)}(x, n)\)，如果 \(P(x, n) \leftrightarrow (\exists m)\neg Q(x, n, m)\)，其中 \(Q(x, n, m)\) 是第 \(i\) 个 \(\Sigma_b^0\)-谓词。

如果 \(b = 3 \cdot 5^e \in \mathcal{O}\) 且 \(b <_O a\)，则谓词 \(P(x, n)\) 是第 \(i\) 个 \(\Sigma_b^0\)-谓词，或 \(P(x, n) = P_{\Phi(b, i)}(x, n)\)，如果 \(P(x, n) \leftrightarrow P_{\Phi(i, \Phi(b, n))}(x, n)\)，其中 \(P(i, \Phi(b, n)) = (i_0(n), i_1(n))\) 使得对每个 n 都有 \(i_0(n) <_O b\)。下一个引理通过对 b 的记号进行归纳证明，留给读者。

### 引理 7.3.3

存在递归函数 \(f : \omega \to \omega\) 和 \(g : \omega \to \omega^2\) 使得对任意 \(b <_O a\)，

- (i) 若 \(b = 1\) 或 \(2^e\)，则 \(P_{\Phi(b, f(b))} \equiv_T H_{f(b)}^2\) 通过 \(g(b)\)；
- (ii) 若 \(b = 3 \cdot 5^e <_O a\)，则 \(P_{\Phi(b, f(b))} \equiv_T H_{f(b)}^2\) 通过 \(g(b)\)。





我们现在定义在 $\Sigma^0_b$-谓词上的 Cohen forcing 概念，其中 $b <_0 a$。如果 $P(x, n)$ 是一个 $\Sigma^0_1$-谓词，那么存在一个部分递归函数 $\Phi^b(n)$，使得 $P(x, n) \Leftrightarrow \Phi^b(n) \downarrow$。定义 $\sigma \Vdash P(x, n)$ 当且仅当 $\Phi^b(n) \downarrow$。

如果 $b = 2^c \in O$，且 $b <_0 a$，并且 $P(x, n)$ 是 $\Sigma^0_b$，那么 $P(x, n) \Leftrightarrow (\exists m)\neg Q(x, \langle n, m \rangle)$。定义 $\sigma \Vdash P(x, n) \Leftrightarrow (\exists m)(\forall \tau \sqsupset \sigma)(Q(x, \langle n, m \rangle))$。

如果 $b = 3 \cdot 5^e \in O$，且 $b <_0 a$，并且 $P(x, n)$ 是一个 $\Sigma^0_b$ 谓词，那么 $P(x, n) \Leftrightarrow P_{\Phi^b(\Phi(e)(n))}(x, n)$ 对某个 $i$ 成立。定义 $\sigma \Vdash P(x, n) \Leftrightarrow \sigma \Vdash P_{\Phi^b(\Phi(e)(n))}(x, n)$。

给定 $b <_0 a$，如果 $P(x, n)$ 是一个 $\Sigma^0_b$ 谓词，那么 $\sigma \Vdash \neg P(x, n) \Leftrightarrow (\forall \tau \sqsupset \sigma)(\tau \nVdash P(x, n))$。

下面引理的验证也留给读者。

#### 引理 7.3.4. 存在一个部分递归函数 $h : a^2 \times 2 \to \omega$，使得对于任何 $b <_0 a$，

- (i) 如果 $b = 1$ 或 $2^c$，那么 $(\forall n)(\forall m)((\sigma \Vdash P_{\Phi(b,n)}(x, m) \implies \Phi^h_{\langle b,n \rangle}(\sigma, m) = 1) \wedge (\sigma \nVdash P_{\Phi(b,n)}(x, m) \implies \Phi^h_{\langle b,n \rangle}(\sigma, m) = 0))$；
- (ii) 如果 $b = 3 \cdot 5^e$，那么 $(\forall n)(\forall m)((\sigma \Vdash P_{\Phi(b,n)}(x, m) \implies \Phi^h_{\langle b,n \rangle}(\sigma, m) = 1) \wedge (\sigma \nVdash P_{\Phi(b,n)}(x, m) \implies \Phi^h_{\langle b,n \rangle}(\sigma, m) = 0))$。

一个实数 $g$ 是 $a$-泛的，如果对于任何 $b <_0 a$ 和 $\Sigma^0_b$-谓词 $P(x, n)$，存在一个 $m$ 使得要么 $g \mid m \Vdash P(x, n)$，要么 $g \mid m \Vdash \neg P(x, n)$。这得出了以下真理引理：

#### 引理 7.3.5. 假设 $g$ 是 $a$-泛的。对于任何 $m$、$n$ 和 $b <_0 a$，$P_{\Phi(b,n)}(g, m)$ 当且仅当存在一个 $k$ 使得 $g \mid k \Vdash P_{\Phi(b,n)}(x, m)$，且 $\neg P_{\Phi(b,n)}(g, m)$ 当且仅当存在一个 $k$ 使得 $g \mid k \Vdash \neg P_{\Phi(b,n)}(x, m)$。

#### 引理 7.3.6. 如果 $g$ 是 $a$-泛的，那么存在一个部分递归函数 $r$，使得对于任何 $b <_0 a$

- 如果 $b = 1$ 或 $2^c$，那么 $H^g_b = \Phi^{g_{H(b)}}_{r(b)}$；
- 如果 $b = 3 \cdot 5^e$，那么 $H^g_b = \Phi^{g_{H(b)}}_{r(b)}$。

**证明。** 我们给出 $b$ 的记号为后继的情况的证明，并将极限情况留给读者。

如果 $b = 1$，那么根据引理 7.3.3，$n \in H^g_b$ 当且仅当 $P_{\Phi(1,n)}(g, n)$。根据引理 7.3.5，存在一个 $k$ 使得要么 $g \mid k \Vdash P_{\Phi(1,n)}(g, n)$，要么 $g \mid k \Vdash \neg P_{\Phi(1,n)}(g, n)$。根据引理 7.3.4，这可以由 $\Phi^{H_g}_{\langle 1,n \rangle}(g \mid k, n)$ 判定。因此 $H^g_1 = \Phi^{g_{H(1)}}_{r(1)}$ 对某个 $i$ 成立。令 $r(1) = i$。

如果 $b = 2^c$，那么根据引理 7.3.3，$n \in H^g_b$ 当且仅当 $P_{\Phi(b,n)}(g, n)$。根据引理 7.3.5，存在一个 $k$ 使得要么 $g \mid k \Vdash P_{\Phi(b,n)}(g, n)$，要么 $g \mid k \Vdash \neg P_{\Phi(b,n)}(g, n)$。由于 $P_{\Phi(b,n)}(g, n) \Leftrightarrow (\exists m)P_{\Phi(c,n)}(g, n, m)$，我们有

$(\exists m)(g \mid k \Vdash P_{\Phi(c,n)}(g, n, m)) \vee (\forall \tau \sqsupset g \mid k)(\forall m)(\tau \nVdash P_{\Phi(c,n)}(g, n, m))$。

根据引理 7.3.4，这可以由 $g \mid H^g_c = g \mid H_{2^c} (= c 2^d$ 对某个 $d)$ 或 $g \mid H^g_c \le_T g \mid H_{2^c} (= c \cdot 3 \cdot 5^e$ 对某个 $e)$ 判定。因此 $H^g_b = \Phi^{g_{H(b)}}_{r(b)}$ 对某个 $i$ 成立，该数可以从 $b$ 有效计算得出。令 $r(b) = i$。

我们现在准备证明定理 7.3.2。我们建立 $\beta$ 为后继序数的情况，并将极限情况留给读者。

令 $a \in \omega$ 使得 $a = \beta$。对所有 $b <_0 a$ 固定 $z > \tau_H$。我们可以假设 $z$ 对任何 $b <_0 a$ 都不是在 $H_b$ 中递归可枚举的。给定 $b <_0 a$ 和 $i, j < \omega$，考虑以下陈述：

$(\forall \sigma \in 2^{<\omega})(\exists n)[(n \notin z \land \sigma^\frown 0 1^n \Vdash \neg P_{\Phi(b,i)}(x,j)) \lor (n \notin z \land (\exists \tau \supseteq \sigma^\frown 0 1^n)(\tau \Vdash P_{\Phi(b,j)}(x,i)))]$。$(\sharp_{b,(i,j)})$

由于 $z$ 对 $b <_0 a$ 不是在 $H_b$ 中递归可枚举的，根据引理 7.3.4，$(\sharp_{b,(i,j)})$ 对每个 $b <_0 a$ 和 $n < \omega$ 都成立。我们分阶段构造 $g$ 作为序列 $\{g_s\}_{1 \le s < \omega} \subset 2^{<\omega}$ 的并，其中 $g_0 < g_1 < g_2 < \cdots$。

令 $\langle \langle b_s, \langle i_s, j_s \rangle \rangle \rangle_{s < \omega}$ 成为 $\{b \mid b <_0 a\} \times \omega^2$ 的一个枚举。

- 阶段 0：令 $g_0 = \emptyset$。
- 阶段 s + 1：
- 子阶段 1。定义 $g(s, 1) = g_s \frown z^*(s) \frown H_a(s)$。
- 子阶段 2。定义 $g(s, 2) = g(s, 1) \frown 0^{\langle b_s, \langle i_s, j_s \rangle \rangle} 1$。
- 子阶段 3。
- 情况 (1)：$2^{b_s} \# a$。定义 $g(s, 3) = g(s, 2) \frown 0^{e_s} 1$，其中 $e_s$ 是一个索引，使得 $\Phi_{e_s}^z = \Phi_{H_a(b_s)}^{H_a}$（$b_s = 2^c$ 对某个 $c$）或 $\Phi_{e_s}^z = \Phi_{H_a(b_s)}^{H_a}$（$b_s = 3 \cdot 5^e$ 对某个 $e$）。
- 情况 (ii)：$2^{b_s} = a$。令 $g(s, 3) = g(s, 2) \frown 0^{e_s} 1$，其中 $e_s$ 是一个索引，使得 $\Phi_{e_s}^z = \Phi_{H_a(b_s)}^{H_a}$（$b_s = 2^c$ 对某个 $c$）或 $\Phi_{e_s}^z = \Phi_{H_a(b_s)}^{H_a}$（$b_s = 3 \cdot 5^e$ 对某个 $e$）。
- 子阶段 4。找到最小的 $n$ 使得以下之一成立：

  $n \notin z \land g(s, 3) \frown 0^n 1 \Vdash \neg P_{\Phi(b,i_s)}(x, j_s)$

  或

  $n \notin z \land (\exists \tau \supseteq g(s, 3) \frown 0^n 1)(\tau \Vdash P_{\Phi(b,j_s)}(x, j_s))$。

  根据 $(\sharp_{b,(i_s,j_s)})$，这样的数 $n$ 存在。如果它满足析取式的前半部分，定义 $g_{s+1} = g(s, 3) \frown 0^n 1$。否则，选择字典序最小的 $\tau$ 使得 $\tau \supseteq g(s, 3) \frown 0^n 1$ 且 $\tau \Vdash P_{\Phi(b,i_s)}(x, j_s)$。定义 $g_{s+1} = g(s, 3) \frown \tau$。

令 $g = \bigcup_{s < \omega} g_s$。

很明显，$g$ 是 $a$-泛的。根据引理 7.3.6，$\hat{H}_g^z \equiv_T g \oplus H_a$。根据引理 7.3.4，该构造可以由 $g$ 在 $H_a$ 中解码。所以 $z \oplus g \le_T g \oplus H_a \equiv_T \hat{H}_g^z$。

为了证明 $z \oplus g \ge_T \hat{H}_g^z$，只需通过 $z \oplus g$ 解码构造并计算 $H_a$。为此，我们重复定理 7.3.1 证明中的相同步骤。假设我们知道 $g_s$。那么 $z(s+1) = g(|g_s|+1)$ 和 $H_a(s) = g(|g_s|_2)$。然后通过计算 $g(s, 2)$ 得到 $(b_s, i_s, j_s)$。通过计算 $g(s, 3)$，我们找到一个 $e_s$ 使得 $\Phi_{e_s}^z$ 计算集合 $\{(\sigma, i_s, j_s) \mid \sigma \Vdash P_{\Phi(b,i_s)}(x, j_s)\}$。为了计算 $g_{s+1}$，搜索唯一的数 $n$ 使得 $(g \mid |g(s, 3)|) \frown 0^n 1 \prec g$。根据构造，以下之一成立：

- (1) $n \notin z$ 或
- (2) $n \notin z$ 并且存在一个 $\tau \supseteq g(s, 3) \frown 0^u 1$ 使得 $\tau \Vdash P_{\Phi(b_s)}(x, j_s)$。

我们可以使用 $\Phi_e^\tau$ 来找到 $\tau$。那么 $g_{s+1} = \tau$ 并且我们得出 $z \oplus g \ge_T H_a$。

### 7.3.3 进一步的推广

Posner–Robinson 定理（7.3.1）到超有限的另一个推广如下：

#### 定理 7.3.7 (Shore and Slaman [134]). 对于任何递归序数 $\beta$，如果 $x \not\le_T 0^{(\gamma)}$ 对 $\gamma < \beta$，那么存在一个 $g$ 使得 $x \oplus g \equiv_T g^{(\beta)}$。

定理 7.3.7 通过一种与 Cohen forcing 不同的 forcing 参数（Kumabe–Slaman forcing）来证明，并用于证明完整 Turing 度 $0'$ 的可定义性（参见练习 7.3.3）。另一方面，可以将定理 7.3.7 扩展到超越递归序数的范围。Woodin 使用集合论参数证明了这一点：

#### 定理 7.3.8 (Woodin [169]). 如果 $z$ 不是超算术的，那么存在一个 $g$ 使得 $z \oplus g \equiv_T 0^{(\delta)}$。

### 7.3.4 练习

- **练习 7.3.1.** 证明引理 7.3.3 和引理 7.3.4。
- **练习 7.3.2.** 证明，不使用定理 7.3.8，如果 $x >_T 0^{(\beta)}$ 对 $\beta < \omega_1^{CK}$，那么存在一个 $g$ 使得对所有 $\beta < \omega_1^{CK}$ 都有 $x \ge_T g^{(\beta)}$。
- **练习 7.3.3** (Shore and Slaman [134]). 使用定理 7.3.7，证明如果对于某个 $n > 1$，函数 $\mathbf{x} \mapsto \mathbf{x}^{(n)}$ 在 $(\mathscr{P}, \le)$ 中可定义，其中 $\mathscr{P}$ 是 Turing 度的集合，那么函数 $\mathbf{x} \mapsto \mathbf{x}'$ 也在 $(\mathscr{P}, \le)$ 中可定义。

## 7.4 对 $2^\omega$ 上序保持函数的分类

我们说 $f : 2^\omega \to \omega_1$ 是度不变的，如果 $x \equiv_T y$ 蕴含 $f(x) = f(y)$。

#### 引理 7.4.1. 假设 $f : 2^\omega \to \omega_1$ 是度不变的，并且在一个锥上 $f(x) < \omega_1^x$。那么 $f$ 在一个锥上是常数。

**证明。** 假设 $f : 2^\omega \to \omega_1$ 是 Turing 不变的，并且在 $\{x \mid x \ge_T z_0\}$ 上 $f(x) < \omega_1^x$。对于任何 $e$，令 $A_e = \{x \mid x \ge_T z_0 \land \Phi_e^x \text{ 是序类型为 } f(x) \text{ 的良序}\}$。那么存在一个 $e_0$ 使得 $A_{e_0}$ 是终沓的。根据命题 6.65，存在一个指示树 $T_0$ 使得对 $x \in [T_0]$ 有 $x \in A_{e_0}$。我们声称存在一个可计序数 $a_0$ 使得对 $x \in [T_0]$ 有 $f(x) < a_0$。否则，对于任何 $x$，$x \in \text{WO}$ 当且仅当存在一个 $y \in [T_0]$



并且一个保序函数 \( f \) 从 \( x \) 到 \( \Phi^y_e \)。换句话说，WO\(_1\) 是 \( \Delta^1_1(T_0) \)，这产生了矛盾。

再次由命题 6.6.5，存在一个指示树 \( T_1 \subseteq T_0 \) 和一个可数序数 \( \alpha_1 < \alpha_0 \)，使得对任意 \( x \in [T_1] \) 都有 \( f(x) = \alpha_1 \)。

如果 \( F : 2^\omega \to 2^\omega \) 是度不变的，那么当对任意 \( x \le_T y \) 都有 \( F(x) \le_T F(y) \) 时，它是保序的。

**定理 7.4.2** (Slaman and Steel [142]). 假设 ZF + AD + DC. 假设 \( F : 2^\omega \to 2^\omega \) 在一个锥上是保序且递增的。那么要么 (i) 存在一个 \( a < a_1 \)，使得在一个锥上 \( F(x) =_T x^{(a)} \)，要么 (ii) 在一个锥上，对任意 \( a < a_1 \) 都有 \( F(x) >_T x^{(a)} \)。

证明. 假设 \( F \) 在锥 \( C \) 上是递增的。如果 (ii) 对 \( F \) 不成立，那么由引理 7.4.1 和命题 6.6.5，存在一个序数 \( a < \omega_1 \)，使得在一个锥 \( C_1 \subseteq C \) 上 \( x^{(a)} \le_T F(x) \)。令 \( \alpha_0 \) 为满足条件的最小序数。那么对任意 \( \beta < \alpha_0 \) 都有 \( F(x) >_T x^{(\beta)} \)。我们可以假设 \( \alpha_1 > \alpha_0 \)。令 \( x_0 \in C_1 \)。通过将定理 7.3.2 相对化到 \( x_0 \)，存在一个 \( y \ge_T x_0 \) 使得 \( F(x_0) \equiv_T y^{(\alpha_0)} \)。由于 \( F \) 是保序且递增的，\( F(y) \ge_T F(x_0) \equiv_T y^{(\alpha_0)} \)。因此 \( F(y) \equiv_T y^{(\alpha_0)} \)。由此可见集合 \( \{x \mid F(x) \equiv_T x^{(\alpha_0)}\} \) 是终沓的。再次由命题 6.6.6，在一个锥上 \( F(x) \equiv_T x^{(\alpha_0)} \)。

### 7.4 练习.

**练习 7.4.1.** 假设 ZF + AD + DC. 假设 \( F \) 在一个锥上是保序且递增的。那么要么 (i) 在一个锥上 \( (\exists a < \omega_1)(F(x) \equiv_T x^{(a)}) \)，要么 (ii) 在一个锥上 \( F(x) \ge_T 0^\alpha \)。

## 7.5 压下函数

一个函数 \( F : 2^\omega \to 2^\omega \) 在锥 \( C \) 上被称为压下函数，如果对 \( x \in C \) 都有 \( F(x) <_T x \)。由定理 7.1.3，每个在锥上压下的均匀度不变函数在一个锥上是常数。

**定理 7.5.1** (Slaman and Steel [142]). 假设 ZF + AD + DC. 如果 \( F \) 是一个在锥上的度不变压下函数，那么 \( F \) 在一个锥上是常数。

定理 7.5.1 的证明. 假设 \( F \) 是某个 \( z \) 的锥 \( C = \{x \mid x \ge_T z\} \) 上的度不变压下函数。由命题 6.6.5，存在一个 \( e_0 \) 和一个指示树 T，使得对所有 \( x \in [T] \) 都有 \( F(x) = \Phi^z_{e_0} \)。由引理 7.1.5，我们可以假设 \( \Phi_{e_0} \) 是从 [T] 到一个完备集 [S] 的同胚。

不失一般性，我们可以假设对于任意分裂节点 \( \alpha \in T \)，\( \Phi_{e_0}^{\alpha \upharpoonright 0} \) 与 \( \Phi_{e_0}^1 \) 兼容。计划是在 [T] 中找到两个实 \( x_0, x_1 \le_T T \)，使得 \( \Phi_{e_0}^{x_0} \oplus \Phi_{e_0}^{x_1} \ge_T T \)。由于 F 是度不变的且 T 是指示的，\( F(x_0 \oplus x_1) \equiv_T F(x_0) \equiv_T F(x_0) \oplus F(x_1) \ge_T T \equiv_T x_0 \oplus x_1 \)。这与在 C 上 \( F(x) <_T x \) 的假设矛盾。下面的引理说明，对于 \( x \in [T] \)，任何函数 \( h \le_T x \) 的增长率都由 F(x) 控制。

#### 引理 7.5.2. 假设 \( x \in [T] \) 且 \( h \le_T x \)。对每个 e，令 \( l^e \) 为在 \( \Phi_{e_0}^x \) 中递归的函数，使得

\( l^e(0) = 0 \)

和

\( l^e(n + 1) = \sum_{i \le n} \min \{ m \mid \Phi_{e(i)}^{x \upharpoonright m}(i) \downarrow \} \).

那么存在一个 e，使得 \( l^e \) 是全定的且 \( (\exists m)(\forall n \ge m)(h(l^e(n)) < l^e(n + 1)) \)。

证明. 不失一般性，我们可以假设 h 是递增的。假设引理不成立。我们在 [T] 中构造一个实 \( y \le_T x \)，使得 \( \Phi_e^y \ne \Phi_{e_0}^x \)。如果需要，通过缩小 T，我们可以假设 \( x \le_T T \)。由于 T 是指示的，我们有 \( y \equiv_T x \) 但 \( \Phi_{e_0}^x \not\ge_T \Phi_{e_0}^y \)，这产生矛盾。

y 的构造是关于 x 的完全逼近递归。我们将构造一个 x-递归序列 \( \sigma_0 < \sigma_1 \cdots \) 并令 \( y = \bigcup_{s < \omega} \sigma_s \)。在任何阶段 s，我们可以声明一个数 e 被废弃。

令 \( \sigma_0 = 0 \)。

在阶段 s + 1，令 \( \tau > s \) 为 T 中的直接分裂节点，使得对某个 \( k_s \) 有 \( \Phi_{e_0}^{\tau \upharpoonright 0}(k_s) \downarrow \neq \Phi_{e_0}^{\tau \upharpoonright 1}(k_s) \downarrow \)。对 \( i \in \{0,1\} \)，令 \( \tau_i > \tau \) 为 T 中的下一个直接分裂节点，使得对某个 \( k_s^i > k_s \) 有 \( \Phi_{e_0}^{\tau_i \upharpoonright 0}(k_s) \downarrow \neq \Phi_{e_0}^{\tau_i \upharpoonright 1}(k_s) \downarrow \)。

搜索最小的未被废弃的 e < s，使得 \( \Phi_e^{h(h(|\tau_0| + |\tau_1|))}(k_s) \downarrow \)。

如果存在这样的 e，则令 \( \sigma_{s+1} = \tau^i \)，其中 i 是使得 \( \Phi_e^{h(h(|\tau_0| + |\tau_1|))}(k_s) \downarrow \neq \Phi_{e_0}^{\tau_i}(k_s) \) 的最小数，并废弃 e。否则，令 \( \sigma_{s+1} = \sigma_s \)。

显然 \( y \le_T x \)。假设对某个 e 有 \( \Phi_e^y = \Phi_{e_0}^{x_0} \)。由假设，对任意 m 存在 \( n \ge m \) 使得 \( h(l^e(n)) \ge l^e(n + 1) \)。令 \( s_0 \) 为足够大的阶段，使得在 \( s_0 \) 之后没有 \( e' \le e \) 被废弃。那么存在一个 \( n > |s_0| + s_0 \) 使得 \( h(l^e(n)) \ge l^e(n + 1) \)。令 \( s_1 \) 为满足 \( k_{s_1} \le l^e(n) \) 的最大阶段 \( \ge s_0 \)。那么在阶段 \( s_1 + 1 \)，要么 \( k_0 \) 要么 \( k_1 \) 大于 \( l^e(n) \)。因此 \( \Phi_{e_0}(k_{s_1}) > l^e(n) \)。由于 \( k_{s+1} \le l^e(n + 1) \)，我们有 \( \Phi_{e_0}^{h(h(|\tau_0| + |\tau_1|))}(k_s) \downarrow \)。换句话说，e 在阶段 \( s_1 + 1 \) 被废弃。

令 \( t \) 为一个 T-递归递增函数，使得对任意 \( k \) 和 \( \sigma \in 2^{t(k)} \cap T \) 都有 \( |\Phi_{e_0}^\sigma| = k \)。令 \( \pi : \omega^\omega \to T \) 为通过归纳定义的函数，如下：

- \( \pi(0) = \sigma \)，其中 \( \sigma \) 是 T 中的分裂节点，使得每个 \( \tau \in T \) 都与 \( \sigma \) 兼容；
- \( (\forall i)(\pi(i^\frown) = \pi(i)^\frown \tau) \)，其中 \( \pi(i)^\frown \tau \) 是 T 中的一个分裂节点，存在有限序列 \( \sigma = \sigma_0 \succ \sigma_1 \succ \cdots \sigma_i \prec \tau \)，使得对每个 \( j \le t(i) \)，\( \sigma_j \) 是 T 中扩展 \( \sigma_{j-1}^\frown 0 \) 的直接分裂节点，且 \( \tau \) 是 T 中扩展 \( \sigma_i^\frown 1 \) 的下一个直接分裂节点。

因此 \( \pi \) 诱导了一个从 \( \omega^\omega \) 到 \([T]\) 的 T-递归连续单射，使得对每个 \( h \in \omega^\omega \)，\( \pi(h) \equiv_T h \oplus T \)。

由引理 7.5.2，对每个 h，存在一个最小的 \( e_h \)，对其选择最小的 \( m_h \) 使得 \( (\forall n \ge m_h)(h(l^{e_h}(n)) < l^{e_h}(n+1)) \)。

注意函数 \( h \mapsto (e_h, m_h) \) 是 \( \Delta_1^1(T) \)。那么对每个对 \( (e, m) \)，集合 \( H_{e,m} = \{h \mid (e_h, m_h) = (e, m)\} \) 是一个 Borel 集，因此具有 Baire 性质。那么存在一个对 \( (e_1, m_1) \) 使得 \( H_{e_1, m_1} \) 不是第一类集。换句话说，存在一个 \( u \in \omega^{<\omega} \) 使得对任意 \( \tau \supset u \)，存在一个 \( h \in H_{e_1, m_1} \) 与 \( h \supset \tau \)。现在对任意 \( \sigma \in \omega^{<\omega} \)，我们 T-递归地定义一个有限函数 \( l_\sigma \)，使得 \( l_\sigma(0) = 0 \)

和 \( l_\sigma(n+1) = \sum_{i \le l_\sigma(n)} \min\{m \mid |\Phi_{e_1}^{\sigma(i^\frown m)}[i](m)| \} \)。

对 \( h \in \omega^\omega \)，如果存在一个 m 使得 \( l_{h|n}(m) = k \)，则令 \( l_h(n) = k \)。下面引理的证明是直接的。

#### 引理 7.5.3.

- (i) \( (\forall \sigma)(\forall i)(k[\sigma] > k \land k \supset l_\sigma(i) \Rightarrow l_{k[\sigma]}(i) = k) \);
- (ii) \( (\forall \tau \supset u)(\forall n)(n \ge m_1 \land l_\tau(n) \ge [\tau] \Rightarrow n+1 \notin \text{Dom}(l_\tau)) \).

证明. (i) 如果 \( |\sigma| > k \) 且 \( k = l_\sigma(i) \)，那么 \( |\tau[\sigma]| \ge t(|\sigma|) \ge t(|k|) \)。那么 \( |\Phi_{e_0}^{\pi(k)}| = k \)。因此 \( l_{k[\sigma]}(i) = k \)。

如果 (ii) 不成立，那么存在一个 \( \tau \supset u \) 和 \( n \ge m_1 \) 使得 \( l_\tau(n) \ge [\tau] \) 且 \( l_\tau(n+1) \) 有定义。那么 \( l_\tau(l_\tau(n)) \) 未定义。由对 \( u \) 的假设，存在一个 \( h \supset \tau \) 在 \( H_{e_1, m_1} \) 中，使得 \( h(l_h(n)) > l_\tau(n+1) = l_h(n+1) \)，这产生矛盾。

令 \( x \equiv_T T \)，\( m_2 \ge m_1 \) 和 \( h \supset u \) 使得 \( l_h(m_2) \) 有定义。令 \( \tau_0 = \tau_1 = h \mid l_h(m_2) \)。由引理 7.5.3，\( l_{\tau_0}(m_2) \) 有定义且 \( [\tau_0] = l_{\tau_0}(m_2) \)（因此 \( l_{\tau_0}(m_2+1) \) 未定义）。我们 T-递归地构造两个序列 \( \tau_0 = \tau_0^0 \prec \tau_1^0 \dots \) 和 \( \tau_1 = \tau_1^0 \prec \tau_1^1 \dots \)，如下。





在阶段 $s + 1$，假设 $l_{\tau_i}(m_2 + s)$ 已定义且 $|\tau_i^s| = l_{\tau_i}(m_2 + s)$（因此 $l_{\tau_i}(m_2 + s + 1)$ 未定义），其中 $i = 0, 1$。

情况 1. $x(s) = 0$。那么根据对 $u$ 的假设和引理 7.5.3，取 $r_{\tau_{s+1}}^0 > r_{\tau_s}^0$，使得 $l_{\tau_i}(m_2 + s + 1)$ 已定义且 $|\tau_i^s| = l_{\tau_i}(m_2 + s)$。令 $\tau = (\tau_{s+1}^0)^\frown (l_{\tau_i}(m_2 + s + 1) + 1)$。再次根据对 $u$ 的假设和引理 7.5.3，取 $r_{\tau_{s+1}} > \tau$，使得 $l_{\tau_{s+1}}^r(m_2 + s + 1)$ 已定义且 $|\tau_i^r| = l_{\tau_i}(m_2 + s + 1)$。注意，根据对 $u$ 的假设，存在 $H_{e_1, m_1}$ 中的 $h > r_{\tau_{s+1}}^1$。因此，根据引理 7.5.3，

$l_{\tau_{s+1}}^r(m_2 + s + 1) = l_0(m_2 + s + 1) \ge h(m_2 + s + 1) = l_{\tau_{s+1}}^0(m_2 + s + 1) + 1 > l_{\tau_{s+1}}^0(m_2 + s + 1)$。

情况 2. $x(s) = 1$。做与情况 1 相同的构造，但将 0 替换为 1。我们有

$l_{\tau_{s+1}}^1(m_2 + s + 1) < l_{\tau_{s+1}}^0(m_2 + s + 1)$。

令 $h_i = \bigcup_s \tau_i^s$ 且 $x_i = \pi(h_i) \in [T]$，其中 $i \le 1$。则 $x_0 \equiv_T x_1 \equiv_T T$。令 $l_i$ 为引理 7.5.2 中为 $x_i$ 定义的 $l^{\tau_i}$。则 $l_i \le_T \Phi_{e_0}^{x_i}$，其中 $i \le 1$。而且，

(vii)($(l_i(m+i+1) > l_0(m+i+1)) \Leftrightarrow x(i) = 0$) $\wedge$ ($(l_i(m+i+1) < l_0(m+i+1)) \Leftrightarrow x(i) = 1$)).

因此 $T \equiv_T x \le_T \Phi_{e_0}^{x_0} \oplus \Phi_{e_0}^{x_1}$。

这完成了定理 7.5.1 的证明。

#### 7.5.1 练习

**练习 7.5.1.** 证明在引理 7.5.2 中存在一棵指向树 $T_1 \subseteq T$，使得对任意 $x \in [T_1]$，若 $x$ 是递归的，则 $F(x) \ge_T 0^{(d)}$。

**练习 7.5.2** (Sloman 和 Steel)。假设 $F : 2^\omega \to 2^\omega$ 是一个压下度不变函数。那么存在一个 $z_0$，使得对任意 $z_1$，存在一个 $x \ge_T z_1$ 使得 $F(x) \not\ge_T z_0$。

**练习 7.5.3** (Sloman)。存在一个连续单射 $F : 2^\omega \to 2^\omega$，使得对每个 $x \not\ge_T 0'$，有 $F(x) \equiv_T x$，且对任意 $x \equiv^= y$，有 $F(x) \equiv_T F(y)$，其中 $\equiv^=$ 表示有限差关系。

## 8 $\Pi^1_1$-集的构造

如前几章所示，归纳定义在超算术理论中起着关键作用。事实上，Gandy（参见 [106]）认为，归纳定义而非计算构成了任何广义递归理论的核心特征。可接受集理论（第 3 章）强化了这一思想。在此，我们更详细地讨论归纳定义，并介绍这一概念在构造 $\Pi^1_1$-集方面的一些应用。有关此主题的更多内容，读者可参阅 [47] 和 [106]。

### 8.1 归纳定义简介

#### 8.1.1 归纳可定义性

定义 8.1.1. 设 $\Gamma : 2^\omega \to 2^\omega$ 为一个函数。

- $\Gamma$ 是渐进的，如果对每个 $x \in 2^\omega$ 都有 $x \in \Gamma(x)$；
- $\Gamma$ 是单调的，如果 $y \subseteq x$ 蕴含 $\Gamma(y) \subseteq \Gamma(x)$。

给定函数 $\Gamma : 2^\omega \to 2^\omega$，令

$$
\begin{aligned}
\Gamma_0 &= \emptyset; \\
\Gamma_{\alpha+1} &= \bigcup \Gamma(\Gamma_\alpha) \cup \Gamma_\alpha; \\
\Gamma_\lambda &= \bigcup_{\beta < \lambda} \Gamma_\beta \quad \text{若 $\lambda$ 为极限序数；} \\
\Gamma_\infty &= \bigcup_\alpha \Gamma_\alpha.
\end{aligned}
$$

若实数 $x \in 2^\omega$ 满足 $x = \Gamma_\infty$，则称 $x$ 由 $\Gamma$ 归纳定义。我们用 $|\Gamma|$ 表示满足 $\Gamma_\alpha = \Gamma_\infty$ 的最小序数 $\alpha$。注意 $|\Gamma| < (2^{\aleph_0})^+$。不难看出，对于任意实数 $x$，存在一个函数 $\Gamma : 2^\omega \to 2^\omega$ 使得 $x$ 由 $\Gamma$ 归纳定义（练习 8.1.1）。

定理 8.1.2 (Gandy)。假设 $\Gamma$ 是一个渐进函数，使得集合 $\{(n, x) \in \omega \times 2^\omega \mid n \in \Gamma(x)\}$ 是 $\Pi^1_1$。则 $|\Gamma| \le \omega_1^{CK}$ 且 $\Gamma_\infty$ 是 $\Pi^1_1$。

证明。根据定理 3.1.8，存在一个 $\Sigma_1(L_{\omega_1^{CK}})$-可定义函数 $f : \omega_1^{CK} \to L_{\omega_1^{CK}}$，使得对 $\beta < \omega_1^{CK}$ 有 $f(\beta) = \Gamma_\beta$。设 $x$ 为一个实数，使得

$n \in x \leftrightarrow (\exists \beta < \omega_1^{CK})(n \in f(\beta))$。

注意 $x = \Gamma_{\omega_1^{CK}}$。而且 $x$ 在 $(L_{\omega_1^{CK}}, \in)$ 中是 $\Sigma_1$-可定义的，因此是 $\Pi^1_1$。设 $R$ 为一个递归谓词，使得对任意 $i$，

$i \in \Gamma(x) \leftrightarrow (\forall j) R(i, x \mid j)$。

修正一个 $i \in \Gamma(x)$。则 $(\forall j)R(i, x \upharpoonright j)$。现在，对于每个 $j \in \omega$，存在一个序数 $\beta < \omega_1^{CK}$ 使得 $\Gamma_\beta \upharpoonright j = x \upharpoonright j$，从而对每个 $k \le j$ 有 $R(i, \Gamma_\beta \upharpoonright k)$。由于 $R$ 是递归的，我们有

$(L_{\omega_1^{CK}}, \in) \equiv (\forall j)(\exists R(i, \Gamma_\beta \upharpoonright j))$。

通过归纳，令 $\beta_j$ 为满足 $(L_{\omega_1^{CK}}, \in) = R(i, \Gamma_\beta \upharpoonright k)$ 对每个 $k \le j$ 成立的最小序数 $\beta > \beta_{j-1}$。那么函数 $p : j \mapsto \beta_j$ 是 $\Sigma^1_1(L_{\omega_1^x})$-可定义的，因此根据 $L_{\omega_1^x}$ 的可接受性属于 $L_{\omega_1^x}$。由此可见，序数 $\beta(i) = \bigcup_{j < \omega} \beta_j$ 是小于 $\omega_1^{CK}$ 的极限序数。注意，对 $j < \omega$ 有 $\Gamma_\beta \subseteq \Gamma_{\beta+1}$。那么对每个 $k$，存在 $j \ge k$ 使得 $\Gamma_{\beta(j)} \upharpoonright k = \Gamma_\beta \upharpoonright k$。因此

$(L_{\omega_1^{CK}}, \in) = R(i, \Gamma_{\beta(i)} \upharpoonright k)$。

换句话说，

$(L_{\omega_1^{CK}}, \in) \equiv (\forall k)R(i, \Gamma_{\beta(i)} \upharpoonright k)$。

因此，若 $i \in \Gamma(x)$，则 $i \in \Gamma_{\beta(i)}$，从而 $i \in x$。故 $\Gamma(x) \subseteq x$，即 $\Gamma(x) = x$。我们得出 $x = \Gamma_{co}$。

#### 8.1.2 $\Pi^1_1$-实数的单调归纳可定义性

**命题 8.1.3.** 设 $k > 0$。假设 $\Gamma$ 是渐进且单调的，且集合 $\{(n, x) \mid n \in \Gamma(x)\}$ 是 $\Pi^1_k$。则 $\Gamma_{co}$ 是 $\Pi^1_k$。

证明。由于 $\Gamma$ 是渐进且单调的，$\Gamma_{co}$ 是满足 $\Gamma(x) \subseteq x$ 的最小实数（按包含关系意义）。则 $n \in \Gamma_{co}$ 当且仅当

$(\forall x)(\Gamma(x) \subseteq x \rightarrow n \in \Gamma(x))$。

若集合 $\{(n, x) \mid n \in \Gamma(x)\}$ 是 $\Pi^1_k$，则 $\Gamma_{co}$ 是 $\Pi^1_k$。

以下结果对单调函数加强了定理 8.1.2。

**定理 8.1.4** (Specter [153])。假设 $\Gamma$ 是渐进且单调的，且 $\{(n, x) \in \omega \times 2^\omega \mid n \in \Gamma(x)\}$ 是 $\Pi^1_1$。则 $|\Gamma| \le \omega_1^{CK}$。

证明。我们证明 $\Gamma(\Gamma_{\omega_1^{CK}}) = \Gamma_{\omega_1^{CK}}$ 且 $|\Gamma| \le \omega_1^{CK}$。

- 设 $C \subseteq \mathscr{B}(\omega \times \omega)$ 为一个 $\Sigma^1_1$-集，使得 $x \in C$ 当且仅当
  - $\{n \mid (1, n) \in x\} = \emptyset$
  - $(\forall j)(\Gamma(n \upharpoonright j, n, x) \subseteq \{n \mid \langle 2', n \rangle \in x\})$，且
  - $(\forall e)(e \in \omega \rightarrow (\bigcup_{j \in \omega} n \mid (\Phi_e(j), n) \in x) = \{n \mid \langle 3 \cdot 5^e, n \rangle \in x\})$。

令
$$z = \bigcap_{x \in C} x.$$

则 $z$ 是 $\Pi_1^1$。我们留给读者验证

$(\forall j \in \mathcal{O})((n \mid (j, n) \in z) = \Gamma(j))$。

因此 $\Gamma_{\omega^{CK}} = \{n \mid (\exists j \in \mathcal{O})((j, n) \in z)\}$ 是一个 $\Pi_1^1$-实数。

令 $i \in \mathcal{O}^* \setminus 0$。定义 $D \subseteq \mathcal{O}^* \times 2^\omega$ 为一个 $\Sigma_1^1$-集，使得 $x \in D$ 当且仅当

$(\forall n)(\forall j)(j \in \mathcal{O} \cap 2^\omega \to ((j, n) \in z \leftrightarrow ((j, n) \in x)))$。

根据 Gandy 的基数定理（2.5.3），存在 $z^* \in D$ 使得 $\omega_1^{z^*} = \omega_1^{CK}$。

对于 $j \in \mathcal{O}^*$，令

$z_j^* = \{n \mid (\exists k)(k <_\mathcal{O} j \land (k, n) \in z^*)\}$。

显然 $\Gamma_{\omega^{CK}} = \bigcup_{j \in \mathcal{O} \cap \mathcal{O}^*} z_j^*$。而且，对任意 $j_0 <_\mathcal{O} j_1 <_\mathcal{O} \dots$，有 $z_{j_n}^* \subseteq z_j^*$。

假设 $n \in \Gamma(\omega^{CK})$。我们声称存在 $j \in \mathcal{O} \cap \mathcal{O}_1^*$ 使得 $n \in \Gamma(z_j^*) = \Gamma(\Gamma(j))$。否则，由于 $\Gamma$ 是单调的，必有对任意 $j \in \mathcal{O}_1^* \setminus 0$ 都有 $n \notin \Gamma(z_j^*)$。令

$j \in y_n \leftrightarrow n \in \Gamma(z_j^*)$。

注意，对每个 $j \in \mathcal{O}^*$ 都有 $z_j^* <_{h^*} z^*$。根据推论 2.2.12，$y_n$ 是 $\Pi_1^1\{z^*\}$。根据假设，$y_n = \mathcal{O}_1^* \cap \mathcal{O}$。因此 $y_n$ 也是 $\Sigma_1^1\{z^*\}$，故是 $\Delta_1^1\{z^*\}$。显然 $\omega_1^{\mathcal{O}_1^* \cap \mathcal{O}} > \omega_1^{CK}$，从而 $\omega_1^{y_n} > \omega_1^{CK}$，这与 $z^*$ 的选取矛盾。我们得出 $\Gamma(\Gamma_{\omega^{CK}}) \subseteq \bigcup_{j \in \mathcal{O} \cap \mathcal{O}^*} \Gamma(j) = \bigcup_{j \in \mathcal{O} \cap \mathcal{O}^*} \Gamma[j] = \Gamma_{\omega^{CK}}$。$\square$

#### 8.1.1 归纳定义 $\mathcal{O}$

作为示例，我们展示如何归纳定义 $\mathcal{O}$。设 $\Gamma$ 为一个函数，使得对任意 $x$，

$$
\Gamma(x)(n) = \begin{cases} 1 & n \in x \\ 1 & n = 1 \\ 1 & (\exists m \in x)(n = 2^m), \\ 1 & (\exists e)(\forall i)(n = 3 \cdot 5^e \cdot \Phi_i(e) \in x), \\ 0 & \text{否则。} \end{cases}
$$

我们将其他命题的证明留给读者。

**命题 8.1.5.** 设 $\Gamma$ 如上定义。则 $\Gamma_\infty = \Gamma_{\omega^{CK}} = \emptyset$。

因此 $\mathcal{O}$ 由算术函数 $\Gamma$ 归纳定义。事实上，每个 $\Pi_1^1$-实数都由一个简单的单调函数 $\Gamma$ "生成"（练习 8.1.3）。

#### 8.1.4 练习

**练习 8.1.1.** 证明对于任意实数 $x$，存在一个函数 $\Gamma : 2^\omega \to 2^\omega$ 使得 $x$ 由 $\Gamma$ 归纳定义。





**练习 8.1.2.** 证明命题 8.1.5.

**练习 8.1.3.** 对于任意 \(\Pi^1_1\)-实数 z，存在一个单调函数 \(\Gamma\)，使得集合 \(\{(n, x) \mid n \in \Gamma(x)\}\) 是 \(\Pi^0_2\)，且 z 对 \(\Gamma_\omega\) 多一归约。

**练习 8.1.4.** 假设 \(\Gamma\) 是一个渐进函数，使得 \(\{(n, x) \in \omega \times 2^\omega \mid n \in \Gamma(x)\}\) 是 \(\Pi^0_2\)。证明如果 x 是 \(\Pi^1_1\)，那么每个 \(n \in \Gamma(x)\) 都属于某个超算术 \(y \le x\) 的 \(\Gamma(y)\)。

## 8.2 归纳定义 \(\Pi^1_1\)-实数集

存在一种归纳定义 \(\Pi^1_1\)-实数集的平行方法。在 [164] 中，Engelen、Miller 和 Steel 构造了若干不基于归纳定义方法的 \(\Pi^1_1\)-实数集。1 我们在此通过归纳定义证明了一些结果（参见 Chong 和 Yu [17]）。

#### 8.2.1 实数的 \(\Pi^1_1\)-归纳原理

**定义 8.2.1.** 一个二元关系 \(P(x, y) \subseteq 2^\omega \times 2^\omega\) 称为最终渐进的，如果对于每个实数 x，集合 \(\{y \mid P(x, y)\}\) 在超度中是终沓的，即对于每个 z，存在一个 \(y \ge_h z\) 使得 \(P(x, y)\) 成立。

令 \(\mathbb{C} = \{y \mid y \in L_{\omega_1^y}\}\)。

**引理 8.2.2.** 假设 \((2^\omega)^L = 2^\omega\)。如果 P 是 \(\Pi^1_1\) 且最终渐进的，那么对于每个 x 和 z，存在一个 \(y \ge_h z\) 使得 \(y \in \mathbb{C}\) 且 \(P(x, y)\)。

**证明.** 假设 \((2^\omega)^L = 2^\omega\) 且 P 是最终渐进的。那么对于任意实数 x, z，集合 \(A = \{y \mid x \oplus z \in L_{\omega_1^y}, A(x, y)\}\) 是一个非空的 \(\Pi^1_1(\{x \oplus z\})\)-集。根据定理 4.1.2，存在一个 \(y \in A\) 使得 \(y \in L_{\omega_1^{y[x]}}[x \oplus z]\)。由于 \(x \oplus z \in L_{\omega_1^y}\)，我们有 \(x \oplus z \le_h y\)，因此 \(\omega_1^{x \oplus z} = \omega_1^y\)。于是 \(y \in L_{\omega_1^{y[x]}}[x \oplus z] = L_{\omega_1^y}\) 且 \(P(x, y)\) 成立。

给定一个可数的实数集 A 和一个实数 x，我们说 x 编码 A，如果 \(\{(y)_n \mid n < \omega\} = A\)，其中 \((x)_n = \{m \mid m < \omega \wedge (n, m) \in x\}\)。

一个最终渐进关系按如下方式生成一个渐进关系：设 \(P(x, y)\) 是最终渐进的。对于每个 \(X \in 2^\omega\)，令 \(Q(X) = X \cup \{y \mid (\exists x \in X)P(x, y)\}\)。显然对于所有 X 都有 \(Q(X) \supseteq X\)。然而，像 Q 这样的操作可能过于笼统而不实用，这促使我们对 Q 进行改进，使其类似于良定义集的一致化函数。现在如果 \(P(x, y)\) 是 \(\Pi^1_1\)，那么定理 4.2.1 保证了 P 的一致化函数的存在。然而，我们关注的是强一致化，即一致化“实数初始段”的函数，其大致作用如下：如果 X 编码了 \(\epsilon\) 中的一组实数，使得 x 中任意两个元素 \(w <_L z\) 满足 P(w, z)，那么存在一个 \(\epsilon\) 中的“最小” \(y\) 使得 \(x \le y\) 且 P(x, y) 成立。这种强一致化性质使得可以实现一个归纳构造，其精确表述由以下 \(\Pi^1_1\)-归纳原理 \(\exists\) 给出：

\(\Pi^1_1\)-归纳原理 3. 如果 P(x, y) 是 \(\Pi^1_1\) 且最终渐进的，那么存在一个 \(\Pi^1_1\)-集 \(A \subseteq \epsilon\)，使得：

- (i) \(|\le_L| A\)，即 \(\le_L\) 限制到 A 上的高度，为 \(\omega_1\)；
- (ii) \((\forall y)(y \in A \to (\exists x)(x \in L_{\omega_1^y} \wedge x \text{ 编码集合 } \{z \mid z \in A \wedge z <_L y\} \wedge P(x, y)))\)。

**定理 8.2.3** (Chong 和 Yu [17]). V = L 蕴含 \(\exists\)。

**证明.** 假设 V = L，且 P 是 \(\Pi^1_1\) 且最终渐进的。回顾，对于每个可构可数序数 \(\beta\)，存在一个 \(\alpha > \beta\) 使得 \((L_{\alpha+1} \setminus L_\alpha) \cap 2^\omega \neq \emptyset\)。给定序数 \(\beta < \alpha\) 和 \(X \subseteq \alpha \omega\)，记 \(X[\beta]\) 为实数 \(n \mapsto (\beta, n) \in X\)。我们可以将 X 视为长度为 \(\alpha\) 的实数序列。

由于 P 是 \(\Pi^1_1\)，根据 Spector–Gandy 定理 (3.71)，存在一个 \(\Sigma_0\)-公式 \(\psi(x, y, s)\) 使得
\(P(x, y) \Leftrightarrow (L_{\omega^{xy}}[x, y], \in) \models (\exists s)\psi(x, y, s).\)

假设 V = L。我们定义一个偏函数 F，将证明其在 \(\omega_1 \times \bigcup_{\alpha < \omega_1} 2^{\alpha \omega}\) 上是全函数。对于 \(\alpha < \omega_1\)、\(z \in 2^\omega\) 和 \(X \subseteq \alpha \omega\)，令 \(\omega_1^{X,z}\) 为使得 \(L_\gamma[X, z]\) 可接受的最小序数 \(\gamma\)。我们定义 \(F(\alpha, X)\) 为实数 z，使得 \(L_{\omega_1^{X,z}}[X, z]\) 满足以下性质：

- (1) 存在一个 \(\beta \ge \alpha\) 使得 \(z \in L_{\beta+1} \setminus L_\beta\)；
- (2) 存在一个 \(x \in L_{\omega_1^{X,z}}\) 编码 X；
- (3) 存在一个极限序数 \(\gamma\) 和一个元素 \(s \in L_\gamma\) 使得 \(L_\gamma[X, z] \models \psi(x, z, s)\)；
- (4) 如果 \((t, y) \prec_L (s, z, y)\)，那么 \((L_\mu[X, y], \in) \models \psi(x, y, t)\) 蕴含 \(\omega_1^{(X,y)} < \beta\)；
- (5) 如果 \((t, y) \prec_L (s, z, y)\) 且 \((L_\mu[X, y], \in) \models \psi(x, y, t)\)，那么要么没有实数 \(t \in L_{\omega_1^{X,y}}\) 编码 X，要么 \(y \in L_{\omega_1^{(t,y)}}\)。

由于 \(L_{\omega_1^{X,z}}[X, z] = L_{\omega_1^{X,z}} \prec_L\) 在 \(L_{\omega_1^{X,z}}[X, z]\) 中是一致 \(\Delta_1\) 的。此外，(4) 蕴含 (5) 在 \(L_{\omega_1^{X,z}}[X, z]\) 中是 \(\Sigma_1\) 的。我们证明如果 X 是可数的，则对于 \(\alpha < \omega_1\)，\(F(\alpha, X)\) 有定义。

修正 (a, X)。由于 V = L，存在一个大于 \(\alpha\) 的可数 \(\gamma'\) 和一个实数 \(x \in L_{\gamma'}\) 编码 X。由于 P 是最终渐进的，根据引理 8.2.2，存在一个 \(\beta > \gamma'\) 使得 \((L_{\beta+1} \setminus L_\beta) \cap 2^\omega \neq \emptyset\)，以及一个实数 \(z \in L_{\beta+1} \setminus L_\beta\) 使得对于某个极限序数 \(\gamma < \omega_1^z\) 和 \(s \in L_\gamma\)，有 \(x \in z \prec \omega_1^{X,z} \models \psi(x, z, s)\)。注意 \(L_{\omega_1^z} = L_{\omega_1^{X,z}}[X, z]\) 且对于所有足够大的 \(\gamma' < \omega_1^z\)，\(\gamma' = L_\gamma[X, z]\)。因此 (1)–(3) 得到满足。显然我们可以假设 \((s, z, y)\) 是满足这些性质的 \(<_L\)-最小元。因此 (4) 和 (5) 也得到满足。由于 \(<_L\) 的绝对性，可以得出 F 是在每个 \((\alpha, X)\) 上定义良好的函数，其中 \(\alpha < \omega_1\) 且 X 是可数的。

观察到 (1)-(4) 是 \(\Sigma_1\)-陈述。根据 (4)，可以验证 (5) 是一个 \(\Delta_1\)-陈述。因此存在一个 \(\Sigma_0\)-公式 \(\varphi(a, X, z, s)\) 使得
\(F(a, X) = z \Leftrightarrow L_{\omega_1^X}[X, z] \models (\exists s)\varphi(a, X, z, s).\)

因此我们可以对 \(\alpha\) 进行跨诱导，使用 \(F\) 定义一个序列 \(\{z_\alpha \mid \alpha < \omega_1\}\)。然而，得到的序列通常产生一组在 \(L_{\omega_1}\) 上是 \(\Sigma_1\) 的实数，即 \(\Sigma_1^1\) 但不一定在二阶算术中是 \(\Pi^1_1\)。为了确保达到 \(\Pi^1_1\) 性，我们按如下方式改进方法。

定义 \(G(a) = z\) 当且仅当 \(a < \omega_1^X\) 且存在一个函数 \(f : a + 1 \to 2^\omega\) 与 \(f \in L_{\omega_1}[z]\)，使得对于所有 \(\beta \le a\)，\(f(\beta) = F(\beta, \{\langle \gamma, n \rangle \in f(\gamma) \mid \gamma < \beta\})\) 且 \(f(a) = z\)。由于 \(L_{\omega_1}[z]\) 是可接受的，\(f(\gamma) \mid y \le \alpha \in L_{\omega_1}[z]\)。因此 \(G(a) = z\) 当且仅当存在一个函数 \(f : a + 1 \to 2^\omega\) 与 \(f \in L_{\omega_1}[z]\) 使得
\(\langle L_{\omega_1^\gamma}[z], \in \rangle \models (\forall \beta \le a)(\exists s \in \rho)(\beta, \langle \gamma, n \rangle \in f(\gamma) \land \gamma < \beta \land s, f(\beta)) \land f(a) = z.\)

由于 \(L_{\omega_1^\gamma}[z]\) 是可接受的，\(G\) 是 \(\Sigma_1\)-可定义的。换句话说，\(G(a) = z\) 当且仅当存在一个函数 \(f : a + 1 \to 2^\omega\) 与 \(f \in L_{\omega_1}[z]\) 使得
\(\langle L_{\omega_1^\gamma}[z], \in \rangle \models ((\exists \beta)(\forall \beta \le a)(\exists s \in \rho)(\beta, \langle \gamma, n \rangle \in f(\gamma) \land n \in f(\gamma) \land \gamma < \beta \land s, f(\beta))) \land f(a) = z.\)

令 \(A\) 为 \(G\) 的值域。那么 \(z \in A\) 当且仅当存在一个序数 \(a < \omega_1^Y\) 和一个函数 \(f : a + 1 \to 2^\omega\) 与 \(f \in L_{\omega_1}[z]\) 使得
\(\langle L_{\omega_1^\gamma}[z], \in \rangle \models ((\exists \beta)(\forall \beta \le a)(\exists s \in \rho)(\beta, \langle \gamma, n \rangle \in f(\gamma) \land n \in f(\gamma) \land \gamma < \beta \land s, f(\beta))) \land f(a) = z.\)

因此 \(A\) 是 \(\Pi^1_1\)。

剩下的就是使用类似于定理 3.1.8 的论证来证明 \(G\) 是 \(\omega_1\) 上一个定义良好的全函数。唯一非平凡的部分是证明上面定义的函数 \(f\) 存在。这可以通过归纳来完成。给定 \(a < \omega_1\)，并假设 \(\{f_\beta\}_{\beta < a}\) 是一致 \(\Sigma_1\) 且递增（即对于 \(\beta > \gamma\) 有 \(f_\beta \subset f_\gamma\)）的序列，使得每个 \(f_\beta\) 都是在阶段 \(\beta < a\) 所要求的 \(f\)。令 \(f_a\) 使得 \(f_a \in L_{\omega_1}[z]\) 且对于所有 \(\beta \le a\)，\(f_a(\beta) = F(\beta, \{\langle \gamma, n \rangle \mid n \in f_\beta(\gamma) \land \gamma < \beta\})\) 且 \(f_a(a) = z\)，其中 \(F(a, X) = z\) 且 \(X = \{\langle \gamma, n \rangle \mid \exists \beta(\gamma < \beta \land a \in n \in f_\beta(\gamma))\}\)。注意根据绝对性，\(X = \{\langle \gamma, n \rangle \mid \gamma \le a \land n \in f_\gamma(\gamma)\}\)。那么对于所有 \(\beta < a\)，\(f_a \supset f_\beta\) 且满足阶段 \(a\) 上这样的 \(f\) 的要求。

根据上面的 (1) 和 (2)，\((x, z) \in L_Y\) 且 \(L_Y \in L_{\omega_1}\)。所以 \(A \subset C\)。由于 P 是最终渐进的，定义 I 中的 (i) 得到满足。

对于 (ii)，如果 \(y \in A\)，那么对于某个 \(a < \omega_1\) 有 \(y = G(a)\)。根据 \(G\) 的定义，存在一个实数 \(x \in L_{\omega_1^{G(a)}}\) 使得 \(x\) 编码集合 \(\{G(\beta) \mid \beta < a\}\) 且 \(P(x, G(a))\) 成立。显然 \(\beta < a\) 当且仅当 \(G(\beta) <_L G(a)\)。因此 (ii) 成立。

结果表明，\(\Pi^1_1\)-归纳原理 \(\mathcal{I}\) 与集合论假设 \((\omega_1)^L = \omega_1\) 等价，正如我们现在所示的。




#### 定理 8.2.4.
$(\omega_1)^L = \omega_1$ 当且仅当 $\Pi^1_1$-归纳原理 $\mathfrak{I}$ 成立。

证明. “如果”方向立即成立：选取 $P(x, y)$ 来表达 $x \le_T y$。则 $P$ 是终极渐进的。令 $A$ 为对 $P$ 满足 $\mathfrak{I}$ 的 $\Pi^1_1$-集，其 $<_1$-高度为 $\omega_1$。则 $(\omega_1)^L = \omega_1$。

对于逆方向，假设 $P$ 是 $\Pi^1_1$ 且终极渐进的。则对于任意实数对 $x, z \in L$，集合 $U_{x,z} = \{y \mid y \ge_T z \ge P(x, y)\}$ 是一个非空的 $\Pi^1_1(x, z)$-集。由定理 4.12，存在 $y \in U_{x,z} \cap L$。再次由定理 4.1.2，$(L, \in) \models P$ 是终极渐进的。

由定理 8.2.3，存在一个 $\Pi^1_1$-集 $A$，使得 $(A)^L$ 见证了归纳原理 $\mathfrak{I}$ 在 $L$ 中的正确性。

由于 $(\omega_1)^L = \omega_1$，$\mathfrak{I}$ 在 $V$ 中为真。由于陈述 "$x \in L^A_{\omega_1}$" 是 $\Pi^1_1$ 且 $(L, \in) \models (\forall x)(x \in A \to x \in L^A_{\omega_1})$，

由 Shoenfield 绝对性引理（推论 4.2.9），$(V, \in) \models (\forall x)(x \in A \to x \in L^A_{\omega_1})$。故 $A \subset L$。

令 $y \in A$。由于 $A \subseteq L$，$y \in L$。则存在 $x \in L^A_{\omega_1}$ 使得 $(L, \in) \models x$ 编码集合 $\{z \mid z \in A \wedge z <_L y\} \wedge P(x, y)$。

由于 $A \subset L$，$x$ 编码集合 $\{z \mid z \in A \wedge z <_L y\}$。由于关系 $P$ 是 $\Pi^1_1$ 且 $x, y \in L$，再次由 Shoenfield 绝对性引理（推论 4.2.9），$P(x, y)$ 成立。故 (ii) 得证。

可以将 $\Pi^1_1$-归纳原理 $\mathfrak{I}$ 相对化以容纳实数参数，并得到其粗体版本 $\underline{\mathfrak{I}}$。则定理 8.2.4 可推广为：粗体 $\Pi^1_1$-归纳原理 $\underline{\mathfrak{I}}$ 失败当且仅当不存在实数 $x$ 使得 $(\omega_1)^{L[x]} = \omega_1$。这导出以下结论。

#### 推论 8.2.5.
陈述 "ZFC + $\Pi^1_1$-归纳原理 $\mathfrak{I}$ 为假" 是相容的，当且仅当 "ZFC + 存在不可达基数" 是相容的。

证明. 若 $\mathfrak{I}$ 失败，则对所有 $x$ 有 $(\omega_1)^{L[x]} < \omega_1$，故后者在 $L$ 中是不可达的。反之，假设 ZFC + "存在不可达基数" 是相容的。则由命题 6.2.9（Lévy 折叠映射），ZFC + "$\omega_1$ 在 $L^r$ 中是不可达的" 是相容的。

现在在具有该性质的模型 $M$ 中，对所有 $x$ 有 $\omega_1 > (\omega_1)^{L[x]}$。故 $\mathfrak{I}$ 在 $M$ 中失败。

#### 8.2.2 练习

**练习 8.2.1** (Miller [100]). $2^\omega$ 的一个子集若其任意两个不同元素的交集为有限集，则称其为近不相交。假设 $2^\omega = (2^\omega)^L$。证明存在一个 $\Pi^1_1$-极大近不相交集。

## 8.3 \(\Pi^1_1\)-极大链和 Turing 度的反链

我们现在将 \(\Pi^1_1\)-归纳原理 \(\mathfrak{I}\) 应用于构造一些特殊的 \(\Pi^1_1\)-Turing 度集合。

#### 8.3.1 Turing 度中的链

给定偏序 \((P, \le_P)\)，$p \in P$ 是 $A \subseteq P$ 的一个最小覆盖，若对所有 $q \in A$ 有 $q <_P p$，且不存在 $r \in P$ 使得 $r <_P p$ 且具有相同性质。集合 $A \subseteq P$ 是一条 *链*，若对任意 $x, y \in A$，要么 $x \le_P y$ 要么 $y \le_P x$。链 $A$ 是 *极大* 的，若不存在链 $B \supset A$。定义 $P(x, y)$ 当且仅当

\(y\) 是 \(\{\chi(n) \mid n \in \omega\}\) 在 \(\le_T\) 下的一个最小覆盖。

引理 8.3.1. $P(x, y)$ 是一个终极渐进关系。

证明. 我们证明：对于任意可数集合 \(A = \{x_i\}_{i < \omega}\) 和任意实数 \(x\)，存在 $A$ 的一个最小覆盖 $z$ 使得 \(z'' \ge_T x\)。

修正部分递归函数的有效枚举 \(\{\Phi_e\}_{e < \omega}\)。

给定完美树 \(T\)，定义 \(T\) 的第 \(n\) 层 \(Lev_n(T)\) 为

\(\{\sigma \notin Lev_{n-1}(T) \mid (\exists \tau)(\tau \in T \land \sigma \preceq \tau \land \tau \text{ 是 } T \text{ 上的第 } n\text{-th 分裂节点})\}.\)

令 \(\{p_n\}_{n < \omega}$ 为素数的递归一一枚举。允许歧义，我们也将使用 \(p_\sigma\) 表示编码字符串 \(\sigma\) 的素数。给定递归神谕函数 \(\Phi\)，我们用 \(\Phi^v = T\) 来表达以下内容：

- (1) \(\Phi^v\) 是全函数；
- (2) \((\forall n)(\Phi^v(n) = \prod_{\sigma \in Lev_n(T)} p_\sigma)\)。

给定树 \(T\) 和字符串 \(v \in T\)，令 \(T^v\) 为 \(T\) 的子树，由所有扩展 \(v\) 的 \(v' \in T\) 组成。定义 \(L_n(T)\) 为 \(T\) 上最左侧的第 \(n+1\)-th 分裂节点，\(R_n(T)\) 为 \(T\) 上最右侧的第 \(n+1\)-th 分裂节点。

对每个有限字符串 \(\sigma^*\)、实数 \(x\) 和完美树 \(T \subseteq 2^{<\omega}\)（其中 \(\sigma^* \in T\)），定义 \(T(\sigma^*, x, T)\) 为完美树序列 \(T_n\) 的交集，给定如下：

\(T_0 = T^{\sigma^*}\).

\(T_{n+1} = \{\tau \mid (\exists \sigma \in Lev_n(T_n))(\sigma \preceq \tau \land \tau \in S_{n+1})\}.\)

其中 \(S_{n+1}\) 定义如下：

情况 1. \(x(n) = 0\): \(\sigma \in S_{n+1}\) 当且仅当存在 \(\tau \in Lev_{n+1}(T_n)\) 使得 \(\sigma \succeq \tau\) 且 \(\sigma = L_1(T_n^\tau)\) 对某个 \(T_n\) 的第 \(n\)-th 分裂节点 \(v\) 成立。

情况 2. \(x(n) = 1\): \(\sigma \in S_{n+1}\) 当且仅当存在 \(\tau \in Lev_{n+1}(T_n)\) 使得 \(\sigma \succeq \tau\) 且 \(\sigma = R_1(T_n^\tau)\) 对某个 \(T_n\) 的第 \(n\)-th 分裂节点 \(v\) 成立。

\(\mathcal{T}(\sigma^*, x, T) = \bigcap_n T_n\).

换句话说，$\mathcal{T}(\sigma^*, x, T)$ 是一棵子树，粗略地说，在 $T^*$ 的第 $2n$-th 分裂节点处编码 $x(n)$。注意 $\mathcal{T}(\sigma^*, x, T) \oplus_T T \ge_T x$。此外，假设对于某个递归神谕函数 $\Phi$，对所有 $y \in [T]$ 有 $\Phi^y = T$。则存在递归神谕函数 $\Psi$ 使得对所有 $y \in \mathcal{T}(\sigma^*, x, T)$ 有 $\Psi^y = x$。而且，给定神谕函数 $\Phi$ 的索引，递归函数 $\Psi$ 的索引可从 $\sigma^*$ 有效得到。换句话说，存在递归函数 $f$ 使得对所有 $y \in [\mathcal{T}(\sigma^*, x, T)]$ 有 $\Phi_{f(\sigma^*)}^y = x$。由于对所有 $y \in [\mathcal{T}(\sigma^*, x, T)] \subseteq [T]$ 有 $\Phi^y = T$ 且 $x \ge_T \mathcal{T}(\sigma^*, x, T)$，存在递归函数 $g$ 使得对所有 $y \in [\mathcal{T}(\sigma^*, x, T)]$ 有 $\Phi_{g(\sigma^*)}^y = \mathcal{T}(\sigma^*, x, T)$。

我们给出构造背后思想的草图。要得到可数集合 $A = \{x_i\}_{i<\omega}$ 的一个最小覆盖，人们对最小度的构造（见 [82]）做适当修改。为了使最小度相对较高（即通过跳变计算给定的 $x$），需要在构造过程中编码完美树的索引。若构造是一致的，人们可以利用递归定理在逐步构造过程中编码下一个正在定义的完美树的索引。该技术可用于对每个 $i < \omega$ 将 $x$ 和 $x_i$ 编码到 $z$ 中。然而，为了达到最小性的构造是非一致的（人们需要决定下一棵树是 "s-分裂树" 还是 "满树"，这在一般情况下是一个 "双跳变" 问题）。尽管构造高度非一致，但一旦确定所处的情况，构造确实变得一致（见下面构造中的子步骤 3）。这就是使用 $z''$ 来 "提升" 到 $x$ 的原因。

我们现在转向构造。

修正实数 $x$ 和 $A$ 的枚举 $(x_i)_{i \in \omega}$。假设递归神谕泛函 $\Phi_0$ 满足对所有实数 $y$ 有 $\Phi_0^y = 2^{<\omega}$。我们逐步构造一组完美树序列。在第 $n$ 步，我们构造一棵完美树 $T_n \le_T \Phi_{<e(x_i)}$ 和一个有限字符串 $\sigma_n$，使得 $T_n \upharpoonright |\sigma_n| = \{\tau \mid \tau \le \sigma_n\}$，$|\sigma_n| > n$ 且存在递归神谕泛函 $\Phi_{e_n}$ 使得对每个 $y \in [T_n]$ 有 $\Phi_{e_n}^y = T_n$。

#### 构造

- 第 0 步。定义 $T_0 = 2^{<\omega}$ 和 $\sigma_0 = \emptyset$。
- 第 $n+1$ 步。有三个子步骤：
  - 子步骤 1（编码 $x$）。对每个 $k$，若 $x(n) = 0$ 则定义 $\sigma^k_{n+1,0} = R_1(T^{L_k}_n(T_x))$。否则，令 $\sigma^k_{n+1,0} = L_1(T^{R_k}_n(T_x))$。定义 $T_{n+1,0,k} = T^{n_{k+1,0}}_{n,k}$。故存在递归神谕泛函 $\Phi_{k_i}$ 使得对每个 $y \in T_{n+1,0,k}$ 有 $\Phi_{e_k}^y = T_{n+1,0,k}$。注意函数 $k \mapsto i_k$ 是递归的。由递归定理可知存在数 $k_0$ 使得对所有 $y \in [T^{n_{k_0+1,0}}_{n}]$ 有 $\Phi_{k_0}^y = \Phi_{i_{k_0}}^y$。修正此 $k_0$ 并定义 $\sigma^0_{n+1} = \sigma^{k_0}_{n+1,0}$ 和 $T_{n+1,0} = T_{n+1,0,k_0}$。




#### 子步骤 2（对 $x_n$ 编码）。对每个 $k$，定义

```
$T_{n+1,1,k} = \mathcal{T}(R_1(T_{n+1,0}^{L_k(x_n)}), x_n, T_{n+1,0}).$
```

根据上述讨论，存在递归函数 $f, g$，使得对所有 $y \in [T_{n+1,k}]$，都有 $\Phi_{f(k)}^y = x_n$ 且 $\Phi_{g(k)}^y = T_{n+1,1,k}$。根据递归定理，存在一个 $k_1$，使得对所有 $y \in [T_{n+1,1,k_1}]$，都有 $\Phi_{k_1}^y = \Phi_{g(k_1)}^y = T_{n+1,1,k_1}$。定义 $\sigma_{n+1,1} = R_1(T_{n+1,0}^{L_{k_1}(x_n)})$ 和 $T_{n+1,1} = T_{n+1,1,k_1}$。

#### 子步骤 3（强制一个最小覆盖）。这是唯一使用 $z''$ 的地方。

情况 1。存在 $\alpha \in T_{n+1}$ 和一个数 $l_k$，使得对于所有 $m > l_k$，若 $T_1 \supseteq \sigma, (t_1, t_2) \subset T_{n+1,1} \supset \Phi_{k_1}^{t_1}(m) \downarrow \wedge \Phi_{k_2}^{t_2}(m) \downarrow$，则 $\Phi_{k_1}^{t_1}(m) = \Phi_{k_2}^{t_2}(m)$。在字符串编码意义下，选择满足条件的最小 $\sigma \in T_{n+1,1}$。定义 $S = T_0^{l_k}$。对每个 $k$，定义 $S_k = S^R(S^{(l_k)})$。再次根据递归定理，存在一个 $k_2$，使得对所有 $y \in [S^R(S^{(l_k)})]$，都有 $\Phi_{k_2}^y = S^R(S^{(l_k)})$。定义 $\sigma_{n+1} = R_1(S_k^{(l_k)})$ 和 $T_{n+1} = S^{n+1}$。

情况 2。否则，对每个 $k$ 定义 $S_k = T_{n+1,1}^{k-1}$。然后我们可以 $S_1$-递归地找到 $S_k$ 的一个完美树 $P_k$，使得对所有 $y \in [P_k]$，$\Phi_k^y$ 是全函数，并且对于所有 $\tau_0, \tau_1 \in P_k$ 且 $\tau_0 \sqsubset \tau_1$，存在一个 $i$，使得对所有实数 $z_0 \supset \tau_0$ 和 $z_1 \supset \tau_1$，都有 $\Phi_k^i(i) \downarrow \neq \Phi_k^i(i) \downarrow$。根据递归定理，存在一个 $k_2$，使得对所有 $y \in [P_k]$，都有 $\Phi_{k_2}^y = P_k$。令 $T_{n+1} = P_{k_3}$ 和 $\sigma_{n+1} = R_1(T_{n+1,1}^{L_{k_3}(x_n)}) \in T_{n+1}$。

令 $e_{n+1} = k_3$。则对于所有 $y \in [T_{n+1}]$，都有 $\Phi_{e_{n+1}}^z = T_{n+1}$。这完成了第 $n+1$ 步的构造。

注意，通过对 $n$ 归纳，$T_n \le_T \oplus_{i<n} X_i$。

最后，令 $z = \bigcup_n \sigma_n$。

根据构造，对于每个 $n \in \omega$，都有 $T_{n+1} \nleq_T \oplus_{i<n+1} X_i$。如果 $\sigma_n^z$ 是全函数且 $\Phi_{e_{n+1}}^z \nleq \oplus_{i<n+1} X_i$，那么在第 $n+1$ 步的子步骤 3 中我们处于情况 (2)。那么显然 $z \le_T \Phi_{e_{n+1}}^z$。因此 $z$ 是 $A$ 的一个最小覆盖。

我们证明 $z'' \ge_T x$。这通过对 $n$ 归纳来证明：$x(n)$ 可以被 $z''$-一致地计算。为此，我们论证索引 $e_n$ 可以从 $z''$ 一致地计算得出。

假设我们在第 $n+1$ 步。根据归纳假设，假设 $z''$ 递归地计算出索引 $e_n$。根据构造，对于所有 $y \in [T_n]$，都有 $\Phi_{e_n}^z = T_n$。使用 $z$ 递归地找到 $z$ 的一个初始段，它是某个 $k_0$ 的 $R_1(T_n^{L_n(x_n)})$ 或 $L_1(T_n^{L_n(x_n)})$。在第一种情况下，$x(n) = 0$。在第二种情况下，$x(n) = 1$。注意 $\Phi_{k_0}^z$ 是构造中子步骤 1 的完美树。现在使用 $z$ 递归地找到 $k_1$，使得 $R_1((\Phi_{k_0}^z)^{L_{k_1}(x_n)}) \supset z$。那么 $\Phi_{k_1}^z = \mathcal{T}(R_1((\Phi_{k_0}^z)^{L_{k_1}(x_n)}), x_n, T_{n+1,0}) = T_{n+1,1}$。使用 $z''$ 来判断 $\Phi_{k_1}^z$ 处于哪种情况。在情况 1 中，我们使用 $z''$ 递归地找到满足所需性质的最小 $\sigma \in T_{n+1,1}$。令 $S = T_0^{l_k}$。然后使用 $z$ 计算出 $k_2$，使得 $\Phi_{k_2}^z = S^R(S^{(l_k)})$。那么 $e_{n+1} = k_2$ 且 $T_{n+1} = \Phi_{k_2}^z$。在情况 2 中，使用 $z$ 计算出 $k_2$，使得 $R_1(T_{n+1,1}^{L_{k_2}(x_n)}) \le z$。然后根据构造，$e_{n+1} = k_2$ 且 $T_{n+1} = \Phi_{k_2}^z$。因此 $z'' \ge_T x$。

#### 定理 8.3.2（Chong 和 Yu [15]）。假设 \((\omega_1)^L = \omega_1\)。在图灵度中存在一个 \(\Pi^1_1\)-极大链。

证明。根据引理 8.3.1，P 是一个 \(\Delta^1_1\)-最终渐进关系。因此根据定理 8.2.4，存在一个按规定的 \(\Pi^1_1$-集合 A。J(ii) 蕴含 A 是一个极大链。

### 8.3.2 图灵度中的反链

给定一个偏序 \((P, <_P)\)，一个集合 \(A \subseteq P\) 是一个 *反链*，如果任何不同的 \(x, y \in A\) 是 \(<_P\)-不可比的。A 是 *极大* 的，如果它不是反链的真子集。

定义二元关系 P(x, y)，如果以下 (1) 或 (2) 中的一个成立：

- 1. 存在 \(n \neq m\) 使得 \((x)_n \neq (x)_m\) 但 \((x)_n\) 与 \((x)_m\) 图灵可比；
- 2. \(\{(x)_n \mid n \in \omega\} \cup \{y\}\) 是一个反链，使得
  - (2a) \(x \oplus y \in L_{\omega_1^{x,y}}\)，
  - (2b) \(\{(x)_n \mid n \in \omega\} \cup \{(y)_0\}\) 是一个反链，且
  - (2c) 对于每个 \(r <_L y\)，\(\{(x)_n \mid n \in \omega\} \cup \{r\}\) 不是一个反链。

#### 引理 8.3.3。如果 \(2^\omega = (2^\omega)^L\)，那么 P 是一个最终渐进关系。

证明。修正 \(y_0\)。给定 x，令 \(X = \{(x)_n \mid n \in \omega\}\)。假设集合 \(X \cup \{y_0\}\) 是图灵度的一个反链。我们证明对于任何 \(y_1 \ge_T (x \oplus y_0)''\)，存在一个 z 使得

- 1. \(z'' \ge_T y_1\)，
- 2. \(y_0 \le_T z \le_T y_1\)，
- 3. \(X \cup \{z\}\) 是一个反链。

然后给定一个可构造的 \(y_{-1}\) 和一个可数反链 \(X \cup \{y_0\}\)，使得对于每个 \(r <_L y_0\)，\(X \cup \{r\}\) 不是一个反链，根据命题 4.3.4，存在一个 \(y_1 \ge_T (y_{-1} \oplus X \oplus y_0)''\) 使得 \(y_1 \in L_{\omega_1^{y_1}}\)。然后根据上面的 (1)-(3)，存在一个 z 使得 \(z \equiv_T y_1\)（因此 \(y_0 \notin z \in L_{\omega_1^{y_0,x}}\)）且 \(X \cup \{z\}\) 是一个反链。因此 \(P(x, y_0 \oplus z)\) 是最终渐进的。

我们构造一个实数 z 使得 \((z \oplus x)_0'' \ge_T y_1\) 并且满足以下要求：

```
\(N_{e,i} : \Phi_e^{z \oplus y_0}_i \text{ is total} \Rightarrow \Phi_e^{z \oplus y_0}_i \neq \langle x \rangle_i.\)
```

那么 \(X \cup \{z \oplus y_0\}\) 是一个反链。实数 z 是由一串有限字符串 \(\sigma_0 < \sigma_1 < \cdots\) 的并集得到的。

#### 构造

- 步骤 0。令 \(\sigma_0 = \emptyset\)。
- 步骤 n + 1 = (e, i)。

#### 子步骤 1（满足 \(N_{e,i}\)）。考虑以下陈述：

```
\((\exists \tau \supseteq \sigma_n)(\forall \tau_0, \tau_1 \supseteq \tau)(\forall m)(\Phi^{\tau_0 \oplus y_0}(m) \downarrow \land \Phi^{\tau_1 \oplus y_0}(m) \downarrow \rightarrow \Phi^{\tau_0 \oplus y_0}(m) = \Phi^{\tau_1 \oplus y_0}(m)).\)
```

如果该陈述为真，则找到（字典序）最小的这样的 \(\tau\) 并定义 \(\sigma_{n+1}^0 = \tau\)。那么对于每个实数 \(z \supset \sigma_{n+1}^0\)，\(\Phi_e^{z \oplus y_0}\) 是全函数蕴含 \(\Phi_e^{z \oplus y_0} \le_T y_0\)。因此 \(\Phi_e^{z \oplus y_0} \neq (x)_i\)，因为 \(X \cup \{y_0\}\) 是一个反链。如果该陈述为假，则找到最小的 \(\tau_0 \supseteq \sigma_n\)，使得存在一个（最小的）\(\tau_1 \supseteq \sigma_n\) 使得对某个 \(m\)，\(\Phi^{\tau_0 \oplus y_0}(m) \downarrow \neq \Phi^{\tau_1 \oplus y_0}(m) \downarrow\)。定义 \(\sigma_{n+1}^0 = \tau_1\)，其中 \(\Phi^{\tau_1 \oplus y_0}(m) \neq (x)_i(m)\)。

#### 子步骤 2（对 \(y_1\) 编码）。定义 \(\sigma_{n+1} = (\sigma_{n+1}^0)^\frown \langle y_1(n) \rangle\)。

最后，令 \(z = \bigcup_n \sigma_n\)。

由于对于所有 \(i\)，\(y_0 \not\le_T (x)_i\)，同样的结论对 \(z \oplus y_0\) 也成立。根据构造，对于所有 \(i\)，\(z \oplus y_0 \not\le_T (x)_i\)，因此 \(X \cup \{z \oplus y_0\}\) 是一个反链。

要看到 \((z \oplus y_0)'' \ge_T y_1\)，考虑子步骤 1 中的陈述。该陈述可以由 \(y_0''\) 判定。如果它为真，则我们使用 \(y_0''\) 递归地找到最小的这样的 \(\tau\)。那么 \(\tau = \sigma_{n+1}^0\)。否则，我们可以使用 \(y_0''\) 递归地找到 \(\tau_0\) 和 \(\tau_1\)。在这种情况下，我们使用 \(z\) 来决定哪个字符串是 \(\sigma_{n+1}\)。因此 \(y_1(n) = 0\) 当且仅当 \(z(\sigma_{n+1}^0 + 1) = 0\)。而且，\(\sigma_{n+1} = z \upharpoonright [\sigma_{n+1}^0 + 1)\)。因此序列 \((\sigma_n)_n\) 可以从 \(z \oplus y_0''\) 计算得出。所以 \((z \oplus y_0)'' \ge_T z \oplus y_0'' \ge_T y_1\)。

显然整个构造可以由 \(y_1\) 解码。因此 \(y_1 \ge_T z\)。

#### 定理 8.3.4（Chong 和 Yu [16]）。假设 \((2^\omega)^L = 2^\omega\)。在图灵度中存在一个 \(\Pi^1_1\)-稀疏极大反链。

证明。根据引理 8.3.3，P 是一个最终渐进关系。注意 (2c) 等价于

```
\(L_{u^{[\kappa,n]}}(x, y) \models (\exists \beta)((y)_0 \in L_\beta \land (\forall z \in L_\beta)(z <_L (y)_0 \rightarrow (\exists n)((x)_n \ge_T y \lor y \succ_T (x)_n))).\)
```

因此 P 是 \(\Pi^1_1\)。因此根据定理 8.2.4，存在一个具有所需性质的 \(\Pi^1_1\) 集合 A。使用 (3ii)，我们通过对 \(<_L\) 归纳证明 A 是一个反链。

假设 \(x \in A\) 且 \(\{y \mid y \in A \land y <_L x\}\) 是一个反链。根据 (i)，存在一个编码 \(\{y \mid y \in A \land y <_L x\}\) 的 z 使得 \(P(z, y)\) 成立。然后根据 (2)，\(\{(z)_n \mid n \in \omega\} \cup \{y\}\) 是一个反链。所以 A 是一个反链。注意 \(A \in c\)。这连同引理 4.3.1 蕴含 A 是一个稀疏集。根据上面的 (2b)，A 是极大的。

### 8.3.3 练习

练习 8.3.1。证明在图灵度中不存在 \(\Sigma^1_1\)-极大链。

练习 8.3.2。证明 ZFC+ “在图灵度中不存在 \(\Pi^1_1\)-极大链” 是一致的，当且仅当 ZFC+ “存在一个不可达基数” 是一致的。





**练习 8.3.3.** 证明在图灵度中存在一个稀疏的极大反链。

**练习 8.3.4.** 证明图灵度中每个极大反链的大小为 \(2^{\aleph_0}\)。

**练习 8.3.5.** 证明如果在图灵度中存在一个 \(\Pi^1_1\)-稀疏的极大反链，那么每个实数都是可构的。

**练习 8.3.6.** 证明不存在 \(\Pi^1_1\)-极大的高度链。

*练习 8.3.7 (Harrington 和 Kechris [46]). 证明每个 \(\ge \deg(0)\) 的图灵度都是最小覆盖。

## 8.4 针对 \(\Pi^1_1\)-函数的马丁猜想

#### 8.4.1 \(L\) 中的 \(\Pi^1_1\)-马丁猜想

由于博雷尔确定性是 ZF + DC [93] 的一个定理，第 7 章的结果在 ZF + DC 下对 \(\Delta^1_1\)-函数成立。由于第 7 章关注的是全函数，根据命题 11.8 (v)，这些结果也适用于全 \(\Pi^1_1\)-函数。然而，当涉及到偏 \(\Pi^1_1\)-函数时，情况会发生变化。在本节中，如果函数 \(F\) 的图 \(G^F\) 是 \(\Pi^1_1\)，则称函数 \(F\) 为 \(\Pi^1_1\)。我们证明，在 \(V = L\) 的假设下，马丁猜想对某些 \(\Pi^1_1\)-函数不成立。作为开端，引理 7.2.1 说明（在 ZF + AD + DC 下）\(\le_M\) 对于递增的一致度不变函数是一个线性序。如果假设 \(V = L\)，则该结论不成立。

**定理 8.4.1.** 假设 \(V = L\)。存在一个 \(\Pi^1_1\)-一致度不变函数 \(F\)，它在某个锥上是递增且保序的，使得对于所有 \(y\)，存在实数 \(x_0, x_1 \ge_T y\) 满足 \(F(x_0) \equiv_T x_0\) 和 \(F(x_1) \ge_T 0^{(\omega)}\)。

**证明.** 假设 \(V = L\)。定义 \(P(x, y)\) 为

\(y \in L_{\omega_1^y} \wedge 0^{O^y} = (y)_0 \wedge (y)_1 = x \wedge (y)_2 \text{ is the } <_L\text{-least real such that } (y)_2 \not<_T (y)_0.\)

由于 "\(0^{O^y} = (y)_0\)" 是 \(\Pi^1_1\)，\(P\) 是一个 \(\Pi^1_1\)-终沓渐进关系。根据定理 8.2.4，存在一个 \(\Pi^1_1\)-集合 \(A\) 满足 J 中规定的性质。

根据 P 的定义，每个实数都是图灵低于 A 中某个实数的。此外，P 确保 \(<_T\) 在 A 上是一个良序，并与 \(<_L\) 一致。

定义 \(F(x) = y\) 如果

- (1) \(y \in A\);
- (2) \(x \le_T y\);
- (3) \(x \not\ge_T 0 \Rightarrow (\forall n) x \not<_T ((y)_1)_n\).

粗略地说，\(y\) 是 A 中满足 \(x \le_T y\) 的 \(<_T\)-最小实数。

根据 (3) 和 A 的性质，\(F\) 是良定义的。此外，它是 \(\Pi^1_1\)、递增、保序且一致度不变的（\(x \equiv_T y\) 蕴含 \(F(x) = F(y)\)）。而且，由于对于每个 \(x \in A\) 有 \(F(x) = x\)，我们有 \(F(x) \equiv_T x\) 最终成立。

对于每个实数 \(s\)，选择 \(x_s \in A\) 使得 \(x_s \ge_T s\)。然后对于 A 中高于 \(x_s\) 的 \(<_T\)-最小实数 \(y\)，存在一个 \(z\) 对 \(\{x \mid x <_L y \wedge x \in A\} = \{x \mid x <_T y \wedge x \in A\}\) 进行编码，使得 \(P(z, y)\) 成立。显然 \(x'_s \le_T z \le_T O^y\)。根据 P 的定义，

\(O^{x'} \le_T O^{y'} \le_T \Sigma y,\)

且 \((y)_1 = z\)。因此

\(\{((y)_1)_n \mid n \in \omega\} = \{r \mid r \le_T x \wedge r \in A\}.\)

由于对于所有 \(r \in A\) 且 \(r \le_T x'_s\) 有 \(x'_s \le_T r\)，我们有对于所有 \(n \in \omega\) 的 \(x'_s \le_T ((y)_1)_n\)。因此

\(F(x'_s) = y.\)

因此函数 \(F\) 与函数 \(G\) 是 \(M\)-不可比的，其中对于每个 \(x\) 有 \(G(x) \equiv_T x'\)。

假设 ZF + DC + AD。根据引理 7.14，如果 \(F\) 是一致度不变的且在某个锥上非递增，那么对于某个 \(z_0\)，在锥 \(C = \{x \mid x \ge_T z_0\}\) 上有 \(F(x) <_T x\)。我们表明，在 \(V = L\) 下，这对 \(\Pi^1_1\)-函数也失败。

**定理 8.4.2.** 假设 \(V = L\)。存在一个一致度不变、非递增的 \(\Pi^1_1\)-函数 \(F\)，使得在某个锥上 \(F(x) <_T x\)。特别是，\(F\) 在某个锥上不是常数。

**证明.** 令 \(A\) 为定理 8.4.1 中构造的 \(\Pi^1_1\)-集合。定义 \(F(x) = y\) 当且仅当存在一个实数 \(z \equiv_T y'\) 使得

- (1) \(z \in A\);
- (2) \(y\) 的度是最小的；
- (3) 对于某个 \(e\)，\(y = O_e^x\)，使得对于所有 \(i < e\)，如果 \(\Phi_i^x\) 的度是最小的，那么 \((\Phi_i^x)' \# z\)；且
- (4) \(x >_T 0 \Rightarrow (\forall n)(x \le_T ((z)_1)_n)\)。

我们留给读者验证 \(F\) 是所需的反例。

根据引理 7.2.4，ZF + AD + DC 蕴含 \(\le_M\) 在递增一致度不变函数的集合上是一个良序。在 \(V = L\) 的假设下，这再次失败。

**定理 8.4.3.** 假设 \(V = L\)。存在一致度不变、递增的 \(\Pi^1_1\)-函数序列 \(\{f_n\}_{n < \omega}\)，使得对所有 \(n\) 有 \(f_{n+1} <_M f_n\)。因此 \(<_M\) 不是一个预良序。

**证明.** 定义 \(P(x, y)\) 为

\(y \in L_{\omega_1^y} \wedge (y)_0 = x \wedge (y)_1 \text{ is the } <_L\text{-least such that}\)
\((y)_1 \le_T (y)_0 \wedge y \equiv_T (y)_0 \oplus (y)_1 \oplus (y)_2).\)

显然 \(P(x, y)\) 是一个 \(\Pi^1_1\)-终沓渐进关系。根据定理 8.2.4，存在一个 \(\Pi^1_1\)-集合 \(A\) 具有 P 规定的性质。

根据 P 的定义，每个实数都是图灵低于 A 中某个元素的，且 \(<_T\) 在 A 上是一个与 \(<_L\) 一致的良序。

不难看出存在一个算术集合 \( W \subseteq \{(m, n, z) \mid m, n < \omega \land z \in 2^\omega\} \)，使得 \( (W_n^z)_{n < \omega} \)（其中 \( W_n^z = \{m \mid (m, n, z) \in W\} \)）是一组 \( z \)-r.e. 集合的序列，对于每个 \( n \) 满足 \( z <_T W_{n+1}^z \leq_T W_n^z \)。

令 \( f_n(x) = y \) 如果存在一个 \( z <_T y \) 使得

- (i) \( z \in A \);
- (ii) \( z \geq_T x \);
- (iii) \( y = W_{n+1}^z \);
- (iv) \( x >_T 0 \Rightarrow (\forall m)(x \not\leq_T ((z)_0)_m) \).

粗略地说，\( y \) 是 A 中满足 \( z \geq_T x \) 的 \( <_T \)-最小 \( z \) 对应的 \( W_{n+1}^z \)。

显然 \( \{f_n\}_{n < \omega} \) 是一组 \(\Pi^1_1\)-函数的序列。注意，对于 A 中任何 \( x <_T y \)，都有 \( x' \leq_T y \)。因此对于每个 \( n \)，\( f_n \) 是度不变且递增的。

根据 (iv) 和 A 的性质，\( f_n \) 是良定义的。根据 \( \{W_n^z\}_{n < \omega} \) 的选择，\( \{f_n\}_{n < \omega} \) 是一个 \( <_M \)-下降序列。

#### 8.4.2 \(\Pi^1_1\)-马丁猜想的一致性强度

鉴于第 7 章的结果是在 AD 下建立的，而 AD 本质上是一个大基数假设，人们会期望马丁猜想与大基数之间存在直接联系。此类研究的首个层次显然是 \( \Pi^1_1 \)。我们证明，如果 \(\Pi^1_1\)-马丁猜想成立，则 \( 0^\sharp \) 存在。\(^2\) 定义 Friedman 集 \( F^* \) 为
\( F^* = \{x \mid (\forall a < \omega_1^x)(\forall a \subseteq a)(a \in L_{a^+_1} \rightarrow a \in L_{a+1}[x]) \} \)

不难看出 \( F^* \) 是 \( \Sigma^1_1 \)。

**引理 8.4.4.** \( F^* \) 在图灵度中是终沓的。

**证明.** 对于任意实数 \( z \)，令
\( F(z) = \{x \oplus z \mid (\forall a < \omega_1^x)(\forall a \subseteq a)(a \in L_{a^+_1} \rightarrow a \in L_{a+1}[x \oplus z]) \} \)。
那么 \( F(z) \) 是 \( \Sigma^1_1(z) \) 且非空。根据相对于 \( z \) 的 Gandy 基定理（2.5.3），存在一个 \( x \) 使得 \( \omega_1^{x \oplus z} = \omega_1^z \) 且 \( x \oplus z \in F(z) \)。于是 \( x \oplus z \in F^* \)。

我们将使用以下由 Harrington 得出的结果。证明的草图在练习 8.4.3 到 8.4.8 中给出。

**引理 8.4.5** (Harrington [45]). 如果 \( 0^\sharp \) 不存在，则 \( \tilde{F}^* = 2^\omega \setminus F^* \) 在图灵度中是终沓的。

**定理 8.4.6** (Chong, Wang 和 Yu [13]). 如果不存在一致保序的 \(\Pi^1_1\)-函数 \( G \)，使得 \( \{x \mid G(x) = 0^{0^{x'}}\} \) 和 \( \{x \mid G(x) = 0^{0^{0^{x'}}}\} \) 在图灵度中是终沓的，则 \( 0^\sharp \) 存在。





证明。如果 \(0^\sharp\) 不存在，则根据引理 8.4.4 和 8.4.5，\(F^*\) 和 \(\tilde{F}^*\) 都是共终的。设 \(P(x, y)\) 为如下定义的算术谓词

\(x \in \tilde{F}^* \leftrightarrow (\forall y)P(x, y)\)。

#### 断言 1. 若 \(x \le_T y\) 满足 \(x \in F^*\) 且 \(y \in \tilde{F}^*\)，则 \(O^x \le_h y\)。

证明。由于 \(y \notin F^*\)，存在 \(a < \omega_1^x\) 且 \(a \le \omega\) 使得 \(a \in L_{a_1^x}[L_{a+1}(y)]\)。则 \(a \notin L_{a+1}[x]\) 且 \(\omega_1^x \le a < \omega_1^y\)。由于 \(x \le_T y\)，故 \(O^x <_h y\)。

根据断言 1，若 \(x \le_T y\) 满足 \(x \in F^*\) 且 \(y \in \tilde{F}^*\)，则 \(O^{O^x} \le_T O^y\)。

- (1) \((y)_0 = 0^{O^x} \land x \in F^* \text{ 或 } (y)_0 = 1^{O^{O^x}} \land (\exists v \le_T y)(y)_0 \neg P(x, v)\),
- (2) \((y)_1 = O^x\),
- (3) \(\Phi_e^x\) 是偏的 \(\Rightarrow (y)_{e+2} = 0\),
- (4) \(u = \Phi_e^x\) 是全的 \(\Rightarrow\)
  - (i) \((y)_0(0) = 0 \land (\exists v \le_T (y)_1)\neg P(u, v) \land (y)_{e+2} = 1^{O^{0^{y(e_i)}}}\) 其中 \(i\) 是使得 \(O^{y(e_i)} = O^{0^{y(e_i)}}\) 的最小索引，或
  - (ii) \((y)_0(0) = 1 \land (\exists v \le_T (y)_1)\neg P(u, v) \land (y)_{e+2} = 0^{O^{O^x}}\), 或
  - (iii) \((\forall v \le_T (y)_1)P(u, v) \land (y)_{e+2} = 0^{O^{O^x}}\).

可以直接验证 \(G\) 是 \(\Pi^1_1\)。

#### 断言 2. 若 \(x \in F^*\)，则 \(G(x) \equiv_T O^{O^{O^x}}\)。

证明。显然 \(x \in F^* \Rightarrow O^{O^{O^x}} \le_T G(x)\) 且 \((G(x))_0 \oplus (G(x))_1 \le_T O^{O^{O^x}}\)。给定 \(e < \omega\)，\(O^{O^{O^x}}\) 可以一致地判定 \(\Phi_e^x\) 是否全。假设 \(\Phi_e^x\) 是全的。要计算 \((G(x))_{e+2}(n)\)，我们需要检查上述子句 (4 ii, 4 iii)。现在谓词 \((\forall v \le_T (y)_1)P(u, v)\) 是 \(\Delta_1^1(O^x)\)，因此在 \(O^{O^x}\) 中递归。一旦该谓词被判定，\(O^{O^{O^x}}\) 将能够利用两个递归函数 \(f, g\) 完成计算，使得 \(u = \Phi_e^x \Rightarrow O^{O^x} = \Phi_{f(e)}^{O^{O^{O^x}}}\) 且 \(u = \Phi_e^w \Rightarrow O^{O^{O^w}} = \Phi_{g(e)}^{O^{O^{O^x}}}\)。

#### 断言 3. 若 \(x \in \tilde{F}^*\)，则 \(G(x) \equiv_T O^{O^x}\)。

证明。这与断言 2 的证明类似，除了计算 \(((G(x))_{e+2}(n))\) 的最后一步。现在 \(O^{O^x}\) 可以判断 (4 i) 或 (4 iii) 是否成立，如上述断言所示。如果 (4 iii) 成立，则计算再次与上述类似。假设 (4 i) 成立。则 \(u \in F^*\)。根据断言 1，\(O^x \le_h x\) 从而 \(O^{O^x} \le_T O^x = (G(x))_1\)。现在 (4) 中规定的索引 \(i\) 可以通过一个 \(\Pi_1^1(O^x)\) 过程一致地找到。因此 \(O^{O^x}\) 一致地计算 \((G(x))_{e+2}(n)\)。

从最后两个断言可知，\(G\) 是度不变的。此外，根据断言 1，\(G\) 保存 \(\le_T\)。

为了证明 \(G\) 是一致序保持的，设 \(h\) 为一个递归函数，使得 \((\forall x, y, e)(x = \Phi_e^y \Rightarrow O^x = \Phi_{h(e)}^{O^y})\)。此外，设 \(s\) 为另一个递归函数，使得

\((\forall y', x, y, e, i)(x = \Phi_e^{y'} \rightarrow \Phi_i^x = \Phi_{s(i)}^y)\)。

假设 \(x = 0_e^\omega\)。则

- (1) \((G(y))_0 = (G(y))_{i+2}\),
- (2) \((G(y))_1 = 0_{(h(e))}^{(G(y))}\), and
- (3) \((G(y))_{i+2} = (G(y))_{s(i)+2}\)。

故 G 符合要求。

### 8.4.3 练习

**练习 8.4.1.** 利用定理 6.5.6 证明，如果 $0^\sharp$ 存在，则马丁关于 $\Pi^1_1$-一致度不变函数的猜想成立。

**练习 8.4.2.** 证明存在图灵度偏序语言中的一个句子 $\varphi$，使得 \(\{ \mathbf{x} \mid (\mathscr{D} \ge \mathbf{x}), \mathbf{s} \} \models \varphi\) 是共终的，并且如果它包含一个锥，则 \(0^\sharp\) 存在。

**练习 8.4.3.** 假设 \(\alpha > \beta > \omega\) 是可数可接受序数，且 \(g\) 是通过在 \(L_\alpha\) 上进行 Steel 强迫产生的通用实数。那么对于任何序数 \(\gamma < \beta\) 和任何集合 \(A \subseteq \gamma\)，如果 \(A \in L_\alpha \cap L_\beta[g]\)，则 \(A \in L_\beta\)。

**练习 8.4.4.** 假设 Friedman 集合 \(F^*\) 包含一个图灵度锥。那么存在一个实数 \(x\)，使得对于任何 \(y \ge_T x\)、任何 \(\alpha < \omega_1^x\) 和任何 \(A \subseteq \alpha\)，若 \(A \in L\) 则 \(A \in L_\alpha[y]\)。

**练习 8.4.5.** 假设 Friedman 集合 \(F^*\) 包含一个图灵度锥。证明存在一个实数 \(x\)，使得对于任何 \(y \ge_T x\) 和可数序数 \(\alpha\)，若 \(L_\alpha[y]\) 是可接受的，则 \(\alpha\) 是 \(L\) 中的基数。

**练习 8.4.6.** 假设 Friedman 集合 \(F^*\) 包含一个图灵度锥。证明存在一个实数 \(x\)，使得对于任何 \(y \ge_T x\) 和序数 \(\alpha\)，若 \(L_\alpha[y]\) 是可接受的，则 \(\alpha\) 是 \(L\) 中的基数。

**练习 8.4.7.** 假设 \(x\) 是一个实数，使得对于任何序数 \(\alpha\)，若 \(L_\alpha[x]\) 是可接受的，则 \(\alpha\) 是 \(L\) 中的基数。此外，假设 \(V = L[x]\)。那么存在一个序数 \(\alpha < \aleph_2\) 和一个初等嵌入 \(\pi : L_\alpha[x] \to L_{\aleph_1}[x]\)，使得
- \(\aleph_2 \in \text{值域}(\pi)\)，
- 存在一个序数 \(\beta < \alpha\) 使得 \(\pi(\beta) > \beta\)，且
- \((\text{值域}(\pi))^\omega \subseteq \text{值域}(\pi)\)。

**练习 8.4.8.** 如同练习 8.4.7，设 \(\beta\) 为使得 \(\pi(\beta) > \beta\) 的最小序数。那么集合 \(\{ X \in L \mid X \subseteq \beta \land \beta \notin \pi(X) \}\) 是 \(L \cap \mathscr{P}(\beta)\) 上的一个 \(\omega\)-完备非主超滤子。因此存在 \(L\) 到 \(L\) 的一个非平凡初等嵌入。

## 9 递归论中的独立性结果

### 9.1 图灵度的独立集

#### 9.1.1 局部可数偏序

**定义 9.1.1.** 一个偏序集 \((\mathbf{P}, \le_P)\) 是局部可数的，如果对于任何 \(p \in \mathbf{P}\)，\(|\{q \mid q \le_P p\}| \le \aleph_0\)。

**定义 9.1.2.** 一个函数 \(f : (\mathbf{P}, \le_P) \to (\mathbf{Q}, \le_Q)\) 是嵌入，如果对于所有 \(p_0, p_1 \in \mathbf{P}\)，\(p_0 \le_P p_1 \Leftrightarrow f(p_0) \le_Q f(p_1)\)。

显然 \((\mathscr{D}, \le_T)\)，即图灵度的偏序，是局部可数的。Sacks 提出了以下猜想。

**猜想 9.1.3** (Sacks [117]). \(2^{\aleph_0}\) 上的每个局部可数偏序都可嵌入到 \((\mathscr{D}, \le_T)\)。

在假设连续统假设的情况下，已知正解：

**定理 9.1.4** (Sacks [117]). 假设 ZFC + CH。每个局部可数偏序集 \((2^{\aleph_0}, \le_P)\) 都可嵌入到 \((\mathscr{D}, \le_T)\)。

#### 9.1.2 图灵度的独立集

作为猜想 9.1.3 的一个“测试问题”，Sacks 引入了独立集的概念，并猜想每个极大独立图灵度集的大小为 \(2^{\aleph_0}\)。

**定义 9.1.5.** 设 \((\mathbf{P}, \le_P)\) 为一个偏序。\(X \subseteq \mathbf{P}\) 是独立的，如果对于 \(X\) 的任何有限子集 \(Y\) 和任何 \(p \in X \backslash Y\)，存在 \(q \in \mathbf{P}\) 使得 \(p \le_P q \wedge (\forall r \in Y)(r \le_P q)\)。

**定理 9.1.6** (Sacks [117]). 假设 ZFC + CH。每个极大独立图灵度集的大小为 \(2^{\aleph_0}\)。

然而，定理 9.1.6 的结论与 ZFC 独立：

**定理 9.1.7** (Groszek and Slaman [40]). 存在一个模型 \(\mathbb{N} \vDash \text{ZFC} + \neg\text{CH}\)，其中含有一个大小为 \(\aleph_1\) 的极大独立图灵度集。

本节余部分专门用于证明定理 9.1.7。我们从一个基模型 \(\mathbb{M} \vDash \text{ZFC} + \text{GCH}\) 开始。设 \(\mathbb{P} = (P, \le) = \Pi_{\alpha < \omega_1} \mathbb{S}_\alpha\) 为带可数支撑的积 Sacks 强迫，其中 \(\mathbb{S}_\alpha\) 是 \(\alpha < \omega_1\) 的 Sacks 强迫。每个 P-通用集 \(G\) 可视为一个 \((\omega_1)^\mathbb{M}\)-实数序列 \(\langle G_\alpha \rangle_{\alpha \in (\omega_1)^\mathbb{M}}\)，其中 \(G_\alpha = \{i \mid (\alpha, i) \in G\}\)。不难看出 \(\langle G_\alpha \rangle_{\alpha \in (\omega_1)^\mathbb{M}}\) 的图灵度构成一个独立集。





### **引理 9.1.8** (Baumgartner [5]). 如果 G 是 M = (M, ε) 上的 P-泛滤子，那么 M[G] 中每个可数序数集在 M 中也是可数的。

**证明.** 证明是类似于定理 6.2.11 的融合论证，留给读者。

由于 M ⊆ GCH 且 P = (P, ≤) 是具有可数支持的乘积强迫概念，我们有 |P| ≤ (ℵ₁)^M。因此 P 满足 (ℵ₂)^M-c.c. 结合引理 9.1.8，我们有：

### **引理 9.1.9.** P 保持基数。

### **引理 9.1.10.** 对于任何实数 x ∈ M 和可数序数 β，存在可数 α > β 使得 x ≤_T G_α。

**证明.** 我们表明对于任何 x ∈ M 和 β < (ω₁)^M，集合 D_{x,β} = {q ∈ P | q ⊩ (∃α > β)(x ≤_T G_α)} 是稠密的。给定 p ∈ P，存在可数 α > β 使得 p(α) = 未定义。选择任意这样的序数 a，并令 q ≤ p 使得对于 γ ≠ α 有 q(γ) = p(γ)，且 q(α) = {ε ∈ 2^<ω | ∀n < |α|(n is even → ε(n) = x(n))}。那么 q(α) 是一个指向树，其中每条无限路径都 Turing 计算 x。因此 q ∈ D_{x,β}。

对于任何可数序数 α ∈ M，令 R_α ≅ ω × ω 为 M 中 ω × ω 的良序，序类型为 α。令 |n|_{R_α} 表示 R_α 限制于小于 n 的数集上的序类型。定义 Φ_{p,β}(Ġ_p β < α = ((n, m) | Ġ_p(m) = 1 ∧ n ∧ α | n|_{R_α} = β)。

### **引理 9.1.11** (Baumgartner [5]). 对于每个实数 x ∈ M[G] \ M，存在可数序数 α 使得 x ≤_T Φ_{p,β}(Ġ_p β < α。因此 M[G] ⊨ CH。

**证明.** 证明再次是类似于定理 6.2.11 的融合论证。

现在令 X ⊇ G 为一组实数，其 Turing 度在 M[G] 中是最大独立的。我们称这样的 X 为最大独立集。

下一步是通过向 M[G] 添加实数来破坏 GCH，但保持 X 作为最大独立集。令 Q̇ = (Q̇, ≤̇) ∈ M 为一个 P-名称，使得对于任何 p ∈ P，

p ⊩ "Q̇ 是长度为 ω₂ 且具有可数支持的乘积 Sacks 强迫"

且

p ⊩ (∀q)(q ∈ Q̇ ∧ q(α) 已定义 → ω₁ < α < ω₂)。

因此 P * Q̇ 是一个两步迭代强迫。根据定理 6.1.11 以及对于任何 P-泛滤子集 G 都有 M[G] ⊨ CH 的假设，我们有以下引理。

### **引理 9.1.12.** 对于任何 p ∈ P，p ⊩ Q̇ 是 ℵ₂-c.c.

### **引理 9.1.13.** P * Q̇ 保持基数。

**证明.** 根据引理 9.1.9，只需证明对于 M 上的任何 P-泛滤子集 G，M[G] ⊨ Q 保持基数。

如同在引理 9.1.8 中，M[G] ⊨ Q 保持 ℵ₁。根据引理 9.1.12，M[G] ⊨ Q 对于所有 k ≥ ℵ₀ 保持 ℵ_k。因此 M[G] ⊨ Q 保持基数。

令 H 为 M[G] 上的 Q-泛滤子集。那么 H 可以看作实数的一个 ω₂-序列 {H_α}_{ω₁ ≤ α < ω₂}。因此 Q 向 M[G] 添加了至少 ℵ₂ 个实数，我们有以下结论：

### **引理 9.1.14.** 如果 (p, q) ∈ (P, Q)，那么 (p, q) ⊩ CH。

### **引理 9.1.15.** 如果 (p₀, q₀) ∈ (P, Q̇)，a < ω₁，且 (p₀, q₀) ⊩ "x 不在 M[Ġ]"，则存在 z ∈ M 和条件 (p₁, q₁) ≤ (p₀, q₀) 使得 (p₁, q₁) ⊩ G_a ≤_T x \hat{} z。

根据引理 9.1.10 和引理 9.1.15，{G_α}_{α < ω₁} 在 M[G][H] 中仍然是一个最大独立集。本节其余部分专门用于证明引理 9.1.15。

给定一个完美树 T，我们将其与自然同态 τ_T : 2^{<ω} → T 关联，使得 τ_T(0) 是 T 中的分裂节点，并且对于每个 σ ∈ T，σ ≤_T τ_T(0) 或 σ ≥_T τ_T(0)。假设 H 是 M[G] 上的 Q-泛滤子集。令 (G, H) 为一个 P * Q-泛滤子集，并令 p 为一个条件，使得

p ⊩ "Q 是具有可数支持的长度为 ω₂ 的乘积 Sacks 强迫"。

对于任何集合 A ≤ ω₂，我们使用 π_{α ∈ A} H_α 表示 {((α, H_α)) | α ∈ A}。固定一个条件 (p₀, q₀) ∈ (G, H) 使得 p₀ ≤ p 且

(p₀, q₀) ⊩ x ∈ 2^ω \ M[Ġ]。

我们定义在 (p₀, q₀) 之下的条件融合序列 {(p_σ, q_σ)}_{σ ∈ 2^{<ω}}，序数序列 {α_n}_{n < ω}，以及序列 {v_σ}_{σ ∈ 2^{<ω}} ⊂ 2^{<ω}，具有以下性质：

- (1) (∀σ)((p_σ, q_σ) ⊩ x ↾ v_σ = v_σ) 且 σ ≤ τ → v_σ ≤ v_τ ∧ (p_τ, q_τ) ≤ (p_σ, q_σ);
- (2) 对于所有 n，对于所有 σ, τ ∈ 2^n 和所有 α，

  α < ω₁ →

  ((∃m < n)(α = α_m ^ σ(m) ≠ τ(m)) → t_{p_σ(α)}(0) || t_{p_τ(α)}(0)) ∧

  ((∀m < n)(α = α_m → σ(m) = τ(m)) → p_σ(α) = p_τ(α))

  且

  p_σ = p_τ →

  (p_σ ↾ α = p_τ ↾ α →

  ((∃m < n)(α = α_m ^ σ(m) ≠ τ(m))) → t_{q_σ(α)}(0) || t_{q_τ(α)}(0)) ∧

  ((∀m < n)(α = α_m → σ(m) = τ(m))) → q_σ(α) = q_τ(α))；以及
- (3) (∀α)((∃β)(p_β(α) 已定义 ∨ q_α(α) 已定义) → (∀β)(∃m > n)(α = α_m));

以及

- (4) (∀σ)(∀τ ∈ 2^n)(∃m < n)(∃α < ω₁)(α = α_m ^ σ(m) ≠ τ(m)) → v_σ || v_τ)。

现在对于 n < ω 和 a < ω₁，令

p_n(a) = ⋃_{σ ∈ 2^n} p_σ(a)

和

p_ω = ⋂_{n < ω} p_n

假设 p_ω ∈ G。那么对于任何 n 和 m < n，存在 σ_m ∈ 2^n 使得如果 σ_m < ω₁，则 G_{σ_m} ∈ [p_{σ_m}(σ_m)]。定义 τ ∈ 2^ω 使得对于 m ≤ n 有 τ(m) = σ_m(m)。根据 (2)，对于每个这样的 m，p_τ(σ_m) = p_{σ_m}(σ_m)，并且对于每个 σ ∈ 2^n 和其他每个 a，p_τ(a) = p_σ(a)。因此每当 p_τ(a) 已定义时，G_a ∈ [p_τ(a)]。故 p_τ ∈ G。我们有以下引理。

### 引理 9.1.16. 如果 p_ω ∈ G，那么对于每个 n 存在 σ ∈ 2^n 使得 p_σ ∈ G。

如果 a ≥ ω₁，令 q̇_a 为一个名称，使得

q_a(a) = ⋃_{σ ∈ 2^n ∧ p_σ ∈ G} q_σ(a)

根据引理 9.1.16，q̇_a 是良定义的。对于 a > ω₁，令 q̇_a 为一个名称，使得

q_a(a) = ⋂_{n < ω} q_n(a)

### 引理 9.1.17. (p_ω, q_ω) ⊩ (∀α)(p_G ∈ Ġ ↔ v_G = ẋ ⊩ [v_G]).

证明. 根据 (1)，对于任何带有 (p_ω, q_ω) ∈ (G, H) 的泛滤子集 (G, H) 且 x ⊩ [v_G] = v_G，(p_ω, q_ω) ⊩ (∀α)(p_G ∈ Ġ → v_G = ẋ ⊩ [v_G])。根据引理 9.1.16，存在 τ ∈ 2^{<ω} 使得 p_τ ∈ G。根据 (2)，对于任何 σ_m < ω₁ 的 m，σ(m) = τ(m)。再次根据 (2)，p_σ = p_τ ∈ G。

显然 (p_ω, q_ω) ≤ (p₀, q₀)。事实上，对于任何 (p′₀, q′₀) ≤ (p₀, q₀)，在 (p₀, q′₀) 之下存在这样的序列。因此存在 (p_ω, q_ω) 使得 (p_ω, q_ω) ∈ (G, H)。现在对于任何 a < ω₁，令 z_a = ((p_ω, a), v_0) ∈ Ġ 为 2^ω 中的一个实数。那么 z_a 可以看作 M 中的一个实数。根据引理 9.1.17，G_a ⊆ z_a ∩ a，从而证明了引理 9.1.15。

接下来是构造满足 (1)-(4) 的序列，其中满足条件 (2) 是关键。我们需要一个技术性引理。

### 引理 9.1.18. 如果 (p, q) ≤ (p₀, q₀)，则存在一个 n 和一个条件 (p′, q′) ≤ (p, q) 使得对于任何 (p′′, q′′) ≤ (p′, q′)，(p′′, q′′) ⊩ ẋ(n) = i 对某个 i < 2 成立。

证明. 假设不成立。那么存在 (p₁, q₁) ≤ (p₀, q₀) 使得对于任何 n 和 (p′, q′) ≤ (p₁, q₁)，都存在 (p′′, q′′) ≤ (p′, q′) 和某个 i_n < 2 使得 (p′′, q′′) ⊩ ẋ(n) = i_n。那么集合

D_n = {p | p \not\perp p₁ ∨ (∃i)(p ≤ p₁ ∧ (p, q̇₁) ⊩ ẋ(n) = i_n)}

是 M 的一个元素且在 P 中是稠密的。固定一个泛滤子集 (G′, H′) 使得 p₁ ∈ G′。那么 val(ẋ, (G′, H′))(n) = i_n 当且仅当存在 p ∈ D_n ∩ G′ 使得 (p, q̇₁) ⊩ ẋ(n) = i_n。因此 val(ẋ, (G′, H′)) ∈ M[G′]，这产生了矛盾。





设 \( f : \omega \to \omega^3 \) 为递归双射，使得若 \( f(n) = (n_0, n_1, n_2) \) 且 \( n > 0 \)，则 \( n > n_0 \)。序列的构造如下：

第 0 阶段。令 \(\langle p_0, q_0 \rangle = \langle p_0, q_0 \rangle\) 且 \( v_0 = 0 \)。令 \(\{\gamma_i\}_{i < \omega}\) 为可数集合

\(\{ \alpha < \omega_2 \mid p_0(\alpha) \text{ 已定义 } \lor p_0 \Vdash \text{``}q_0(\alpha) \text{ 已定义''} \}\)。

的枚举。对 \( i, j < \omega \) 令 \(\beta_{0(i,j)} = \gamma_i\)。列表中每个 \(\gamma_i\) 都出现无穷多次，以确保它被对角化无穷多次。

第 \( n + 1 \) 阶段。我们将其分解为 \( 2^n + 1 \) 个子阶段。

在子阶段 \( j \le 2^n \) 时，定义 \(\{v'_\sigma\}_{\sigma \in 2^{n+1}}\) 和 \(\{(p'_\sigma, q'_\sigma)\}_{\sigma \in 2^{n+1}}\)，使得对每个 \( \alpha \notin \beta[n] \) 和 \( \sigma \in 2^n \)，都有 \( p'_{\sigma^\frown 0}(\alpha) = p'_{\sigma^\frown 1}(\alpha) \)。

对于 \( \sigma \in 2^n \) 和 \( i < 2 \)，令 \( v'_{\sigma^\frown i} = v'_\sigma \)。若 \( \beta[n] < \omega_1 \)，则

\( p^0_{\sigma^\frown i}(\alpha) = \begin{cases} p_\sigma(\alpha) & : \alpha \notin \beta[n], \\ \tau \in p_\sigma(\alpha) \mid \tau < t_{p_\sigma(\alpha)}(i) \lor \tau \succeq t_{p_\sigma(\alpha)}(i) & : \text{否则.} \end{cases} \)

令 \( q^0_{\sigma^\frown i} = q_\sigma \)。若 \( \beta[n] \ge \omega_1 \)，则 \( p^0_{\sigma^\frown i} = p_\sigma \) 且 \( q^0_{\sigma^\frown i} \) 是一个名称，使得

\( p_\sigma \Vdash q^0_{\sigma^\frown i}(\alpha) = \begin{cases} \check{q}_\sigma(\alpha) & : \alpha \notin \beta[n], \\ \tau \in p_\sigma \land \tau \in \check{q}_\sigma(\alpha) \land (\tau < t_{q_\sigma(\alpha)}(i) \lor \tau \succeq t_{q_\sigma(\alpha)}(i)) & : \text{否则.} \end{cases} \)

因此 \(\{p^0_\sigma\}_{\sigma \in 2^{n+1}}\) 满足 (2)。现在有两种情况需要考虑。

情况 1。\( \beta[n] \ge \omega_1 \)。由于 (4) 仅包含不小于 \( \omega_1 \) 的序数，令 \(\langle p_{\sigma^\frown i}, \check{q}_{\sigma^\frown i} \rangle = \langle p^0_{\sigma^\frown i}, q^0_{\sigma^\frown i} \rangle\)，\( \beta[n+1, i, j] = \beta[n, i, j] \)，且对每个 \( \sigma \in 2^n \) 和 \( i < 2 \)，\( v_{\sigma^\frown i} = v_\sigma \)，并进入下一阶段。

情况 2。\( \beta[n] < \omega_1 \)。固定 \( 2^n \) 的一个枚举 \(\{\sigma_j\}_{1 \le j \le 2^n}\)。

子阶段 \( j + 1 \)。根据引理 9.1.18，存在一个 \( m > |v'_\sigma| \) 和一个 \(\langle p'', q'' \rangle \le \langle p^j_{\sigma^\frown 0}, q^j_{\sigma^\frown 0} \rangle\)，使得对任何 \(\langle p'', q'' \rangle \le \langle p', q' \rangle\)，都有 \(\langle p'', q'' \rangle \Vdash x(m) = i\)。定义

\( p''(\alpha) = \begin{cases} p'(\alpha) & : \alpha \notin \beta[n], \\ p^j_{\sigma^\frown 1}(\alpha) & : \text{否则.} \end{cases} \)

注意，对任何 \( \alpha \notin \beta[n] \)，都有 \( p^j_{\sigma^\frown 0}(\alpha) = p^j_{\sigma^\frown 1}(\alpha) \)。我们有 \(\langle p'', q''_{\sigma^\frown 1} \rangle \le \langle p^j_{\sigma^\frown 1}, q^j_{\sigma^\frown 1} \rangle\)。令 \(\langle r_1, s_1 \rangle \le \langle p'', q''_{\sigma^\frown 1} \rangle\)，使得对某个 \( v^{j+1}_1 > v^j_1 \) 在 \( 2^{m+1} \) 中，\(\langle r_1, s_1 \rangle \Vdash x(m) = 1\) 且 \(\langle r_1, s_1 \rangle \Vdash x \restriction m + 1 = q^{j+1}_{\sigma^\frown 1}\)。定义

\( r'_0(\alpha) = \begin{cases} r_1(\alpha) & : \alpha \notin \beta[n], \\ p'(\alpha) & : \text{否则.} \end{cases} \)

则 \( r'_0 \le p' \)，所以 \(\langle r'_0, q'' \rangle \Vdash x(n) = i\) 对 \( i < 2 \) 成立。因此存在一个 \(\langle r_0, s_0 \rangle \le \langle r'_0, q' \rangle\)，使得 \(\langle r_0, s_0 \rangle \Vdash x(m) = 0\) 且 \(\langle r_0, s_0 \rangle \Vdash x \restriction m + 1 = v^j_{\sigma^\frown 0}\) 对某个 \( v^j_{\sigma^\frown 0} > v^j_\sigma \) 在 \( 2^{m+1} \) 中成立。令 \(\langle p^{j+1}_{\sigma^\frown 0}, q^{j+1}_{\sigma^\frown 0} \rangle = \langle r_0, \check{s}_0 \rangle\)。定义

\( p^{j+1}_{\sigma^\frown 1}(\alpha) = \begin{cases} r_0(\alpha) & : \alpha \notin \beta[n], \\ r_1(\alpha) & : \text{否则.} \end{cases} \)

则 \((p_{a_{j-1}}^{j+1}, s_1) \le (r_1, s_1)\)。令 \(q_{a_{j-1}}^{j+1} = s_1\)。现在对于 \(j' \neq j\) 和 \(i < 2\)，令 \(v_{a_{j'-1}}^{j+1} = v_{a_{j'-1}}^j\)，且

\(p_{a_{j-1}}^{j+1}(a) = \begin{cases} p_{a_{j-1}}^{j+1}(a) : p_{a_{j-1}}^j(a) = p_{a_{j-1}}^{j+1}(a), \\ p_{a_{j-1}}^{j+1}(a) : p_{a_{j-1}}^j(a) = p_{a_{j-1}}^{j+1}(a), \\ p_{a_{j-1}}^{j+1}(a) : \text{否则.} \end{cases}\)

令 \(q_{a_{j-1}}^{j+1}\) 为一个名称，使得

\(q_{a_{j-1}}^{j+1}(a) = \begin{cases} q_{a_{j-1}}^{j+1}(a) : p_{a_{j-1}}^{j+1} = p_{a_{j-1}}^{j+1} \wedge p_{a_{j-1}}^{j+1} \Vdash q_{a_{j-1}}^j(a) = q_{a_{j-1}}^j(a), \\ q_{a_{j-1}}^{j+1}(a) : p_{a_{j-1}}^{j+1} = p_{a_{j-1}}^{j+1} \wedge p_{a_{j-1}}^{j+1} \Vdash q_{a_{j-1}}^j(a) = q_{a_{j-1}}^j(a), \\ q_{a_{j-1}}^{j+1}(a) : \text{否则.} \end{cases}\)

这完成了子阶段 \(j + 1\) 的构造。

对于 \(\sigma \in 2^n\) 和 \(i < 2\)，令 \((p_{a_\sigma}^{j+1}, q_{a_\sigma}^{j+1}) = (p_{a_\sigma}^{j+1}, q_{a_\sigma}^{j+1})\) 且 \(v_{a_\sigma} = v_{a_\sigma}^{j+1}\)。令 \(\{\gamma_i\}_{i < \omega}\) 为可数集合

\(\{\alpha < \omega \mid (\exists \sigma)(\sigma \in 2^{n+1} \wedge (p_\alpha(a) \text{ 已定义} \vee p_\alpha \Vdash \neg \dot{q}_\alpha(a) \text{ 已定义}'))\}\)。

的枚举。令 \(\beta_{n+1,i,j} = \gamma_i\) 对 \(i, j < \omega\)。这结束了第 \(n + 1\) 阶段的构造。最后，对每个 \(n\)，令 \(a_n = \beta_{(n)}\)。

所定义的序列立即满足条件 (1)-(4)，因此定理 9.1.7 的证明完成。\(\square\)

#### 9.1.3 练习

- **练习 9.1.1.** 证明存在一个偏序 \(\langle 2^{<\omega}, \le_P \rangle\)，使得每个大小不超过 \(2^{\aleph_0}\) 的局部可数偏序都可嵌入其中。

- **练习 9.1.2.** 证明定理 9.1.4。

- **练习 9.1.3.** (Sacks [107])。若对任意 \(p \in \mathbf{P}\) 都有 \(|\{q \mid q \le_P p\}| < \aleph_0\)，则称偏序 \(\langle \mathbf{P}, \le_P \rangle\) 为局部有限。证明 \(\langle 2^\omega, \le_P \rangle\) 中的每个局部有限偏序都可嵌入到 \(\langle \mathscr{D}, \le \rangle\) 中。

- **练习 9.1.4.** 证明存在一个大小为 \(2^{\aleph_0}\) 的图灵度独立集 \(X\)。

- **练习 9.1.5.** 证明定理 9.1.6。

## 9.2 将局部有限上半格嵌入到 \(\langle \mathscr{P}, \le \rangle\)

#### 9.2.1 嵌入一个上半格

**定义 9.2.1.** 若对任意 \(p, q \in P\)，都存在 \(r \in P\) 使得 \(r\) 是 \(p\) 和 \(q\) 关于 \(\le\) 的最小上界，则称偏序 \(\langle P, \le \rangle\) 为一个 *上半格*。

我们用 \(p \cup q\) 表示 \(p\) 和 \(q\) 的最小上界。显然 \((\mathscr{P}, \le)\) 是一个上半格。在附加假设下，以下内容加强了练习 9.1.3。

**定理 9.2.2** (Sacks [117])。假设 CH。每个局部有限上半格 \(\langle 2^\omega, \subseteq, \cup \rangle\) 都可嵌入到 \((\mathscr{P}, \le)\) 中。

在 [117] 中，Sacks 询问定理 9.2.2 的结论是否是 ZFC 的一个定理。Groszek 和 Slaman 对该问题给出了否定答案。

**定理 9.2.3** (Groszek and Slaman [40])。存在一个模型 \(\mathbb{N} \models \text{ZFC} + 2^{\aleph_0} = \aleph_2\)，其中存在一个局部有限上半格 \(\langle \omega_2, \le, \cup \rangle\)，它不可嵌入到 \((\mathscr{P}, \le, \cup)\) 中。

#### 9.2.2 定理 9.2.3 的证明

假设 \(\mathbb{M} \models \text{ZFC} + \text{GCH}\)。令 \(\langle X_\beta \rangle_{\beta < \omega_2}\) 为 \(\mathbb{M}\) 中 \(\mathscr{P}(\omega_1)\) 的一个双切枚举。令 \(\mathbb{U} = \langle \mathbb{U}, \le_{\mathbb{U}}, \cup \rangle\) 为 \(\mathbb{M}\) 中的一个上半格，使得

- (1) \(|\mathbb{U}| = \aleph_2\);
- (2) \(\omega_2 \subseteq \mathbb{U}\)，且
- (3) \((\forall \alpha < \omega_1)(\forall \beta < \omega_2)(\beta < \omega_1 \rightarrow (\alpha \le_\alpha \alpha \cup \beta \leftarrow \alpha \in X_\beta))\)。

令 \(\mathbb{P} = \Pi_{\alpha < \omega_2} \mathbb{P}_\alpha\) 为 Cohen 强迫条件的有限支持 \(\omega_2\)-积。根据定理 6.1.11，我们有：

**引理 9.2.4.** \(\mathbb{P}\) 是 c.c.c. 的，因而保持基数。

假设 \(G\) 是 \(\mathbb{P}\)-泛滤。则 \(G\) 可视为实数的一个 \(\omega_2\)-序列 \(\langle G_\alpha \rangle_{\alpha < \omega_2}\)。根据引理 6.1.6，我们有

**引理 9.2.5.** 对于任何 \(\mathbb{P}\)-泛滤集 \(G\)，\(\mathbb{M}[G] \models 2^{\aleph_0} = \aleph_2\)。

假设存在一个 \(\mathbb{P}\)-泛滤集 \(G\) 使得 \(\mathbb{M}[G] \models \text{``}\exists f \text{ 是 } \mathbb{U} \to (\mathscr{P}, \le) \text{ 的一个嵌入}\text{''}\)。令 \(p_0\) 满足

\(p_0 \Vdash \text{``} f \text{ 是 } \mathbb{U} \text{ 到 } (\dot{\mathscr{P}}, \dot{\le}) \text{ 的一个嵌入}\text{''}\)。

那么对于 \(\alpha \le \omega_1\) 和 \(n < \omega\)，存在 \(G\) 中的一个条件 \(p_{\alpha, n} \le p_0\)，使得

\(p_{\alpha, n} \Vdash f(\alpha)(n) = i\)

对某个 \(i < 2\) 成立。

给定一个条件 \(p\)，令 \(a_p = \min\{a \mid (\forall \beta \ge a)(p(\beta) \text{ 未定义})\}\)。设

\(a_\alpha = \sup\{a_{p_{\gamma, n}} \mid \gamma < \omega_1\}\)。

则 \(a_0 < \omega_2\)。令 \(\mathbb{P}_{< a_0} = \Pi_{\beta < a_0} \mathbb{P}_\beta\) 和 \(\mathbb{P}_{\ge a_0} = \Pi_{\beta \ge a_0} \mathbb{P}_\beta\)。则 \(f(\alpha) \in \mathbb{M}[G_{< a_0}]\)，其中 \(G_{< a_0} = \langle \langle \beta, G_\beta \rangle \mid \beta < a_0 \rangle\) 是一个 \(\mathbb{P}_{< a_0}\)-泛滤集。由于 \(\mathbb{P} = \mathbb{P}_{< a_0} \times \mathbb{P}_{\ge a_0}\)，根据定理 6.1.9，\(G_{\ge a_0} = \langle \langle \beta, G_\beta \rangle \mid \beta \ge a_0 \rangle\) 是在 \(\mathbb{M}[G_{< a_0}]\) 上的一个 \(\mathbb{P}_{\ge a_0}\)-泛滤集。显然 \(\mathbb{P}_{< a_0}\) 和



$\mathbb{P}_{\ge \aleph_0}$ 保持基数。而且，$\mathcal{M}[G_{\ge \aleph_0}] \vDash \text{GCH}$。因此，不失一般性，我们可以假设 $\mathcal{M}[G_{\ge \aleph_0}] = \mathcal{M}$。换句话说，对于任何 $\alpha \le \omega_1$，存在一个实数 $x_\alpha \in M$ 使得 $p_0 \Vdash \dot{f}(\alpha) = x_\alpha$。

现在对于 $\alpha < \omega_1 < \beta < \omega_2$，我们有
$p_0 \Vdash \text{``}\dot{x}_{\omega_1} \le_T \dot{f}(\beta) \oplus x_\alpha\text{''} \Leftrightarrow \alpha \in X_\beta$。

根据命题 6.11.7 以及对 $p_0$ 的重排（如有必要），我们可以假设 $p_0 \in \mathbb{P}_{<\omega_1}$。令 $a_{p_0} = \min\{n \mid (\forall \beta < \alpha)(p_0(\beta) \text{ is undefined})\}$。那么 $a_{p_0}$ 是一个可数序数。由于 $\dot{f}(\beta)$ 中出现的序数最多只有可数个，对于 $\beta > \omega_1$，如果 $\dot{f}(\beta)$ 不是一个 $\mathbb{P}_{<\omega_0}$-name，那么存在一个置换 $\iota_g$，将 $\dot{f}(\beta)$ 中的序数换成大于 $a_{p_0}$ 的可数序数。换句话说，$\iota_g$ 诱导了 $\mathbb{P}$ 的一个自同构，使得 $\iota_g(p_0) = p_0$ 但 $\iota_g(\dot{f}(\beta)) \in \mathbb{P}_{<\omega_0}$。再次根据命题 6.11.7，
$p_0 \Vdash \text{``}\dot{x}_{\omega_1} \le_T \iota_g(\dot{f}(\beta)) \oplus x_\alpha\text{''} \Leftrightarrow \alpha \in X_\beta$。

现在在 $\mathcal{M}$ 中，最多有 $2^{\aleph_0} = \aleph_1$ 个针对实数的 $\mathbb{P}_{<\omega_0}$-name。因此存在 $\beta_0 \neq \beta_1$ 使得 $\iota_g(\dot{f}(\beta_0)) = \iota_g(\dot{f}(\beta_1))$。故 $X_{\beta_0} = X_{\beta_1}$，这与假设矛盾。
令 $N = M[G]$。那么 $N \models$ "U 不可嵌入到 $(\mathscr{D}, \le, U)$"。这完成了定理 9.2.3 的证明。

**注释 9.2.6.** 定理 9.1.4（参见 [4]）和定理 9.2.2（参见 [167]）的结论在 ZFC + MA + $\neg$CH 下均可证得。

#### 9.2.3 练习

- **练习 9.2.1.** 证明给定 ZFC 的一个模型 $\mathcal{M}$，如果 $g_1$ 和 $g_2$ 都是 $\mathcal{M}$ 上的 Cohen 通用实数，那么 $\mathcal{M}[g_1] \equiv \mathcal{M}[g_2]$，即初等等价。证明这对于一般强迫概念不成立。

- **练习 9.2.2** (Simpson [4]). 假设 ZFC + MA + $\neg$CH。证明每个局部可数偏序 $(2^\omega, \le_P)$ 都可嵌入到 $(\mathscr{D}, \le)$。

## 9.3 $\mathscr{D}$ 中的终极链

#### 9.3.1 类型为 $\omega_1$ 的终极最大链的存在

**定义 9.3.1.** 给定一个偏序 $(P, <_P)$，集合 $A \subseteq P$ 是一个 _终极链_，如果 $A$ 的元素在 $P$ 下线性有序，并且对于任何 $z \in P$，存在 $x \in A$ 使得 $z \le_P x$。

在 ZFC 下，不难看出图灵度的终极链存在当且仅当 CH 成立。一个自然的问题是：在假设 ZFC + CH 的情况下，是否存在 $(\mathscr{D}, \le)$ 中类型为 $\omega_1$ 的终极最大链？本节将讨论这个问题。

以下事实显而易见。

**引理 9.3.2.** 假设 ZF。存在极小度的 $x_0$ 和 $x_1$，使得 $\mathbf{0}'' \equiv_T x_0 \oplus x_1 \equiv_T x_0'' \equiv_T x_1''$。

**引理 9.3.3.** 假设 ZF。存在一个最大链 $\mathbf{0} = c_0 < c_1 < \dots < c_\omega = \mathbf{0}''$ 在 $[\mathbf{0}, \mathbf{0}']$ 中。

**证明.** 修正 $\mathbf{0}''$ 以下度的一个枚举 $\langle d_n : n \in \omega \rangle$。令 $c_0 = \mathbf{0}$。

假设 $c_n$ 已定义且 $c_n'' = \mathbf{0}''$。将引理 9.3.2 相对化，得到在 $c_n$ 上极小的度 $x_0$ 和 $x_1$，使得 $x_0 \oplus x_1 = c_n'' = \mathbf{0}'' = x_0'' = x_1''$。如果 $d_n < \mathbf{0}''$，则存在 $i < 2$ 使得 $x_i \not\le d_n$，并令 $c_{n+1} = x_i$。如果 $d_n = \mathbf{0}''$，令 $c_{n+1} = x_0$。

最后令 $c_\omega = \mathbf{0}''$。

**定理 9.3.4** (Wang, Wu and Yu [168]). 假设 ZFC。那么 CH 成立当且仅当存在 $\mathscr{D}$ 中类型为 $\omega_1$ 的终极最大链。

**证明.** ($\Rightarrow$) 假设 CH，并令 $\langle d_\alpha \mid \alpha < \omega_1 \rangle$ 为图灵度的一个枚举。

我们归纳构造一个链序列 $\{C_\alpha\}_{\alpha < \omega_1}$，使得

- (1) 对每个 $\beta < \alpha$，存在 $c \in C_\alpha$ 使得 $c \ge d_\beta$；
- (2) 如果 $\alpha = 0$ 或 $\alpha$ 是后继序数，则 $C_\alpha$ 的序类型为 $\alpha + \omega$；
- (3) 如果 $\alpha$ 是极限序数，则 $C_\alpha$ 的序类型为 $\alpha \times \omega$；
- (4) 如果 $\beta < \alpha$，则 $C_\beta \subset C_\alpha$。

令 $C_0 = \{\mathbf{0}\}$。假设 $\alpha = \beta + 1$ 且 $C_\beta$ 已定义。给定 $d_\beta$，我们应用引理 8.3.1 得到 $C_\beta$ 的一个最小上界 $a$，使得 $a'' \ge d_\beta$。将引理 9.3.3 相对化，在 $[\mathbf{a}, \mathbf{a}'']$ 中得到一个最大链 $\mathbf{a} = \mathbf{a}_0 < \mathbf{a}_1 < \dots < \mathbf{a}_\omega = \mathbf{a}''$。令 $C_\alpha = C_\beta \cup \{\mathbf{a}_\gamma : \gamma \le \omega\}$。对于极限序数 $\alpha$，令 $C_\alpha = \bigcup_{\gamma < \alpha} C_\gamma$。令 $C = \bigcup_{\alpha < \omega_1} C_\alpha$。可以直接验证 $C$ 的序类型为 $\omega_1$，$C$ 是一个最大链，并且对于每个 $\alpha < \omega_1$，$C$ 的第 $(\alpha \times \omega + \omega + 1)$ 个元素上界为 $d_\alpha$。

($\Leftarrow$) 由于每个度最多上界可数个度，如果存在如描述的最大链，则 CH 立即成立。

### 9.3.2 无选择公理的 CH

为了继续我们对图灵度序的探讨，我们回顾一些集合论事实。CH 是陈述：不存在集合 $X$ 使得 $|\omega| < |X| < |2^\omega|$，其中 "$|X| \le |Y|$" 意味着存在从 $Y$ 到 $X$ 的满射。因此 ZF + CH 并不明显蕴含实数的良序存在性。GCH 关于 AC 也是如此。事实证明，这两个假设之间存在联系。

**定理 9.3.5** (Sierpinski [136]). ZF + GCH $\to$ AC。

沿着这条思路的一个问题是：定理 9.3.5 是否逐层成立？例如，CH 是否蕴含 $2^\omega$ 的良序存在性？

**定理 9.3.6** (Kanamori and Pincus [62]). ZFC + “存在不可达基数”是相容的，当且仅当 ZF + CH + “不存在 $2^\omega$ 的良序”是相容的。

**证明.** 假设 ZFC + “存在不可达基数”是相容的。根据 Solovay [150]，存在一个 ZF 的模型 $M$，其中每个不可数实数集都包含一个完美子集。换句话说，$M \models$ ZF + CH。此外，$M$ 中不存在实数集的良序。

反之，假设 ZF + CH + “不存在 $2^\omega$ 的良序”是相容的，并令 $M$ 为该理论的传递模型。我们声称 $(\omega_1)^M$ 在 L 中是不可达的。显然 $(\omega_1)^M$ 在 L 中是正则的。只需证明对于任何 $\alpha < (\omega_1)^M$，$|(2^\omega)^L| < \omega_1$。否则，存在一个可数 $\alpha$ 使得 $|(2^\omega)^L| = (\omega_1)^M$。那么 $(2^\omega)^L \in M$ 且 $M$ 中存在 $(2^\omega)^L$ 的良序。由于 $|\omega| < |(2^\omega)^L| \le |2^\omega|$，我们有 $|(2^\omega)^L| = |2^\omega|$。换句话说，$M$ 中存在 $(2^\omega)^L$ 与 $2^\omega$ 之间的双射。由此可知 $M$ 中存在 $2^\omega$ 的良序，这与假设矛盾。

定理 9.3.6 表明，“ZF + CH + 不存在 $2^\omega$ 的良序”是一个如此强的理论，以至于需要不可达基数来保证其相容性。然而，对于强迫扩展，有以下命题：

**命题 9.3.7.** 令 $M \models$ ZFC。如果 $N$ 是 $M$ 的一个保持 $(\omega_1)^M$ 的扩展，且 $N \models$ ZF+“存在图灵度的终极链”，那么 $N \models \neg$CH 当且仅当 $N \models$ “不存在 $2^\omega$ 的良序”。

**证明.** 如果 $N \models$ “存在 $2^\omega$ 的良序”，那么由于 $N \models$ ZF+“存在图灵度的终极链”，我们有 $N \models$ CH。

现在假设 $N \models$ “不存在 $2^\omega$ 的良序”。取 $C \in M$ 为 $(2^\omega)^M$ 的一个子集，使得 $<_T$ 是 $C$ 的一个良序，序类型为 $(\omega_1)^M$。由于 $N$ 是 $M$ 的一个保持 $(\omega_1)^M$ 的扩展，$N \models |\omega| < |C|$。由于 $N$ 中不存在 $2^\omega$ 的良序，我们有 $N \models |C| < |2^\omega|$。所以 $N \models \neg$CH。

### 9.3.3 终极链与 CH

进一步探讨 CH 与图灵度之间的联系，人们会问：在 ZF 下，CH 是否等价于存在类型为 $\omega_1$ 的图灵度终极最大链？答案是否定的：根据 Solovay [150]，存在一个 ZF 的模型 $M$，其中每个不可数实数集都包含一个完美子集。由于 ZF 的一个定理是每个完美集合包含两个图灵度不可比的实数，因此不存在类型为 $\omega_1$ 的图灵度链。

目前尚不清楚 ZF + “存在类型为 $\omega_1$ 的图灵度终极最大链”是否蕴含 CH。然而，有一个部分答案：

**定理 9.3.8** (Wang, Wu and Yu [168]). 如果 ZFC 是相容的，那么 ZF + $\neg$CH + “存在类型为 $\omega_1$ 的图灵度终极链”也是相容的。





本节其余部分专门用于证明定理 9.3.8。我们从基模型 \(\langle L, \in \rangle\) 开始。令 \(\mathbb{P}\) 为 Cohen 强迫条件的集合。\(\mathbb{P}_{\aleph_1}\) 是长度为 \(\aleph_1\) 的有限支持的结果积强迫。

For \(\alpha < \omega_1\), let \(\mathbb{P}_{<\alpha} = (\mathbb{P}_{<\alpha}, \le)\), where \(p \in \mathbb{P}_{<\alpha}\) if and only if \(p \in \mathbb{P}_{\aleph_1}\) and \(\text{dom}(p) \subseteq \alpha\). The partial order on \(\mathbb{P}_{<\alpha}\) is the restriction of that on \(\mathbb{P}_{\aleph_1}\) to \(\mathbb{P}_{<\alpha}\). Thus \(\mathbb{P}_{\aleph_1} = \mathbb{P}_{<\aleph_1}\). Let \(E\) be the set of limit ordinals less than \(\omega_1\). For \(\alpha < \omega_1\), let \(\omega_1^\alpha\) be the least admissible ordinal greater than \(\alpha\). Then \(\mathbb{P}_{<\alpha} \in L_{\omega_1^\alpha}\).

**Lemma 9.3.9.** There exists an uncountable set \(E_1 \subseteq E\) in \(L\) and a sequence of binary relations \(\{R_\alpha\}_{\alpha \in E_1} \in L\) such that for each \(\alpha \in E_1\),
- \(R_\alpha \in L\) is a binary relation on \([2^n \mid n < \omega]\) that is a well-ordering of order type \(\alpha\);
- for each \(\beta < \alpha\), there is a function \(f_\beta \le_T R_\alpha\) which is an isomorphism between \(R_\beta\) and an initial segment of \(R_\alpha\).

Proof. We define \(E_1\) and \(\{R_\alpha\}_{\alpha \in E_1}\) by induction on \(\alpha < \omega_1\). Let \(E_{1,0} = \emptyset\). At stage \(\alpha + 1\), suppose that \(E_{1,\alpha}\) and \(\{R_\gamma\}_{\gamma \in E_{1,\alpha}}\) have been defined. Let \(R \in L\) be a well-ordering of \(\{2^n \mid n < \omega\}\) of order type a limit ordinal greater than that of \(R_\gamma\) for \(\gamma \in E_{1,\alpha}\). Then for every \(\gamma \in E_{1,\alpha}\), there is a function \(f_\gamma\) which maps \(R_\gamma\) isomorphically onto an initial segment of \(R\). Let \(x \in L\) be a real that computes all the \(f_\gamma\)’s. Let \(E_{1,\alpha+1} = E_{1,\alpha} \cup \{\gamma_1\}\) where \(\gamma_1 = \alpha + \omega \cdot \alpha\). Let \(R^1\) be a binary relation on \(\{2^{n+1} \mid n < \omega\}\) such that for any \(n \neq m\), \((2^{n+1}, 2^{m+1}) \in R^1\) if and only if either \(n \in x\) and \(m \notin x\) or \(n \notin x \land m \in x\) and \(n < m\). So \(R^1 \ge_T x\) in \(L\) and is a well-ordering of order type \(\omega + \omega\) on \(\{2^{n+1} \mid n < \omega\}\). Let

\[
R_{\alpha+1} = R \cup R^1 \cup \langle (2^{2n}, 2^{2m+1}) \mid n, m \in \omega \rangle.
\]

If \(\alpha\) is a limit ordinal, let \(E_{1,<\alpha} = \bigcup_{\gamma < \alpha} E_{1,\gamma}\) and repeat the above upon replacing \(E_{1,\alpha}\) by \(E_{1,<\alpha}\).
Let \(E_1 = \bigcup_{\beta < \omega_1} E_{1,\beta}\). Then \(E_1\) and \(\{R_\alpha\}_{\alpha \in E_1}\) are as required.

From now on, let \(E_1\) and \(\{R_\alpha\}_{\alpha \in E_1}\) in \(L\) be as above. Let \(G\) be a \(\mathbb{P}_{\aleph_1}\)-generic set over \(L\). Then \(G\) may be viewed as an \(\omega_1\)-sequence \(\langle G_\alpha \mid \alpha < \omega_1 \rangle\) such that for every \(\alpha < \omega_1\), \(G_\alpha = \bigcup_{p \in G} p(\alpha)\) is a real. Let \(G_\alpha = \langle \langle \beta, G_\beta \rangle \mid \beta < \alpha \rangle\).

**Definition 9.3.10.** For any \(\gamma < \alpha \in E_1\) and any sequence \(\langle z_\beta \rangle_{\beta < \alpha}\) of reals, define the join of \(\langle z_\beta \rangle_{\beta < \gamma}\) along \(R_\alpha\) to be the set

\[
\bigoplus_{R_\alpha} \langle z_\beta \rangle_{\beta < \gamma} = R_\alpha \upharpoonright \{2^n \cdot 3^j \mid (\exists \beta < \gamma)(j \in z_\beta \land \beta = \text{order type of } (R_\alpha \upharpoonright n))\}.
\]

The following lemma says that the join operator is order preserving.

**Lemma 9.3.11.** For any \(\beta_1 \le \beta_2 \le \alpha_1 \le \alpha_2 \in E_1\),

\[
\bigoplus_{R_{\beta_2}} \langle G_\gamma \rangle_{\gamma < \beta_1} \le_T \bigoplus_{R_{\alpha_2}} \langle G_\gamma \rangle_{\gamma < \alpha_1}.
\]

Proof. It is immediate that \( R_{\beta_1} \le_T R_{\alpha_1} \). Let \( f \) be an \( R_{\alpha_1} \)-recursive function which is an isomorphism between \( R_{\beta_1} \) and an initial segment of \( R_{\alpha_1} \). Then for any \( n, j \), \( 2^n \cdot 3^j \in \bigoplus_{R_{\beta_1}} (G_\gamma)_{\gamma < \beta_1} \) if and only if \( 2^{f(n)} \cdot 3^j \in \bigoplus_{R_{\alpha_1}} (G_\gamma)_{\gamma < \alpha_1} \). Hence \(\bigoplus_{R_{\beta_1}} (G_\gamma)_{\gamma < \beta_1} \le_T \bigoplus_{R_{\alpha_1}} (G_\gamma)_{\gamma < \alpha_1} \).

The following lemma is used in the construction of a cofinal chain.

**Lemma 9.3.12.** For any real \(x\) and \(\alpha \in E_1\), if \( x \in L[G_\alpha] \) then there is a \(\beta \ge \alpha\) in \( E_1 \) such that \( x \le_T (\bigoplus_{R_\beta} (G_\gamma)_{\gamma < \beta})^\beta \).

Proof. Note that for any \(\alpha < \omega_1\), \( L[G_\alpha] = L[(\bigoplus_{R_\alpha} (G_\gamma)_{\gamma < \alpha})] \) since \( R_\alpha \in L \). Suppose that \( x \in L[G_\alpha] \). There is a \(\beta_1 \ge \alpha\) in \( E_1 \) such that \( x \in L_{\beta_1} [(\bigoplus_{R_\alpha} (G_\gamma)_{\gamma < \alpha})] \). By Lemma 9.3.11, \(\bigoplus_{R_\alpha} (G_\gamma)_{\gamma < \alpha} \le_T \bigoplus_{R_{\beta_1}} (G_\gamma)_{\gamma < \beta_1} \). Thus \( x \in L_{\beta_1} [(\bigoplus_{R_{\beta_1}} (G_\gamma)_{\gamma < \beta_1})] \). Since \(\beta_1 < \omega_1\), by relating Theorem 3.7.1 to \(\bigoplus_{R_{\beta_1}} (G_\gamma)_{\gamma < \beta_1} \) we have \( x \) to be \( A^1 \) in \(\bigoplus_{R_{\beta_1}} (G_\gamma)_{\gamma < \beta_1} \). Hence there is a \(\beta_2 \ge \beta_1\) below \(\omega_1^{\bigoplus_{R_{\beta_1}} (G_\gamma)_{\gamma < \beta_1}}\) such that \( x \le_T (\bigoplus_{R_{\beta_1}} (G_\gamma)_{\gamma < \beta_1})^{(\beta_2)} \). By Lemma 9.3.11 again, \( x \le_T (\bigoplus_{R_{\beta_1}} (G_\gamma)_{\gamma < \beta_1})^{(\beta_1)} \). Then \(\beta_2\) is the required \(\beta\).

In \( L[G] \), if \(\alpha \in E_1\) let \( x_\alpha^G = (\bigoplus_{R_\alpha} (G_\gamma)_{\gamma < \alpha})^{(\alpha)} \), and let \( r_\alpha \) be the canonical \(\text{P}_{\aleph_1}\)-name of \( x_\alpha^G \). Let

\[
A = \{z \mid (\exists \alpha \in E_1) (z \le_T r_\alpha^G) \}.
\]

Obviously \( A \) is a chain of Turing degrees in \( L[G] \). Set

\[
N = (\text{HOD}(\text{TC}([A])))^{L[G]}.
\]

where \(\text{TC}([A]) \in L[G] \) is the transitive closure of \( [A] \).

**Lemma 9.3.13.** For any \(\alpha < \omega_1\), (i) \(\text{P}_{\alpha}\) preserves cardinals; (ii) \( G_{\alpha} \) is \(\text{P}_{\alpha}\)-generic over \( L \); (iii) \( A \in \mathbb{N} \) is a cofinal chain of Turing degrees of order type \(\omega_1 \); (iv) \( (2^\omega)^{L[G]} = (2^\omega)^{\mathbb{N}} \).

Proof. (i) follows from Theorem 6.11.1 and (ii) from Theorem 6.1.9, while (iv) is an immediate consequence of (iii). We prove (iii). Given \( x \in L[G] \), there is an ordinal \(\alpha < \omega_1 \) such that \( x \in L[G_\alpha] \). Then there is a countable ordinal \(\alpha_1 \ge \alpha \) such that \( x \in L_{\alpha_1} [G_\alpha] \). By Lemma 9.3.12, for any \(\beta \ge \alpha_1\) in \( E_1 \), \( x \le_T (\bigoplus_{R_\beta} (G_\gamma)_{\gamma < \beta})^{(\beta)} \). Thus \( x \le_T x_\beta^G \).

Hence \(\mathbb{N}\) is a cardinal preserving extension of \( L \) satisfying \(\text{ZF}^+\)-"There exists a cofinal chain of Turing degrees". If we take \(\mathbb{N}' = \text{HOD}((G_\alpha \mid \alpha < \omega_1))\), then in \(\mathbb{N}'\) there is no well-ordering of \( 2^\omega \) by the proof of Theorem 6.2.15. However, to apply the argument for \(\mathbb{N}\), additional precaution is required to preserve the name of \( A \). For this purpose, we work with a subset of permutations of \(\omega_1\).

If \(\pi\) is a permutation of \(\omega_1\), let \(\text{spt}(\pi) = \{ \alpha < \omega_1 \mid \pi(\alpha) \neq \alpha \}\). Let \(H_0\) be the set of all permutations \(\pi\) of \(\omega_1\) with \(|\text{spt}(\pi)| < \omega\), and set

\[
H = \{ \pi \in H_0 \mid (\forall \alpha < \omega_1)(\pi(\alpha) < \alpha + \omega) \}.
\]

For each \(\pi \in H\), let \(\hat{\pi}\) be the permutation of \(L^{\aleph_1}\) induced by \(\pi\). Let \(B\) be the set of \(\mathbf{P}_{\aleph_1}\)-names of reals, and define

\[
\hat{A} = \{ (\tau, p) \in B \times \mathbf{P}_{\aleph_1} \mid (\exists \alpha \in E_1)(p \Vdash (\tau =_T \tau_\alpha)) \}.
\]

**Lemma 9.3.14.** If \(\pi \in H\) and \(\alpha \in E_1\) then \(\Vdash \tau_\alpha = \hat{\pi}(\tau_\alpha)\).

Proof. Note that the canonical name \(\dot{\alpha}\) of \(\alpha\) is invariant under \(\pi\), and \(R_\gamma\) is definable in \(\alpha\) as \(L\) is the minimal inner model. Then for any \(\mathbf{P}_{\aleph_1}\)-generic \(G\), \(\tau_\alpha^G\) and \(\hat{\pi}(\tau_\alpha)^G\) differ at most finitely many columns. The lemma follows immediately.

**Corollary 9.3.15.** If \(\pi \in H\), then \(\emptyset \Vdash \hat{A} = \hat{\pi}(\hat{A})\).

Hence the permutations in \(H\) are sufficient to show

\[
\mathbb{N} \Vdash \text{``There is no well-ordering of } 2^\omega\text{''}.
\]

By Proposition 9.3.7, \(\mathbb{N} \Vdash \neg \text{CH}\) and this completes the proof of Theorem 9.3.8.

### 9.3.4 Exercises

- **Exercise 9.3.1.** Prove Lemma 9.3.2.
- **Exercise 9.3.2** (Kunen). Prove that if there is a well-ordering of the Turing degrees, then there is a well-ordering of \(2^\omega\).
- **Exercise 9.3.3** (Wang, Wu and Yu [168]). Prove that in the proof of Theorem 9.3.8, we may assume \(\mathbb{M} \Vdash \text{ZFC} + \text{CH} + \omega_1 = (\omega_1)^L\).
- **Exercise 9.3.4.** Prove that there is a model \(\mathbb{M}\) of ZF in which no set of reals has exactly one representative from each Turing degree, and in which there is a thin set \(A\) where \(2^\omega \setminus A\) is also thin.

## 9.4 \(\omega\)-homogeneity of the Turing degrees

**Definition 9.4.1.** \(\langle \mathscr{D}, \le \rangle\) is \(\omega\)-homogeneous if for any two \(n+1\)-tuples \((\mathbf{a}_0, \dots, \mathbf{a}_n)\) and \((\mathbf{b}_0, \dots, \mathbf{b}_n)\) in \(\mathscr{D}\), if \(\langle \mathscr{D}, \le, \mathbf{a}_0, \dots, \mathbf{a}_n \rangle \equiv \langle \mathscr{D}, \le, \mathbf{b}_0, \dots, \mathbf{b}_n \rangle\) then there is an automorphism \(\pi : \mathscr{D} \to \mathscr{D}\) such that \(\pi(\mathbf{a}_i) = \mathbf{b}_i\) for each \(i \le n\).

Slaman and Woodin [144] showed:

**Theorem 9.4.2.** The \(\omega\)-homogeneity of \(\langle \mathscr{D}, \le \rangle\) is independent of ZFC.





我们称一个函数 $f : 2^\omega \to 2^\omega$ 展示了一个自同构 $\pi : (\mathscr{P}, \le) \to (\mathscr{P}, \le)$，如果对于每个图灵度 $\mathbf{x}$ 和实数 $x \in \mathbf{x}$，都有 $f(x) \in \pi(\mathbf{x})$。接下来的两个结果用于定理 9.4.2，且不作证明。

### 定理 9.4.3.
每个自同构 $\pi : (\mathscr{P}, \le) \to (\mathscr{P}, \le)$ 都由一个算术函数 $f : 2^\omega \to 2^\omega$ 展示。

如果 $R$ 是某个 $n$ 上 $(2^\omega)^{n+1}$ 的度不变关系，那么它在度上诱导出一个关系 $\bar{R}$，使得 $(x_0, \dots, x_n) \in \bar{R} \Leftrightarrow (\exists x_0) \dots (\exists x_n)(x_0 \in x_0 \land \dots \land x_n \in x_n \land (x_0, \dots, x_n) \in R)$。为简化起见，我们将 $\bar{R}$ 与 $R$ 识别。

### 定理 9.4.4.
对于任何在 $\mathscr{P}$ 上由 $2^\omega$ 上的度不变解析关系诱导的关系 $R$，如果 $R$ 在 $\mathscr{P}$ 的任何自同构下不变，那么 $R$ 在 $(\mathscr{P}, \le)$ 中可定义。

我们现在证明定理 9.4.2。

### 引理 9.4.5.
如果 $V = L$，那么 $(\mathscr{P}, \le)$ 是 $\omega$-齐次的。

证明。根据命题 4.4.2，$<_1$ 是 $2^\omega$ 的一个 $\Delta^1_2$ 良序。由 $<_1$ 诱导的 $n + 1$ 元组的字典序意味着对于每个 $n$，存在 $(2^\omega)^{n+1}$ 的一个 $\Delta^1_2$ 良序 $<_{n+1}$。

对于 $m < \omega$ 和 $k \le n$，令 $R_{m,k} \subseteq (2^\omega)^{n+1}$ 满足
\[
(x_0, \dots, x_n) \in R_{m,k} \Leftrightarrow k \le n \land \\
(\exists y_0) \dots (\exists y_n)((y_0, \dots, y_n) \text{ 是 } <_{n+1}\text{-最小的，使得} \\
(\exists \pi)(\forall i \le n)(\pi : (\mathscr{P}, \le) \to (\mathscr{P}, \le) \text{ 是一个自同构 } \land \pi(y_i) = x_i \land m \in y_k)).
\]

可以直接验证 $R_{m,k}$ 是度不变的，因此诱导出在 $\mathscr{P}$ 上在任何自同构下不变的关系。根据定理 9.4.3，$R_{m,k}$ 也是解析的。因此根据定理 9.4.4，$R_{m,k}$ 在 $(\mathscr{P}, \le)$ 中可定义。

假设 $(\mathscr{P}, \le, a_0, \dots, a_n) \equiv (\mathscr{P}, \le, b_0, \dots, b_n)$。那么对于每个 $m$ 和 $k \le n$，都有 $R_{m,k}(a_0, \dots, a_n) \Leftrightarrow R_{m,k}(b_0, \dots, b_n)$。对于这样的 $k$，定义 $y_k$ 使得 $m \in y_k$ 当且仅当 $R_{m,k}(a_0, \dots, a_n)$。根据 $R_{m,k}$ 的定义，存在自同构 $\pi_0$ 和 $\pi_1$，使得对于每个 $k \le n$，$\pi_0(y_k) = x_k$ 且 $\pi_1(y_k) = b_k$。那么 $\pi_1 \circ \pi_0^{-1}$ 是 $(\mathscr{P}, \le)$ 和 $(\mathscr{P}, \le)$ 之间的一个自同构，且 $\pi_1 \pi_0^{-1}(a_k) = b_k$，这意味着 $(\mathscr{P}, \le)$ 是 $\omega$-齐次的。

我们用以下引理完成定理 9.4.2 的证明。

### 引理 9.4.6.
如果 $V = L[g]$，其中 $g$ 是一个 Cohen 通用实数，那么 $(\mathscr{P}, \le)$ 不是 $\omega$-齐次的。

证明。令 $g = g_0 \oplus g_1$。我们留给读者验证 $(g_0, g_1)$ 是产品 Cohen 强迫 $\mathbb{C} \times \mathbb{C}$ 上的一对通用实数。然后根据定理 9.4.3，$(\mathscr{P}, \le)$ 上没有将 $g_0$ 送到 $g_1$ 的自同构。

现在让 \(\varphi\) 成为一个公式，使得 \((L[\mathbf{g}], \in) \models (L[\langle g_0, g_1 \rangle], \in) \models (\langle \mathscr{D}, \le \rangle \equiv \varphi(\mathbf{g}_0))^\wedge$。那么存在一个条件 $(p_0, p_1) \in 2^{<\omega} \times 2^{<\omega}$，使得 $[p_0] = [p_1]$、$(p_0, p_1) < (\mathbf{g}_0, \mathbf{g}_1)$ 且 $(p_0, p_1) \Vdash (\langle \mathscr{D}, \le \rangle \equiv \varphi(\mathbf{g}_0))^\wedge$。显然存在一个自同构 \(\tau : \mathbb{C} \times \mathbb{C} \to \mathbb{C} \times \mathbb{C}$，使得 \(\tau((p_0, p_1)) = (p_1, p_0)$ 且 \(\tau(\mathbf{g}_0) = \mathbf{g}_1$。根据命题 6.1.17，$(p_1, p_0) \Vdash (\langle \mathscr{D}, \le \rangle \equiv \varphi(\mathbf{g}_1))^\wedge$。那么 $(L[\langle \mathbf{g}_1, \mathbf{g}_0 \rangle], \in) \models (\langle \mathscr{D}, \le \rangle \equiv \varphi(\mathbf{g}_1))^\wedge$。然而，$L[\langle \mathbf{g}_1, \mathbf{g}_0 \rangle] = L[\langle \mathbf{g}_0, \mathbf{g}_1 \rangle] = L[\mathbf{g}]$，因此 $(L[\mathbf{g}], \in) \models (\langle \mathscr{D}, \le \rangle \equiv \varphi(\mathbf{g}_1))^\wedge$。故 $(\mathscr{D}, \le)$ 不是齐次的。

## 9.5 一些一般独立性结果

关于图灵度主题的一般参考，参见 Lerman [82]。令 \(\mathcal{L}(\le)\) 为偏序语言。\(\mathcal{L}(\le)\) 是集合论语言中可定义的集合。此外，$(\mathscr{D}, \le)$ 和关系 "\((\mathscr{D}, \le) \models \varphi\)" 都可以被视为集合论语言中的可定义集合。我们用一个数 "\(\ulcorner \varphi \urcorner\)" 对 \(\mathcal{L}(\le)$ 中的每个公式 \(\varphi\) 进行编码。

令

\(\text{Th}_{\exists_1}(\mathscr{D}, \le) = \{ \ulcorner \varphi \urcorner \mid \varphi \text{ 是 } \mathcal{L}(\le)$ 中的一个 } \Sigma_2\text{-句子 } \wedge (\mathscr{D}, \le) \models \varphi \}$。

Lerman 和 Shore [131] 证明：

### 定理 9.5.1.
集合 \(\text{Th}_{\exists_1}(\mathscr{D}, \le)$ 是递归的。

因此，集合 \(\text{Th}_{\exists_1}(\mathscr{D}, \le)$ 可由一个 \(\Sigma^0_1$-公式 \(\psi_0$ 和一个 \(\Pi^0_1$-公式 \(\psi_1$ 定义。由此可知，对于任何 \(\Sigma_2$-句子 \(\varphi$，

\(\text{ZFC} \vdash (\mathscr{D}, \le) \models \varphi \leftrightarrow \psi_0(\ulcorner \varphi \urcorner)$

和

\(\text{ZFC} \vdash (\mathscr{D}, \le) \models \neg \varphi \leftrightarrow \neg \psi_1(\ulcorner \varphi \urcorner)$。

因为对于任何 \(\Sigma^0_1$-公式 \(\psi(u)$ 和自然数 \(n$，

\(\text{ZFC} \vdash \psi(n) \leftrightarrow (\omega, \le, +, \cdot, 0, 1) \models \psi(n)$，

（参见 [145]），对于任何 \(\Sigma_2$-句子 \(\varphi$，要么

\(\text{ZFC} \vdash (\mathscr{D}, \le) \models \varphi$

要么

\(\text{ZFC} \vdash (\mathscr{D}, \le) \models \neg \varphi$。

因此我们有以下结论。

### 推论 9.5.2.
对于 \(\mathcal{L}(\le)$ 中的任何 \(\Sigma_2$-句子 \(\varphi\)，"\((\mathscr{D}, \le) \models \varphi\)" 或 "\((\mathscr{D}, \le) \models \neg \varphi\)" 在 ZFC 中可证。

显然集合 \(\text{Pr} = \{ \ulcorner \varphi \urcorner \mid \text{ZFC} \vdash (\mathscr{D}, \le) \models \varphi \}$ 是 r.e. 的。图灵度理论的复杂性由 Simpson [139] 确立：

### 定理 9.5.3.
ZFC 证明存在一个递归双射 $f : \omega \to \omega$，使得对于任何 $n$，$n \in \ulcorner \varphi \urcorner \langle \mathscr{D}, \le \rangle \vDash \varphi$ 当且仅当 $f(n) \in \ulcorner \varphi \urcorner \langle \omega, 2^\omega, +, \cdot, \subseteq \rangle \vDash \psi \rangle$，其中 \(\psi\) 是二阶算术语言中的一个公式。

因此 ZFC 证明集合 $\ulcorner \varphi \urcorner \langle \mathscr{D}, \le \rangle \vDash \varphi$ 不是解析的。由此可知，对于任何 $\mathsf{M} \vDash \mathsf{ZFC}$，我们有 $\mathsf{Pr} \vdash \ulcorner \varphi \urcorner \vdash \mathsf{M} \vDash \ulcorner \langle \mathscr{D}, \le \rangle \vDash \varphi \urcorner$。这导出以下结论。

### 推论 9.5.4.
对于任何 $\mathsf{M} \vDash \mathsf{ZFC}$，存在一个句子 $\varphi$，使得 $\ulcorner \varphi \urcorner \in \ulcorner \psi \urcorner \vdash \mathsf{M} \vDash \ulcorner \langle \mathscr{D}, \le \rangle \vDash \psi \urcorner \vdash \mathsf{Pr}$。

令 $\mathsf{M} \vDash \mathsf{ZFC}$ 和 $\varphi$ 如上所述。由于 $\mathsf{ZFC} \vdash \ulcorner \langle \mathscr{D}, \le \rangle \vDash \varphi \urcorner$，存在一个模型 $\mathsf{N} \vDash \mathsf{ZFC}$，使得 $\mathsf{N} \vDash \ulcorner \langle \mathscr{D}, \le \rangle \vDash \neg \varphi \urcorner$。因此陈述 $\ulcorner \langle \mathscr{D}, \le \rangle \vDash \varphi \urcorner$ 独立于 ZFC。这个论证暗示了存在一个在 ZFC 中不可证的句子 $\varphi$，但并未提供关于 $\varphi$ 的任何信息。以下提供了更多信息：根据推论 4.4.1，陈述“每个实数都是可构的”是 $\Pi_2^1$。因此存在 $\mathcal{L}(\in)$ 中的一个句子 $\varphi$，使得 $\ulcorner \langle \mathscr{D}, \le \rangle \vDash \varphi \urcorner$ 当且仅当每个实数都是可构的。因此陈述 $\ulcorner \langle \mathscr{D}, \le \rangle \vDash \varphi \urcorner$ 独立于 ZFC。然而，该论证的一个弱点是句子 $\varphi$ 非常复杂，不一定被视为“自然”，并且高度依赖于编码方案。目前不知道是否存在 $\mathcal{L}(\in)$ 中一个独立于 ZFC 的“自然”句子。





## 10 超度的刚性与双可解释性

令 $(\mathscr{P}_h, \le)$ 表示超算归约下的偏序 $\le$ 意义下的超度结构。同图灵度 $(\mathscr{P}, \le_T)$ 一样，超度在连接算子 $\cup$ 意义下构成一个上半格，其中若 $x$ 和 $y$ 的超度分别为 $\mathbf{a}$ 和 $\mathbf{b}$，则 $x \oplus y$ 的超度为 $\mathbf{a} \cup \mathbf{b}$。注意 $\cup$ 可用 $\le$ 定义。$\mathscr{P}$ 或 $\mathscr{P}_h$ 到自身的一个映射若是双射且保持 $\le$，则称为一个 *自同构*。递归论中的一个主要未解问题是询问恒等映射是否是图灵度的唯一自同构，即图灵度是否 *刚性*。Slaman 和 Woodin ([141] 和 [144]) 使用精巧的元数学论证，证明了关于 $(\mathscr{P}, \le_T)$ 的若干显著结果，包括该结构至多有可数个非平凡自同构的定理（实际上，度 $\ge \mathbf{0}'$ 在任何自同构下均不变），以及超度是刚性的。在本章中，我们呈现了 Shore [133] 关于后者的一个更“初等”的证明。$(\mathscr{P}_h, \le)$ 与二阶算术的双可解释性作为刚性的应用得出（参见 § 10.3）。

#### 10.1 将格嵌入超度

回顾，若偏序集 $(\mathscr{C}, \le)$ 中任意两个元素 $c, c' \in \mathscr{C}$ 均有最小上界和最大下界，分别记作 $c \cup c'$ 和 $c \cap c'$，则称其为一个 *格*。若格的元素（通过某种有效编码）被递归枚举，则称该格是递归表示的。若在 $\le$ 意义下的偏序中，关系 $\le, \nleq$ 和算子 $\cup, \cap$ 均为偏递归，则称其为偏格。下一个定理可追溯至 Jónsson [61]（另见 Lerman [81] 和 Shore [132]）。

**定理 10.1.1.** *假设* $\mathscr{C} = \{c_i\}_{i < \omega}$ *是带有最小元素* $c_0$ *的递归表示偏格的一个枚举。存在一组一致递归的函数数组* $\langle f_n \in \omega^\omega \mid n < \omega \rangle$ *，使得对所有* $i, j, k, m$ *和* $n$ *，*

- (i) $f_n(0) = 0$;
- (ii) $c_i \le c_j \Rightarrow [\exists d, e (f_d(i) = f_e(i) \land f_d(i) \neq f_e(i))]$;
- (iii) $c_i \cup c_j = c_k \Rightarrow [\exists d, e (f_d(i) = f_m(i) \land f_d(j) = f_m(j) \Rightarrow f_n(k) = f_m(k)];$
- (iv) $c_i \cup c_j = c_k \Rightarrow f_m(i) = f_m(i) \land f_n(j) \Rightarrow f_m(i) = f_m(k)];$
- (v) $c_i \cap c_j = c_k \land f_n(k) = f_m(k) \Rightarrow (\exists d_1, d_2, d_3)[f_n(i) = f_{d_1}(i) \land f_n(i) = f_{d_1}(i) \land f_{d_2}(i) = f_{d_3}(i) \land f_{d_3}(i) = f_{d_3}(i)];$

Proof. Define

$f^*_{2j+1}(i) = \begin{cases} 0 & i = 0, \\ 2^{j+1} & i > 0. \end{cases}$

and

$$f^*_{2j}(i) = \begin{cases} 0 & i = 0, \\ 2^{j+1} & c_i \le c_j, \\ 2^j & c_i \nleq c_j. \end{cases}$$

我们使用 $\{f_i^*\}_{i \in \omega}$ 作为基础来生成数组 $\{f_n\}_{n \in \omega}$。可以直接验证，(i)--(v) 对每个 $f_i^*$ 都成立。对于任何已生成且满足 (v) 假设的两个函数 $f, \hat{f}$，我们定义函数 $\hat{f}_{d_1}, \hat{f}_{d_2}, \hat{f}_{d_3}$ 如下：若 $c_i \le c_j$，则令 $\hat{f}_{d_1} = \hat{f}_{d_2} = \hat{f}_{d_3} = \hat{f}$，此时 (v) 成立。若 $c_i \nleq c_j$，设 $a_1, a_2, a_3, a_4$ 为不在 $f$ 和 $\hat{f}$ 值域中的数。定义

$$\hat{f}_{d_1}(s) = \begin{cases} f(s) & c_s \le c_i, \\ a_1 & c_s \nleq c_i. \end{cases}$$ $$\hat{f}_{d_2}(s) = \begin{cases} f(s) & c_s \le c_j, \\ a_2 & c_s \le c_i \land c_s \notin c_j, \\ a_3 & \text{Otherwise.} \end{cases}$$ $$\hat{f}_{d_3}(s) = \begin{cases} \hat{f}(s) & c_s \le c_j, \\ a_2 & c_s \le c_i \land c_s \notin c_j, \\ a_4 & \text{Otherwise.} \end{cases}$$

我们留给读者验证，(v) 对 $f, \hat{f}$ 成立，且加入这三个新函数后，(i)--(iv) 仍然有效。通过此过程生成的函数集合是定理所规定的递归数组 $\{f_n\}_{n \in \omega}$。

科恩强迫法（§ 5.2）的一个改编允许将一个递归表示的格嵌入超度中。

**定理 10.1.2.** 设 $\mathcal{C} = \{c_i\}_{i < \omega}$ 为带有 0 的递归偏格，且 $\{f_n\}_{n < \omega}$ 为定理 10.1.1 给出的 $\mathcal{C}$ 的递归表示。设 $\mathfrak{A}(\omega_1^{\text{CK}})$ 为 § 5.1 为分层分析层次定义的结构。若 $g$ 是在 $\mathfrak{A}(\omega_1^{\text{CK}})$ 上的科恩泛则，则存在一组集合 $\{h_i\}_{i < \omega}$，使得 $h_i \le_T g$ 且将 $c_i$ 映射到 $h_i$ 的超度的映射是 $\mathcal{C}$ 在 $\mathscr{D}_h$ 中的一个嵌入，保持 $\le, \vee, \cup$ 和 $\cap$。

**证明。** 此处考虑的科恩强迫概念定义在 Baire 空间 $\omega^\omega$ 上，而非如 § 5.2 中所定义的 Cantor 空间 $2^\omega$ 上。一个条件是形式为 $\sigma(m) = n$ 的一致关系集的有限集合。泛则集 $g$ 于是是 $\omega^\omega$ 中的一个元素的函数，满足 $\omega_1^{\text{CK}} = \omega_1^{\text{CK}, g}$。另请回顾，根据推论 5.2.6 (ii)，若 $g$ 是科恩泛则且 $h \le_T g$，则对于某个递归序数 $\gamma$，有 $h \le_T g \oplus \emptyset'$。

对每个 $i$，令 $h_i(n) = f_{g(n)}(i)$。首先，根据定理 10.1.1 (i)，对所有 $n$ 均有 $h_0(n) = f_{g(n)}(0) = 0$，因此 $0 \in \mathcal{C}$ 被映射到一个递归集。假设 $c_i \le c_j$。对每个 $n$，寻找最小的 $m$ 使得 $f_m(n) = h_i(n) = f_{g(n)}(j)$。注意这样的 $m$ 必须存在，因为 $g(n)$ 是一个候选。于是 $f_m(i) = f_{g(n)}(i) = h_i(n)$。由于 $\{f_n\}_{n < \omega}$ 是一致递归的，我们实际上有 $h_i \le_T h_j$，表明该映射保持序。

现在假设 $c_i \cup c_j = c_k$。要计算 $h_k(n)$，即 $f_{g(n)}(k)$，递归地找到一个 $m$ 使得 $f_m(i) = h_i(n) = f_{g(n)}(i)$ 且 $f_m(j) = h_j(n) = f_{g(n)}(j)$。根据定理 10.1.1 (iv)，有 $f_m(k) = f_{g(n)}(k) = h_k(n)$。因此，当连接定义时，该嵌入保持连接。

我们利用 $g$ 的泛则性来论证 $\vee$ 和 $\cap$ 在嵌入下被保持。假设 $c_i \nleq c_j$。根据定理 10.1.1 (iii)，存在 $m, n$ 使得 $f_m(i) = f_n(j)$ 且 $f_m(i) \neq f_n(i)$。若 $h_i \leq h_j$，则存在 $k \in \omega$、一个数 $e$ 和一个条件 $p$，使得
$p \Vdash h_i = \Phi_{e_i}^{h_j}$。

设 $q$ 是扩展 $p$ 的条件，包含不在 $p$ 域中的 $d$，使得 $q \Vdash g(\bar{d}) = \bar{n}$，且 $q$ 决定 $\Phi_{e_i}^{h_j}(\bar{d})$ 的值。设 $q'$ 与 $q$ 类似，只是将 $n$ 替换为 $m$。由于 $q$ 和 $q'$ 的泛则扩展仅在 $d$ 处取值不同，对 $h_j$ 具有相同的解释，因此两个条件强迫 $\Phi_{e_i}^{h_j}(\bar{d})$ 取相同的值。于是
$q \Vdash \Phi_{e_i}^{h_j}(\bar{d}) = f_n(i) \text{ 且 } q' \Vdash \Phi_{e_i}^{h_j}(\bar{d}) = f_m(i)$。

这与我们对 $m$ 和 $n$ 的选择矛盾。因此 $c_i \nleq c_j$ 蕴含 $h_i \nleq h_j$。

最后需要考虑的情况是 $c_i \cap c_j = c_k$。根据嵌入下序的保持，有 $h_i \cap h_j \leq h_k$。假设 $f \nleq h_i$ 且 $f \nleq h_j$，目标是证明 $f \nleq h_k$。设 $p$ 为被 $g$ 扩展的条件，使得
$p \Vdash f = \Phi_{e_0}^{h_j} = \Phi_{e_1}^{h_j}$。

其中 $m, n \in \omega$ 和 $e_0, e_1$。对于给定的 $u$，使用 $h_k$ 找到扩展 $p$ 的条件 $q$，使得 $q$ 强迫 $\Phi_{e_0}^{h_j}(i)$ 和 $\Phi_{e_1}^{h_j}(i)$ 取（必然相同的）值，从而对 $q$ 域中的每个 $d$ 均有 $h_k(d) = f_{g(d)}(k)$（注意，对 $q$ 域中的每个 $d$ 均有 $f_{g(d)}(k) = f_{g(d)}(k)$）。我们声称，这是一个在 $h_k$ 中超算地计算 $f$ 的算法。

由于分级公式的强迫关系是超算的，且寻找满足上述陈述后半部分的条件的搜索是递归的，$q$ 可在 $h_k$ 中超算地计算。我们证明，$\Phi_{e_i}^{h_j}(i)$ 的值是 $f(u)$ 的正确值。为求矛盾，假设 $v \neq w$ 是数，使得
$\Phi_{e_0}^{h_j}(u) = \Phi_{e_1}^{h_j}(u) = w \text{ 且 } q \Vdash \Phi_{e_0}^{h_j}(v) = \Phi_{e_1}^{h_j}(v) = v$。

根据 $g$ 的泛则性，存在比 $p$ 更强且被 $g$ 扩展的条件 $r$，使得
$r \Vdash \Phi_{e_0}^{h_j}(u) = \Phi_{e_1}^{h_j}(u) = \bar{w}$。

如有必要，通过扩展域，我们可以假设 $q$ 和 $r$ 具有相同的域。于是对域中的每个 $d$ 均有 $f_{g(d)}(k) = h_d(k) = f_{g(d)}(k)$。根据定理 10.1.1 (v)，对于每个这样的 $d$，存在数 $d_1, d_2$ 和 $\bar{d}_3$，使得对 $f_{g(d)}$ 和 $f_{f(d)}$ 满足 (v) 中的结论。对 $l = 1, 2, 3$，设 $q_l$ 为使得 $q_l(d) = \bar{d}_l$ 的条件，并令若 $d$ 不在 $q_l$ 的域中则 $g_l(d) = g(d)$，否则等于 $q_l(d)$。于是 $g_1$


### 10.2 超度的刚性

令 $x \le \omega$。刚性证明的下一步是定义一个带有有限参数集的部分格 $\mathcal{C}_x$，该参数集生成 $\omega$ 的一个副本。此外，$x$ 将在 $\mathcal{C}_x$ 中被编码。对于预期的应用，$x$ 中成员和非成员的编码将仅涉及 $\le$ 和 $u$ 的正公式，即否定符号 $-$ 和交符号 $\wedge$ 不出现在定义 $x$ 中的 $n$ 或 $n \notin x$ 的公式中。这是一个关键手段，用于确保在任何将 $\mathcal{C}_x$ 嵌入到 $\mathcal{D}_h$ 且保持 $\le$ 和 $u$ 的嵌入 $f$ 中，$x$ 总是关于定义部分格的参数是高算术的（以下引理 10.2.1 (iv) 的一个推论）。

首先，令 $d_0, e_0, e_1, f_0, f_1$ 为 $\mathcal{C}_x$ 的元素，它们将是 $\{d_n \mid n < \omega\}$ 的生成元，旨在作为 $\omega$ 的一个副本。对于每个 $n < \omega$，令：

- $(d_{2n} \cup e_0) \cap f_1 = d_{2n+1}$
- $(d_{2n+1} \cup e_1) \cap f_0 = d_{2n+2}$

这些条件保证 $d_n$ 递归枚举。给定 $x \le \omega$，我们添加两个额外参数 $c_x$ 和 $c_x'$，并要求对 $n \in x$ 有 $d_n \le c_x$，对 $n \notin x$ 有 $d_n \cap c_x = 0$。我们还设定 $d_{2n+1} \le (d_{2n} \cup e_0)$、$d_{2n+1} \le f_1$ 且 $d_{2n+1} \neq 0$。为避免使用 $-$，最后的不等式可以通过引入两个进一步参数 $c$ 和 $c'$ 来满足，并要求在部分格中 $c' \neq 0$ 且对每个 $n$ 有 $c \cup d_n \ge c'$。如果对某个 $n$ 有 $u = d_n$，则 $u \neq 0$ 表示为 $c \cup u \ge c'$。

#### 引理 10.2.1. 令 $x \le \omega$。存在一个递归集 $\{p_n \mid n \in \omega\}$ 的正存在公式，仅涉及 $\le$、$u$ 以及参数 $c_x, c_x', c, c', d_0, e_0, e_1, f_0, f_1$，使得在上述定义的任何部分格 $\mathcal{C}_x$ 中，

- (i) $p_n(u) \leftrightarrow 0 \le u \le d_n$;
- (ii) $n \in x \leftrightarrow (\exists u)(p_n(u) \wedge u \le c_x)$;
- (iii) $n \notin x \leftrightarrow (\exists u)(p_n(u) \wedge u \le c_x)$;
- (iv) 在将 $\mathcal{C}_x$ 嵌入到 $\mathcal{D}_h$ 且保持 $\cap, \cup$ 和 $\le$ 的任何嵌入中，这些公式等价于 $\Pi_1^1$-公式（带有相关参数）。

证明。首先令 $\varphi_0(u)$ 为 $u = d_0$。递归定义 $\varphi_{2n+1}(u)$ 为

$(\exists w)(\varphi_{2n}(w) \land u \subseteq w \cup e_0 \land u \lesssim f_1 \land c \cup u \supseteq c')$

并令 $\varphi_{2n+2}(u)$ 为

$(\exists w)(\varphi_{2n+1}(w) \land u \subseteq w \cup e_1 \land u \lesssim f_0 \land c \cup u \supseteq c')$

假设 $\varphi_{2n+1}(u)$ 对 $u$ 成立。那么存在如所述的 $w$，使得通过归纳，$0 < w \le d_{2n}$。因此 $w \cup e_0 \subseteq d_{2n} \cup e_0$，从而 $d_{2n} \cup e_0 \subseteq f_1$。由于 $d_{2n+1} = (d_{2n} \cup e_0) \cap f_1$，故 $u \subseteq d_{2n+1}$。此外，$c' \subseteq c \cup u$ 确保 $u > 0$ 也成立，因此 (i) 对 $\varphi_{2n+1}$ 成立。$\varphi_{2n+2}$ 的论证类似。

我们将 (ii) 和 (iii) 的验证留给读者。最后，(iv) 从推论 3.7.4 得出。

#### 注释 10.2.2. 定理 10.1.2 可以相对于任何实数 x 进行相对化。部分格 $c_x$ 递归地在 x 中从参数 $d_0, e_0, e_1, f_0, f_1, c_x, c_+, c_-, c'$ 定义，使用 $\le, \cup, \cap$ 作为部分函数。然后，将 $c_x$ 嵌入到超度中的任何嵌入都将 $c_x$ 的 0 映射到 x。

现在固定一个实数 x。根据相对于 x 的定理 10.1.2，存在一个保持 $\le, \cup, \cap$ 和 $\neg$ 的嵌入 $f : c_x \to \mathscr{D}_h$，使得 $f(0_{c_x}) = x$。根据引理 10.2.1，x 和 $\omega \setminus x$ 都相对于以下表示的表达是 $\Pi^0_1$-可定义的：

$f(d_0) \cup f(e_0) \cup f(e_1) \cup f(f_0) \cup f(f_1) \cup f(c_x) \cup f(c) \cup f(c') \le f(1_{c_x})$.

因此 $x \le f(1_{c_x})$。

以下结果将用于证明 $(\mathscr{D}_h, \le)$ 与二阶算术的双可解释性。

#### 引理 10.2.3. 对于任意 x 和 y，$y \le_R x$ 当且仅当存在 $y_0, y_1 > x$ 使得 $y_0 \cap y_1 = x$ 且 $c_y$ 可以嵌入到 $[x, y_0]$ 和 $[x, y_1]$ 中，且最小元为 x。

证明。令 $g_0$ 和 $g_1$ 为相对于 x 的 Cohen 一般实数，使得 $(x \cup g_0) \cap (x \cup g_1) = x$。那么“仅当”方向立即从相对于 x 的定理 10.1.2 得出，取 $y_0 = x \cup g_0$ 和 $y_1 = x \cup g_1$。

对于另一方向，注意根据引理 10.2.1，$y \le y_0$ 且 $y \le y_1$。所以 $y \le x$。

我们现在准备证明本节的主定理。

#### 定理 10.2.4 (Slaman 和 Woodin [141], Shore [133]). 如果 $\pi : \mathscr{D}_h \to \mathscr{D}_h$ 是一个自同构，那么 $\pi$ 是恒等映射。

证明。令 x 为包含 x 作为元素的超度。令 $c_x$ 为由上述 $d_0, e_0, e_1, f_0, f_1$ 生成的格。令 $\hat{c}_x$ 为 $c_x$ 的一个不相交副本，并定义一个部分格 $\mathscr{P}_x$，它是 $c_x$ 和 $\hat{c}_x$ 的并集，使得 $0_{\mathscr{P}_x} = 1_{c_x} \cap 1_{\hat{c}_x}$ 且 $1_{\mathscr{P}_x} = 1_{c_x} \cup 1_{\hat{c}_x}$。根据相对于 x 的定理 10.1.2，存在一个将 $\mathscr{P}_x$ 嵌入到超度中的嵌入 f，使得 $f(0_{\mathscr{P}_x}) = x$。

假设 \(\pi : \mathscr{D}_h \to \mathscr{D}_h\) 是一个自同构，使得 \(\pi(\mathbf{x}) \neq \mathbf{x}\)。那么编码方案（参见注释 10.2.2）确保 \(\mathbf{x} \le \pi f(1_{\hat{c}_x})\) 且 \(\mathbf{x} \le \pi f(1_{\hat{c}_x})\)。由于 \(\mathbf{x} = f(0_{\hat{c}_x}) = f(1_{\hat{c}_x}) \cap f(1_{\hat{c}_x})\)，我们有 \(\pi(\mathbf{x}) = \pi(f(1_{\hat{c}_x}) \cap f(1_{\hat{c}_x})) = \pi(f(1_{\hat{c}_x})) \cap \pi(f(1_{\hat{c}_x}))\)，从而 \(\mathbf{x} \le \pi(\mathbf{x})$。与 \(\pi^{-1}$ 的类似论证表明 \(\pi(\mathbf{x}) \le \mathbf{x}$，从而 \(\pi(\mathbf{x}) = \mathbf{x}$，这产生了矛盾。

### 10.2.1 练习

- 练习 10.2.1. 证明定理 10.2.1 (ii) 和 (iii)。
- 练习 10.2.2. 证明如果 \(x \in L_{uf}\)，且 \(\pi : \mathscr{D}_h(\le \mathbf{x}) \to \mathscr{D}_h(\le \mathbf{x})\) 是一个同构，那么 \(\pi$ 是恒等映射。

## 10.3 双可解释性

图灵度中的双可解释性基本上表示，$\mathscr{D}$ 上的关系可定义当且仅当它在二阶算术中可定义。

虽然 $(\mathscr{D}, \le)$ 的双可解释性尚未确立，但我们在本节中表明它对超度成立。

#### 10.3.1 Slaman–Woodin 编码

Slaman 和 Woodin [14] 表明了图灵度上任何可数关系的（带参数的）可定义性。这是通过一种现在称为 Slaman–Woodin 编码的技术实现的。该技术适用于一系列度结构，包括超度，并且是证明 $(\mathscr{D}_h, \le)$ 与二阶算术双可解释性的关键。

#### 定理 10.3.1 (Slaman 和 Woodin [143]). 对于每个 $n < \omega$，存在超度语言中的一个公式 $\varphi_n$，使得对于任何可数的 n 元关系 $R \subseteq \mathscr{D}_h$，都存在 $\mathbf{g}_1, \dots, \mathbf{g}_m$ 使得 $(\mathbf{a}_1, \dots, \mathbf{a}_n) \in R \leftrightarrow (\mathscr{D}_h, \le) \models \varphi_n(\mathbf{a}_1, \dots, \mathbf{a}_n; \mathbf{g}_1, \dots, \mathbf{g}_m)$。

我们通过首先表明任何可数的超度反链在 $(\mathscr{D}_h, \le)$ 中可定义来建立此定理。设置如下：令 $A = \{\mathbf{a}_i \mid i < \omega\}$ 为一个反链，并令 $a_i$ 为超度 $\mathbf{a}_i$ 的一个实数，使得 $a_i$ 在其每个无限子集中都是递归的（注意，每个无限集合都与其有限初始段的（代码）集图灵等价）。令 $a \in \mathbf{a}$ 为 $A$ 的一个上界。




定义一个强迫概念 $\mathbf{P} = (\mathbf{P}, \le)$，使得每个 \(p \in \mathbf{P}\) 都是一个三元组 \((p_1, p_2, p_3)\)，其中 \(p_1, p_2 \in 2^{<\omega}\) 具有相同的长度（称为 \(p\) 的长度），\(p_3 \in \omega\)，并且对于 \(p, q \in \mathbf{P}\)，\(p \le q\) 当且仅当

- (i) 对于 \(j = 1, 2\)，\(q_j \ge p_j\)；
- (ii) \(q_3 \ge p_3\)；
- (iii) 对于所有 \(k \le p_3\)，对于所有 \(m \in a_k\)，如果 \((k, m)\) 在 \(q_1 \setminus p_1\) 的定义域中（因此也在 \(q_2 \setminus p_2\) 的定义域中），则 \(q_1((k, m)) = q_2((k, m))\)。

通过引入带秩变量 \(x^\alpha\)（其中 \(\beta < \alpha^+\)）、每个 \(i < \omega\) 的项 \(a_i\)、表示 \(a\) 的 \(a\) 以及表示从 \(\mathbf{P}\) 获得的通用实数 \(g_1\) 和 \(g_2\) 的 \(g_1, g_2\)，将二阶算术中的 Cohen 强迫语言（参见 § 5.2）相对于 \(a\) 进行相对化扩展。对于扩展语言中的公式 \(\phi\)，如同在第 5.2 节中一样定义 \(\mathbf{p} \Vdash \phi\)。我们留给读者验证，对于任何通用 \(g\)，都有 \(a_i^{\omega_g} = \omega_i^a\)。

设 \(g\) 为 \(\mathbf{P}\)-通用，其中 \(\mathbf{g}\) 为 \(j = 1, 2\) 时 \(g_j\) 的超算度，且 \(g_1 = \bigcup \{p_1 \mid (\exists p_2)(\exists p_3)((p_1, p_2, p_3) \in g)\}\) 以及 \(g_2 = \bigcup \{p_2 \mid (\exists p_1)(\exists p_3)((p_1, p_2, p_3) \in g)\}\)。计划是证明 \(A\) 是下式的最小解集：

\(\{x \in a \mid (\exists z)((z \subseteq x \cup g_1) \land (z \subseteq x \cup g_2) \land (z \notin x))\}.\)

**Lemma 10.3.2.** 设 \(g_1\) 和 \(g_2\) 如上。对于每个 \(k\)，存在一个实数 \(c_k\)，使得对于每个 \(j\) 都有 \(c_k \le_h a_k \oplus g_j\) 且 \(c_k \not\le_h a_k\)。

**Proof.** 设 \(p \in g\) 为满足 \(|p_1| > k\) 的一个条件。令 \(c_k = \{m \mid m \in a_k \land |p_1| < (k, m) \in g_1\}\)。显然 \(c_k \le_T a_k \oplus g_1\)。另外，根据 (iii)，我们有 \(c_k = \{m \mid m \in a_k \land |p_1| < (k, m) \in g_2\}\)，因此也有 \(c_k \le_T a_k \oplus g_2\)。注意 \(c_k \not\le_h a_k\)：一个简单的对角化方法表明，对于任何 \(x \le_h a\)，\(c_k\) 都不等于 \(x\)。所以 \(c_k \not\le_h a\)，从而 \(c_k \not\le_h a_k\)。

**Lemma 10.3.3.** 对于任何实数 \(x, z \le_h a\)，如果对于 \(j = 1, 2\) 都有 \(z \le_h x \oplus g_j\) 且 \(z \not\le_h x\)，那么存在某个 \(k\) 使得 \(x \ge_h a_k\)。

**Proof.** 固定带秩公式 \(\varphi_x, \varphi_z\)，使得 \(m \in x \Leftrightarrow \mathfrak{A}(\omega_1^a, a) \models \varphi_x(m)\) 且 \(m \in z \Leftrightarrow \mathfrak{A}(\omega_1^a, a) \models \varphi_z(m)\)。另外，对于 \(j = 1\) 和 \(2\)，令 \(\varphi_{x \oplus g_j}\) 满足 \(m \in z \Leftrightarrow \mathfrak{A}(\omega_1^a, a, g_j) \models \varphi_{x \oplus g_j}(m) \Leftrightarrow \mathfrak{A}(\omega_1^a, a, g) \models \varphi_{x \oplus g_j}(m)\)。注意 \(\varphi_{x \oplus g_j}\) 是用 \(\varphi_x\) 和 \(g_j\) 表示的。因此存在一个条件 \(p \in g\) 使得

\(p \Vdash (\forall m)(\varphi_x(m) \leftrightarrow \varphi_{x \oplus g_1}(m)) \land (\varphi_z(m) \leftrightarrow \varphi_{x \oplus g_2}(m)).\)

**Claim.** 存在无穷多个 \(m\) 以及条件 \(q^m, r^m > p\)，它们的公共长度至少为 \(m\)，使得 \(q^m \Vdash \varphi_{x \oplus g_1}(m)\) 且 \(r^m \Vdash \neg \varphi_{x \oplus g_1}(m)\)。

**Proof of Claim.** 否则，对于所有足够大的 \(m\)，对于所有长度至少为 \(m\) 的 \(q, r > p\)，\(q\) 和 \(r\) 不会对 \(\varphi_{x \oplus g_1}(m)\) 强迫不同的值。由于 \(x \le_h a\)，句子 \(\varphi_{x \oplus g_1}(m)\) 对每个 \(m\) 都有（相同的）秩小于 \(\omega_1^a\)，因此关系 \(\text{‘}q \Vdash \varphi_{x \oplus g_1}(m)\text{’}\) 在 \(x\) 中是超算的。但这意味着 \(z \le_h x\)，与假设矛盾。

因此，按 Claim 所述选择 \(q^m, r^m\)。注意 \(m \mapsto (q^m, r^m)\) 在 \(x\) 中是超算的。

我们从（最小的）\(i < |Q|\) 开始，使得 \(q_1^m\) 和 \(r_1^m\) 在 \(i\) 处不一致（如果存在的话）。通过首先将 \(q_1^m\) 在点 \(i\) 处的值改为与 \(r_1^m\) 一致，令 \(s_2(0) \mid [q_1^m]^2 = q_2^m\) 且 \(s_3(0) = q_3^m\)，然后扩展它以决定 \(\varphi_{x \oplus g_i}(m)\) 的值，来定义条件 \(s(0) = (s_1(0), s_2(0), s_3(0))\)。然后将 \(q_1^m, q_2^m\) 和 \(r_1^m, r_2^m\) 的定义域扩展到 \(s_1(0)\) 的定义域，使得这些定义域中的新点在值上与 \(s_1(0)\) 一致。将得到的条件称为 \(q^m(0)\) 和 \(r^m(0)\)。要么 \(s_1(0)\) 和 \(q_1^m(0)\) 在恰好一个点处不一致，\(s_2(0) = q_2^m(0)\)，且 \(s(0)\) 和 \(q^m(0)\) 对 \(\varphi_{x \oplus g_i}(m)\) 强迫不兼容的值，要么 \(s(0)\) 和 \(r^m(0)\) 强迫不兼容的值，并且它们之间的不一致点比 \(q^m\) 和 \(r^m\) 之间的更少。对于 \(q_1^m\) 和 \(r_1^m\)，我们执行相同的构造。通过归纳，依次定义 \(s(0), s(1), \dots\)，并得出存在一个 \(j\) 使得 \(s(j)\) 和 \(s(j+1)\) 在前两个分量中恰好有一个不一致点，并对 \(\varphi_{x \oplus g_i}(m)\) 强迫不兼容的值。

因此，我们可以假设 \(q^m\) 和 \(r^m\) 仅在一点 \((k, l)\) 处不同，即 \(q_1^m((k, l)) \neq r_1^m((k, l))\)。如果 \(k > p_3\) 或 \(l \notin a_k\)，则令 \(s = (s_1^m, r_2^m, q_3 + r_3)\)。那么 \(s \le p\)。这意味着我们可以将 \(p\) 扩展为一个通用 \(g\)，使得 \(g_1\) 和 \(g_2\) 在它们的公共点上分别与 \(q^m\) 和 \(r^m\) 具有相同的值。然而，这与对 \(p\) 的假设矛盾。

因此，存在无穷多对扩展 \(p\) 的条件，它们仅在一个 \((k, l)\) 处不同，其中 \(k \le p_3\) 且 \(l \in a_k\)，并按上述方式强迫不同的值。特别是，存在一个 \(k \le p_3\)，对于无穷多个这样的 \(l\) 满足此要求。如前所述，此处考虑的固定秩句子的强迫关系在参数 \(x\) 中是超算的，因此可以在 \(x\) 中超算地枚举一个包含在 \(a_k\) 中的无穷 \(l\) 集合。由于 \(a_k\) 在其每个无限子集中都是递归的，这个集合计算出 \(a_k\)。

因此 \(x \ge_h a_k\)，从而证明了该引理。

现在可以将度上的任意可数关系转换为一个反链，使得原始关系可以使用参数从反链中定义。

### 定理 10.3.1 的证明.

设 \(R\) 是超算度上的一个 \(n\)-元关系。设 \(\{\mathbf{a}_j \mid j < \omega\}\) 是所有 \(\le \mathbf{a}\) 的超算度的列表，其中 \(a_j \in \mathbf{a}_j\) 且 \(a \in \mathbf{a}\)。设 \(\{g_{i,j} \mid 1 \le i \le n \text{ 且 } j < \omega\}\) 是关于 \(a\) 互为 Cohen 通用的实数。这可以按照 §5.2 并使用前面描述的扩展语言来得到，将 \(g_{i,j}\) 取为单个通用 \(g\) 的适当列。根据练习 10.3.1，以下集合是超算度的反链：

\(S_i = \{g_{i,j} \mid j < \omega\}\);
\(T_i = \{\mathbf{a}_j \mid j < \omega\}\);
\(U = \{\mathbf{g}_{1,j}, \dots, \mathbf{g}_{n,j} \mid R(\mathbf{a}_j, \dots, \mathbf{a}_j)\}\)。

那么 $S_i, T_i$ 和 $U$ 在 $(\mathscr{P}_n, \le)$ 中是可定义的。对于任何 $\mathbf{x}_1, \dots, \mathbf{x}_n \le \mathbf{a}$，$R(\mathbf{x}_1, \dots, \mathbf{x}_n)$ 成立当且仅当对于每个 $i \in [1, n]$，存在 $\mathbf{y}_i \in S_i$ 和 $\mathbf{z}_i \in T_i$ 使得 $\mathbf{y}_1 \cup \cdots \cup \mathbf{y}_n \in U$ 且 $\mathbf{x}_i \cup \mathbf{y}_i = \mathbf{z}_i$。因此，\(R\) 限制在 \(\mathbf{a}\) 以下的超算度上是可定义的，从而完成了定理 10.3.1 的证明。

### 10.3.2 对 PA 扩展标准模型的编码

考虑由一元谓词 \(x\) 扩展的 Peano 算术的标准模型 \(\langle \omega, x, <, +, \cdot, 0, 1 \rangle\)。我们可以将其表示为度上的关系。设 \(\langle \mathbf{d}_n \rangle_{n < \omega}\) 是一个超算度的可数序列。我们将 \(\mathbf{d}_n\) 解释为数 \(n\)，并以显而易见的方式在 \(\langle \mathbf{d}_n \rangle_{n < \omega}\) 的有限子集上定义算术关系和函数。从这些出发，可以在 \(\langle \mathbf{d}_n \rangle_{n < \omega}\) 上定义一个可数关系 \(R^*\)，将其变为（算术标准模型的一个副本）带有一个表示实数 \(x\) 的一元谓词。根据定理 10.3.1，存在一个度的有限序列 \(\bar{\mathbf{p}}\) 和偏序语言中的一个公式 \(\varphi\)，它们共同定义 \(R^*\)。在本节中固定公式 \(\varphi\)。注意，并非每个 \(\bar{\mathbf{p}}\) 连同 \(\varphi\) 都必然编码一个算术标准模型。

**Definition 10.3.4.** 给定一个超算度的有限序列 \(\bar{\mathbf{p}}\) 和一个实数 \(x\)，如果 \(\bar{\mathbf{p}}\) 和 \(\varphi\) 共同定义一个关系 \(R^* = (R_\omega, R_<, R_+, R_\cdot, R_0, R_1)\)，该关系表示算术标准模型 \(\mathcal{M} = \langle \omega, x, <, +, \cdot, 0, 1 \rangle\)，则我们说 \(\bar{\mathbf{p}}\) 带 \(x\)（作为二阶元素）编码一个标准模型。

如果去掉一元谓词 \(x\)，那么如果 \(\bar{\mathbf{p}}\) 和 \(\varphi\) 定义一个关系 \(R = (R_\omega, R_<, R_+, R_\cdot, R_0, R_1)\)，该关系表示 \(\mathcal{M} = \langle \omega, <, +, \cdot, 0, 1 \rangle\)，则 \(\bar{\mathbf{p}}\) 编码一个标准模型。那么关系 "\(\bar{\mathbf{p}}\) 和 \(\varphi\) 编码一个标准模型" 在 \((\mathscr{P}_n, \le)\) 中是可定义的。为了看到这一点，我们作如下观察：

- (i) 由 \(R\) 表示的模型 \(\mathcal{M}\) 满足 Robinson 算术 \(Q\) 系统。由于 \(Q\) 是一个有限公理集合，它可以用一个句子表示；
- (ii) \(\mathcal{M}\) 是良基的（well-founded）。换句话说，不存在无限下降的 \(R_<\)-序列。根据定理 10.3.1，存在一个公式 \(\psi(\bar{U}, \mathbf{v})\)，使得 \(\mathcal{M}\) 是良基的当且仅当对于任何有限序列 \(\bar{\mathbf{q}}\)，集合 \(\{ \mathbf{d} \mid (\mathscr{P}_n, \le) \vDash \psi(\bar{\mathbf{q}}, \mathbf{d}) \}\) 不是一个无限下降的 \(R_<\)-序列。

因此，\(\bar{\mathbf{p}}\) 和 \(\varphi\) 编码一个标准模型的陈述是可定义的。

### 10.3.3 双可解释性

关于双可解释性的一般定义，参见 Hodges [52]。我们将注意力集中在超算度背景下的双可解释性。

固定一个关系 \(R^*\)，使得

\(R^*(\bar{\mathbf{p}}, \mathbf{x})\) 当且仅当 \(\bar{\mathbf{p}}\) 编码一个实数 \(x\) 且 \(x \in \mathbf{x}\)。





### Definition 10.3.5.
度结构 $(\mathscr{P}_h, \le)$ 与二阶算术是 *双可解释的*，当且仅当 $R^*$ 在 $(\mathscr{P}_h, \le)$ 中可定义。

其直觉如下：显然 $(\mathscr{P}_h, \le)$ 可以在二阶算术的标准模型 $\mathcal{M} = (\omega, \mathscr{P}(\omega), <, +, \cdot, 0, 1, \in)$ 中被“解释”。换句话说，任何 $(\mathscr{P}_h, \le)$-可定义关系在 $\mathcal{M}$ 中都可定义。逆命题并不明显。Slaman 和 Woodin [144] 表明，$(\mathscr{P}_h, \le)$ 的双可解释性将使人们能够在 $(\mathscr{P}_h, \le)$ 中解释 $\mathcal{M}$。换句话说，任何 $\mathcal{M}$-可定义的度关系在 $(\mathscr{P}_h, \le)$ 中都可定义。这就是以下定理的内容。我们说，一组超度是解析的，如果它是某个解析集的超度集合。

### Proposition 10.3.6.
*如果* $(\mathscr{P}_h, \le)$ *与二阶算术双可解释，则每个解析的超度集合在* $(\mathscr{P}_h, \le)$ *中可定义*。

**证明。** 假设 $A$ 是解析的。令 $\tilde{A} = \{ \mathbf{x} \mid \exists \mathbf{y} \in A \, \mathbf{x} \in \mathbf{y} \}$。我们证明 $\tilde{A}$ 在 $(\mathscr{P}_h, \le)$ 中可定义。设 $\psi$ 为二阶算术语言中的一个公式，使得
\( x \in A \Leftrightarrow (\omega, \mathscr{P}(\omega), <, +, \cdot, 0, 1, \in) \models \psi(x) \)。

由于对可数超度集合的量化可以通过编码在 $(\mathscr{P}_h, \le)$ 中表达，对 $\omega$ 的二阶量化也可以通过对 $\omega$ 子集编码的一阶量化在 $(\mathscr{P}_h, \le)$ 中得到解释。因此，$\mathbf{x} \in A$ 当且仅当存在一个有限序列 $\tilde{\mathbf{p}}$，使得 $R^*(\tilde{\mathbf{p}}, \mathbf{x})$ 且 $\psi(x)$ 在由 $\tilde{\mathbf{p}}$ 对 $\mathbf{x}$ 进行编码且包含 $\omega$ 的模型中得到满足。

因此，$\tilde{A}$ 在 $(\mathscr{P}_h, \le)$ 中可定义。

定理 10.2.4 中证明的超度刚性使人们能够证明该结构与二阶算术的双可解释性：

### Theorem 10.3.7 (Slaman and Woodin [141], Shore [133]).
*结构* $(\mathscr{P}_h, \le)$ *与二阶算术双可解释*。

**证明。** 设 $\psi(\tilde{\mathbf{p}}, \mathbf{x})$ 定义如下：

- $\tilde{\mathbf{p}}$ 对实数 $\mathbf{x}$ 进行编码；
- 对于任何编码的实数 $y \le_\alpha x$，存在度 $\mathbf{y}_0, \mathbf{y}_1 > \mathbf{x}$，使得
- $\mathbf{y}_0 \cap \mathbf{y}_1 = \mathbf{x}$，且
- $e_\gamma$ 可以嵌入到 $[\mathbf{x}, \mathbf{y}_0]$ 和 $[\mathbf{x}, \mathbf{y}_1]$ 中，且最小元为 $\mathbf{x}$。

根据定理 10.3.1，$\psi$ 可以被视为偏序语言中关于 $\langle \mathscr{P}_h, \le \rangle$ 的一阶公式。如果 $R^*(\tilde{\mathbf{p}}, \mathbf{x})$ 成立，则根据引理 10.2.3，$\langle \mathscr{P}_h, \le \rangle \models \psi(\tilde{\mathbf{p}}, \mathbf{x})$。

如果 $\langle \mathscr{P}_h, \le \rangle \cong \langle \psi(\mathbf{p}), \in \rangle$，则根据引理 10.2.3，所述实数 $x$ 必须具有超度 $\mathbf{x}$。因此 $R^*(\tilde{\mathbf{p}}, \mathbf{x})$ 为真。

总之，结构 $(\mathscr{P}_h, \le)$ 与二阶算术双可解释。

### 10.3.4 练习

**练习 10.3.1.** 证明集合 \(S_i\)、\(T_i\) 和 \(U_i\) 是反链。

**练习 10.3.2.** 证明如果 \(\pi : \mathscr{D}_h \to \mathscr{D}_h\) 是一个初等嵌入，则 \(\pi\) 是恒等映射。

**练习 10.3.3** (Simpson [139]). 证明超度的一阶理论与算术的二阶理论递归同构。

**练习 10.3.4** (Slaman and Woodin [143]). 证明定理 10.3.1 对图灵度成立。

**练习 10.3.5.** 证明在假设 \(V = L\) 下，如果 \((\mathscr{D}_h, \le, \mathbf{a}) \equiv (\mathscr{D}_h, \le, \mathbf{b})\)，则 \(\mathbf{a} = \mathbf{b}\)。

## 11 基定理

在前几章中，我们已经见过不可数实数集的例子（例如 \(\Sigma^1_1\) 和某些 \(\Pi^1_1\)-集），它们包含完美子集。在本章中，我们研究不可数实数集的基定理以及完美集的基性质。

### 11.1 关于 \(\Delta^1_1\)-实数集的基定理

#### 11.1.1 弗里德曼猜想

Friedman [29] 猜想，每个不可数的 \(\Delta^1_1\)-实数集在每个大于或等于 \(\emptyset\) 的超度的超度中都有一个元素。该猜想由 Martin [94] 和 Friedman 独立解决。

**Theorem 11.1.1** (Martin [94] and Friedman). 如果 \(A \subseteq \omega^\omega\) 是一个不可数的 \(\Delta^1_1\)-集，则存在一个完美树 \(T \subseteq \omega^{<\omega}\) 使得 \([T] \equiv A\) 且对于任何 \(x \ge_h \emptyset$，存在 \(z \in [T]\) 使得 \(z \equiv_h x\)。

Suppose that \(A \subseteq \omega^\omega\) 是一个不可数的 \(\Delta^1_1\)-集。根据推论 2.2.14，存在一个递归函数 \(h : \omega^\omega \to \omega^\omega\) 和一个 \(\Pi^0_1\)-集 \(B \subseteq \omega^\omega\) 使得 \(h\) 将 \(B\) 映射到 \(A\) 并在 \(B\) 上是单射的。然后对于每个 \(x \in B$，\(h(x) \equiv_h x\) 且对于每个 \(y \in A$，存在 \(x \in B\) 使得 \(x \equiv_h h(x) = y\)。因此，只需证明每个 \(x \ge_h \emptyset\) 满足某些 \(z \in B\) 的 \(z \equiv_h x\)。由于 \(B\) 是一个 \(\Pi^0_1\)-类，存在一个递归树 \(T \subseteq \omega^{<\omega}\) 使得 \(B = [T] = \{x \mid (\forall n)(x \upharpoonright n \in T)\}\)。我们将在下一节证明一个稍强的结果：

**Theorem 11.1.2.** 每个具有不可数多条无限路径的 \(\Sigma^1_1\)-树 \(T_1\) 在每个大于或等于 \(\emptyset\) 的超度中都有一个元素。

#### 11.1.2 弗里德曼猜想的证明

我们按照 [172] 证明 Theorem 11.1.2。设 \(T_1 \subseteq \omega^{<\omega}\) 是一个带有非超算术路径的 \(\Sigma^1_1\)-树。那么 \(\omega^\omega \setminus T_1\) 的节点有一个 \(\Sigma_1(L_{\omega_1^{CK}})\)-枚举。我们用 \(T_1[\beta]\) 表示直到阶段 \(\beta\) 尚未被枚举的节点集合。那么 \(T_1 = \cap_{\beta < \omega_1^{CK}} T_1[\beta]\)。修正一个非空递归树 \(T_0 \subseteq \omega^{<\omega}\)，它有一条无限路径且没有超算术无限路径。设 \(f\) 为 \(T_0\) 的最左路径。那么 \(f \equiv_h \emptyset\)。

**Lemma 11.1.3.** 如果 \(T_1 \cap [v] = \{ \tau \in T_1 \mid \tau \supseteq v \}\) 没有非超算术无限路径，则存在一个阶段 \(\beta < \omega_1^{CK}\) 证明这一点。换句话说，存在一个 \(\Sigma_1(L_{\omega_1^{CK}})\) 部分函数 \(H : \omega^{<\omega} \to \{0\}\) 使得 \(H(\sigma)\) 未定义当且仅当 \(T_1 \cap [\sigma]\) 包含一条非超算术无限路径。

Proof. Suppose that \(\sigma \in T_1\) 和 \(T_1 \cap [\sigma]\) 没有非超算术无限路径。我们对 \(T_1 \cap [\sigma]\) 执行一种康托尔-本迪克森类型操作，如下：设 \(\le_{KB}\) 为 \(\omega^{<\omega}\) 上的克莱尼-布劳威尔序。在阶段 \(\beta < \omega_1^{CK}\)，定义一棵子树 \(T_1^\beta\)。\(T_1^0\) 实际上是 \(T_1[\sigma]\)，但移除了那些字符串 \(\sigma'\)，其中 \([\sigma]\) 在阶段 \(\beta\) 被看到在 \(T_1\) 中不包含非超算术路径。

Stage 0. Let \(T_1^0 = T_1[\sigma]\)。

Stage \(\beta + 1\)。给定 \(\sigma \in T_1^\beta\) 和 \(\tau > \sigma\)，如果 (1) 存在一个在 \(L_\beta\) 中的 \(<_{KB}\) 序保持函数 \(h : T_1^\beta \cap [\tau] \to \beta\)（因此 \(T_1^\beta \cap [\tau]\) 中没有无限路径），或 (2) 存在一个函数 \(h \in L_\beta\) 将 \(T_1^\beta \cap [\tau]\) 枚举为唯一的超算术路径。

那么令 \(T_1^{\beta+1} = T_1^\beta \setminus [\tau]\) 并声明 \(\tau\) 在阶段 \(\beta + 1\) 从 \(T_1^\beta\) 中移除。

根据命题 3.6.10 中常见的康托尔-本迪克森证明，如果 \(T_1 \cap [\sigma]\) 没有非超算术无限路径，则每个 \(\tau > \sigma\) 在某个阶段 \(\beta\) 被移除。然后根据 \(\omega_1^{CK}\) 的可接受性，存在一个阶段 \(\beta_\sigma < \omega_1^{CK}\) 使得每个 \(\tau > \sigma\) 在 \(\beta_\sigma\) 被移除。在阶段 \(\beta_\sigma\)，定义 \(H(\sigma) = 0\)。

因此，\(H\) 可以被视为一个 \(\Sigma_1(L_{\omega_1^{CK}})\)-部分枚举函数。一个节点 \(\sigma \in \omega^{<\omega}\) 是树 \(T_1\) 中的分裂节点，如果存在 \(j \neq j'\) 使得 \(H(\sigma^\frown j)\) 和 \(H(\sigma^\frown j')\) 都未定义。对于 \(\beta < \omega_1^{CK}\)，一个节点 \(\sigma \in \omega^{<\omega}\) 是树 \(T_1[\beta]\) 中的分裂节点，如果存在 \(i \neq j\) 使得 \(H(\sigma^\frown i)\) 和 \(H(\sigma^\frown j)\) 在阶段 \(\beta\) 都未定义。通过类似的论证，存在一个 \(\Sigma_1(L_{\omega_1^{CK}})\)-部分函数 \(K : \omega^{<\omega} \to \{0\}\) 使得 \(K(\sigma)\) 未定义当且仅当存在 \(T_0 \cap [\sigma]\) 中的一条无限路径。注意 \(K\) 与 \(H\) 不同。

我们称一个节点 \(\sigma \in \omega^{<\omega}\) 为 \(T_0\) 中的终端节点，如果 \(K(\sigma)\) 已定义。对于 \(\beta < \omega_1^{CK}\)，\(\sigma \in \omega^{<\omega}\) 是 \(T_0[\beta]\) 中的终端节点，如果 \(K(\sigma)\) 在阶段 \(\beta\) 已定义。

现在，对于任何 \(x \in \omega^\omega\)，我们构造一个 \(z \in [T_1]\) 使得 \(x \equiv_B z\)：Stage 0. Let \(\sigma_0 = 0\)。

Stage \(s + 1\)。设 \(\sigma' > \sigma_s\) 为 \(T_1\) 扩展 \(\sigma_s\) 的最左分裂节点，使得 \(\sigma_s\) 和 \(\sigma'\) 之间有 \(f(s)\) 个分裂节点。设 \(\sigma'' > \sigma'\) 为 \(T_1\) 扩展 \(\sigma'\) 的第二个最左分裂节点。设 \(\sigma_{s+1} > \sigma''\) 为 \(T_1\) 扩展 \(\sigma''\) 的第 \(x(s) + 1\) 个最左分裂节点。

令 \(z = \bigcup_{s \in \omega} \sigma_s\)。

我们证明 \(x \in L_{\omega_1}[z]\)。事实上，我们表明存在一个 \(\Sigma_1(L_{\omega_1}[z])\)（因此也是 \(\Delta_1(L_{\omega_1}[z])\)）可定义的递增序数序列 \(\{\alpha_s\}_{s \in \omega}\)，位于 \(\omega_1^{CK}\) 之下，使得 \(x \in L_{\bigcup \{ \alpha_s, \alpha_{s+1} \}}[z]\)。那么 \(\bigcup_s \alpha_s + 1 < \omega_1^{CK}\)，从而证明 \(x \in L_{\omega_1}[z]\)。

其思想是在 \(L_{\omega_1}[z]\) 中解码 \(z\) 的构造。对于每个 \(n < \omega\)，我们使用 \(z\) 来识别 \(f(n)\) 的值，其中 \(f\) 是 \(T_0\) 的最左路径。例如，考虑 \(n = 0\) 的情况。给定 \(\beta < \omega_1^{CK}\)，我们从 \(T_1[\beta]\) 的根开始，计算 \(z\) 在 \(T_1[\beta]\) 中“向左转”的次数 \(l_\beta\)。那么 \(l_\beta\) 是 \(f(0)\) 的一个可能值。当然，这个猜测可能是错误。为了帮助做出更好的猜测，我们还通过询问 \(0^\frown l_\beta\) 是否不是 \(T_0[\beta]\) 中的终端节点，但对于每个 \(l' < l_\beta\)，\(0^\frown l'\) 都是终端节点，来确定 \(l_\beta\) 是否为 \(f(0)\)。如果



这不成立，进入一个阶段 \(\beta' > \beta\)，使得此处成立。根据编码过程，必存在一个大于 \(\beta\) 且小于 \(\omega_1^{CK}\) 的 \(\beta''\)，使得 \(l_{\beta''}\) 满足这些要求。

令 \(\beta_1\) 为第一个这样的阶段。无法断定 \(l_\beta\) 确实是 \(f(0)\) 的真实值。\(l_\beta\) 和 \(f(0)\) 的计算值（如在 \(T_0[\beta_1]\) 中所见）在后续阶段可能会改变。然而，这种情况不会无限次发生，因为否则要么 \(l_\beta\) 趋于无穷，要么对于某个有限极限 \(l\)，\(l_\beta = l\) 无限次出现。无论哪种情况，由于 "\(\sigma\) 是 \(T_1\) 中的终端节点" 是一个 \(\Sigma_1\)-陈述，\(z\) 将是 \(T_1\) 中的最左路径，这产生矛盾。因此错误猜测最多出现有限多次，且 \(l_\beta\) 在有限次变化后达到极限。

一般来说，为了从 \(z\) 计算 \(f(n)\)，人们模仿 \(f(0)\) 的猜测过程。这将涉及有限损伤论证。因此，一旦有限序列 \((0, l_\beta^0)^\frown (1, l_\beta^1)^\frown \dots (n, l_\beta^n)\) 在阶段 \(s\) 时与 \(f \lceil n\) 的计算值匹配，我们就令 \(\beta_s\) 为 \(\beta''\)。在后续阶段计算的序列和 \(f \lceil n\) 的值可能会改变，但变化最多发生有限次。因此 \(l_\beta^n\) 将达到极限。令 \(y\) 为 \(\{\beta_s\}_{s<\omega}\) 的最小上确界。显然 \(y < \omega_1^{CK}\)，且 \(l_\beta|_{s<y}\) 的极限是 \(T_0[y]\) 中的一条无限路径。由于 \([T_0] = [T_0[y]]\)，它也是 \(T_0\) 中的一条无限路径。而且，它是最左路径。因此 \(z\) 超算术地计算 \(T_0\) 的最左路径。利用这一点，通过解码方法可以证明 \(z \equiv_T x\)。

现在进行正式证明。

定义 \(\alpha_s, \sigma_s^0, f_s(n)\) 如下。目标是确保 \(\lim_{s \to \omega} f_s(n) = f(n)\)。

阶段 0。令 \(\sigma_0^0 = 0\)，且对每个 \(n\)，\(\beta_0 = f_0(n) = 0\)。我们说 0 受到关注。假设在阶段 \(s \ge 0\) 时，\(\beta_s\) 已定义，且如果 \(j \le s\) 受到关注，则 \(f_s(j)\) 和 \(\sigma_s^j\) 已定义。那么，如果说 \(z\) *在 \(\beta\) 处直到 j 都正确*，是指对于每个 \(i \le j\)，如果 \(0 < i\)，则

- (1) \(f_s \lceil (i + 1)\) 是 \(T_0[\beta]\) 中的最左非终端节点；
- (2) 存在一个 \(\sigma' < \sigma_s^i\)，它是 \(T_1[\beta]\) 中的最左分裂节点，使得 \(\sigma'\) 在 \(T_1[\beta]\) 中有 \(f_s(i)\) 个扩展 \(\sigma_s^{i-1}\) 的分裂节点；且
- (3) 对于上述 \(\sigma'\)，存在一个节点 \(\sigma'' < \sigma'\)，它扩展 \(\sigma'\) 并且是在 \(T_1[\beta]\) 上扩展 \(\sigma'\) 的第二个最左分裂节点，使得 \(\sigma_s^i\) 是在 \(T_1[\beta]\) 中扩展 \(\sigma''\) 的下一个分裂节点。

阶段 \(s+1\)。令 \(j_{s+1}\) 为 \(j \le s\) 中使得 \(z\) 在 \(\beta_s + 1\) 处直到 \(j\) 都不正确的最小值（若存在这样的 \(j\)），否则令其为 \(s+1\)。初始化每个 \(j > j_{s+1}\)，并对 \(j < j_{s+1}\) 令 \(f_{s+1}(j) = f_s(j)\) 且 \(\sigma_{s+1}^j = \sigma_s^j\)。对于 \(j = j_{s+1}\)，有两种情况：

情况 1。\(j_{s+1} = 1\) 自上次初始化以来（如果有的话）未受到任何关注。令 \(\beta_{s+1} = \beta_s + 1\)，\(\sigma_{s+1}^{j_{s+1}} > \sigma_s^{j_{s+1}-1}\) 为 \(T_1[\beta_{s+1}]\) 中的下一个分裂节点，且 \(f_{s+1}(j_{s+1}) = 0\)，并宣布 \(j_{s+1}\) 在阶段 \(s+1\) 受到关注。

情况 2。否则。搜索一个小于 \(\omega_1^{CK}\) 且大于 \(\beta_s\) 的 \(\beta\)，使得 \(z\) 在 \(\beta\) 处直到 \(j_{s+1} - 1\) 都正确，并且存在一个扩展 \(\sigma_s^{j_{s+1}-1}\) 的 \(\sigma < z\)，使得存在一个满足以下条件的 \(l\)：

- (i) \(f_s \lceil j_{s+1} \lceil (j_{s+1}, l)\) 是 \(T_0[\beta]\) 中的最左非终端节点；
- (ii) 存在一个 \(\sigma' < \sigma\)，它是 \(T_1[\beta]\) 中的最左分裂节点，使得 \(\sigma'\) 在 \(T_1[\beta]\) 中有 \(l\) 个扩展 \(\sigma'_{s-1}^{-1}\) 的分裂节点；且
- (iii) 对于上述 \(\sigma'\)，存在一个扩展 \(\sigma'\) 的节点 \(\sigma'' < \sigma\)，它是在 \(T_1[\beta]\) 中扩展 \(\sigma'\) 的第二个最左分裂节点，使得 \(\sigma\) 是在 \(T_1[\beta]\) 中扩展 \(\sigma''\) 的下一个分裂节点。

假设在情况 2 的搜索过程中，\(z\) 始终在 \(\beta\) 处直到 \(j_{s+1} - 1\) 都正确。根据 \(z\) 的定义，所规定的 \(\beta\) 存在。然后令 \(\beta_{s+1} = \beta\)，\(f_{s+1}(j_{s+1}) = l\) 且 \(\sigma'_{s+1}^{-1} = \sigma\)。宣布 \(j_{s+1}\) 在阶段 \(s+1\) 受到关注。否则，\(z\) 在 \(\beta\) 处直到 \(j_{s+1} - 1\) 不正确，我们将 \(j_{s+1}\) 替换为 \(j_{s+1} - 1\) 来进行搜索。然而，这种替换过程只发生有限多次，因为 \(z\) 在任何 \(\beta\) 处始终直到 0 都正确。这完成了构造。

令 \(\gamma = \bigcup_{s \in \omega} \beta_s\)。那么 \(\{\beta_s\}_{s \in \omega}\) 是一个 \(\Delta_1(L_{\omega_1}[z])\)-序列，因此 \(\gamma < \omega_1^z\)。

#### **引理 11.1.4.** 对于每个 \(j\)，存在一个阶段 \(s_j\)，使得如果 \(s \ge s_j\)，则 \(z\) 在 \(\beta_s\) 处直到 \(j\) 都正确。

证明。假设否则。令 \(j^*\) 为最小的 \(j\)，使得对于无限多个 \(s\)，\(z\) 在 \(\beta_s\) 处直到 \(j^*\) 都不正确。那么构造中的情况 2 适用于 \(j^*\)。令 \(s_{j^*-1}\) 为最小阶段，使得对于每个 \(s \ge s_{j^*-1}\)，\(z\) 在 \(\beta_s\) 处直到 \(j^* - 1\) 都正确。对于 \(s > s_{j^*-1}\)，令 \(\sigma_s^0\) 为构造中在阶段 \(s\) 针对 \(j^*\) 定义的 \(\sigma^0\)。换句话说，对于 \(z\) 的某个初始段 \(\sigma\)，\(\sigma_s^0 < \sigma\) 是 \(T_1[\beta_s]\) 中的最左分裂节点，使得 \(\sigma_s^0\) 在 \(T_1[\beta_s]\) 中有 \(f_s(j^*)\) 个扩展 \(\sigma_s^{0-1}\) 的分裂节点。注意，对于任何 \(s \ge s_{j^*-1}\)，\(f_{s+1}(j^*) \ge f_s(j^*)\)。因此，每当 \(s > s_{j^*-1}\) 时，\(|\sigma_{s+1}^0| \ge |\sigma_s^0|\)。由于对于任何 \(r\)，\(z\) 都不是 \(T_1[\gamma \cap r]\) 的最左路径，\(\sigma^0 = \lim_s \sigma_s^0\) 存在。令 \(s_1 > s_{j^*-1}\) 使得对于 \(s \ge s_1\)，\(\sigma_s^0 = \sigma^0\)。根据构造，对于 \(s \ge s_2\)，\(f_{s+1}(j^*) = f_s(j^*)\)。由此可知存在一个 \(s_{j^*} \ge s_1\)，使得对于所有 \(s \ge s_{j^*}\)，\(\sigma_s^0 = \sigma_{s_{j^*}}^0 = \sigma^0\)。那么对于任何 \(s \ge s_{j^*}\)，\(z\) 在 \(\beta_s\) 处直到 \(j^*\) 都正确。

根据引理 11.1.4，我们可以令 \(f(j) = \lim_{s \to \omega} f_s(j)\)。显然，\(\hat{f} \in L_{\omega+1}[z]\)。注意，对于任何 \(j\)，\(T_0 \supseteq \sigma \langle \forall k \le j \rangle (\sigma(k) = \hat{f}(k))\)。因此 \(\hat{f}\) 是 \(T_0\) 中的一条无限路径。根据构造，\(\hat{f} = f\)，因此 \(f \in L_{\omega+1}[z]\)。由于 \(\hat{f} \notin \emptyset\)，我们有 \(\emptyset \notin z\) 且 \(\omega_1^{CK} < \omega_1^z\)。那么构造可以从 \(z\) 解码出来。因此 \(z \not\ge_h x\)。如果 \(x \not\ge_h \emptyset\)，则 \(x\) 也可以解码该构造，从而 \(x \not\ge_h z\)。

上述证明中的构造产生了一棵完美树 \(T \le_T \emptyset\)，其中 \([T] \subseteq A\)，且其中每条无限路径 \(x\) 都在超算术意义上高于 \(\emptyset\)。这完成了定理 11.1.2 的证明。

### 11.1.3 练习

- **练习 11.1.1.** 证明存在一个 \(\Sigma^1_1\)-集 \(A\)，它包含一个实数 \(x \ge_h \emptyset\)，但高于 \(\emptyset\) 的超度并非每个都在 \(A\) 中有代表元。

- **练习 11.2 (Feferman).** 证明存在一个 \(\Sigma^1_1\)-集 \(A\)，其中任何两个不同的成员在超算术意义上不可比。

- **练习 11.3.** 证明如果一个 \(\Sigma^1_1\)-集 \(A\) 包含一个成员，该成员超算术地计算每个可构实数，那么存在一个超度锥，其中每个成员都在 \(A\) 中有代表元。

- **练习 11.4.** 证明存在一个完美的 \(\Pi^0_1\)-集 \(A \subseteq 2^\omega\)，其中没有成员图灵计算 \(0'\)。

- **练习 11.5.** 证明集合 \(\{x \oplus y \mid x \le_h y\} \subseteq 2^\omega\) 不是博雷尔集。

- **练习 11.6 (Kechris [64]).** 证明 HYP 是 \(2^\omega\) 中在超算术可归约性下封闭的最大 \(\Pi^1_1\)-真子集。

## 11.2 \(\Pi^0_1\)-集的反基定理

#### 11.2.1 定理 11.1.1 的分析

由定理 11.1.1 引发的一个自然问题是：陈述中的条件 \(x \ge_h \emptyset\) 是否可以减弱为 \(x^{(\beta)} \ge_T \emptyset\)，甚至对于某些 \(\beta < \omega_1^{CK}\) 减弱为 \(x^{(\beta)} \ge_T 0^{(\beta+1)}\)。该定理的证明需要至少 \(\omega_1^{CK}\) 次图灵跳跃的迭代。Harrington 给出了否定答案：

**定理 11.2.1 (Harrington [43]).** 对于任何序数 \(\beta < \omega_1^{CK}\)，存在一个不可数的 \(\Pi^0_1\)-集 \(A \subseteq \omega^\omega\)，使得对于每个 \(x \in A\)，\(x^{(\beta)} \not\ge_T 0^{(\beta+1)}\)。

我们从定理 11.2.1 的有限版本开始讨论。

**定理 11.2.2.** 存在一个不可数的 \(\Pi^0_1\)-集 \(A \subseteq \omega^\omega\)，使得对于任何 \(x \in A\) 和 \(n < \omega\)，\(x^{(n)} \not\ge_T 0^{(n+1)}\)。

Harrington 的证明使用了一种巧妙的逆归纳构造。下面的证明比必要的更复杂，但该论证适用于更一般的情况。根据定理 2.1.4，集合 \(H = \{(i, (0)^i) \mid i < \omega\} \subseteq \omega \times 2^\omega\) 是 \(\Pi^0_2\)。因此存在一个递归谓词 \(P(i, \sigma, m)\)，使得 \((i, x) \in H \Leftrightarrow (\forall m)(\exists k)P(i, x \unknown k, m)\)。令 \(T^\omega \subseteq \omega \times \omega^{<\omega}\) 为一棵递归树，使得

\((i, \sigma) \in T^\omega \Rightarrow (\exists m)(\exists s_m)(\sigma = \sigma_0 \oplus \sigma_1 \dots \sigma_s \mid \sigma_0 = s_m \wedge |\sigma_0| = 2^m \cdot 3^{s_m} \wedge s_m = \min\{|s| \mid (\forall l \le m)(\exists k \le s)P(i, \sigma_0 \unknown k, l)\})\).

很容易验证，对于每个 \(i < \omega\)，存在唯一的 \(z_i\) 使得 \((i, z_i) \in [T^\omega]\) 且 \(z_i = (0)^i \oplus y_i\) 对于某些 \(y_i \in \omega^\omega\)。因此，一致地，每个 \(\emptyset^{(i)}\) 都是一个 \(\Pi^0_1\)-单元素集（在 \(\omega^\omega\) 中）。

我们定义三棵树的序列 \(\{T_i\}_{i < \omega}\)、\(\{T'_i\}_{i < \omega, j < 2}\) 在 \(\omega^{<\omega} \times \omega^{<\omega}\) 中，一个函数序列 \(\{\psi_i\}_{i < \omega}\)，以及 \(\omega\) 中的常数序列 \(\{c_j\}_{j \le 2}\)，使得对每个 \(i < \omega\)，



- (1) \( T_1^i = \{\sigma \mid (\sigma, i) \in T^0\} \);
- (2) \( (\sigma, \tau) \in T_i \Rightarrow (\exists \tau' \supseteq \tau)(\tau' \in T_1^i \land \Delta_{c_0}^{T^0}(\sigma)[\tau'] = 1) \);
- (3) \( T_0^i = \sigma \mid (\exists \tau > \emptyset)(\langle \sigma, \tau \rangle \in T_i) \);
- (4) \( \psi_i : T_{i+1}^i \to T^0 \) 是 \( \emptyset^{(i+1)} \);
- (5) \( \psi_i \) 是从 \( [T_{i+1}^i] \) 到 \( [T_0^i] \) 的同胚，使得 \( (\forall x \in [T_i])(\psi_i(x^{-1}) \ominus \emptyset^{(i+1)} \equiv_T (x \ominus \emptyset^{(i)})') \) 通过 (c2, c3) 和
- (5a) \( \sigma < \tau \Rightarrow \psi_i(\sigma) \le \psi_i(\tau) \);
- (5b) 如果 \( \sigma \nsubseteq T_0^i \)，那么 \( |\psi_i(\sigma)| \ge |\sigma| \);
- (6) \( T_0^i \cap \emptyset^{<i} = 2^{<i} \)，且
- (7) \( (\forall \sigma \in T_{i+1}^i \cap \emptyset^i)(\sigma \le \psi_i(\sigma)) \).

假设这些序列已被定义。

#### 引理 11.2.3.
对于每个 \( x \in [T_0^0] \) 和 \( i < \omega \)，
(i) \( x^0 \equiv x \ominus \emptyset^0 \) 且
(ii) \( x^{(i)} \not\le_T \emptyset^{(i+1)} \).

**证明.** 由 (4)、(5) 关于 \( i \) 的归纳，(i) 立即成立。若 \( x^{(i)} \ge_T \emptyset^{(i+1)} \)，则 \( x^{(i+1)} \equiv_T x \ominus \emptyset^{(i+1)} \le_T x^0 \)，这产生矛盾。故 (ii) 成立。

#### 引理 11.2.4.
\( [T_0^0] \) 与 \( 2^\omega \) 同胚.

**证明.** 我们定义 \( [T_0^0] \) 与 \( 2^\omega \) 之间的双射 \( f \) 如下：对于每个 \( x \in [T_0^0] \)，令
\( f(x) = \bigcup_{i < \omega} \psi_1^{i-1} \circ \psi_{i-1}^1 \circ \cdots \circ \psi_0^1(x) \mid i \).

令 \( x \in [T_0^0] \). 对于 \( i < \omega \)，令 \( x_i = \psi_1^{i-1} \circ \psi_{i-1}^1 \circ \cdots \circ \psi_0^1(x) \mid i \). 则 \( \psi_1^{i-1} \circ \cdots \circ \psi_0^1(x) \in [T_{i+1}^i] \cap [\sigma_i] \). 又 \( \psi_{i+1}^1 \circ \cdots \circ \psi_0^1(x) \in [T_{i+2}^i] \). 因为 \( \psi_{i+1}^1 \) 是单射，所以 \( \psi_{i+1} \circ \psi_i^1 \circ \cdots \circ \psi_0^1(x) \in [T_{i+1}^i] \cap [\sigma_i] \). 由 (7)，\( \psi_{i+1}^1 \circ \cdots \circ \psi_0^1(x) \mid (i+1) \ge \psi_{i+1}^1 \circ \cdots \circ \psi_0^1(x) \mid i+1 = \sigma_{i+1} \). 故 \( \sigma_{i+1} \ge \sigma_i \). 由 (5b)，\( f(x) \in 2^\omega \).

令 \( y \in 2^\omega \) 且对 \( n, i < \omega \) 令 \( \tau_{n,i+1} = \psi_n \circ \cdots \circ \psi_{i+1}(y \mid n+t) \). 由 (5a), (6) 和 (7),
\( y \upharpoonright n \le \tau_{n,n} \le \tau_{n,n+1} \le \tau_{n,n+2} \cdots \).

此外，由 (5b)，对每个 \( i \)，\( |\tau_{n,n+i}| \ge n+i \). 令 \( X_n = \bigcup_{i < \omega} \tau_{n,n+i} \). 则 \( X_n \in [T_0^0] \cap [y \mid n] \). 因为 \( \psi_n^{-1} \) 是单射，由 (7) 得 \( \psi_n^{-1} \circ \psi_{n+1}^{-1} \circ \cdots \circ \psi_0^{-1}(x_0) \mid n = X_n \mid n = y \mid n \). 由 \( f \) 的定义，有 \( f(x_0) = y \). 所以 \( f \) 是满射.

现在假设 \( x_0, x_1 \in [T_0^0] \) 满足 \( f(x_0) = f(x_1) \)，且对某个 \( n_0 \) 以及 \( i \neq j \)，有 \( x_0 \mid n_0 = x_1 \mid n_0 \)，且 \( x_0 \supset x_0 \mid n_0 \)，\( x_1 \supset x_1 \mid n_0 \). 由 (5b) 和 (7)，\( \psi_{n_0+1}^1 \circ \psi_{n_0}^1 \circ \cdots \circ \psi_0^1(x_0) \mid n_0 + 1 = \psi_{n_0+1}^1 \circ \psi_{n_0}^1 \circ \cdots \circ \psi_0^1(x_1) \mid n_0 + 1 \). 然后由 (5a) 和 (5b)，\( x_0 \mid n_0 + 1 = x_1 \mid n_0 + 1 \)，这产生矛盾.
显然 \( f \) 和 \( f^{-1} \) 都是连续的。因此 \( [T_0^0] \) 与 \( 2^\omega \) 同胚.

注意 \( T_0^0 = \{\sigma \mid \Phi_{e_0}^0(\sigma) = 1\} \) 是一棵递归树。因此集合 \( A = [T_0^0] \) 是一个具有所需性质的不可数 \( \Pi_1^0 \)-集.

我们现在转向定义满足 (1)-(7) 的树、函数序列以及常数。给定一棵树 \( T \)，若对任意 \( \sigma, \tau \in T \) 当且仅当 \( \Phi_i^t(\sigma) = 1 \)，则记 \( T = \Phi_i^t \).

#### **引理 11.2.5.** 存在一个递归函数 \( t : \omega \to \omega \)，使得对于任何 \( x \in 2^\omega \) 和 \( \omega^\omega \) 中的树 \( T = \Phi_{e_i}^x \)，\( \Phi_{i(x)}^0 \) 是 \( \omega^\omega \) 中的一棵树 \( \hat{T} \)，且 \( [\hat{T}] = \{z \oplus h_x \mid z \in [T]\} \)，其中 \( h_x \) 是一个 \( x \)-递归函数，使得 \( h_x(e, n) \) 要么是 0，要么是 \( \min\{s + 1 \mid \Phi_{e(x)}^x(n)[s] \downarrow\} \).

**证明.** 令

\(\hat{T} = \{\sigma \oplus \tau \mid (\forall e, n)((\langle e, n \rangle < |\tau| \land \tau(\langle e, n \rangle) > 0 \to \tau(\langle e, n \rangle) = \min\{s + 1 \le |\tau| \mid \Phi_{e(x)}^{t_k}(n)[s] \downarrow\}) \land (\exists v < 2^{|\tau|}(\forall e \le |v|)(v(e) = 1 \to \Phi_{e(\tau(\langle e, e \rangle))}^{t_k(\langle e, e \rangle)}(e)[\tau(\langle e, e \rangle)] \downarrow) \land \Phi_i^0(\sigma) = 1)\}.\)

则 \( \hat{T} \) 即为所需。由于 \( \hat{T} \) 是一致得到的，存在一个递归函数 \( t : \omega \to \omega \)，使得 \( \hat{T} = \Phi_{i(0)}^t \).

现在对于 \( i, j < \omega \) 且 \( T_{i+1} = \Phi_{i+1}^{\psi(i+1)} \)，我们定义一棵树 \( T_i \)，使得 \( T_i \) 在将 \( \{c_i\}_{i \le j} \) 替换为依赖于 \( T_{i+1} \) 的参数后满足 (1)-(7). 该构造在 \( i \) 和 \( j \) 中是一致的。这意味着存在一个递归函数 \( t \)，使得 \( T_j^0 = \Phi_{i(j)}^{\psi(j)} \). 由递归定理，存在一个 \( c_0 \) 使得 \( T_0^0 = \Phi_{c_0}^0 = \Phi_{i(0)}^{\psi(0)} \). 令 \( T_i = \{(\sigma, \tau) \mid (\exists t' \ge t)(\langle i, t' \rangle \in T^{\omega \omega} \Phi_{c_i}^{t'}(\sigma)[t'] = 1)\} \).

其余参数 \( c_i \)（\( 1 \le i \le 3 \)）以同样的方式得到。因此我们可以假设 \( T_{i+1}^0 \) 具有性质 (1)-(7). \( T_i^0 \) 由 \( T_{i+1}^0 \) 定义.

#### **引理 11.2.6.** 给定一棵递归树 \( T_0 \le \omega^\omega \)，存在一棵递归树 \( T_1 \) 和一个 \( A_2^0 \)-同态 \( \psi : T_0 \to T_1 \)，使得对于任何 \( x \in [T_1] \)，\( x' \equiv_T x \oplus 0' \).

**证明.** 证明采用有限损伤论证。给定一棵递归树 \( T_0 \le \omega^\omega \)，我们通过完全逼近构造定义 \( \psi \) 和 \( T_1 \).

#### 阶段 0.
令 \( \psi_0(\emptyset) = \emptyset \) 且 \( T_{0,0} = \emptyset \). 我们声明所有节点 \( \sigma \in T_0 \) 都是新鲜的.

#### 阶段 \( s + 1 \).
假设 \( \psi_s : T_0 \to T_{1,s} \le 2^{<\omega} \) 是部分定义的。搜索最小的 \( t \le s \)，使得存在一个新鲜的 \( \sigma \in T_0 \)，对于该 \( \sigma \) 存在一个 \( \tau \in T_{1,s} \upharpoonright (\psi_s(\sigma)) \cap 2^{>s} \)，使得 \( \Phi_i^t(t)[\tau] \downarrow \). 对于每个这样的 \( \sigma \)，定义 \( \psi_{s+1}(\sigma) = \tau' > \tau \)，其中 \( |\tau'| = \tau' \cap 0^{t+1} \). 对于所有在 \( T_0 \cap \text{Dom}(\psi_s) \) 中与这样的 \( \sigma \) 不兼容的 \( v \)，令 \( \psi_{s+1}(v) = \psi_s(v) \). 若 \( v \in \text{Dom}(\psi_s) \) 与这些 \( \sigma \) 不兼容且对所有 \( \tau' \in T_0 \upharpoonright \text{Dom}(\psi_s) \)，则定义 \( \psi_{s+1}(\nu') = \psi_s(\nu') \). 声明对于每个这样的 \( \sigma \)，\( \sigma \) 不是新鲜的，且对于扩展这样的 \( \sigma \) 的任何 \( \tau \)，\( \tau \) 是新鲜的. 令 \( T_{1,s+1} = \text{Range}(\psi_{s+1}) \).

这完成了阶段 \( s + 1 \) 的构造。注意对于每个 \( \sigma \)，\( |\{s \mid \psi_s(\sigma) \neq \psi_{s+1}(\sigma)\}| \le |\sigma| \). 因此对于每个 \( \sigma \)，\( \psi(\sigma) = \lim_{s \to \infty} \psi_s(\sigma) \) 存在。于是 \( \psi \) 是 \( A_2^0 \).

令 \( T_1 = \bigcup_{s < \omega} T_{1,s} \). 由构造，\( \psi : [T_0^0] \to [T_1] \) 是一个同态。假设 \( x \in [T_1] \). 给定 \( t \)，为了判定 \( \Phi_i^t(t) \) 是否收敛，我们以 \( \emptyset' \)-递归方式搜索一个

\(\sigma \in T_1 \cap 2^{<\omega}\) 和一个阶段 \( s \ge t \) 使得 \( \psi_s(\sigma) = \psi(\sigma) < x \). 则 \( \Phi_i^t(t) \) 收敛当且仅当 \( \Phi_i^{\psi(\sigma)}(t)[s] \). 因此 \( x' \le_T x \oplus \emptyset' \).

现在如果 \( i < \omega \) 且 \( \sigma \in 2^{<\omega} \)，令 \( \hat{T}_{i+1,l,\alpha} \) 如引理 11.2.5 所述为一个 \( \emptyset^{(i)} \)-递归树，其中将 \( T \) 设为 \( \{\tau \mid \sigma^\frown \tau \in T_{i+1}^0\} \)，将 \( x \) 设为 \( \emptyset^{(i)} \). 通过将 \( T_0 \) 替换为 \( \hat{T}_{i+1,l,\alpha} \) 来对 \( \emptyset^{(i)} \) 实现引理 11.2.6，我们得到一个 \( \emptyset^{(i)} \)-递归同胚 \( \psi_i : \hat{T}_{i+1,l,\alpha} \to T_{l,\alpha} \)，其中 \( T_{l,\alpha} \) 是引理 11.2.6 中的 \( T_1 \). 定义 \( T_i^0 \) 为一个 \( \emptyset^{(i)} \)-递归树，使得 \( \tau \in T_i^0 \) 当且仅当以下之一成立：

- \( |\tau| \le 1 \)，或

- \( \tau = (\tau \upharpoonright \gamma)^\frown \tau' \)，其中 \( \tau' \in T_{1, \upharpoonright \gamma} \).

定义 \( \psi_i \le_T \theta^{(i+1)} : T_{i+1}^0 \to T_i^0 \)，使得

- 若 \( \tau \in 2^{<\omega} \)，则 \( \psi_i(\tau) = \tau \);

- 否则，令 \( \tau = (\tau \upharpoonright \gamma)^\frown \tau' \). 定义 \( \psi_i(\tau) = \tau \upharpoonright \gamma \psi_i(\tau' \oplus (h_{00} \upharpoonright |\tau'|)) \).

因此对于任何路径 \( x \in [T_i^0] \),

\( (x \oplus \theta^{(i)})' \equiv_T x \oplus \theta^{(i+1)} \equiv_T \psi_i^{-1}(x) \oplus \theta^{(i+1)} \).

由于构造是一致的，可以直接验证 (1)-(7) 都满足。这完成了定理 11.2.2 的证明.

### 11.2.2 哈灵顿定理的证明

我们遵循 Hjorth [50] 的表述。由定理 2.6.5，对于任何递归序数 \( \beta \ge \omega \)，存在一个 \( n \in \omega \) 使得 \( [n] = \beta \) 且集合 \( \{m \mid m <_n n\} \) 是递归的。我们选择这样的序数 \( \beta \) 和相应的 \( n \).

对于每个 \( m = 3 \cdot 5^k < \alpha_0 \)，令 \( \{i_{j,m}\}_{j<\omega} \) 为满足以下条件的数字序列：

\( i_{0,m} = \Phi_k(m) \)

和

\( i_{j+1,m} = \Phi_k(m+j+1) \).

由定理 2.6.5 的证明，我们可以假设对所有 \( j \) 都有 \( m \le i_{j,m} < i_{j+1,m} \). 显然集合 \( \{(i_{j,m}, m) \mid (\exists k)(m = 3 \cdot 5^k \land \alpha_0 < n \land j \in \omega)\} \) 是递归的.

#### 引理 11.2.7.

- (i) 对于任何 \( m = 3 \cdot 5^k < \alpha_0 \) 和 \( j < \omega \)，\( i_{j,m} < i_{j+1,m} \).

- (ii) 对于任何 \( l < \alpha_0 \)，集合 \( \{m \mid (\exists k)(i_{0,m} < l < m = 3 \cdot 5^k < \alpha_0)\} \) 是有限的;

- (iii) 集合 \( \{(m,l) \mid (\exists k)(i_{0,m} < l < m = 3 \cdot 5^k < \alpha_0)\} \) 是递归的;

- (iv) 若 \( m = 3 \cdot 5^k < \alpha_0 \) 且 \( |m| = \lim_{n \to \infty} \alpha_n \)，其中 \( \{\beta_i\} \) 是一个递增的极限序数序列，那么对于任何 \( i \)，存在一个 \( m' = 3 \cdot 5^{k'} < \alpha_0 \) 且 \( |m'| > \beta_i \)，使得对于任何 \( m'' = 3 \cdot 5^{k''} < \alpha_0 \) 且 \( |m'| > |m''| \)，都有 \( |i_{0,m'}| > |m''| \).





证明。(i) 立即成立。(ii) 成立，因为对于任何数 $l$，只有有限多个 $m \le l$ 满足 $l <_o m <_o n$。(iii) 成立，因为 $<_o$ 是递归集合 $\{i \mid i <_o n\}$ 上的递归关系。

我们证明 (iv)。如果 $m = 3 \cdot 5^k <_o n$ 且 $|m| = \lim_{i \to \infty} \beta_i$，其中 $\{\beta_i\}$ 是极限序数的递增序列，那么对于任何 $i$，存在一个 $m' = 3 \cdot 5^{k'} <_o m$ 使得 $|m'| > \beta_i$，这样只要 $m' = 3 \cdot 5^{k'} <_o m$ 且 $|m'| > |m''|$，就有 $m' > m''$。因此 $|i_{0,m'}| > |m''|$。

将定理 11.2.2 扩展到任意层级的递归序数时的主要困难在于极限序数阶段的编码。这里，如同在定理 11.2.2 的证明中一样，在每个继承阶段，人们试图进行一种逐步下降的构造，以编码在极限层级计算出的信息。仅处理一个极限序数没有困难。当有多个极限序数时，必须选择其中一个进行编码。引理 11.2.7 允许在极限序数的近似中使用良序列，以便于选择。

为方便起见，在本节余下部分，令 $[n] = \beta_{\infty}$，并将每个 $\le_o n$ 的自然数与它作为序数表示法的序数 $\beta < \beta_{\infty}$ 相识别。特别是，我们用 $\lambda$ 表示那些是极限序数序数表示法的自然数。另外，当 $\lambda = |m|$ 时，令 $\beta_{j,\lambda} = |i_{j,m}|$。我们用 $\theta^{(\beta)}$ 和 $x^{(\beta)}$ 分别表示 $H_i$ 和 $H_i^X$，其中 $|i| = \beta$。最后，$\beta^+$ 与 $2^k$ 相识别，其中 $|k| = \beta$。

对于 $\beta \le_o n$，令

$$
\Lambda(\beta) = \{\lambda \mid \beta <_o \lambda \land (\exists j \in \omega)(\beta_{j,\lambda} \le_o \beta)\}.
$$

注意，根据引理 11.2.7，对于任何 $\beta \le_o n$，$\Lambda(\beta)$ 都是有限的。因此以下定义良好：

$$
j(\beta) = \max(\{0\} \cup \{j \mid (\exists \lambda \in \Lambda(\beta))(\beta_{j,\lambda} \le_o \beta)\}).
$$

对于每个 $a \in \omega$，定义以下“特化”到 $\omega \setminus a$ 的函数：

$$
p_a(\sigma) = \tau \Leftrightarrow (\forall i, j, k)(\tau(\langle j, i \rangle) = k > 0 \leftrightarrow j \notin a \land \sigma(\langle j, i \rangle) = k > 0).
$$

则

$$
p_a(T) = \{p_a(\sigma) \mid \sigma \in T\},
$$

且

$$
p_a(\dot{X}) = x \Leftrightarrow (\forall i, j, k)(x(\langle j, i \rangle) = k > 0 \leftrightarrow j \notin a \land \dot{X}(\langle j, i \rangle) = k > 0).
$$

对于 $\beta <_o \gamma \le_o \beta_{\infty}$，令

$$
(\beta, \gamma] = \{\delta \mid \beta <_o \delta \le_o \gamma\}.
$$

显然，如果 $\beta < \gamma < \delta$，则 $p_{(\beta, \delta]} = p_{(\beta, \gamma]} \circ p_{(\gamma, \delta]}$。如同在上一节中，存在一棵递归树 $T \subseteq \beta_{\infty} \times \omega^{<\omega}$，使得 $T(\beta) = \{\sigma \mid (\beta, \sigma) \in T\}$ 包含恰好一条路径 $\theta^{(\beta)}$。令

$$
T^{\beta_{\infty}} = \{\sigma \mid (\forall \beta)(\exists i)(\exists \tau)(\sigma(\beta, i) \text{ defined} \rightarrow ((\beta, \tau) \in T \land (\forall j)(\sigma(\beta, j) = \tau(j))))\}.
$$

因此 $T^{\beta_{\infty}}$ 将 $T$ 编码为一棵单一的树。对于 $\beta \le_o \beta_{\infty}$，令 $y_\beta$ 为一个实数，使得 $(\forall i, j, k)[y_\beta(\langle i, j \rangle) = k \leftrightarrow i \le_o \beta \wedge \theta^{\langle i \rangle}(j) = k]$。

注意，存在常数 $d_0, d_1$，使得 $y_\beta \equiv_T \theta^{\langle \beta \rangle}$ 通过 $(d_0, d_1)$。我们构建一个系统，包含一致的 r.e. 树序列 $\{T_\beta\}_{\beta \le_o \beta_{\infty}} = \{T_\beta^{p_0} \times T_\beta^{p_1}\}_{\beta \le_o \beta_{\infty}}$、函数 $\{\psi_{\beta, \bar{p}}\}_{\beta \le_o \beta_{\infty}}$ 和常数 $\{c_i\}_{i \le 3}$，使得

- (1) $T_{\beta_{\infty}} = 2^\omega \times T^{\beta_{\infty}}$;
- (2) $T_\beta \cap \omega^{S(\beta)} \times \omega^{S(\beta)} = \{(\sigma, \tau) \in \omega^{S(\beta)} \times \omega^{S(\beta)} \mid (\exists \lambda \in \Lambda(\beta))(\exists \bar{j})(\exists \bar{p})(\beta_{\bar{j}, \lambda} \le \beta \wedge (\sigma, \bar{\tau}) \in T_\lambda \cap 2^{S(\beta)} \times 2^{S(\beta)} \wedge p_{P(\lambda, \bar{j})}(\bar{\tau}) = \tau \}$;
- (3) $T_\beta^p = p_{\beta, \bar{p}_\beta}(T_\beta^\infty)$ 且因此 $[T_\beta^p] = \{y_\beta\}$。令 $T_\beta^0 = \{\sigma \mid (\sigma, y_\beta \upharpoonright |\sigma|) \in T_\beta\} = \mathcal{O}_{C_1}^{\theta^{\langle \beta \rangle}}$;
- (4) $\psi_{\beta, \bar{p}} : T_\beta \to T_\beta^0$ 是一个 $C_1^{\theta^{\langle \beta \rangle}}$;
- (5) $\psi_{\beta, \bar{p}}$ 可视为从 $[T_\beta^0]$ 到 $[T_\beta^0]$ 的同态，使得 $(\forall x \in [T_\beta^0])[p_{\psi_{\beta, \bar{p}}^{-1}}(x) \oplus \theta^{\langle \beta \rangle} \equiv_T (x \oplus \theta^{\langle \beta \rangle})']$ 通过 $(c_2, c_3)$，且
- (5i) 对于 $\sigma, \tau \in T_\beta^0$，$\sigma \prec \tau \Rightarrow \psi_{\beta, \bar{p}}(\sigma) \le \psi_{\beta, \bar{p}}(\tau)$;
- (5ii) 如果 $\sigma \in T_\beta^0$，则 $|\psi_{\beta, \bar{p}}(\sigma)| \ge |\sigma|$；且
- (6) 对于 $\sigma \in T_\beta^0 \cap \omega^{S(\beta)}$，$\psi_{\beta, \bar{p}}(\sigma) = \sigma$。

假设我们有上述的树序列。根据 (4) 和 (5)，对于每个 $x \in T_0^0$，通过对 $\beta \le_o \beta_{\infty}$ 的归纳，可以得出 $x^{(\beta)} \equiv x \oplus \theta^{\langle \beta \rangle} \ge_T \theta^{\langle \beta \rangle}$。

乍看之下，(2) 对 $T_\beta \cap \omega^{S(\beta)} \times \omega^{S(\beta)}$ 设定的要求似乎是一个问题，因为来自 $T_\lambda$（其中 $\lambda \in \Lambda(\beta)$）的太多节点被放入其中。然而，以下引理表明，由于引理 11.2.7 (iv)，$T_\beta \cap \omega^{S(\beta)} \times \omega^{S(\beta)}$ 是一个有序结构。

### 引理 11.2.8.

假设 $\lambda \in \Lambda(\beta)$ 且对于某个 $j$，$\beta_{j, \lambda} \le_o \beta$。那么 $(\sigma, \tau) \in T_\beta \cap \omega^{S(j)} \times \omega^{S(j)}$ 当且仅当存在一个 $(\sigma, \bar{\tau}) \in T_\lambda$ 使得 $p_{\beta, \lambda}(\bar{\tau}) = \tau$。

证明。假设不成立。那么存在一个 $\lambda \in \Lambda(\beta)$，一个使得 $\beta_{j, \lambda} \le_o \beta$ 的 $j$，这样对于某个 $(\sigma, \tau) \in T_\beta \cap \omega^{S(j)} \times \omega^{S(j)}$，不存在 $(\sigma, \bar{\tau}) \in T_\lambda$ 使得 $p_{\beta, \lambda}(\bar{\tau}) = \tau$。

根据 (2)，存在一个 $\lambda_1 \in \Lambda(\beta)$ 使得 $\beta_{j, \lambda_1} \le_o \beta$ 且 $j \le j_1$，并且对于某个 $(\sigma, \bar{\tau}_1) \in T_{\lambda_1} \cap \omega^{S(j)} \times \omega^{S(j)}$，有 $p_{\beta, \lambda_1}(\bar{\tau}_1) = \tau$。

我们声称 $\lambda_1 <_o \lambda$。否则，$\lambda <_o \lambda_1$ 且因此 $\beta_{j, \lambda_1} \le_o \beta <_o \lambda_1$。换句话说，$\lambda_1 \in \Lambda(\lambda)$。将 (2) 应用于 $\lambda$，得到 $(\sigma, p_{\lambda, \lambda_1}(\bar{\tau}_1)) \in T_\lambda$。于是

$$
p_{\beta, \lambda}(p_{\lambda, \lambda_1}(\bar{\tau}_1)) = p_{\beta, \lambda_1}(\bar{\tau}_1) = \tau,
$$

产生矛盾。

因此 $\lambda \in \Lambda(\lambda_1)$。注意，不存在 $(\sigma, \bar{\tau}) \in T_\lambda \cap \omega^{S(j)} \times \omega^{S(j)}$ 使得 $p_{\lambda, \lambda_1}(\bar{\tau}) = \bar{\tau}_1$。将上述过程重复，将 $\beta$ 和 $(\sigma, \tau)$ 分别替换为 $\lambda_1$ 和 $(\sigma, \bar{\tau}_1)$，我们看到存在一个 $\lambda_2 \in \Lambda(\lambda_1)$ 和 $\beta_{j_1, \lambda_2} \le_o \lambda_1 <_o \lambda_2$ 使得 $\lambda_2 <_o \lambda$，

$(\sigma, \tau_j) \in T_{\lambda_i}$ 且 $p_{\beta_{j, \lambda_i}}(\tau_j) = \tau_i$。由此可知，存在一个极限序数的递增序列 $\lambda_1 <_o \lambda_2 <_o \cdots <_o \lambda$，使得对于每个 $i \in \omega$，$\beta_{j, \lambda} <_o \lambda_i$，这与引理 11.2.7 (iv) 矛盾。

对于 $\gamma \succeq \beta$，通过对 $\beta \preceq_o \beta_{c, o}$ 的归纳定义映射 $\psi_{\gamma, \beta} : T_\gamma^\infty \to T_\beta^\infty$。如果 $\beta = 0$，则 $\psi_{0, 0}$ 是恒等映射。在以下内容中，$\psi_{\beta, \beta}$ 始终是恒等映射。

如果 $\gamma \succ \beta$，则 $\psi_{\gamma, \beta} = \psi_{\gamma, \beta'} \cdot \psi_{\beta', \beta}$。如果 $\lambda$ 是极限序数，那么对于使得 $\beta \le_o \beta_{j, \lambda} <_o \lambda$ 的 $j$ 和 $\sigma \in T_\lambda^\infty \cap \omega^{<j}$，根据 (2) 和引理 11.2.8，有 $\sigma \in T_\beta^\infty$。定义 $\psi_{\lambda, \beta}(\sigma) = \psi_{\beta_{j, \lambda}, \beta}(\sigma)$。

注意，在 $\beta = \beta_{j, \lambda}$ 的情况下，有 $\psi_{\lambda, \beta}(\sigma) = \psi_{\beta_{j, \lambda}, \beta}(\sigma) = \sigma$。我们证明 $\psi_{\lambda, \beta}$ 定义良好。

### 引理 11.2.9.

设 $\delta \le_o \beta_{c, o}$。

- (i) 如果 $\beta \le_o \delta$，则 $\psi_{\delta, \beta}$ 定义良好。
- (ii) 对于 $\beta \le_o \beta_1 \le_o \delta$，$\psi_{\delta, \beta} = \psi_{\beta_1, \beta} \circ \psi_{\delta, \beta_1}$。
- (iii) 对于 $\beta \le_o \delta$ 和 $\sigma, \tau \in T_\beta^\infty$，$\sigma \le_T \psi_{\delta, \beta}(\sigma) \succeq \psi_{\delta, \beta}(\tau)$。而且，$|\psi_{\delta, \beta}(\sigma)| \ge |\sigma|$。
- (iv) 存在一个递归函数 $g$，使得对于每个 $\beta \le_o \delta$，$\psi_{\delta, \beta} = g^{\psi_{\delta, \beta}(\beta)}$。

证明。我们通过对 $\delta$ 的归纳同时证明 (i) 和 (ii)。根据 $\psi_{\delta, \beta}$ 的定义，唯一非平凡的情况是 $\delta = \lambda$ 对于某个极限序数 $\lambda$。

对于 (i)，固定 $\alpha <_o \lambda$ 和 $\beta \le_o \beta_{j_0, \lambda} <_o \beta_{j_1, \lambda} <_o \lambda$，其中 $j_0 < j_1$。假设 $\sigma \in T_\lambda^\infty \cap \omega^{<j_0}$ 且 $j_0$ 用于定义 $\psi_{\lambda, \beta}(\alpha)$。根据 (2) 和引理 11.2.8，$\sigma \in T_{\beta_{j_0, \lambda}}^\infty \cap T_{\beta_{j_1, \lambda}}^\infty$。注意，对于任何满足 $\beta_{j_0, \lambda} <_o \gamma \le_o \lambda$ 的 $\gamma$，都有 $\lambda \in \Lambda(\gamma)$ 且 $j(\gamma) \ge j_0$。根据 (6) 以及对 $\gamma$ 在 $(\beta_{j_0, \lambda}, \lambda]$ 上的归纳，$\psi_{\gamma, \beta_{j_0, \lambda}}(\sigma) = \sigma$。用同样的论证，对于 $\gamma$ 在 $(\beta_{j_1, \lambda}, \lambda]$，有 $\psi_{\gamma, \beta_{j_1, \lambda}}(\sigma) = \sigma$。因此，通过对 $\beta$ 的归纳，$\psi_{\lambda, \beta}(\sigma) = \psi_{\beta_{j_0, \lambda}, \beta}(\psi_{\lambda, \beta_{j_0, \lambda}}(\sigma)) = \psi_{\beta_{j_0, \lambda}, \beta}(\psi_{\beta_{j_1, \lambda}, \beta_{j_0, \lambda}}(\sigma)) = \psi_{\beta_{j_1, \lambda}, \beta}(\psi_{\lambda, \beta_{j_1, \lambda}}(\sigma)) = \psi_{\beta_{j_1, \lambda}, \beta}(\sigma)$。故 $\psi_{\delta, \beta}$ 定义良好。

对于 (ii)，给定使得 $|d| < j$ 且 $\beta \le_o \beta_1 <_o \beta_{j, \lambda} \le_o \lambda$ 的 $j$。则 $\psi_{\lambda, \beta_1}(\sigma) = \sigma$。根据 $\psi_{\lambda, \beta_1}$ 的定义，$\psi_{\lambda, \beta}(\sigma) = \psi_{\beta_1, \beta}(\sigma)$。然后通过归纳，$\psi_{\beta_1, \beta}(\sigma) = \psi_{\beta_1, \beta}(\psi_{\lambda, \beta_1}(\sigma))$。

我们通过使用 (5i) 和 (5ii) 以及对 $\beta$ 的归纳得到 (iii)。最后，(iv) 从 (3) 得出。

如果 $x \in [T_\beta^\infty]$，令 $\psi_{\beta, \delta}(x) = \cup_{m < \omega} \psi_{\beta, \delta}(x \upharpoonright m)$。根据引理 11.2.9 (iii)，$\psi_{\delta, \beta}$ 定义良好。

### 引理 11.2.10.

对于任何 $\beta \le_o \gamma \le_o \beta_{c, o}$，$\psi_{\gamma, \beta} : [T_\gamma^\infty] \to [T_\beta^\infty]$ 是一个同胚。

证明。这是通过对 $\gamma$ 的归纳证明的。首先，(5) 意味着唯一非平凡的情况是 $\gamma = \lambda$，一个极限序数。

对于 $x \in [T_\gamma^\infty]$ 和 $m \in \omega$，选择 $j_m > m$ 使得 $\beta <_o \beta_{j_m, \lambda}$。通过归纳，存在唯一的 $z_m \in [T_{\beta_{j_m, \lambda}}]$ 使得 $\psi_{\beta_{j_m, \lambda}, \beta}(z_m) = x$。根据引理 11.2.9 (iii)，$\psi_{\beta_{j_m, \lambda}, \beta}(z_m \upharpoonright m) \succeq x \upharpoonright m$。令 $\sigma_m = z_m \upharpoonright m$。根据引理 11.2.9 的 (ii) 和 (iii)，存在 $z = \cup_m \sigma_m$。由于 $j_m > m$，对于每个 $m$ 都有 $\sigma_m \in T_\lambda$。因此 $z \in [T_\beta^\infty]$。而且，



\(\psi_{\beta, \Lambda}(\sigma_m) = \psi_{\beta_{<m}, \Lambda}(\psi_{\beta, \beta_{<m}}(\sigma_m)) = \psi_{\beta_{<m}, \Lambda}(\sigma_m) = x \mid m\)。因此 \(\psi_{\Lambda, \beta}(z) = x\)。换句话说，\(\psi\) 是满射。

现在假设 \(x_0, x_1 \in [T^0_\beta]\)，\(x_0 \mid n_0 = x_1 \mid n_0 = \sigma_0\)，\(x_0 \succ \sigma' k_0\)，\(x_1 \succ \sigma' k_1\)，其中 \(k_0 \neq k_1\)。令 \(j > |\sigma| + 1\) 使得 \(\beta_{j, \Lambda} > \beta\)。则 \(\psi_{\beta, \beta_{j, \Lambda}}(x_0 \mid [\sigma] + 1) = x_0 \mid [\sigma] + 1 \uparrow x_0 \mid [\sigma] + 1 = \psi_{\beta, \beta_{j, \Lambda}}(x_1 \mid [\sigma] + 1)\)。由归纳法，对于任意 \(y_0 \succ x_0 \mid [\sigma] + 1\) 和 \(y_1 \succ x_1 \mid [\sigma] + 1\)，有 \(\psi_{\beta, \beta_{j, \Lambda}}(y_0) \neq \psi_{\beta, \beta_{j, \Lambda}}(y_1)\)。由引理 11.2.9 (ii)，\(\psi_{\Lambda, \beta}(x_0) \neq \psi_{\Lambda, \beta}(x_1)\)。

因此，对于 \(\gamma = \Lambda\)，\(\psi_{\gamma, \beta}\) 是 \([T^0_\gamma]\) 和 \([T^0_\beta]\) 之间的双射。显然 \(\psi_{\gamma, \beta}\) 和 \(\psi^{-1}_{\gamma, \beta}\) 都是连续的。因此 \(\psi_{\gamma, \beta}\) 是同胚。

由 (3)，\(T^0_\beta\) 是递归树。由递归定理，可以假设已经存在一个满足 (1)-(6) 的系统。我们从 \(T_{\beta^*}\) 定义 \(T_\beta\)。令 \(T^1_\beta = P_{\beta, \beta_{<\Lambda}}(T^{0\beta\sigma})\) 为递归树。递归地计算 \(f(\beta)\)。

对于 \(\sigma \in \omega^{<\beta}\)，令 \(T^{0\beta}_\sigma\) 为由引理 11.2.5 得到的 \(\theta^{(\beta)}\)-递归树，其中将 \(T\) 替换为 \(\{\tau \mid \sigma' \tau \in T^{0\beta}_\sigma\}\)，将 \(x\) 替换为 \(\theta^{(\beta)}\)。将引理 11.2.6 相对化到 \(\theta^{(\beta)}\)（将 \(T_0\) 替换为 \(T^{0\beta}_{\sigma, \sigma}\)），我们得到一个 \(\theta^{(\beta)}\)-递归同胚 \(\psi_\sigma : T^{0\beta}_{\sigma, \sigma} \to T^{0\beta}_{\sigma, \sigma}\)，其中 \(T^{0\beta}_{\sigma, \sigma}\) 是引理 11.2.6 中的 \(T_1\)。定义 \(T^0_\beta\) 为一个 \(\theta^{(\beta)}\)-递归树，使得 \(\tau \in T^0_\beta\) 当且仅当以下条件之一成立：

- \((\tau, P^0_{\beta^*, \Lambda}(\forall \beta' \langle j[\beta']\rangle) \in T_\alpha \cap \alpha \omega^{S(\beta)} \times \alpha \omega^{S(\beta)}\) 对于某些 \(\lambda \in \Lambda(\beta)\) 成立，或
- \(\tau = (\tau \uparrow j[\langle \beta' \rangle] \uparrow \tau'\) 对于某些 \(\tau' \in T^0_{\beta, \tau \uparrow j[\langle \beta' \rangle]}\) 成立。

定义 \(\psi_{\beta^*, \beta} \le_T \theta^{(\beta)} : T^0_{\beta^*} \to T^0_\beta\) 使得

- 如果 \((\tau, P^0_{\beta^*, \Lambda}(\forall \beta' \langle j[\beta']\rangle)) \in T_\alpha \cap \alpha \omega^{S(\beta)} \times \alpha \omega^{S(\beta)}\) 且 \(\lambda \in \Lambda(\beta)\)，则 \(\psi_{\beta^*, \beta}(\tau) = \tau\)；
- 否则，令 \(\tau = (\tau \uparrow j[\langle \beta' \rangle] \uparrow \tau'\)。定义 \(\psi_{\beta^*, \beta}(\tau) = \tau \uparrow j[\langle \beta' \rangle] \uparrow \psi_{\theta(\beta)}(\tau' \uparrow (\oplus_{\beta \in \beta^*} \uparrow \tau' \uparrow))\)。

因此，对于任意 \(x \in T^0_\beta\)，
\((x \oplus \theta(\beta))' \equiv_T x \oplus \theta(\beta') \equiv_T \psi^{-1}_{\beta^*, \beta}(x) \oplus \theta(\beta')\)。

注意 \(T^0_\beta = T^0_{\beta^d}\)（参见 (3)），其中 \(d\) 与 \(\beta\) 无关。定义 \(T_\beta\) 使得 \((\sigma, \tau) \in T_\beta\) 当且仅当以下条件之一成立：

- 存在某些 \(\lambda \in \Lambda(\beta)\) 的 \((\sigma, \tau) \in T_\alpha \cap \alpha \omega^{S(\beta)} \times \alpha \omega^{S(\beta)}\) 使得 \(\tau = p_{\beta, \Lambda}(\tau)\)，或
- 或存在 \(\tau' \succeq \tau\) 使得 \(\tau' \in T^1_\beta\)，\(\forall^0_{\beta^*}(\sigma)(\uparrow \tau' \uparrow) = 1\)，且 \((\sigma \uparrow j[\langle \beta' \rangle], \tau' \uparrow j[\langle \beta' \rangle]) \in T_\alpha\) 对于某些 \(\lambda \in \Lambda(\beta)\) 和 \(\tau'\) 使得 \(\tau' = p_{\beta, \Lambda}(\tau' \uparrow)\)。

那么树 \(T_\beta\) 即为所需。由于构造是一致的，(1)-(6) 的其余部分随之成立。这完成了定理 11.2.2 的证明。

由 \(\Sigma^1_1\)-有界性，我们有以下推广：

#### 推论 11.2.11 (Harrington). 存在一个不可数的 \(\Pi^1_2\)-集合 \(A\)，使得对于任何递归序数 \(\beta\) 和 \(x \in A\)，\(x^{(\beta)} \not\ge_T 0^{(\beta+1)}\)。

证明。假设不然。令 \(B = \omega \times \omega^{<\omega}\) 为算术集，使得 \([\{B_e\}]_{e < \omega}\)，其中 \(B_e = \{ \alpha \in \omega^{<\omega} \mid (e, \alpha) \in B \}\)，是所有 \(\Pi^1_1\)-子集的递归列表，子集属于 \(\omega^{<\omega}\)。令 \(O \subseteq \Theta\) 如定理 2.6.5 所定义。

回顾一下，满足 (1)–(6) 的系统是通过固定一个序数记号 \(n\) 且 \(|n| \ge \omega\) 得到的。令 \(e_0\) 使得 \(3 \cdot 5^{e_0} = \omega\)。定义一个 \(\Pi^1_1\)-关系 \(R \subseteq \omega \times \omega\) 使得

$R(e, n) \Leftrightarrow 3 \cdot 5^{e_0} \le_\Theta n \wedge n \in \Theta \wedge$

不存在满足 (1)–(6) 的系统用于 \(n\) 且 \(B_e = T_0^0\)。

然后由定理 4.2.1 和假设，存在一个 \(\Pi^1_1\) 全函数，因此也是 \(\Delta^1_1\)，关于 \(R\) 的一致化函数 \(f : \omega \to O\)。令 \(I = \{ e \mid [B_e] > \aleph_0 \}\)。由定理 11.10，\(I\) 是 \(\Sigma^1_1\)。由推论 11.5.2，存在一个 \(n \in O\) 使得对所有 \(m \in I\)，\(f(e) \in e \mid I\)，我们有 \(m <_\Theta n\)，这与上面的证明矛盾。

因此存在一个 \(e \in I\) 使得 \(B_e = T_0^0\)，并且对于每个 \(n \in O\) 且 \(|n| \ge \omega\)，存在一个满足 (1)–(6) 的系统。由上面的证明，\(H_n^1 \not\ge_T H_{2n}\)。

#### 11.2.2 练习

- 练习 11.2.1. 证明在定理 11.2.1 中，集合 \(A\) 可以选为 \(2^\omega\) 的子集。
- 练习 11.2.2 (Harrington). 存在一条穿过 \(\Theta\) 的 \(\Pi^1_1\)-路径，使得在其中递归的超算术实数只有递归实数。
- 练习 11.2.3 (Harrington). 证明对于任何递归序数 \(\beta < \omega_1^{CK}\)，存在 \(2^\omega\) 中的两个 \(\Pi^1_1\)-单点 \(x\) 和 \(y\)，使得 \(x^{(\beta)} \not\ge_T y\) 且 \(y^{(\beta)} \not\ge_T x\)。
- 练习 11.2.4 (Harrington). 证明存在 KP 的过渡模型 \(N\) 使得 \(N \models \text{“并非每个 } \Delta^1_1\text{-实数都是超算术的”}\)。

## 11.3 L 中的完美集

#### 11.3.1 普里克里的问题

在 [98] 中，Prikry 提出了以下问题。

#### 问题 11.3.1. 假设存在一个非可构实数。每个完美集是否包含一个非可构实数？

Friedman [29] 也提出了与问题 11.3.1 相关的问题：

#### 问题 11.3.2. 假设存在一个非可构实数。\(L \cap \mathbb{R}\) 是 \(\Sigma^1_1\)-集合吗？

由定理 11.1.10，问题 11.3.1 的肯定回答将蕴含问题 11.3.2 的否定解答。后者由 Velickovic 和 Woodin 给出了否定解答：

#### 定理 11.3.1 (Velickovic 和 Woodin ([66]). 如果可构实数的集合是 \(\Sigma^1_1\)，那么要么 \(\omega_1^{ck}\) 是可数的，要么每个实数都是可构的。

另一方面，问题 11.3.1 由 Groszek 和 Slaman [41] 给出了肯定回答，该解答将在下一节中讨论。

#### 定理 11.3.4. 如果存在一个完美集 \(A \subseteq (2^\omega)^L\)，那么每个实数都是可构的。

#### 11.3.2 定理 11.3.4 的证明

给定一个树 \(T \subseteq 2^{<\omega}\)，集合 \(A \subseteq 2^\omega\) 在 \(T\) 中是稠密的，如果对于任何 \(\sigma \in T\)，\([\sigma] \cap T \cap A \neq \emptyset\)。实数 \(x \in [T]\) 在 \(T\) 中是最终常数的，如果存在一个 \(n\) 使得 \(x\) 是 \([x \restriction n] \cap T\) 中最左或最右的无限路径。

#### 引理 11.3.5. 设 \(T\) 为完美树。假设 \(\{g_i\}_{i<\omega} \in L\) 包含 \(T\) 的一个稠密子集，其中没有成员在 \(T\) 中是最终常数的。那么对于任意 \(z\)，存在 \(x, y \in [T]\) 使得 \(x \oplus y \oplus (\oplus_{i<\omega} g_i) \ge_T z\)。

假设引理 11.3.5。设 \(T\) 为完美树，使得 \([T] \subseteq L\)。那么 \((\omega_1)^L = \omega_1\)。从 \([T]\) 中选取一个可数序列 \(\{x_i\}_{i<\omega}\)，使其稠密且没有 \(x_i\) 是最终常数的。由于 \((\omega_1)^L = \omega_1\)，存在 \(x^* \in L\) 使得对每个 \(i < \omega\) 有 \(x_i <_L x^*\)。令 \(\{g_i\}_{i<\omega}\) 为集合 \(\{x \mid x <_L x^*\}\) 的一个枚举。注意 \(\{g_i\}_{i<\omega}\) 属于 \(L\)。由引理 11.3.5，对于每个 \(z\)，存在 \(x, y \in [T]\)，因此也在 \(L\) 中，使得 \(x \oplus y \oplus (\oplus_{i<\omega} g_i) \ge_T z\) 且 \(z \in L\)。

证明的思路如下。假设 \(z\) 是给定的实数，\(T\) 是完美的，且 \(\{g_i\}_{i<\omega} \in L\) 是一个序列，其中包含 \(T\) 的一个稠密子集，且没有元素在 \(T\) 中是最终常数的。我们定义 \(x \in [T]\) 和一个索引函数 \(h_x : \omega \to \omega\)，使得对每个 \(i\)，\(h_x(i)\) 是穿过 \(T\) 且在 \(T\) 中不是最终常数的路径。集合 \(x\) 在 \(i\) 增大时与 \(g_{h_x(i)}\) 在越来越长的初始段上一致，并且 \(z\) 被编码进 \(x\) 和 \(\{g_{h_x(i)}\}_{i<\omega}\) 中，使得 \(z(i)\) 是 \(x\) 在第一个与 \(g_{h_x(i)}\) 不同的位置上的值。很容易看出 \(z \le_T x \oplus h_x \oplus (\oplus_{i<\omega} g_i)\)。递归地定义这样的 \(x\) 和 \(h_x\) 没有问题。

挑战在于解码 \(h_x\)。通过定义另一个实数 \(y \in [T]\) 使得 \(h_x \le_T x \oplus y \oplus (\oplus_{i<\omega} g_i)\) 来处理这个问题。为了实现这一点，我们定义一个额外的索引函数 \(h_y : \omega \to \omega\) 具有相同的性质（除了这里不编码 \(z\)），这样 \(h_x\) 和 \(h_y\) 可以从 \(x\)、\(y\) 和 \(\oplus_{i<\omega} g_i\) 中计算出来。

#### 引理 11.3.5 的证明. 我们现在描述集合 \(x\)、\(y\) 和函数 \(h_x, h_y\) 的构造。





第 0 阶段。令 \(\sigma_0\) 和 \(\tau_0\) 为 \(T\) 扩展其根的第一个分裂节点，即 \(T\) 的一个分裂节点，使得 \(T\) 中的每个节点都扩展 \(\sigma_0\) 或 \(\tau_0\)。令 \(h_x(0)\) 为最小的 \(i\)，使得 \(T_i \models [z^\frown \sigma] \cap [T]\)，并令 \(h_y(0)\) 为最小的 \(j\)，使得 \(g_j \models [\tau_0] \cap T\)。

第 \(n + 1\) 阶段。假设由归纳假设可知，\(\sigma_n\) 和 \(\tau_n\) 是 \(T\) 中的分裂节点，且 \(\sigma_n z^n(n)\) 和 \(\tau_n h_n(n)\)。

子阶段 (a)。定义 \(j_0\) 为最小的索引 \(j\)，使得 \(g_j \in [\sigma_n (1 - z(n))] \cap [T]\) 不是最终常数。令 \(m_0\) 为最小的 \(m > |\tau_n|\)，使得对每个 \(i < j_0\) 都有 \(g_i \models m_i \neq g_{j_0} \models m\)。令 \(m_1\) 为最小的 \(m > m_0\)，使得 \(g_{h_n(n)} \models m\) 是 \(T\) 中的一个分裂节点。令 \(t' = g_{h_n(n)} \models m_i \models (1 - g_{h_n(n)}(m_i))\)。那么对于 \(i < j_0\) 都有 \(g_i \models m_i \neq g_{j_0} \models m\)，且节点 \(m_1\) 是最小的 \(m\)，使得 \(t' \models m \neq g_{h_n(n)}(m)\)。

子阶段 (b)。令 \(j_1\) 为最小的 \(j\)，使得 \(g_j \in [t'] \cap [T]\)。令 \(m_2\) 为最小的 \(m\)，使得对任何 \(i < j_1\) 都有 \(g_i \models m \neq g_{j_1} \models m\)。由于 \(g_{j_0}\) 不是最终常数，我们可以选择 \(m_3\) 为最小的 \(m > m_2\)，使得 \(g_{j_0} \models m\) 是 \(T\) 中的一个分裂节点且 \(g_{j_0} > g_{j_0} \models m_i (n + 1)\)。那么对于 \(i < j_1\) 都有 \(g_i \models m_i \neq g_{j_1} \models m_3\)。令 \(\sigma_{n+1} = g_{j_0} \models m_3\)，\(\tau_{n+1} = g_{j_1} \models m_3\)，\(h_x(n + 1) = j_0\) 和 \(h_y(n + 1) = j_1\)。

令 \(x = \bigcup_{n < \omega} \sigma_n\) 和 \(y = \bigcup_{n < \omega} \tau_n\)。这就完成了构造。

该构造保证，对于每个 \(n\)，\(h_x(n + 1)\) 是最小的 \(i\)，使得 \(g_i \models m_i = x \models m_1\)，其中 \(m_1\) 是满足 \(y(m) \neq g_{h_n(n)}(m)\) 的最小 \(m\)。同样，\(h_y(n + 1)\) 是最小的 \(i\)，使得 \(g_i \models m_3 = y \models m_3\)，其中 \(m_3\) 是满足 \(x(m) \neq g_{h_n(n+1)}(m)\) 的最小 \(m\)。因此 \(h_x \leq_T y \leq_T x \oplus y \oplus (\exists_{i < \omega} g_i)\)，从而 \(z \leq_T x \oplus y \oplus (\exists_{i < \omega} g_i)\)。

### 11.3.3 练习

练习 11.3.1。证明在没有“没有 \(T\) 中的元素是最终常数的”条件下，引理 11.3.5 依然成立。

*练习 11.3.2 (Harrington)。证明对于任何不是稀疏的 \(\Pi^1_1\)-集 \(A \subseteq 2^\omega\)，\(A\) 包含一个超算术指向的完美树 \(T\)，即对于每个 \(x \in [T]\) 都有 \(T \leq_h x\)。

## 12 经典算法随机性回顾

我们假设读者熟悉经典算法随机性理论，并在此章节对该主题进行回顾。详情见 [111] 和 [24]。

### 12.1 通过测度论的随机性

直观上，一个随机实数应当通过每个可行的统计检验。这就是使用测度论来定义随机性的动机。在测度论语言中，检验与一个零集相关联。以下是测度论随机性关键概念的摘要。

#### 12.1.1 Kurtz 和 Schnorr 随机性

（现在称为）Kurtz 随机性的概念由 Kurtz [79] 引入。

**定义 12.1.1.** (i) 一个集 \(A \subseteq 2^\omega\) 是一个 *Kurtz 检验*，如果它是 \(\Pi^0_1\) 且 \(\mu(A) = 0\)；(ii) 一个实数 \(x\) 是 *Kurtz 随机*，如果对于每个 Kurtz 检验 \(A\) 都有 \(x \notin A\)。

**定义 12.1.2** (Schnorr [125] 和 [127])。(i) 一组开集 \(\{U_n\}_{n<\omega}\) 是一个 *Schnorr 检验*，如果 \(\{(n, \sigma) \mid \sigma \in U_n\}\) 是递归可枚举的且对每个 \(n < \omega\) 都有 \(\mu(U_n) = 2^{-n}\)；(ii) 一个实数 \(x\) 是 *Schnorr 随机*，如果对于每个 Schnorr 检验 \(\{U_n\}_{n<\omega}\) 都有 \(x \notin \bigcap_{n<\omega} U_n\)。

**命题 12.1.3** (Terwijn 和 Zambella [163])。一个实数 \(x\) 是 Schnorr 随机，当且仅当对于每一组开集 \(\{V_n\}_{n<\omega}\)，若 \(\{(n, \sigma) \mid \sigma \in V_n\}\) 是递归可枚举的且对某个递归函数 \(f\) 有 \(\mu(V_n) = 2^{-f(n)}\)，则 \(x \notin \bigcap_{n<\omega} V_n\)。

#### 12.1.2 Martin-Löf 随机性

Kurtz 和 Schnorr 随机性的概念都证明有些限制且不尽令人满意。接下来由 Martin-Löf 提出的概念，或许是迄今为止研究最广泛的。

**定义 12.1.4** (Martin-Löf [96])。(i) 一组开集 \(\{U_n\}_{n<\omega}\) 是一个 *Martin-Löf 检验*，如果 \(\{(n, \sigma) \mid \sigma \in U_n\}\) 是递归可枚举的且对每个 \(n < \omega\) 都有 \(\mu(U_n) < 2^{-n}\)；(ii) 一个实数 \(x\) 是 *Martin-Löf 随机*，如果对于每个 Martin-Löf 检验 \(\{U_n\}_{n<\omega}\) 都有 \(x \notin \bigcap_{n<\omega} U_n\)。

下一个结果表明，Martin-Löf 随机性由单个检验决定。

**命题 12.1.5** (Martin-Löf [96])。*存在一个通用的 Martin-Löf 检验。也就是说，存在一个 Martin-Löf 检验* \(\{U_n\}_{n<\omega}\) *，使得对每个 Martin-Löf 检验* \(\{V_n\}_{n<\omega}\) *都有* \(\bigcap_{n<\omega} V_n \subseteq \bigcap_{n<\omega} U_n\)。

#### 12.1.3 强 Martin-Löf 随机性

**定义 12.1.6** (Kurtz [79])。
(i) 一组开集 \(\{U_n\}_{n<\omega}\) 是一个广义 Martin-Löf 检验，如果 \(\{(n, \sigma) \mid \sigma \in U_n\}\) 是递归可枚举的且 \(\lim_{n \to \infty} \mu(U_n) = 0\)；
(ii) 一个实数 \(x\) 是强 Martin-Löf 随机，如果对于任何广义 Martin-Löf 检验 \(\{U_n\}_{n<\omega}\) 都有 \(x \notin \bigcap_{n<\omega} U_n\)。

强 Martin-Löf 随机性具有一些 Martin-Löf 随机性所不具备的正则性性质。

#### 12.1.4 相对化随机性

上述每个概念都可以相对化到任意实数 \(x\)。例如，一个 \(x\)-Martin-Löf 检验是一组开集 \(\{U_n\}_{n<\omega}\)，使得 \(\{(n, \sigma) \mid \sigma \in U_n\}\) 是 \(x\)-递归可枚举的且对每个 \(n \in \omega\) 都有 \(\mu(U_n) < 2^{-n}\)。那么 \(z\) 是 \(x\)-Martin-Löf 随机，如果对于任何 \(x\)-Martin-Löf 检验 \(\{U_n\}_{n<\omega}\) 都有 \(z \notin \bigcap_{n<\omega} U_n\)。特别是，\(z\) 是 \(n\)-随机，如果 \(z\) 是 \(0^{(n-1)}\)-Martin-Löf 随机。

以下被称为 van Lambalgen 定理。

**定理 12.1.7** (van Lambalgen [165])。\(x \oplus y\) 是 Martin-Löf 随机，当且仅当 \(x\) 是 Martin-Löf 随机且 \(y\) 是 \(x\)-Martin-Löf 随机，也当且仅当 \(y\) 是 Martin-Löf 随机且 \(x\) 是 \(y\)-Martin-Löf 随机。

Martin-Löf 随机性似乎是唯一使得 van Lambalgen 定理成立的随机性概念。

#### 12.1.5 随机性概念的相对强度

上述引入的随机性概念的相对强度可总结如下。注意蕴含关系不可逆：

- 强 Martin-Löf 随机性 \(\Rightarrow\) Martin-Löf 随机性
- \(\Rightarrow\) Schnorr 随机性
- \(\Rightarrow\) Kurtz 随机性

一个实数 \(x\) 是 *递归主导的*，如果每个函数 \(f \le_T x\) 都被某个递归函数主导。以下结果给出了递归主导实数的强 Martin-Löf 随机性的刻画。

**命题 12.1.8 (Yu)**。如果 \(x\) 是递归主导的，那么 \(x\) 是强 Martin-Löf 随机，当且仅当它是 Kurtz 随机。

接下来是用 Schnorr 随机性刻画 Martin-Löf 随机性。

**定理 12.1.9 (Nies, Terwijn 和 Stephan [112])。** 对于任何实数 \(x\)，
(i) 如果 \(x\) 是 Schnorr 随机且 \(x' \not\ge_T 0''\)，那么 \(x\) 是 Martin-Löf 随机；
(ii) 如果 \(x' \ge_T 0''\)，那么存在一个 Schnorr 随机实数 \(y \equiv_T x\)，使得 \(y\) 不是 Martin-Löf 随机。

#### 12.1.6 随机实数的计算能力

以下定理表明，随机实数可能具有非常强的计算能力：

**定理 12.1.10 (Kučera [76])。** *对于任何实数* \(x \ge_T 0'\) *，存在一个 Martin-Löf 随机实数* \(z \equiv_T x\)。

出人意料的是，强 Martin-Löf 随机性并不得出相同的结论：

**定理 12.1.11 (Downey, Nies, Weber, Yu [23] 和 Hirschfeldt, Miller)。** *一个实数* \(x\) *是强 Martin-Löf 随机，当且仅当* \(x\) *是 Martin-Löf 随机且图灵不计算任何非递归的* \(\Delta_2^0\)*-实数。*

在算法随机性理论中，有一个论点认为 *随机性越多，计算能力越少*。虽然一个随机实数 \(x\) 包含大量信息，但这些信息在计算上可能是无用的，因为它不能用来预测除集合 \(x\) 本身之外的任何集合。文献中有大量证据支持这一论点。我们举一些例子。

**定义 12.1.12。** 设 \(h\) 为一个函数。一个实数 \(x\) 是 \(h\)-对角非递归的，缩写为 \(h\)-DNR，如果存在一个函数 \(f \le_T x\)，使得对每个 \(e < \omega\) 都有 \(f(e) \neq \Phi_e(e)\) 且 \(f(e) < h(e)\)。我们说 \(x\) 是 DNR，如果存在一个函数 \(f \le_T x\)，使得对 \(e < \omega\) 都有 \(f(e) \neq \Phi_e(e)\)。

下一个定理表明，没有不完备的 Martin-Löf 随机实数是 2-DNR。

**定理 12.1.13 (Stephan)。** *假设* \(x \in 2^\omega\) *是 Martin-Löf 随机。那么* \(x\) *是* 2*-DNR，当且仅当* \(x \ge_T 0'\)。





定理 12.1.13 有一个有趣的推论。根据低基定理（练习 1.5.3），存在一个实数 x，它是 2-DNR 且 x' ≡_T 0'。根据命题 12.1.5，存在一个非空的 Π^0_1 集合，其中仅包含 Martin-Löf 随机实。因此存在一个 Martin-Löf 随机实 z ≤_T x，因为每个 2-DNR 实数都图灵计算任何给定的非空 Π^0_1 集合的一个元素。根据定理 12.1.13，不存在与 x 图灵等价的随机实。因此我们有以下结论：

**定理 12.1.14** (Kučera [76]). Martin-Löf 随机实的图灵度集合不是向上封闭的。

另一方面，Martin-Löf 随机实的图灵度可能是向下封闭的，如下所示。

**定理 12.1.15** (Demuth [20]). 任何 y >_T 0 若对某个 Martin-Löf 随机实真值表可归约，则它与某个 Martin-Löf 随机实图灵等价。

显然，每个图灵可归约于某个递归支配实 x 的实数都对 x tt-可归约。因此，Martin-Löf 随机实的图灵度集合对于递归支配的随机实是向下封闭的。下列结果为随机性论题提供了另一项证据。

**定理 12.1.16** (Miller and Yu [103]). 对于任意 z，如果 x ≤_T y 都是 Martin-Löf 随机且 y 是 z-Martin-Löf 随机，那么 x 也是。

#### 12.1.7 练习

- **练习 12.1.1.** 证明不存在通用 Kurtz 测试。

- **练习 12.1.2** (Schnorr [127]). 证明不存在通用 Schnorr 测试。

- **练习 12.1.3** (Downey, Nies, Weber and Yu [23]). 证明不存在通用广义 Martin-Löf 测试。

- **练习 12.1.4** (Merkle et al. [99], Yu [170], and Kjos-Hanssen). 证明 van Lambalgen 定理对 Schnorr 随机性不成立。

## 12.2 通过复杂性理论的随机性

直觉上，一个随机实不被其任何部分信息所预测，且其内容的任何信息都不可压缩。这是用复杂性来定义随机性的基础。

#### 12.2.1 普通柯尔莫哥罗夫复杂度

**定义 12.2.1** (Solomonoff [146] 和 Kolmogorov [73]). 给定一个图灵机 $M$ 和一个有限字符串 $\sigma \in 2^{<\omega}$，$\sigma$ 的 $M$-Kolmogorov 复杂度 $C_M(\sigma)$ 为 $\min\{|\tau| \mid M(\tau) = \sigma\}$。

如果 $U$ 是通用图灵机，那么对于任何图灵机 $M$，存在一个常数 $c_M$，使得 \((\forall \sigma)(C_U(\sigma) \le C_M(\sigma) + c_M)\)。

换句话说，$C_U$ 至多相差一个常数是最优的。我们省略下标 $U$ 并用 $C$ 表示普通柯尔莫哥罗夫复杂度函数 $C_U$。然后可以定义一个实数 x 为随机的，如果存在一个常数 $c$，使得 \((\forall n)(C(x \mid n) \ge n - c)\)。然而，对于任何 x 和 n，$x \mid \text{Code}(x \mid n)$（其中 Code(x) 是对字符串 $\sigma$ 进行编码的自然数）可以通过 U 从 $x \mid \text{Code}(x \mid n)$ 的一个末段（记为 $\sigma$）中得到，该末段的长度为 Code(x | n) - n。这是因为一旦 $\sigma$ 已知，就可以找到一个唯一的字符串 $\tau$，使得 $\tau$ 对 $\tau$ 进行编码，即 $|\tau^\frown \sigma| = \text{Code}(\tau)$。此时 $|\tau| = n$ 且 $\tau^\frown \sigma = x \mid \text{Code}(x \mid n)$。因此我们有 $|\tau^\frown \sigma|$ 如下。

**命题 12.2.2** (Martin-Löf). 对于任意实数 x，$\lim_{n} n - C(x \mid n) = +\infty$。

命题 12.2.2 表明，在普通柯尔莫哥罗夫复杂度的意义下不存在随机实，这引出了 Levin 和 Chaitin 引入的下一个定义。

**定义 12.2.3.** (i) 一个集合 $A \in 2^{<\omega}$ 是 *前缀自由* 的，如果对于任何 $\sigma \prec \tau \in 2^{<\omega}$，要么 $\sigma \notin A$ 要么 $\tau \notin A$。 (ii) 一个图灵机 $M$ 是 *前缀自由* 的，如果它的定义域是一个前缀自由集合。

**定义 12.2.4** (Levin [83] 和 Chaitin [9]). 给定一个前缀自由图灵机 $M$ 和一个字符串 $\sigma \in 2^{<\omega}$，$\sigma$ 的 $M$-Kolmogorov 复杂度 $K_M(\sigma)$ 为 $\min\{|\tau| \mid M(\tau) = \sigma\}$。

不难看出存在一个通用前缀自由图灵机 U，我们用 $K(\sigma)$ 表示 $K_U(\sigma)$。下面的技术定理指出了一种构造前缀自由机的方法。

**定理 12.2.5** (Levin [83] 和 Chaitin [9] 和 Schnorr [126]). 设 $\{\langle d_i, \tau_i \rangle\}_{i < \omega} \subseteq \omega \times 2^{<\omega}$ 为一个递归序列，使得 $\sum_{i < \omega} 2^{-d_i} \le 1$。则存在一个前缀自由机 M 和长度为 $d_i$ 的字符串 $\sigma_i$，使得对所有 i 都有 $M(\sigma_i) = \tau_i$ 且 $\text{Dom}(M) = \{\sigma_i \mid i < \omega\}$。此外，M 的一个索引可以从序列的一个索引有效地得到。

下列结果总结了 K 的一些基本性质。

**定理 12.2.6** (Chaitin). (i) $\sum_{\sigma} 2^{-K(\sigma)} \le 1$; (ii) $(\exists c)(\forall \sigma)(K(\sigma) \le |\sigma| + K(|\sigma|) + c)$; (iii) $(\exists c)(\forall n)(\forall k)(|\{\sigma \in 2^n \mid K(\sigma) \le n + K(n) - k\}| \le 2^{n-k+c})$。

#### 12.2.2 通过复杂性刻画随机性

Martin-Löf 随机性与 Kolmogorov 复杂度之间的等价性由以下给出：

**定理 12.2.7** (Schnorr). 一个实数 x 是 Martin-Löf 随机的，当且仅当

```
(∃c)(∀n)(K(x ↾ n) ≥ n - c).
```

Chaitin [9] 给出了一个 Martin-Löf 随机实的“具体”例子：

```
\Omega = \sum_{U(\sigma)\downarrow} 2^{-|\sigma|},
```

并且几种随机性概念已用 Kolmogorov 复杂度进行了刻画。接下来的两个定理分别用普通柯尔莫哥罗夫复杂度刻画了 Martin-Löf 随机性和 2-随机性。

**定理 12.2.8** (Miller and Yu [103]). 一个实数 x 是 Martin-Löf 随机的，当且仅当对于每个递归函数 g 且满足 \sum_{n<\omega} 2^{-g(n)} < \infty，

```
(∃c)(∀n)(C(x ↾ n) ≥ n - g(n) - c).
```

**定理 12.2.9** (Miller [101] 和 Nies, Stephan, Terwijn [112]). 一个实数 x 是 2-随机的，当且仅当

```
(∃c)(∀n)(∃m ≥ n)(C(x ↾ m) ≥ m - c).
```

2-随机性也可以通过前缀自由柯尔莫哥罗夫复杂度如下刻画：

**定理 12.2.10** (Ding, Downey, and Yu [173] 和 Miller [102]). 一个实数 x 是 2-随机的，当且仅当

```
(∃c)(∀n)(∃m ≥ n)(K(x ↾ m) ≥ m + K(m) - c).
```

以下定理给出了 Martin-Löf 随机性与两种复杂度概念之间的联系：

**定理 12.2.11** (Miller and Yu [103]). x ∨ y 是 Martin-Löf 随机的，当且仅当

```
(∃c)(∀n)(K(x ↾ n) + C(y ↾ n) ≥ 2n - c).
```

用普通和前缀自由复杂度比较两个实数有一种自然的方式：

**定义 12.2.12.** 写 x ≤_K y（或 x ≤_C y）当且仅当

```
(∃c)(∀n)(K(x ↾ n) ≤ K(y ↾ n) + c)
```

（或 (∃c)(∀n)(C(x ↾ n) ≤ C(y ↾ n) + c)）。

通过结合 van Lambalgen 定理 12.1.7 和定理 12.2.11，我们有以下结论。

**推论 12.2.13** (Miller and Yu [103]). 假设 $x, y, z$ 都是 Martin-Löf 随机的。如果 $x \le_K y$ 或 $x \le_C y$ 且 $x$ 是 $z$-Martin-Löf 随机的，那么 $y$ 也是。

目前尚不知强 Martin-Löf 随机性是否是 $\le_K$-向上封闭的。根据定理 12.11.0，推论 12.2.13 表明集合中更高的复杂度蕴含更强的随机性。然而，以下两个结果暗示了一幅更微妙的图景。

**定理 12.2.14** (Miller [102]). 如果 $x$ 是 2-随机的，那么 $|\{y \mid x \le_K y\}| = \aleph_0$ 且 $|\{y \mid x \le_C y\}| = \aleph_0$。

**定理 12.2.15** (Miller and Yu [104]). 存在两个 Martin-Löf 随机实 $x$ 和 $y$，使得 $|\{z \mid x \le_K z \le_K y\}| = 2^{\aleph_0}$。

#### 12.2.3 K-平凡性

**定义 12.2.16.** 一个实数 $x$ 是 $K$-平凡的，如果 $(\exists c)(\forall n)(K(x \mid n) \le K(n) + c)$。

因此，一个 $K$-平凡实是远离随机性的实。显然每个递归实都是 $K$-平凡的。然而，$K$-平凡实的类包含非递归成员，它们全部递归于某个固定实。

**定理 12.2.17** (Solovay [151]). 存在一个非递归的 $K$-平凡实。

**定理 12.2.18** (Nies [110]). 如果 $x$ 是 $K$-平凡的，那么 $x' \le_T \emptyset'$。

**定理 12.2.19** (Kučera and Slaman [77]). 存在一个满足 $x' \equiv_T \emptyset'$ 的 $x$，它计算每个 $K$-平凡实。

#### 12.2.4 练习

- **练习 12.2.1** (Miller and Yu [103]). 证明一个实数 $x$ 是 Martin-Löf 随机的，当且仅当 $\sum_{n} 2^{-K(x \mid n)} < \infty$。

- **练习 12.2.2.** 证明 Kurtz 随机性和 Schnorr 随机性都不是 $\le_K$-向上封闭的。

- **练习 12.2.3** (Chaitin [10]). 证明不存在非递归实 $x$ 使得 $(\exists c)(\forall n)(K(x \mid n) \le C(n) + c)$。

- **练习 12.2.4.** 证明存在一个 Kurtz 随机实且是 $K$-平凡的。





## 12.3 对于随机性的低性

#### 12.3.1 一般低性概念

给定一个随机性概念 \(\Gamma\)，我们可以将其相对于一个实数 \(x\) 相对化以得到 \(\Gamma^x\)。定义 \(\text{Low}(\Gamma) = \{x \in 2^\omega \mid \Gamma \subseteq \Gamma^x\}\)。那么 \(\text{Low}(\Gamma)\) 的每个成员都被称为对于 \(\Gamma\) 低。

可以考虑一个稍强的低性概念。由于每个 \(\Gamma\) 都是用 \(\Gamma\)-测试定义的，我们可以说 \(x\) 对于 \(\Gamma\)-测试是低的，如果每个被某个 \(\Gamma\)-测试（作为集合）覆盖的 \(\Gamma^x\) 测试。关于这些的更多细节可以在 [111] 和 [24] 中找到。

因此，如果 \(x \in \text{Low}(\Gamma)\)，那么它不提供关于 \(\Gamma\) 的随机性的任何信息。尽管如此，低性属性似乎有些神秘，因为人们对 \(\text{Low}(\Gamma)\) 成员的复杂性一无所知。经典递归论一个非常重要且成功的应用是刻画各种随机性概念的低性属性。

#### 12.3.2 对于 Kurtz 随机性的低性

**定理 12.3.1** (斯蒂芬·于 [160] 和格林伯格·米勒 [38])。_对于任意实数_ \(x\) _，以下等价：_

- (i) \(x\) 对于 Kurtz 随机性是低的；
- (ii) \(x\) 对于 Kurtz 测试是低的；
- (iii) \(x\) 是递归支配且非 DNR 的。

已知有 \(2^{\aleph_0}\) 个递归支配且非 DNR 的实数。因此，定理 12.3.1 表明存在大量不提供任何关于 Kurtz 随机性信息的实数。

#### 12.3.3 对于 Schnorr 随机性的低性

**定义 12.3.2。** 一个实数 \(x\) 是 _递归可追踪的_，如果对于任何 \(f \le_T x\)，存在一个递归函数 \(g : \omega \to \mathscr{P}_{<\omega}(2^{<\omega})\)，使得对于任何 \(e\)，\(f(e) \in g(e)\) 且 \(|g(e)| \le e\)。

不难看出，每个递归可追踪的实数都是递归支配且非 DNR 的。此外，构造一个递归可追踪的实数与构造一个最小图灵度的集合相当相似。它们都是使用带有递归完美树的 Sacks 强迫法得到的。

**定理 12.3.3** (特尔温·赞贝拉 [163] 和科斯-汉森、尼斯、斯蒂芬 [67])。_对于任意实数_ \(x\) _，以下等价：_

- (i) \(x\) 对于 Schnorr 随机性是低的；
- (ii) \(x\) 对于 Schnorr 测试是低的；
- (iii) \(x\) 是递归可追踪的。

因此，同样存在许多对于 Schnorr 随机性是低的实数。

#### 12.3.4 对于 Martin-Löf 随机性的低性

**定义 12.3.4。** 设 \(\Gamma\) 为一个随机性概念。如果存在一个 \(\Gamma^*\)-随机的 \(y\) 使得 \(x \le_T y\)，则称实数 \(x\) 是 \(\Gamma\) 的一个 _基_。

以下结果是算法随机性理论中最深刻的结果之一。

**定理 12.3.5** (尼斯 [110] 和赫希费尔德、尼斯、斯蒂芬 [48])。_对于任意_ \(x\) _，以下等价：_
(i) _\(x\) 是 K-平凡的；_
(ii) _\(x\) 是 Martin-Löf 随机性的一个基；_
(iii) \((\exists c)(\forall n)(K(n) \le K^c(n) + c)\)；_
(iv) _\(x\) 对于 Martin-Löf 测试是低的；_
(v) _\(x\) 对于 Martin-Löf 随机性是低的。_

随机性基的概念在定理 12.3.5 的证明中尤为重要。请注意，可以将 Martin-Löf 随机性视为最弱的随机性概念，因为它只有可数个基（参见 [27]）。根据定理 12.3.5 中的刻画，尼斯引入了一个新的归约关系 \(\le_{LR}\)：

**定义 12.3.6。** 如果每个 \(y\)-Martin-Löf 随机实数都是 \(x\)-Martin-Löf 随机的，则称 \(x \le_{LR} y\)。

因此，根据定理 12.3.5，\(x \le_{LR} 0\) 当且仅当 \(x\) 是 \(K\)-平凡的。该关系用柯尔莫哥罗夫复杂度表示如下：

**定理 12.3.7** (科斯-汉森、米勒、所罗门 [66])。\(x \le_{LR} y\) 当且仅当
\((\exists c)(\forall n)(K^y(n) \le K^x(n) + c)\)。

将推论 12.2.13 与 van Lambalgen 定理 (12.1.7) 结合，为随机性论题提供了额外证据：

**命题 12.3.8。** _对于任意两个 Martin-Löf 随机实数_ \(x\) _和_ \(y\) _，_\(x \le_K y\) _蕴含_ \(y \le_{LR} x\)。

#### 12.3.5 对于强 Martin-Löf 随机性的低性

**定理 12.3.9** (道尼等人 [23]、尼斯 [111] 和科斯-汉森等人 [66])。_对于任意_ \(x\) _，以下等价：_
(i) _\(x\) 是 K-平凡的；_
(ii) _\(x\) 对于强 Martin-Löf 测试是低的；_
(iii) _\(x\) 对于强 Martin-Löf 随机性是低的。_

#### 12.3.6 练习

**练习 12.3.1。** 证明存在 $2^{\aleph_0}$ 个递归支配且非 DNR 的实数。

**练习 12.3.2。** 证明存在一个递归可追踪的 \(x\)，使得 \(x' \le_T x \oplus \emptyset'\)。

**练习 12.3.3。** 设 \(\mathcal{M}\) 为 ZFC 的一个模型，设 \(x\) 是在 \(\mathcal{M}\) 上的 Sacks 通用实数。证明如果 \(y\) 在 \(\mathcal{M}\) 中是随机的，那么 \(y\) 在 \(\mathcal{M}[x]\) 中也是随机的。

## 13 关于高算术理论的更多内容

### 13.1 高算术测度理论

测度理论在递归论中的应用由 Spector [155]、Sacks [117] 以及 Leeuw, Moore, Shannon 和 Shapiro [19] 开创。自然数上的随机性理论可以被视为这种应用，而高阶随机性理论则是测度理论与高算术理论的结合。在本章中，我们将讨论这些联系，为下一章的高阶随机性奠定基础。

#### 13.1.1 $\Pi_1^1$-集的测度

**引理 13.1.1** (Sacks [120])。集合

\{(\varphi, p) \mid p \text{ 是有理数} \land \varphi \text{ 是秩公式，且 } x \text{ 为其唯一自由变量} \land \mu(\{x \mid \mathfrak{A}(\omega_1^{CK}, x) = \varphi\}) \ge p\}

是 $\Pi_1^1$。

**证明。** 根据 Spector–Gandy 定理 (3.7.1)，只需证明集合

\{(\varphi, p) \mid p \text{ 是有理数} \land \varphi \text{ 是秩公式，且 } x \text{ 为其唯一自由变量} \land \mu(\{x \mid \mathfrak{A}(\omega_1^{CK}, x) = \varphi\}) \ge p\}

在 $(L_{\omega_1^{CK}}, \in)$ 上是 $\Sigma_1$。我们通过对 \(\varphi\) 的秩进行归纳来应用定理 3.1.8。

如果 \(\varphi\) 是原子的，那么

\{(\varphi, p) \mid p \text{ 是有理数} \land \varphi\text{的唯一自由变量是 } x \land \mu(\{x \mid \mathfrak{A}(\omega_1^{CK}, x) = \varphi\}) \ge p\}

是递归的。通过对 \(\varphi\) 的复杂性进行归纳，不难看出

\{(\varphi, p) \mid p \text{ 是有理数} \land \varphi\text{的唯一自由变量是 } x \land \varphi \text{ 的秩为 } 0 \land \mu(\{x \mid \mathfrak{A}(\omega_1^{CK}, x) = \varphi\}) \ge p\}

是算术的，因此在 $(L_{\omega_1^{CK}}, \in)$ 上是 $\Sigma_1$。现在假设集合

\{(\varphi, p) \mid p \text{ 是有理数} \land \varphi\text{的唯一自由变量是 } x \land \varphi \text{ 的秩至多为 } \alpha \land \mu(\{x \mid \mathfrak{A}(\omega_1^{CK}, x) = \varphi\}) \ge p\}

在 $(L_{\omega_1^{CK}}, \in)$ 上是 $\Sigma_1$。现在假设集合

设 \(\varphi(x, x^\beta)\) 为秩至多为 \(\beta\) 的公式，使得唯一的自由变量是 \(x\) 和 \(x^\beta\)。那么 \(\mathfrak{A}(\omega_1^{CK}, x) \equiv (\exists x^\beta)\varphi(x, x^\beta)\) 当且仅当 \(\mathfrak{A}(\omega_1^{CK}, x) \equiv \varphi(x, x^\beta \mid \psi)\) 对某个秩小于 \(\beta\) 的公式 \(\eta(n)\) 成立，其中 \(n\) 是 \(\psi\) 的唯一自由变量。

为简化起见，将 \(\varphi(x, x^\beta \mid \psi)\) 写作 \(\varphi(x, \psi)\)。那么

\(\{(\lnot(\exists x^\beta)\varphi(x, x^\beta), p) \mid \mu(\{x \mid \mathfrak{A}(\omega_1^{CK}, x) \equiv (\exists x^\beta)\varphi(x, x^\beta)\}) \ge p \wedge p \text{ 是有理数} \} = \{(\lnot(\exists x^\beta)\varphi(x, x^\beta), p) \mid (\exists n \text{ 的秩} < \beta) (n \text{ 是 } \psi \text{ 的唯一自由变量}) \wedge p \text{ 是有理数} \wedge \mu(\{x \mid (\omega_1^{CK}, x) \equiv \varphi(x, \psi)\}) \ge p \}.\)

请注意，秩 \(< \beta\) 且 \(n\) 为唯一自由变量的公式 \(\varphi\) 的集合属于 \(L_{\omega_1^{CK}}\)。因此，集合 \(\{(\lnot(\exists x^\beta)\varphi(x, x^\beta), p) \mid p \text{ 是有理数} \wedge \mu(\{x \mid \mathfrak{A}(\omega_1^{CK}, x) \equiv (\exists x^\beta)\varphi(x, x^\beta)\}) \ge p \}\) 在 \((L_{\omega_1^{CK}}, \in)\) 上是 \(\Sigma_1\)。

对于形式为 \((\forall x^\beta)\varphi(x, x^\beta)\) 且 \(n\) 为唯一自由变量的公式，请注意，在 \((L_{\omega_1^{CK}}, \in)\) 中一致地存在这样一组公式的 \(\omega\)-枚举。固定这样的枚举 \(\{\psi_i(n)\}_{i < \omega}\)。那么

\(\mu(\{x \mid \mathfrak{A}(\omega_1^{CK}, x) \equiv (\forall x^\beta)\varphi(x, x^\beta)\}) \ge p\)

当且仅当

\(\mu(\{x \mid \mathfrak{A}(\omega_1^{CK}, x) \equiv (\forall i)\varphi(x, \psi_i)\}) \ge p\)

当且仅当

\((\forall j)\mu(\{x \mid \mathfrak{A}(\omega_1^{CK}, x) \equiv \wedge_{i \le j} \varphi(x, \psi_i)\}) \ge p.\)

因此，\(\{(\forall x^\beta)\varphi(x, x^\beta), p\} \mid p \text{ 是有理数} \land \mu(\{x \mid \mathfrak{A}(\omega_1^{CK}, x) \equiv (\forall x^\beta)\varphi(x, x^\beta)\}) \ge p\}\) 在 \((L_{\omega_1^{CK}}, \in)\) 上是 \(\Sigma_1\)。

其余情况留给读者验证。请注意，归纳是一致的，因此引理得证。

**推论 13.1.2.** 设 \(p > 0\) 为有理数。假设 \(\varphi(n, y)\) 是一个秩公式，其唯一的自由无界集变量是 \(y\)。如果对于任何 \(n < \omega\)，\(\mu(\{x \mid \mathfrak{A}(\omega_1^{CK}, x) \equiv (\exists y)\varphi(n, y)\}) \ge p\)，则存在一个 \(\beta < \omega_1^{CK}\)，使得 \((\forall n)\mu(\{x \mid (\omega_1^{CK}, x) \equiv (\exists y^\beta)\varphi(n, y^\beta)\}) \ge p\)。

**证明。** 固定 \(m_0\) 使得 \(p > 2^{-m_0}\)。根据引理 13.1.1 和假设，存在一个函数 \(f : \omega \times (\omega \setminus \{m_0\}) \to \omega_1^{CK}\)，使得对于每个 \(n\) 和 \(m > m_0\)，

\(\mu(\{x \mid \mathfrak{A}(\omega_1^{CK}, x) \equiv (\exists y^{<m_0})\varphi(n, y^{<m_0})\}) \ge p \ge 2^{-m}.\)

令 \(g(n) = \bigcup_{m < \omega} f(n, m)\)。由于 \(L_{\omega_1^{CK}}\) 的可接受性，\(g\) 在 \(L_{\omega_1^{CK}}\) 上是全定义的。因此对于所有 \(n\)，\(\mu(\{x \mid \mathfrak{A}(\omega_1^{CK}, x) \equiv (\exists y^{<g(n)})\varphi(n, y^{<g(n)})\}) \ge p\)。令 \(\beta = \bigcup_{n < \omega} g(n)\)。再次根据可接受性，\(\beta < \omega_1^{CK}\)。此外，\((\forall n)\mu(\{x \mid \mathfrak{A}(\omega_1^{CK}, x) \equiv (\exists y^\beta)\varphi(n, y^\beta)\}) \ge p\)。

**定理 13.1.3.** (Sacks [120])。设 \(p\) 为有理数。集合 \(\{(\ulcorner \varphi \urcorner, p) \mid p \text{ 是有理数。} \}\) 是 \(\Sigma_1^1 \wedge \varphi\) 的唯一自由变量是 \(x\) 如果 \(\mu(\{x \mid \mathfrak{A}(\omega_1^{CK}, x) \equiv \varphi\}) \ge p\}\) 是 \(\Pi_1^1\)。

**证明。** 这直接从引理 13.1.1 和推论 13.1.2 得出。





定理 13.1.3 作为高阶算术测度理论的基本工具很有用。

### 13.1.2 测度论的一致性

#### **定理 13.1.4** (Sacks [120]). $\{x \mid \omega_1^{\text{CK}, x} = \omega_1^{\text{CK}}\}$ 的测度为 1.

证明。根据定理 5.15，只需证明集合
$\{x \mid \mathfrak{A}(\omega_1^{\text{CK}, x}) = \Delta_1^1\text{-comprehension}\}$
的测度为 1。令 $(\langle \varphi_i, \psi_i \rangle)_{i < \omega}$ 为算术公式的递归枚举。

对每个 $i$，定义 $\Pi_1^1$-集
$A_i = \{x \mid \mathfrak{A}(\omega_1^{\text{CK}, x}) \models (\forall n) \exists y (\varphi_i(n, y) \lor \neg \psi_i(n, y)) \}$.

令
$A_{i, \beta} = \{x \mid \mathfrak{A}(\omega_1^{\text{CK}, x}) \models (\forall n)(\exists \beta') (\varphi_i(n, y^\beta) \lor \neg \psi_i(n, y^\beta)) \}$.

则对所有 $i < \omega$ 和 $\beta < \omega_1^{\text{CK}}$，有 $A_{i, \beta} \subseteq A_i$。根据推论 13.1.2，对任意 $i, j < \omega$，存在 $\beta_{i, j} < \omega_1^{\text{CK}}$ 使得 $\mu(A_i \setminus A_{i, \beta_{i, j}}) < 2^{-i-j}$。此外，对任意 $j < \omega$ 和 $x \notin \bigcup_{i < \omega} (A_i \setminus A_{i, \beta_{i, j}})$，有 $\mathfrak{A}(\omega_1^{\text{CK}, x}) = \Delta_1^1\text{-comprehension}$。于是对任意 $j$，
$\mu(\{x \mid \mathfrak{A}(\omega_1^{\text{CK}, x}) = \Delta_1^1\text{-comprehension}\}) \ge 1 - \sum_{i < \omega} 2^{-i+j} \ge 1 - 2^{-j+1}$.

因此
$\mu(\{x \mid \mathfrak{A}(\omega_1^{\text{CK}, x}) = \Delta_1^1\text{-comprehension}\}) = 1$.

定理 13.1.4 有些反直觉，因为构造一个高阶算术计算高跳跃的实数要容易得多。该定理也可被视为支持随机性论的又一证据，因为高阶算术计算 0 的实数集的测度为 0。

已知（参见 Sacks [117] 和 Leeuw, Moore, Shannon, 及 Shapiro [19]），对任意非递归 x，集合 $\{y \mid y \ge_T x\}$ 是零测度集。下面的定理是其高阶算术类比。

#### **定理 13.1.5** (Sacks [123]). 若 $x$ 不是高阶算术的，则 $\mu(\{y \mid y \ge_h x\}) = 0$.

证明。对任意 x，集合 $\{y \mid y \ge_h x\}$ 是 $\Pi_1^1(x)$，因此根据推论 3.7.10 可测。

现在假设 $\mu(\{y \mid y \ge_h x\}) > 0$。根据定理 13.1.4，$\omega_1^x = \omega_1^{\text{CK}}$。此外，$\mu(\{y \mid \omega_1^y = \omega_1^{\text{CK}} \land y \ge_h x\}) > 0$。根据定理 5.14，存在一个分级公式 $\varphi(n)$ 使得 $\mu(\{y \mid n \in x \iff \mathfrak{A}(\omega_1^{\text{CK}, y}) \models \varphi(n)\}) > 0$。根据勒贝格密度定理，存在一个字符串 $\sigma \in 2^{<\omega}$ 使得 $\mu(\{y \mid y > \sigma \land n \in x \iff \mathfrak{A}(\omega_1^{\text{CK}, y}) \models \varphi(n)\}) > \frac{1}{2} \cdot 2^{-|\sigma|}$。于是
$n \in x \iff \mu(\{y > \sigma \mid \mathfrak{A}(\omega_1^{\text{CK}, y}) \models \varphi(n)\}) > \frac{1}{2} \cdot 2^{-|\sigma|}$
且
$n \notin x \Rightarrow \mu(\{y > \sigma \mid \mathfrak{A}(\omega_1^{\text{CK}, y}) \models \neg \varphi(n)\}) > \frac{1}{2} \cdot 2^{-|\sigma|}$.

根据引理 13.1.1，x 是高阶算术的，这产生了矛盾。

还可知，若 A 是实数的 r.e. 集且 p 为有理数，则陈述 "\(\mu(A) > p\)" 是 r.e. 的。高阶算术理论中存在下述对应结果。

#### **命题 13.1.6** (Sacks [123]). 设 \(A \subseteq \omega \times 2^\omega\) 为 \(\Pi_1^1\) 且 \(A_n = \{x \mid (n, x) \in A\}\)。则 \(\{(n, p) \mid p \text{ 为有理数} \land \mu(A_n) > p\}\) 是 \(\Pi_1^1\).

证明。由于 A 是 \(\Pi_1^1$，根据推论 3.7.4 存在一个算术公式 \(\varphi(n, x, z)$ 使得
\((n, x) \in A \Leftrightarrow (\exists z \leqslant_{\text{h}} x) \varphi(n, x, z)$.

令 \(B = \{(n, x) \mid \mathfrak{A}(\omega_1^x, x) \models (\exists i)(\varphi(n, x, z) \leqslant i)\}$。根据定理 13.1.4，对每个 n，\(\mu(B_n) = \mu(\{x \mid (n, x) \in B\}) = \mu(A_n)$。根据推论 13.1.2，\(\mu(B_n) > p$ 当且仅当
\((\exists i)(\mu(B_n) \ge p + 2^{-i})\)
当且仅当
\((\exists i)(\exists m)(m \in \omega_1 \land \mu(\{x \mid \mathfrak{A}(\omega_1^{\text{CK}}, x) \models (\exists z^{\le m}) \varphi(n, x, z^{\le m})\}) \ge p + 2^{-i})\).

根据引理 13.1.1，可得集合 \(\{(n, p) \mid \mu(A_n) > p \land p \text{ 为有理数}\}\) 是 \(\Pi_1^1$。

Kechris 在 [63] 中在 PD 假设下证明了以下结果。结果表明，额外的假设可以被削弱。

#### **推论 13.1.7** (Kechris [63]). 假设 \(\omega_1^x < \omega_1$。给定一个 \(\Sigma_2^1$-集 \(A \subseteq 2^\omega$，则 \(\{p \in \mathbb{Q} \mid \mu(A) > p\}$ 和 \(\{p \in \mathbb{Q} \mid \mu(A) \ge p\}$ 均为 \(\Sigma_2^1$。

证明。根据假设，几乎每个实数都是 L 上的 R-通用（参见 § 6.2.2）。注意，对任意 L 上的 R-通用 x，有 \(L_1^{\omega_1^x} = \omega_1^x$。由于 A 是 \(\Sigma_2^1$，存在一个 \(\Pi_1^1$ 关系 R 使得
\(x \in A \Leftrightarrow (\exists y \in L_{\omega_1^x}[x]) R(x, y)$.

于是 \(\mu(A) > p$ 当且仅当存在一个序数 \(\beta < \omega_1^x$ 使得 \(\mu(\{x \mid (\exists y \in L_\beta[x]) R(x, y)\}) > p$。因此 \(\mu(A) > p$ 当且仅当存在一个实数 \(r \in L$ 编码序数类型为 \(\beta$ 的良序，使得 \(\mu(\{x \mid (\exists y \in L_\beta[x]) R(x, y)\}) > p$。根据命题 13.1.6，后者是一个 \(\Sigma_2^1$ 陈述。

推论的第二部分直接从第一部分得出。

根据推论 13.1.7 的证明，有以下结论。

#### **推论 13.1.8.** 若 \(\omega_1^x < \omega_1$，则每个 \(\Sigma_2^1$-集均可测。

#### **命题 13.1.9** (Kechris [63]). 假设 \(\omega_1^x < \omega_1$。对任意 x，若 \(\{y \mid x \leqslant_{\Delta_1^1} y\}$ 不是零测度集，则 x 是 \(\Delta_2^1$。

证明。根据 \(\Pi^1_1$-一致化定理（4.2.1），存在一个 \(\Pi^1_1$-部分函数 \(F : \omega \times 2^\omega \to 2^\omega$ 使得对任意 \(y\) 和 \(\Pi^1_1(y)\)-单点 \(z$，存在一个 \(n$ 使得 \(F(n, y) = z$。根据推论 4.2.8，\(x \le_{\Delta^1_1} y$ 当且仅当存在 \(n$ 和 \(e$ 使得 \(x = \Phi_e^{F(n, y)}$。注意，对任意对 \((n, e)$ 和数 \(m$、\(i$，集合 \(D_{n,e,m,i} = \{y \mid \Phi_e^{F(n,y)}(m) = i\}$ 是 \(\Sigma^1_1$，因此根据推论 13.1.8 可测。还要注意，对任意 \(n$ 和 \(e$，集合 \(D_{n,e} = \{y \mid \Phi_e^{F(n,y)}(m) = x(m)\} = \bigcap_{m \in \omega} D_{n,e,m,x(m)}$ 是可测的。因此 \(E = \{y \mid x \le_{\Delta^1_1} y\}$ 是可测的。现在假设 \(E$ 不是零测度集。则存在一对 \((n, e)$ 使得 \(D_{n,e}$ 具有正测度。令 \(\sigma \in 2^{<\omega}$ 使得 \(\mu(D_{n,e} \cap [\sigma]) > 2^{-|\sigma|} \cdot \frac{3}{4}$。则 \(m \in x \iff \mu(D_{n,e,m,1} \cap [\sigma]) > 2^{-|\sigma|} \cdot \frac{3}{4}$。根据推论 13.1.7，\(x$ 是 \(\Sigma^1_1$。用同样的论证，\(\omega \backslash x$ 也是 \(\Sigma^1_1$，因此 \(x$ 是 \(\Delta^1_1$。\(\square\) 应当指出，命题 13.1.9 中的假设 "\(\omega_1^{\text{CK}} < \omega_1$" 在 ZFC 下不可证。

### 13.1.3 测度论基础定理

在测度论中，每个实数的可测集都由闭集逼近。高阶算术理论中存在其有效版本。

#### **引理 13.1.10.** 存在一个 \(\Pi^1_1$-函数 \(f : \omega \times \omega \to \omega$ 使得对任意分级公式的 Gödel 数 \(n$，
- (i) \(f(n, m)\) 是一个分级公式的 Gödel 数，其唯一自由变量为 \(x\);
- (ii) 集合 \(\{x \mid \mathfrak{A}(\omega_1^{\text{CK}}, x) \vDash \phi_{f(n,m)}\}\) 是 \(\{x \mid \mathfrak{A}(\omega_1^{\text{CK}}, x) \vDash \phi_n\}\) 的闭子集;
- (iii) \(\mu(\{x \mid \mathfrak{A}(\omega_1^{\text{CK}}, x) \vDash \phi_n\} \setminus \{x \mid \mathfrak{A}(\omega_1^{\text{CK}}, x) \vDash \phi_{f(n,m)}\}) < 2^{-m}\).

证明。我们通过公式的秩对函数 \(f$ 进行归纳构造。令 \(\beta < \omega_1^{\text{CK}}$，并假设通过归纳，\(f$ 对每个秩小于 \(\beta$ 的公式均已定义。在 \(\langle L_{\omega_1^{\text{CK}}}, \in \rangle$ 中，存在一组以 \(n$ 为唯一自由变量的秩 \(< \beta$ 的公式的统一枚举 \(\{\psi_{(n)}\}_{i < \omega}$。

令 \(\varphi(x^E)\) 为秩 \(\le \beta$ 且唯一自由秩变量为 \(x^E$ 的公式。对于公式 \((\exists x^E)\varphi(x^E)$，\(\mathfrak{A}(\omega_1^{\text{CK}}, x) \vDash (\exists x^E)\varphi(x^E)$ 当且仅当存在一个 \(j$ 使得 \(\mathfrak{A}(\omega_1^{\text{CK}}, x) \vDash \forall^j \varphi(\Psi b)$。根据定理 13.1.3，存在一个高阶算术函数，将每个 \(m$ 映射到足够大的 \(j$ 使得
\(\mu(\{x \mid \mathfrak{A}(\omega_1^{\text{CK}}, x) \vDash (\exists x^E)\varphi(x^E)\}) - \mu(\{x \mid \mathfrak{A}(\omega_1^{\text{CK}}, x) \vDash (\exists i \le j)(\varphi(\Psi_i))\}) < 2^{-m-1}$.





由归纳假设，存在一个公式 \(\phi'\) 对应于 \(\vee_{i \le j} \psi(\eta_i)\)（即 \(\ulcorner \phi' \urcorner = f(\ulcorner \vee_{i \le j} \psi(\eta_i) \urcorner, m+1)\)）使得

\(\mu(\{x \mid \mathfrak{A}(\omega_1^{\text{CK}}, x) = \vee_{i \le j} \psi(\phi_i)\}) - \mu(\{x \mid \mathfrak{A}(\omega_1^{\text{CK}}, x) = \phi'\}) < 2^{-m-1}.\)

那么 \(\mu(\{x \mid \mathfrak{A}(\omega_1^{\text{CK}}, x) = (\exists \beta)\rho(\beta^x)\}) - \mu(\{x \mid \mathfrak{A}(\omega_1^{\text{CK}}, x) = \phi'\}) < 2^{-m}\)。令 \(f'((\exists \beta)\phi(\varphi(\beta^x)), m) = \ulcorner \phi' \urcorner\)。

对于 \((\forall x \beta)\phi(\varphi(\beta^x))\)，有 \(\mathfrak{A}(\omega_1^{\text{CK}}, x) = (\forall x \beta^j)\phi(\varphi(\beta^x))\) 当且仅当对于所有 \(j < \omega\)，\(\mathfrak{A}(\omega_1^{\text{CK}}, x) = \wedge_{i \le j} \psi(\eta_i)\)。由归纳假设，存在一个超算术函数，将每个 \(j\) 映射到一个公式 \(\phi'_j\)，该公式对应于 \(\wedge_{i \le j} \psi(\phi_i)\)（即 \(\ulcorner \phi'_j \urcorner = f(\ulcorner \wedge_{i \le j} \psi(\phi_i) \urcorner, m+j+2)\)）使得

\(\mu(\{x \mid \mathfrak{A}(\omega_1^{\text{CK}}, x) = \wedge_{i \le j} \psi(\phi_i)\}) - \mu(\{x \mid \mathfrak{A}(\omega_1^{\text{CK}}, x) = \phi'_j\}) < 2^{-m-j-2}.\)

现在 \(\{x \mid (\forall j)\mathfrak{A}(\omega_1^{\text{CK}}, x) = \phi'_j\}\) 是超算术的。因此存在一个分级公式 \(\phi'\) 使得对于任意 \(x\)，

\(\mathfrak{A}(\omega_1^{\text{CK}}, x) = \phi' \Leftrightarrow (\forall j)\mathfrak{A}(\omega_1^{\text{CK}}, x) = \phi'_j.\)

注意集合 \(\{x \mid \mathfrak{A}(\omega_1^{\text{CK}}, x) = \phi'\}\) 是闭集。而且，

\(\mu(\{x \mid (\forall x \beta^j)\phi(\varphi(\beta^x))\}) - \mu(\{x \mid \mathfrak{A}(\omega_1^{\text{CK}}, x) = \phi'\}) \le \sum_{i < \omega} 2^{-m-i-2} < 2^{-m}.\)

因此定义 \(f'((\forall x \beta)\phi(\varphi(\beta^x)), m) = \ulcorner \phi' \urcorner\)。对于其他情况，\(f\) 的定义是直接的。\(\square\)

#### 推论 13.1.11.

如果 \(A\) 是 \(\Pi_1^1\) 且 \(\mu(A) = r\)，其中 \(r\) 是超算术的，那么存在一个 \(\Delta_1^1\)-集 \(B \subseteq A\) 使得 \(\mu(B) = \mu(A)\)。

#### 命题 13.1.12 (Kechris [63]).

假设 \(\omega_1^L < \omega_1\)。假设 \(A \subseteq 2^\omega\) 是一个正测度的 \(\Sigma_1^1\)-集。那么对于任意 \(n\)，存在一个 \(\Delta_1^1\) 完美集 \(B_n \subseteq A\) 使得 \(\mu(A) < \mu(B_n) + 2^{-n}\)。此外，如果 \(\mu(A)\) 是 \(\Delta_1^1\)，那么 \(\{(n, x) \mid x \in B_n \land n < \omega\}\) 是 \(\Delta_1^1\)。

#### 证明.

由于 \(A\) 是 \(\Sigma_2^1\)，存在一个 \(\Pi_1^1\) 关系 \(R\) 使得

\(x \in A \Leftrightarrow (\exists y \in L_{\omega_1^L}[x])R(x, y).\)

令 \(p\) 为介于 \(\mu(A)\) 和 \(\mu(A) - 2^{-n}\) 之间的一个有理数。通过与推论 13.11.7 类似的论证，\(\mu(A) > p\) 当且仅当存在一个对 \(\omega\) 进行良序编码的 \(r \in L\)，使得 \(\mu(\{x \mid (\exists y \in L_r[x])R(x, y)\}) > p\)。令 \(C = \{r \mid r \text{ codes a well-ordering of } \omega \land \mu(\{x \mid (\exists y \in L_r[x])R(x, y)\}) > p\}\)。那么 \(C\) 是一个非空的 \(\Pi_1^1\)-集。因此存在一个 \(\Delta_2^1\) 的 \(r_n \in C\)。令

\(B_n = \{x \mid (\exists y \in L_{r_n}[x])R(x, y)\}.\)

那么 \(B_n \subseteq A\) 是 \(\Delta_1^1\) 且 \(\mu(B_n) > p > \mu(A) - 2^{-n}\)。命题的另一部分从上述内容得出。\(\square\)

以下是一个测度论基础定理：

#### 定理 13.1.13 (Sacks [120]).

如果 \(A \subseteq 2^\omega\) 是一个正测度的 \(\Pi^1_1\)-集，那么 \(A\) 包含一个超算术实数。

证明。假设 \(A \subseteq 2^\omega\) 是一个正测度的 \(\Pi^1_1\)-集。由推论 3.7.4，存在一个算术公式 \(\varphi(x, \omega)\) 使得

$$
x \in A \Leftrightarrow (\exists z \le_h x) \varphi(x, z).
$$

令 \(B = \{x \mid \aleph(x^K_1, x) = (\exists z)\varphi(x, z)\}\)。那么 \(B \subseteq A\)。由定理 13.1.4，\(\mu(B) = \mu(A) > 0\)。由引理 13.1.10，存在一个由分级公式 \(\psi(x)\) 定义的非空闭集 \(C \subseteq B\)。令

$$
T = \{t \in 2^{<\omega} \mid \mu(\{x \mid \forall t(x^K_1, x) = \psi(x) \wedge x \supset t\}) > 0\}.
$$

那么，由引理 13.1.11，\([T] \subseteq C\) 是一个超算术树。\(T\) 中最左无限路径是超算术的。

### 13.1.4 练习

- 练习 13.1.11. 令 \(A \subseteq \omega \times 2^\omega\) 为 \(\Pi^1_1\)，并令 \(A_n = \{x \mid (n, x) \in A\}\)。证明集合 \(\{(n, p) \mid p(A_n) \ge p \wedge p \text{ is rational}\}\) 是 \(\Pi^1_1\)。

- 练习 13.1.12. 证明如果 \(A \subseteq 2^\omega\) 是 \(\Pi^1_1\)，那么 \(\mu(A) \le_T \emptyset\)。

- 练习 13.1.13. 证明对于任意实数 \(x\)，集合 \(\{y \mid (\forall z)(\le_h x \wedge x \wedge z \le_h y \rightarrow z \in \text{HYP})\}\) 的测度为 1。

- 练习 13.1.14. 证明推论 13.1.11。

- 练习 13.1.15. 证明对于任意递归序数 \(\beta\)，存在一个测度为 1 的超算术集 \(A\)，使得 \(A\) 中没有实数在 \(0^{(\beta)}\) 中是递归的。

- 练习 13.1.16 (Jockusch). 如果 \(A \subseteq 2^\omega\) 是一个不包含超算术实数的 \(\Pi^1_1\)-集，那么集合 \(\{x \mid (\exists y)(y \in A \wedge y \le_h x)\}\) 是零集。

- 练习 13.1.17. 假设 \(V = L\)。证明对于任意 \(x\)，\(\{y \mid x \le_{\Delta^1_1} y\}\) 的测度为 1。

## 13.2 在 Kleene's O 之上对集合进行编码

#### 13.2.1 \(\Sigma^1_1\)-集的连接基定理

关于是否存在一个不可数的 \(\Sigma^1_1\)-集 \(A\)，使得对于任意 \(x, y \in A\) 都有 \(x \not\le_h y \not\le_h O\) 的问题在 Friedman [29] 和 Simpson[138] 中被提出。Harrington（未发表）给出了否定答案。以下是一个更强的版本，用于研究更高随机性理论。

#### 定理 13.2.1 (Chong and Yu [14]).

令 \(A_0\) 和 \(A_1\) 为不可数的 \(\Sigma^1_1\)-集。对于任意 \(z \ge_h \emptyset\)，存在 \(x_0 \in A_0\) 和 \(x_1 \in A_1\) 使得 \(x_0 \oplus x_1 \equiv_h z\)。

#### 证明.

修正一个实数 \(z \ge_h \emptyset\) 和两个不可数的 \(\Sigma^1_1\)-集 \(A_0\) 和 \(A_1\)。那么存在两个递归树 \(T_0, T_1 \subseteq 2^{<\omega} \times \omega^{<\omega}\) 使得对于 \(i \le 1\)，\(A_i = \{x \mid [\exists f](n \in [n, f] \in T_i)\}\)。我们可以假设 \(A_0\) 和 \(A_1\) 都不包含超算术实数。还假设如果 \((\sigma, \tau) \in T_i, i \le 1\)，则 \(|\sigma| = |\text{Dom}(\tau)|\)。令 \(T_2 \subseteq \omega^{<\omega}\) 为递归树，使得 \([T_2]\) 是不可数的且不包含超算术无限路径。令 \(f_0\) 为 \(T_2\) 中最左路径。然后 \(f_0 \oplus_h \emptyset\)。

对于 \(s=1\)，令 \([T_1] = (x_i, f_i) \mid \forall n [n \notin n \in T_i])\)。我们的计划是定义 \(x_i \in A_i\) 使得 \(z \equiv_h x_0 \oplus x_1\)。为此，将介绍一种将 \(z\) 和 \(f_0\) 编码进 \(x_0\) 并从 \(x_0 \oplus x_1\) 中解码它们的过程。\(x_i\) 的构造将在递归树 \(T_i\) 上在 \(\omega^x[x]\) 中进行，因此在 \(z\) 中是超算术的（因为 \(z \ge_h \emptyset\)）。由于 \(A_i\) 是 \(\Sigma^1_1\)，\(x_{i-1}\) 也将在函数 \(f_i\) 中进行编码，该函数是 \([T_i]\) 第二分量中最左路径，作为 \(x_i\) 在 \(A_i\) 中的见证，（即 \((x_i, f_i) \in [T_i]\) 并且对于任意 \(i\)，如果 \((x_i, f_i) \in [T_i]\) 且 \(f_i \neq f_j\)，那么 \(f_i(n) \neq f(n)\) 的最小 \(n\) 满足 \(f_i(n) < f(n)\)）。由于 \(A_i\) 没有超算术元素，对于任意 \((\sigma, \tau) \in T_i\)，如果 \(\sigma \prec \tau\) 且对于某些 \((x, f) \in [T_i]\) 有 \(\tau \prec f\)，则存在 \(\sigma\) 的不相容扩展 \(\sigma'\) 和 \(\sigma''\)，以及 \(\tau\) 的（可能相容）扩展 \(\tau'\) 和 \(\tau''\)，使得 \((\sigma', \tau')\) 和 \((\sigma'', \tau'')\) 在 \([T_i]\) 中都有扩展。\([T_i]\) 的这个“分裂性质”允许将 \(z, f_i\) 和 \(f_0\) 编码进 \(x_0\) 并将 \(f_0\) 编码进 \(x_1\)。更具体地说，当 \(z(s)\) 要在构造第 \(s+1\) 阶段的分裂节点处由 \(x_0\) 编码时，所选择的分支将遵循 \(z(s)\) 的值，因此如果 \(z(s) = 0\) 则采取“左转”，如果 \(z(s) = 1\) 则采取右转。在构造第 \(s+1\) 阶段对 \(\tau_{1,s}\) 的编码，它表示 \(f_1\) 在第 \(s\) 阶段结束时定义的初始段，通过对每个 \(t \in \text{Dom}(\tau_{1,s})\) 在分裂节点处取 \(\tau_{1,s}(t)\) 个连续左转来完成。在构造第 \(s+1\) 阶段对 \(f_0(s)\) 的编码通过在 \(f_0(s)\) 个连续分裂节点处取左转来完成。

为了解码目的，必须划清编码阶段中采取的不同类型的操作。由于 \(\tau_{1,s}\) 是一个有限函数，对于 \(t < |\text{Dom}(\tau_{1,s})|\)，对值 \(\tau_{1,s}(t)\) 的编码结束和对值 \(\tau_{1,s}(t+1)\) 的编码开始，由两个编码之间的分裂节点处的右转分隔（当然，由于构造是逐阶段执行的，可以假设在阶段 \(s+1\) 开始时，\(\tau_{1,s-1}\) 的编码已完成。这意味着在阶段 \(s+1\)，只需要对 \(t \in \text{Dom}(\tau_{1,s}) \setminus \text{Dom}(\tau_{1,s-1})\) 的值 \(\tau_{1,s}(t)\) 进行编码）。在下一个分裂节点处选择“右转”以表示 \(\tau_{1,s}\) 的编码结束和 \(f_0(s)\) 的编码开始。最后，在编码 \(f_0(s)\) 之后的下一个分裂阶段处采取右转，以标记阶段 \(s+1\) 中 \(x_0\) 的编码动作结束。在阶段 \(s+1\) 中对 \(x_0\) 的这个初始段记为 \(\sigma_{0,s+1}\)。那么 \(\sigma_{0,s+1} \prec f_0\) 是 \(\omega^{<\omega}\) 中的一个有限字符串，使得 \(|\text{Dom}(\tau_{0,s+1})| = |\sigma_{0,s+1}|\)。\(\tau_{0,s+1}\) 扩展了 \(\tau_{0,s}\)，并且是这样的最左字符串。在阶段 \(s+1\) 中对 \(f_0\) 的初始段 \(\tau_{0,s+1}\) 在 \(x_1\) 中的编码，记为 \(\sigma_{1,s+1}\)，继续



类似地。$r_{1,s+1}$ 的定义，即在阶段 $s+1$ 构造的 $f_1$ 的一个初始段，遵循相同的格式。

我们现在详细描述 $x_0$ 和 $x_1$ 以及相关字符串的构造。对于 $i \le 1$ 和 $\sigma, \tau \in T_i$，令 $T_i(\sigma, \tau)$ 为 $T_i$ 中与 $\sigma$ 和 $\tau$ 兼容的字符串集合，即

$$T_i(\sigma, \tau) = \{ \langle \sigma', \tau' \rangle \in T_i \mid \exists (\sigma'', \tau'') \in T_i (\sigma' \preceq \sigma'' \wedge \tau' \preceq \tau'' \wedge \sigma \preceq \sigma'' \wedge \tau \preceq \tau'') \}.$$

注意上述定义中不要求 $|\sigma| = |\tau|$。

我们说一个字符串（或节点）$\sigma^* \in 2^{<\omega}$ 在 $T_i$ 中关于 $(\sigma, \tau)$ 分裂，如果 $\sigma^* \succeq \sigma$ 且对于 $j \le 1$，

$$T_{i, \sigma^* \frown j}(\sigma, \tau) = \{ \langle \sigma', \tau' \rangle \mid \sigma' \succeq \sigma^* \frown j \wedge \tau' \succeq \tau \wedge \langle \sigma', \tau' \rangle \in T_i \}$$

包含一条无限路径。注意 $\sigma^*$ 本身不在 $T_i$ 上，但某个对 $(\sigma^*, \tau^*)$ 在 $T_i$ 上，我们称 $(\sigma^*, \tau^*)$ 为 $T_i$ 上的一个分裂节点。

对于每个 $i \le 1$，我们在 $T_i$ 上构造一个序列 $(\sigma_{i,0}, \tau_{i,0}) < (\sigma_{i,1}, \tau_{i,1}) < \cdots$，并令 $x_i = \bigcup_j \sigma_{i,j}$。再次，其思想是应用“互编码”技术，使得 $x_0$ 为 $x_1$ 编码最左见证函数 $f_1 = \cup_s r_{1,s}$（在 $\Sigma^1_1$-定义中），而 $x_1$ 为 $x_0$ 编码最左见证函数 $f_0 = \cup_s r_{0,s}$。此外，我们还指定 $x_0$ 负责编码 $z$ 以及 $f_0$。更精确地说，对于每个 $s \in \omega$，我们用 $\sigma_{0,s}$ 编码 $z(s)$、$f_0(s)$ 和 $\tau_{1,s-1}$，并用 $\sigma_{1,s}$ 编码 $\tau_{0,s}$。

在阶段 0，对于 $i \le 1$，令 $(\sigma_{i,0}, \tau_{i,0}) = (\emptyset, 0)$。不失一般性，假设 $(\emptyset, \emptyset)$ 是 $T_0$ 和 $T_1$ 中的一个分裂节点。

阶段 $s+1$ 的构造如下：

#### 子阶段 (i)

首先，令 $\sigma^*$ 为 $T_0$ 中关于 $(\sigma_{0,s}, \tau_{0,s})$ 的最短分裂节点。因此，对于 $j \le 1$，$T_{0, \sigma^* \frown j}(\sigma_{0,s}, \tau_{0,s})$ 包含一条无限路径。令 $\sigma^0_{0,s+1}$ 为 $T_0$ 中关于 $(\sigma_{0,s}, \tau_{0,s})$ 且扩展 $\sigma^* \frown z(s)$ 的最左分裂节点。因此，$z(s)$ 在此处被编码。接下来我们编码 $r_{1,s}$。令 $n^*_{s+1} = |\text{Dom}(r_{1,s})|$（如果 $s=0$，则令 $|\text{Dom}(r_{1,s-1})| = 0$）。归纳地，对于任何 $k \in \{1, n^*_{s+1}\}$，令 $\sigma^k_{0,s+1}$ 为 $T_0$ 中关于 $(\sigma_{0,s}, \tau_{0,s})$ 且扩展 $(\sigma^{k-1}_{0,s+1}) \frown 1$ 的最左分裂节点，使得在 $T_0$ 中关于 $(\sigma_{0,s}, \tau_{0,s})$ 的分裂节点在 $\sigma^{k-1}_{0,s+1}$ 和 $\sigma^k_{0,s+1}$ 之间共有 $r_{1,s}(k + |\text{Dom}(r_{1,s-1})|)$ 个。这完成了 $r_{1,s}$ 的编码。为了编码 $f_0(s)$，令 $\sigma^{n^*_{s+1}+1}_{0,s+1}$ 为 $T_0$ 中关于 $(\sigma_{0,s}, \tau_{0,s})$ 且扩展 $(\sigma^{n^*_{s+1}}_{0,s+1}) \frown 1$ 的最左分裂节点，使得在 $T_0$ 中关于 $(\sigma_{0,s}, \tau_{0,s})$ 的分裂节点在 $\sigma^{n^*_{s+1}}_{0,s+1}$ 和 $\sigma^{n^*_{s+1}+1}_{0,s+1}$ 之间共有 $f_0(s)$ 个。对于 $j \le 1$，令 $\sigma^{n^*_{s+1}+j+1}_{0,s+1}$ 为 $T_0$ 中关于 $(\sigma_{0,s}, \tau_{0,s})$ 且扩展 $(\sigma^{n^*_{s+1}+j}_{0,s+1}) \frown 1$ 的下一个分裂节点。这个编码告诉我们，子阶段中“$x_0$ 侧”的动作已完成。定义 $\sigma_{0,s+1} = \sigma^{n^*_{s+1}+3}_{0,s+1}$。令 $\tau_{0,s+1}$ 扩展 $\tau_{0,s}$，使得 $|\text{Dom}(\tau_{0,s+1})| = |\sigma_{0,s+1}|$ 且 $\tau_{0,s+1}$ 是最左节点，使得树 $T_0(\sigma_{0,s+1}, \tau_{0,s+1})$ 有一条无限路径。

#### 注记

在阶段 $s+1$，通过 $\sigma_{0,s+1}$ 在 $T_0$ 中对 $x_0$ 的编码采用了证明 11.11 的方法，将 $\Sigma^1_1$-集合 $A_0$ 视为“闭集”。这意味着首先忽略第二个分量（“r 侧”），并将证明定理 11.1.1 中的编码构造应用于闭集 $X_{\sigma_{0,s}, \tau_{0,s}} = \{x \supset \sigma_{0,s} \mid \forall n > |\tau_{0,s}| \exists y \supset \tau_{0,s} (x \upharpoonright n = y \upharpoonright n \forall f \in T([0]))\}$。一旦 $\sigma_{0,s+1}$（$x_0$ 的一个初始段）的编码完成，就有一个对与有限字符串 $\tau$ 匹配，该 $\tau$ 具有无限扩展，以保证 $x_0$ 属于 $A_0$。由于 $x_0$ 不知道应选择哪个正确的 $\tau$，$x_1$ 被设计用来帮助解码正确的 $\tau$。互编码策略对此至关重要。

#### 子阶段 (ii)

令 $\sigma^0_{1,s+1} = \sigma_{1,s}$ 且 $n^1_{s+1} = |\text{Dom}(\tau_{0,s+1})| - |\text{Dom}(\tau_{0,s})|$。归纳地，对于任何 $k \in [1, n^1_{s+1}]$，令 $\sigma^k_{1,s+1}$ 为关于 $(\sigma_{1,s}, \tau_{1,s})$ 且扩展 $(\sigma^{k-1}_{1,s+1}) \frown 1$ 的最左分裂节点，使得在 $T_1$ 中关于 $(\sigma_{1,s}, \tau_{1,s})$ 的分裂节点在 $\sigma^{k-1}_{1,s+1}$ 和 $\sigma^k_{1,s+1}$ 之间共有 $\sigma_{0,s+1}(k + |\text{Dom}(\tau_{0,s})|)$ 个。因此，$\sigma_{0,s+1}$ 被编码。对于 $j \le 1$，令 $\sigma^{n^1_{s+1}+j+1}_{1,s+1}$ 为 $T_1$ 中关于 $(\sigma_{1,s}, \tau_{1,s})$ 且扩展 $(\sigma^{n^1_{s+1}+j}_{1,s+1}) \frown 1$ 的下一个分裂节点。这个编码告诉我们，子阶段中“$x_1$ 侧”对 $\tau_{0,s+1}$ 的编码动作已完成。定义 $\sigma_{1,s+1} = \sigma^{n^2_{1,s+1}}_{1,s+1}$。因此，我们已将 $\tau_{0,s+1}$ 编码到 $\sigma_{1,s+1}$ 中。令 $\tau_{1,s+1}$ 扩展 $\tau_{1,s}$，使得 $|\text{Dom}(\tau_{1,s+1})| = |\sigma_{1,s+1}|$ 且 $\tau_{1,s+1}$ 是最左有限字符串，使得树 $T_1(\sigma_{1,s+1}, \tau_{1,s+1})$ 有一条无限路径。

这结束了阶段 $s+1$ 的构造。

对于 $i \le 1$，令 $x_i = \bigcup_{s<\omega} \sigma_{i,s}$。注意，构造是在 $L_{\omega_1^{CK}-1}[z]$ 上进行的，因为 $\emptyset \in L_{\omega_1^{CK}+1}$，以及 $(\sigma, \tau) \in T_i$ 是否在 $T_i$ 中有一条无限路径扩展由阶段 $L_{\omega_1^{CK}+1}^z$ 决定。由于 $z \ge_h \emptyset$，我们有 $a_i^X > \omega_1^{CK}$，因此 $z \ge_h x_0 \bowtie x_1$。

我们现在使用 $x_0$ 和 $x_1$ 来解码编码构造，从而从 $x_0 \bowtie x_1$ 高算术地恢复 $\emptyset$ 和 $z$。解码是通过一种类似于证明定理 11.1.1 中所用的有限损伤方法实现的。然而，正确的解码需要使用见证函数 $f_0$ 和 $f_1$。如果没有这些见证函数，$x_0$ 仍然会编码 $z$ 并属于 $A_0$ 的闭包。整个构造随后归约为证明 Martin 定理 11.1.1 中的构造。然而，在这种情况下，不能得出 $x_0$ 属于 $A_0$ 的结论。这一困难通过互编码程序得到解决，其中 $x_0$ 也编码 $f_1$，而 $x_1$ 编码 $f_0$。$z$ 的编码在构造过程中被编织到互编码策略中。

我们现在指出关键的解码步骤，并将细节留给读者。如同在证明定理 11.1.1 中一样，我们可以在 $L_{\omega_1^{CK}}$ 上固定一个 $\Sigma_1$-枚举 $\{T_i[a]\}_{i \le 2, a \in \omega_1^{CK}}$，使得对于 $i \le 2$，

- $T_i[0] = T_i$
- 如果 $a \le \beta$，则 $T_i[a] \le T_i[\beta]$
- $T_i[\langle \omega^a \rangle] = \langle \text{acc}_\omega^{X_i} T_i[a] \rangle$
- $T_i[\omega_1^{CK}]$ 没有死端节点，且
- $A_i = \{x \mid \exists \forall n (x \upharpoonright n, f \upharpoonright n) \in T_i[\omega_1^{CK}]\}$。

由于 $[T_i]$ 不包含高算术无限路径，我们有 $[T_i[\omega_1^{CK}]] = [T_i]$ 是一棵完美树（如前所述，这使得编码程序得以实现）。显然，对于每个 $a$，$(x_i, f_i)$ 是 $T_i[a]$ 中的一条无限路径。与 $T_i, i \le 1$ 的情况一样，对于每个 $a < \omega_1^{CK}$，可以定义字符串 $\sigma'$ 在 $T_i[a]$ 中关于 $(\sigma, \tau)$ 是分裂节点的概念。特别是，对于 $(\sigma, \tau) \in T_i[a]$ 且 $\sigma \prec x_i$，说 $x_i \upharpoonright n$ 在 $T_i[a]$ 中关于 $(\sigma, \tau)$ 分裂是有意义的。这意味着存在字符串 $\tau'_0, \tau'_1 \supseteq \tau$，使得 $(x_i \upharpoonright n \frown 0, \tau'_0), (x_i \upharpoonright n \frown 1, \tau'_1) \in T_i[a]$。在这种情况下，我们还说 $x_i \upharpoonright n$ 是 $T_i[a]$ 中关于 $(\sigma, \tau)$ 的一个 *局部分裂节点*。这里“局部”指的是这样一个事实：不能保证对于 $j=0, 1$，$(x_i \upharpoonright n \frown j, \tau'_j)$ 在 $T_i[a]$ 中有一个无限扩展。

由于对于每个 $i \le 1$ 和 $a < \omega_1^{CK}$，$(x_i, f_i)$ 是 $T_i[a]$ 上的一条路径，可以使用 $x_0 \oplus x_1$ 通过在 $T_i[a]$ 中模拟 $x_i$ 的构造来近似 $f_0(s)$ 和 $f_1(s)$ 的值。这是通过尝试使用 $x_0 \oplus x_1$ 检索序列 $\langle \langle \sigma_{i,s}, \tau_{i,s} \rangle \rangle_{s \le \omega}$，$i \le 1$，来实现的。当然，由于尚未确立 $z$ 和 $f_0$ 在 $x_0 \oplus x_1$ 中是高算术的，检索只是通过近似原始构造来进行的。使用 $x_0 \oplus x_1$，可以模仿 $\langle \langle \sigma_{i,s}, \tau_{i,s} \rangle \rangle_{s \le \omega}$ 的构造来为 $i \le 1$ 定义 $\langle \langle \sigma_{i,s+1}[a], \tau_{i,s}[a] \rangle \rangle_{s \le \omega}$，使得 $\sigma_{i,s+1}[a]$ 是 $x_i$ 的一个初始段（按长度升序排列）并且是在 $T_i[a]$ 中关于 $\langle \sigma_{i,s}[a], \tau_{i,s}[a] \rangle$ 的一个局部分裂节点。此外，对于每个 $i$，$\tau_{i,s+1}[a]$ 是阶段 $a$ 上 $f_i \upharpoonright s$ 的一个近似。换句话说，$\tau_{i,s+1}[a]$ 是最左有限字符串，使得 $\langle \sigma_{i,s+1}[a], \tau_{i,s+1}[a] \rangle \in T_i[a]((\sigma_{i,s}, \tau_{i,s}))$。

注意，对于每个 $n$ 和 $a < a' < \omega_1^{CK}$，在 $T_i[a]$ 中沿 $(x_i \upharpoonright n, f_i \upharpoonright n)$ 的分裂节点数量大于或等于在 $T_i[a']$ 中的数量。

可以使用 $T_2[a]$ 定义 $f_0$ 的一个“从左侧”的 $\Sigma_1(L_{\omega_1^{CK}})$-近似 $f_0^a$：$f_0^a(0)[a] \frown \cdots \frown f_0^a(n)[a]$ 是 $T_2[a]$ 中的最左字符串（可能只有有限多个这样的 $n$）。然后对于 $a < \omega_1^{CK}$，$f_0^a(0)[a] = f_0(0)$。假设 $n > 0$ 且对于所有 $m < n$，$f_0^a(m)[a] = f_0(m)$。那么 $f_0^a(n)[a] \le f_0(n)$，且 $\lim_{a \to \omega_1^{CK}} f_0^a(n)[a] = f_0(n)$。我们采用的解码算法如下。构造一序列序数 $\langle \alpha_s \rangle_{s \le \omega}$，该序列在 $L_{\omega_1^{CK}}[x_0 \oplus x_1]$ 中是 $\Delta_1$-可定义的，使得 $\lim_{s \to \omega} \alpha_s = \omega_1^{CK}$，并将其作为参数来解码实数 $z$，从而得出 $x_0 \oplus x_1 \cong_h z$。

令 $\tilde{G}_{0,0}(0) = f_0(0)$ 且 $a_0 = 0$。

我们说 $x_0 \oplus x_1$ 在阶段 $a$ *一致地计算* $f_0$ *直到 j*，如果对于每个 $k < j$，

- (1) $\tau_{1,a}[a]$ 与使用 $\sigma_{0,k+1}[a]$ 在 $x_0$ 中编码的内容一致。换句话说，令 $\sigma_{0,k+1}^*[a]$ 为 $T_0[a]$ 中关于 $\langle \sigma_{0,k}[a], \tau_{0,k}[a] \rangle$ 的最短局部分裂节点。那么存在一个 $\sigma_{0,k+1}^*[a]$，它是关于 $\langle \sigma_{0,k}[a], \tau_{0,k}[a] \rangle$ 且扩展 $\sigma_{0,k+1}^*[a] \frown i$ 的最左局部分裂节点，其中 $i \in \{0, 1\}$。此外，归纳地，对于每个 $l \in [1, n_{0,k+1}^*[a]]$，其中 $n_{0,k+1}^*[a] = \text{Dom}(\tau_{1,k+1}[a]) - \text{Dom}(\tau_{1,k}[a])$，令 $\sigma_{0,k+1}^*[a]$ 为 $T_0[a]$ 中关于 $\langle \sigma_{0,k}[a], \tau_{0,k}[a] \rangle$ 且扩展 $(\sigma_{0,k+1}^*[a]) \frown 1$ 的最左局部分裂节点。那么在 $T_2[a]$ 中关于 $\langle \sigma_{0,k}[a], \tau_{0,k}[a] \rangle$ 的局部分裂节点在 $\sigma_{0,k+1}^*[a]$ 和 $\sigma_{0,k+1}^{l}[a]$ 之间共有 $\tau_{1,k+1}[a](l + |\text{Dom}(\tau_{1,k}[a])|)$ 个；

- (2) 在阶段 $a$ 通过 $T_2$ 使用 $f_0^{a_0}$ 对 $f_0$ 的近似与通过 $\langle \sigma_{0,k}[a] \rangle_{i \le k}$ 的近似在解码 $f_0 \upharpoonright k$ 之前一致。换句话说，令 $\sigma_{0,k+1}^{a_0}[a]$ 为在 $T_0[a]$ 中关于 $\langle \sigma_{0,k}[a], \tau_{0,k}[a] \rangle$ 且扩展 $(\sigma_{0,k+1}^{a_0}[a]) \frown 1$ 的最左局部分裂节点，使得关于 $(\sigma_{0,k}[a], \tau_{0,k}[a])$ 的局部分裂节点共有 $f_0^{a_0}[k](a)$ 个



在 \( T_0[\alpha] \) 中，介于 \( \sigma_{0,k+1}^{n_0[\alpha]}[a] \) 和 \( \sigma_{0,k+1}^{n_0[\alpha]+1}[a] \) 之间。对于 \( i \le 1 \)，令 \( \sigma_{0,k+1}^{n_0[\alpha]+i+1}[a] \) 为在 \( T_0[\alpha] \) 上超过 \( (\sigma_{0,k}[a], \tau_{0,k}[a]) \) 并扩展 \( (\sigma_{0,k+1}^{n_0[\alpha]+i+1}[a])^\frown 1 \) 的下一个局部分裂节点。

那么 \( \sigma_{0,k+1}[a] = \sigma_{0,k+1}^{n_0[\alpha]+3}[a] \)，且

- (3) \( T_{0,k+1}[a] \) 与使用 \( \sigma_{1,k+1}[a] \) 在 \( x_1 \) 中编码的内容一致。因此，归纳地，对于每个 \( l \in [1, n_{k+1}^1[a]] \)，其中 \( n_{k+1}^1[a] = |\text{Dom}(T_{0,k+1}[a])| = |\text{Dom}(\tau_{0,k}[a])| \)，令 \( \sigma_{1,k+1}^l[a] \) 为在 \( T_1[a] \) 上超过 \( (\sigma_{1,k}[a], \tau_{1,k}[a]) \) 并扩展 \( (\sigma_{1,k+1}^{l-1}[a])^\frown 1 \) 的最左局部分裂节点，使得在 \( T_1[a] \) 中，介于 \( \sigma_{1,k+1}^l[a] \) 和 \( \sigma_{1,k+1}^{l+1}[a] \) 之间，超过 \( (\sigma_{1,k}[a], \tau_{1,k}[a]) \) 有 \( \tau_{0,k+1}[a](l+|\text{Dom}(T_{0,k}[a])|) \) 个局部分裂节点。对于 \( l \le 1 \)，令 \( \sigma_{1,k+1}^{n_1[\alpha]+1}[a] \) 为在 \( T_1[a] \) 上超过 \( (\sigma_{1,k}[a], \tau_{1,k}[a]) \) 的下一个局部分裂节点。那么 \( \sigma_{1,k+1}[a] = \sigma_{1,k+1}^{n_1[\alpha]+2}[a] \)。

注意，在任何阶段 \( \alpha \)，我们可以假设 \( x_0 \oplus x_1 \) 始终一致地计算 \( f_\emptyset \) 直到 0。此外，对于每个 \( \alpha < \omega_1^{CK} \) 和 \( j \in \omega \)，总存在一个 \( \alpha' \ge \alpha \)，使得 \( \alpha' < \omega_1^{CK} \) 且 \( x_0 \oplus x_1 \) 在阶段 \( \alpha' \) 上一致地计算 \( f_\emptyset \) 直到 \( j \)。

假设 \( t_{-1} \) 已定义，其中 \( t \ge 1 \)。搜索最小的阶段 \( \alpha > \alpha_{t-1} \)，使得 \( x_0 \oplus x_1 \) 在 \( \alpha \) 上一致地计算 \( f_\emptyset \) 直到 \( t \)。令 \( \alpha_t = \alpha \) 且对于每个 \( j \le t \)，\( \hat{g}_{\emptyset,t}(j) = f_\emptyset^\alpha(j)[a_t] \)。

这完成了步骤 \( t \) 的构造。

我们验证解码构造产生一个算法，以超算术方式从 \( x_0 \oplus x_1 \) 计算 \( z \)。

令 \( \gamma = \bigcup_{t \in \omega} \alpha_t \)。

显然 \( \gamma \le \omega_1^{CK} \) 且是一个极限序数。此外 \( \gamma < \omega_1^{x_0 \oplus x_1} \)。我们证明 \( \gamma = \omega_1^{CK} \)。

为求矛盾，假设 \( \gamma < \omega_1^{CK} \)。利用 \( x_0 \) 和 \( x_1 \) 都不是超算术的事实，我们将证明对于 \( i \le 1 \)，上述解码过程中引入的每个参数序列 \( n_i^1[a_t] \)、\( \sigma_{i,t}[a_t] \) 和 \( \tau_{i,t}[a_t] \) 最终在 \( t \to \omega \) 时稳定。假设这是错误的。那么存在一个最小的 \( j_0 \) 和相应的最小的 \( t_0 \)，使得对于所有 \( t \ge t_0 \)，\( f_\emptyset \) 在 \( a_t \) 上一直被一致地计算直到 \( j_0 - 1 \)，但 \( j_0 \) 除外。我们论证这种情况不会发生。

证明按阶段 \( a_{t_0} \) 参数引入的顺序进行归纳。为方便起见，我们只展示 \( \sigma_{0,j_0}^{n_0[\alpha]+1}[a_1] \) 在某个 \( t \) 之后达到极限（基本上相同的论证适用于证明其他参数序列也稳定）。这意味着 \( \hat{g}_{\emptyset,t}(j_0) \neq \hat{g}_{\emptyset,t+1}(j_0) \) 最多只对有限多个 \( t \) 成立。

假设 \( \sigma_{0,j_0}^{n_0[\alpha]}[a_1] \) 从阶段 \( a_{t_0} \) 开始不再改变（\( \sigma_{0,j_0}^{n_0[\alpha]}[a_1] \) 如上文所述，在 (2) 中对 \( f_\emptyset \upharpoonright k \) 进行解码之前定义）。如果 \( \sigma_{0,j_0}^{n_0[\alpha]+1}[a_{t+1}] \) 无限次改变，那么 \( \hat{g}_{\emptyset,t}(j_0) \neq \hat{g}_{\emptyset,t+1}(j_0) \) 对无限多个 \( t \) 成立。那么，根据解码构造，我们有以下主张。

#### 主张 1. 对于任何 \(t > t_0 + 1\)，\(\tilde{g}_{\emptyset, t+1}(j_0) \ge \tilde{g}_{\emptyset, t}(j_0)\)，因此 \(\lim_{t \to \omega} \tilde{g}_{\emptyset, t}(j_0) = +\infty\)。

证明。如果在某个阶段 \(\alpha_{t+1} > \alpha_t\) 为 \(\tilde{g}_{\emptyset, t}(j_0)\) 赋予一个新值 \(k\)，则必然有 \(\tilde{g}_{\emptyset, t}(0)^\frown \cdots \frown \tilde{g}_{\emptyset, t}(j_0 - 1)^\frown k \in T_2[\alpha_t]\)。然而，根据对 \(j_0\) 的假设，\(\tilde{g}_{\emptyset, t}(0)^\frown \cdots \frown \tilde{g}_{\emptyset, t}(j_0 - 1) \in T_2[\alpha_t]\)，因此 \(k > \tilde{g}_{\emptyset, t+1}(j_0)\)。

主张 1 意味着，在无限多个 \(t\) 时，在解码阶段中，为了逼近 \(f_\emptyset(j_0)\)，在 \(T_0[\alpha_t]\) 的局部分裂节点处选择了左转。

令 \(\sigma = \sigma_{0, j_0}^{n_0[\alpha_t]}[\alpha_t]\) 且 \(\tau = \tau_{0, j_0}[\alpha_t]\)。注意 \(|\sigma| > |\tau|\)。定义

\(X = \{x \succ \bar{\sigma} \mid \forall n \exists \beta < \gamma \exists \beta' \exists \tau' (\beta \le \beta' < \gamma \land |\tau'| = n \land (x \upharpoonright n, \tau') \in T_0[\beta'])\}\)。

如果我们令 \(p(\tau) = \{ \sigma \mid \exists \tau' (\sigma, \tau') \in T \}\) 成为树 \(T \subseteq \tau^{<\omega} \times \omega^{<\omega}\) 的一个“局部投影”，那么不难看出 \(\cap_{\beta < \gamma} p(T_0[\sigma, \tau][\beta])\) 是一棵树（注：\(T_0[\sigma, \tau][\beta]\) 表示 \(T_0[\beta]\) 中 \(T_0[\sigma, \tau]\) 的类似物）。此外，

\(X = \bigcap_{\beta < \gamma} p(T_0[\sigma, \tau][\beta])\)。

换句话说，\(X\) 由所有实数 \(x\) 组成，它们“潜在地”带有一个伴随见证 \(f\)，使得 \((x, f)\) 是 \(T_0[\sigma, \tau][\gamma]\) 中的一条无限路径。注意，由于 \(\gamma < \omega_1^{CK}\)，\(X\) 是 \(2^\omega\) 的一个 \(\Delta_1^1\) 闭子集。

#### 主张 2. \(x_0\) 是 \(X\) 中的最左路径。

证明。假设不然。那么存在 \(y_0\) 和 \(\sigma\)，使得 \(\tilde{\sigma} < \sigma\)，\(y_0 \succ \sigma^\frown \langle 0 \rangle\)，\(x_0 \succ \sigma^\frown \langle 1 \rangle\)，且 \(\forall \beta < \gamma \exists \beta' \exists \tau' (\beta \le \beta' < \gamma \land |\tau'| = |\sigma| + 1 \land (y_0 \upharpoonright |\sigma| + 1, \tau') \in T_0[\beta'])\)。

现在，根据主张 1，令 \(t_1 > t_0\) 使得对于所有 \(t \ge t_1\)，\(\tilde{g}_{\emptyset, t}(j_0) > |\sigma| + 1\)。那么存在长度为 \(|\sigma|\) 的 \(\tau, \tau'\)，使得 \((((x_0 \upharpoonright |\sigma| + 1, \tau), (y_0 \upharpoonright |\sigma| + 1, \tau')) \in T_0[\alpha_{t+1}]\)。然而，由于 \(y_0\) 在 \(x_0\) 的左侧，由 \(x_0\) 编码的 \(\tilde{g}_{\emptyset, t+1}(j_0)\) 的值最多为 \(|\sigma| + 1\)。因此 \(\tilde{g}_{\emptyset, t+1}(j_0) \le |\sigma| + 1\)，这产生了矛盾。

主张 2 意味着 \(x_0\) 是超算术的，这产生了矛盾。因此存在一个 \(t^0\)，使得对于任何 \(t \ge t^0\)，\(\tilde{g}_{\emptyset, t}(j_0) = \tilde{g}_{\emptyset, t+1}(j_0)\)，因而 \(\sigma_{0, j_0}^{n_0[\alpha_{t+1}]}[\alpha_t]\) 对于所有 \(t > t^0\) 都是常数。

我们留给读者去验证其他参数序列的稳定性。

因此，对于每个 \(j\)，存在一个 \(t_j\)，使得对于 \(t \ge t_j\)，\(\tilde{g}_{\emptyset, t}(j) = f_\emptyset^j(\alpha_t)\)。对于 \(j \in \omega\)，定义 \(\tilde{g}(j) = \lim_{t \to \omega} \tilde{g}_{\emptyset, t}(j)\)。那么 \(\tilde{g}(j) = \lim_{t \to \omega} f_\emptyset^j(\alpha_t)[t]\) 且 \(\tilde{g} \in L_{\gamma+1}\)。现在 \(\tilde{g}\) 是 \(T_2[\gamma]\) 中的最左路径，因此也是 \(T_2\) 中的最左路径。于是 \(\tilde{g} = f_\emptyset \in L_{\gamma+1}\)。这与假设 \( \gamma < \omega_1^{CK} \) 矛盾。因此 \( \gamma = \omega_1^{CK} \)，进而 \( f_\emptyset = x_0 \le_h x_1 \)。

利用这一点，可以通过 \( T_1[\omega_1^{CK}] \) 中的整个构造进行解码，并得出 \( z \le_h x_0 \oplus x_1 \)，从而完成定理的证明。

### 13.2.2 练习

练习 13.2.1. 证明存在一个不可数的 \(\Pi^1_1\)-集 \(A\)，使得对于任何 \(x, y \in A\)，\(x \oplus y \notin_T 0'\)。

## 13.3 超算术计算

在本节中，我们讨论超算术理论背景下关于有效界定的一些概念。这些结果将被应用于研究更高随机性。

#### 13.3.1 超算术支配

定义 13.3.1. 一个实数 \(x\) 是 \(\Delta^1_1\)-支配的，如果对于任何函数 \(f : \omega \to \omega\) 且 \(f \le_T x\)，存在一个超算术的 \(g\)，使得 \((\forall n)(g(n) > f(n))\)（记作 \(g > f\)）。

首先需要注意的是，存在大量的 \(\Delta^1_1\)-支配实数。

定理 13.3.2 (Chong, Nies and Yu [12])。\(\mu(\{x \mid x \text{ 是 } \Delta^1_1\text{-支配的}\}) = 1\)。

证明。我们证明对于任何随机数 \(p\)，\(\mu(\{x \mid x \text{ 是 } \Delta^1_1\text{-支配的}\}) \ge p\)。

这通过使用融合论证来实现。

首先，我们证明对于任何 \(e\)、有理数 \(r\)、记号 \(n \in \mathcal{O}\) 以及 \(\Delta^1_1\)-集 \(A\)，其中 \(p + r < \mu(A)\)，存在一个超算术函数 \(f\)，使得 \(\mu(\{x \mid x \in A \wedge \Phi_e^{B_k} \text{ 是全函数} \to \Phi_e^{B_k} < f\}) > p + \frac{r}{2}\)。

注意集合 \(\{(x, i, m) \mid \Phi_e^{B_k}(i) \downarrow \to \Phi_e^{B_k}(i) < m\}\) 是 \(\Delta^1_1\)。由于 \(A\) 是 \(\Delta^1_1\)，命题 13.1.6 蕴含集合 \(C = \{(i, m, k) \in \omega^3 \mid \mu(\{x \mid x \in A \wedge (\Phi_e^{B_k}(i) \downarrow \to \Phi_e^{B_k}(i) < m)\}) > \mu(A) - \frac{r}{2^{k+2}}\}\) 是 \(\Delta^1_1\)。注意对于每个 \(k\)，存在一个 \(m\) 使得 \((k, m, k) \in C\)。因此存在一个 \(\Delta^1_1\) 全函数 \(f\)，使得对于所有 \(k\)，\((k, f(k), k) \in C\)。定义 \(B_k = \{x \mid x \in A \wedge (\Phi_e^{B_k}(k) \downarrow \to \Phi_e^{B_k}(k) < f(k))\}\)。

那么集合 \(\{(k, x) \mid x \in B_k\}\) 是 \(\Delta^1_1\)。此外，对于每个 \(k\)，\(B_k \subseteq A\) 且 \(\mu(B_k) > \mu(A) - \frac{r}{2^{k+2}}\)。因此 \(B = \cap_k B_k\) 是 \(\Delta^1_1\) 且 \(\mu(B) \ge \mu(A) - \sum_{k \ge 0} \mu(A - B_k) \ge p + r - \sum_{k \ge 0} \frac{r}{2^{k+2}} = p + \frac{r}{2}\)。





现在对于每个 \(x \in B\)，如果 \(\Phi_e^{H_s}\) 是全函数，则 \(\Phi_e^{H_s} < f\)。因此我们可以构造一个 \(\omega\)-序列的 \(\Delta_1^1\)-集 \(\{B^{(e,n)}\}_{e<n,e \in \Omega}\) 使得

- (1) 如果 \((e, n) > (e', n')\)，则 \(B^{(e,n)} \subseteq B^{(e',n')}\);
- (2) \(\mu(B^{(e,n)}) > p\).

定义

\(D = \{x \mid \omega_1^x = \omega_1^{CK}\} \cap (\bigcap_{e < \omega \wedge e \in \Omega} B^{(e,n)})\).

根据定理 13.1.4，\(D \subseteq [x \text{ 是 } \Delta_1^1\text{-dominated}]\) 且 \(\mu(D) \ge p\)。\(\square\)

显然，如果 \(x\) 是 \(\Delta_1^1\)-dominated，则 \(\omega_1^x = \omega_1^{CK}\)。然而逆命题不成立。

**命题 13.3.3.** *存在一个不可数的* \(\Sigma_1^1\)*-集 A，其中每个 x 超算术地计算一个 f，使得对于每个超算术函数 g 都有 f > g。*

*证明.* 显然存在一个 Turing oracle 函数 \(\Phi\)，使得 \(\Phi^\Omega\) 支配所有超算术函数。令

\(A = \{x \mid \Phi^x \text{ 是全函数 } \wedge (\forall f (f \in \text{HYP} \rightarrow f < \Phi^x))\}\).

根据推论 2.2.12，\(A\) 是 \(\Sigma_1^1\)。由于 \(\Omega \in A\)，根据引理 2.5.4，\(A\) 是不可数的。\(\square\)

因此根据 Gandy 基础定理 (2.5.3)，我们有以下结论。

**推论 13.3.4.** *存在一个 x，使得* \(\omega_1^x = \omega_1^{CK}\) *但 x 不是* \(\Delta_1^1\)*-dominated.*

### 13.3.2 可追踪性

**定义 13.3.5.**

- (i) 设 \(h\) 为一个非递减无界且超算术的函数。带界 \(h\) 的 \(\Pi_1^1\)-迹/\(\Delta_1^1\)-迹是一个 \(\Pi_1^1/\Delta_1^1\)-集 \(T \subseteq \omega \times \omega\)，使得对每个 \(e\) 都有 \(|T_e| \le h(e)\)，其中 \(T_e = \{k \mid (e, k) \in T\}\)。
- (ii) \(x\) 是 \(\Pi_1^1\)-可追踪/\(\Delta_1^1\)-可追踪，如果存在一个 \(h \in \Delta_1^1\)，使得对每个 \(f \le_h x\)，都存在一个带界 \(h\) 的 \(\Pi_1^1\)-迹/\(\Delta_1^1\)-迹 \(T\)，使得对每个 \(e\) 都有 \(f(e) \in T_e\)。

不难看出，界函数 \(h\) 可以选为任意超算术函数，例如对每个 \(e\) 取 \(h(e) = e\)。

**命题 13.3.6** (Chong, Nies 和 Yu [12]). *如果 x 是* \(\Pi_1^1\)*-可追踪，则 x 是* \(\Delta_1^1\)*-可追踪。*

*证明.* 首先我们证明 \(\omega_1^x = \omega_1^{CK}\)。只需证明 \(\Omega\) 不是 \(\Pi_1^1\)-可追踪的。由于每个 \(\Pi_1^1\)-集都 many-one 归约到 \(\Omega\)，存在一个一致 \(\emptyset\)-递归的列表 \((T^e)_{e \in \omega}\)，即所有带界 \(h(e) = e\) 的 \(\Pi_1^1\)-迹。定义 \(f \le_h \Omega\) 为

\(f(e) = \mu n [n \notin T_e^e]\)。

那么 $f$ 没有 \(\Pi^1_1\)-迹。现在给定 $f \le_T x$，存在一个 \(\Pi^1_1\)-迹 \((T_e)_{e < \omega}\)，使得对每个 \(e\) 都有 \(f(e) \in T_e\)。那么存在一个递归函数 \(h : \omega^2 \to \omega\)，使得 \(k \in T_e\) 当且仅当 \(h(k, e) \in \Pi^1(x)\)-关系 \(R \subseteq \omega \times \Omega\)，由

\((e, n) \in R \Rightarrow h(f(e)) \in \Theta_n\)。

注意，对每个 \(e\)，存在一个记号 \(n \in \Theta\) 使得 \((e, n) \in R\)。根据 \(\Pi^1_1\)-一致化定理 (4.2.1)，存在一个全的 \(\Pi^1_1(x)\)（因此也是 \(\Delta^1_1(x)\)）函数 \(g\) 使 \(R\) 一致化。由于 \(\omega_1^{CK} = \omega_1^x\)，存在一个记号 \(n_0 \in \Theta\)，使得对每个 \(e\) 都有 \(|g(e)| < |n_0|\)。定义集合 \(\tilde{T}_e \subseteq T_e\) 如下：

\(k \in \tilde{T}_e \Rightarrow h(k, e) \in \Theta_{n_0}\)。

根据 \(n_0\) 的定义，对所有 \(e \in \omega\) 都有 \(f(e) \in \tilde{T}_e\)。注意关系 \(n \in \tilde{T}_e\) 是 \(\Delta^1_1\)。因此 \((T_e)_{e < \omega}\) 是 \(f\) 的一个 \(\Delta^1_1\)-迹。由此可见 \(f\) 是 \(\Delta^1_1\)-可追踪的。

\(\Delta^1_1\)-可追踪实数也有大量供应。事实上，每个 Sacks 一般实都是 \(\Delta^1_1\)-可追踪的。

#### 命题 13.3.7. 每个 Sacks 一般实都是 \(\Delta^1_1\)-可追踪的。

**证明.** 假设 $x$ 是 Sacks 一般的。那么 \(\omega_1^x = \omega_1^{CK}\)。如果 $f \le_T x$，那么存在一个 $e$ 和一个记号 $n \in \Theta$ 使得 $\Phi_e^{\tilde{H}_e} = f$。注意分级公式

$(\exists z^{[n]})(H(n, z^{[n]}, y) \wedge \Phi_e^{\tilde{H}_e^{[n]}}(i) = j)$

定义集合 $A = \{(y, n, i, j)|\Phi_e^{\tilde{H}_e}(i) = j\}$。为简化起见，我们可以将 $\Phi_e^{\tilde{H}_e}$ 视为一个分级公式。由于 $\Phi_e^{\tilde{H}_e}$ 是全函数，根据引理 5.3.6，存在一个条件 $T \Vdash \text{``}\Phi_e^{\tilde{H}_e} \text{ 是全函数''}$。我们证明，对每个条件 $S \le T$，存在一个条件 $Q \le S$ 使得

$Q \models (\exists f)(f \in \Delta^1_1 \wedge (\forall i)(\Phi_e^{\tilde{H}_e^{[i]}}(i) \in D_{f(i)} \wedge |D_{f(i)}| \le 2^{i+1}))$。

然后根据强迫的定义，存在一个 \(\Delta^1_1\) 函数 $f$ 使得对所有 $i$，\(\Phi_e^{\tilde{H}_e}(i) \in D_{f(i)} \wedge |D_{f(i)}| \le 2^{i+1}$。由于 \(T \Vdash \text{``}\Phi_e^{\tilde{H}_e} \text{ 是全函数''}\)，$S$ 也强迫同一句子。我们考虑两种情况。

情况 1. 存在一个条件 $R \le S$ 使得对所有 $i, j_0, j_1$ 和所有条件 $P_0, P_1 \le R$，如果 $P_0 \Vdash \Phi_e^{\tilde{H}_e}(i) = j_0$ 且 $P_1 \Vdash \Phi_e^{\tilde{H}_e}(i) = j_1$，则 $j_0 = j_1$。在这种情况下，定义 $f(i) = j$ 当且仅当存在一个条件 $P \le R$ 使得 $P \Vdash \Phi_e^{\tilde{H}_e}(i) = j$。那么 $f$ 是一个全的 \(\Pi^1_1\)-函数，因此也是 \(\Delta^1_1$。这意味着 \(R \Vdash f = \Phi_e^{\tilde{H}_e}\)。

情况 2. 否则。定义一个 \(\Pi^1_1$-关系 \(\mathfrak{R}(P, \sigma, i, j_0, Q_0, Q_1)\) 为

\(i \ge |\sigma| \wedge \sigma_0 \neq j_1 \wedge \Lambda \cap \sigma_0 \cap Q_1 = \emptyset \wedge (\forall k \le Q_1)(\exists k \supseteq \sigma Q_k \models \Phi_e^{\tilde{H}_e^{[k]}}(i) = j_k)\)。

根据 \(\Pi^1_1$-一致化定理 (4.2.1)，存在一个 \(\Pi^1_1$-函数 \(F : 2^\omega \times 2^{<\omega} \to (\omega)^3 \times (2^\omega)^\omega\) 使得 \(\mathfrak{R}(P, \sigma, i, j_0, j_1, Q_0, Q_1)\) 成立当且仅当 \(\mathfrak{R}(P, \sigma, F(P, \sigma))$。

不失一般性，我们假设如果 $P \Vdash \Phi_e^{G(i)} = j_i$，则对所有 \(k \le i\)，存在某个 \(j_k\) 使得 $P \Vdash \Phi_e^{G(i)}(k) = j_k$。通过对 \(\omega\) 归纳定义一个 \(\Pi^1_1$-条件序列 \(\{P_\sigma\}_{\sigma \in 2^{<\omega}}\) 如下：

- 步骤 0. 令 \(P_\emptyset = S\)。
- 步骤 \(n + 1$. 对每个 \(\sigma \in 2^n\)，如果 \(F(P_\sigma, \sigma) = (i, j_0, j_1, Q_0, Q_1)\)，则定义 \(P_{\sigma^\frown 0} = Q_0\)，\(P_{\sigma^\frown 1} = Q_1\)。

令 \(G(\sigma) = P_\sigma$。那么 \(G\) 是一个全的 \(\Pi^1_1$-函数，因此也是 \(\Delta^1_1$。注意对每个 \(\sigma\)，\(G(\sigma^\frown 0) \cap G(\sigma^\frown 1) = \emptyset\)，且如果 \(\sigma \subseteq \tau\) 则 \(G(\sigma) \supseteq G(\tau)\)。令

\(Q = \bigcup_n \bigcap_{\sigma \in 2^{\geq n}} G(\sigma)\)。

那么 \(Q\) 是一个 \(\Delta^1_1$ 完美集。

定义 \(g : \bigcup_{k \in \omega} 2^{2k+1} \to \omega$ 使得如果 \(\sigma \in 2^{i+1}\) 且 \(G(\sigma) \Vdash \Phi_e^{G(i)} = k\)，则 \(g(i, \sigma) = k$。因此 \(g\) 是一个全的 \(\Pi^1_1$ 且因此是 \(\Delta^1_1$-函数。定义 \(f(i) = j$ 如果 \(j\) 是使得 \(D_j = \{g(i, \sigma) \mid \sigma \in 2^{i+1}\}\) 的最小数。那么 \(f\) 是一个 \(\Delta^1_1$-函数，且对所有 $i$ 都有 \(|D_{f(i)}| \le 2^{i+1}$。由于对所有 $i$ 都有 \(Q \subseteq \bigcup_{\sigma \in 2^i} G(\sigma)$，很容易看出 \(Q \Vdash \Phi_e^{G(i)} \in D_{f(i)}$。由此可见 \(x\) 是 \(\Delta^1_1$-可追踪的。

我们稍后将看到（定理 14.6.8），\(\Delta^1_1$-可追踪实数的集是零集。

根据定理 5.3.12，存在一个不可数的 \(\Sigma^1_1$-弱 Sacks 一般实集，其中每个实 \(x\) 都具有性质 \(\omega_1^x = \omega_1^{CK}$。根据命题 13.3.7 的证明，很容易推导出以下结论。

#### 推论 13.3.38. 存在一个不可数的 \(\Sigma^1_1$-\(\Delta^1_1$-可追踪实集。

### 13.3.3 半可追踪性

#### 定义 13.3.9.

- (i) \(x \in 2^\omega\) 是 \(\Delta^1_1$-半可追踪的，如果对每个 \(f \le_{tt} x\)，存在一个 \(\Delta^1_1$-函数 \(g\) 使得对无穷多个 \(n\) 有 \(f(n) = g(n)$。我们说 \(g\) 半迹迹 \(f$。
- (ii) \(x \in 2^\omega\) 是 \(\Pi^1_1$-半可追踪的，如果对每个 \(f \le_h x\)，存在一个偏 \(\Pi^1_1$-函数 \(p\) 使得对无穷多个 \(n\) 有 \(f(n) = p(n)$。

#### 引理 13.3.10. \(x\) 是 \(\Pi^1_1$-半可追踪的当且仅当 \(x\) 是 \(\Delta^1_1$-半可追踪的。

**证明.**

不难看出，如果 \(x\) 是 \(\Pi^1_1$-半可追踪的，则 \(\omega_1^x = \omega_1^{CK}$。否则 \(x \ge_h \emptyset$。因此只需证明 \(\emptyset\) 不是 \(\Pi^1_1$-半可追踪的。设 \(\{\Phi_i\}_{i \in \omega}$ 为偏递归函数的有效枚举。设 \(m_i^j$ 为使得 \(p_i(j, k) \in \emptyset$ 的最小 \(k$（如果存在），否则取 0。定义函数 \(g \le_T \emptyset'$ 使得 \(g(i) = \bigcup_{j \le i} m_i^j + 1$。注意，对任何 \(\Pi^1_1$-偏函数 \(p\)，存在一个偏递归函数 \(p_i$ 使得对每对 \(n, m\)，\(p(n) = m$ 当且仅当 \(p_i(n, m) \in \emptyset$。然后根据 \(g$ 的定义，对任何 \(i > j\)，\(g(k) \neq p(i)$。因此 \(g$ 不被 \(p$ 迹迹。





假设 $x$ 是 $\Pi^1_1$-半可追踪的，$\omega_1^x = \omega_1^{ck,x}$，且 $f \leq_h x$。修正一个 $\Pi^1_1$-偏函数 $p$ 以作 $f$ 见证 $x$ 的半可追踪性。由于 $p$ 是一个 $\Pi^1_1$-函数，存在一个递归单射 $h$ 使得 $p(m) = m \leftrightarrow h(m, m) \in O$。

令 $R(n, m)$ 为一个 $\Pi^1_1(x)$-关系，使得 $R(n, m)$ 当且仅当存在一个 $k$，其中 $m > k \geq n$，使得 $f(k) = p(k)$。那么存在一个全函数 $g$ 对 $R$ 进行统一化，使得 $g$ 是 $\Pi^1_1(x)$，因此也是 $\Delta^1_1(x)$。于是对于每个 $n$，存在一个 $m \in [g(n), g(g(n))]$ 使得 $f(m) = p(m)$。令 $g'(0) = g(0)$，且对所有 $n < \omega$ 有 $g'(n + 1) = g(g'(n))$。定义一个 $\Pi^1_1(x)$-关系 $S(n, m)$，使得 $S(n, m)$ 当且仅当 $m \in [g'(n), g'(n + 1))$ 且 $p(m) = f(m)$。对 $S$ 进行统一化，我们得到一个 $\Delta^1_1(x)$-函数 $g''$。

令 $H = \{h(m, k) \mid k \in (\exists n)(g''(n) = m \land f(m) = k)\}$。那么 $H$ 是 $\Delta^1_1(x)$，且由于 $\omega_1^x = \omega_1^{ck,x}$，存在某个 $n \in O$ 使得 $H \subseteq O_n$。由于 $O_n$ 是 $\Delta^1_1$，我们可以定义一个 $\Delta^1_1$-函数 $\bar{f}$：若 $h(i, j) \in O_n$ 则令 $\bar{f}(i) = j$，否则令 $\bar{f}(i) = 1$。那么存在无穷多个 $i$ 使得 $f(i) = \bar{f}(i)$。

下文阐明了可追踪性与半可追踪性之间的关系。

### 提议 13.3.11 (Kjos-Hanssen, Nies, Stephan 和 Yu [68]). 每个 $\Delta^1_1$-可追踪实都是 $\Delta^1_1$-被支配的和 $\Delta^1_1$-半支配的。

证明. 显然每个 $\Delta^1_1$-可追踪实都是 $\Delta^1_1$-被支配的。设 $x$ 为一个 $\Delta^1_1$-可追踪实，设 $f$ 为一个 $\Delta^1_1(x)$-函数。定义 $g(n) = \langle f(2^n), f(2^n + 2), \dots, f(2^{n+1} - 1) \rangle$。那么存在一个 $\Delta^1_1$ 迹 $T$ 对 $g$ 进行追踪，使得对所有 $n$ 有 $|T|_n \leq n$。

对于 $2^n + 1 \leq m \leq 2^{n+1}$，令 $\bar{f}[m]$ 为元组的第 $(m - 2^n)$ 项，该元组是 $T_n$ 的第 $(m - 2^n)$ 个元素（若存在这样的元组），否则令 $\bar{f}(m) = 1$。不难看出，对于每个 $n$，至少存在一个 $m \in [2^n, 2^{n+1})$ 使得 $f(m) = \bar{f}(m)$。

### 推论 13.3.12. 实 $x$ 是 $\Delta^1_1$-可追踪的，当且仅当对于每个在 $x$ 中超算术的 $\bar{y}$，存在一个超算术函数 $f$ 使得

$(\forall n)(\exists m \in [2^n, 2^{n+1}))(f(m) = \bar{f}(m))$。

### 提议 13.3.13. 对任意 $x$，以下等价。

- (i) $x$ 是 $\Delta^1_1$-半支配的和 $\Delta^1_1$-被支配的；
- (ii) 对每个函数 $g \leq_h x$，存在一个递增的 $\Delta^1_1$-函数 $f$ 和一个 $\Delta^1_1$-函数 $F : \omega \to \mathscr{P}_{<\omega}(\omega)$，其中 $|F(n)| \leq n$，使得

$(\forall n)(\exists m \in [f(n), f(n+1)))(g(m) \in F(m))$。

证明. (i) $\Rightarrow$ (ii)：立即成立，因为 $1 \leq n$。

(ii) $\Rightarrow$ (i)。假设 $\bar{g} \leq_h x$。不失一般性，假设 $\bar{g}$ 是单调非递减的。设 $f$ 和 $F$ 为相应的 $\Delta^1_1$-函数。令 $u(n) = \sum_{k \in [f(n)+1)} k_{k \in F(k)}$，并注意 $u$ 是一个支配 $\bar{g}$ 的 $\Delta^1_1$-函数。令

$h(n) = \langle \bar{g}(2^n + 1), \bar{g}(2^n + 2), \dots, \bar{g}(2^{n+1} - 1) \rangle$。则由假设存在相应的 $\Delta^1_1$-函数 $f_n$ 和 $F_n$。对每个 $n$ 和 $m \in [2^n, 2^{n+1})$，若存在这样的 $m$，令 $g(m)$ 为 $F_h(n)$ 中第 $(m - 2^n)$ 个元素的第 $(m - 2^n)$ 项，否则令 $g(m) = 1$。那么 $g$ 是一个对 $\bar{g}$ 进行半追踪的 $\Delta^1_1$-函数。

为了将 $\Delta^1_1$-可追踪性与 $\Delta^1_1$-半可追踪性和 $\Delta^1_1$-支配性的合取分开，人们应用了一个修改过的 Sacks 强迫构造。

### 定义 13.3.14.

- (i) 一个 $\Delta^1_1$-完美树 $T \subseteq 2^{<\omega}$ *在 n 处完全分裂*，如果对于每个 $\sigma \in T$ 且 $|\sigma| \in [2^n, 2^{n+1})$，$\sigma 0$ 和 $\sigma 1$ 都在 $T$ 中。此时称 $n$ 为 $T$ 的*完全分裂层*。
- (ii) 一个 $\Delta^1_1$-完美树 $T \subseteq 2^{<\omega}$ 是*团状的*，如果存在无穷多个 $n$ 使得 $T$ 在 $n$ 处完全分裂。

令 $\mathbb{F} = \langle F, \le \rangle$ 为按包含关系序团状树的偏序集。给定在分析层次分支语言（§ 5.1.1）$\mathscr{L}(\omega_1^{ck}, X)$ 中的一个公式 $\varphi$，如同在 Sacks 强迫法中一样定义强迫关系 $T \Vdash \varphi$：

- 若 $\varphi$ 为有秩句子且 $(\forall x \in T)(\exists(\alpha \in O^{ck}, x) \Vdash \varphi)$，则 $T \Vdash \varphi$；
- 若 $\varphi(y)$ 为无秩且存在某个秩至多为 $\beta$ 的 $\psi$ 使得 $T \Vdash \varphi(y \mid \psi)$，则 $T \Vdash (\exists y)^\beta \varphi(y^\alpha)$；
- 若 $T \Vdash (\exists y)^\beta \varphi(y^\alpha)$，则 $T \Vdash (\exists y)\varphi(y)$；
- 若 $\varphi(n)$ 为无秩且存在某个数词 $\bar{m}$ 使得 $T \Vdash \varphi(\bar{m})$，则 $T \Vdash (\exists n)\varphi(n)$；
- 若 $\varphi$ 和 $\psi$ 均为无秩，$T \Vdash \varphi$ 且 $T \Vdash \psi$，则 $T \Vdash \varphi \land \psi$；
- 若 $\varphi$ 为无秩且 $(\forall p)(P \subseteq T \rightarrow P \Vdash \varphi)$，则 $T \Vdash \neg \varphi$。

由定理 5.1.1，我们有以下结论。

### 引理 13.3.15.

集合

\(\{ (T, \ulcorner \varphi \urcorner) \mid T \text{ 是一个条件 } \land \varphi \text{ 是 } \Sigma_1^1 \land T \Vdash \varphi \}\)

是 $\Pi_1^1$。

### 引理 13.3.16.

- (i) 设 $\langle \varphi_i \rangle_{i < \omega}$ 为一个超算术的 $\Sigma_1^1$-句子序列。假设对于每个 $i$ 和 $Q \le T$，存在一个 $R \le Q$ 使得 $R \Vdash \varphi_i$。那么存在一个 $R \le T$ 使得对每个 $i$ 都有 $R \Vdash \varphi_i$。
- (ii) $(\forall \psi)(\forall T)(\exists Q \le T)(Q \Vdash \psi \lor Q \Vdash \neg \psi)$。

证明. 使用记号 $P \Vdash n = \{ \tau \in 2^{<\omega} \mid \tau \in P \}$，定义一个 $\Pi_1^1$-关系 $\mathcal{R}$ 为

\(\mathcal{R}(R, i, \sigma, P) \leftrightarrow (\sigma \in R \wedge P \subseteq R \wedge P \Vdash \varphi_i \wedge P \Vdash [\sigma] = \{ \tau \mid \tau < \sigma \} \wedge \log |\sigma| - 1 \text{ 是 } R \text{ 的第 } i \text{ 个完全分裂层})。\)

然后 $\mathcal{R}$ 由一个偏 $\Pi_1^1$-函数 $F : F \times \omega \times 2^{<\omega} \rightarrow \mathbf{F}$ 统一化。利用 $F$，可通过对 $\sigma$ 递归定义一个超算术族 $\langle P_\sigma \mid \sigma \in 2^{<\omega} \rangle$。令 \( P_\alpha = T \)。若 \( \sigma \notin P_\alpha \)，令 \( P_\sigma \cap P_\alpha = \emptyset \)。若 \( \log |\sigma| - 1 \) 不是 \( P_\alpha \) 的完全分裂层，令 \( P_\sigma \cap P_\alpha = P_\alpha \)。否则，\( P_\sigma \cap P_\alpha = \emptyset, P_\sigma \cup P_\alpha \subseteq P_\alpha, P_\sigma \cap [\sigma], P_\sigma \cap [\sigma] \models [\sigma] = \{ \tau \mid \tau \prec \sigma \} \) 且 \( P_\sigma \cap P_\alpha \models \bigwedge_{i \le i} \psi_i \)，其中 \( \log |\sigma| - 1 \) 是 $T$ 的第 $i$ 个完全分裂层。

令 \( R = \cap_i \bigcup_{|g|=n} P_\alpha \)。则 \( R \in \mathbf{F} \)。可以常规地验证对于每个 $i$ 都有 \( R \models \varphi_i \)。(ii) 的证明与引理 5.3.4 的证明类似。

实 $x$ 是通用的，如果对于每个在 $\mathcal{O}$ 中可算的稠密集 $\mathscr{D} \subseteq \mathbf{F}$，存在一个 $T \in \mathscr{D}$ 使得 $x \in [T]$。可以如同引理 5.3.6 的证明中所示，对于每个句子 $\varphi$ 和通用 $x$，

\( \mathfrak{A}(\omega_1^{CK}, x) \models \varphi \iff (\exists P)(x \in P \land P \models \varphi) \)。

### 引理 13.3.17.

- (i) \( \mathfrak{A}(\omega_1^{CK}, x) \) 满足 \( \Delta_1^1 \)-理解公理。因此 \( \omega_1^x = \omega_1^{CK} \)；
- (ii) \( x \) 是 \( \Delta_1^1 \)-被支配的和 \( \Delta_1^1 \)-半可追踪的；
- (iii) \( x \) 不是 \( \Delta_1^1 \)-可追踪的。

证明. (i) 的证明与引理 5.3.7 相同，留给读者。

对于 (ii)，由提议 13.3.13，只需证明对于每个条件 \( g \le_h x \)，存在一个递增的 \( \Delta_1^1 \)-函数 \( f \) 和一个 \( \Delta_1^1 \)-函数 \( F : \omega \to \omega^\omega \)，使得

- (1) \( |F(n)| \le n \)；
- (2) 每个区间 \( [f(n), f(n) + 1) \) 捕获一个 $m$ 使得 $g(m) \in F(m)$。

由于 \( g \le_h x \) 且 \( \omega_1^x = \omega_1^{CK} \)，存在一个有秩公式 \( \varphi \) 使得对每个 $n$，$g(n) = m$ 当且仅当 \( \mathfrak{A}(\omega_1^{CK}, x) \models \varphi(n, m) \)。因此存在一个条件 \( S \models (\forall n)(\exists m)\varphi(n, m) \)。令 \( T \subseteq S \)。如同在引理 13.3.16 的证明中，可以构造一个条件的超算术序列 \( \langle P_\sigma \rangle_{\sigma \in 2^{<\omega}} \)，使得

\( P \models \varphi(0, [m_0, m_0 + 1)) \) 对 $i \le 1$ 成立

其中 \( \sigma \in P_\alpha \) 且 \( \log |\sigma| - 1 \) 是 \( P_\alpha \) 的一个完全分裂层。令 $Q$ 如同在引理 13.3.16 的证明中所定义。令 $f$ 为这样的 \( \Delta_1^1 \)-函数：$f(0) = 0$，且 $f(n+1)$ 是大于 $f(n)$ 的最小数 $k$，使得对某个满足 $f(n) < |\sigma| < k$ 的 $\sigma$，$m_0$ 有定义。令 \( F(n) = \{0\} \cup \{m_0 \mid |\sigma| = n\} \)，并注意 $f$ 是一个 \( \Delta_1^1 \)-函数。那么

\( Q \models (\forall n)(|F(n)| \le n) \land (\forall n)(\exists m \in [f(n), f(n) + 1))(\exists i \in F(m))(\varphi(m, i)) \)。

这意味着

\( Q \models (\exists F)(\exists f)[(\forall n)(|F(n)| \le n) \land (\forall n)(\exists m \in [f(n), f(n) + 1))(\exists i \in F(m))(\varphi(m, i))] \)。

由于 \( T \) 是比 $S$ 更强的任意条件，故有

\( S \models (\exists F)(\exists f)[(\forall n)(|F(n)| \le n) \land (\forall n)(\exists m \in [f(n), f(n) + 1))(\exists i \in F(m))(\varphi(m, i))] \)。

由于 \( x \in S \),

\( \mathfrak{A}(\omega_1^{CK}, x) \models (\exists F)(\exists f)[(\forall n)(|F(n)| \le n) \land \)
\( (\forall n)(\exists m \in [f(n), f(n) + 1))(\exists i \in F(m))(\varphi(m, i))] \)。

因此 $x$ 是 \( \Delta_1^1 \)-被支配的和 \( \Delta_1^1 \)-半可追踪的。




对于 (iii)，假设 \( f : \omega \to \omega \) 是一个 \(\Delta^1_1\)-函数，使得对于每个 \( n \)，存在一个 \( m \in [2^n, 2^{n+1}) \) 使得 \( f(m) = x(m) \)。那么存在一个分级公式 \( \varphi \)，使得 \( f(n) = m \Leftrightarrow \mathcal{A}(\omega_1^{CK}, x) \models \varphi(\bar{n}, \bar{m}) \)。此外，\(\mathcal{A}(\omega_1^{CK}, x) \models (\forall n)(\exists m \in [2^n, 2^{n+1}))(\varphi(m, x(m)))\)。因此存在一个条件 \( T \)，它强制 \( (\forall n)(\exists m \in [2^n, 2^{n+1}))(\varphi(m, x(m))) \) 且 \( x \in T \)。令 \( n \) 使得 \( T \) 在层级 \( n \) 处完全分裂，并令 \( \sigma \in 2^{n-1} \) 成为 \( T \) 中的一个字符串。令 \( v \) 成为一个字符串，使得 \( v(m) = 1 - f(m + 2^{n-1}) \)。定义 \( S = \{\sigma^\frown \tau \mid \tau \in T\} \subseteq T \)。那么 \( S \Vdash (\forall m \in [2^n, 2^{n+1}))(\neg \varphi(m, x(m)))\)。但 \( S \) 比 \( T \) 更强，这是一个矛盾。根据推论 13.3.12，\( x \) 不是 \(\Delta^1_1\)-可迹的。

我们现在可以将 \(\Delta^1_1\)-可迹性与 \(\Delta^1_1\)-半递归性和 \(\Delta^1_1\)-支配性的合取分开。

#### 定理 13.3.18 (Kjos-Hanssen, Nies, Stephan and Yu [68]). 存在 \( 2^{\aleph_0} \) 个 \(\Delta^1_1\)-支配且 \(\Delta^1_1\)-半递归实数，它们不是 \(\Delta^1_1\)-可迹的。

**证明.** 这直接由引理 13.3.17 得出。注意存在 \( 2^{\aleph_0} \) 个泛化实数。

通过与定理 5.3.12 证明中完全相同的论证，我们有以下结论。

#### 命题 13.3.19. 存在一个不可数的 \(\Sigma^1_1\)-集合，它仅包含 \(\Delta^1_1\)-支配和 \(\Delta^1_1\)-半递归实数。

#### 13.3.4 练习

- **练习 13.3.1.** 证明没有 Cohen 泛化实数是 \(\Delta^1_1\)-支配的。

- **练习 13.3.2.** 证明每个 Cohen 泛化实数都是 \(\Delta^1_1\)-半递归的。

- **练习 13.3.3.** 证明命题 13.3.19。

## 14 高阶随机性理论

高阶随机性理论利用超算术理论和集合论的技术和思想，研究随机性的算法复杂性问题。由于二阶算术提供了对实数更广阔（尽管有时更粗略）的视角，人们得到的随机性图景与一阶理论的图景截然不同。

### 14.1 高阶 Kurtz 随机性

#### 14.1.1 \(\Delta^1_1\) 和 \(\Pi^1_1\)-Kurtz 随机性

**定义 14.11.** 令 \(x \in 2^\omega\)。给定实数集的一个类 \(\Gamma\)，如果 \(x\) 不属于 \(\Gamma\) 中的任何闭零集，则称 \(x\) 是 \(\Gamma\)-Kurtz 随机的。

我们关注 \(\Delta^1_1\)、\(\Sigma^1_1\) 和 \(\Pi^1_1\)-Kurtz 随机性。回顾（§ 2.7.1），BC 表示博雷尔码的集合，\(\{A_z \mid z \in \text{BC}\}\) 是由这些码生成的实数集合。

#### 命题 14.1.2.

- (i) \(x\) 是 \(\Delta^1_1\)-Kurtz 随机的，当且仅当 \(x\) 不属于任何 \(\Pi^1_1(\text{HYP})\)-零集。

- (ii) \(\Delta^1_1\)-Kurtz 随机实数的集合是 \(\Sigma^1_1\) 但不是 \(\Delta^1_1\)。

证明. 注意 (i) 直接由定理 2.7.4 得出。此处给出一个自包含的证明。

根据定理 2.7.2，每个 \(\Pi^1_1(\text{HYP})\)-集合都是一个 \(\Delta^1_1\)-集合。因此没有 \(\Delta^1_1\)-Kurtz 随机实数属于一个 \(\Pi^1_1(\text{HYP})\)-零集。反之，令 \(P\) 成为一个 \(\Delta^1_1\)-零集。那么 \(U = \{\sigma \mid (\forall z)(\forall x \in P \to z \neq \sigma) \text{ 是 } \Pi^1_1\}\)。由于 \(P\) 是闭集，且超算术实数的集合是稠密的，我们有

\(\sigma \in U \iff (\forall z \in \text{HYP})(z > \sigma \to z \notin P)\).

根据推论 2.2.12，\(U\) 也是 \(\Sigma^1_1\)，因此是 \(\Delta^1_1\)。故 \(P \in \Pi^1_1(\text{HYP})\)。由此可见 \(x\) 不属于一个 \(\Pi^1_1(\text{HYP})\)-零集，因此 \(x\) 是 \(\Delta^1_1\)-Kurtz 随机的。

为了证明 (ii)，观察集合

\(C = \{(\langle n, e \rangle, y) \mid n \in \emptyset \land \Delta^{B_n}_e \in \Pi_1 \cap \text{HYP} \land y \in A_{\varrho^{B_n}_e}\}\)

是 \(\Pi^1_1\)，其中 \(A_z\) 如 § 2.7.1 所定义。根据命题 13.1.6，集合

\(D = \{(\langle n, e \rangle, y) \mid \mu(y \mid ((\langle n, e \rangle, y) \in C)) = 0\}\)

是 \(\Pi^1_1\)。因此集合

\(E = \{y \mid (\exists m)((m, y) \in D)\}\)

是一个 \(\Pi^1_1\)-零集。此外，根据 (i)，

\((\forall x)(x \in E \to x \text{ 不是 } \Delta^1_1\text{-Kurtz 随机}).\)

因此 \(\Delta^1_1\)-Kurtz 随机实数的集合是 \(\Sigma^1_1\)。现在 \(\mu(E) = 1\)，并且由于没有超算术实数是 \(\Delta^1_1\)-Kurtz 随机的，根据定理 13.11.3 可得出 \(E\) 不是 \(\Delta^1_1\)。

#### 定理 14.1.3 (Kjos-Hanssen, Nies, Stephan and Yu [68]). \(\Pi^1_1\)-Kurtz 随机性 \(\subset \Sigma^1_1\)-Kurtz 随机性 \(= \Delta^1_1\)-Kurtz 随机性。

证明. 显然 \(\Pi^1_1\)-Kurtz 随机性 \(\subseteq \Sigma^1_1\)-Kurtz 随机性 \(\subseteq \Delta^1_1\)-Kurtz 随机性。我们表明第一个包含是真包含。令

\(R(\langle e, n \rangle, z) \Leftrightarrow n \in \emptyset \wedge \Phi_e^\emptyset \in \Sigma^1_1 \wedge \exists z \in \Phi_e^\emptyset \wedge\)
\((\mu(A_\sigma) > 1 - 2^{-(e,n)}).\)

根据命题 13.16.1，\(R\) 是 \(\Pi^1_1\)，并且根据定理 4.2.1，存在一个 \(\Pi^1_1\)-函数 \(f: \omega \to 2^{<\omega}\) 一致化 \(R\)。令

\(C = \{y \mid (\forall m)(f(m) \downarrow \to y \in A_{f(m)})\}.\)

那么 \(C\) 是一个闭的 \(\Sigma^1_1\)-集合，且 \(\mu(C) \ge 2^{-1}\)。注意，如果 \(z_1 \in \Sigma^1_1 \cap \text{HYP}\) 且对于某个 \(p\) 有 \(\mu(A_{z_1}) > p\)，那么存在一个有限的 \(z \le z_1\) 在 \(\Sigma^1_1 \cap \text{HYP}\) 中，使得 \(\mu(A_z) > p\)。根据命题 14.1.2，\(C\) 中的每个实数都是 \(\Delta^1_1\)-Kurtz 随机的。由于 \(C\) 是闭集且是 \(\Sigma^1_1\)，它可以由一个 \(\Sigma^1_1\)-树表示。根据定理 11.1.2，存在一个 \(x \in C\) 使得 \(x \equiv_h \emptyset\)。令 \(e\) 和 \(n \in \emptyset'\) 使得 \(x = \Phi_e^{H_n^\emptyset}\)。那么

\(z \in \{x\} \Leftrightarrow (\exists y \le_P x)(y \in \{0\} \Leftrightarrow x = \Phi_e^{H_n^\emptyset}).\)

换句话说，\(x\) 是一个 \(\Pi^1_1\)-单点，因此不是 \(\Pi^1_1\)-Kurtz 随机的。

我们现在表明每个 \(\Delta^1_1\)-Kurtz 随机实数都是 \(\Sigma^1_1\)-Kurtz 随机的。令 \(A\) 成为一个测度为 1 的 \(\Pi^1_1\)-开集。定义 \(X = \{ \sigma \in 2^{<\omega} (\forall y)(\forall \sigma \to y \in A) \}\)。那么 \(x\) 是一个编码 \(A\) 的 \(\Pi^1_1\)-实数（即 \(y \in A\) 当且仅当存在一个 \(\sigma \in x\) 使得 \(y \in A_\sigma\)）。因此存在一个递归函数 \(f : 2^{<\omega} \to \omega\)，使得 \(\sigma \in x\) 当且仅当 \(f(\sigma) \in \emptyset\)。定义一个 \(\Pi^1_1\)-关系 \(R \subseteq \omega \times \omega\)，使得 \((k, n) \in R\) 当且仅当 \(n \in \emptyset\) 且 \(\mu(\bigcup \{ \sigma \mid \exists m \in \emptyset_n)(f(\sigma) = m) \}) > 1 - \frac{1}{k}\)。显然 \(R\) 是一个可以由 \(\Pi^1_1\)-函数 \(f\) 一致化的 \(\Pi^1_1\)-关系。由于 \(\mu(A) = 1\)，\(f\) 是一个全函数。因此 \(f\) 的值域被一个记号 \(n \in \emptyset\) 所界定。定义 \(B = \{ y \mid (\exists \sigma)(y > \sigma \land f(\sigma) \in \emptyset_n) \}\)。那么 \(B \subseteq A\) 是一个测度为 1 的 \(\Delta^1_1\)-开集。由此可见，每个 \(\Pi^1_1\)-开余零集都有一个 \(\Delta^1_1\)-开余零子集。故 \(\Sigma^1_1\)-Kurtz 随机性 \(= \Delta^1_1\)-Kurtz 随机性。

以下结果阐明了 \(\Delta^1_1\) 和 \(\Pi^1_1\)-Kurtz 随机性之间的联系。

#### 命题 14.1.4. 如果 \(\omega_1^x = \omega_1^{CK}\)，那么 \(x\) 是 \(\Pi^1_1\)-Kurtz 随机的，当且仅当 \(x\) 是 \(\Delta^1_1\)-Kurtz 随机的。

证明. 假设 \(\omega_1^x = \omega_1^{CK}\) 且 \(x\) 是 \(\Delta^1_1\)-Kurtz 随机的。如果 \(A\) 是一个 \(\Pi^1_1\)-闭零集，使得 \(x \in A\)，那么根据 Spector-Gandy 定理 3.7.3，存在一个算术公式 \(\varphi(z, y)\)，使得公式 \((\exists z \in \text{HYP})\varphi(z, y)\) 定义 \(A\)。由于 \(\omega_1^x = \omega_1^{CK}\)，存在一个递归序数 \(\beta\)，使得

\(x \in B = \{ y \mid \exists \beta(\omega_1^{CK}, y) = (\exists \beta 2^\beta)(\varphi(x^\beta, y) \subseteq A \}.\)




定义 \( T = \{\sigma \in 2^{<\omega} \mid (\exists y \in B)(y \succ \sigma)\} \)。显然 \( B \subseteq [T] \)。由于 \( B \) 是 \( \Sigma_1^1 \)，\( [T] \) 是 \( \Sigma_1^1 \)。由于 \( A \) 是闭集，我们有 \( [T] \subseteq A \)。另外，\( A \) 是零集意味着 \( [T] \) 也是零集。根据引理 13.1.10 和 \( \Pi_1^1 \)-一致化的常规应用，存在一个全态的 \( \Sigma_1^1 \)-函数 \( f : \omega \to \text{HYP} \)，使得对于任意 \( k \)，\( f(k) \in \Sigma_1 \cap \text{HYP} \)，\( A_{f(k)} \subseteq 2^\omega \setminus [T] \) 且 \( \mu(A_{f(k)}) > 2^{-k} \)。令

```
\( C = \{z \mid (\forall k)(z_k \notin A_{f(k)})\} \)。
```

那么 \( C \) 是一个 \( \Sigma_1^1 \)-闭零集。然而，\( x \in C \)，这产生了矛盾。

### 14.1.2 Kurtz 随机实数的圆锥基

从定理 14.1.3 的证明可以看出，高于 \( \mathcal{O} \) 的超度都包含一个 \( \Sigma_1^1 \)-Kurtz 随机实数。这对于 \( \Pi_1^1 \)-Kurtz 随机性不成立。我们说，一个超度 \( \mathbf{a} \) 是 *T-Kurtz 随机性的圆锥基*，如果对于每个超度 \( \mathbf{b} \ge \mathbf{a} \)，\( \mathbf{b} \) 包含一个 \( T \)-Kurtz 随机实数。

\( \mathcal{O} \) 的超度是 \( \Sigma_1^1 \)-Kurtz 随机性的圆锥基，如定理 14.1.3 所证明。并非每个非零超度都是 \( \Sigma_1^1 \)-Kurtz 随机性的圆锥基（见引理 14.6.1）。是否存在 \( \Pi_1^1 \)-Kurtz 随机性的圆锥基？如果存在，这样的基，比如说 \( \mathbf{b} \)，不能高算术归约到一个 \( \Pi_1^1 \)-单元。这意味着充当基的超度必须相当复杂。

**引理 14.1.5.** 对于任意实数 \( x \) 和 \( z \ge_T x' \)，存在一个 \( x \)-Kurtz 随机实数 \( y \equiv_T z \)。

**证明.** 令 \( z \ge_T x' \) 并固定 \( x \)-t.e. 开集 \( \{U_n^s\}_{n < \omega} \) 的一个枚举。我们按如下方式构造字符串的一个递增序列 \( \{\sigma_s\}_{1 \le s < \omega} \)。

- 令 \( \sigma_0 = 0 \)。

- 阶段 \( s + 1 \)。令 \( l_0 = 0, l_1 = |\sigma_s| \)，且对于 \( n > 1 \)，\( l_{n+1} = 2^{l_n} \)。对于每个这样的 \( n \)，令

```
\( A_n = \{\sigma \in 2^{l_{n-1}} \mid (\exists m < n)(\forall i)(\forall j)(l_m \le i, j < l_{m+1} \implies \sigma(i) = \sigma(j))\} \)。
```

那么

```
\( |A_n| \le 2 \cdot 2^{-l_{n+1}} \)。
```

换句话说，

```
\( \mu(B_n = \bigcup \{[\sigma] \mid \sigma \ge \sigma_s \wedge \sigma \notin A_n\}) \ge 2^{-l_1} \cdot (1 - 2^{-l_{n+1} + l_{n+1}}) \)。
```

情况 1。存在一个 \( m > l_1 + 1 \)，使得 \( |\{\sigma \ge \sigma_s \mid \sigma \in 2^m \cap [\sigma] \subseteq U_k^s\}| > 2^{m-l_1-1} \)。

令 \( n = m + 1 \)。那么 \( l_{n+1} - 1 - l_n > 2 \) 且 \( l_n > m \)。存在一个 \( \sigma \in 2^{l_{n-1}} \setminus A_n \) 和一个 \( \tau \le \sigma \)，使得 \( [\tau] \subseteq U_k^s \) 且 \( \tau \ge 2^m \)。

令 \( \sigma_{s+1} = \sigma(s)^{[l_{n-1}]} \)。

情况 2。否则。令 \( \sigma_{s+1} = \sigma_s^c(s)^{[l_{s-1}]} \)。

这完成了阶段 \( s + 1 \) 的构造。令 \( U = \bigcup_s \sigma_s \)。显然该构造在 \( z \) 中是递归的，因此 \( y \ge_T z \)。此外，如果 \( U_k^s \) 的测度为 1，那么情况 1 在阶段 \( s + 1 \) 成立。因此 \( y \) 是 \( x \)-Kurtz 随机的。

令 \( l_0 = 0 \) 且对于 \( n > 0 \)，令 \( l_n = 2^n \)。要从 \( y \) 计算 \( z(n) \)，用 \( y \)-递归方式找到第 \( n \) 个 \( l_m \)，使得对于所有 \( i \)、\( j \) 且 \( l_m \le i < j < l_{m+1} \)，有 \( y(i) = y(j) \)。那么 \( z(n) = y(l_m) \)。

我们称 \( A \subseteq \omega \times 2^\omega \) 为一个通用的 \( \Pi_1^1 \)-闭集，如果 (i) 它是 \( \Pi_1^1 \)，(ii) 对于每个 \( n \)，\( A_n = \{x \mid (n, x) \in A\} \) 是一个 \( \Pi_1^1 \)-闭集，且 (iii) 每个 \( \Pi_1^1 \)-闭集都是某个 \( n \) 的 \( A_n \)。根据定理 13.1.3 和 13.1.14，实数 \( x_0 = \{n \mid \mu(A_n) = 0\} \) 是 \( \Sigma_1^1 \)。令

\( c = \{(n, \sigma) \mid n \in x_0 \wedge (\exists x)(n, x) \in A \wedge \sigma \prec x\} \subseteq \omega \times 2^{<\omega} \)。

那么 \( c \) 可以被视为一个 \( \Sigma_1^1 \)-实数。由于每个 \( \Pi_1^1 \)-零闭集都是 \( \Pi_1^1(c) \)，每个 \( c \)-Kurtz 随机实数都是 \( \Pi_1^1 \)-Kurtz 随机的。

### 定理 14.1.6. \( c \) 的超度是 \( \Pi_1^1 \)-Kurtz 随机性的圆锥基。

证明。引理 14.1.5 意味着任何 \( y \ge_T c' \) 的图灵度包含一个成员，该成员是 \( c \)-Kurtz 随机的，因此也是 \( \Pi_1^1 \)-Kurtz 随机的。因此 \( c \) 是 \( \Pi_1^1 \)-Kurtz 随机性的一个基。

我们分析 \( c \) 的复杂度。由于每个 \( \Pi_1^1 \)-单元在 \( c \) 中是递归的，\( c \notin L_{\delta_1^1} \)。此外，集合 \( \{x \mid x \text{ 是一个 } \Pi_1^1\text{-单元}\} \) 是 \( \Delta_1^1(c) \)。换句话说，\( \{x \mid x \text{ 是一个 } \Pi_1^1\text{-单元}\} \in L_{\omega_1^{ck}}[c] \)。因此有 \( \omega_1^c > \delta_1^1 \)。应用与命题 4.4.4 中相同的论证，\( L_{\delta_1^1} \) 中的实数恰好是那些 \( \Delta_1^1 \) 的实数，因此 \( c \) 不是 \( \Delta_1^1 \)。此外，由于 \( c \) 是 \( \Sigma_2^1 \)，它在 \( L_{\delta_1^1} \) 上是 \( \Sigma_1^1 \) 可定义的，因此 \( c \in L_{\delta_1^1+1} \)。确实，所有 \( \Sigma_1^1 \)-实数都属于 \( L_{\delta_1^1+1} \)。因此，

\( c \) 在所有 \( \Sigma_2^1 \) 实数中具有最大的超度。

### 14.1.3 练习

练习 14.1.1. 证明 \( \Delta_1^1 \) 实数集和 \( \Pi_1^1 \)-Kurtz 随机实数集都不是 \( \Sigma_2^0 \)。

练习 14.1.2. 证明存在一个不是 Schnorr 随机的 \( \Pi_1^1 \)-Kurtz 随机实数。

练习 14.1.3. 证明 \( \Pi_1^1 \)-Kurtz 随机实数集不是 \( \Pi_1^1 \)。

练习 14.1.4. 证明 \( \langle L_{\delta_1^1}, \in \rangle <_{\Sigma_1} \langle L, \in \rangle \)。

## 14.2 \( \Delta_1^1 \) 和 \( \Pi_1^1 \)-Martin-Löf 随机性

#### 14.2.1 \( \Delta_1^1 \)-随机性

定义 14.2.1. 设 \( \Gamma \) 是实数集的一个可定义类。我们说 \( x \) 是 \( \Gamma \)-随机的，如果它不属于任何 \( \Gamma \)-零集。

在本节中，我们研究 \( \Delta^1_1 \)-随机性的关键性质。

命题 14.2.2. 假设 \( A \) 是一个 \( \Delta^1_1 \)-零集。存在一个 \( \Delta^1_1 \)-集 \( V \subseteq \omega \times 2^{<\omega} \)，使得 \( (\forall n)(\mu(V_n) = 2^{-n}) \) 且 \( A \subseteq \bigcap_{n<\omega} V_n \)，其中 \( V_n = \{\sigma \mid (n, \sigma) \in V\} \) 是一个 \( \Delta^1_1 \)-开集。

证明。如前所述，\( \{A_s\} \) 是由 Borel 码 \( z \) 生成的实数集的集合（§2.7.1）。由于 \( A \) 是一个 \( \Delta^1_1 \)-零集，根据引理 13.11.10，存在一个 \( \Delta^1_1 \)-函数 \( f : \omega \to \Sigma_1 \cap \text{HYP} \)，使得对于每个 \( n < \omega \),

- \( \mu(A_{f(n)}) < 2^{-n} \)，且
- \( A \subseteq A_{f(n)} \)

那么 \( A_{f(n)} = [U_n] \) 对于某个 \( \Delta^1_1 \)-集 \( U_n \subseteq 2^{<\omega} \)。现在只需证明 \( \{U_n\}_{n<\omega} \) 可以扩展为一个 \( \Delta^1_1 \)-集族 \( \{V_n\}_{n<\omega} \)，使得 \( U_n \subseteq V_n \) 且 \( \mu(V_n) = 2^{-n} \)。由于集合 \( U = \{(n, \sigma) \mid \sigma \in U_n\} \) 是 \( \Delta^1_1 \)，存在一个 \( m \in \Theta \) 使得 \( U \le_T H_m \)。注意集合 \( \{(x, e, p) \in 2^\omega \times \omega \times \mathbf{Q} \mid \mu(\{o\} \mid (\exists i)(\Phi_e^i(i) = o\})) > p\} \) 是 r.e. 的。然后，通过经典随机性理论中相对于 \( H_{2^m} \) 的标准技术，存在一个 \( V \subseteq \omega \times 2^{<\omega} \)，在 \( H_{2^m} \) 中是递归的，使得对于每个 \( n \)，\( \mu(V_n) = 2^{-n} \) 且 \( U_n \subseteq V_n \)。那么 \( A \subseteq \bigcap_{n<\omega} V_n \)。

根据命题 14.2.2，\( \Delta^1_1 \)-随机性可以被视为 Schnorr 随机性的高阶类比。

命题 14.2.3 (Martin-Löf [97])。\( \Delta^1_1 \)-随机实数集是 \( \Sigma^1_1 \) 但不是 \( \Delta^1_1 \)。

证明。定义一个 \( \Sigma^1_1 \)-集

```
\( A = \{x \mid (\forall e)(\forall n)((m \in \Theta)(\mu m[\{i(\{o\} \mid \exists i)(\Phi_e^{H_n}(\langle m, i \rangle) = o\})) \le 2^{-m}) \to (\exists m)(\forall i)(x \not\prec \Phi_e^{H_n}(\langle m, i \rangle))).\)
```

根据命题 14.2.2，\( A \) 正是 \( \Delta^1_1 \)-随机实数集。由于 \( A \) 不包含任何高算术成员，根据定理 13.13.13，它不是 \( \Delta^1_1 \)。

#### 14.2.2 \( \Pi^1_1 \)-Martin-Löf 随机性

开集序列 \( \{U_n\}_{n<\omega} \) 是一个 Martin-Löf 测试（ML 测试），如果对于所有 \( n \)，\( \mu(U_n) < 2^{-n} \)。给定实数集的一个类 \( \Gamma \)（例如，\( \Pi^1_1 \)），\( \{U_n\}_{n<\omega} \) 是一个 \( \Gamma \)-ML 测试，如果 \( \{(n, \sigma) \mid \sigma \in 2^{<\omega} \wedge [\sigma] \in U_n\} \in \Gamma \)。

定义 14.2.4. 设 \( \Gamma \) 是实数集的一个类。那么 \( x \) 是 \( \Gamma \)-ML 随机的，如果对于任何 \( \Gamma \) ML 测试 \( \{U_n\}_{n<\omega} \)，\( x \notin \bigcap_{n<\omega} U_n \)。

命题 14.2.5 (Jorhth and Nies [51])。存在一个通用的 \( \Pi^1_1 \)-ML 测试 \( \{U_n\}_{n<\omega} \)，即，对于每个 \( \Pi^1_1 \)-ML 测试 \( \{V_n\}_{n<\omega} \)，\( \bigcap_{n<\omega} V_n \subseteq \bigcap_{n<\omega} U_n \)。





证明。令 \(\hat{U} \subseteq \omega \times 2^{<\omega}\) 为一个通用的 \(\Pi^1_1\)-集，即 \(\hat{U}\) 是 \(\Pi^1_1\) 且每个 \(\Pi^1_1\)-集 \(\hat{V} \subseteq 2^{<\omega}\) 对某些 \(n\) 都是 \(\hat{U}_n = \{ \sigma \mid (n, \sigma) \in \hat{U} \}\)。那么存在一个递归函数 \(f : \omega \times 2^{<\omega} \to \omega\) 使得 \((n, \sigma) \in \hat{U} \Leftrightarrow (n, \sigma) \in \emptyset\)。

\(\hat{V} = \{ (n, \sigma) \mid (n, \sigma) \in \hat{U} \wedge \sum_{(3k \in O_{(n, \sigma)}) \cap (f(n, r) = k)} 2^{-|\Gamma|} < 2^{-n} \}.\)

换句话说，如果 \(\hat{U}_n\) 直到阶段 \(f(n, \sigma)\) 的测度小于 \(2^{-n}\)，则 \((n, \sigma)\) 被枚举进 \(\hat{V}\)。

\(U = \{ (n, \sigma) \mid (\exists m)(m \ge n + 1 \wedge (m, \sigma) \in \hat{V}) \}.\)

那么 \(U\) 也是 \(\Pi^1_1\)。令 \(U_n = \{ \sigma \mid (n, \sigma) \in U \}\)，我们有

\(\mu(U_n) < \sum_{m \ge n+1} 2^{-m} = 2^{-n}.\)

因此 \(\{ U_n \}_{n < \omega}\) 是一个 \(\Pi^1_1\)-ML 测试。由于 \(\hat{U}\) 的普遍性，\(\{ U_n \}_{n < \omega}\) 是一个通用的 \(\Pi^1_1\)-ML 测试。\(\square\)

#### **推论 14.2.6** (Hjorth and Nies [51])

- (i) 存在一个正测度的 \(\Sigma^1_1\)-闭集，由 \(\Pi^1_1\)-ML 随机实数组成。
- (ii) 对于每一个 \(z \ge_T \emptyset\)，存在一个 \(\Pi^1_1\)-ML 随机的 \(x \equiv_T z\)。

证明。(i) 直接从命题 14.2.5 得出，而 (ii) 是 (i) 和定理 11.1.2 的推论。\(\square\)

下列结果表明，每个正测度的 \(\Sigma^1_1\)-闭集本质上包含所有 \(\Pi^1_1\)-ML 随机实数。

#### **命题 14.2.7.** 假设 \(T \subseteq 2^{<\omega}\) 是一个 \(\mu([T]) > 0\) 的 \(\Sigma^1_1\)-树。那么对于任何 \(\Pi^1_1\)-ML 随机的 \(x\)，存在一个 \(z \in [T]\) 使得 \(z =^* x\)，即 \((\exists m)(\forall n \ge m)(x(n) = z(n))\)。

证明。令 \(T \subseteq 2^{<\omega}\) 如所给。对于任何 \(n \ge 0\)，令

\(U^n = \{ \sigma_0^* \sigma_1 \dots \sigma_n^* \mid (\forall i \le n)(\sigma_i \notin T) \}.\)

那么 \(\{ U^n \}_{n < \omega}\) 是一个 \(\Pi^1_1\)-ML 测试。而且，\(\mu(U^n) = \mu(2^{<\omega} \setminus [T]) = 1 - \mu([T])\)。对于任何 \(n\)，\(\mu(U^{n+1}) = \mu(U^n) \cdot (1 - \mu([T])) = (1 - \mu([T]))^{n+2}\)。令 \(V_n = \bigcup_{m \ge n} U^m\)。那么 \(\mu(V_n) \le \sum_{m \ge n} (1 - \mu([T]))^{n+1}\)，因此 \(\{ V_n \}_{n < \omega}\) 可视为一个 \(\Pi^1_1\)-ML 测试。由此可知存在一个最小的 \(n\) 使得 \(x \notin V_n\)。如果 \(n = 0\)，则 \(x \in [T]\)。否则存在一个 \(\sigma_0^* \sigma_1 \dots \sigma_{n-1} < x\) 使得 \(x = \sigma_0^* \sigma_1 \dots \sigma_{n-1} z\) 对某些 \(z \in [T]\)。故 \(x =^* z\)。\(\square\)

### 14.2.3 将 \(\Pi^1_1\)-Martin-Löf 随机性与 \(\Delta^1_1\)-随机性分离

定义强迫概念 \(\mathbf{D} = \langle \mathbf{D}, \le \rangle\) 如下：

- (i) \(P \in \mathbf{D}\) 当且仅当 \(P \subseteq 2^\omega\) 是 \(\Delta^1_1\)-闭集且具有正测度；
- (ii) 对于任何 \(P, Q \in \mathbf{D}\)，\(P \le Q\) 当且仅当 \(P \subseteq Q\)。

假设 \(U \subseteq \omega \times 2^{<\omega}\) 是 \(\Delta^1_1\) 且 \(U_n = \{ \sigma \mid (n, \sigma) \in U \}\)。假设 \(\lim_{n \to \infty} \mu(U_n) = 0\) 并令

\(\mathscr{D}_U = \{ P \mid P \in \mathbf{D} \wedge P \cap (\bigcap_{n < \omega} U_n) = \emptyset \}.\)

#### 引理 14.2.8. \(\mathscr{D}_U\) 是稠密的。

证明。令 \(P \in \mathbf{D}\)。存在一个 \(n\) 使得 \(\mu(U_n) < \mu(P)/2\)。现在补集 \(P_0 = 2^\omega \setminus U_n\) 的测度大于或等于 \(1 - \mu(P)/2\)。那么 \(P_0 \cap P\) 是一个 \(\Delta^1_1\)-闭集且测度大于或等于 \(\mu(P)/2\)。因此 \(P_0 \cap P \in \mathbf{D}\)。

对于任何 \(\Pi^1_1\)-集 \(G\)，令 \(\mathscr{D}_G = \{ P \mid P \in \mathbf{D} \wedge P \cap G = \emptyset \}\)。

#### 引理 14.2.9. 如果 \(G\) 是仅由 \(\Delta^1_1\)-随机实数组成的 \(\Pi^1_1\)-集，那么 \(\mathscr{D}_G\) 在 \(\mathbf{D}\) 中是稠密的。

证明。令 \(P \in \mathbf{D}\)。那么存在一个超算术的 \(x\) 使得 \(P\) 是 \(P_0^x(x)\)。不失一般性，我们可以假设对于任何 \(\sigma\)，如果 \([\sigma] \cap P \neq \emptyset\)，则 \(\mu([\sigma] \cap P) > 0\)（因为我们可以假设 \(P\) 仅包含 1-\(x\)-随机实数）。根据定理 13.11.13，\(P\) 中存在一个超算术的 \(z\)。故 \(z \notin G\)。由于 \(G\) 是闭集，存在一个 \(n\) 使得 \([z \nmid n] \cap G = \emptyset\)。令 \(Q = [z \nmid n] \cap P\)。那么 \(Q \in \mathscr{D}_G\)。

#### 定理 14.2.10 (Chong, Nies and Yu [12]). \(\Pi^1_1\)-ML 随机性 \(< \Delta^1_1\)-随机性。

证明。根据命题 14.2.2，\(\Pi^1_1\)-ML 随机性 \(\subseteq \Delta^1_1\)-随机性。根据命题 14.2.5，令 \(\{U_n\}_{n < \omega}\) 为一个通用的 \(\Pi^1_1\)-ML 测试。对于 \(n < \omega\)，令

\(\mathscr{D}_{U_n} = \{ P \mid P \in \mathbf{D} \wedge P \subseteq U_n \}.\)

根据引理 14.2.9，\(\mathscr{D}_{U_n}\) 是稠密的。根据引理 14.2.8，存在一个 \(\Delta^1_1\)-随机的 \(x\) 使得对于任何 \(n\)，存在一个 \(P \in \mathscr{D}_{U_n}\) 与 \(x \in P\)。故 \(x \in \bigcap_{n < \omega} U_n\)，即 \(x\) 不是 \(\Pi^1_1\)-ML 随机的。

我们指出，\(\mathbf{D}\) 是 §6.2.2 中讨论的随机强迫 \(\mathbf{R}\) 的一个类比。然而，\(\mathbf{R}\) 是 c.c.c. 因而保持所有基数，而 \(\mathbf{D}\) 在 \(L_{\omega_1^{CK}}\) 中不是 c.c.c.。根据定理 14.2.10 的证明和下面的推论 14.3.2，任何 \(\mathbf{D}\)-泛化 \(x\) 都会使 \(\omega_1^{CK}\) 坍塌，因而不保持可递序序数。

### 14.2.4 强 \(\Pi^1_1\)-Martin-Löf 随机性

一组开集 \(\{U_n\}_{n<\omega}\) 如果 \(\lim_{n\to\infty} \mu(U_n) = 0\)，则是一个 *广义 Martin-Löf 测试* (ML 测试)。给定实数集的一个类 \(\Gamma\)（例如 \(\Pi^1_1\)），\(\{U_n\}_{n<\omega}\) 是一个广义 \(\Gamma\)-ML 测试，如果 \(\{(\sigma, n) \mid \sigma \in 2^{<\omega} \wedge \sigma \in U_n\} \in \Gamma\)。

#### 定义 14.2.11. 给定实数集的一个类 \(\Gamma\)，如果对于任何广义 \(\Gamma\)-ML 测试 \(\{U_n\}_{n<\omega}\)，都有 \(x \notin \bigcap_{n<\omega} U_n\)，则称 \(x\) 是强 \(\Gamma\)-ML 随机的。

显然每个强 \(\Pi^1_1\)-ML 随机实数都是 \(\Pi^1_1\)-ML 随机的。

#### 引理 14.2.12. 如果 \(x\) 是实数 \(\Sigma^1_1\)-闭集的最左路径，则 \(x\) 不是强 \(\Pi^1_1\)-ML 随机的。

证明。令 \(P\) 为一个 \(\Sigma^1_1\)-闭集。那么存在一个 \(\Sigma^1_1\)-树 \(T \subseteq 2^{<\omega}\) 使得 \(P = [T]\)。根据 Gandy–Spector 定理 (3.71)，存在一个 \(\Sigma_0\)-公式 \(\varphi(\sigma, \beta)\) 使得 \(\sigma \in T \Leftrightarrow (L_{\omega_1^{CK}}, \in) \models (\forall \beta) \varphi(\sigma, \beta)\)。

对于 \(\beta < \omega_1^{CK}\)，令 \(T[\beta] = \{\sigma \mid (L_{\omega_1^{CK}}, \in) \models (\forall \gamma \le \beta) \varphi(\sigma, \gamma)\}\)。

对于 \(n < \omega\) 和 \(\beta < \omega_1^{CK}\)，令 \(U_{n,\beta} = \{\sigma \mid (\exists z)(z \text{ is the leftmost path in } T[\beta] \cap [\sigma] \wedge \sigma \sqsubset z \nmid n+1)\}\)。

定义 \(U_{n,<\beta} = \bigcup_{\gamma < \beta} U_{n,\gamma}\)

并 \(U_n = \bigcup_{\beta < \omega_1^{CK}} U_{n,\beta}\)。

以下事实易于验证：对于 \(n < \omega\) 和 \(\beta < \omega_1^{CK}\)，

- (1) \(U_{n+1,\beta} \subseteq U_{n,\beta}\);
- (2) \(\mu(U_{n,\beta}) < 2^{-n}\);
- (3) \(x \in \bigcap_{n<\omega} U_n\);
- (4) 对于任何 \(z\)，如果 \(z \in U_{n,<\beta} \setminus U_{n,\beta}\)，则对于任何 \(\gamma \ge \beta\) 都有 \(z \notin U_{n,\gamma}\)。

现在假设 \(\mu(\bigcap_{n<\omega} U_n) > 0\)。那么存在一个 \(\sigma_0\) 使得 \(\mu(\bigcap_{n<\omega} U_n \cap [\sigma_0]) > \frac{3}{4} \cdot 2^{-|\sigma_0|}\)。

令 \(n_0 = |\sigma_0| + 2\)。那么存在一个 \(\beta_0 < \omega_1^{CK}\) 使得 \(\mu(U_{n_0,<\beta_0} \cap [\sigma_0]) > \frac{3}{4} \cdot 2^{-|\sigma_0|}\)。





根据 (2),

\(\mu(U_{n_0, <\beta_0} \cap [\sigma_0]) > \frac{1}{2} \cdot 2^{-|\sigma_0|}.\)

根据 (1) 和 (4),

\(\mu(\bigcap_{n>n_0} U_{n, <\beta_0} \cap [\sigma_0]) > \frac{1}{4} \cdot 2^{-|\sigma_0|}.\)

因此存在一个 \(\sigma_1 > \sigma_0\) 使得

\(\mu(\bigcap_{n>n_0} U_{n, <\alpha} \cap [\sigma_1]) > \frac{3}{4} \cdot 2^{-|\sigma_1|}.\)

令 \(n_1 = |\sigma_1| + 2\)。存在一个 \(\beta_1 < \beta_0\) 使得

\(\mu(U_{n_1, <\beta_0} \cap [\sigma_1]) > \frac{3}{4} \cdot 2^{-|\sigma_1|}.\)

重复该过程，得到一个无限下降的序数序列 \(\beta_0 > \beta_1 > \cdots\)，这产生了矛盾。由此可见，\(\{U_n\}_{n<\omega}\) 是一个广义 \(\Pi^1_1\)-ML 测试，且 \(x \in \bigcap_{n<\omega} U_n\).

**定理 14.2.13** (Chong, Nies 和 Yu). _存在一个实数，它是_ \(\Pi^1_1\)_-ML随机，但不是强_ \(\Pi^1_1\)_-ML随机。_

_证明._ 根据推论 14.4.26，存在一个正测度的 \(\Sigma^1_1\)-闭集 _P_，其仅由 \(\Pi^1_1\)-ML 随机实数组成。根据引理 14.2.12，存在一个 \(x \in P\)，它不是强 \(\Pi^1_1\)-ML 随机。

#### 14.2.5 练习

- **练习 14.2.1** (Sacks [123]). _证明每个_ \(\Delta^1_1\)_-随机实数是_ \(\Sigma^1_1\)_-随机。_

- **练习 14.2.2.** _证明对于任意_ \(\Delta^1_1\)_-随机 x 和递归序数_ \(\beta\)_,_ \(f^{x(\beta)} \equiv_T x \oplus 0^{(\beta)}\)_._

- **练习 14.2.3** (Yu [171]). _证明_ \(\Delta^1_1\)_-随机实数的集合不是_ \(\Sigma^0_2\)_。_

- **练习 14.2.4.** _证明对于任意_ \(\Delta^1_1\)_-随机 x 和递归函数_ \(f: 2^\omega \to 2^\omega\)_, 如果 f 几乎处处可微，则 f 在 x 处可微。_

- **练习 14.2.5** (Bienvenu, Greenberg 和 Monin). _证明对于任何 x，它是_ \(\Sigma^1_1\)_-闭实数集的最左路径，存在一个广义_ \(\Pi^1_1\)_-Martin-Löf 测试_ \(\{U_n\}_{n<\omega}\) _，使得_ \(x \in \bigcap_{n<\omega} U_n\) _且_ \(\bigcap_{n<\omega} U_n\) _是可数的。_

- **练习 14.2.6** (Chong 和 Yu). _证明对于任意_ \(x \ge_T 0\)_, 存在一个_ \(z \equiv_T x\) _，它是_ \(\Pi^1_1\)_-Martin-Löf 随机但不是强_ \(\Pi^1_1\)_-Martin-Löf 随机。_

## 14.3 \(\Pi^1_1\)-随机性

#### 14.3.1 最大的 \(\Pi^1_1\)-零集

\(\Pi^1_1\)-随机性的概念由 Hjorth 和 Nies [51] 引入，是高阶随机性研究特有的概念。在经典随机性理论中没有此概念的类比。

**定理 14.3.1** (Kechris [64]; Stern [161]; Hjorth 和 Nies [51]). _存在一个最大的_ \(\Pi^1_1\)_-零集。_

_证明._ 定义

\(\mathcal{P} = \{(\ulcorner \varphi \urcorner, x) \mid \varphi \text{ is a ranked formula} \land \Omega(\mathfrak{A}_1^{\text{CK}}, x) \vDash \varphi(x) \land \mu(\{x \mid \Omega(\mathfrak{A}_1^{\text{CK}}, x) \vDash \neg \varphi(x)\}) \ge 1\}\)

和

\(\Omega_{\ulcorner \varphi \urcorner} = \{x \mid (\ulcorner \varphi \urcorner, x) \in \mathcal{P}\}.\)

定义

\(\Omega = \bigcup_{n < \omega} \Omega_n \cup \{x \mid \omega_1^x > \omega_1^{\text{CK}}\}.\)

我们证明 \(\Omega\) 是最大的 \(\Pi^1_1\)-零集。根据定理 13.11.1，\(\Omega\) 是 \(\Pi^1_1\)。此外，对于所有 \(n < \omega\)，\(\mu(\Omega_n) = 0\)。根据定理 13.1.4，\(\mu(\Omega) = 0\)。

如果 \(A\) 是一个 \(\Pi^1_1\)-零集，那么根据推论 3.74，存在一个算术公式 \(\varphi(x, z)\)，使得如果 \(\omega_1^x = \omega_1^{\text{CK}}\)，则 \(x \in A \Leftrightarrow \mathfrak{A}(\omega_1^x, x) \vDash (\exists y)\varphi(x, y)\)。因此，如果 \(\omega_1^x = \omega_1^{\text{CK}}\)，则对于某些 \(\beta < \omega_1^{\text{CK}}\)，\(x \in A \Leftrightarrow \mathfrak{A}(\omega_1^{\text{CK}}, x) \vDash (\exists y)\beta(\varphi, y^\beta)\)。由于 \(A\) 是零集，我们有

\(A \cap \{z \mid \omega_1^z = \omega_1^{\text{CK}}\} \subseteq \bigcup_{\beta < \omega_1^{\text{CK}}} \Omega_{\ulcorner (\exists y)\beta(\varphi, y^\beta) \urcorner}.\)

因此 \(A \subseteq \Omega\).

**推论 14.3.2.** _对于任意_ \(x \in 2^\omega\)_, 以下等价：_

- (i) \(x\) 是 \(\Pi^1_1\)-随机；
- (ii) \(x\) 是强 \(\Pi^1_1\)-ML 随机且 \(\omega_1^x = \omega_1^{\text{CK}}\)；
- (iii) \(x\) 是 \(\Pi^1_1\)-ML 随机且 \(\omega_1^x = \omega_1^{\text{CK}}\)。
- (iv) \(x\) 是 \(\Delta^1_1\)-随机且 \(\omega_1^x = \omega_1^{\text{CK}}\)。

_证明._ 假设 \(x\) 是 \(\Pi^1_1\)-随机。由于 \(\{z \mid \omega_1^z > \omega_1^{\text{CK}}\}\) 是一个 \(\Pi^1_1\)-零集，我们有 \(\omega_1^x = \omega_1^{\text{CK}}\)，因此 (i) \(\Rightarrow\) (ii) \(\Rightarrow\) (iii)。

根据定理 14.2.10，(iii) 蕴含 (iv)。我们现在证明 (iv) \(\Rightarrow\) (i)。根据定理 4.31 的证明，如果 \(\omega_1^x = \omega_1^{\text{CK}}\) 且 \(x \in \Omega\)，则对于某些 \(n\)，\(x \in \Omega_n\)。由于 \(\Omega_n\) 是一个 \(\Delta^1_1\)-零集，如果 \(\omega_1^x = \omega_1^{\text{CK}}\) 且 \(x\) 是 \(\Delta^1_1\)-随机，那么它是 \(\Pi^1_1\)-随机。

(i) 和 (iv) 之间的等价性也由 Stern [161] 得到。

#### 14.3.2 支配与 \(\Pi^1_1\)-随机性

**引理 14.3.3.** 如果 \(x\) 是 \(\Pi^1_1\)-随机，那么它是 \(\Delta^1_1\)-支配的。

证明. 根据定理 13.3.2 的证明，对于每个 \(e \in \omega\) 和 \(n \in \omega\)，集合 \(A_{e,n} = \{x \mid (\exists f \in HYP)(\Phi_e^{f(x)} \text{ is total} \rightarrow \Phi_e^{f(x)} < f)\}\) 的测度为 1。注意 \(A_{e,n} \in \Pi^1_1\)。根据推论 13.11.1，存在一个 \(\Delta^1_1\)-集 \(\hat{A}_{e,n} \subseteq A_{e,n}\)，使得 \(\mu(A_{e,n}) = 1\)。因此，如果 \(x\) 是 \(\Pi^1_1\)-随机，则 \(x \in \hat{A}_{e,n}\)。根据推论 14.3.2，\(\omega_1^{CK} = \omega_1^x\)。因此，如果 \(g \le_T x\)，则对于某些 \(e\) 和 \(n \in \omega\)，\(g = \Phi_e^{f(x)}\)，从而证明了引理。

**命题 14.3.4** (Kjos-Hanssen, Nies, Stephan 和 Yu [68]). 对于任意 \(x \in 2^\omega\)，以下等价：

- (i) \(x\) 是 \(\Pi^1_1\)-随机；
- (ii) \(x\) 是强 \(\Pi^1_1\)-ML 随机且 \(\Delta^1_1\)-支配；
- (iii) \(x\) 是 \(\Pi^1_1\)-ML 随机且 \(\Delta^1_1\)-支配；
- (iv) \(x\) 是 \(\Delta^1_1\)-随机且 \(\Delta^1_1\)-支配；
- (v) \(x\) 是 \(\Pi^1_1\)-Kurtz 随机且 \(\Delta^1_1\)-支配。
- (vi) \(x\) 是 \(\Delta^1_1\)-Kurtz 随机且 \(\Delta^1_1\)-支配。

证明. 根据推论 14.3.2 和引理 14.3.3，我们有 (i) \(\Rightarrow\) (ii) \(\Rightarrow\) (iii) \(\Rightarrow\) (iv) \(\Rightarrow\) (v) \(\Rightarrow\) (vi)。

要证明 (vi) \(\Rightarrow\) (i)，根据推论 14.3.2，只需证明 (vi) \(\Rightarrow\) (iv)。假设 \(x\) 是 \(\Delta^1_1\)-支配且 \(\Delta^1_1\)-Kurtz 随机。令 \((U_n)_{n < \omega}\) 为一个 \(\Delta^1_1\) ML 测试。那么存在一个递归函数 \(f : \omega \times 2^{<\omega} \rightarrow \omega\)，使得对于任意对 \((n, \sigma)\)，\(\sigma \in U_n\) 当且仅当 \(f(n, \sigma) \in \omega\)。由于 \(x\) 是 \(\Delta^1_1\)-支配，\(\omega_1^x = \omega_1^{CK}\)。定义一个 \(\Pi^1_1(x)\) 关系 \(R \subseteq \omega \times \omega\)，使得

\(R(n, m) \equiv (\exists \sigma)(m \equiv \sigma \wedge f(n, \sigma) \in O_m \wedge \sigma \prec x),\)

其中 \(O_m = \{i \in \omega \mid i < |m|\}\)。根据 \(\Pi^1_1\)-一致化定理 (4.2.1)，存在一个一致化 \(R\) 的部分函数 \(p\)。由于 \(x \in \cap_n U_n\)，\(p\) 是一个全函数，因此是 \(\Delta^1_1(x)\)。由于 \(\omega_1^x = \omega_1^{CK}\)，存在一个 \(m_0 \in \omega\)，使得对于每个 \(n\)，\(p(n) \in O_{m_0}\)。定义一个 \(\Delta^1_1\)-Martin-Löf 测试 \((\hat{U}_n)_{n < \omega}\)，使得 \(\sigma \in \hat{U}_n\) 当且仅当 \(f(n, \sigma) \in O_{m_0}\)。那么 \(x \in \cap_n \hat{U}_n\)。令

\(\hat{f}(n) = \min\{l \mid (\exists \sigma \in 2^{<\omega})(\sigma \in \hat{U}_n \wedge x \prec [\sigma])\}\)

为一个 \(\Delta^1_1(x)\)-函数。那么存在一个 \(\Delta^1_1\)-函数 \(f\) 支配 \(\hat{f}\)。对于 \(n < \omega\)，定义

\(V_n = \{\sigma \mid \sigma \in 2^{\le f(n)} \wedge \sigma \in \hat{U}_n\}.\)

那么 \(P = \cap_{n \in \omega} V_n\) 是一个 \(\Delta^1_1\)-闭集，且 \(x \in P\)。因此 \(x\) 不是 \(\Delta^1_1\)-Kurtz 随机，产生矛盾。





### 14.3.3 随机实数的超度

由推论 14.2.6 可知，$\Delta_1^1$-随机实数集合的超度包含以 0 为基的超度锥。这引出了一个自然问题：$\Delta_1^1$-随机实数的超度是否向上封闭。

**命题 14.3.5.** 如果 $x$ 是 $\Delta_1^1$-随机且 $\omega_1^x = \omega_1^{CK}$，则存在 $y \ge_h x$，使得没有 $z \equiv_h y$ 是 $\Delta_1^1$-随机。

**证明.** 假设 $x$ 是 $\Delta_1^1$-随机且 $\omega_1^x = \omega_1^{CK}$。令

$F(x) = \{ y \mid y \ge_T x \land (\forall f \le_T y)(\forall g \le_h x)(g < f) \}.$

则 $F(x)$ 是 $\Sigma_1^x(x)$。由于 $\emptyset^x \in F(x)$，$F(x)$ 非空。根据甘地基定理并相对化到 $x$，存在 $y \in F(x)$ 使得 $\omega_1^y = \omega_1^x = \omega_1^{CK}$。根据推论 14.3.2 和命题 14.3.4，没有 $z \equiv_h y$ 是 $\Delta_1^1$-随机。

另一方面，$\Pi_1^1$-随机实数的超度是向下封闭的。

**引理 14.3.6.** 如果 $x$ 是 $\Pi_1^1$-随机且 $y \le_h x$，则存在递归序数 $\gamma$ 使得 $y \le_T x \oplus \emptyset^{(\gamma)}$。

**证明.** 由于 $x$ 是 $\Pi_1^1$-随机，我们有 $\omega_1^x = \omega_1^{CK}$。令 $y \le_h x$。则存在公式 $\varphi(\dot{n}, \dot{x})$，其秩至多为 $\beta_0 < \omega_1^{CK}$，使得

$n \in y \Leftrightarrow \mathfrak{A}(\omega_1^{CK}, x) \vDash \varphi(\dot{n}, \dot{x})$.

根据引理 13.1.11，存在递归序数 $\beta > \beta_0$ 使得

$A_{\beta_0} = \{ \ulcorner \varphi \urcorner \mid \varphi \text{ has rank at most } \beta_0 \land \mu(\{ z \mid \mathfrak{A}(\omega_1^{CK}, z) \vDash \varphi \}) > 0 \}$

在 $\emptyset^{(\beta)}$ 中是递归的。根据引理 13.1.10，存在递归序数 $\beta_1 \ge \beta$ 使得对于任意数 $i$ 和秩为 $\beta$ 的公式 $\psi$，存在秩至多为 $\beta_1$ 的公式 $\psi'$，使得 $\{ z \mid \mathfrak{A}(\omega_1^{CK}, z) \vDash \psi' \}$ 是 $\{ z \mid \mathfrak{A}(\omega_1^{CK}, z) \vDash \psi \}$ 的一个 $\Pi_1^0(\emptyset^{(\beta)})$-子集，且度量差小于 $2^{-i}$。注意，从 $\beta_0$ 搜索 $\beta_1$ 的过程在 $L_{\omega_1^x}$ 中是有效的。这样，在 $L_{\omega_1^x}$ 中得到一个序数的 $\Delta_1$-序列 $\beta_0 < \beta_1 < \cdots$。令 $\gamma = \bigcup_{i < \omega} \beta_i$。则对于任意 $\beta < \gamma$，

- (i) $A_\beta = \{ \ulcorner \varphi \urcorner \mid \varphi \text{ has rank at most } \beta \land \mu(\{ z \mid \mathfrak{A}(\omega_1^{CK}, z) \vDash \varphi \}) > 0 \}$

在 $\emptyset^{(\beta)}$ 中是递归的，且

- (ii) 对于任意数 $i$ 和秩为 $\beta$ 的公式 $\psi$，存在秩小于 $\gamma$ 的公式 $\psi'$，使得 $\{ z \mid \mathfrak{A}(\omega_1^{CK}, z) \vDash \psi' \}$ 是 $\{ z \mid \mathfrak{A}(\omega_1^{CK}, z) \vDash \psi \}$ 的一个 $\Pi_1^0(\emptyset^{(\beta)})$-子集（对某个 $\beta' < \gamma$），且度量差小于 $2^{-i}$。

注意，对于任意带秩的公式 $\psi$，如果 $x \in P_\psi = \{ z \mid \mathfrak{A}(\omega_1^{CK}, z) \vDash \psi \}$，则 $P_\psi$ 具有正度量。

由于 \( x \) 是 \( \Delta^1_1 \)-支配的，存在一个超算术函数 \( f : \omega \to \omega \) 使得对于任意 \( e \) 和 \( n \in \omega \) 且 \( |n| < \gamma \)，如果 \( \Phi_e^{H_e} \) 计算出一棵树 \( T_{e,n} \)，且 \( x \notin [T_{e,n}] \)，则 \( f(n,e) \notin T_{e,n} \)。

现在在 \( x \oplus 0^{(\beta)} \oplus f \) 中递归地搜索一个秩小于 \( \gamma \) 的公式 \( \psi_0 \)，使得 \( S_0 = \{z \mid \mathfrak{A}(\omega_1^{CK}, z) \vDash \psi_0\} \) 包含 \( x \)，并且是 \( \{z \mid \mathfrak{A}(\omega_1^{CK}, z) \vDash \varphi(z, 0)\} \) 或 \( \{z \mid \mathfrak{A}(\omega_1^{CK}, z) \vDash \neg \varphi(z, 0)\} \) 的一个闭子集。

由于 \( x \) 是 \( \Pi^1_1 \)-随机，根据 (ii) 存在这样的 \( \psi_0 \)。注意，需要 \( x \oplus 0^{(\beta)} \oplus f \) 来判定 \( x \in S_0 \)。归纳地，对于每个 \( n \)，在 \( x \oplus 0^{(\beta)} \oplus f \) 中递归地搜索一个秩小于 \( \gamma \) 的公式 \( \psi_{n+1} \)，使得 \( S_{n+1} = \{z \mid \mathfrak{A}(\omega_1^{CK}, z) \vDash \psi_{n+1}\} \) 包含 \( x \)，具有正度量，并且是 \( S_n \cap \{z \mid \mathfrak{A}(\omega_1^{CK}, z) \vDash \varphi(z, n+1)\} \) 或 \( S_n \cap \{z \mid \mathfrak{A}(\omega_1^{CK}, z) \vDash \neg \varphi(z, n+1)\} \) 的一个闭子集。

由于 \( x \) 是 \( \Pi^1_1 \)-随机，根据 (ii)，这样的 \( \psi_{n+1} \) 存在。这意味着 \( y \not\le_T x \oplus 0^{(\beta)} \oplus f \)。

由于 \( f \) 是超算术的，存在 \( \gamma_0 < \omega_1^{CK} \) 使得 \( f \le_T 0^{(\gamma_0)} \)。不失一般性，假设 \( \gamma_0 \le \gamma$（必要时将 \( \gamma \) 替换为 \( \gamma_0 + \gamma \)）。则 \( y \not\le_T x \oplus 0^{(\gamma)} \)。\(\square\)

### **推论 14.3.7.** 如果 \( x \) 是 \( \Pi^1_1 \)-随机且 \( y \le_h x \)，则存在递归序数 \( \beta \)、函数 \( f \le_T 0^{(\beta)} \) 和递归泛函 \( \Psi \)，使得对每个 \( n \)，\( y(n) = \Psi^{x \oplus 0^{(\beta)}(n)}(n)[f(n)] \)。

**证明.** 假设 \( x \) 是 \( \Pi^1_1 \)-随机且 \( y \le_h x \)。根据引理 14.3.6，存在递归序数 \( \gamma \) 和递归函数 \( \Phi \)，使得对每个 \( n \)，\( y(n) = \Phi^{x \oplus 0^{(\gamma)}(n)}(n)[g(n)] \)。由于 \( x \) 是 \( \Pi^1_1 \)-支配的，存在函数 \( g \le_h x \) 使得对每个 \( n \)，\( y(n) = \Phi^{x \oplus 0^{(\gamma)}(n)}(n)[g(n)] \)。由于 \( x \) 是 \( \Pi^1_1 \)-支配的，存在超算术函数 \( h \) 使得对所有 \( n \)，\( h(n) > g(n) \)。

因此存在足够大的递归序数 \( \beta \)，使得 \( x \) 和 \( h \) 都多一归约到 \( 0^{(\beta)} \)。定义函数 \( f \le_T 0^{(\beta)} \) 和递归函数 \( \Psi \) 并不困难，使得对每个 \( n \)，\( y(n) = \Psi^{x \oplus 0^{(\beta)}(n)}(n)[f(n)] \)。\(\square\)

### **定理 14.3.8.** 如果 \( x \) 是 \( \Pi^1_1 \)-随机且 \( y \le_h x \) 不是超算术的，则存在 \( \Pi^1_1 \)-随机 \( z \equiv_h y \)。

**证明.** 假设 \( x \) 是 \( \Pi^1_1 \)-随机且 \( y \le_h x \) 不是超算术的。根据推论 14.3.7，存在递归序数 \( \beta \)、非递减函数 \( f \le_T 0^{(\beta)} \) 和递归函数 \( \Psi \)，使得 \( \lim_{n \to \infty} f(n) = \infty \) 且对每个 \( n \)，

\( y(n) = \Psi^{x \oplus 0^{(\beta)}(n)}(n)[f(n)] \).

对于每个 \( u \in 2^{<\omega} \)，令

\( l(u) = \sum_{\tau \in 2^{|\tau|} \cap \text{Cl}} \left( \sum_{g \in 2^{|\tau|} \wedge \forall \rho \prec u \exists \rho' \in [u] [f(|\rho|)] \|\tau\| = \tau} 2^{-|\sigma|} \right) \)

和

\( r(u) = l(u) + \sum_{\sigma \in 2^{|\tau|} \wedge \forall \rho \prec u \exists \rho' \in [u] [f(|\rho|)] \|\tau\| = u} 2^{-|\sigma|} \),

其中 \( \tau < u \) 表示，作为字符串，\( \tau \) 在 \( u \) 的左侧。

可以将 \(\sum_{\sigma \in 2^{<\omega}} \lambda \mu[\text{ext}(\sigma) \oplus \emptyset^{(\beta)}[f(|\sigma|)]]_{r(\sigma)} 2^{-|\sigma|}\) 视为 \( \tau \) 的一个“度量”。对于每个 \( n \)，令

\( l_n = l(y \upharpoonright n) \)，且 \( r_n = r(y \upharpoonright n) \)。

则 \( l_n \le l_{n+1} \le r_{n+1} \le r_n$。由于 \( y \) 不是超算术的，不难看出 \(\lim_{n \to \infty} r_n = 0\)。因此存在唯一的

\( z = \bigcap_{n<\omega} (l_n, r_n) \)。

显然 \( z \le_T y \oplus \emptyset^{(\beta)} \)。我们留给读者验证 \( y \le_T z \oplus \emptyset^{(\beta)} \)。因此 \( z \equiv_T y \)。

假设 \( z \) 不是 \( \Delta^1_1 \)-随机。则存在递归序数 \( \gamma < \beta \) 和一个 \( \emptyset^{(\gamma)} \)-ML-测试 \( \{V_n\}_{n \in \omega} \) 使得 \( z \in \bigcap_{n<\omega} V_n \)。令

\( \tilde{V}_n = \{u \mid (\exists v)(v \text{ is the } k\text{-th string in } V_n \wedge (\exists p \in \mathbb{Q})(\exists q \in \mathbb{Q})(p < l(u) < r(u) < q \land \forall \sigma \sqsubseteq u (q - p < 2^{-|v|} - 2^{-n-k-2}))\} \).

直观地，\( \{\tilde{V}_n\}_{n<\omega} \) 是相对于度量 \( \lambda \) 的 \( \Delta^1_1 \)-Martin-Löf 测试，其中对任意 \( \sigma \in 2^{<\omega} \)，\( \lambda(\sigma) = \sum_{\tau \in C(\sigma)} 2^{-|\tau|} \)。

由于 \( z \in V_n \)，对每个 \( n \) 都有 \( y \in \tilde{V}_n \)。注意 \( \{\tilde{V}_n\}_{n<\omega} \) 是 \( \emptyset^{(\gamma+1+\beta)} \)-递归可枚举。令

\( U_n = \{\sigma \mid (\exists \tau \in \tilde{V}_n)(|\sigma| = f(|\tau|) \land \tau \oplus \emptyset^{(\gamma)}[f(|\tau|)][f(|\tau|)] \ge \tau)\} = \bigcup_{u \in \tilde{V}_n} C(u) \).

则 \( \{U_n\}_{n<\omega} \) 是 \( \emptyset^{(\gamma+1+\beta)} \)-递归可枚举 且 \( x \in \bigcap_{n<\omega} U_n \)。注意对每个 \( n \)，

\( \mu(U_n) \le \mu(V_n) + \sum_{k<\omega} 2^{-n-k-2+1} < 2^{-n} + 2^{-n} = 2^{-n+1} \).

则 \( \{U_{n+1}\}_{n<\omega} \) 是一个 \( \emptyset^{(\gamma+1+\beta)} \)-ML-测试。因此 \( x \) 不是 \( \Delta^1_1 \)-随机，矛盾。

### 14.3.4 练习

**练习 14.3.1** (Jorhth and Nies [51]). 证明 \( x \oplus y \) 是 \( \Pi^1_1 \)-随机当且仅当 \( x \) 是 \( \Pi^1_1 \)-随机且 \( y \) 是 \( \Pi^1_1(x) \)-随机。

**练习 14.3.2** (Yu [171]). 对任意 \( z \ge_h \emptyset \)，存在 \( \Delta^1_1 \)-随机 \( x \equiv_h z \)，且 \( x \) 不是 \( \Pi^1_1 \)-ML 随机。

**练习 14.3.3.** 证明如果 \( x \) 是 \( \Pi^1_1 \)-随机，则对于任何包含 \( x \) 的 \( \Sigma^1_1 \)-实数集 \( A \)，

\( \lim_{n \to \infty} \frac{\mu(A \cap [x \upharpoonright n])}{2^{-n}} = 1 \).





Exercise 14.3.4. Prove that there is a \(\Sigma^1_1\)-set \(A\) and a \(\Pi^1_1\)-ML random \(x \in A\) such that \(\lim_{n \to \infty} \frac{\mu(A[n|x])}{2^{-n}} = 0\).

Exercise 14.3.5. Prove that every \(x \notin\) HYP hyperarithmetically reducible to a \(\Pi^1_1\)-random real is \(\Pi^1_1\)-random relative to a continuous measure.

Exercise 14.3.6 (Kjos-Hanssen and Yu). Let \(\Phi\) be a universal partial \(\Pi^1_1\)-function from \(\omega\) to 2, and assume that \(x(n) \neq \Phi(n, e)\) for each \(e\). Show that \(x\) hyperarithmetically computes some member of a given nonempty \(\Sigma^1_1\)-closed subset of \(2^\omega\).

Exercise 14.3.7 (Greenberg, Montalbán and Slaman [39]; Kulikumin and Nies). Suppose that \(\mathbb{M}\) is a structure such that the set \(A = \{x \mid (\exists N \le_T x)(N \equiv \mathbb{M})\}\) has measure 1. Prove that every \(\Pi^1_1\)-random real is in \(A\).

Exercise 14.3.8 (Kripke [120]). If \(A\) is a nullset of hyperdegrees such that \(\mathbf{0} \notin A\), then the set \(U_K(A) = \{x \mid (\exists y \in A)(x \ge_T y)\}\) is also null.

## 14.4 \(\Delta^1_2\) and \(\Sigma^1_2\)-randomness

#### 14.4.1 \(\Delta^1_2\)-randomness

Since there is a \(\Delta^1_1\)-real which is \(\Pi^1_1\)-random, \(\Delta^1_2\)-randomness is strictly stronger than \(\Pi^1_1\)-randomness. By Corollary 13.1.7 and Proposition 13.1.12, we have the following conclusion.

**Proposition 14.4.1.** Assume that \(\omega_1^L < \omega_1\). Then \(\Delta^1_2\)-randomness = \(\Delta^1_2\)-ML randomness = \(\Pi^1_2\)-randomness.

#### 14.4.2 \(\Sigma^1_2\)-ML randomness

Let \(\{\varphi_n(\sigma)\}_{n < \omega}\) be a recursive enumeration of \(\Sigma^1_1\)-formulas. There is a \(\Sigma_1\)-formula \(\psi(n, \sigma)\) (in set theory) such that

\(\varphi_n(\sigma) \leftrightarrow (\exists X)(x \text{ is a } \Pi^1_1\text{-singleton} \land \langle L_{\omega_1^X}, \in \rangle \models \psi(n, \sigma)).\)

Let \((n, \sigma) \in U\) if and only if

\((\exists x)(x \text{ is a } \Pi^1_1\text{-singleton} \land \langle L_{\omega_1^x}, \in \rangle \models \psi(n, \sigma)) \land \mu(\{z \mid (\exists m)(\langle L_{\omega_1^z}, \in \rangle \models \psi(n, z \mid m))\}) < 2^{-n}.\)

One may view \((n, \sigma) \in U\) as an enumeration of strings \(\sigma\) in \(U\) up to any stage coded by a \(\Pi^1_1\)-singleton where the measure is less than \(2^{-n}\). We leave it to the reader to verify that \(U\) is \(\Sigma^1_2\). Then the set \(\{U_n\}_{n < \omega}\), where \(U_n = \{\sigma \mid (n, \sigma) \in U\}\), is a universal \(\Sigma^1_2\)-ML test.

Hence there is a \(\Pi^1_2\)-closed set P which contains only \(\Sigma^1_2\)-ML random reals. It follows that the leftmost path in P is \(\Delta^1_2\)-equivalent to a \(\Sigma^1_2\)-real and so belongs to L.

By Proposition 4.4.6, every \(x \in P \cap L\) satisfies \(\delta_2^{1+} > \delta_2^{1\uparrow}\). This applies in particular to the leftmost path x in P. Hence if one stays within L, the situation that one normally sees in standard randomness theory no longer applies. Note that by applying a method similar to that in the proof of Theorem 14.2.10, one may separate \(\Sigma^1_2\)-ML randomness from \(\Delta^1_2\)-randomness.

**Proposition 14.4.2.** If \(V = L\), then every nonzero \(\Delta^1_2\)-degree contains a \(\Sigma^1_2\)-ML random real.

**Proof.** First observe that the set P above can be presented by a \(\Pi^1_2\)-tree T. By Proposition 4.4.6, T is \(\Delta^1_2\) in every \(x \in [T]\) and T has the least nontrivial \(\Delta^1_2\)-degree. Hence the proposition follows.

#### 14.4.3 \(\Sigma^1_2\)-randomness

**Definition 14.4.3.** We say that x is L-random if for any Martin-Löf test \(\{U_n\}_{n<\omega}\) in L, \(x \notin \bigcap_{n<\omega} U_n\).

L-randomness was essentially introduced by Solovay [150]. The following fact is immediate.

**Proposition 14.4.4.** The following are equivalent:

- (i) x is L-random;
- (ii) x does not belong to any Borel nullset coded in L;
- (iii) x is \(\mathbb{R} = (\mathbf{T}, \le)\)-generic over L, where R is the notion of random forcing as defined in § 6.2.2.

**Proof.** Obviously (iii) => (ii) => (i). By Proposition 6.2.6, R is c.c.c. Then it follows that for any dense subset \(\mathscr{D}\), \(\bigcup_{p \in \mathscr{D}} p\) is a Borel co-nullset with a Borel code in L. Hence (ii) => (iii).

**Theorem 14.4.5** (Solovay [150]). If the set of L-random reals has measure 1, then every \(\Sigma^1_2\)-set is measurable.

**Proof.** Suppose that A is a \(\Sigma^1_2\)-set of reals defined by a formula \(\varphi(x)\) in the language of set theory so that
\(x \in A \Leftrightarrow (L[x], \in) \models \varphi(x)\).

Let \(\mathscr{D}\) be a maximal antichain in L so that for any \(p \in \mathscr{D}\), \(p \Vdash \dot{\varphi}(\dot{G})\). Then \(\mathscr{D}\) is countable. Let \(R = \bigcup_{p \in \mathscr{D}} p\). Then R is a Borel set with a Borel code in L. If x is L-random, then x is an R-generic real over L. Hence if x is L-random in R, then \((L[x], \in) \models \varphi(x)\) and so x belongs to A. Note that \(\mathscr{D}' = \{r \mid (\exists p \in \mathscr{D})(r \le p) \lor (\forall q)(q \in \mathscr{D} \land q \le p \rightarrow q \not\parallel r)\}\) is a dense set. Thus if \(x \in A\), then \(x \in R\) so that for any L-random real x, \(x \in A\) if and only if \( x \in R \). Since the set of \( L \)-random reals has measure 1, \( A \) is equal to \( R \) modulo a nullset. It follows that \( A \) is measurable.

**Theorem 14.4.6** (Stern [161]). For any real \( x \), \( x \) is \( \Delta^1_2 \)-random and \( \delta_2^{1,x} = \delta_2^1 \) if and only if \( x \) is \( L \)-random.

**Proof.** Let \( x \) be \( \Delta^1_2 \)-random such that \( \delta_2^{1,x} = \delta_2^1 \). If \( x \) is not \( L \)-random, then let

\( A = \{r \mid r \text{ codes a well-ordering } \wedge x \text{ is not } L_{|r|}\text{-random}\} \)

be a nonempty \( \Delta^1_2(x) \)-set. Then there is an \( r \le_{\Delta_1^1} x \) so that \( x \in L_{\delta_1} \), a contradiction.

Conversely, let \( x \) be \( L \)-random. Then \( x \) is \( \Delta^1_2 \)-random. Suppose that \( \delta_2^{1,x} > \delta_2^1 \). Then there are \( \Sigma^1_2 \)-formulas \( \varphi(x, m, n) \) and \( \psi(x, m, n) \) defining an \( r \in L \) coding a well-ordering greater than \( \delta_2^1 \). By Corollary 4.2.29, \( r \in L_{\delta_2^1}[x] \). By (iii) in Proposition 14.4.4, there is a condition \( p \in \mathbf{T} \cap L \) such that

\( p \Vdash (\forall m)(\forall n)((m, n) \in \dot{r} \leftrightarrow \varphi(x, m, n)) \wedge ((m, n) \in \dot{r} \leftrightarrow \psi(x, m, n)). \)

Then for any \( L \)-random real \( z \in p \), \( r \le_{\Delta_1^1} z \). Applying Levy collapse \( \mathbb{L}(\aleph_2)^L \) over \( V \), in \( V[G] \) the set of \( L \)-random reals is of measure 1. It follows that in \( V[G] \), the set

\( A_r = \{z \mid r \le_{\Delta_1^1} z\} \)

has positive measure. By Theorem 14.4.5 and Proposition 13.19, \( r \) is \( \Delta^1_2 \) in \( V[G] \) and so in \( V \), a contradiction.

Note that the set of \( L \)-random reals is \( \Pi^1_2 \). Thus if the measure of non-\( L \)-random reals is 0, then every \( \Sigma^1_2 \)-random real is \( L \)-random.

**Theorem 14.4.7** (Stern [161]). Assume that the set of \( L \)-random reals has measure 1. Then the set of non-\( L \)-random reals is the largest null \( \Sigma^1_2 \)-set and so \( \Sigma^1_2 \)-randomness is equivalent to \( L \)-randomness.

**Proof.** For a contradiction, suppose that \( A \) is a null \( \Sigma^1_2 \)-set containing an \( L \)-random real \( x \). Then there is a formula \( \varphi \) defining \( A \) such that \( L[x] \models \varphi(x) \). By Proposition 14.4.4, there is a condition \( p \in \mathbf{T} \cap L \) such that \( p \Vdash \varphi(\dot{x}) \). Hence for any random real \( y \in p \), we have \( (L[y], \in) \models \varphi(y) \). Thus \( \varphi(y) \) holds for any \( y \in p \). Since the set of \( L \)-random reals has measure 1, it follows that \( \mu(A) > 0 \), a contradiction.

Hence if \( (\omega_1)^L < \omega_1 \), then \( \Sigma^1_2 \)-randomness is strictly stronger than \( \Sigma^1_2 \)-ML randomness. Indeed, the conclusion is provable in ZFC.

**Proposition 14.4.8.** There is a \( \Sigma^1_2 \)-ML random real which is not \( \Sigma^1_2 \)-random.

**Proof.** Let \( T \subseteq 2^{<\omega} \) be a \( \Pi^1_2 \)-tree containing only \( \Sigma^1_2 \)-ML random reals. Then by a method similar to that used in the proof of Lemma 14.2.12, replacing \( \omega_1^{CK} \) with \( \delta_2^1 \), one is able to show that the leftmost path of \( T \) is covered by a \( \Sigma^1_2 \)-nullset. We leave it to the reader to fill in the details.





也可以通过考虑避免所有广义 \(\Sigma^1_1\)-ML 测试的实数来引入强 \(\Sigma^1_1\)-ML 随机性的概念。命题 14.4.8 表明，强 \(\Sigma^1_1\)-ML 随机性不同于 \(\Sigma^1_1\)-ML 随机性。注意，每个广义 \(\Sigma^1_1\)-ML 测试 \(\{U_n\}_{n \in \omega}\) 都是 \(L\) 的一个元素，并且根据推论 13.17，\((L, \epsilon) \vDash \mu(\cap_{n \in \omega} U_n) = 0\)。因此，存在 \(L\) 中的一个实数，它是强 \(\Sigma^1_1\)-ML 随机的。由此可见，如果可构实数的集合是零集，那么强 \(\Sigma^1_1\)-ML 随机性严格弱于 \(\Sigma^1_1\)-随机性。

#### 14.4.4 练习

- **练习 14.4.1.** 将 \(\Sigma^1_1\)-ML 随机性与 \(\Delta^1_1\)-随机性分开。
- **练习 14.4.2.** 每个 \(\Sigma^1_1\) 集是可测的，当且仅当几乎每个实数都是 \(L\)-随机的。
- **练习 14.4.3.** 假设 \(V = L\)。证明不存在最大的 \(\Sigma^1_1\)-零集。
- **练习 14.4.4.** 完成命题 14.4.8 的证明。
- **练习 14.4.5** (Stern [161])。证明与 ZFC 相容的是 \((\omega_1)^L = \omega_1\)，且几乎每个实数都是 \(L\)-随机的。
- **练习 14.4.6.** 假设 \(V = L\)。证明每个非平凡的 \(\Delta^1_2\)-度包含一个强 \(\Sigma^1_1\)-ML 随机实数。
- **练习 14.4.7.** 设 \(r\) 是在 \(L\) 上随机的。证明在 \(L[r]\) 中，没有实数是在 \(L\) 上科恩泛化的。
- **练习 14.4.8.** 设 \(g\) 是在 \(L\) 上科恩泛化的。证明在 \(L[g]\) 中，可构实数的集合是零集，但没有实数是 \(L\)-随机的。

## 14.5 Kolmogorov 复杂性与随机性

#### 14.5.1 \(\Delta^1_1\)-随机实数的 Kolmogorov 复杂性

**命题 14.5.1.** 以下等价：

- (i) \(x\) 是 \(\Delta^1_1\)-随机的。
- (ii) 对于任何马丁-勒夫随机的 \(z \in \text{HYP}\)，
  \((\exists c)(\forall n)(K(x \mid n) \ge 2n - C(z \mid n) - c).\)
- (iii) 对于任何马丁-勒夫随机的 \(z \in \text{HYP}\)，
  \((\exists c)(\forall n)(C(x \mid n) \ge 2n - K(z \mid n) - c).\)

**证明。** (i) \(\Rightarrow\) (ii)。根据命题 14.2.2，\(x\) 是 \(\Delta^1_1\)-随机的，当且仅当对于任何超算术的 \(z\)，\(x\) 相对于 \(z\) 是马丁-勒夫随机的。根据定理 12.1.10，这等价于断言：对于任何超算术马丁-勒夫随机的 z，x 相对于 z 是马丁-勒夫随机的。根据 van Lambalgen 定理 12.17，这进一步等价于：对于每个超算术马丁-勒夫随机的 z，x \(\oplus\) z 是马丁-勒夫随机的，而根据定理 12.2.11，这等价于“对于任何超算术马丁-勒夫随机的 z，\((\exists c)(\forall n)(K(x \upharpoonright n) \ge 2n - C(z \upharpoonright n) - c)\)”。

类似地可证 (i) <=> (iii)。

**推论 14.5.2.**

\(\Delta^1_1\)-随机性对 K- 和 C- 度都向上封闭。

#### 14.5.2 \(\Pi^1_1\)-随机实数的 Kolmogorov 复杂性

**命题 14.5.3.**

对于任何 \(\Pi^1_1\)-随机的 x，如果 x \(\le_K\) y 或 x \(\le_C\) y，则 y 是 \(\Pi^1_1\)-随机的。

**证明.**

假设 x 是 \(\Pi^1_1\)-随机的，且 x \(\le_K\) y（或 x \(\le_C\) y）。根据推论 14.5.2，y 是 \(\Delta^1_1\)-随机的。注意，集合 {z | x \(\le_K\) z}（或 {z | x \(\le_C\) z}）是 \(\Delta^1_1(x)\)。根据定理 12.2.14 和相对于 x 的引理 2.5.4，y \(\le_h\) x，因此 \(\omega_1^x = \omega_1^{CK}\)。然后根据推论 14.3.2，y 是 \(\Pi^1_1\)-随机的。

同样可以证明，\(\Delta^1_1\)-随机性对 K- 和 C- 都向上封闭。根据定理 14.4.7，如果 \((\omega_1^x)^L < \omega_1\)，那么 \(\Sigma^1_1\)-随机性对 \(\le_K\) 和 \(\le_C\) 都向上封闭。目前尚不知 \(\Pi^1_1\)-ML 随机性是否对这两种可归约性中的任何一种向上封闭。

#### 14.5.3 练习

**练习 14.5.1.**

证明不存在函数 f，使得 x 是 \(\Delta^1_1\)-随机的，当且仅当 \((\exists c)(\forall n)(K(x \upharpoonright n) \ge n + f(n) - c)\)。

## 14.6 随机性的下垂性

高阶随机性的下垂性概念通常与自然数上的随机性的下垂性概念相平行。在本节中，我们省略了关于下垂性性质的证明，这些证明只是对后者的小幅修改。详情请参阅相关书籍或论文。

#### 14.6.1 高阶 Kurtz 随机性的下垂性

**引理 14.6.1.**

如果 x 是 \(\Delta^1_1\)-支配的且 \(\Delta^1_1\)-半可迹的，那么 x 对 \(\Delta^1_1\)-Kurtz 测试是下垂的。

证明。假设 \(x\) 是 \(\Delta^1_1\)-支配的且 \(\Delta^1_1\)-半可迹的。设 \(U\) 是一个测度为 1 的 \(\Delta^1_1(x)\) 开集。那么存在 \(y \le_h x\) 使得 \(U\) 是 \(\Delta^1_1(y)\)。设 \(\Phi\) 为一个图灵归约，使得 \(\Phi^y\) 的定义域为 \(U\)。对任意 \(z\)，记 \(U'\) 为 \(\Phi^x\) 的定义域。注意 \(U = U'\)。

定义一个 \(\Delta^1_1(x)\) 函数 \(\hat{f}\) 如下：\(\hat{f}(n)\) 是满足 \(\mu(U'[\sigma]) > 1 - 2^{-n}\) 的最短字符串 \(\sigma \prec y\)。根据定理的假设，存在一个递增的 \(\Delta^1_1\)-函数 \(g\) 和一个 \(\Delta^1_1\)-函数 \(f\)，使得对于每个 \(n\)，存在 \(m \in [g(n), g(n+1)]\) 且 \(f(m) = f(m)\)。不失一般性，我们可以假设对于每个 \(m\)，\(\mu(U'[f(m)]) > 1 - 2^{-m}\)。

定义一个 \(\Delta^1_1\)-开集 \(V\)，使得 \(\sigma \in V\) 当且仅当存在 \(n\) 使得 \([\sigma] \subseteq \bigcap_{g(n) \le m \le g(n+1)} U'[f(m)]\)。根据 \(f\) 和 \(g\) 的性质，\(V \subseteq U' = U\)。但是对于每个 \(n\)，

\(\mu\left(\bigcap_{g(n) \le m \le g(n+1)} U'[f(m)]\right) > 1 - \sum_{g(n) \le m \le g(n+1)} 2^{-m} \ge 1 - 2^{-g(n)+1}.\)

因此，

\(\mu(V) \ge \lim_n \mu\left(\bigcap_{g(n) \le m \le g(n+1)} U'[f(m)]\right) = 1.\)

这意味着 \(x\) 对 \(\Delta^1_1\)-Kurtz 测试是下垂的。

**引理 14.6.2.** 如果 \(x\) 对 \(\Delta^1_1\)-Kurtz 随机性是下垂的，那么 \(x\) 是 \(\Delta^1_1\)-支配的。

证明。我们首先证明，如果 \(x\) 对 \(\Delta^1_1\)-Kurtz 测试是下垂的，那么 \(x\) 是 \(\Delta^1_1\)-支配的。

假设 \(f \le_h x\) 是一个递增函数。设 \(S_f = \{z \mid (\forall n)(z(f(n)) = 0)\}\)。显然 \(S_f\) 是一个 \(\Delta^1_1(x)\)-闭零集。因此存在一个 \(\Delta^1_1\)-闭零集 \([T] \supseteq S_f\)，其中 \(T \subseteq 2^{<\omega}\) 是一个 \(\Delta^1_1\)-树。定义

\(g(n) = \min\{m \mid |\{\sigma \in 2^m \mid [\sigma] \subseteq T\}| < 2^{-n}\} + 1.\)

由于 \(\mu([T]) = 0\)，\(g\) 是 \(\Delta^1_1\)。我们声称 \(g\) 支配 \(f\)。

对于每个 \(n\)，\(S_{f(n)} = \{\sigma \in 2^{f(n)} \mid (\forall i < n)(\sigma(f(i)) = 0)\}\) 的基数为 \(2^{f(n)-n}\)。但是，如果 \(g(n) \le f(n)\)，则应用 \(S \subseteq [T]\) 得到

\(|S_{f(n)}| \le 2^{f(n)-g(n)} \cdot |\{\sigma \in 2^{g(n)} \mid \sigma \in T\}| < 2^{f(n)-g(n)} \cdot 2^{g(n)-n} = 2^{f(n)-n}.\)

这是一个矛盾。因此 \(x\) 是 \(\Delta^1_1\)-支配的。

现在假设 \(x\) 不是 \(\Delta^1_1\)-支配的，由某个 \(f \le_h x\) 见证。那么 \(S_f\) 不包含在任何 \(\Delta^1_1\)-闭零集中。实际上，不难看出，对于任何使得 \([\sigma] \cap S_f \neq \emptyset\) 的 \(\sigma\) 神谕，\([\sigma] \cap S_f\) 都不包含在任何 \(\Delta^1_1\)-闭零集中（否则，如上文所示，可以证明 \(f\) 被一个 \(\Delta^1_1\)-函数支配）。然后通过归纳，构造一个 \(\Delta^1_1\)-Kurtz 随机的 \(z \in S_f\) 如下：

设 \(P_0, P_1, \dots\) 为 \(\Delta^1_1\)-闭零集的一个枚举。首先选择最小的 \(\tau\)，使得 \([\tau] \cap S_f \neq \emptyset\) 但 \([\tau] \cap S_f \cap P_0 = \emptyset\)。设 \(l_0 = |\tau|\) 和 \(Z_0 = \tau\)。假设在第 \(n+1\) 阶段，\(Z_n \in l_n\) 已被定义，使得 \([Z_n \cap l_n] \cap S_f \neq \emptyset\)。那么存在一个 \(\tau > Z_n \cap l_n\)，使得 \([\tau] \cap S_f \neq \emptyset\) 但 \([\tau] \cap S_f \cap P_n = \emptyset\)。选择这样的最小 \(\tau\)，并设 \(l_{n+1} = |\tau|\) 和 \(z \cap l_{n+1} = \tau\)。那么 \(z \in S_f\) 是 \(\Delta^1_1\)-Kurtz 随机的。因此 \(x\) 对 \(\Delta^1_1\)-Kurtz 随机性不是下垂的。





以下引理的证明留给读者。

#### 引理 14.6.3 (库切拉 [76]). 假设 $T \subseteq 2^{<\omega}$ 和 $P \subseteq \omega \times 2^{<\omega}$ 是 $\Sigma^1_1$-树，且 $\mu([T]) > 0$。则存在一个 $\Sigma^1_1$-树 $S \subseteq T$ 和一个常数 $c$，使得对于任意 $e$，若 $[P_e] \subseteq S$ 非空，则 $\mu([P_e]) > 2^{-c}$，其中 $P_e = \{ \sigma \mid (\sigma, e) \in P \}$。

以下引理基本上归功于约瑟夫·米勒。

#### 引理 14.6.4. 对于任意非-$\Delta^1_1$-半可回溯的实数 $x$ 和 $\Sigma^1_1$-树 $T \subseteq 2^{<\omega}$（满足 $\mu([T]) > 0$），存在 $z \in [T]$ 和 $y \le_h x$，使得 $y \notin z$ 且 $|\{n \mid y(n) = 1\}| = \aleph_0$。

证明。设 $x$ 为非-$\Delta^1_1$-半可回溯的实数，并设 $T \subseteq 2^{<\omega}$ 为满足 $\mu([T]) > 2^{-k}$ 的 $\Sigma^1_1$-树，其中 $k > 0$。由引理 13.3.10，存在函数 $f \le_h x$，使得对于任意偏 $\Pi^1_1$-函数 $p : \omega \times 2^{<\omega} \to \omega$，满足 $f(n, \sigma) = p(n, \sigma)$ 的 $(n, \sigma)$ 最多只有有限个。

设 $P \subseteq \omega \times 2^{<\omega}$ 为通用 $\Sigma^1_1$-树，即 $P$ 是 $\Sigma^1_1$-树，且对于任意 $\Sigma^1_1$-树 $Q \subseteq 2^{<\omega}$，存在 $e$ 使得 $P_e = Q$。我们可以假设存在递归函数 $h$，使得对任意 $(e_0, e_1)$，有 $P_{h(e_0, e_1)} = P_{e_0} \cap P_{e_1}$。

设 $S \subseteq T$ 如引理 14.6.3 所述。令 $S = P_{e_0}$，其中 $e_0$ 为某个索引。我们还可以假设存在递归函数 $g : 2^{<\omega} \to \omega$，使得 $P_{g(\sigma)} = \{ \tau \mid \tau \in P_{e_0} \land \forall n (\sigma(n) = 1 \to \tau(n) = 1) \}$。对于 $\sigma \in 2^{<\omega}$，令

$$
A_\sigma = \{ n \mid [S] \cap \{ y \in 2^\omega \mid y(n) = 1 \land (\forall m)(\sigma(m) = 1 \to y(m) = 1) \} = \emptyset \}.
$$

则集合 $\{ (\sigma, A_\sigma) \mid \sigma \in 2^{<\omega} \}$ 是一个 $\Pi^1_1$-集合。而且，若 $[P_{g(\sigma)}] \neq \emptyset$，则

$$
2^{-h(\sigma, c)} - c \le \mu([P_{g(\sigma)}]) \le \mu(\{ y \mid A_\sigma \cap \gamma \neq \emptyset \}) = 2^{-|A_\sigma|}.
$$

故 $|A_\sigma| \le h(\sigma, c) + c$。由此可知存在偏 $\Pi^1_1$-函数 $p : \omega \times 2^{<\omega} \to \omega$，使得对任意 $n$，若 $p(n, \sigma) = k$，则

- $k \in A_\sigma$，且
- $(\forall m < n)(\exists k')(k' \neq k \land p(m, \sigma) = k')$。

因此 $\{ p(n, \sigma) \}_{n \le h(\sigma, c) + c}$ 是 $A_\sigma$ 的一一枚举。注意

$$
|\{ n \mid p(n, \sigma) \text{ is defined} \}| \le h(\sigma, c) + c.
$$

以 $x$ 为超算术参数，按如下方式计算一个 $k$，使得 $k \notin A_\sigma$ 且 $k > |\sigma|$。固定一个递归双射 $q : \omega \to \omega^{<\omega}$。我们可以假设对所有 $n$ 和 $\sigma$，$f(n, \sigma) \neq q(p(n, \sigma))(n)$。以 $x$ 为超算术参数定义 $g_1 : 2^{<\omega} \to \omega^{<\omega}$，使得 $g_1(\sigma)$ 是 $\omega^{h(\sigma, c) + c}$ 中的有限字符串，且

$$
(\forall n \le 2^{h(\sigma, c) + c})(g_1(\sigma)(n) = f(n, \sigma)).
$$

故若 $[P_{g(\sigma)}] \neq \emptyset$，则对所有 $n \le h(\sigma, c)$，有 $g_1(\sigma) \neq q(p(n, \sigma))$。对于这样的 $\sigma$，对所有 $n$ 都有 $q^{-1}(g_1(\sigma)) \neq p(n, \sigma)$。因此 $q^{-1}(g_1(\sigma)) \notin A_\sigma$，故 $P_{g(q^{-1}(g_1(\sigma)))} \neq \emptyset$。不失一般性，我们可以假设 $q^{-1}(g_1(\sigma)) > |\sigma|$。

利用 $q^{-1} \circ g_1$，从 $\sigma_0 = \emptyset$ 开始，以 $x$ 为超算术参数构造字符串序列 $\sigma_0 < \sigma_1 < \cdots$，使得对每个 $n$，

- $P_{g(n)} \neq \emptyset$，且
- $\sigma_{n+1} = \sigma_n \cup \{q^{-1}(g_1(\sigma_n))\}$。

故 $\cap_{n<\omega} P_{g(n)} \neq \emptyset$，且对于任意 $z \in \cap_{n<\omega} P_{g(n)}$，实数 $y = \bigcup_{n<\omega} \sigma_n$ 是 $z$ 的子集。

#### 推论 14.6.5. 若 $x$ 不是 $\Delta^1_1$-半可回溯的，则 $x$ 不是对 $\Delta^1_1$-Kurtz 随机性低的。

证明。假设 $x$ 不是 $\Delta^1_1$-半可回溯的。设 $T$ 为 $\Sigma^1_1$-树，使得 $\mu([T]) > 0$ 且 $[T]$ 仅包含 $\Pi^1_1$-ML 随机实数。则由引理 14.6.4，存在 $z \in [T]$ 和 $y \le_T x$，使得 $z$ 是 $\Delta^1_1(x)$-闭零集 $\{r \mid y \le_T r\}$ 的元素。故 $x$ 不是对 $\Delta^1_1$-Kurtz 随机性低的。

这引出了以下定理。

#### 定理 14.6.6 (约斯-汉森、尼斯、斯蒂芬和于 [68]). 对于任意 $x \in 2^\omega$，以下命题等价：

- (i) $x$ 是对 $\Delta^1_1$-Kurtz 测试低的；
- (ii) $x$ 是对 $\Delta^1_1$-Kurtz 随机性低的；
- (iii) $x$ 是 $\Delta^1_1$-被支配的且 $\Delta^1_1$-半可回溯的。

目前尚不清楚是否存在非超算术实数且对 $\Pi^1_1$-Kurtz 随机性低。然而，我们可以证明以下集合包含关系。

#### 提议 14.6.7 (约斯-汉森、尼斯、斯蒂芬和于 [68]). 若 $x$ 是对 $\Pi^1_1$-Kurtz 随机性低的，则 $x$ 是对 $\Delta^1_1$-Kurtz 随机性低的。

证明。假设 $x$ 是对 $\Pi^1_1$-Kurtz 随机性低的，$y$ 是 $\Delta^1_1$-Kurtz 随机的，且存在 $\Delta^1_1(x)$-闭零集 $A$ 使得 $y \in A$。由提议 14.1.2，集合

$$
B = \bigcup \{[C] \mid C \text{ is a } \Delta^1_1\text{-closed nullset}\}
$$

是 $\Pi^1_1$-零集。则 $A \setminus B$ 是 $\Sigma^1_1(x)$。由于 $y$ 是 $\Delta^1_1$-Kurtz 随机的，$y \notin B$。故 $y \in A \setminus B$，且 $A \setminus B$ 是 $\Sigma^1_1(x)$ 且非空。因此存在 $z \in A \setminus B$，使得 $\omega_1^x = \omega_1^z = \omega_1^y$。由于 $z \notin B$，$z$ 是 $\Delta^1_1$-Kurtz 随机的。由提议 14.1.4，$z$ 是 $\Pi^1_1$-Kurtz 随机的。这与 $x$ 是对 $\Pi^1_1$-Kurtz 随机性低的事实矛盾。

### 14.6.2 对 $\Delta^1_1$-随机性低

#### 定理 14.6.8. 对于实数 $x$，以下命题等价：

- (i) $x$ 是 $\Delta^1_1$-可追踪的；
- (ii) 每个 $\Delta^1_1(x)$-零集都包含于某个 $\Delta^1_1$-零集；
- (iii) $x$ 是对 $\Delta^1_1$-随机性低的；
- (iv) 每个 $\Pi^1_1$-ML 随机实数都是 $\Delta^1_1(x)$-随机的。

证明。(i) \(\Rightarrow\) (ii): 假设 $x$ 是 $\Delta^1_1$-可追踪的。设 $S$ 为 $\Delta^1_1(x)$-零集。由相对化于 $x$ 的提议 14.2.2，存在 $\Delta^1_1(x)$-ML 测试 $(U_n)_{n \in \omega}$，使得对每个 $n$ 有 $\mu(U_n) = 2^{-n}$ 且 $S \subseteq \bigcap U_n$。令 $(S_e)_{e \in \omega}$ 为 $2^{<\omega}$ 所有有限子集的递归枚举。存在函数 $f \le_S x$ 使得 $(S_{f(n,s)})_s = U_{n,s}$ 满足 $U_{n,s} \subseteq U_{n,s+1}$、$U_n = \bigcup_{s < \omega} U_{n,s}$ 且 $\mu(U_{n,s}) > 2^{-n}(1 - 2^{-s})$。令 $T = (T_e)_{e \in \omega}$ 为 $f$ 的 $\Delta^1_1$-迹。我们可以选取 $T$，使得此外对每个 $e > 0$ 有 $|T_e| \le e$。

我们现在通过 $\hat{T}$ 定义 $T$ 的子迹 $V_n$，即对每个 $n, s$ 有 $\hat{T}_{(n,s)} \subseteq T_{(n,s)}$。目标是通过 $\hat{T}$（以待指定的方式）定义开集 $V_n$，使其足够小以给出 $\Delta^1_1$-零集 $\mathcal{V} = \bigcap_{n < \omega} V_n$，同时又足够大以将所有“相关”实数排除于 $T_{(n,s)} - \hat{T}_{(n,s)}$ 之外，从而 $\bigcap_{n < \omega} U_n \subseteq \mathcal{V}$。

令 $\hat{T}_{(n,s)}$ 为 $T_{(n,s)}$ 中满足 $2^{-n}(1 - 2^{-s}) \le \mu([S_e]) \le 2^{-n}$ 且 $[S_e] \subseteq [S_d]$（其中 $d \in \hat{T}_{(n,s-1)}$，并令 $\hat{T}_{(n,-1)} = \omega$）的所有 $e$ 的集合。注意 $f((n,s)) \in \hat{T}_{(n,s)}$。令 $V_n = \bigcup \{ [S_e] \mid e \in \hat{T}_{(n,s)}, s \in \omega \}$。

则 $\mu(V_n) \le 2^{-n} \lceil T_{(n,0)} \rceil + \sum_{s < \omega} 2^{-2-n} \lceil T_{(n,s)} \rceil$。由于对 $(n,s) \neq 0$ 有 $\lceil T_{(n,s)} \rceil \le \lceil T_{(n,s)} \rceil \le \langle n,s \rangle$，且 $\langle n,s \rangle$ 在 $n$ 和 $s$ 中仅多项式增长，显然 $\lim_n \sum_{s < \omega} 2^{-2-n} \lceil T_{(n,s)} \rceil = 0$，故 $\lim_n \mu(V_n) = 0$。因此 $\mathcal{V} = \bigcap_n V_n$ 是 $\Delta^1_1$-零集且 $\bigcap U_n \subseteq \mathcal{V}$。

(ii) \(\Rightarrow\) (iii) 和 (iii) \(\Rightarrow\) (iv) 立即成立。

(iv) \(\Rightarrow\) (i)。证明与 [67] 中的证明相同。我们将其留给读者。

由定理 13.3.18，对 $\Delta^1_1$-随机性低与对 $\Delta^1_1$-Kurtz 随机性低不同。

### 14.6.3 对 $\Pi^1_1$-ML 随机性低

#### 定理 14.6.9 (约赫特和尼斯 [51]). 每个对 $\Pi^1_1$-ML 随机性低的实数都是超算术的。

证明。我们给出一个证明概略。假设 $x$ 是对 $\Pi^1_1$-ML 随机性低的。则不难验证 $\omega_1^x = \omega_1^{CK}$，且存在 $\Pi^1_1(x)$-ML 随机实数 $y \ge_T x$。事实上，可以使用 [51] 中引入的 $\Pi^1_1$-版图灵归约（称为 $\le_{fin-h}$）来论证 $x \le_{fin-h} y$。换言之，存在一致的 $\Pi^1_1$-偏映射 $\Phi : 2^{<\omega} \to 2^{<\omega}$，使得 $x = \bigcup_{n < \omega} \Phi(Y \upharpoonright n)$。应用 [48] 中的方法可以证明 $x$ 是 $K_{HJ}$-平凡的，其中 $K_{HJ}$ 是 $\Pi^1_1$ 设置中 Kolmogorov 复杂度的类比。如 [51] 所示，每个 $K_{HJ}$-平凡实数要么是超算术的，要么与 $0^\triangledown$ 超算术等价。由于 $\omega_1^x = \omega_1^{CK}$，$x$ 必须是超算术的。





### 14.6.4 对 \(\Pi^1_1\)-随机性和强 \(\Pi^1_1\)-ML 随机性的低度

定理 14.6.9 引发了一个自然问题：刻画对 \(\Pi^1_1\)-随机性低的实数——特别是是否存在一个不是超算术的实数。后者的答案是否定的。命题 14.6.10 给出了这类实数的刻画。我们说 x 是非 \(\Pi^1_1\)-随机可上确的，如果对于所有 \(\Pi^1_1\)-随机 y，都有 x \(\oplus\) y \(\ge_h\) 0。可以立即看出，如果 x 对 \(\Pi^1_1\)-随机性低，则 \(\omega_1^{CK} = \omega_1^x\)。

#### Proposition 14.6.10 (Harrington, Nies 和 Slaman [12]). 实数 x 是低 for \(\Pi^1_1\)-随机性当且仅当 x 是低 for \(\Delta^1_1\)-随机性且 x 是非 \(\Pi^1_1\)-随机可上确的。

Proof. If x is low for \(\Pi^1_1\)-randomness, then every \(\Pi^1_1\)-random real is \(\Pi^1_1(x)\)-random. Note that by relativizing Theorem 13.14, the \(\Pi^1_1(x)\)-set \(\{y \mid y \oplus x \ge_h 0\}\) is null since \(x \ge_h 0\). Thus x is non-\(\Pi^1_1\)-random cupable.

Suppose y is \(\Delta^1_1\)-random. If x is not \(\Delta^1_1(x)\)-random, then there is a \(\Delta^1_1(x)\)-nullset A containing y. By Proposition 14.2.3, the set \(B = \bigcup \{C \mid \mu(C) = 0 \land C \text{ is } \Delta^1_1\}\) is a \(\Pi^1_1\)-nullset. Now \(y \in A \land B\). Hence \(A \land B\) is a nonempty \(\Sigma^1_1(x)\)-set. By the Gandy Basis Theorem (2.5.3), there is \(z \in A \land B\) such that \(\omega_1^x = \omega_1^z = \omega_1^{CK}\). By Corollary 14.3.2, z is \(\Pi^1_1\)-random but not \(\Pi^1_1(x)\)-random, a contradiction.

Conversely, suppose x is low for \(\Delta^1_1\)-randomness and non-\(\Pi^1_1\)-random cupable. Then \(x \ge_h 0\). Let z be a \(\Pi^1_1\) random real. Relativizing the proof of Theorem 14.3.1, the largest \(\Pi^1_1(x)\)-nullset \(\mathcal{O}(x)\) is a union of countably many \(\Delta^1_1(x)\)-null sets \(\mathcal{O}_n(x)\) and the \(\Pi^1_1(x)\)-nullset \(\{y \mid y \oplus x \ge_h 0\}\). Since x is low for \(\Delta^1_1\)-randomness, \(z \notin \bigcup_n \mathcal{O}_n(x)\). Since x is non-\(\Pi^1_1\)-random cupable, \(z \oplus x \ge_h 0\). Hence z is \(\Pi^1_1(x)\)-random. We conclude that x is low for \(\Pi^1_1\)-randomness.

#### Proposition 14.6.11. There is a \(\Delta^1_1\)-traceable x which is \(\Pi^1_1\)-random cupable.

Proof. By Corollary 13.33.8, there is an uncountable \(\Sigma^1_1\)-set A containing only nonhyperarithmetic \(\Delta^1_1\)-traceable reals. Let \(\mathcal{O}\) be the largest \(\Pi^1_1\)-nullset. By Theorem 13.2.1, there exist \(x \in A\) and \(y \notin \mathcal{O}\) such that \(x \oplus y \ge_h 0\).

#### Corollary 14.6.12.

- (i) Lowness for \(\Pi^1_1\)-Kurtz randomness is different from \(\Delta^1_1\)-Kurtz randomness;
- (ii) Lowness for \(\Pi^1_1\)-randomness is different from \(\Delta^1_1\)-randomness.

Proof. To prove (i), note that by Theorem 14.6.8 and 14.6.6, every \(\Delta^1_1\)-traceable real is low for \(\Delta^1_1\)-Kurtz randomness. By Proposition 14.6.11, there is an x which is low for \(\Delta^1_1\)-Kurtz randomness for which there is a \(\Pi^1_1\)-random y satisfying \(x \oplus y \equiv_h 0\). We claim that x is not low for \(\Pi^1_1\)-Kurtz randomness. Let \(e < \omega\) and \(e \in \mathcal{O}\) such that \(y = \Phi_e^{H_e^\emptyset}\). Then
\(z \in \{y\} \Leftrightarrow (\exists r \le_h x \land z(r) \in \{e\}) \land z = \Phi_e^{H_e^\emptyset}\).

Hence y is a \(\Pi^1_1(x)\)-singleton and so non-\(\Pi^1_1(x)\)-random. Note that (ii) follows immediately from Proposition 14.6.10 and 14.6.11.

We now show that no nonhyperarithmetic real is low for \(\Pi^1_1\)-random. Let \(\mathbb{P} = \langle \mathbf{P}, \le \rangle\) be a notion of forcing, where

\(\mathbf{P} = \{P \mid P \text{ is nonempty and } \Sigma_1^1\text{-closed containing only } \Pi_1^1\text{-ML random reals}\}\).

For \(P, Q \in \mathbf{P}\), define \(P \le Q\) if and only if \(P \subseteq Q\). Note that \(\mu(P) > 0\) for each \(P\).

Let \(((\varphi_i, \psi_i))_{i < \omega}\) be a recursive enumeration of arithmetical formulas. For each \(i\), let

\(A_i = \{x \mid \exists l (\omega_1^{\text{CK}, x}, x) = (\forall k)(\exists y)(\varphi_i(k, y) \lor \neg \psi_i(k, y))\}\).

Define an approximation of \(A_i\) at \(j\) as

\(A_{i,j} = \{x \mid \exists l (\omega_1^{\text{CK}, x}, x) = (\forall k \le j)(\exists y)(\varphi_i(k, y) \lor \neg \psi_i(k, y))\}\)

and for \(n \in \mathcal{O}\), set

\(A_{i,j,n} = \{x \mid \exists l (\omega_1^{\text{CK}, x}, x) = (\forall k \le j)(\exists y^{|n|})(\varphi_i(k, y^{|n|}) \lor \neg \psi_i(k, y^{|n|}))\}\).

Suppose \(x \in A_i\). Then for each \(j\), there is an \(n\) such that \(x \in A_{i,j,n}\). Uniformly for each \(j < \omega\) and \(n \in \mathcal{O}\), apply a "dual form" of Lemma 13.1.10 obtained by replacing \(m, n\) there respectively with \(l\) and the Gödel number of "\((\forall k < j)(\exists y^{|n|})(\varphi_i(k, y^{|n|}) \lor \neg \psi_i(k, y^{|n|}))\)". We then have a \(\Pi_1^1\)-function \(p_i : \omega^2 \times \mathcal{O} \to \omega\) such that for \(j, l < \omega\) and \(n \in \mathcal{O}\),

\(U_{i,j,l,n} = \{x \mid \exists l (\omega_1^{\text{CK}, x}, x) = \neg p_i(j, l, n)\}\)

is a \(\Delta_1^1\)-open cover of \(A_{i,j,n}\), with \(\mu(U_{i,j,l,n} \setminus A_{i,j,n}) < 2^{-j-n-1}\). Then \(U_{i,j,l} = \bigcup_{n \in \mathcal{O}} U_{i,j,l,n}\) is a \(\Pi_1^1\)-open set. Note that \(A_{i,j} \subseteq U_{i,j,l}\) and

\(\mu(U_{i,j,l} \setminus A_{i,j}) < \sum_{n < \omega} 2^{-j-n-1} \le 2^{-j-l+1}\).

Let \(G_i \supseteq A_i\) be the \(\Pi_1^1\)-set defined as \(\bigcap_{l,j} U_{i,j,l}\). Let

\(\mathcal{D}_1 = \{P \in \mathbb{P} \mid P \subseteq G_i \lor P \cap G_i = \emptyset\}\).

#### Lemma 14.6.13. \(\mathcal{D}_1\) is dense for each \(i\).

Proof. Let \(P\) be a condition. There are two cases to consider:

Case 1. \(\mu(P \setminus G_i) > 0\). Then there is a \(k\) such that \(\mu(P \cap \bigcap_{(j,b) \le k} U_{i,j,l}) > 0\). Let \(Q = P \cap \bigcap_{(j,b) \le k} U_{i,j,l}\). Then \(Q \in \mathcal{D}_1 \cap \mathbf{P}\).

Case 2. \(\mu(P \setminus G_i) = 0\). By Lemma 13.1.10, there exists a \(\Sigma_1^1\)-closed set \(F \subseteq G_i\) such that \(\mu(F \cap P) > 0\). Let \(Q = P \cap F\). Then \(Q \in \mathcal{D}_1 \cap \mathbf{P}\).

#### Theorem 14.6.14 (Monin [105]). If \(g\) is a \(\mathbb{P}\)-generic real meeting all \(\mathcal{D}_i\)'s, then \(a_g^E = \omega_1^{\text{CK}}\).

Proof. Let g be P-generic. It is sufficient to prove that \(\mathfrak{A}(\omega_1^{CK}, g) = \Delta^1_1\)-comprehension. Let P be a condition such that \(g \in P\). If \(P \cap G_i = \emptyset\), then \(P \cap A_i = \emptyset\). It follows that there is a k such that \(\mathfrak{M}(\omega_1^{CK}, g) = (\forall y)(\neg \varphi_i(k, y) \land \varphi_i(k, y))\). Otherwise \(P \subseteq G_i\). By topological compactness, for any j and l there is an n such that \(P \subseteq U_{i,j,l,n}\). It follows that there is a total \(\Pi_1^1\) - hence \(\Delta^1_1\) - function \(f : \omega^2 \to \omega\) such that for any i, j, l, \(f(i, l) \in \mathcal{O}\) and \(P \subseteq U_{i,l,f(i,l)}\). Hence there is an \(m \in \mathcal{O}\) such that \(f(i, l) < |m|\) for any j, l. Then \(C_i = \bigcup_{l < \omega} \bigcap_{n < \omega} (U_{i,l,f(i,l),n} \setminus A_{i,f(i,l),n})\) is a \(\Delta^1_1\)-nullset. Since g is \(\Pi^1_1\)-ML-random, \(g \in C_i\). Then for any j, there is an l such that \(g \in A_{i,l,f(i,l),n}\). Thus \(\mathfrak{A}(\omega_1^{CK}, g) \models (\forall k)(\exists m)(\varphi_i(k, y^{|m|}) \lor \neg \varphi_i(k, y^{|m|}))\) and so \(\mathfrak{A}(\omega_1^{CK}, g) \models \Delta^1_1\)-comprehension.

#### Theorem 14.6.15 (Greenberg and Monin). Every low for \(\Pi^1_1\)-random real is hyperarithmetic.

Proof. Suppose that x is not hyperarithmetic. By Theorem 14.6.9, x is not low for \(\Pi^1_1\)-ML randomness. Let \(\{U_n\}_{n<\omega}\) be a universal \(\Pi_1^1(x)\)-ML test. We claim that for any n and \(P \in \mathbf{P}\), \(U_n^P \cap P \neq \emptyset\). Otherwise, \(P \cap U_n^P = \emptyset\) for some n. Then every real \(z \in P\) is \(\Pi_1^1(x)\)-ML random. However, for any \(\Pi^1_1\)-ML random y, by Proposition 14.2.7, there is a \(z \in P\) such that \(y =^* z\). Hence y is also \(\Pi_1^1(x)\)-ML random. In other words, x is low for \(\Pi_1^1\)-ML random, a contradiction.

Since P contains only \(\Pi_1^1\)-ML random reals, \(P \cap U_n^P \neq \emptyset\) implies that there is a condition \(Q \subseteq P \cap U_n^P\).

Let \(\mathscr{D}^n = \{P \in \mathbf{P} \mid P \subseteq U_n^P\}\). Then \(\mathscr{D}^n\) is dense for each n. If g is P-generic meeting each \(\mathscr{D}_i\) and \(\mathscr{D}^n\), then g is \(\Pi_1^1\)-random and \(g \in \bigcap_{n<\omega} U_n^P\). In other words, g is not \(\Pi_1^1(x)\)-ML random and hence not \(\Pi_1^1(x)\)-random.

By the proof of Theorem 14.6.15, for any x if every \(\Pi^1_1\)-random real is \(\Pi_1^1(x)\)-ML random, then x must be hyperarithmetic.

#### Corollary 14.6.16. A real x is low for strongly \(\Pi^1_1\)-ML random if and only if it is hyperarithmetic.

Proof. Obviously every hyperarithmetic real is low for strongly \(\Pi^1_1\)-ML random. Now suppose that x is low for strongly \(\Pi^1_1\)-ML random. Then every \(\Pi^1_1\)-random real is strongly \(\Pi_1^1(x)\)-ML random and so \(\Pi_1^1(x)\)-ML random. So x must be hyperarithmetic.

### 14.6.5 Lowness for \(\Delta^1_2\)- and \(\Sigma^1_2\)-randomness

One may also introduce the notion \(\Delta^1_2\)-traceability as for \(\Delta^1_1\)-traceability. However, this notion is vacuous under \(V = L\) in view of Proposition 14.4.2. Thus we have the following conclusion



### 命题 14.6.17. 如果 V = L，则

\(\Sigma^1_2\)-ML 随机性的低度 = \(\Delta^1_2\)-随机性的低度。

在 \(\Sigma^1_2\)-随机性的低度情况下，可以应用定理 14.4.7 来获得一个刻画。最后，可以以显而易见的方式引入建设性可追踪性的概念，并利用它在额外集合论假设下研究 \(\Sigma^1_2\)-随机性的低度属性。这将涉及集合论中一些复杂技术的使用。有兴趣的读者可参阅 [2]。

### 14.6.6 练习

- 练习 14.6.1. 证明引理 14.6.3。
- 练习 14.6.2. 证明 x 是 \(\Delta^1_1\)-半递归的当且仅当每个 \(\Pi^1_1\)-ML 随机实数都是 \(\Delta^1_1(x)\)-Kurtz 随机的。
- 练习 14.6.3. 证明存在两个不可数的 \(\Sigma^1_1\)-集合 A, B，使得对于任何 x ∈ A, y ∈ B 和递归序数 \(\beta\)，(x ⊕ y)^β ≮_T O。
- 练习 14.6.4 (Bienvenu, Greenberg 和 Monin)。设 \((G_i)_{i \in \omega}\) 如前定义。证明一个 \(\Delta^1_1\)-随机 x 是 \(\Pi^1_1\)-随机的当且仅当对于任何 i，要么 x ∉ G_i，要么 x ∈ ⋃ {P ∈ P | P ⊆ G_i}。
- 练习 14.6.5 (Monin [105])。证明 \(\Pi^1_1\)-随机实数的集合是 \(\Pi^1_3\) 但不是 \(\Sigma^1_3\)。
- 练习 14.6.6 (Greenberg 和 Monin)。证明如果 x 是 \(\Delta^1_1\)-随机性的低度但不是超算术的，那么 x 是 \(\Pi^1_1\)-随机性可加的。

## A 开放问题

### A.1 超算术理论

我们首先列出一个悬而未决近 40 年的问题。

- **问题 A.1.1** (Sacks [122]). *每个可数的超度集合是否都有一个最小上界？*

下一个问题涉及超算术设置中 Posner–Robinson 定理的一个版本。

- **问题 A.1.2.** 设 \( x \notin \text{HYP} \) 且 \( A \subseteq 2^\omega \) 为 \(\Sigma^1_1\) 且不可数。是否存在 \( y \in A \) 使得 \( x \oplus y \ge_h \emptyset \)？

### A.2 递归论中的集合论问题

本领域最重要的问题大概是 Martin's Conjecture (6.6.9)。我们还有以下猜想。

- **猜想 A.2.1.** 假设 ZF + AD + \( V = L(\mathbb{R}) \)。那么 Martin's Conjecture 对于序保持函数成立。

- **问题 A.2.2** (Sacks [117]). 每个局部可数的偏序集 \( (2^\omega, \le_P) \) 是否都可以嵌入到 \( (\mathscr{D}, \le) \) 中？

以下内容受定理 9.3.8 启发。

- **问题 A.2.3.** 在 ZF + DC 下，序类型为 \(\omega_1\) 的图灵度终极最大链的存在是否蕴含实数集的良序存在？

也许更神秘的是图灵度的反链结构。

- **问题 A.2.4.** 是否存在 \(\Sigma^1_1\)-最大反链的图灵度？

虽然在第 9 章中展示了若干独立于 ZF 的递归论例子，但目前不知道是否存在偏序语言中一个“自然”的一阶句子 \(\varphi\)，使得 "\( (\mathscr{D}, \le) \vDash \varphi \)" 独立于 ZF。

- **问题 A.2.5.** 是否存在偏序语言中一个自然的一阶句子 \(\varphi\)，使得 "\( (\mathscr{D}, \le) \vDash \varphi \)" 独立于 ZF？

在 [128] 中，证明了如果每个实数集都是可测的，那么 \(\omega_1\) 在 L 中是不可达的。

- **问题 A.2.6.** 将一组图灵度 \(\mathscr{A}\) 与其度属于 \(\mathscr{A}\) 的实数集合识别。如果每个图灵度集合都是可测的，那么 \(\omega_1\) 在 L 中是否不可达？

### A.3 高阶随机性理论

- **问题 A.3.1.** 每个 \(\Pi^1_1\)-随机实数是否都是强 \(\Pi^1_1\)-ML 随机的？

根据推论 14.34，问题 A.3.1 可以归约为存在一个强 \(\Pi^1_1\)-ML 随机的 \(x \ge_h 0\) 的问题。

目前不知道是否存在一个非超算术实数且不是 \(\Pi^1_1\)-随机性可加的，尽管我们知道 \(\Pi^1_1\)-随机性的低度与超算术性重合。

在第 14 章中，算法随机性的研究被推广到 \(\Pi^1_1\)-水平。同时也表明，在 \(V = L\) 假设下，将随机性概念推广到 \(\Sigma^1_2\)-水平无法获得令人满意的理论。事实上，在这个假设下，将随机性概念推广到解析层次结构中 \(\Pi^1_1\) 之外的任何层次，都会导致一个本质上平凡的理论。关键原因是 \(L\) 内存在 \(2^\omega\) 的一个 \(A_3\) 良序。因此，需要其他集合论公理来在解析层次结构的更高层次上建立可行的算法随机性理论。描述集合论中存在一种“正则性”现象，即在 PD 下所有 \(\Pi^1_{2n+1}\) 和 \(\Sigma^1_{2n}\) 集合都被视为可枚举集的类比。我们有兴趣看看这是否适用于高阶随机性理论。

- **问题 A.3.2.** 在某些大基数假设下，是否可以将高阶随机性理论扩展到整个解析层次结构？

Kechris, Martin 和 Solovay [65] 在 PD 下将高阶算术理论扩展到 Q-理论。随后可以在 Q-理论中引入高阶随机性理论。然而，描述集合论的现代发展已经踏上了一条与之前略有不同的路线。在 1980 年代之前，大多数描述集合论结果是通过巧妙构造获得的，例如与博弈和 AD 相关的构造。今天，大基数和内模理论在描述集合论的研究中占据重要地位。即使看似是其低阶对应物的“直接推广”的结果也是以这种方式确立的。由于递归论建立在有效可计算性的前提之上，人们有兴趣拥有一个“好的 L 类似模型”来执行如同在 L 中那样的递归论构造。在这样的模型中，高阶随机性的研究可以合理地进行。

## B 与 Gerald E. Sacks 的访谈

Chi Tat Chong 和 Yue Yang¹

Gerald E. Sacks 是哈佛大学数理逻辑荣休教授。他于 1961 年在康奈尔大学获得博士学位，并在康奈尔大学任教直到 1967 年，之后受聘于 MIT。他从 1972 年起在哈佛大学和 MIT 任教，2006 年从 MIT 退休，2012 年从哈佛大学退休。萨克斯教授在递归论方面的工作在过去 50 年里对该学科的发展产生了深远影响。此次访谈于 2009 年 6 月在纽约市立大学研究生中心进行。

**提问：** 感谢您接受此次访谈。我们认为花些时间与您交谈，听取您关于递归论及一般逻辑的工作和观点，是个好主意。这将对逻辑学的学生是一种启发，也是专业逻辑学家以及该学科历史学家的重要信息来源。我们认为人们会有兴趣从您的角度了解递归论中主要主题和思想的发展。这样的叙述将非常有启发性。

**萨克斯：** 我很难相信这一点，但我愿意试一试。
*（笑声）*

**问：** 我认为就此次访谈的目的而言，我们最好从头开始。我了解您来自布鲁克林。
**萨：** 纽约布鲁克林。是的。

**问：** 您曾就读于一所名为布鲁克林技术高中的地方。那时您是否已经决定想成为一名数学家？
**萨：** 没有。没有。我大约在 10 或 11 岁时对数学感兴趣。但当我 12 或 13 岁时，兴趣就消退了。我注意到的是，女生对数学不感兴趣，或者那些整天谈论数学的男生也不感兴趣。但他们对文学和艺术感兴趣。所以我的兴趣转移了。*（笑声）* 我对数学的兴趣减少了，而对文学、诗歌和艺术等更感兴趣。

**问：** 但当你上大学时，你是否……
**萨：** 我上大学时，我想成为一名工程师，我不知道为什么。那将是一个可怕的错误。但幸运的是，在我完成工程学业之前，我去了军队。我在军队待了三年，再次对数学产生了兴趣。有人给了我一本 S. C. Kleene 所著的 *元数学导论*……

**问：** 我想，是一位数学家给了你？
**萨：** 是的，是的，我开始阅读它，并觉得它非常有趣。




这是我毕业之前的事。我当时大约修完了工程课程的一半。我中断学业去参军了。例如，他对数学归纳法原理的运用让我惊叹不已。在我对数学非常感兴趣的那些日子里，我学习过数学归纳法。但这里克莱尼用它来证明关于公式的某些东西。所以我觉得这太神奇了。我以为你得对整数进行归纳，你知道。但这里，他正在用归纳法证明演绎定理及相关定理。我想这只是针对命题演算。对我来说，这太神奇了。

Q: 在那之前，你没有修过任何逻辑课程吗？所以这是你第一次接触这个学科？
S: 布鲁克林技术学院的数学课程只是例行公事。你知道，老派的课程。没有微积分，只有代数、平面几何和立体几何——你知道，那些东西。我是说那里有四年的数学，但与现在学校提供的相比，相当基础。

Q: 那你是去布鲁克林学院学工程的吗？
S: 不。我在康奈尔大学。

我回到康奈尔，决定最简单的办法就是完成工程课程。但我修了数学系所有可能的选修课。我现在对数学感兴趣了。但我仍不确定是否要放弃工程。等我完成工程课程时，我已经致力于数学，原因之一是康奈尔有一位著名的逻辑学家巴克利·罗瑟，他同意担任我的导师。我现在致力于数学，特别是逻辑。

Q: 但在那之前你从未跟他上过逻辑课。
S: 没有。但我读过克莱尼书的大部分内容。所以我对逻辑知道一些。我啃完了不完备定理，他让我第一年就向他详细讲解证明——那是他的教学方法。我不得不站在黑板前，详细地向他讲述哥德尔不完备定理的证明。他希望得到详细的证明，我当时对此颇感兴趣，但我从未强迫我的任何学生这样做。

Q: 那时康奈尔只有你一个逻辑学生吗？
S: 是的。我是他唯一的学生。大致说来，逻辑研讨会由他和我组成。他也会讲。他向我解释了各种事情。但他让我来讲——让我想想——不完备定理，哥德尔在 L 中对广义连续统假设的证明。所以我们就这样继续下去了。

Q: 那是哪一年？
S: 应该是 1958-59 学年。那本橙色的书（《选择公理与广义连续统假设与集合论公理的一致性》）。

Q: 普林斯顿数学研究丛书的最早卷本之一。
S: 罗瑟当然熟悉它。但你说得对，当时可用的资料很少。例如，罗瑟知道塔斯基关于实数的判定过程，以及实闭域等等，但他手头只有油印稿。没有一本书讨论过这个。逻辑方面的书非常少。我是说，虽然哥德尔的连续统专著已经出版，但我不会真的称其为一本书。那只是一种论证形式。里面没有一句直观的评论。

Q: 这当然是一本专著，肯定不是那种……
S: 所以我啃完了它。我不敢说我真的理解了其中到底发生了什么，但我肯定是逐行理解了。我当时还不熟悉向下斯科伦–勒文海姆定理²，也没有人听说过精细结构之类的东西。我是说，那些东西当时根本不存在。但我能够给自己提供直观的解释，同时检查所有形式化内容。哥德尔的专著告诉你每一个细节，你只需要检查它，论证大概就讲得通了。我猜大概是这样。但真正的理解是后来才来的。多亏了许多人，其中之一是达纳·斯科特。

Q: 你是在五十年代末遇到斯科特的吗？
S: 不。我猜是 '61 年遇到他的。我 '61 年拿到博士学位，我想我在普林斯顿附近某个地方遇到他，可能是 '60 年秋天。在 '61 到 '63 学年期间，他一定是路过那里。让我想想。我 '61 到 '62 年以博士后奖学金去普林斯顿，并在高等研究院使用了它。当然，很多人来那里做报告。他一定是其中之一。例如，克雷塞尔来过几次。丘奇休假了一个学期或两个学期。所以他由亚伯拉罕·罗宾逊接替，我当时遇到了他。

Q: 罗宾逊是访问……
S: 罗宾逊大概是从 1961 学年开始担任访问教授。我那时遇到了他，他非常鼓励人。他似乎很渴望和我交谈。他确实给了我很大鼓舞。

Q: 也许我可以把话题稍微拉回到几年前。所以你当时在军队，得到了克莱尼的这本书。但当你决定做数学——转向数学时——你是如何决定选择逻辑，而不是代数、几何或其他什么的？

S: 我不确定。当然，递归（可计算）函数的想法非常有吸引力。但很难解释。当然，我对哥德尔的连续统专著印象深刻，其中涉及的想法以及能够证明类似的东西——其相对一致性——这似乎很有趣，也很不寻常。它与实分析或复分析、代数拓扑等截然不同。我是说，数学很有趣，但这些想法不知为何似乎更有趣。

Q: 你是否将哥德尔在其专著中引入的方法和想法视为无限图灵机运行的例证？
S: 哦，不，不。我只是惊讶于你可以拿出像“选择公理与 ZF 是否相容”这样的问题，并给出肯定的回答。我无法想象有人怎么能想出这个。

Q: 你那时有没有想过某些独立性结果的可能性？
S: 没有。不太有。第一年我不知道自己要做什么。罗瑟试图把我推向集合论，但我抵制了，因为他在集合论方面的兴趣不同。他仍然关注与新基础相关的一些未解决问题……

Q: 奎因的新基础？
S: 是的。我研究过那个。他把它整理好了。他的新基础版本比奎因的简单得多，并且与之等价。罗瑟也对更传统的集合论性质感兴趣。他非常关注这样一个问题：“是否存在不可达基数？”例如，他曾玩弄过这样一个想法：试图证明作为集合论定理不存在不可达基数。但我看不出如何开始做这样的事情。显然，你会假设存在一个不可达基数，然后试图推出矛盾，试图做一些组合数学的事情，他为此有一些宏大的计划。但我回避了那种事情……

Q: 但他知道在 ZF 下这是不可证明的——他知道这一点吗？
S: 他知道你无法证明不可达基数的存在。哦，是的，他知道这一点。但他试图证明不存在不可达基数。所以那没有被证明。我是说，据我所知，直到今天，没有什么能排除这种可能性，除非你假设更强的东西。与此同时，递归函数理论方面的论文不断涌现，越来越多。第一年我们手头只有克莱尼-波斯特论文，我认为那是一篇好论文。他让我把整篇论文向他讲解一遍。那篇论文末尾有一个我非常喜欢的定理，即：算术集的度上基本上存在一个最小对：存在度 a 和 b，使得一个度在 a 和 b 中都可递归，当且仅当它是算术的。

Q: 是的，那是一个非常漂亮的结果？
S: 那里的构造让我着迷，然后第二年罗瑟不在。那一年他由阿尼尔·尼罗德和西蒙·科赫接替。

Q: 他们刚加入康奈尔。
S: 所以科赫教了我一点模型论，当然那时模型论仍处于非常原始的状态。但尼罗德非常渴望讨论递归论。现在我们有了更多可用的论文：斯佩克特有两篇论文，一篇关于度，另一篇关于 \(\Pi^0_1\)-集的超度。

另外，肖恩菲尔德有一篇关于度的论文，我认为这真的让我信服了。在肖恩菲尔德的论文末尾还有一个未解决的问题，这让我决定尝试写一篇关于递归论的论文。我想尝试那些问题。我们还有弗里德伯格对波斯特问题的解答。但肖恩菲尔德的论文让我想到，弗里德伯格的方法——实际上是弗里德伯格-穆奇尼克方法——可以进一步发展 a

走得更远。当然，Post 问题的解决方案真的让我着迷。我无法释怀。它看起来与我曾经见过或思考过的任何东西都截然不同。我的意思是，当然现在这很平凡，但在那个时候，没有什么类似的东西。

- **Q:** 你第一次听说 Friedberg 解法是什么时候？

- **S:** 第二年秋天，Nerode 讲授了一门递归理论课程。那是 '59-'60 学年，他讲解了该解法。他进行了讲解。

- **Q:** 我明白了。Rosser 没有让你做研讨会并谈论……

- **S:** 我想，如果他那年不在那里，他会让我做的。但我们第一年很忙。他知道 Friedberg，等他讲到那里时。我们涉及了很多不同的东西。然后 Nerode 让我注意到 Shoenfield、Spector 等人的其他论文。我也很感兴趣，Spector 当时给出了一个度量论证，证明存在不可比拟的超级度。所以这同样很有趣。这又是一个意外的论证：是什么让他那样思考？第二年结束时，夏天开始时，我开始写我的论文。当然，我对那个时候有一些记忆，其中一些可能是假的，谁知道呢？我们总是在重写过去。但 Shoenfield 在他的论文中有一个定理：这里是 0'，存在两个都小于 0' 的度 a 和 b，它们的并是 0'。他将 0' 分割成两个更小的度 a 和 b。所以我想，为什么 a 和 b 不能是 r.e. 集的度呢？我整个夏天都在思考这个问题。我最终明白，如果我取一个非递归的 r.e. 集……哦，首先我取了一个度为 0' 的集，我最终明白我可以将它分割成两个不可比拟的集。然后我意识到，对于任何非递归的 r.e. 集，该论证仍然成立。所以我有了一个定理，并且我如鱼得水……

那应该是 1960 年的夏天。那是我第二年的结束。哦对，我忘了，那是 Friedberg 的分割定理。我想是 Nerode 把这个带到我面前的。Friedberg 将一个非递归的 r.e. 集分割成了两个非递归的 r.e. 集——这在我脑海中。所以问题是如何让它们具有更低的度。所以这是一个影响。分割定理的证明使用了有限损伤论证，但还有一个进一步的转折。

- **Q:** 是的，我们现在称之为 Sacks 保存策略。该方法在递归理论中已经是经典了。

- **S:** 我无法解释我的思路是怎样的。我只是日复一日地琢磨这个问题。但最终它成功了。现在 Shoenfield 在该论文末尾有另一个未解问题，即一个小于 0' 的最小度。所以我思考了这个问题，但没有进展。夏天结束时，虽然我还是学生，我去了普林斯顿，成为普林斯顿的访问学生，进行我研究生学习的第三年也是最后一年，因为 Rosser 在那里。他在第一年结束时离开时，决定在普林斯顿待两年。所以我又和他团聚了。我一直在思考 Shoenfield 的问题，即 0' 以下的最小度，因为这个最小度构造又是一个让我极其着迷的问题。

我反复读了那段。我想一年前 Nerode 让我向他解释证明。这似乎是一种常见的教学方法。（笑）我想，双方都受益。

Q: 那么，你开始思考这个问题是在遇见 Spector 之前还是之后？

S: 我还没有遇见 Spector。我拿到学位后才遇见他。我在普林斯顿又待了一年，但不是作为研究所的 NSF 博士后研究员。他刚完成这样一年。他即将离开，但那个夏天他还在那里。不幸的是，那个夏天他去世了。他当时只有 31 岁。

Q: 这是一个悲惨的损失……

S: 我思考了 0' 以下最小度的问题。我看了他的论证。他使用了康托尔集，我相当早就决定，我可以使用相当任意的树，但我不确定该如何处理它们。与此同时，我也思考了许多其他问题，例如在度中嵌入偏序。所以我在这方面玩了很多。最后我想——我不记得确切了——也许是 1961 年 2 月，当我在普林斯顿附近超市排队时，我明白了如何做到 0' 以下的最小度。

Q: 在超市排队有帮助！

S: 这个想法很简单。换句话说，看看 Spector 的论证，使用合适类型的树，每棵树本质上由一组 r.e. 数字编码。所以我意识到你可以改变主意。如果你有限次地改变主意，事情就会稳定下来。我意识到这可以做到。换句话说，0' 足以作为神谕。我不需要 0'' 神谕。如果我知道 0' 的故事，我就能做到这一切。

Q: 我想你不会建议研究生在卡住数学问题时花时间在超市吧？

S: 我不知道。几年后，我在密度定理上有过类似的经历。

Q: 这似乎成了习惯……

S: 我在那个问题上工作了很长时间，也许将近两年，断断续续。

我于 1961 年 6 月在研究所毕业。我仍然在尝试做递归理论。所以在 Shoenfield 的论文中，又有一个定理说，如果你取一个介于 0' 和 0'' 之间、在 0' 中是 r.e. 的度，那么它是 0' 以下某个度的跳。所以我对自己说，那个度能是 r.e. 吗？那将是一个更漂亮的定理，但出于显而易见的原因，我开始着手研究它——他不在这里为自己辩护——但 Shoenfield 是我在那一年研究所遇到的人之一，他也路过那里，我们聊了聊，我告诉他我正试图以这种方式改进他的结果。他说他不相信那是可能的。

我试图弄清楚他为什么那样想；他为什么那么确定？这是一种重建。他的论证是一个有限损伤论证，他觉得自己已经使用了递归理论中可用的最强方法。既然没有更强的方法，那就不会有更强的结果，大概是这样。是啊，那是我与他开始一段非常愉快关系的开端。他总是以一种有点粗鲁的方式非常鼓励人。之后我经常遇见他。多年来他总是说“你现在在做什么？”，而我会说“嗯，我之前在做这个，我已经做了那个”，或者“我正试图做某某事”。他会告诉我那是做错的事；你应该做这个。但他是推动密度定理的人。他认为那是正确的。在完成之前，他会撞见我：“你做完密度定理了吗？是什么在阻碍它？”（笑）我很长一段时间都没有意识到他喜欢我。我总觉得他在吹毛求疵，但后来我意识到……所以他不像亚伯拉罕·罗宾逊那样有人情味。他有同样的美好情感。

Q: 关于密度定理：要在这个问题上工作，必须对 r.e. 序的结构有强烈的信念。当时可用的关于结构的线索非常少。

S: 我花了那么多时间和精力，冒了很大的风险。嗯，有了分割定理，你就有一点证据。好吧，还有什么？我成功证明了“跳定理”，那是对 Shoenfield 结果的改进。为了做到这一点，我使用了无限损伤论证。

Q: 这是第一次使用无限损伤……吗？

S: 嗯，对我来说是第一次，但几年后我发现 Shoenfield 也做过无限损伤论证并发表了一篇论文。我想我有一种方法，似乎能处理密度定理中出现的一些困难，但不是全部。例如，有一个问题我大致玩了一下，作为热身：如果我有 r.e. 集 A <_T B，并且假设 A' <_T B'，那么我就能做到。我可以得到一个严格介于 A 和 B 之间的 r.e. 集 C。所以那是热身，但回避了真正的问题。问题本身花了一段时间。但我当时在超市排队。所以那是 1962 年春天的事。我和刚一起吃过午饭的人有个约会。

Q: 你当时在普林斯顿吗？

S: 不。我去纽约市拜访他。我本应在某个时间在他公寓楼前见他，但他迟到了。所以我又一次在思考这个问题。如何定义一个 r.e. 集 C，来智胜任何试图使用 A 作为神谕来计算 C 的计算？我突然明白了如何做到。

我在论文中试图说一些关于构造背后思想的直观内容，但失败了。我说，嗯，我们这里有一个方案，大致是假装将 B 嵌入 C，但如果需要则擦除它。从直观上看，擦除它在这里是合理的，如果你看看的话，但我认为这对阐述帮助不大。

Q: 但你早期的论文相当正式。

S: 但那是……我能怪谁呢？（笑）我曾向 Spector 抱怨他的论文非常正式。他的借口是 Kleene 是他的博士导师

克莱尼也是那篇论文的审稿人。所以审稿人迫使他用那种语言写作。

Q: 我想，要完全准确的话。

S: 是的，我以为自己没那么正式，但差不多。

Q: 我想，在你的橙色书《不可解度》中，有些页面和段落，你确实试图激励读者。

S: 是的，但那仍然很糟糕。我猜罗瑟也鼓励那种方法。他似乎不需要直观评论。（笑声）我是说，他可以直接读这些东西，一口气看完。他实际上是个非常强的数学家。他比我快。我可以把一大堆方程摆在他面前。他可以直接一口气看完。

Q: 他的老师是谁？

S: 丘奇。他是丘奇的学生。这很有趣。他和克莱尼同时是丘奇的学生。人们认为罗瑟是更快的那个。再说一遍，克莱尼不在这里为自己辩护。但我注意到克莱尼更坚持。这得到了回报。罗瑟不那么坚持。他懂得更多数学。他更快。但是…

Q: 他的兴趣似乎很广泛，不仅限于数学，还涉及各种各样的事情。

S: 火箭弹道学、解析数论：他从一件事跳到另一件事。

Q: 克莱尼可能更专注。

S: 是的，非常专注，专注到你无法想象的程度。我曾经问过他关于他最喜欢的定理，简单来说就是：2^E 的某一截正好由超算术集组成。我对此非常着迷。但这不是凭空捏造的。这两样东西都是由他定义的——相隔多年！（笑声）有一天他意识到它们是相等的。所以我认为这就是问题中的那个定理。我不是一天做到的。不，不，我认为他最坚持的事情是：如果一组整数是 A_1^1，那么它是 HYP——它是超算术的。所以我学了这个，因为当我还是康奈尔的助理教授时，涅罗德让我解释这个。（笑声）那是个挑战。那篇论文完全是形式化的。没有一句直观的评论。我一遍又一遍地读。他用定点定理来做有效跨递归，但“有效跨递归”这个短语根本没有出现！他只是直接做了。

Q: 思路是存在的。

S: 我不知道他正在做那件事。他只是对我而言非常惊人地使用了定点定理。所以我能够正式地表述它，但我并没有真正直观地理解它。我的意思是，我能够验证一切。所以我曾经问过他是如何得到那个定理的。他对经典描述集合论也一无所知。如果他懂，那会有帮助，因为他可以把它当作一种指南。但他一无所知。他只是从无中创造了它。花了一段时间，但他说他非常清楚，你不能永远做一个问题。你必须划出一些界限，否则你就会毁掉自己。所以他选择了一个界限，这个问题的一个时间限制，某一天，下午5点，之后他就不再做那个问题了。于是几个月过去了，那一天临近了。那天下午4点30左右，他解决了。

我不是在编造。他亲口告诉我的这个故事。所以我想我是向他学的。你问我为什么早期的论文那么正式，这确实是个跑题。我认为，部分是他的影响。他对我而言也太正式了。我对形式主义没有好感，却又喜欢它。但我想，是他和罗瑟的某种压力让我那样写。我最终让罗瑟承认，他脑海中有各种直观的图像，尽管他做的某些事情，我看不出那是如何可能的。你看，他在组合逻辑和 $\lambda$-演算方面做了一些事情，我看不出那里有任何可能的直观图像。那真是纯粹的形式化，你只能被困在那其中。但他能做到。也许这些人比你我更能进行形式化感知。（笑声）这种程度我甚至无法想象。当我研究经典递归论时，我总是在纸上或黑板上画点、叉、线来做图，但这些都没有出现在写稿中。（笑声）

Q: 你当时已经非常自由地使用丘奇论题了，至少在内心是这样？

S: 当然，当然。写稿与我思考那些事情的方式毫无关系，回头看，那毫无意义。我建议人们尽可能按实际操作的方式来写。

Q: 是的。似乎在你完成那两三个主要结果——分裂定理、跳跃反演定理、稠密定理——之后不久，你就……

S: 我也很自豪于 $0'$ 之下的最小度……

Q: 是的，我忘了提那个。

S: ……因为那是树上的有限优先级论证。换句话说，整棵树对其定义改变主意的次数是有限的。

Q: 那么，到1963年，甚至更早的时候，你开始思考高阶递归论了，我的意思是，超越自然数？

S: 是的，我想，这最初我要归功于涅罗德。在'62年秋天，我作为康奈尔助理教授的第一年，他让我做一个持续必要时间的研讨会。他有一群逻辑学生。那时康奈尔一定有四五个逻辑学生，这是一个惊人的变化。罗瑟大概每七年才有一个逻辑学生之类。（笑声）但时代变了。所以涅罗德认为，如果对逻辑感兴趣，人们应该学习 HYP 理论。这激发了我对更高层次事物的兴趣。

Q: 所以你做了一个关于那个的研讨会，为期一年的研讨会？

S: 这让我准备去理解克赖塞尔在说什么。克赖塞尔以一种难以理解的方式谈论递归论的推广。他研究出了一些东西，当然，这不必要地复杂，他解释的方式也很难透彻理解或领会。但最终它开始让我明白。他最初的表述基于 HYP 理论，这成了他和我称之为元递归论的东西。这是关于递归序数的递归论。

Q: 那是'65或'66年，它出现的时候？

S: 但我们在'63年夏天就开始谈论它了。所以在'63年春天，我完成了稠密定理的证明，并在'63年夏天把它写出来（以一种非常不吸引人的方式），并开始和他谈论递归序数上的递归论，元递归论。所以是'63年夏天。在'63年秋天，我们有了基本结果。

Q: 合作是如何发生的？

S: 我通常去拜访他。他经常去普林斯顿，我去过那里几次。当然没有电子邮件之类的东西。我尽可能多地去拜访他。他希望我用他的表述来处理递归序数上的波斯特问题。于是他这么做了。他提出了一些其他问题，于是我们写了一篇论文。我们在'64年春天发表了它，我想。有一个 AMS 会议，克莱尼是主席。克莱尼说我应该做报告，他会坐在前排，也许回答问题。所以我做了报告。当然，这是 HYP 理论的扩展。克莱尼非常感兴趣，当时间到时，我停了下来。于是他说：哦，如果你愿意，可以讲更久；时间充裕，（笑声）他非常非常和蔼。

Q: 从那以后你就再也没有回到经典递归论。你一直在继续前进……

S: 是的，我完全被克赖塞尔的计划吸引了，他有一个学生普拉特克，他让他去研究后来被称为可容序数的东西。盖伊·竹内首先注意到构造基数是可容的。可容序数的正式概念，以及一般集合，是由理查德·普拉特克和索尔·克里普克引入的。詹森对 L 的精细结构理论被萨克斯等人富有成果地用于研究 α-递归论中的问题。我见过他，和他谈过，并且一直和克赖塞尔交谈，他不想再写任何合著论文了。他说他会提供问题给我，但我应该自己写论文。我说好的。他说他不想再当合著者了。我认为在这方面他非常慷慨。这是他很少向人展示的一面。（笑声）他慷慨的一面，是存在的。他想要每个可容序数上的波斯特问题。我研究了那个。所以我做出了最初的结果，有点平凡，即对于每个可容的 α，总是存在一个中间度——α-度。但我没有得到两个不可比较的，暂时搁置了。

Q: 那大概是'65或'66年？

S: 这是在'65和'66年左右，因为我对强迫法产生了兴趣。我想思考强迫法，以及用完备集进行强迫和一些度量论证，仅用一个简单的度量论证就得到科恩的结果。但然后我又回到了 α-递归论，事实上，我要归功于肖尔，理查德·肖尔。我也开始对模型论感兴趣，想稍微思考一下。但是理查德


当时肖尔在 MIT 读书，而我休假一年后回来了。所以在 1970 年秋天，他说：为什么不为每个可接受序数 $\alpha$ 研究 Post 问题呢？为什么这还没人做过？我说，嗯，我以为罗杰斯的一个学生做过了。我们找他们确认一下。罗杰斯有个学生声称在他的论文中做过了。于是肖尔说他看过那个，但是是错的。你知道那篇论文稍早些时候就被接受了。我说，真的吗？他说完全错了。根本没有什么内容。所以我愿意相信他，我是说，我认识他。他研究生第一年我就在身边，和他谈过话，如果他说错了，那就是错了。我开始谈论这件事，边说边走到黑板前，说：嗯，假设我们看看这个案例，我说这似乎不算太糟糕。于是我说，我想这大概可以做成。但我决定和史蒂夫·辛普森分享一下。我和他聚在一起，把它当作一个联合成果完成了。他是个资历更深的学生。

Q: 你没有把这个问题交给辛普森去做吗？他确实写了关于 $\alpha$-递归的论文。

S: 不，他当时是最后一年，而且是的，他在思考 $\alpha$-递归理论。但我决定稍微逼他一下，因为他刚开始他的——也就是他必须完成的——最后一年。我说我把这件事分成了几种情况，并向他展示了我已经完成的那个情况。我说只剩下这个情况了，他隐约知道应该怎么做。他完成了那部分并写了论文。我觉得他写得非常好。

Q: 那就是萨克斯-辛普森论文了。

S: 实际上我们有好几种证明方法。但我决定他在论文中采用的方式是一种很好的写法。我发展出一种使用了比必要多得多的精细结构的证明。于是他去掉了一部分，曼尼·勒曼去掉了所有部分。（笑声）

Q: 勒曼不喜欢精细结构？

S: 我和他讨论过精细结构，他对精细结构了解一些。但我当然对根本不使用任何精细结构的想法很感兴趣。他把它拿捏得很准。

Q: 我一直认为，将精细结构理论的方法和思想融入递归理论是一件美妙的事情。你可以看到递归理论与集合论，以及模型论之间非常精妙的相互作用。

S: 当然。在肖尔关于所有可接受序数的密度定理的证明中，有一些精细结构的使用。事实上，他证明了一个关于精细结构的新事实，这在集合论界之前从未出现过。所以那里确实有一些精细结构，我是说，我无法证明，但我会断言它绝对是必要的。一旦你在 $\alpha$-递归理论中钻得足够深，你当然需要精细结构。所以你干脆从一开始就拥有它。于是我深深地沉迷于 $\alpha$-递归理论……

Q: 然后你决定可接受性其实并不必要，于是转向了 $\beta$-递归理论。

S: 我对不可接受的情况做了一些研究。然后西·弗里德曼深入其中，取得了一些出色的结果。

Q: 在这之后，你想，嗯，也许 E-递归* 是走向正确方向的办法？

S: 我当时还没到那一步。在那期间，我看了克莱尼关于高类型、有限类型对象中递归的论文。我想也许是谢恩菲尔德让我对此感兴趣。他稍微简化了一下克莱尼的定义。他研究了二类型对象中的递归；并写了一篇非常有趣的论文，准确解释了那里发生了什么。突然间，至少对于那个案例，一切都变得清晰明了，而在克莱尼那里并非如此。而莫斯乔瓦基斯正在研究 1/2 E，他做了一些看起来非常有趣的事情。我对截面问题产生了兴趣，1-截面，k-截面……

Q: 我记得在 1970 年的国际数学家大会上，你的演讲标题是 n 类型对象的 k-截面，大致是这样的……

S: 是的，我对此产生了兴趣。我对截面有一个猜想。当然我问了一位该领域的专家，他告诉我那绝不可能是真的。（笑声）令人惊讶的是，坚信某件事是事实是多么容易，但实际上并非如此！我想我们都犯过这个错误，但我可以告诉你，我猜我有一长串清单，里面是我研究过的一些事情，一些递归理论家告诉我那些不可能是真的。我每次都成功了（笑声）。

Q: 你的直觉告诉你相反的情况？

S: 是的，当然。至少我希望事情是这样。我不认为我的直觉比他们的好。我想要的方式比他们想要的更优美。

Q: 回到最小度。你的工作中一个主要的主线似乎围绕着与完美集强迫法相关的思想和技术展开：从 0' 以下的最小度到最小超度，可构性的最小度，以及 HYP 度的最小上界等等。其直觉是想看看你能把最小超度构造推多远吗？

S: 是的，我和罗宾·甘迪写了这篇论文（《一个最小超度》）。同样，涉及完美集，那是大约在 1965 年。所以现在强迫法被涉及进来；它确实是需要的。那是一个使用完美集的强迫论证。当然，这在集合论中也有意义。

Q: 但是进入 1980 年代，你仍在研究与那里相关的或使用那里技术的问题，例如超度集合的最小上界问题。

S: 是的，是的，我想我最终对完美集强迫法说了再见（笑声），我不记得是哪一年了，但定理是关于可数超度集合的上界。那就是论文的标题。那花了一段时间。我之前已经对 L 的一个可数初始段做过这件事。但那大量使用了 L 的非常好的可效良序。现在的可接受集合没有良序，但满足 $\Sigma_1$-依赖选择。所以那里有点东西，一个丑陋的三重强迫法的面孔。我没有把那篇论文写得像我可能做到的那样清晰。到那时我当然更直觉化了。这有点好笑。那篇论文被几个学生读过，他们似乎都很容易理解，尽管论证中存在漏洞，但一些学生似乎毫无问题地理解了它。鲍勃·卢巴斯基是其中之一，利奥·哈灵顿是另一个——当然他什么都能理解——还有弗雷德·艾布拉姆森。

Q: 你第一次遇见詹森是什么时候？使用 L 的精细结构来进行 $\alpha$-递归理论的想法是如何产生的？

S: 我第一次见到詹森，我得想一想。我想是卡罗尔·卡普告诉我的他。他们写了一篇重要的合著论文，标题是……

Q: 《原始递归集合函数》？它发表在 AMS 夏季研究所关于集合论的论文集中。

S: 我认为“凝结引理”这个词第一次出现在那里。所以他们试图整理一下，那些当时正在成为民间传说或常识的东西，换句话说，他们尝试并成功地在印刷品中说出了必须说的话。我当时觉得它过于正式，但我想我错了。有人必须做这件事，而他们做到了。我想是她让他对此感兴趣，然后他继续深入研究，当然他发展了精细结构。现在，我想他在 1967 年访问了剑桥（马萨诸塞州），我们谈过话。我想我比这更早见过他。1967 年在 UCLA 有一个大型集合论会议。他参加了那个会议。我不记得那时和他谈过多少话。他有点害羞。他避免人们可能彼此尖刻的场合。例如，那时一些人有点互相挑衅。我认为他们不如现在文明。他不喜欢那种事情。我乐意参与，而他不喜欢。当他来到剑桥时，我那时更理解他了，所以我们相处得不错。而且我认为他当时情绪有些低落。我想他正在研究一些难题，那正是他许多突破之前的事情。那是 60 年代末。在萨克斯-辛普森事件之前，我一定对他用精细结构在做什么有所耳闻，那件事大约是在 1970 年秋天完成的。辛普森在 1971 年完成。所以我们一定是在 1970 年秋天做的那件事。所以精细结构已经存在一段时间了，对吧？

Q: 詹森的论文本身直到 1972 年才发表。

S: 哪篇论文？

Q: 《可构宇宙的精细结构》。那篇论文的预印本当然在此之前就已经可以获得了。

S: 好吧，他一定做过报告。换句话说，我当然不是专家，但我对此了解一些。有递归序数的经验，入门很容易。我是说，关键在于投影，对吧？我当然知道 $\Sigma_1$-投影。我能看出这很有道理：对于任何 $\alpha$，你可以定义它的 $\Sigma_1$-投影。我当然知道凝结方法，我想，是从卡普-詹森论文中了解的。





Q: 但是，至少对于实数来说，细结构的研究实际上是从希拉里·普特南开始的。

S: 哦，是的，是的，对。那是另一个来源，布洛斯和普特南。

Q: 那是在詹森之前。你看过那篇论文并思考过它吗？

S: 是的。我了解那个，但当然我需要的本质上是说，\(\Sigma_n\)-投影的两种不同定义是相同的这一事实。我只需要针对 \(\Sigma_1\) 的情况。在 \(\omega_1^{CK}\) 的情况下，那几乎是平凡的。至少对于 \(\Sigma_1\)，通过一个简单的压缩论证很容易证明。当然，布洛斯-普特南的东西也是一个压缩论证。

Q: 另外，主码及其刻画的概念已经在他们论文中了。它被嵌入在某个地方，被称为“算术副本”。

S: 哦，是的。但只是动机大不相同。换句话说，我需要的正是那个事实，即 \(\Sigma_1\)-投影的两种定义。换句话说，一个非常小的，可以说，\(\alpha\)-t.e.集必须是 \(\alpha\)-有限的。那是关键。但我花了大量时间在高类型对象上，我不知道为什么。我又对有限类型对象上的递归产生了一段时间的浓厚兴趣。我的意思是，哈灵顿就是在这个主题上写他的博士论文，泰德·斯拉曼也在这个主题上写了他的博士论文。这在我脑海中停留了很长一段时间，我的意思是，我思考过各种问题，但就是做不出来。

Q: 关于最小 \(\alpha\)-度问题，首先，你认为这个问题有正解吗？

S: 哦，是的，是的，对于任意可接受的 \(\alpha\) 的最小 \(\alpha\)-度问题。是的，我思考过，但毫无进展，完全没有进展。我的意思是，当然我发现自己在思考 L 中的 \(\omega\)。也许那太难了（笑声）。

Q: 那 \(\omega_\alpha\) 呢？

S: 也许尝试那个会明智一些。可能 \(\omega_\alpha\) 是所有情况中最难的，应该留给下一代，或者下个世纪。

Q: 那么久？

S: 不。我在开玩笑，但是，是的，\(\omega_\alpha\)，也许一个明智的人会尝试那个。

Q: 但你仍然认为答案是肯定的吗？

S: 我倾向于这么认为，我的意思是，我没有充分的理由。我猜这就是我希望它成为的样子。

Q: 与你过去对其他问题的直觉一致吗？

S: 不。我对这个问题的直觉不值一提。只是，论证必须很有趣，对吧？如果有人能做到，那对集合论者来说几乎也会很有趣。我的意思是，可能需要对细结构有一种新的洞察。很难相信关于细结构还有什么可说的，但也许还有。我的意思是，在詹森出现之前，我没觉得关于它有什么新可说的，对吧？所以他纠正了这一点。也许还有更多。我猜，有些专家会说不，我们对细结构了如指掌。嗯，也许不是。很难看出。我曾详细讨论过 L 的细结构的每个人似乎都有一个略有不同的直观图景。我的意思是，(梅纳赫姆) 马吉多尔谈论细结构的方式，或者西·弗里德曼的方式，或者詹森的方式，都各不相同。马吉多尔直观得多，然后他就轻描淡写地带过了 J-层级。你可以相当粗略，相当直观，只要你足够用力推，它就能奏效。但当然，詹森的表述非常优美。他伟大的洞察是，存在这些主码，它们不仅仅是神谕，而且会被压缩论证所保留。现在我从未需要过那个。也许它在 \(\alpha\)-递归理论中有发挥作用的空间。我认为西·弗里德曼在不可接受的情况下使用过它。但我很久没有看过了。它似乎在可接受的情况下不会出现。也许我错了。

Q: 那么，展望未来，你希望看到递归理论如何发展？

S: 嗯，多年来我一直倾向于预测递归理论即将终结（笑声）。但我每次都错了……

Q: 你说的“终结”是指人们对这个主题失去兴趣？

S: 是的。你知道他们都停止研究它了。但这还没有发生。整个随机性现象对我来说是个大惊喜。我的意思是，这些概念已经存在很长时间了。

Q: 你甚至在你的书《高阶递归理论》里提到过，隐藏在各处的页面中。

S: 真的吗？我提到过随机性？

Q: 是的，在一些习题中。

S: 但那只是非常弱的使用。现在人们在随机性研究上变得非常微妙。有大量的活动和堆积如山的论文。我也以为强迫法到现在应该结束了，但仍然有人在做非常复杂的、高度组合性质的强迫论证。我以为集合论差不多已经消亡了，但有 AD 人士，由休·伍德因领导。我认为从某种意义上说，他正变得越来越孤立。越来越少的人知道他在做什么。

Q: 越来越难以理解。

S: 他走得越来越远。材料的数量，我看不出一个学生如何能去研究生院并希望在那个领域写博士论文。

Q: 对于该领域的学生来说，毕业时有出版物以找到学术工作也会很有挑战性。

S: 嗯，这可能不是培养那么多学术数学家的好理由。我认为世界需要更多数学家，但他们不必都是教授。他们不必都有学术职位。他们可以去其他地方工作……

我们必须试图让数学家渗透到世界各行各业。那些习惯于像数学家那样思考的人。我认为这样的人短缺。我不认为“应用数学”这个短语是对的，但他们可以在工作中简单地使用数学思维或数学方法。可以是分子生物学，也可以是法律领域。我认为数学方法非常强大。哥德尔当然这么认为。哥德尔当然认为这是处理几乎任何问题的方法。

Q: 你能谈谈哥德尔吗？你第一次见他是什么时候？
S: 我想是在 61 年秋天见他的。换句话说，我访问该研究所是在他的赞助下进行的。必须申请，尽管有国家科学基金会提供资金，他们必须接受你作为临时成员。显然这取决于他（哥德尔）。

Q: 所以他是你在研究所的东道主？
S: 是的，但当然，我害怕他，从未主动找过他，基本上从未和他说过话。但在研究所的另一年——我想是 1974/75 年——我们有很多联系，也许我们每月见一次面。

Q: 那时他还对数学感兴趣吗？
S: 是的。我记得有一天我问他他认为逻辑学中的突出问题是什么，他当面给了我一个简短的清单。其中之一就是 P ≠ NP 问题。

Q: 他知道那个问题吗？
S: 是的，他是最早引起人们关注那个问题的人之一，如果不是第一个的话。他在冯·诺依曼临终前给他写了一封信，并得到了回复。冯·诺依曼大致说，这是一个非常有趣的问题，我以后有空想一想。（笑声）

我想，这封信的往来是马丁·戴维斯给我看的。那是很久以前的事了。冯·诺依曼在 50 年代去世了。另一个并非完全没有希望的问题是分析的一致性——证明分析的一致性。有很多种解释方式。所以你可以试图找到一个能做到这一点的序数。这个序数与分析的关系，就像 ε₀ 与形式数论的关系一样。那个序数是什么？还有人……嗯，我遇过一个人，他认为这是可行的，米夏埃尔·拉特耶。但他也似乎认为追求它可能是疯狂的，因为它太复杂了。换句话说，这个序数的描述会长达书籍篇幅。但有可能给出一个相当清晰的那个序数的描述，然后证明它是正确的。

哥德尔还有一个问题：看，现在称为可计算函数的东西——他称它们为一般递归函数，全函数——有一种直觉认为这个比那个更复杂。找到相应的正式概念。

Q: 不是从可定义性的角度吗？
S: 不。找到可计算函数复杂性的真正层次。当然，没有人做到过，而且我认为很多人认为这是可以做到的。在他看来，人们轻易地说这个比那个更复杂，所以有证据表明直观概念是存在的。如果存在，那么必然有



a formal concept that captures that intuitive concept. That's how his mind worked. It might also be a little complicated. (laughter)

Q: What about set theory? Did he have any comments on set theory?

S: I don't recall. I mean, I tried to get him interested in AD, but he wouldn't listen. I understood his objections to AD, but I thought I could say something that he might find of interest. But he would not tolerate.

Q: Not even Projective Determinacy?

S: I tried to work up from there, say Borel, since for Borel it's true. I mean, I had a pep talk prepared. He said AD is obviously false; for it falsifies the Axiom of Choice which is obviously true. He even made a nasty remark which is unusual for him. He said: I suppose something is interesting in seeing what a man can do with one hand tied behind his back. I mean, that was how the study of AD was to him. I think he was hasty there. I think there is something to talk about even if you believe AD is false, because it might be true in a very restricted setting. It might be true in L(R) or it may be true for the projective sets, or something. I mean, there is something fruitful there, you are not wasting your time even if AD is false, even if AD is dramatically false. There is something going on there.

Q: But he never believed that V = L, right? I guess he only saw L as a tool.

S: Oh, I teased him about that. I teased him because if you go back far enough, he thought V = L might be true; and it might be the completion of ZF – this completed it and in other words, it settled every reasonable problem in set theory and so on. Then some time passed, he seemed to say that Continuum Hypothesis was false. It's just definitely false. He said so in a paper.

So he tried to settle the matter. He tried to find the right cardinal. He seemed to think it's $\aleph_2$, because he spent lots of time trying to show that the continuum was $\aleph_2$, and he even developed some false proofs. But what he was calling a proof was not from ZF. He knew ZF couldn't do it. So he tried to write down some axioms about the real numbers, just true statements about real numbers which he found intuitively appealing, and these kept changing over time. But every once in a while he would use that trying to prove the continuum was $\aleph_2$, and he would succeed. Then he would find a mistake. So then more time passed. Now it's near the end of his life. Now he told me he thought the continuum was $\aleph_1$.

I said – I was teasing him and said – I thought you've said it's equal to $\aleph_2$. So he looked at me and said, I misspoke. (laughter). Apparently the people that told him all those examples, weird examples that you derive from Continuum Hypothesis misled him. So in the end, he tried to prove it with new axioms that were plausible. So for most of his life he is working on $\aleph_2$.

Q: Thank you very much for spending time here.

S: Oh, I enjoyed the conversation very much. Thanks for your patience.

## C 符号和记号

- A real x is a member of \(2^\omega\) or \(\omega^\omega\). A string is a member of either \(2^{<\omega}\) or \(\omega^{<\omega}\). Strings are denoted \(\sigma, \tau\) etc.
- If x is a real, then \(x \restriction n\) is a finite string \(\sigma\) of length \(n\) such that for all \(i < n\), \(\sigma(i) = x(i)$.
- If \(\sigma\) is a finite string, then \(|\sigma|\) is its length.
- \(x > \sigma\) means \(x \restriction \sigma = \sigma\).
- \([\sigma] = \{x \mid x \in \omega^\omega \land x > \sigma\}\).
- If f is a function, then Dom(f) denotes the domain of f, and Rang(f) its range. Dom(\(\sigma\)) and Rang(\(\sigma\)) carry the obvious meaning where \(\sigma\) is considered as a finite function.
- If T is a tree, then \([T] = \{x \mid x \in \omega^\omega \land (\forall n)(x \restriction n \in T)\}\).
- Given a set A, \(\mathscr{P}(A) = \{B \mid B \subseteq A\}\) is the power set of A.
- \(\le_T\) denotes Turing reduction.
- \(x'\) is the Turing jump of x.
- \(x \oplus y\) is the real z such that \(z(2n) = x(n)\) and \(z(2n + 1) = y(n)\).
- \((\cdot, \cdot)\) is a recursion bijection from \(\omega^2\) to \(\omega\).
- For any n and \(x \in 2^\omega\), \(x^{[n]} = \{m \mid \langle n, m \rangle \in x\}\).
- If A is a set, then \(\mathscr{P}(A)\) denotes the power set of A.
- \(A \subseteq 2^\omega\) or \(\omega^\omega\) is \(\Pi^0_1\) or \(\Pi^0_1\) (resp. \(\Sigma^0_1\) or \(\Sigma^0_1\)) if it is \(\Pi^0_1\) or \(\Pi^0_1\) (resp. \(\Sigma^0_1\) or \(\Sigma^0_1\)) definable with real number parameters.
- Given a partial ordering \((\mathbf{P}, \le)\), \(p \perp q\) means p and q are incomparable, i.e. \(p \nleq q\) and \(q \nleq p\).

## 参考文献

- [1] J. W. Addison, 经典与有效描述集论层次中的分离原理, Fund. Math. 46 (1959), 123–135.
- [2] T. Bartoszynski 和 H. Judah, 集合论：实线的结构, AK Peters Ltd., Wellesley, MA, 1995.
- [3] J. Barwise, 可容纳集与结构, Springer-Verlag, Berlin, 1975.
- [4] J. Barwise, 数理逻辑手册。H. J. Keisler, K. Kunen, Y. N. Moschovakis, A. S. Troelstra 合作。第2次印刷。逻辑与数学基础研究，第90卷，阿姆斯特丹，纽约，牛津：北荷兰出版公司，XI, 1978.
- [5] J. E. Baumgartner, Sacks强迫与Martin公理的彻底失败, Topology Appl. 19 (1985), 211–225.
- [6] J. E. Baumgartner 和 R. Laver, 迭代完备集强迫, Ann. Math. Logic 17 (1979), 271–288.
- [7] A. Blass, 获胜策略的复杂性, Discrete Math. 3 (1972), 295–300.
- [8] G. Boolos 和 H. Putnam, 可构整数集的不可解度, J. Symbolic Logic 33 (1968), 497–513.
- [9] G. J. Chaitin, 与信息论形式上相同的程序大小理论, J. Assoc. Comput. Mach. 22 (1975), 329–340.
- [10] G. J. Chaitin, 递归无穷串的信息论特征, Theoret. Comput. Sci. 2 (1976), 45–48.
- [11] C. T. Chong, 可构实数的递归论特征, Bull. London Math. Soc. 9 (1977), 241–244.
- [12] C. T. Chong 和 A. Nies, 高阶随机性概念的下属性, Israel J. Math. 166 (2008), 39–60.
- [13] C. T. Chong, W. Wang 和 L. Yu, 投影Martin猜想的强度, Fund. Math. 207 (2010), 21–27.
- [14] C. T. Chong 和 L. Yu, 高阶环境中的随机性, 即将发表.
- [15] C. T. Chong 和 L. Yu, 图灵度中的极大链, J. Symbolic Logic 72 (2007), 1219–1227.
- [16] C. T. Chong 和 L. Yu, 图灵度中的极大反链, 现实世界中的计算与逻辑, Lecture Notes in Comput. Sci. 4497, 第162–168页, Springer, Berlin, 2007.
- [17] C. T. Chong 和 L. Yu, 实数的\(\Pi^1_1$一致化原理, Trans. Amer. Math. Soc. 361 (2009), 4233–4245.
- [18] P. J. Cohen, 集合论与连续统假设, W. A. Benjamin, Inc., New York-Amsterdam, 1966.
- [19] K. de Leeuw, E. F. Moore, C. E. Shannon 和 N. Shapiro, 概率机器的可计算性, 自动机研究, 数学研究丛书，第34号，第183–212页, Princeton University Press, Princeton, N. J., 1956.
- [20] O. Demuth, 基于可构度论的tt-度结构评论, Comment. Math. Univ. Carolin. 29 (1988), 233–247.
- [21] K. J. Devlin 和 R. B. Jensen, Silver定理的边注, ISILC逻辑会议（国际暑期学院与逻辑讨论会论文集，基尔，1974），第115–142页, Springer, Berlin, 1975. Lecture Notes in Math., 第499卷.
- [22] K. J. Devlin, 可构性, 数理逻辑视角, Springer-Verlag, Berlin, 1984.
- [23] R. Downey, A. Nies, R. Weber 和 L. Yu. 下属性与\(\Pi^0_2$零集, J. Symbolic Logic 71 (2006), 1044–1052.
- [24] R. G. Downey 和 D. R. Hirschfeldt, 算法随机性与复杂性, 可计算性理论与应用, Springer, New York, 2010.
- [25] S. Feferman, 强迫与泛化集概念的一些应用, Fund. Math. 56 (1964/1965), 325–345.
- [26] S. Feferman 和 C. Spector, 理论序列路径上的不完备性, J. Symbolic Logic 27 (1962), 383–390.
- [27] J. N. Y. Franklin, F. Stephan 和 L. Yu, 随机性与泛化性概念的相对化, Bull. Lond. Math. Soc. 43 (2011), 721–733.
- [28] R. M. Friedberg, 两个不可比不可解度的递归可枚举集（Post问题的解，1944）, Proc. Nat. Acad. Sci. U.S.A. 43 (1957), 236–238.
- [29] H. Friedman, 数理逻辑中的一百零二个问题, J. Symbolic Logic 40 (1975), 113–129.
- [30] H. Friedman, 一致定义的度的降序列, J. Symbolic Logic 41 (1976), 363–367.
- [31] H. M. Friedman 和 R. Jensen, 关于可容纳序数的注记, Lecture Notes in Mathematics 72 (1968), 77–79.
- [32] H. Gaifman, 集合论模型及其某些子理论的初等嵌入, 公理化集合论（纯数学讨论会论文集，第XIII卷，第一部分，加州大学洛杉矶分校，1967）, Amer. Math. Soc., Providence, R.I., 1974, 第33–101页.
- [33] R. O. Gandy, 关于Kleene的一个问题, Bull. Amer. Math. Soc. 66 (1960), 501–502.
- [34] R. O. Gandy, Mostowski猜想的证明, Bull. Acad. Polon. Sci. Sér. Sci. Math. Astronom. Phys. 8 (1960), 571–575.
- [35] R. O. Gandy, G. Kreisel 和 W. W. Tait, 集合存在性。II, Bull. Acad. Polon. Sci. Sér. Sci. Math. Astronom. Phys. 9 (1961), 881–882.
- [36] R. O. Gandy 和 G. E. Sacks, 一个极小超度, Fund. Math. 61 (1967), 215–223.
- [37] K. Gödel, 连续统假设的相容性, 数学研究丛书，第3号, Princeton University Press, Princeton, N.J., 1940.
- [38] N. Greenberg 和 J. S. Miller, Kurtz随机性的下属性, J. Symbolic Logic 74 (2009), 665–678.
- [39] N. Greenberg, A. Montalbán 和 T. A. Slaman, 高阶递归论中的Slaman–Wehner定理, Proc. Amer. Math. Soc. 139 (2011), 1865–1869.
- [40] M. J. Groszek 和 T. A. Slaman, 图灵度全局结构上的独立性结果, Trans. Amer. Math. Soc. 277 (1983), 579–588.
- [41] M. J. Groszek 和 T. A. Slaman, 完备集的基定理, Bull. Symbolic Logic 4 (1998), 204–209.
- [42] D. Guspari, 关于Kondo–Addison定理的注记, J. Symbolic Logic 39 (1974), 567–570.
- [43] L. A. Harrington, McLaughlin猜想, 手册笔记 (1976).
- [44] L. A. Harrington, 长投影良序, Annals of Mathematical Logic 12 (1977), 1–24.
- [45] L. A. Harrington, 分析确定性与\(0^\sharp\), J. Symbolic Logic 43 (1978), 685–693.
- [46] L. A. Harrington 和 A. S. Kechris, 实数\(\Sigma^1_1$集的基结果及其在极小覆盖中的应用, Proc. Amer. Math. Soc. 53 (1975), 445–448.
- [47] P. G. Hinman, 递归论层次, 数理逻辑视角, Springer-Verlag, Berlin, 1978.
- [48] D. R. Hirschfeldt, A. Nies 和 F. Stephan, 将随机集用作神谕, J. Lond. Math. Soc. (2) 75 (2007), 610–622.
- [49] G. Hjorth, 解析补集的连续像, 逻辑讨论会'98（布拉格）, Lecture Notes in Logic 13, Assoc. Symbol. Logic, Urbana, IL, 2000, 226–237.




- [50] G. Hjorth, 归功于 Leo Harrington 的一个论证, 在线草稿 (2004).

- [51] G. Hjorth 和 A. Nies, 通过有效描述集论的随机性, J. Lond. Math. Soc. (2) 75 (2007), 495–508.

- [52] W. Hodges, 模型论, 数学及其应用百科全书 42, Cambridge University Press, Cambridge, 1993.

- [53] T. Jech, 集合论, Springer Monographs in Mathematics, Springer-Verlag, Berlin, 2003.

- [54] R. B. Jensen, 可容纳集, 在线草稿 (1969).

- [55] R. B. Jensen, 可构造层次的精细结构, Ann. Math. Logic 4 (1972), 229–308; 勘误, 同上 4 (1972), 443.

- [56] C. G. Jockusch, Jr., Kleene's O 的初始段的递归性, Fund. Math. 87 (1975), 161–167.

- [57] C. G. Jockusch, Jr. 和 R. A. Shore, 伪跳算子. II. 超限迭代、层次和最小覆盖, J. Symbolic Logic 49 (1984), 1205–1236.

- [58] C. G. Jockusch, Jr. 和 S. G. Simpson, 分析分支层次的度理论定义, Ann. Math. Logic 10 (1976), 1–32.

- [59] C. G. Jockusch, Jr. 和 R. I. Soare, 最小覆盖和算术集, Proc. Amer. Math. Soc. 25 (1970), 856–859.

- [60] C. G. Jockusch, Jr. 和 R. I. Soare, Π⁰₁ 类和理论的度, Trans. Amer. Math. Soc. 173 (1972), 33–56.

- [61] B. Jónsson, 关于格的表示, Math. Scand. 1 (1953), 193–206.

- [62] A. Kanamori 和 D. Pincus, GCH 是否局部蕴含 AC?, Paul Erdős 及其数学, II (Budapest, 1999), Bolyai Soc. Math. Stud., vol. 11, pp. 413–426, János Bolyai Math. Soc., Budapest, 2002.

- [63] A. S. Kechris, 有效描述集论中的测度与范畴, Ann. Math. Logic 5 (1972/73), 337–384.

- [64] A. S. Kechris, 可数解析集理论, Trans. Amer. Math. Soc. 202 (1975), 259–297.

- [65] A. S. Kechris, D. A. Martin 和 R. M. Solovay, Q-理论导论, Cabal Seminar 79–81, Lecture Notes in Math., 1019, pp. 199–282, Springer, Berlin, 1983.

- [66] B. Kjos-Hanssen, J. Miller 和 R. Solomon, 下垂性概念、测度与随机性, J. Lond. Math. Soc. 85 (2012), 869–888.

- [67] B. Kjos-Hanssen, A. Nies 和 F. Stephan, 对 Schnorr 随机实数类的下垂性, Symbol. Comput. 33 (2005), 647–657.

- [68] S. C. Kleene, 关于构造序数理论中的谓词形式 (第二篇), Ann. Math. 43 (1941), 20–120.

- [69] S. C. Kleene, 算术谓词与函数量词, Trans. Amer. Math. Soc. 79 (1955), 312–340.

- [70] S. C. Kleene, 数论谓词的层次, Bull. Amer. Math. Soc. 61 (1955), 193–213.

- [71] S. C. Kleene, 关于构造序数理论中的谓词形式. II, Amer. J. Math. 77 (1955), 405–428.

- [72] S. C. Kleene, 数论函数的量化, Compositio Math. 14 (1959), 23–40.

- [73] A. N. Kolmogorov, 信息量定义的三种方法, Internat. J. Comput. Math. 2 (1968), 157–168.

- [74] M. Kondô, 关于解析补集的一致化与第二类射影集, Japan. J. Math. 15 (1938), 197–230 (法文).

- [75] S. Kripke, 可容纳序数上的超限递归. I, II, J. Symbolic Logic 29 (1964), 161–162.

- [76] A. Kučera, 测度, \(\Pi^0_1\)-类和 PA 的完全扩展, *递归理论周* (Oberwolfach, 1984), Lecture Notes in Math. 1141, pp. 245–259, Springer, Berlin, 1985.

- [77] A. Kučera 和 T. A. Slaman, 理想的低上界, J. Symbolic Logic 74 (2009), 517–534.

- [78] K. Kunen, *集合论：独立性证明导论*, Studies in Logic and the Foundations of Mathematics 102, North-Holland Publishing Co., Amsterdam, 1980.

- [79] S. Kurtz, *不可解度中的随机性与泛性*, 博士论文, University of Illinois, Urbana, 1981.

- [80] A. H. Lachlan, 一致枚举运算, J. Symbolic Logic 40 (1975), 401–409.

- [81] M. Lerman, 不可解度的初始段, Ann. of Math. (2) 93 (1971), 365–389.

- [82] M. Lerman, *不可解度：局部与全局理论*, Perspectives in Mathematical Logic, Springer-Verlag, Berlin, 1983.

- [83] L. A. Levin, 信息守恒（零增加）定律及概率论基础问题, Problemy Peredachi Informacii 10 (1974), 30–35.

- [84] A. Lévy, 公理化集论中的可定义性. I, 逻辑, *方法与科学哲学* (1964 年国际会议论文集), pp. 127–151, North-Holland, Amsterdam, 1965.

- [85] A. Louveau, \(\Sigma^1_1\) 集的分离定理, Trans. Amer. Math. Soc. 260 (1980), 363–378.

- [86] N. Lusin, 关于贝尔先生的分类, C. R. 164 (1917), 91–94 (法文).

- [87] R. Mansfield, 可定义实数集的完美子集, *太平洋数学杂志* 35 (1970), 451–457.

- [88] R. Mansfield 和 G. Weitkamp, *描述集论的递归方面*, Oxford Logic Guides 11, The Clarendon Press Oxford University Press, New York, 1985, 附 Stephen Simpson 撰写的一章.

- [89] W. Markwald, 关于构造良序理论, Math. Ann. 127 (1954), 135–149.

- [90] D. A. Martin 和 R. M. Solovay, 内部 Cohen 扩展, Ann. Math. Logic 2 (1970), 143–178.

- [91] D. A. Martin, 决定性公理及分析层次中的归约原理, Bull. Amer. Math. Soc. 74 (1968), 687–689.

- [92] D. A. Martin, 可测基数与解析博弈, Fund. Math. 66 (1969/1970), 287–291.

- [93] D. A. Martin, Borel 确定性, Ann. of Math. (2) 102 (1975), 363–371.

- [94] D. A. Martin, Friedman 猜想的证明, Proc. Amer. Math. Soc. 55 (1976), 129.

- [95] D. A. Martin 和 J. R. Steel, 射影确定性的证明, J. Amer. Math. Soc. 2 (1989), 71–125.

- [96] P. Martin-Löf, 随机序列的概念, *信息与控制* 9 (1966), 602–619.

- [97] P. Martin-Löf, 关于随机性概念, *直觉主义与证明理论* (会议论文集, Buffalo, N.Y., 1968), pp. 73–78, North-Holland, Amsterdam, 1970.

- [98] A. R. D. Mathias, 超现实景观与图形 (集合论近期结果综述), *匈牙利定期数学杂志* 10 (1979), 109–175.

- [99] W. Merkle, J. S. Miller, A. Nies, J. Reimann 和 F. Stephan, Kolmogorov–Loveland 随机性与随机性, Ann. Pure Appl. Logic 138 (2006), 183–210.

- [100] A. W. Miller, 无穷组合论与可定义性, Ann. Pure Appl. Logic 41 (1989), 179–203.

- [101] J. S. Miller, 每个 2-随机实数都是 Kolmogorov 随机的, J. Symbolic Logic 69 (2004).

- [102] J. S. Miller, \(K\)-度, 对 \(K\)-度的下垂性, 以及对 \(K\) 集的弱下垂性, *圣母大学逻辑杂志* 50 (2009), 381–391 (2010).

- [103] J. S. Miller 和 L. Yu, 关于初始段复杂度与随机度, Trans. Amer. Math. Soc. 360 (2008), 3193–3210.

- [104] J. S. Miller 和 L. Yu, 随机实数初始段复杂度中的振荡, Adv. Math. 226 (2011), 4816–4840.

- [105] B. Monin, 高阶随机性与闭集强迫, 收录于: 第 31 届计算机科学理论方面国际研讨会 (STACS 2014), E. W. Mayr 和 N. Portier 编, Leibniz International Proceedings in Informatics (LIPIcs) 25, pp. 566–577, Schloss Dagstuhl, Leibniz-Zentrum für Informatik, Dagstuhl, Germany, 2014.

- [106] Y. N. Moschovakis, 抽象结构上的基本归纳, Studies in Logic and the Foundations of Mathematics, Vol. 77, North-Holland Publishing Co., Amsterdam, 1974.

- [107] Y. N. Moschovakis, 描述集论, 第二版, Mathematical Surveys and Monographs 155, American Mathematical Society, Providence, RI, 2009.

- [108] A. Motsakis, 一个不可判定的算术陈述, Fund. Math. 36 (1949), 143–164.

- [109] A. A. Muchnik, 关于算法理论中归约问题的不可解性, Dokl. Akad. Nauk SSSR (N.S.) 108 (1956), 194–197.

- [110] A. Nies, 下垂性性质与随机性, Adv. Math. 197 (2005), 274–305.

- [111] A. Nies, 可计算性与随机性, Oxford Logic Guides 51, Oxford University Press, Oxford, 2009.

- [112] A. Nies, F. Stephan 和 S. A. Terwijn, 随机性、相对化与 Turing 度, J. Symbolic Logic 70 (2005), 515–535.

- [113] R. Platek, 递归理论基础, 博士论文, Stanford University, 1966.

- [114] D. B. Posner 和 R. W. Robinson, 与 $0'$ 汇合的度, J. Symbolic Logic 46 (1981), 714–722.

- [115] H. Putnam, 关于可计算整数集的简要说明, Notre Dame J. Formal Logic 4 (1963), 270–273.

- [116] H. Rogers, Jr., 递归函数与有效可计算性理论, McGraw-Hill Book Co., New York, 1967.

- [117] G. E. Sacks, 不可解度, Princeton University Press, Princeton, N.J., 1963.

- [118] G. E. Sacks, Post 问题、可容纳序数与正则性, Trans. Amer. Math. Soc. 124 (1966), 1–23.

- [119] G. E. Sacks, 关于 Lachlan 和 Martin 的一个定理, Proc. Amer. Math. Soc. 18 (1967), 140–141.

- [120] G. E. Sacks, 递归理论与集合论中的测度论一致性, Trans. Amer. Math. Soc. 142 (1969), 381–420.

- [121] G. E. Sacks, 使用完美闭集的强迫, 公理化集合论 (纯数学研讨会论文集, 第 XIII 卷, 第 I 部分, 加州大学洛杉矶分校, 1967), pp. 331–355, Amer. Math. Soc., Providence, R.I., 1971.

- [122] G. E. Sacks, 可数可容纳序数与超度, Adv. Math. 19 (1976), 213–262.

- [123] G. E. Sacks, 高阶递归理论, Perspectives in Mathematical Logic, Springer-Verlag, Berlin, 1990.

- [124] G. E. Sacks, 逻辑论文选, World Scientific Series in 20th Century Mathematics 6, World Scientific Publishing Co., Inc., River Edge, NJ, 1999.

- [125] C.-P. Schnorr, 随机序列定义的统一方法, Math. Systems Theory 5 (1971), 246–258.

- [126] C.-P. Schnorr, 过程复杂度与有效随机检验, J. Comput. System Sci. 7 (1973), 376–388, 第四届年度 ACM 计算理论研讨会 (Detroit, Colo., 1972).

- [127] C.-P. Schnorr, 随机性与概率. 概率论的算法基础, Lecture Notes in Mathematics, Vol. 218, Springer-Verlag, Berlin, 1971.

- [128] S. Shelah, 你能拿走 Solovay 的不可达基数吗?, Israel J. Math. 48 (1984), 1–47.

- [129] J. R. Shoenfield, 前瞻性问题, 数学基础论文集, pp. 132–139, Magnes Press, Hebrew Univ., Jerusalem, 1961.




- [130] J. R. Shoenfield, 非分支强迫, 公理集合论 (纯数学研讨会论文集, 第XIII卷, 第I部分, 加州大学, 洛杉矶, 加利福尼亚州, 1967), 第357–381页, 美国数学学会, 普罗维登斯, 罗得岛州, 1971.

- [131] R. A. Shore, 关于$\alpha$-递归论中的$\forall\exists$-句子, 广义递归论, II (第二届研讨会论文集, 奥斯陆大学, 奥斯陆, 1977), 逻辑与数学基础研究 94, 第331–353页, 北荷兰出版社, 阿姆斯特丹, 1978.

- [132] R. A. Shore, 有限生成编码与度d中的可枚举度, 美国数学学会会议录 84 (1982), 第256–263页.

- [133] R. A. Shore, 超度中的刚性与双可解释性, 无限的计算前景. 第二部分. 所做报告, 新加坡国立大学数学科学研究所讲义丛书 15, 第299–312页, 世界科学出版社, 新泽西州哈肯萨克, 2008.

- [134] R. A. Shore 和 T. A. Slaman, 定义图灵跳跃, 数学研究快报 6 (1999), 第711–722页.

- [135] W. Sierpiński, 关于一类集合, 基础 7 (1925), 第237–243页 (法文).

- [136] W. Sierpiński, 连续统广义假说与选择公理, 数学基础 34 (1947), 第1–5页.

- [137] J. H. Silver, 集合论中模型论的一些应用, 数学逻辑年刊 3 (1971), 第45–110页.

- [138] S. G. Simpson, 最小覆盖与超度, 美国数学学会汇刊 209 (1975), 第45–64页.

- [139] S. G. Simpson, 递归不可解度的一阶理论, 数学年刊 (2) 105 (1977), 第121–139页.

- [140] T. A. Slaman, 关于西尔宾斯基的一个问题, 数学基础 159 (1999), 第153–159页.

- [141] T. A. Slaman, 图灵度与图灵跳跃的全局性质, 无限的计算前景. 第一部分. 教程, 新加坡国立大学数学科学研究所讲义丛书 14, 第83–101页, 世界科学出版社, 新泽西州哈肯萨克, 2008.

- [142] T. A. Slaman 和 J. R. Steel, 度上的可定义函数, Cabal研讨会 81–85, 数学讲义 1333, 第37–55页, 春季出版社, 柏林, 1988.

- [143] T. A. Slaman 和 W. H. Woodin, 图灵度中的可定义性, 伊利诺伊数学杂志 30 (1986), 第320–334页.

- [144] T. A. Slaman 和 W. H. Woodin, 度结构的可定义性, 在线草稿 (2005).

- [145] R. M. Solovay, Gödel的不完备定理, 牛津逻辑指南 19, 克拉伦登出版社·牛津大学出版社, 纽约, 1992.

- [146] R. M. Solovay, 归纳推理的形式理论, 信息与控制 7 (1964), 第1–22页, 第224–254页.

- [147] R. M. Solovay 和 S. Tennenbaum, 迭代科恩扩张与索斯林问题, 数学年刊 (2) 94 (1971), 第201–245页.

- [148] R. M. Solovay, 一个不可构造的$\Delta_1^3$整数集, 美国数学学会汇刊 127 (1967), 第50–75页.

- [149] R. M. Solovay, 关于$\Sigma_1^2$实数集的基数, 数学基础论文集 (纪念库尔特·Gödel研讨会, 哥伦布, 俄亥俄州, 1966), 第58–73页, 春季出版社, 纽约, 1969.

- [150] R. M. Solovay, 一个集合论模型，其中每个实数集都是勒贝格可测的, 数学年刊 (2) 92 (1970), 第1–56页.

- [151] R. M. Solovay, 关于Chaitin工作的论文（或系列论文）草稿, (1975), 未发表笔记, 215页.

- [152] R. M. Solovay, 超算术可编码集, 美国数学学会汇刊 239 (1978), 第99–122页.

- [153] C. Spector, 递归良序, 符号逻辑杂志 20 (1955), 第151–163页.

- [154] C. Spector, 关于递归不可解度, 数学年刊 (2) 64 (1956), 第581–592页.

- [155] C. Spector, 不可比超度的度理论构造, 符号逻辑杂志 23 (1958), 第280–288页.

- [156] C. Spector, 超算术量词, 数学基础 48 (1959/1960), 第313–320页.

- [157] J.R. Steel, 度的下降序列, 符号逻辑杂志 40 (1975), 第59–61页.

- [158] J.R. Steel, 带标记树的强迫, 数学逻辑年刊 15 (1978), 第55–74页.

- [159] J.R. Steel, 跳跃算子的分类, 符号逻辑杂志 47 (1982), 第347–358页.

- [160] F. Stephan 和 L. Yu, 弱1-泛型和Kurtz-随机的下属性, 计算模型的理论与应用, 计算机科学讲义 3959, 第756–764页, 春季出版社, 柏林, 2006.

- [161] J. Stern, 有效描述集论中的一些度论结果, 以色列数学杂志 20 (1975), 第97–110页.

- [162] M. Susslin, 关于不含跨finite数的B可测集的定义, 科学院学报 164 (1917), 第88–91页.

- [163] S.A. Terwijn 和 D. Zambella, 计算随机性与下属性, 符号逻辑杂志 66 (2001), 第1199–1205页.

- [164] F. van Engelen, A. W. Miller 和 J. Steel, 刚性博雷尔集与更佳准序理论, 逻辑与组合论 (阿卡塔, 加利福尼亚州, 1985), 现代数学 65, 第199–222页, 美国数学学会, 普罗维登斯, 罗得岛州, 1987.

- [165] M. van Lambalgen, 随机性的公理化, 符号逻辑杂志 55 (1990), 第1143–1167页.

- [166] B. Velickovic 和 W.H. Woodin, 集合论内模型中实数的复杂度, 纯粹与应用逻辑年刊 92 (1998), 第283–295页.

- [167] W. Wang, 马丁公理与上半格嵌入图灵度, 纯粹与应用逻辑年刊 161 (2010), 第1291–1298页.

- [168] W. Wang, L. Wu 和 L. Yu, 图灵度中的终极最大链, 美国数学学会会议录 142 (2014), 第1391–1398页.

- [169] W. H. Woodin, Posner–Robinson定理的tt版本, 无限的计算前景: 第二部分. 所做报告, 新加坡国立大学数学科学研究所讲义丛书 15, 第355–392页, 世界科学出版社, 新泽西州哈肯萨克, 2008.

- [170] L. Yu, 当van Lambalgen定理失效时, 美国数学学会会议录 135 (2007), 第861–864页.

- [171] L. Yu, 随机性概念的描述集论复杂度, 数学基础 215 (2011), 第239–231页.

- [172] L. Yu, 弗里德曼猜想的新证明, 符号逻辑通报 17 (2011), 第455–461页.

- [173] L. Yu, D. Ding 和 R. Downey, 随机实数的柯尔莫哥罗夫复杂度, 纯粹与应用逻辑年刊 129 (2004), 第163–180页.

## Index

- (x)_n 40
- +_n 14
- 0^+ 120
- << 11
- <^*> 12
- C(a) 217
- Def^4(X) 54
- G^f 5
- H_n 23
- H_n^2 23
- J[A] 55
- K-triviality 219
- K(a) 217
- L[A] 54
- W0_1 9
- [T] 293
- [a] 293
- a^{CK} 11
- R^{CK}(U) 54
- S^f(U) 54
- \Gamma_\infty 147
- O 11
- O^* 37
- O_1^* 37
- O^+ 12
- O^{++} 38
- O_n^* 25
- MA 106
- MA_n 106
- \Omega 218
- \Pi_1^1-inductive principle 151
- \Pi_1^1-random cuppable 268
- \Sigma_n-Skolem function 57
- \Sigma_n(N) 57
- Z_p(HWP) 43
- Z_2^f 40
- + 106
- WF_0 8
- WF_1 8
- W_n 8
- \aleph_1 82
- x_1^2 105
- a^{(\emptyset)} 30
- \equiv_2 50
- H_2^2 27

- \kappa-closed 107
- (.) 293
- \le_C 218
- \le_K 218
- \le_M 127
- \le_T 293
- L(x) 111
- E 79
- \Omega 151
- \mathfrak{A}(\omega_1^k, x) 86
- \mathfrak{A}(a, x) 99
- HF 51
- rk 49
- \mathscr{L}(\omega_1^k, x) 85
- \mathscr{L}(a, x) 99
- \mathscr{P}(A) 293
- BC 40
- BC(HYP) 41
- DNR 215
- -h- 215
- Low(I) 220
- \omega_1^f 12
- \oplus 293
- <_f^L 50
- \Gamma^{MC} 65
- \tau^g 64
- D_n^g 10
- A_n^g 10
- \Pi_n^g 10
- \Sigma_n^g 10
- \varphi(x) 10
- \rho(x | b) 89
- || 11
- |x|_L 12
- |a| 293
- a-generic 139
- g > f 236
- L(r) 109
- o(N) 51
- x > 293
- x >_T 293
- x | a 293
- x^{[n]} 293

- $OD(A)^M$ 113
- HOD(A)^M 113
- HOD^M 113
- Ref(t, p, q) 101
- val(r, G) 105
- KP 46
- OD^M 113
- <_* 37
- \(\rho_2^A\) 59
- \(M^P\) 105

- Absolute 50
  - downward 50
  - upward 50
- Almost disjoint set 115
- Antichain 157
  - antichain of conditions 106
- Axiom
  - \(A_1^1\)-comprehension- 87
  - Martin's 106
- Axiom of determinacy 122

- Base
  - for a cone of \(\Gamma\)-randomness 247
- Base for P 33
- Base for randomness 221

- Canonical \(\Sigma_1\)-Skolem function 58
- Cardinal
  - inaccessible 118
  - measurable 119
  - weakly inaccessible 118
- Chain 154
  - cofinal 172
- Chain condition
  - ccc 106
- Code
  - hyperarithmetic 41
  - Borel 40
- Condition 105

- Definable
  - \(\mathcal{J}\)-uniformly 50
- Definable \(\Gamma\) 49
- Dense embedding 109
- Dominance
  - recursive 215

- Elementarily equivalent 50
  - \(\Sigma\) 50
- Elementary embedding
  - \(\Sigma\) 50
- Elementary extension 50
  - \(\mathcal{T}\) 50
- Elementary substructure 50
  - \(\mathcal{T}\) 50
- Equicontinuence 119

- Filter 105
  - \(\eta\)-complete 119
  - nonprincipal 119
- Forcing
  - Almost disjoint 115
  - clumpy 241
  - Cohen 109
  - iterated 108
  - Lévy collapsing 111
  - product 107
  - random 110
  - Sacks 112
  - Sacks (over ramified analytic hierarchy) 93
  - Steel 100
- Formula
  - \(\Delta_0\) 45
  - \(\Delta_n\) 45
  - \(\Pi\) 45
  - \(\Pi_n\) 45
  - \(\Sigma\) 45
  - \(\Sigma_n\) 45
  - ranked 85
- Function
  - degree invariant 127
  - increasing on an upper cone 127
  - monotonic 147
  - order preserving 142
  - pressdown 142
  - progressive 147
  - uniformly degree invariant 131

- Gandy topology 8
- Gödel number 64
- Gödel primitively recursive operators 54
- Graph 5
- Homogeneity
  - \(\sim \omega\) 177
- Hyperjump 31





- 克莱尼-布劳威尔序 \(\le_{KB}\) 8
- 局部可数偏序 165
- 低度 220
- 主代码
  - \(\Sigma^0_1\) 60
- 最小覆盖 154
- 模型
  - \(\omega\) 62
  - 对 \(\omega\) 的良好编码 67
- 名称 105
- 范数 71
- 序数
  - 构造的 11
  - 递归的 16
- 序数可定义 113
  - 遗传的 113
- 普通 Kolmogorov 复杂度 217
- 谓词
  - \(\neg A^0_1\) 3
  - \(\neg A_1\) 4
  - \(\neg \Pi^0_2\) 3
  - \(\neg \Pi^0_1\) 4
  - \(\neg \Sigma^0_1\) 3
  - \(\neg \Sigma^1_1\) 4
  - 解析的 4
  - 算术的 3
  - 偏递归的 3
  - 递归的 3
- 前缀-free Kolmogorov 复杂度 217
- 前缀-free 机器 217
- 投影
  - \(\Sigma_n\) 59
- 性质 (K) 108
- 随机实数 110
- 随机性
  - L- 260
  - F- 248
  - T-Kurtz 245
  - F-ML 249
  - n- 214
  - Kurtz 213
  - Martin-Löf 213
  - Schnorr 213
  - Strong F-ML 252
  - Strong Martin-Löf 214
- 阶 49
- 实数
  - \(\Delta^1_1\)-支配的 236
  - \(\Delta^1_1\)-可追踪的 237
  - \(\Pi^0_1\)-可追踪的 237
  - Cohen-泛的 90
  - 超算术的 23
  - 半-\(\Delta^1_1\)-可追踪的 239
  - 半-\(\Pi^0_1\)-可追踪的 239
- 递归语言 64
- 递归结构 65
- 递归理论 64
- 可递归枚举 (r.e.) 9
- 可递归追踪的 220
- 归约
  - \(\le_T\) 31
  - \(\le_{sA_1}\) 31
- 关系
  - 共终进的 150
- 集合
  - E-闭的 62
  - H- 23
  - X-可定义的 54
  - \(\Delta^0_n\) 4
  - \(\Pi^0_n\) 4
  - \(\Pi^1_1\) 5
  - \(\Sigma^0_n\) 4
  - \(\Sigma^1_1\) 5
  - H* 27
  - 可容纳的 51
  - 终沓的 126
  - 可构造的 54
  - 稠密的 105
  - 外延的 49
  - Friedman 161
  - 泛的 105
  - 遗传有限的 51
  - 归纳可定义的 147
  - 完美的 6
  - 指向的 126
  - 前缀-free 217
  - 投影的 10
  - 稀疏的 79
  - 传递的 49
  - 一致指向的 126
- Shoenfield 绝对性 79
- 单子
  - \(\Gamma^-\): 24
  - 标准部分 62
- 测试
  - 广义 Martin-Löf 214
  - Kurtz 213
  - Martin-Löf 213
  - Schnorr 213
  - 定理
    - Gandy 基 34
    - Kreisel 基 35
    - Spector-Gandy 69
    - van-Lambalgen 214
    - 图灵确定性 127
    - \(\Gamma^-\): 127
- 极滤子 119
- 一致化 77
- 上半格 170
- 0锐 120

## 德古依特 逻辑及其应用丛书

第 7 卷
伊塔伊·尼曼
长博弈的确定性，2008
ISBN 978-3-11-018341-2, e-ISBN 978-3-11-020006-5, Set-ISBN 978-3-11-916429-0

第 6 卷
戈德哈德·林克 (编)
罗素悖论一百年，2008
ISBN 978-3-11-017438-0, e-ISBN 978-3-11-019968-0, Set-ISBN 978-3-11-916554-9

第 5 卷
马丁·泽曼
内模型与大基数，2011
ISBN 978-3-11-016368-1, e-ISBN 978-3-11-085781-8, Set-ISBN 978-3-11-179317-7

第 4 卷
罗德·道尼，丹尼斯·R·赫希费尔特 (编)
复杂性的各方面，2011
ISBN 978-3-11-016810-5, e-ISBN 978-3-11-088917-8, Set-ISBN 978-3-11-180439-2

第 3 卷
S. D. 弗里德曼
精细结构与类强迫，2011
ISBN 978-3-11-016777-1, e-ISBN 978-3-11-080911-4, Set-ISBN 978-3-11-174922-8

第 2 卷
马拉特·N·阿斯拉诺夫，斯蒂芬·莱普
递归理论与复杂性，2014
ISBN 978-3-11-016587-6, e-ISBN 978-3-11-080748-6, Set-ISBN 978-3-11-175948-7

