
该函数的操作如下：

- 第99行调用实用函数 `checkKey`（定义在第160–170行），以确保密钥仅包含字母。
- 第101行定义字符串 `plaintext`，它将存储未加密的文本。
- 第102行定义 `size_t keyIndex`，它将跟踪密钥中的当前字符。该字符用于选择维吉尼亚方阵（Vigenère square）的一行。
- 对于 `plaintext` 中的每个字符，第104–147行要么解密该字母并将其添加到 `plaintext`，要么如果该字符不是字母，则直接将其添加到 `plaintext`。
- 第107行判断原字符是否为小写，以便我们在生成明文时保持该大小写。
- 第111–112行将当前字符转换为大写。如果它已经是大写或不是字母，`std::toupper` 会返回原字符。我们将 `std::toupper` 的结果（一个 `int`）转换为 `char`，并将其放入 `currentChar`。
- 如果 `currentChar` 是字母（第115行），则第119–142行对其进行解密。
- 第119行将 `keyIndex` 处的密钥字母转换为大写，然后减去 'A'，得到一个 0–25 的值，表示要选择的维吉尼亚方阵行。
- 第123行将 `keyIndex` 递增到密钥中的下一个位置；如果已到达密钥末尾，则将其重置为0。
- 第126–138行对一个字符执行维吉尼亚密码解密算法。我们通过遍历当前行来定位与 `currentChar` 匹配的字符的索引（i），从而确定维吉尼亚方阵的列索引。然后，第137–138行将该列索引与 'A' 相加，以确定 `originalChar`。
- 第141–142行随后使用 `currentChar` 的原始大小写将 `originalChar` 追加到 `plaintext`。
- 如果 `currentChar` 不是字母，第145行会直接将其追加到 `plaintext`。

### 私有数据和实用函数 checkKey

第153行定义静态常量 `m_size`，表示维吉尼亚方阵的行数和列数。第156行定义字符的二维数组 `m_square`，构造函数（第16–39行）用维吉尼亚方阵填充它。静态实用函数 `checkKey`（第160–170行）接收一个密钥字符串，并确保它仅包含字母；否则，该函数抛出 `invalid_argument` 异常，因为该密钥不能用于我们的维吉尼亚密码实现。

```cpp
private:
  // number of rows and columns in the Vigenère square
  static constexpr size_t m_size{26};

  // 26-by-26 array of characters to store the Vigenère square
  std::array<std::array<char, m_size>, m_size> m_square;

  // utility function checks that secret key contains only letters;
  // throws an invalid_argument exception if key contains non-letters
  static void checkKey(std::string_view secret) {
    for (size_t i{0}; i < secret.size(); ++i) {
      // if the uppercase version of the character at index i
      // is not a letter throw an invalid_argument exception
      if (std::toupper(secret.at(i)) > 'Z') {
        throw std::invalid_argument(
          "key must contain only letters A-Z or a-z");
      }
    }
  }
};
```

### 秘密密钥密码学的弱点：审视公钥密码学

秘密密钥加密和解密有一个弱点——密文的安全性仅与密钥相当。任何发现或窃取密钥的人都可以解密该密文。**公钥密码学**使用公钥进行加密，而该公钥为每个可能想向特定接收者发送秘密消息的发送者所知。公钥可用于加密消息，但不能解密消息。消息只能使用接收者独知的配对私钥解密，因此它比秘密密钥密码学中的密钥安全得多。最流行的公钥密码学方案之一是 RSA。[41][42]

### 关于密码学与计算能力的说明

理想情况下，密文应当无法被“破解”——也就是说，在没有解密密钥的情况下，不应能够从密文确定明文。由于各种原因，这一目标并不切实际。因此，密码学方案的设计者满足于让它们变得极其难以破解。当今计算能力日益强大的计算机带来的一个问题是，它们使破解过去几十年中使用的大多数加密方案成为可能。

- 41. “RSA（密码系统）。” 访问于2023年4月14日。https://en.wikipedia.org/wiki/RSA_(Cryptosystem).
- 42. “RSA 算法。” 访问于2023年4月14日。https://simple.wikipedia.org/wiki/RSA_Algorithm.

密码学是比特币等加密货币的根基。^43 量子计算将带来的极其强大的计算机正使密码学方案和加密货币面临风险。^44,45 加密货币社区正在努力应对这些挑战。^46,47,48

## 9.23 小结

在本章中，你创建了自己的类，实例化了这些类的对象，并调用这些对象的成员函数来执行有用的操作。你声明了类的数据成员，以维护该类每个对象的数据，并定义了成员函数来操作这些数据。你还学习了如何使用类的构造函数来初始化对象的数据成员。

我们使用 Time 类案例研究介绍了各种附加特性。我们展示了如何将类的接口与其实现分离。你使用箭头运算符通过指向对象的指针访问对象的成员。你看到成员函数具有类作用域——成员函数的名称只对该类的其他成员函数可见，除非类的客户端通过对象名、对类对象的引用、指向类对象的指针或作用域解析运算符来引用它。我们还讨论了访问函数（通常用于获取数据成员的值或测试条件为真还是假）和实用函数（支持类公共成员函数操作的私有成员函数）。

你看到构造函数可以指定默认实参，从而能够以多种方式调用。你还看到，任何可以在没有实参的情况下调用的构造函数都是默认构造函数。我们演示了如何使用委托构造函数在构造函数之间共享代码。我们讨论了析构函数，用于在对象被销毁之前对该对象执行终止清理工作，并演示了对象的构造函数和析构函数的调用顺序。

我们展示了当成员函数返回对私有数据成员的引用或指针时可能出现的问题，这会破坏类的封装。我们还展示了同一类型的对象可以使用默认赋值运算符相互赋值。

你学习了如何指定 const 对象和 const 成员函数以防止修改对象，从而执行最小特权原则。你还了解到

- 43. “加密货币。” 访问于2023年4月14日。https://www.investopedia.com/terms/c/cryptocurrency.asp.
- 44. “量子计算对现有密码学的影响。” 访问于2023年4月14日。https://arxiv.org/pdf/1804.00200.pdf.
- 45. “量子计算及其对密码学的影响。” 访问于2023年4月14日。https://www.cryptomathic.com/news-events/blog/quantum-computing-and-its-impact-on-cryptography.
- 46. “加密货币如何为谷歌的‘量子霸权’做准备？” 访问于2023年4月14日。https://www.coindesk.com/how-should-crypto-prepare-for-googles-quantum-supremacy.
- 47. “这就是为什么量子计算不会破坏加密货币。” 访问于2023年4月14日。https://www.forbes.com/sites/rogerhuang/2020/12/21/heres-why-quantum-computing-will-not-break-cryptocurrencies/.
- 48. “加密世界如何为量子计算做准备，解释如下。” 访问于2023年4月14日。https://cointelegraph.com/explained/how-the-crypto-world-is-preparing-for-quantum-computing-explained.
