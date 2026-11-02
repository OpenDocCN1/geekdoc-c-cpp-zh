
## 2.4 大模型智能涌现的根源

> 大模型智能涌现的根源是什么？目前学术界对此未有定论，主要有三种解释：

- ① 大模型的规模效应使其从量变到质变，产生了非线性跃迁的智能涌现能力。
- ② 大模型的智能主要来源于海量数据中蕴含的知识，模型通过记忆和泛化产生了智能。
- ③ 大模型与人类交互过程中产生的智能，是人与机器协同进化的结果。

这些解释从不同角度揭示了超大模型智能涌现的成因。在大模型引领的智能革命中，人类的价值观和伦理准则被以一种可供机器学习的表达形式嵌入超大模型的算法架构中，使之与人类智能的价值观对齐（alignment），因此大模型不仅是人类知识学习的结果，也是人类价值观的映射。

| 表2-1 人类智能与AI智能的区别 | |
| --- | --- |
| **人类智能** | **AI智能** |
| 主动性：人类具有主动性和创造性 | 被动性：不具有主动性和创造性 |
| 社会性：人类社会性的产物 | 技术性：人类技术发展的产物 |
| 灵活性：处理的事物不确定、多变 | 机械性：按设定程序进行数据处理 |
| 价值观：受情感、伦理、道德影响 | 无价值观：不受情感、伦理、道德影响 |
| 适应性：能适应环境变化 | 局限性：只能在特定领域发挥作用 |

需要指出的是，表2-1所列差异并非绝对，随着通用人工智能和超级人工智能的发展，AI智能与人类智能之间的边界可能发生变化。

## 燃气灶

家用燃气灶

| 型号 | JZT-BCD1 | 类别 | 台式燃气灶 |
|---|---|---|---|
| 燃气种类 | 天然气（12T） | 额定压力 | 2000Pa |

## 使用安全注意事项

- 1. 请在使用前仔细阅读本说明书，并妥善保管。
- 2. 燃气具安装、改装应由专业人员进行。
- 3. 使用前请确认燃气种类与产品铭牌一致。
- 4. 保持厨房通风良好，防止一氧化碳中毒。

## 主要技术参数

| 项目 | 参数 |
|---|---|
| 额定热负荷 | 4.2kW |
| 热效率 | ≥63% |
| 点火方式 | 脉冲电子点火 |
| 安全装置 | 热电偶熄火保护 |

## 安装说明

- 1. 本产品为嵌入式灶具，安装前请确认橱柜台面开孔尺寸。
- 2. 安装时请注意灶具底部与柜体之间留有适当空间。
- 3. 连接软管前，请在接头处安装管卡，并检查连接是否牢固。

```
开孔尺寸（mm）：650×350 R≥20
台面厚度（mm）：≥15
```

## 使用方法

- 1. 点火：按下旋钮并逆时针转动至90°位置，听到“啪”声后松手。
- 2. 火焰调节：转动旋钮可调节火力大小。
- 3. 使用完毕后，请确认火已完全熄灭并关闭气源阀门。

## 清洁保养

- 1. 请勿使用钢丝球或硬质刷子清洗灶具表面。
- 2. 火盖可拆下清洗，晾干后装回原位。
- 3. 保持点火针与热电偶清洁干燥。

## 非故障现象

| 现象 | 可能原因 | 处理方法 |
|---|---|---|
| 黄焰 | 风门调整不当 | 调整风门至火焰呈蓝色 |
| 点不着火 | 燃气软管折弯或气量不足 | 检查软管或更换燃气罐 |
| 熄火保护启动 | 热电偶位置偏移 | 请专业人员调整 |

本公司产品经严格检验合格后出厂。如有任何疑问，请致电售后服务热线。

## CHAPTER 11
RECURSION

![](img/d61019b035dd82beb581604273c0ee6b_572_0.png)

## CHAPTER GOALS

- To learn to “think recursively”
- To be able to use recursive helper functions
- To understand the relationship between recursion and iteration
- To understand when the use of recursion affects the efficiency of an algorithm
- To analyze problems that are much easier to solve by recursion than by iteration
- To process data with recursive structures using mutual recursion

## CHAPTER CONTENTS

- 11.1 TRIANGLE NUMBERS 364
- CE1 Tracing Through Recursive Functions 367
- CE2 Infinite Recursion 368
- HT1 Thinking Recursively 369
- WE1 Finding Files 372
- 11.2 RECURSIVE HELPER FUNCTIONS 372
- 11.3 THE EFFICIENCY OF RECURSION 373
- 11.4 PERMUTATIONS 377
- 11.5 MUTUAL RECURSION 380
- 11.6 BACKTRACKING 383
- WE2 Towers of Hanoi 389
- C&S The Limits of Computation 390

© Nicolae Popovici/Stockphoto.

```cpp
int term_value()
{
   int result = factor_value();
   bool done = false;
   while (!done)
   {
      char op = cin.get();
      if (op == '*' || op == '/')
      {
         int value = factor_value();
         if (op == '*') { result *= value; }
         else { result /= value; }
      }
      else { cin.unget(); done = true; }
   }
   return result;
}
```

```cpp
/**
   Evaluates the next factor found in cin.
   @return the value of the factor
*/
int factor_value()
{
   int result = 0;
   char c = cin.get();
   if (c == '(')
   {
      result = expression_value();
      cin.get(); // Read ')'
   }
   else
   {
      cin.unget();
      cin >> result;
   }
   return result;
}
```

```cpp
int main()
{
   cout << "Enter an expression: ";
   cout << expression_value() << endl;
   return 0;
}
```

## Program Run

```
Enter an expression: 1+2*12*12
1729
```

## 11.6 Backtracking

Backtracking is a problem solving technique that builds up partial solutions that get increasingly closer to the goal. If a partial solution cannot be completed, one abandons it and returns to examining the other candidates.

- **E11.18** Recursively generate all ways in which a vector can be split up into a sequence of nonempty subvectors. For example, if you are given the vector `{1, 7, 2, 9}`, return the following vectors of vectors:
  
  `{{1}, {7}, {2}, {9}}, {{1, 7}, {2}, {9}}, {{1}, {7, 2}, {9}}, {{1}, {7}, {2, 9}}, {{1, 7, 2}, {9}}, {{1, 7}, {2, 9}}, {{1}, {7, 2, 9}}, {{1, 7, 2, 9}}`
  
  *Hint:* First generate all subvectors of the vector with the last element removed. The last element can either be a subsequence of length 1, or it can be added to the last subsequence.

- **E11.19** Given a vector of integers, recursively find all vectors of elements of a whose sum is a given integer n.

- **E11.20** Suppose you want to climb a staircase with n steps and you can take either one or two steps at a time. Recursively enumerate all paths. For example, if n is 5, the possible paths are:
  
  `{1, 2, 3, 4, 5}, {1, 3, 4, 5}, {1, 2, 4, 5}, {1, 2, 3, 5}, {1, 4, 5}`

- **E11.21** Repeat Exercise E11.20, where the climber can take up to k steps at a time.

- **E11.22** Given an integer price, list all possible ways of paying for it with $100, $20, $5, and $1 bills, using recursion. Don’t list duplicates.

- **E11.23** Extend the expression evaluator in Section 11.5 so that it can handle the `%` operator as well as a “raise to a power” operator `^`. For example, `2 ^ 3` should evaluate to 8. As in mathematics, raising to a power should bind more strongly than multiplication:
  
  `5 * 2 ^ 3` is 40.

- **E11.24** The backtracking algorithm will work for any problem whose partial solutions can be examined and extended. Provide a class

```cpp
class PartialSolution
{
public:
    virtual int examine() const;
    virtual vector<PartialSolution*> extend() const;
    virtual void print() const;
    PartialSolution* solve() const;
};
```

and a derived class EightQueensPartialSolution.

- **E11.25** Refine the program for solving the eight queens problem so that rotations and reflections of previously displayed solutions are not shown. Your program should display twelve unique solutions.

- **E11.26** Refine the program for solving the eight queens problem so that the solutions are written to an HTML file, using tables with black and white background for the board and the Unicode character `♛` (`\u2655`) for the white queen.

- **E11.27** Generalize the program for solving the eight queens problem to the n queens problem. Your program should prompt for the value of n and display the solutions.

- **E11.28** Using backtracking, write a program that solves summation puzzles in which each letter should be replaced by a digit, such as
  
  `send + more = money`

Your program should find the solution 9567 + 1085 = 10652. Other examples are base + ball = games and kyoto + osaka = tokyo.

**Hint:** In a partial solution, some of the letters have been replaced with digits. In the third example, you would consider all partial solutions where k is replaced by 0, 1, ..., 9: 0yoto + osa0a = to0yo, 1yoto + osala = to1yo, and so on. To extend a partial solution, find the first letter replaced by a digit that doesn’t occur in the partial solution. If a partial solution has no more letters, check whether the sum is correct.

- **EX11.29** The recursive computation of Fibonacci numbers can be speeded up significantly by keeping track of the values that have already been computed. Provide an implementation of the fib function that uses this strategy. Whenever you return a new value, also store it in an auxiliary array. However, before embarking on a computation, consult the array to find whether the result has already been computed. Compare the running time of your improved implementation with that of the original recursive implementation and the loop implementation.

## PROGRAMMING PROJECTS

- **P11.1** Phone numbers and PIN codes can be easier to remember when you find words that spell out the number on a standard phone keypad. For example, instead of remembering the combination 2633, you can just think of CODE. Write a recursive function that, given a number, yields all possible spellings (which may or may not be real words).

- **P11.2** Continue Exercise P11.1, checking the words against the `/usr/share/dict/words` file on your computer, or the `words.txt` file in the companion code for this book. For a given number, return only actual words.

- **P11.3** With a longer number, you may need more than one word to remember it on a phone pad. For example, 846-386-2633 is TIME TO CODE. Using your work from Exercise P11.2, write a program that, given any number, lists all word sequences that spell the number on a phone pad.

- **P11.4** Change the permutations function of Section 11.4 (which computed all permutations at once) to a `PermutationIterator` (which computes them one at a time).

```cpp
class PermutationIterator
{
public:
    PermutationIterator(string s) { ... }
    string next_permutation() { ... }
    bool has_more_permutations() { ... }
};
```

Here is how you would print out all permutations of the string "eat":

```cpp
PermutationIterator iter("eat");
while (iter.has_more_permutations())
{
    cout << iter.next_permutation() << endl;
}
```

Now we need a way to iterate through the permutations recursively. Consider the string "eat". As before, we’ll generate all permutations that start with the letter 'e',
