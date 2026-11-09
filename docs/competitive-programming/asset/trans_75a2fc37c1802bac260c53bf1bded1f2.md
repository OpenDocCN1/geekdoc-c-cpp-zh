
在本章中，我们已经看到一种相当有效的试除法，用于寻找整数的质因数。为了更快的**整数分解**，可以使用 **Pollard’s rho** 算法 [4]。然而，如果要分解的整数是一个大质数，那么这仍然是一件缓慢的事情。这一事实正是现代密码学技术中的安全性所在。

关于质数还有其他定理、假设和猜想，例如 Carmichael 函数、黎曼假设、哥德巴赫猜想、孪生质数猜想等。然而，当这些东西出现在*编程*竞赛中时，通常会给出它们的定义！

我们可以使用矩阵乘法在 \(O(\log n)\) 时间内计算 \(f_b(n)\)，但这在竞赛环境中通常并不需要，除非出题人使用非常大的 \(n\)。

编程竞赛中可能出现的其他数学问题包括涉及以下内容的问题：**中国剩余定理**（例如 UVa 756 - Biorhythms）、**整除性**性质（例如 UVa 995）、**帕斯卡三角形**、**组合博弈**（例如针对 UVa 10165 - Stone Game（Nim 游戏）、国际象棋、井字棋等游戏的 **Sprague-Grundy 定理**）、涉及非常规**网格**系统的问题（例如 UVa 10182 - Bee Maja）等。

注意，（计算）几何也是数学的一部分，但由于我们有一章专门讨论它，因此我们将与几何问题相关的讨论保留在第 7 章。

就 ICPC 中取得好成绩而言，你的 ICPC 队伍中至少有一名强大的数学家的想法是很好的。这是因为题目集中通常存在一两个数学问题，其解法很短，但要得到解法/公式却需要很强的思考能力。

我们建议有兴趣的读者多浏览一些数论相关内容——参见 [20] 之类的书籍、http://mathworld.wolfram.com/、Wikipedia，并做更多与数学问题相关的编程练习，访问 http://projecteuler.net/ [7]。

本章大约讨论了 **175 道编程练习**。

## 第 6 章 字符串处理

> *人类基因组大约有 33 亿碱基对*
> — 人类基因组计划

> *在本章中，我们将再介绍一个在 ICPC 中会考查的主题，即：字符串处理。处理（长）字符串在生物信息学研究领域相当常见，其中一些问题在 ICPC 中作为竞赛题目出现。*

### 6.1 概述与动机

尽管不如前两章中的图和数学问题那么频繁，字符串处理问题也出现在近期的 ICPC 中（见表 6.1）。一些与字符串相关的问题具有巨大的输入。因此，解法必须使用高效的字符串数据结构和算法。

| LA | 题目名称 | 来源 | 字符串问题（算法） |
|---|---|---|---|
| 2460 | Searching Sequence ... | Singapore01 | 经典字符串对齐问题（DP） |
| 2972 | A DP Problem | Tehran03 | 线性方程分词 |
| 3170 | AGTC | Manila06 | 经典字符串编辑问题（DP） |
| 3669 | String Cutting | Hanoi06 | Ad Hoc 字符串处理 |
| 3791 | Team Arrangement | Tehran06 | Ad Hoc 字符串处理 |
| 3901 | Editor | Seoul07 | 最长重复子串 |
| 3999 | The longest constant gene | Danang07 | 至少 2 个字符串的最长公共子串 |
| 4200 | Find the Format String | Dhaka08 | Ad Hoc 字符串处理 |
| 4657 | Top-10 | Jakarta09 | 后缀数组 + 线段树 |

表 6.1：近期 ACM ICPC 亚洲区域赛中的一些字符串处理问题

### 6.2 Ad Hoc 字符串处理问题

我们以提到 Ad Hoc 字符串处理问题来开始本章。它们是涉及字符串的竞赛问题，只需要不超过基础编程技巧。我们只需仔细阅读题目描述中的要求并编写代码。有时，纯字符数组（又称字符串）操作就足够了。有时，我们需要像 `C <string.h>`、`C++ <string>` 类或 Java String 类这样的字符串库。例如，我们可以使用 C 中的 strstr 在较长字符串中查找某个子串（也称为字符串匹配或字符串搜索），使用 C 中的 strtok 根据某些分隔符将较长字符串分词为若干标记。以下是一些示例：

与 Ad Hoc 字符串处理相关的编程练习：

- 1. UVa 148 - Anagram Checker（+ 回溯）
- 2. UVa 159 - Word Crosses
- 3. UVa 263 - Number Chains
- 4. UVa 353 - Pesky Palindromes
- 5. UVa 401 - Palindromes
- 6. UVa 409 - Excuses, Excuses!（字符串匹配）
- 7. UVa 422 - Word Search Wonder（在网格中进行字符串搜索）
- 8. UVa 537 - Artificial Intelligence?
- 9. UVa 644 - Immediate Decodability
- 10. UVa 865 - Substitution Cypher（简单字符替换映射）
- 11. UVa 902 - Password Search
- 12. UVa 10010 - Where's Waldorf?（在网格中进行字符串搜索）
- 13. UVa 10115 - Automatic Editing
- 14. UVa 10197 - Learning Portuguese
- 15. UVa 10293 - Word Length and Frequency
- 16. UVa 10391 - Compound Words（使用高效数据结构！）
- 17. UVa 10508 - Word Morphing
- 18. UVa 10815 - Andy's First Dictionary
- 19. UVa 10878 - Decode the Tape
- 20. UVa 10896 - Known Plaintext Attack
- 21. UVa 11056 - Formula 1（涉及不区分大小写的字符串比较）
- 22. UVa 11062 - Andy's Second Dictionary
- 23. UVa 11221 - Magic Square Palindrome（无需 DP 即可求解）
- 24. UVa 11233 - Deli Deli
- 25. UVa 11278 - One-Handed Typist
- 26. UVa 11362 - Phone List
- 27. UVa 11385 - Da Vinci Code（字符串操作 + 斐波那契数）
- 28. UVa 11048 - Automatic Correction of Misspellings
- 29. UVa 11713 - Abstract Names（修改后的字符串比较函数）
- 30. UVa 11716 - Digital Fortress（简单密码）
- 31. UVa 11734 - Big Number of Teams will Solve This（修改后的字符串比较函数）

然而，ACM ICPC 近期的竞赛问题通常不会要求解决基础字符串处理，除非是那种所有队伍都应能解决的“送分”题。有些字符串处理问题可以用动态规划（DP）技术解决。我们在 6.3 节讨论它们。其他一些字符串处理问题必须处理**长**字符串，因此必须使用像后缀树或后缀数组这样高效的字符串数据结构。我们在 6.4 节讨论这些数据结构以及使用这些数据结构的若干专门算法。

### 6.3 使用动态规划的字符串处理

本节讨论一些可以用 3.4 节所讨论的 DP 技术解决的字符串处理问题。

#### 6.3.1 字符串对齐（编辑距离）

字符串对齐（或编辑距离）问题定义如下：给定两个字符串 A 和 B，以最大对齐得分（或最小编辑操作数）将 A 与 B 对齐¹：

在将 A 与 B 对齐后，对于所有索引 i，字符 A[i] 与 B[i] 之间存在以下几种可能：

- 1. 字符 A[i] 与 B[i] **匹配**（假设我们给出“+2”得分），
- 2. 字符 A[i] 与 B[i] **不匹配**，并且我们用 B[i] 替换 A[i]（“-1”得分），
- 3. 我们在 A[i] 中插入一个空格（也是“-1”得分），或
- 4. 我们从 A[i] 中删除一个字母（也是“-1”得分）。

例如：

```
A = 'information'    -> '_ _ _ _information_'
B = 'bioinformatics' -> 'bioinformatic_s'
        ----22222222---- -> String Alignment Score = 9 x 2 - 6 = 12
```

尝试所有可能对齐的暴力解法，对于长字符串 A 和/或 B，通常会导致超时（TLE）判决。该问题的解法是著名的 DP 解法（Needleman-Wunsch 算法 [24]）。考虑两个字符串 A[1 ... n] 和 B[1 ... m]。我们定义 V(i,j) 为 A[1 ... i] 与 B[1 ... j] 之间最优对齐的得分，而 score(A,B) 是字符 A 与字符 B 对齐时的得分。

基本情况：

```
V(0,0) = 0 // no score for matching two empty strings
```

递推式：对于 i > 0 且 j > 0：

```
V(0,j) = V(0,j-1) + score(_, B[j]) // insert space j times to make alignment
V(i,0) = V(i-1,0) + score(A[i], _) // delete i times to make alignment
V(i,j) = max(option1, option2, option3), where
option1 = V(i-1,j-1) + score(A[i], B[j]) // score of match or mismatch
option2 = V(i-1,j) + score(A[i], _) // delete
option3 = V(i,j-1) + score(_, B[j]) // insert
```

简而言之，该 DP 算法关注最后一对字符的三种可能性，即它必须是匹配/不匹配、删除或插入。虽然我们不知道哪一种最好，但我们可以尝试所有可能性，同时避免重复计算重叠子问题（即基本上是一种 DP 技术）。

![](img/2f3eff2c1d9ecd727dd36c1db12a8ec9_123_0.png)

使用一个简单的代价函数，其中匹配得到 +2 分，而不匹配、插入、删除都得到 -1 分，A = 'ACAATCC' 和 B = 'AGCATGC' 的字符串对齐得分细节如下所示

¹ 对齐是指向字符串 A 或 B 中插入空格，使它们具有相同字符数的过程。
