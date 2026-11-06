

## 第 4.11.7 节 使用列表初始化防止窄化转换

-   还可以使用流操纵符 `showpoint`（第 130 页）强制显示小数点。如果指定了 `showpoint` 而未指定 `fixed`，则不会打印尾随零。
-   非参数化流操纵符 `fixed` 和 `showpoint` 需要头文件 `<iostream>`。

## 第 4.12 节 复合赋值运算符

-   **复合赋值运算符** `+=`、`-=`、`*=`、`/=` 和 `%=`（第 **136** 页）是赋值表达式的简写形式。

## 第 4.13 节 自增和自减运算符

-   **自增**（第 137 页；`++`）和**自减**（第 137 页；`--`）运算符分别将变量加 1 或减 1。如果运算符位于变量之前（前缀），则先将变量加 1 或减 1，然后使用其新值参与所在表达式的计算。如果运算符位于变量之后（后缀），则先使用该变量在表达式中进行计算，然后再将变量的值加 1 或减 1。

## 第 4.14 节 基本类型不可移植

-   所有变量都必须有类型。
-   基本类型在不同计算机上并不保证完全相同。在一台机器上，`int` 可能用 16 位（2 字节）内存表示，在另一台机器上可能是 32 位（4 字节），而在其他机器上可能是 64 位（8 字节）。

## 自测练习

-   1. **4.1** 回答下列各题。
    -   **A.** 所有程序都可以用三种控制语句编写：________、________ 和 ________。
    -   **B.** 当条件为*真*时执行一种操作，当条件为*假*时执行另一种操作，使用的是 ________ 选择语句。
    -   **C.** 将一组指令重复执行特定次数称为 ________ 迭代。
    -   **D.** 当事先不知道一组语句将重复多少次时，可以使用 ________ 值来终止迭代。
-   2. **4.2** 编写四条不同的 C++ 语句，每条语句都将整数变量 `x` 加 1。
-   3. **4.3** 编写 C++ 语句来完成以下各项任务：
    -   **A.** 用一条语句将 `x` 和 `y` 的当前值之和赋给 `z`，并对 `x` 进行后缀自增。
    -   **B.** 判断变量 `count` 的值是否大于 10。如果是，则打印 `"Count is greater than 10"`。
    -   **C.** 将变量 `x` 前缀自减 1，然后从变量 `total` 中减去它。
    -   **D.** 计算 `q` 除以 `divisor` 后的余数，并将结果赋给 `q`。用两种不同的方式编写此语句。
-   4. **4.4** 编写 C++ 语句来完成以下各项任务。
    -   **A.** 声明变量 `sum` 为 `unsigned int` 类型并将其初始化为 `0`。
    -   **B.** 声明变量 `x` 为 `unsigned int` 类型并将其初始化为 `1`。
    -   **C.** 将变量 `x` 加到变量 `sum` 中，并将结果赋给变量 `sum`。
    -   **D.** 打印 `"The sum is: "` 并在其后跟上变量 `sum` 的值。
-   5. **4.5** 将你在**练习 4.4** 中编写的语句组合成一个程序，该程序计算并打印从 1 到 10 的整数之和。使用 `while` 语句循环执行计算和自增语句。当 `x` 的值变为 11 时，循环应终止。
-   6. **4.6** 计算执行后，指出*每个*这些 `unsigned int` 变量的值。假设每条语句开始执行时，所有变量的整数值都为 5。
    -   **A.** `product *= x++;`
    -   **B.** `quotient /= ++x;`
-   7. **4.7** 编写单条 C++ 语句或语句片段来完成以下操作：
    -   **A.** 使用 `cin` 和 `>>` 输入 `unsigned int` 变量 `x`。
    -   **B.** 使用 `cin` 和 `>>` 输入 `unsigned int` 变量 `y`。
    -   **C.** 声明 `unsigned int` 变量 `i` 并将其初始化为 `1`。
    -   **D.** 声明 `unsigned int` 变量 `power` 并将其初始化为 `1`。
    -   **E.** 将变量 `power` 乘以 `x`，并将结果赋给 `power`。
    -   **F.** 将变量 `i` 前缀自增 `1`。
    -   **G.** 判断 `i` 是否小于或等于 `y`。
    -   **H.** 使用 `cout` 和 `<<` 输出整数变量 `power`。
-   8. **4.8** 编写一个 C++ 程序，使用**练习 4.7** 中的语句计算 `x` 的 `y` 次幂。程序应包含 `while` 迭代语句。
-   9. **4.9** 找出并更正以下各项中的错误：
    -   **A.**
        ```cpp
        while (c <= 5) {
            product *= c;
            ++c;
        ```
    -   **B.** `cin << value;`
    -   **C.**
        ```cpp
        if (gender == 1) {
            cout << "Woman" << endl;
        }
        else; {
            cout << "Man" << endl;
        }
        ```
-   10. **4.10** 下面的 `while` 迭代语句有什么问题？
    ```cpp
    while (i2 >= 0) {
        sum += 2;
    }
    ```

## 自测练习答案

-   1. **4.1**
    -   **A.** 顺序、选择和迭代。
    -   **B.** `if...else`。
    -   **C.** 计数器控制或确定性。
    -   **D.** 哨兵、信号、标志或哑元。
-   2. **4.2**
    ```cpp
    x = x + 1;
    x += 1;
    ++x;
    x++;
    ```
-   3. **4.3**
    -   **A.**
        ```cpp
        z = x++ + y;
        ```
    -   **B.**
        ```cpp
        if (count > 10) {
            cout << "Count is greater than 10" << endl;
        }
        ```
    -   **C.**
        ```cpp
        total -= --x;
        ```
    -   **D.**
        ```cpp
        q %= divisor;
        q = q % divisor;
        ```
-   4. **4.4**
    -   **A.**
        ```cpp
        unsigned int sum{0};
        ```
    -   **B.**
        ```cpp
        unsigned int x{1};
        ```
    -   **C.**
        ```cpp
        sum += x;
        // 或
        sum = sum + x;
        ```
    -   **D.** `cout << "The sum is: " << sum << endl;`
-   5. **4.5** 请参阅以下代码：
    ```cpp
    // Exercise 4.5: Calculate.cpp
    // Calculate the sum of the integers from 1 to 10
    #include <iostream>
    using namespace std;

    int main() {
        unsigned int sum(0);
        unsigned int x(1);

        while (x <= 10) {  // while x is less than or equal to 10
            sum += x;  // add x to sum
            ++x;  // increment x
        }

        cout << "The sum is: " << sum << endl;
    }
    ```
    ```text
    The sum is: 55
    ```
-   6. **4.6**
    -   **A.** `product = 25, x = 6;`
    -   **B.** `quotient = 0, x = 6;`
-   7. **4.7**
    -   **A.** `cin >> x;`
    -   **B.** `cin >> y;`
    -   **C.** `unsigned int i{1};`
    -   **D.** `unsigned int power{1};`
    -   **E.**
        ```cpp
        power *= x;
        // 或
        power = power * x;
        ```
    -   **F.** `++i;`
    -   **G.** `if (i <= y)`
    -   **H.** `cout << power << endl;`
-   8. **4.8** 请参阅以下代码：
    ```cpp
    // Exercise 4.8 Solution: power.cpp
    // Raise x to the y power.
    #include <iostream>
    using namespace std;

    int main() {
        unsigned int i(1); // initialize i to begin counting from 1
        unsigned int power(1); // initialize power

        cout << "Enter base as an integer: "; // prompt for base
        unsigned int x; // base
        cin >> x; // input base

        cout << "Enter exponent as an integer: "; // prompt for exponent
        unsigned int y; // exponent
        cin >> y; // input exponent

        // count from 1 to y and multiply power by x each time
        while (i <= y) {
            power *= x;
            ++i;
        } // end while

        cout << power << endl; // display result
    } // end main
    ```
    ```text
    Enter base as an integer: 2
    Enter exponent as an integer: 3

    8
    ```
-   9. **4.9**
    -   **A.** *错误：* `while` 循环体缺少右花括号。  
        *更正：* 在语句 `++c;` 之后添加右花括号。
    -   **B.** *错误：* 使用流插入代替了流提取。  
        *更正：* 将 `<<` 改为 `>>`。
    -   **C.** *错误：* `else` 后面的分号是一个逻辑错误。第二条输出语句总是会执行。  
        *更正：* 删除 `else` 后面的分号。
-   10. **4.10** 变量 `z` 的值在 `while` 语句中从未改变。因此，如果循环继续条件（`z >= 0`）最初为*真*，则会产生无限循环。为防止无限循环，必须递减 `z`，使其最终小于 0。

