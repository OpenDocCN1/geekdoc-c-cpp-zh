

```cpp
cout << endl;

cout << "The pig Latin form of " << str << " is: "
     << pigLatinString(str) << endl;

return 0;
}
```

```cpp
// Place the definitions of the functions isVowel, rotate, and
// pigLatinString as described previously here.
```

**示例运行：** 在这些示例运行中，用户输入以底纹显示。

**示例运行 1：**

输入一个字符串：`eye`

eye 的猪拉丁语形式为：eye-way

**示例运行 2：**

输入一个字符串：`There`

There 的猪拉丁语形式为：ere-Thay

**示例运行 3：**

输入一个字符串：`why`

why 的猪拉丁语形式为：y-why

**示例运行 4：**

输入一个字符串：`123456`

123456 的猪拉丁语形式为：123456-way

## 快速回顾

- 1. 枚举类型是一组有序值。
- 2. C++ 的保留字 `enum` 用于创建枚举类型。
- 3. `enum` 的语法为：
  ```cpp
  enum typeName {value1, value2,...};
  ```
  其中 value1、value2、... 是标识符，且 value1 < value2 < ...
- 4. 枚举类型不允许进行算术运算。
- 5. 关系运算符可用于 `enum` 值。
- 6. 枚举类型的值不能直接输入或输出。
- 7. 枚举类型可以按值或按引用作为参数传递给函数。
- 8. 函数可以返回枚举类型的值。
- 9. 匿名类型是指在不指定任何类型名称的情况下指定变量值的类型。
- 10. C++ 的保留字 `typedef` 用于为已定义的数据类型创建同义词或别名。
- 11. 匿名类型不能作为参数传递给函数。
- 12. `namespace` 机制是 ANSI/ISO 标准 C++ 的一个特性。
- 13. `namespace` 成员通常是命名常量、变量、函数或另一个 `namespace`。
- 14. `namespace` 成员的作用域局限于该 `namespace` 内。
- 15. 在 `namespace` 外访问其成员的一种方法是在该成员名前加上 `namespace` 名和作用域解析运算符。
- 16. 在 C++ 中，`namespace` 是保留字。
- 17. 要使用 `namespace` 机制，程序必须包含 ANSI/ISO 标准 C++ 头文件——即不带 .h 扩展名的头文件。
- 18. `using` 语句简化了对 `namespace` 成员的访问。
- 19. 在 C++ 中，`using` 是保留字。
- 20. 关键字 `namespace` 必须出现在 `using` 语句中。
- 21. 在不使用 `using` 语句访问 `namespace` 成员时，`namespace` 名和作用域解析运算符必须位于该成员名之前。
- 22. 要在不使用 `namespace` 名的情况下使用标准头文件中声明的标识符，在包含所有必需的头文件后，程序中必须出现以下语句：
  ```cpp
  using namespace std;
  ```
- 23. 字符串是零个或多个字符的序列。
- 24. C++ 中的字符串用双引号括起来。
- 25. 要使用 `string` 类型，程序必须包含头文件 `string`。程序中使用的其他头文件应为 ANSI/ISO 标准 C++ 风格的头文件。
- 26. 赋值运算符可用于 `string` 类型。
- 27. 运算符 `+` 可用于连接两个 `string` 类型的值。要使运算符 `+` 能用于 `string` 数据类型，`+` 的操作数之一必须是 `string` 变量。
- 28. 第 4 章讨论的关系运算符可应用于 `string` 类型。
- 29. 在字符串中，第一个字符的位置是 0，第二个字符的位置是 1，依此类推。
- 30. 字符串的长度是字符串中的字符数。
- 31. 在 C++ 中，`[]` 称为数组下标运算符。
- 32. 要访问字符串中的单个字符，请将数组下标运算符与该字符的位置一起使用。
- 33. `string` 类型包含 `at`、`append`、`clear`、`compare`、`erase`、`find`、`find_first_of`、`find_first_not_of`、`insert`、`length`、`replace`、`size`、`substr` 和 `swap` 等函数，用于操作字符串。这些函数在表 7-1 中描述。

## 练习题

练习题末尾括号中的数字指本章开头列出的学习目标。

- 1. 判断以下陈述的真假。(1)
  - a. 以下是一个有效的 C++ 枚举类型：(1)
    ```cpp
    enum romanNumerals {I, V, X, L, C, D, M};
    ```
  - b. 给定声明：
    ```cpp
    enum cars {FORD, GM, TOYOTA, HONDA};
    cars domesticCars = FORD;
    ```
    语句
    ```cpp
    domesticCars = domesticCars + 1;
    ```
    将 `domesticCars` 的值设置为 GM。(1, 2)
  - c. 枚举类型取值域中的值称为枚举量。(1)
  - d. 枚举类型允许的唯一算术运算是递增和递减。(2)
  - e. 可以直接从标准输入设备输入枚举类型的值。(4)
  - f. 函数可以返回枚举类型的值。(6)
  - g. 以下是在 C++ 程序同一块中合法的 C++ 语句：(1)
    ```cpp
    enum mathStudent {BILL, JOHN, LISA, RON, CINDY, SHELLY};
    enum historyStudent {AMANDA, BOB, JACK, TOM, SUSAN};
    ```
  - h. 以下语句创建匿名类型：(8)
    ```cpp
    enum {A, B, C, D, F} studentGrade;
    ```
  - i. 可以将 `namespace` 机制与扩展名为 h 的头文件一起使用。(10)
  - j. 假设 `str = "ABCD";`。在执行语句 `str[1] = 'a';` 后，`str` 的值为 `"aBCD"`。(11)
  - k. 假设 `str = "abcd"`。在执行语句：
    ```
    str = str + "ABCD";
    ```
    后，`str` 的值为 `"ABCD"`。(11)

- 2. 编写完成以下操作的 C++ 语句：(1, 2, 3, 4, 5)
  - a. 定义一个枚举类型 birdType，其值为 PEACOCK、SPARROW、CANARY、PARROT、PENGUIN、OSTRICH、EAGLE、CARDINAL 和 HUMMINGBIRD。
  - b. 声明一个类型为 birdType 的变量 bird。
  - c. 将 CANARY 赋给变量 bird。
  - d. 将 bird 推进到列表中的下一个值。
  - e. 将 bird 递减到列表中的前一个值。
  - f. 输出变量 bird 的值。
  - g. 向变量 bird 中输入值。

- 3. 给定：
  ```
  enum currencyType {DOLLAR, POUND, FRANK, LIRA, MARK};
  currencyType currency;
  ```
  下列哪些语句有效？(1, 2, 3, 4, 5)
  - a. currency = DOLLAR;
  - b. cin >> currency;
  - c. currency = static_cast<currencyType>(currency + 1);
  - d. for (currency = DOLLAR; currency <= MARK; currency++)
       cout << "*";

- 4. 考虑以下声明：
  ```
  enum fruitType {ORANGE, APPLE, BANANA, GRAPE, STRAWBERRY, MANGO, GUAVA,
       PINEAPPLE, KIWI};
  fruitType fruit;
  ```
  回答以下问题。(1, 2, 3, 5)
  - a. static_cast<int>(STRAWBERRY) 的值是多少？
  - b. 以下表达式的值（如果有）是什么？
    static_cast<fruitType>(static_cast<int>(MANGO) - 2)
  - c. 以下表达式的值（如果有）是什么？
    static_cast<fruitType>(static_cast<int>(GRAPE) + 2)
  - d. 表达式 BANANA <= KIWI 的值（如果有）是什么？
  - e. 以下代码的输出（如果有）是什么？
    ```
    for (fruit = BANANA; fruit < PINEAPPLE; fruit++)
        cout << static_cast<int>(fruit) << ", ";
    cout << endl;
    ```

- 5. 假设 `enum birdType` 如练习题 2 中所定义。编写一个可用于向 `birdType` 类型变量输入值的 C++ 函数。(7)
- 6. 假设 `enum birdType` 如练习题 2 中所定义。编写一个可用于输出 `birdType` 类型变量值的 C++ 函数。(7)
- 7. 匿名类型有哪些缺点？(8)
- 8. 定义一个枚举类型 `triangleType`，其值为 `EQUILATERAL`、`RIGHT`、`ISOSCELES` 和 `SCALENE`。在定义该类型的同时，声明类型为 `triangleType` 的变量 `triangle`。(7)
- 9. 以下程序有什么问题？(10)
  ```cpp
  #include <iostream>                         //Line 1

  namespace std;                              //Line 2

  int main()                                  //Line 3
  {                                            //Line 4
      cout << "$*$" << endl;                  //Line 5

      return 0;                                //Line 6
  }                                            //Line 7
  ```
- 10. 以下程序有什么问题？(10)
  ```cpp
  #include <iostream.h>                       //Line 1

  int main()                                  //Line 2
  {                                            //Line 3
      int num;                                 //Line 4
      std::cin >> num;                         //Line 5
      std::cout << "num = " << num << endl;   //Line 6
      return 0;                                //Line 7
  }                                            //Line 8
  ```
- 11. 以下程序有什么问题？(10)
  ```cpp
  #include <iostream>                         //Line 1

  using namespace std;                         //Line 2

  int main()                                  //Line 3
  {                                            //Line 4
      int x;                                   //Line 5

      std::cin >> x;                           //Line 6
      cout << "x = " << x << endl;             //Line 7

      return 0;                                //Line 8
  }                                            //Line 9
  ```

