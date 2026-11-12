

函数 binarySearch 只调用自身一次，尽管你在 C++ 代码中看到了两次调用。这两次调用出现在一个 if 语句中；其中只有一次会被执行。

当孤立的递归调用是函数执行的最后一个动作时，将递归解转换为迭代解会更容易。这种情况称为 **尾递归**。例如，函数 writeBackward 表现出尾递归，因为其递归调用是函数执行的最后一个动作。在你得出这显而易见的结论之前，请考虑函数 fact。尽管其递归调用出现在函数定义的最后，fact 的最后一个动作是乘法。因此，fact 不是尾递归的。

回顾 writeBackward 的定义：

```cpp
void writeBackward(string s)
{
   int length = s.size();
   if (length > 0)
   {
      // Write last character
      cout << s.substr(length - 1, 1);
      writeBackward(s.substr(0, length - 1)); // Write rest
   } // end if
} // end writeBackward
```

由于此函数是尾递归的，其最后一次递归调用只是用改变后的参数重复函数的动作。你可以使用迭代来执行这个重复动作，这通常简单且更高效。例如，以下是 writeBackward 的迭代定义：

```cpp
/** Iterative version. */
void writeBackward(string s)
{
   int length = s.size();
   while (length > 0)
   {
      cout << s.substr(length - 1, 1);
      length--;
   } // end while
} // end writeBackward
```

由于尾递归函数通常比其迭代对应物效率低，并且将尾递归函数转换为等效的迭代函数相当机械，一些编译器会自动将尾递归替换为迭代。消除其他形式的递归通常更复杂，如果有必要，这是你需要承担的任务。

一些递归算法，例如 rabbit，本质上效率低下，而其他递归算法，例如 二分查找，效率极高。你将在更高级的算法分析课程中学习如何确定递归算法的相对效率。第 10 章简要介绍了其中一些技术。

第 5 章通过考察几个具有简单递归解的难题，继续讨论递归。本书的其他章节也习惯性地使用递归。

问题 10 在本章中你见过的以下递归函数中，找出表现出尾递归的函数：fact、writeBackward、writeBackward2、rabbit、游行问题中的 P、getNumberOfGroups、maxArray、binarySearch 和 kSmall。

## 摘要

- 1. 递归是一种通过解决同类型的更小问题来解决问题的技术。
- 2. 构建递归解时，请牢记以下四个问题：
  - a. 如何将问题定义为同类型的更小问题？
  - b. 每次递归调用如何减小问题的规模？
  - c. 问题的哪个实例可以作为基础情况？
  - d. 随着问题规模减小，你是否会达到这个基础情况？
- 3. 构建递归解时，如果满足前置条件，你可以假设递归调用的结果是正确的。
- 4. 你可以使用框跟踪来跟踪递归函数的动作。这些框类似于许多编译器用于实现递归的激活记录。尽管框跟踪很有用，但它不能取代对递归的直观理解。
- 5. 递归允许你解决一些问题——例如汉诺塔——其迭代解难以概念化。即使是最复杂的问题，通常也有简单的递归解。此类解比迭代解更容易理解、描述和实现。
- 6. 由于其本质上效率低下的算法和函数调用的开销，某些递归解比相应的迭代解效率低得多。在这种情况下，迭代解可能更可取。然而，你可以使用递归解来推导迭代解。
- 7. 如果你能使用迭代轻松、清晰且高效地解决问题，那么你应该这样做。

## 练习

- 1. 以下递归函数 getNumberEqual 在包含 n 个整数的数组 x 中查找整数 desiredValue 的出现次数。它返回 x 中等于 desiredValue 的整数个数。例如，如果 x 包含十个整数 1、2、4、5、6、7、8、9 和 12，则 getNumberEqual(x, 10, 4) 返回值 2，因为 4 在 x 中出现了两次。

  ```cpp
  int getNumberEqual(const int x[], int n, int desiredValue)
  {
      int count = 0;
      if (n <= 0)
          return 0;
      else
      {
          if (x[n - 1] == desiredValue)
              count = 1;
          return getNumberEqual(x, n - 1, desiredValue) + count;
      } // end else
  } // end getNumberEqual
  ```

  通过列出递归解的标准并说明该函数如何满足每个标准，来证明该函数是递归的。

- 2. 对本章中出现的以下递归函数调用执行框跟踪。清楚地指示每个后续递归调用。
  - a. rabbit(5)
  - b. countDown(5)（你在检查点问题 3 中编写了 countDown。）

- 3. 编写一个递归函数，计算至少包含 n 个整数的数组中前 n 个整数的和。提示：从第 n 个整数开始。

- 4. 给定两个整数 start 和 end，其中 end 大于 start，编写一个递归 C++ 函数，返回从 start 到 end（包含两端）的整数之和。

- 5. a. 修改在第 2.3.1 节中讨论的函数 writeBackward，使其基础情况为长度为 1 的字符串。
  - b. 编写一个 C++ 函数，实现第 2.3.1 节中给出的伪代码函数 writeBackward2。

- 6. 描述以下递归函数的问题：

  ```cpp
  void printNum(int n)
  {
      cout << n << endl;
      printNum(n - 1);
  } // end printNum
  ```

- 7. 给定整数 n > 0，编写一个递归 C++ 函数，输出整数 1、2、..., n。

- 8. 给定整数 n > 0，编写一个递归 C++ 函数，返回 1 到 n 的平方和。

- 9. 编写一个递归 C++ 函数，以逆序输出正十进制整数的各位数字。

- 10. a. 编写一个递归 C++ 函数 writeLine，重复写入一个字符以形成 n 个字符的一行。例如，writeLine('*', 5) 生成一行 *****。
  - b. 现在编写一个递归函数 writeBlock，使用 writeLine 写入 m 行，每行 n 个字符。例如，writeBlock('*', 5, 3) 生成以下输出

  ```
  *****
  *****
  *****
  *****
  ```

- 11. 以下程序产生什么输出？

  ```cpp
  int getValue(int a, int b, int n);
  int main()
  {
      cout << getValue(1, 7, 7) << endl;
      return 0;
  } // end main
  int getValue(int a, int b, int n)
  {
      int returnValue = 0;
      cout << "Enter: a = " << a << " b = " << b << endl;
      int c = (a + b)/2;
      if (c == a + b)
      returnValue = c;
      else
      returnValue = getValue(a, c-1, n);
      cout << "Leave: a = " << a << " b = " << b << endl;
      return returnValue;
  } // end getValue
  ```

- 12. 以下程序产生什么输出？

  ```cpp
  int search(int first, int last, int n);
  int mystery(int n);
  int main()
  {
      cout << mystery(30) << endl;
      return 0;
  } // end main

  int search(int first, int last, int n)
  {
      int returnValue = 0;
      cout << "Enter: first = " << first << " last = "
           << last << endl;
      int mid = (first + last)/2;
      if ( (mid * first == n) && (n < (mid+1) * (mid+1)) )
          returnValue = mid;
      else if (mid * mid > n)
          returnValue = search(first, mid-1, n);
      else
          returnValue = search(mid+1, last, n);
      cout << "Leave: first = " << first << " last = "
           << last << endl;
      return returnValue;
  } // end search

  int mystery(int n)
  {
      return search(1, n, n);
  } // end mystery
  ```

- 13. 考虑以下函数，它将正十进制数转换为八进制并显示结果。

  ```cpp
  void displayOctal(int n)
  {
      if (n > 0)
      {
          if (n / 8 > 0)
              displayOctal(n / 8);
          cout << n % 8;
      } // end if
  } // end displayOctal
  ```

  描述该算法的工作原理。使用 n = 100 跟踪该函数。

- 14. 考虑以下程序：

  ```cpp
  int f(int n);
  int main()
  {
      cout << "The value of f(8) is " << f(8) << endl;
      return 0;
  } // end main
  /* @pre n >= 0. */
  int f(int n)
  {
      cout << "Function entered with n = " << n << endl;
      switch (n)

