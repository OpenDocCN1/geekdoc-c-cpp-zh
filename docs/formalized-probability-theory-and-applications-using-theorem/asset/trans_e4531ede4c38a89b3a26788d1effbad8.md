

返回一个数字列表。解码器执行逆运算，将数字列表转换回字符串。函数 encode 和 decode 具有以下 HOL4 类型：

```
|- encode: string -> num list
|- decode: num list -> string
```

### 11.3.2 加密-解密

加密和解密块被形式化为两个函数 encrypt 和 decrypt，输入为一对相同长度的数字列表，返回一个数字列表。

```
|- encrypt: (num list, num list) -> num list
|- decrypt: (num list, num list) -> num list
```

加密通过对表示编码消息的列表和表示一次性密钥的数字列表进行逐位模10加法来执行。此操作的结果是密文，也由数字列表表示。在接收端，密文通过从密文中减去密钥（模10）来解密，得到表示原始消息的数字列表。如果明文被编码为比特而不是数字，则加密和解密都通过简单的异或操作执行。我们在高阶逻辑中递归形式化 encrypt。h1 和 h2 分别表示列表 l1 和 l2 的首元素（头部）及其尾部。:: 运算符是列表构造器。

```
|- encrypt ([] , []) = [] /\ ∀ t1 t2 h1 h2.
encrypt (h1:: t1, h2:: t2) =
(h1 + h2) MOD 10:: encrypt (t1, t2)
```

同样，我们如下形式化解密块。

```
|- decrypt ([] , []) = [] /\ ∀ t1 t2 h1 h2.
decrypt (h1:: t1, h2:: t2) =
(h1 - h2) MOD 10:: decrypt (t1, t2)
```

最后，设 m 为原始消息（明文），k 为一次性密钥，r 为解密和解码后接收到的消息。然后在 HOL4 中使用以下谓词形式化一次性密钥（OTP）加密。

```
|- ∀ m k r.
   OTP m k r <=>
   r = decode (decrypt (encrypt (encode m, k), k))
```

作为一项令人放心的属性，我们在 HOL4 中证明，如上设计和形式化的一次性密钥确保接收到的消息等于原始消息。

```
|- ∀ m k r. OTP m k r => (r = m)
```

### 11.3.3 完美安全性

我们通过证明在第4章第4.3节中形式化的信息泄露度等于1，来正式验证一次性密钥提供完美安全性。设 M、C 和 K 分别表示表示明文、密文和密钥的随机变量。因此，K 服从均匀分布且与 M 独立，这使我们能够证明

```
|- ∀ m ∈ M, c ∈ C.
   P (M = m | C = c) = P (M = m)
```

这源自以下引理，我们使用在第4章中关于概率分布的形式化证明的属性来证明它们。

- |- P (M = m | C = c) = P (M = m, C = c) / P (C = c)
- |- P (M = m, C = c) = P (M = m, K = m ⊕ c)
- |- P (M = m, K = m ⊕ c) = P (M = m) P (K = m ⊕ c)
- |- P (K = m ⊕ c) = 2^-n
- |- P (C = c) = 2^-n

接下来，我们证明在给定 C 的条件下 M 的条件熵等于 M 的熵，并且互信息 I(M; C) 等于零。

- |- H (M | C) = H (M)
- |- I (M; C) = 0

最后，由此可得出信息泄露度等于1，这意味着一次性密钥加密在信息论上是安全的，不会向潜在的窃听者泄露关于秘密输入（明文）的任何信息。

```
H D (M, C) = 1
```

在本应用中，得益于第4章第4.1节中介绍的各种概率分布属性以及同一章第4.2节中的香农熵和互信息属性，我们能够正式证明OTP加密系统的完美安全性属性。定理证明允许提供一个不依赖于加密了哪条消息的通用结果，这与计算机模拟产生的结果不同。事实上，模拟可用于检测错误的存在，但不能保证没有错误。OTP不同组件的形式化及其安全性属性的证明大约需要两周的人力工作和约800行代码。

### 11.4 结论

在本章中，我们验证了概率论的一些经典结果，即切比雪夫不等式和马可夫不等式以及大数定律的弱形式。我们使用这些结果来正式验证渐近等分配属性，这是许多信息论定理证明中使用的重要属性。我们使用AEP来验证香农源编码定理形式证明中使用的典型编码器的属性。我们还展示了在定理证明器内使用定量分析的两个示例应用，以分析基于匿名性的MIX信道的属性以及一次性密钥加密的属性。在第一个示例中，我们能够检测到一个问题，并针对Zhu和Bettati在一篇重要论文中报告的结果提出了一个反例。在第二个示例中，我们能够形式化加密系统，验证其功能，并证明其完美安全性的通用结果。定理证明器的可靠性和演绎风格保证了在推导这些证明时分析的有效性。此外，这种分析的结果是通用的，对系统的任何实例都有效。我们认为，在处理当今并行和分布式系统所涉及的更大、更复杂的系统时，这些好处更加重要。这些应用说明了我们对信息论及其不同底层理论（测度、勒贝格积分和概率）的形式化如何用于推理大量工程应用。在定理证明器的可靠内核内进行分析有助于增加对已证明结果的信任。它使我们能够检测到MIX信道示例中纸笔分析中的一个错误。

## 参考文献

- Affeldt, R., & Hagiwara, M. (2012). Formalization of Shannon's theorems in SSReflect-Coq. In I. T. Proving (Ed.), LNCS (Vol. 7406, pp. 233–249). Springer. doi:10.1007/978-3-642-32347-8_16
- Chaum, D. L. (1981). Untraceable electronic mail, return addresses, and digital pseudonyms. Communications of the ACM, 24(2), 84–90. doi:10.1145/358549.358563
- Cover, T. M., & Thomas, J. A. (1991). Elements of information theory. Wiley-Interscience. doi:10.1002/0471200611
- Gallager, R. G. (1968). Information theory and reliable communication. John Wiley & Sons, Inc.
- Gray, R. M. (1990). Entropy and information theory. Springer-Verlag. doi:10.1007/978-1-4757-3982-4
- Reiter, M. K., & Rubin, A.D. (1998). Crowds: Anonymity for web transactions. ACM Transactions on Information Systems Security, 1(1), 66–92.
- Syverson, P. F., & Goldschlag, D. M. (1997). Anonymous connections and onion routing. In Proceedings of Symposium on Security and Privacy (pp. 44–54). IEEE Computer Society.
- Zhu, Y., & Bettati, R. (2009). Information leakage as a model for quality of anonymity networks. IEEE Transactions on Parallel and Distributed Systems, 20(4), 540–552. doi:10.1109/TPDS.2008.100

## 关键术语和定义

**渐近等分配属性：** 渐近等分配属性（AEP）是典型集概念背后的基础属性，使我们能够获取随机过程的输出样本。

**数据压缩：** 数据压缩涉及使用比原始表示更少的位来编码信息。数据压缩可能会导致数据丢失，也可能不会。

**伪随机数生成和典型集：** 如果伪随机数的输出序列按某些统计标准位于典型集之外，则会因随机性不足而被拒绝。

## 第12章
可靠性理论

## 摘要

在本章中，描述了可靠性理论的一些基本概念，即累积分布函数、生存函数和风险函数，以及可靠性框图，并介绍了它们的高阶逻辑形式化。使用HOL4定理证明器正式验证了这些可靠性概念的一些重要属性，以便推理工程系统的可靠性。

