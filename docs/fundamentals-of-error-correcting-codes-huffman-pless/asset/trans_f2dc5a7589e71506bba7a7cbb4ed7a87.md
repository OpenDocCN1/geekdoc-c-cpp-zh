

涡轮码涉及前一节介绍并在图 15.12 中总结的两个并行串联码 C1 和 C2。涡轮解码算法实际上使用两个解码器，每个分量码对应一个。假设消息 x = (x(1), x(2), ..., x(m)) 与两个校验向量 c1 = (c1(1), c1(2), ..., c1(m)) 和 c2 = (c2(1), c2(2), ..., c2(m)) 交织后发送。解交织后得到的接收向量 y = (y(1), y(2), ..., y(m))、y1 = (y1(1), y1(2), ..., y1(m)) 和 y2 = (y2(1), y2(2), ..., y2(m)) 是 x、c1 和 c2 的带噪版本。它们的分量来自解调器；例如，如果使用了 8 级量化，则三个接收向量的分量将在 {0, 1, ..., 14} 中。最终，解码器的任务是求出后验概率

prob(x(i) = x | y, y1, y2) for x in {0, 1} and 1 <= i <= m. (15.29)

求出这些值的精确结果会导致一个相当复杂的解码器。Berrou、Glavieux 和 Thitimajshima [20] 发现了一种复杂度低得多的解码器，它通过迭代运算来估计这些概率，从而实现可靠解码。迭代解码从码 C1 开始，使用关于 x 的先验概率、信道统计特性以及接收向量 y 和 y1。第一个解码器将软信息传递给 C2 的解码器，作为第二个解码器的先验概率使用。第二个解码器使用这些关于 x 的先验概率、信道统计特性以及接收向量 y 和 y2 来计算软信息，并将其传回给第一个解码器。从第一个解码器向第二个解码器传递软信息并再传回，构成涡轮解码器的一次迭代；解码器运行多次迭代。“turbo”一词指的是将解码器一部分的信息反馈到另一部分并再返回的过程，以求改进解码，这很像对内燃机进行“turbo-charging”。

我们首先考察解码过程第一次迭代的前半部分。此步骤使用第一个码 C1 和接收向量 y 和 y1，目标是计算

prob(x(i) = x | y, y1) for x in {0, 1} and 1 <= i <= m. (15.30)

从这些概率中，我们可以利用从 y 和 y1 获得的部分信息（忽略 y2 的信息）来获得最可能的消息值。但是

prob(x(i) = x | y, y1) = prob(x(i) = x, y, y1) / prob(y, y1)
= alpha * prob(x(i) = x, y, y1), (15.31)

其中 alpha = 1/prob(y, y1)。alpha 的精确值无关紧要，因为我们只关心 prob(x(i) = 0 | y, y1) 和 prob(x(i) = 1 | y, y1) 哪个更大。这种 alpha 表示法在 [252] 中有更详细的描述，它允许我们删除不影响我们所计算的概率之间相对关系的条件概率；我们在本节中随意使用它。

为了确定 (15.31) 中的概率，对于 x in {0, 1} 和 1 <= i <= m，令 pi_i^(0)(x) = prob(x(i) = x) 为第 i 个消息比特为 x 的先验概率。例如，如果 0 和 1 以相同的概率发送，则 pi_i^(0)(x) = 0.5。对于卷积码，我们看到消息末尾的某些比特始终为 0，以便将编码器送入零态；对于这些比特，pi_i^(0)(0) = 1 且 pi_i^(0)(1) = 0。我们假设信道统计特性 prob(y|c)（例如参见示例 15.2.1）是已知的。使用这些信道统计特性，令 lambda_i(x) = prob(y(i) | x(i) = x)。我们有

prob(x(i) = x, y, y1) = sum_{x(i)=x} prob(x, y, y1)
= sum_{x(i)=x} prob(y, y1 | x) prob(x)
= sum_{x(i)=x} prob(y1 | x) prob(y | x) prob(x). (15.32)

但是，

prob(y | x) prob(x) = prod_{j=1}^m prob(y(j) | x(j)) prob(x(j)) = prod_{j=1}^m lambda_j(x(j)) pi_j^(0)(x(j))

在信道无记忆的假设下。此外，prob(y1 | x) = prob(y1 | c1)，因为 c1 是通过使用 C1 编码直接从 x 确定的。将这些与 (15.30)、(15.31) 和 (15.32) 结合，我们有

prob(x(i) = x | y, y1) = alpha sum_{x(i)=x} prob(y1 | c1) prod_{j=1}^m lambda_j(x(j)) pi_j^(0)(x(j))
= alpha lambda_i(x) pi_i^(0)(x) sum_{x(i)=x} prob(y1 | c1) prod_{j != i}^m lambda_j(x(j)) pi_j^(0)(x(j)). (15.33)

不包括 alpha，(15.33) 是三个项的乘积。第一个是 lambda_i(x)，即系统项，包含从信道统计特性和接收比特 y(i) 得出的关于 x(i) 的信息。第二个是 pi_i^(0)(x)，即仅由第 i 个消息比特确定的先验项。第三个称为外部项，包含从接收校验 y1 得出的关于 x(i) 的信息；我们用以下符号表示该项：

pi_i^(1)(x) = sum_{x(i)=x} prob(y1 | c1) prod_{j != i}^m lambda_j(x(j)) pi_j^(0)(x(j))

请注意，外部信息不包括特定项 lambda_i(x(i)) pi_i^(0)(x(i))，这一现象暗示了消息传递的要求：沿 Tanner 图边传递的消息不能涉及先前沿该边接收到的信息。此外，这种外部信息的和-积形式让人联想到双向 APP 解码算法和和-积解码算法中出现的和-积形式。这种外部信息作为第二个解码器使用的先验概率传递给它。

第二个解码器使用先验概率、信道统计特性以及接收向量 y 和 y2 来执行第一次迭代的后半部分。以与前半部分类似的方式，

prob(x(i) = x | y, y2) = alpha sum_{x:x(i)=x} prob(y2 | c2) prod_{j=1}^m lambda_j(x(j)) pi_j^(1)(x(j))
= alpha lambda_i(x) pi_i^(1)(x) sum_{x:x(i)=x} prob(y2 | c2) prod_{j=1, j != i}^m lambda_j(x(j)) pi_j^(1)(x(j)).

（上述 alpha 的值可能与 (15.31) 中的不同；同样，精确值无关紧要。）来自该解码器的外部信息

pi_i^(2)(x) = sum_{x:x(i)=x} prob(y2 | c2) prod_{j=1, j != i}^m lambda_j(x(j)) pi_j^(1)(x(j))

被传回第一个解码器，作为先验概率以开始第二次迭代的前半部分。

继续以类似方式，第 I 次迭代生成以下概率：

pi_i^(2I-1)(x) = sum_{x:x(i)=x} prob(y1 | c1) prod_{j=1, j != i}^m lambda_j(x(j)) pi_j^(2I-2)(x(j)),
pi_i^(2I)(x) = sum_{x:x(i)=x} prob(y2 | c2) prod_{j=1, j != i}^m lambda_j(x(j)) pi_j^(2I-1)(x(j)).

根据 (15.33) 和类似方程，

prob(x(i) = x | y, y1) = alpha lambda_i(x) pi_i^(2I-2)(x) pi_i^(2I-1)(x),
prob(x(i) = x | y, y2) = alpha lambda_i(x) pi_i^(2I-1)(x) pi_i^(2I)(x),

分别求解 pi_i^(2I-1)(x) 和 pi_i^(2I)(x)，得到

pi_i^(n)(x) = { alpha * prob(x(i) = x | y, y1) / (lambda_i(x) pi_i^(n-1)(x)) if n = 2I - 1,
               alpha * prob(x(i) = x | y, y2) / (lambda_i(x) pi_i^(n-1)(x)) if n = 2I. } (15.34)

（注意 alpha 值与之前不同。）我们最初的目标是计算 (15.29)。事实证明，在 N 次完整迭代后，这可以近似为

alpha lambda_i(x) pi_i^(2N)(x) pi_i^(2N-1)(x).

这导出了涡轮解码算法：

- 1. 直到某个迭代次数 N，计算
  pi_i^(1)(x), pi_i^(2)(x), pi_i^(3)(x), ..., pi_i^(2N)(x)，
  对于 1 <= i <= m 和 x in {0, 1}，使用 (15.34)。

- 2. 对于 1 <= i <= m 和 x in {0, 1}，计算
  gamma_i(x) = alpha lambda_i(x) pi_i^(2N)(x) pi_i^(2N-1)(x).

