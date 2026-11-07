
- 15. 在 `namespace` 外部访问 `namespace` 成员的一种方法是在 `namespace` 成员名之前加上 `namespace` 名称和作用域解析运算符。
- 16. 在 C++ 中，`namespace` 是保留字。
- 17. 要使用 `namespace` 机制，程序必须包含 ANSI/ISO 标准 C++ 头文件——即不带扩展名 h 的头文件。
- 18. `using` 语句简化了对 `namespace` 成员的访问。
- 19. 在 C++ 中，`using` 是保留字。
- 20. 关键字 `namespace` 必须出现在 `using` 语句中。
- 21. 当不使用 `using` 语句访问 `namespace` 成员时，`namespace` 名称和作用域解析运算符必须位于该 `namespace` 成员名称之前。
- 22. 若要使用标准头文件中声明的标识符而不带 `namespace` 名称，则在包含所有必要的头文件之后，程序中必须出现以下语句：
  
  ```cpp
  using namespace std;
  ```
  
- 23. 字符串是由零个或多个字符组成的序列。
- 24. C++ 中的字符串用双引号括起来。
- 25. 要使用 `string` 类型，程序必须包含头文件 `string`。程序中使用的其他头文件应为 ANSI/ISO 标准 C++ 风格的头文件。
- 26. 赋值运算符可用于 `string` 类型。
- 27. 运算符 `+` 可用于连接两个 `string` 类型的值。要使运算符 `+` 能用于字符串数据类型，`+` 的操作数之一必须是字符串变量。
- 28. 第 4 章讨论的关系运算符可应用于 `string` 类型。
- 29. 在字符串中，第一个字符的位置是 0，第二个字符的位置是 1，依此类推。
- 30. 字符串的长度是字符串中的字符数。
- 31. 在 C++ 中，`[]` 称为数组下标运算符。
- 32. 要访问字符串中的单个字符，请将数组下标运算符与该字符的位置一起使用。
- 33. `string` 类型包含 `at`、`append`、`clear`、`compare`、`erase`、`find`、`find_first_of`、`find_first_not_of`、`insert`、`length`、`replace`、`size`、`substr` 和 `swap` 等函数，用于操作字符串。这些函数在表 7-1 中描述。

## 练习

习题末尾括号中的数字指本章开头列出的学习目标。

- 1. 判断以下陈述的真假。 (1)
  - a. 以下是一个有效的 C++ 枚举类型： (1)
    
    ```cpp
    enum romanNumerals {I, V, X, L, C, D, M};
    ```
    
  - b. 给定以下声明：
    
    ```cpp
    enum cars {FORD, GM, TOYOTA, HONDA};
    cars domesticCars = FORD;
    ```
    
    则语句：
    
    ```cpp
    domesticCars = domesticCars + 1;
    ```
    
    会将 `domesticCars` 的值设置为 GM。 (1, 2)
    
  - c. 枚举类型取值域中的值称为枚举量。 (1)
  - d. 枚举类型唯一允许的算术运算是递增和递减。 (2)
  - e. 可以直接从标准输入设备输入枚举类型的值。 (4)
  - f. 函数可以返回枚举类型的值。 (6)
  - g. 以下语句在 C++ 程序的同一代码块中是合法的 C++ 语句： (1)
    
    ```cpp
    enum mathStudent {BILL, JOHN, LISA, RON, CINDY, SHELLY};
    enum historyStudent {AMANDA, BOB, JACK, TOM, SUSAN};
    ```
    
  - h. 以下语句创建一个匿名类型： (8)
    
    ```cpp
    enum {A, B, C, D, F} studentGrade;
    ```
    
  - i. 假设 `str = "ABCD"`。执行语句 `str[1] = 'a';` 后，`str` 的值为 `"aBCD"`。 (11)
  - j. 假设 `str = "abcd"`。执行以下语句后：
    
    ```cpp
    str = str + "ABCD";
    ```
    
    `str` 的值为 `"abcdABCD"`。 (11)

- 2. 编写完成以下操作的 C++ 语句： (1, 2, 3, 4, 5)
  - a. 定义一个枚举类型 `flowerType`，其值为 `ROSE`、`DAISY`、`CARNATION`、`FREESIA`、`GARDENIA`、`ALUM`、`TULIP`、`IRIS`、`SUNFLOWER`、`LILAC` 和 `ORCHID`。
  - b. 声明一个 `flowerType` 类型的变量 `flower`。
  - c. 将 `TULIP` 赋给变量 `flower`。
  - d. 使用 c 部分将 `IRIS` 赋给 `flower`。
  - e. 将 `flower` 递减到列表中的前一个值。
  - f. 输出变量 `flower` 的值。
  - g. 向变量 `flower` 中输入值。

- 3. 给定：
  
  ```cpp
  enum currencyType {DOLLAR, POUND, FRANC, LIRA, MARK};
  currencyType currency;
  ```
  
  以下哪些语句是合法的？ (1, 2, 3, 4, 5)
  
  - a. `currency = DOLLAR;`
  - b. `cin >> currency;`
  - c. `currency = static_cast<currencyType>(currency + 1);`
  - d. `for (currency = DOLLAR; currency <= MARK; currency++)`
    `cout << "* ";`

- 4. 考虑以下声明：
  
  ```cpp
  enum fruitType {ORANGE, APPLE, BANANA, GRAPE, STRAWBERRY,
                  MANGO, GUAVA, PINEAPPLE, KIWI};
  fruitType fruit;
  ```
  
  回答以下问题。 (1, 2, 3, 5)
  
  - a. `static_cast<int>(STRAWBERRY)` 的值是什么？
  - b. 以下表达式的值（如果有）是什么？
    `static_cast<fruitType>(static_cast<int>(MANGO) - 2)`
  - c. 以下表达式的值（如果有）是什么？
    `static_cast<fruitType>(static_cast<int>(GRAPE) + 2)`
  - d. 表达式 `BANANA <= KIWI` 的值（如果有）是什么？
  - e. 以下代码的输出（如果有）是什么？
    
    ```cpp
    for (fruit = BANANA; fruit < PINEAPPLE; fruit++)
        cout << static_cast<int>(fruit) << ", ";
    cout << endl;
    ```

- 5. 假设 `enum flowerType` 如练习 2 中所定义。编写一个 C++ 函数，用于向 `flowerType` 类型的变量中输入值。 (7)

- 6. 假设 `enum flowerType` 如练习 2 中所定义。编写一个 C++ 函数，用于输出 `flowerType` 类型的变量的值。 (7)

- 7. 匿名类型有哪些缺点？ (8)

- 8. 定义枚举类型 **quadrilateralType**，其值为 **SQUARE**、**RECTANGLE**、**RHOMBUS**、**TRAPEZOID**、**PARALLELOGRAM**、**QUADRILATERAL** 和 **KITE**。同时在定义该类型时声明 **quadrilateralType** 类型的变量 **quadrilateral**。 (7)

- 9. 以下程序有什么错误？ (10)
  
  ```cpp
  #include <istream>                         //Line 1
  
  using namespace std;                        //Line 2
  
  int main()                                  //Line 3
  {                                           //Line 4
      cout << "$0$" << endl;                  //Line 5
  
      return 0;                               //Line 6
  }                                           //Line 7
  ```

- 10. 以下程序有什么错误？ (10)
  
  ```cpp
  #include <iostream>                         //Line 1
  #include <strings>                          //Line 2
  
  int main()                                  //Line 3
  {                                           //Line 4
      string str;                             //Line 5
      std::cin >> str;                        //Line 6
      cout << str << endl;                    //Line 7
      return 0;                               //Line 8
  }                                           //Line 9
  ```

- 11. 以下程序有什么错误？ (10)
  
  ```cpp
  #include <iostream>                         //Line 1
  
  using namespace sdt;                        //Line 2
  
  int main()                                  //Line 3
  {                                           //Line 4
      int x;                                  //Line 5
      std::cin >> x;                          //Line 6
      cout << "x = " << x << endl;            //Line 7
  
      return;                                 //Line 8
  }                                           //Line 9
  ```

- 12. 以下程序有什么错误？ (10)
  
  ```cpp
  #include <iostream>                         //Line 1
  
  using namespace mySpace                     //Line 2
  {                                           //Line 3
      const double PRIZE = 50000.00;          //Line 4
      int x;                                  //Line 5
  }                                           //Line 6
  ```
