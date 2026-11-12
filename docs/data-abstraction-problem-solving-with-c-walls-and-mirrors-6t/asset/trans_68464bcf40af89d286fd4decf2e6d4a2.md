

当袋子为空时，持有卡片最多的朋友获胜。清单 1-2 展示了一个玩这个游戏的简单程序。

## 清单 1-2 一个卡片猜谜游戏的程序

```cpp
#include <iostream> // For cout and cin
#include <string> // For string objects
#include "Bag.h" // For ADT bag
using namespace std;

int main()
{
   string clubs[] = { "Joker", "Ace", "Two", "Three",
                      "Four", "Five", "Six", "Seven",
                      "Eight", "Nine", "Ten", "Jack",
                      "Queen", "King" };

   // Create our bag to hold cards.
   Bag<string> grabBag;

   // Place six cards in the bag.
   grabBag.add(clubs[1]);
   grabBag.add(clubs[2]);
   grabBag.add(clubs[4]);
   grabBag.add(clubs[8]);
   grabBag.add(clubs[10]);
   grabBag.add(clubs[12]);

   // Get friend's guess and check it.
   int guess = 0;
   while ( !grabBag.isEmpty() )
   {
      cout << "What is your guess?"
           << " (1 for Ace to 13 for King): ";
      cin >> guess;

      // Is card in the bag?
      if ( grabBag.contains(clubs[guess]) )
      {
         // Good guess - remove card from the bag.
         cout << "You get the card!\n";
         grabBag.remove(clubs[guess]);
      }
      else
      {
         cout << "Sorry, card was not in the bag.\n";
      } // end if
   } // end while

   cout << "\nNo more cards in the bag. Game over!\n";
   return 0;
} // end main
```

**编程提示：** 在你设计一个类之后，尝试在实现该类之前先编写一些使用该类的代码。你不仅能看到你的设计是否适用于当前问题，还能测试你对自己设计的理解，并检查记录你规范的注释。你可能会发现你的类设计或规范存在问题。如果是，请更改你的设计和规范，并尝试再次使用该类。

- **问题 2** 什么是抽象数据类型？
- **问题 3** 在设计 ADT 时应采取哪些步骤？

## 摘要

- 1. 面向对象分析（OOA）用于问题求解的初始阶段，以了解问题是什么以及解决方案的要求是什么。
- 2. 在面向对象设计（OOD）期间，你描述一个问题的解决方案，其要求是在 OOA 期间发现的。你使用软件对象来表达解决方案。
- 3. 封装是面向对象编程的一种原则，用于隐藏函数和对象的内部细节。函数封装行为，对象——即类的实例——封装数据和行为。
- 4. 继承是面向对象编程的另一个相关概念，允许你通过扩展类定义或进行轻微修改来重用已定义的类。
- 5. 多态是面向对象编程的第三个原则，对象在执行时确定适当的操作。
- 6. 每个模块应具有高度内聚性；也就是说，它应执行一个明确定义的任务。
- 7. 耦合是模块之间依赖程度的度量。模块应松散耦合。函数或方法应尽可能独立，并执行一个明确定义的任务。
- 8. UML 是一种用于表达面向对象设计的建模语言。它提供了一种表示法来指定数据和操作，并使用图表来显示类之间的关系。
- 9. 操作契约记录了模块的使用方式及其限制。
- 10. 函数或方法应始终包含一个初始注释，说明其目的、前提条件——即模块开始时必须存在的条件——以及后条件——即模块执行结束时的条件。
- 11. 对于主要涉及数据管理的问题，通过设计类将数据与对该数据的操作封装起来。实践抽象——即关注模块做什么，而不是它如何做。
- 12. 数据抽象是一种控制程序与其数据结构之间交互的技术。它在程序的数据结构周围建立围墙，就像模块性的其他方面在程序的算法周围建立围墙一样。这样的围墙使程序更容易设计、实现、阅读和修改。
- 13. 一组数据管理操作的规范，连同它们操作的数据值，定义了抽象数据类型（ADT）。
- 14. 只有在完全定义 ADT 之后，才应考虑如何实现它。实现 ADT 的合适数据结构的选择既取决于 ADT 操作的细节，也取决于你将使用这些操作的上下文。

## 练习

- 1. 你想购买的商品价格以美元和美分表示。你用现金支付，给收银员 $d$ 美元和 $c$ 美分。为一个计算你应找回的零钱（如果有）的函数编写规范。包括目的陈述、前提条件和后条件以及参数描述。
- 2. 日期由月、日和年组成。考虑表示此类日期的类 Date。假设 Date 将月、日和年表示为整数。例如，1776 年 7 月 4 日是月 7、日 4、年 1776。
     a. 为 Date 内部的一个方法编写规范，该方法将任何给定日期推进一天。包括目的陈述、前提条件和后条件、参数描述以及任何返回值的描述。
     b. 编写此方法的 C++ 实现。设计并指定你需要的任何其他方法。包括对将来维护你实现的人有帮助的注释。
- 3. 为以下每个任务编写一个伪代码函数，使用第 1.4.1 节中描述的 ADT 预约簿。执行这些任务是否需要向 ADT 添加操作？
     a. 更改给定日期和时间的预约目的。
     b. 显示给定日期的所有预约。
- 4. 假设你刚带着一袋杂货离开商店。你担心易碎物品无法安全到家，所以当你到达汽车时，将这些物品放入它们自己的袋子中。如果 bag 是袋子类，请编写 C++ 语句，从 storeBag 中移除所有物品，并将它们放入两个新袋子中的一个，如下所示：将所有面包和鸡蛋放入 fragileBag，将所有其他物品放入 groceryBag。完成后，storeBag 应为空。假设杂货项由字符串表示。
- 5. 假设一个袋子包含表示各种杂货项的字符串。编写一个 C++ 函数，从这样的袋子中移除并计算给定字符串的所有出现次数。你的函数应返回该数字。使用 javadoc 风格的注释来完全指定你的函数。考虑给定袋子可能为空或不包含任何给定字符串出现的情况。
- 6. 两个袋子的并集是一个包含原始两个袋子合并内容的新袋子。为 ADT bag 设计并编写一个 union 方法，该方法作为一个新袋子返回接收方法调用的袋子与作为方法参数的袋子的并集。包括足够的注释来完全指定该方法。
     注意，两个袋子的并集可能包含重复项。例如，如果对象 x 在一个袋子中出现五次，在另一个袋子中出现两次，则这些袋子的并集包含 x 七次。具体来说，假设 bag1 和 bag2 是袋子；bag1 包含字符串 a、b 和 c；bag2 包含字符串 b、d 和 e。表达式 bag1.union(bag2) 返回一个包含字符串 a、b、b、c、d 和 e 的袋子。注意，union 不会影响 bag1 和 bag2 的内容。
- 7. 两个袋子的交集是一个包含原始两个袋子中都出现的条目的新袋子。为 ADT bag 设计并指定一个 intersection 方法，该方法作为一个新袋子返回接收方法调用的袋子与作为方法唯一参数的袋子的交集。包括足够的注释来完全指定该方法。
     注意，两个袋子的交集可能包含重复项。例如，如果对象 x 在一个袋子中出现五次，在另一个袋子中出现两次，则这些袋子的交集包含 x 两次。具体来说，假设 bag1 和 bag2 是袋子；bag1 包含字符串 a、b 和 c；bag2 包含字符串 b、b、d 和 e。表达式 bag1.intersection(bag2) 返回一个仅包含字符串 b 的袋子。注意，intersection 不会影响 bag1 和 bag2 的内容。
- 8. 两个袋子的差集是一个包含在从一个袋子中移除那些也在第二个袋子中出现的条目后所剩下的条目的新袋子。为 ADT bag 设计并指定一个 difference 方法，该方法作为一个新袋子返回接收方法调用的袋子与作为方法唯一参数的袋子的差集。包括足够的注释来完全指定该方法。
     注意，两个袋子的差集可能包含重复项。例如，如果对象 x 在一个袋子中出现五次，在另一个袋子中出现两次，则这些袋子的差集包含 x 三次。具体来说，假设 bag1 和 bag2 是袋子；bag1 包含字符串 a、b 和 c；bag2 包含字符串 b、b、d 和 e。表达式 bag1.difference(bag2) 返回一个仅包含字符串 a 和 c 的袋子。注意，difference 不会影响 bag1 和 bag2 的内容。
- 9. 考虑单变量 x 的 ADT 多项式，其操作包括以下内容：

   ```
   degree() // Returns the degree of a polynomial.
   coefficient(power) // Returns the coefficient of the x^power term.
   changeCoefficient(newCoefficient, power) // Replaces the coefficient of
   // the x^power term with newCoefficient.
   ```

   对于此问题，仅考虑指数为非负整数的多项式。例如，p = 4x^3 + 7x^2 - x + 9

   以下示例演示了该多项式上的 ADT 操作。

   ```
   p.degree() is 5 (the highest power of a term with a nonzero coefficient)
   p.coefficient(3) is 7 (the coefficient of the x^3 term)
   p.coefficient(4) is 0 (the coefficient of a missing term is implicitly 0)
   p.changeCoefficient(-3, 7) changes the polynomial p to -3x^7 + 4x^3 + 7x^2 - x + 9
   ```

   使用这些 ADT 操作，编写语句以执行以下任务：

   a. 显示具有最高幂次的项的系数。
   b. 将 x^4 项的系数增加 8。
   c. 计算两个多项式的和。

## 编程问题

- 1. 将 Transaction 类添加到附录 C 中图 C-4 的银行示例中。该类跟踪交易的日期、时间、金额和类型（支票或储蓄）。
- 2. 考虑一个程序，它将读取员工数据、按员工识别号对数据进行排序、写出排序后的数据，并计算关于数据的各种统计信息，例如员工的平均年龄。使用 UML 表示法为此问题设计模块化解决方案。在设计解决方案期间，你识别了哪些类和方法？为每个模块编写完整的规范，包括前提条件和后条件。

