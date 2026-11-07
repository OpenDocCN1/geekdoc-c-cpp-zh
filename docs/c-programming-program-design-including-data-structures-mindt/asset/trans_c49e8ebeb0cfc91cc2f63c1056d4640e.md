
**f.** 表达式：(2, 5)

```cpp
(ch >= 'A' && ch <= 'Z')
```

如果 `ch < 'A'` 或 `ch > 'Z'`，则求值为 false。

**g.** 假设输入为 5。以下代码的输出：(3)

```cpp
cin >> num;
if (num > 5)
{
    cout << num;
    num = 0;
}
else
    cout << "Num is zero" << endl;
```

为：`Num is zero`

**h.** 逻辑表达式的结果不能赋给 `int` 变量。(4)

**i.** 表达式 `(!x > 0)` 仅在 x 为负数时为 true。(5)

**j.** 在 C++ 中，`!` 和 `!=` 都是逻辑运算符。(5)

**k.** switch 语句中的表达式应求值为简单数据类型的值。(11)

2. 计算下列表达式的值。(2)

- a. `4 * 7 == 74 / 3`
- b. `4 + 7 / 2 <= 9 - 15 % 6`
- c. `'K' < 'k'`
- d. `'+' <= '-'`
- e. `'5' <= '6'`
- f. `3.9 / 4 - 6 >= 8 - 6.2 * 1.5`

3. 假设 x、y 和 z 是 `int` 变量，且 `x = 13`、`y = 45`、`z = 20`。判断下列表达式的求值结果是 true 还是 false。(2, 5)

- a. `!(x - y <= 10)`
- b. `x + y > 10 || z < 15`
- c. `(x != y) && (x <= z)`
- d. `(y - x >= z) || (2 * z <= y - x)`

4. 假设 str1、str2 和 str3 是字符串变量，且 `str1 = "Low"`、`str2 = "High"`、`str3 = "Medium"`。计算下列表达式的值。(2, 7)

- a. `str1 <= str2`
- b. `str1 != "low"`
- c. `str2 <= str1`
- d. `str3 > "Medium"`
- e. `str3 <= "Light"`

5. 假设 x、y、z 和 w 是 int 变量，且 x = 25、y = 3、z = 12、w = 4。下列语句的输出是什么？(2, 5)

- a.

```cpp
cout << "x == z : " << (x == z) << endl;
```

- b.

```cpp
cout << "y != z : " << (y != z) << endl;
```

- c.

```cpp
cout << "x - y == z + 10: " << (x - y == z + 10) << endl;
```

- d.

```cpp
cout << "!(z < w): " << !(z < w) << endl;
```

- e.

```cpp
cout << "w - y < x - 2 * z: " << (w - y < x - 2 * z)
     << endl;
```

6. 下列哪些不是关系运算符？(2)

- a. `>`  b. `==`  c. `=`  d. `!=`  e. `|`

7. 下列语句的输出是什么？(2, 3)

- a.

```cpp
if ('+' < '-')
    cout << "+-";
    cout << "+" << endl;
```

- b.

```cpp
if (12 / 2 == 4 + 1)
    cout << "6 ";
    cout << "12 / 2 != 4 + 1" << endl;
```

- c.

```cpp
if ('*' >= '/')
    cout << "/";
    cout << "*";
    cout << endl;
```

- d.

```cpp
if ("C++" <= "++C")
    cout << "C++" << endl;
    cout << "C++" << endl;
```

- e.

```cpp
if ("low" <= "high")
    cout << "low" << endl;
    cout << "high" << endl;
```

8. 下列哪些是逻辑（布尔）运算符？(5)

- a. `&&`  b. `!=`  c. `!`  d. `||`  e. `<>`

9. 下列语句的输出是什么？(3, 5)

```cpp
if ('K' > '%' || '@' <= '?')
    cout << "?%";
cout << "!!";
cout << endl;
```

```cpp
if ('8' < 'B' && 15 > -13)
    cout << "a b c d" << endl;
cout << "###" << endl;
```

```cpp
if ("Fly" >= "Flying" && "Programming" >= "Coding")
    cout << "Fly Programming" << endl;
cout << "Flying Coding" << endl;
```

10. 下列代码的输出是什么？(2, 4)

```cpp
int num = 17;                         //Line 1
double gpa = 3.85;                    //Line 2
bool done;                             //Line 3

done = (num == static_cast<int>(2 * gpa + 9.3));   //Line 4
cout << "The value of done is: " << done << endl;  //Line 5
```

11. 如果将第 4 行的语句替换为以下语句，练习 10 的输出会如何变化？(2, 4)

```cpp
done = (num == static_cast<int>(2 * gpa)
              + static_cast<int>(9.3));        //Line 4
```

12. 下列程序的输出是什么？(2)

```cpp
#include <iostream>

using namespace std;

int main()
{
    int firstNum = 28;
    int secondNum = 25;

    cout << firstNum << " " << secondNum << endl;
    cout << (firstNum = 38 - 7) << endl;
    cout << (firstNum <= 75) << endl;
    cout << (firstNum > secondNum + 10) << endl;
    cout << (firstNum >= 3 * secondNum - 100) << endl;
    cout << (secondNum - 1 == 2 * firstNum) << endl;
    cout << firstNum << " " << secondNum << endl;

    return 0;
}
```

13. 改正以下代码，使其输出正确的消息。(3)

```cpp
if (score <= 60)
    cout << "Pass" << endl;
else
    cout << "Fail" << endl;
```

14.

- a. 编写 C++ 语句：如果 standing 为 'F'，输出 First Year；如果 standing 为 'S'，输出 Sophomore；否则输出 Junior or Senior。(3)
- b. 编写 C++ 语句：如果 standing 为 '1' 或 '2'，输出 First Year 和 Sophomore；如果 standing 为 '3' 或 '4'，输出 Junior or Senior；否则输出 Graduate Student。(3)

15. 如果购买的商品数量少于 5，则每件购买商品的运费为 $7.00；如果购买的商品数量至少为 5 但少于 10，则每件购买商品的运费为 $3.00；如果购买的商品数量至少为 10，则免运费。改正以下代码，使其计算正确的运费。(3, 5, 6)

```cpp
if (numOfItemsBought > 10)
    shippingCharges = 0.0;
else if (5 <= numOfItemsBought || numOfItemsBought <= 10);
    shippingCharges = 3.00 * numOfItemsBought;
else if (0 < numOfItemsBought || numOfItemsBought < 5)
    shippingCharges = 7.00 * numOfItemsBought;
```

16. 下列 C++ 代码的输出是什么？(2, 5, 6)

```cpp
int x = 15;
int y = 3;
if (x + y > 17 || y - x < 20)
{
    y = x - y;
    x = y + x;
    cout << x << " " << y << " " << x + y << " " << y - x << endl;
}
else
{
    x = y - x + x % 5;
    cout << x << " " << y << " " << x - y << " " << x + y << endl;
}
```

17. 下列程序的输出是什么？(2, 3, 5)

```cpp
#include <iostream>
using namespace std;

int main()
{
    int first = 16;
    int second = 8;

    if ((first / second == 2) || (second / first == 3))
    {
        second = 10;
        first = 20;
    }
    else if ((first % second == 2 || second % first == 1))
    {
        second = 15;
        first = 5;
    }
    else
    {
        first = -10;
        second = -20;
    }

    cout << first << " " << second << endl;

    return 0;
}
```

18.

- a. 如果 `first = 16` 且 `second = 5`，练习 17 中程序的输出是什么？(2, 3, 5)
- b. 如果 `first = 26` 且 `second = 8`，练习 17 中程序的输出是什么？(2, 3, 5)

19. 假设 `sale` 和 `bonus` 是 double 变量。编写一个 if...else 语句，按如下方式给 `bonus` 赋值：如果 `sale` 大于 $20,000，则赋给 `bonus` 的值为 0.10，即 10%；如果 `sale` 大于 $10,000 且小于或等于 $20,000，则赋给 `bonus` 的值为 0.05，即 5%；否则赋给 `bonus` 的值为 0，即 0%。(3)

20. 假设 `overSpeed` 和 `fine` 是 double 变量。按如下方式给 `fine` 赋值：如果 0 < overSpeed <= 5，则赋给 fine 的值为 $20.00；如果 5 < overSpeed <= 10，则赋给 fine 的值为 $75.00；如果 10 < overSpeed <= 15，则赋给 fine 的值为 $150.00；如果 overSpeed > 15，则赋给 fine 的值为 $150.00 加上超过 15 的每英里 $20.00。(3)

21. 假设 `score` 是一个 `int` 变量。考虑以下 if 语句。

```cpp
if (score >= 90);
    cout << "Discount = 10%" << endl;
```

- a. 如果 `score` 的值为 95，输出是什么？说明理由。
- b. 如果 `score` 的值为 85，输出是什么？说明理由。

22. 假设 `score` 是一个 `int` 变量。考虑以下 if 语句。

```cpp
i.  if (score == 70)
        cout << "Grade is C." << endl;

ii. if (score < 70)
        cout << "Grade is C." << endl;
```

### 回答以下问题

- a. 如果 score 的值为 70，(i) 和 (ii) 的输出分别是什么？if 语句执行后 score 的值是什么？
- b. 如果 score 的值为 80，(i) 和 (ii) 的输出分别是什么？if 语句执行后 score 的值是什么？

23. 使用条件运算符重写下列表达式。（假设所有变量都已正确声明。）(9)

- a.

```cpp
if (x == y)
    z = x + y;
else
    z = (x + y) / 2;
```

- b.

```cpp
if (hours >= 40.0)
    wages = 40 * 7.50 + 1.5 * 7.5 * (hours - 40);
else
    wages = hours * 7.50;
```

- c.

```cpp
if (loanAmount >= 200000)
    closingCosts = 10000;
else
    closingCosts = 8000;
```

24. 使用 if...else 语句重写下列表达式。（假设所有变量都已正确声明。）(9)

- a. `(overSpeed > 10) ? fine = 200 : fine = 75;`
- b. `(fuel >= 10) ? drive = 150 : drive = 30;`
- c. `(bill >= 50.00) ? tip = 0.20 : tip = 0.10;`

25. 假设有以下条件表达式。（假设所有变量都已正确声明。）(9)

```cpp
(0 < backyard && backyard <= 5000) ? fertilizingCharges = 40.00
    : fertilizingCharges = 40.00 + (backyard - 5000) * 0.01;
```

- a. 如果 backyard 的值为 3000，fertilizingCharges 的值是多少？
- b. 如果 backyard 的值为 5000，fertilizingCharges 的值是多少？
- c. 如果 backyard 的值为 6500，fertilizingCharges 的值是多少？

