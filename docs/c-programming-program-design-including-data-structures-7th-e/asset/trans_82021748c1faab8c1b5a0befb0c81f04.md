
- 31. 复制构造函数生成实际变量的副本。
- 33. 具有指针数据成员的类应包含析构函数，重载赋值运算符，并通过在类定义中包含复制构造函数并提供其定义来显式提供复制构造函数。
- 35.
    ```text
    ClassA x: 4

    ClassA x: 6
    ClassB y: 10
    ```
- 37. 是。
- 39.
    - a. 因为 employeeType 是抽象类，所以不能实例化该类的对象。因此，这条语句非法。
    - b. 这条语句合法。
    - c. 这条语句合法。

## 第13章
- 1. a. 真；b. 假；c. 真；d. 假；e. 假；f. 假；g. 假；h. 假；i. 真；j. 假；k. 假；l. 真；m. 真
- 3. `.`、`.*`、`::`、`?:` 和 `sizeof`
- 5. 语句 `return this;` 返回对象的地址，而语句 `return *this;` 返回对象的值。
- 7. 友元函数是类的非成员，而成员函数是类的成员。
- 9. 因为 << 的左操作数是流对象，它不是 mystery 类型。
- 11. `()`、`[]`、`->` 和 `=`
- 13.
    ```cpp
    a. friend strange operator+(const strange&, const strange&);
    b. friend bool operator==(const strange&, const strange&);
    c. friend strange operator<<(strange&, int&);
    ```
- 15. 在第4行中，函数 `operator*` 的返回类型应为 `temp`。正确的语句是：
    ```cpp
    temp operator*(const temp& obj);        //Line 4
    ```
- 17. 在第3行中，函数 `operator<` 的返回类型应为 `bool`。正确的语句是：
    ```cpp
    friend bool operator<(const mystery& a,
                         const mystery& b);  //Line 3
    ```
- 19. 在第3行和第11行中，函数 `operator+` 的返回类型应为 `discover`。另外，由于 `operator+` 是该类的友元函数，第11行函数头中的类名和作用域解析运算符不需要。正确的语句是：
    ```cpp
    friend discover operator+(const discover&,
                             const discover&);        //Line 3
    ```
    ```cpp
    discover operator+(const discover& a,
                       const discover& b)        //Line 11
    ```
- 21. 对类 `istream` 对象的引用。
- 23. 假设一个类（例如 `temp`）重载了前置和后置自增运算符 `++`，并且 `tempObj` 是类 `temp` 的对象。那么，语句 `++tempObj;` 被编译为 `tempObj.operator++();`，而语句 `tempObj++;` 被编译为 `tempObj.operator++(0);`。哑参数用于区分前置和后置自增运算符函数。前置和后置自增运算符也采用类似的约定。
- 25. 无。
- 27. 一个。
- 29. 这个问题的答案可在本书配套网站上获取。
- 31. 当类具有指针数据成员时。
- 33. 第4行有错误。模板实例化只能针对内置类型或用户定义类型。尖括号之间的单词“type”必须替换为内置类型或用户定义类型。
- 35. a. 12 b. Sunny Day
- 37.
    ```cpp
    template <class Type>
    void swap(Type &x, Type &y)
    {
        Type temp;
        temp = x;
        x = y;
        y = temp;
    }
    ```

## 第14章
- 1. a. 假；b. 真；c. 真；d. 假；e. 真；f. 假；g. 假；h. 真；i. 假；j. 真；k. 假；l. 真；m. 假
- 3. 程序将终止并显示一条错误消息。
- 5. 如果在 try 块中抛出异常，该 try 块中的其余语句将被忽略。程序按 catch 块在 try 块之后出现的顺序搜索这些 catch 块，并寻找合适的异常处理器。如果抛出的异常类型与某个 catch 块中的参数类型匹配，则执行该 catch 块的代码，并忽略该 catch 块之后的其余 catch 块。
- 7. 至多一个。
- 9. `throw expression;`
    其中 expression 是常量值、变量或对象。
- 11. `catch` 块没有关联的 `try` 块，也就是说，该 `catch` 块没有跟在任何 `try` 块之后。另外，`try` 块没有关联的 `catch` 块，也就是说，该 `try` 块之后没有 `catch` 块。`catch` 块之前的 cout 语句使 `catch` 块与 `try` 块分离。正确的代码是：
    ```cpp
    double radius;

    try
    {
        cout << "Enter the radius: ";
        cin >> radius;
        cout << endl;

        if (radius < 0.0)
            throw radius;

        cout << "Area: " << 3.1416 * radius * radius << endl;
    }
    catch (double x)
    {
        cout << "Negative radius: " << x << endl;
    }
    ```
- 13.
    - a. 离开 `try` 块。
    - b. 当前余额：975
         余额必须大于 1000.00
    - c. 当前余额：-2000
         余额必须大于 1000.00
- 15.
    - a. 进入 `try` 块。
         异常：违反下限。
         在 `catch` 块之后
    - b. 进入 `try` 块。
         异常：0
         在 `catch` 块之后
    - c. 进入 `try` 块。
         退出 `try` 块。
         在 `catch` 块之后
    - d. 进入 `try` 块。
         异常：0
         在 `catch` 块之后
- 17. 无效参数
- 19. throw 语句。
- 21. （假设类 `tornadoException` 的定义在头文件 tornadoException.h 中。）
    ```cpp
    #include <iostream>
    #include "tornadoException.h"

    using namespace std;

    int main()
    {
        int miles;

        try
        {
            cout << "Enter the miles: ";
            cin >> miles;
            cout << endl;

            if (miles < 5)
                throw tornadoException();
            else
                throw tornadoException(miles);
        }
        catch (tornadoException tE)
        {
            cout << tE.what() << endl;
        }

        return 0;
    }
    ```
- 23. 函数在其函数头中使用 throw 子句指定它抛出的异常。
- 25. (1) 什么都不做；(2) 部分处理异常并抛出同一异常或新异常；(3) 抛出新的异常。

## 第15章
- 1. a. 真；b. 真；c. 假；d. 假；e. 假；f. 假；g. 真；h. 真
- 3. 解用其自身更小版本来定义的情况。
- 5. 一个函数调用另一个函数并最终导致原函数调用，称为间接递归。
- 7.
    - a. 第2行和第3行中的语句。
    - b. 第4行和第5行中的语句。
    - c. 任何非正整数。
    - d. 这是一个有效调用。mystery(0) 的值为 0。
    - e. 这是一个无效调用。它将导致无限递归。
    - f. 这是一个有效调用。mystery(-3) 的值为 6。
- 9. a. 8 5 2  b. 7  c. 6 3  d. -85
- 11.
    - a. 它不产生任何输出。
    - b. 5 6 7 8 9
    - c. 它不产生任何输出。
    - d. 它不产生任何输出。
- 13. a. 2；b. 3；c. 5；d. 21
- 15. a. 10  b. 21  c. −23  d. 2  e. −56
- 17. $\operatorname{multiply}(m,n)=\begin{cases}0 & \text{if } n=0\\m & \text{if } n=1\\m+\operatorname{multiply}(m,n-1) & \text{otherwise}\end{cases}$

    基本情况是 $n=0$ 或 $n=1$。一般情况由 otherwise 选项指定。

## 第16章
- 1. a. 真；b. 假；c. 假；d. 假；e. 假；f. 真；g. 真；h. 假；i. 假；j. 真；k. 真；l. 假；m. 假；n. 真
- 3. `nullptr`
- 5. 删除前，第三个结点的链接字段存储第四个结点的地址。删除后，第三个结点的链接字段将存储下一个结点（即原来的第五个结点）的地址。如果没有第五个结点，那么删除后，链接字段将存储值 `nullptr`。因此，删除第四个结点后，第三个结点的链接字段发生了变化。所以需要一个指向第三个结点的指针。
- 7. a. 假；b. 真；c. 真；d. 真；e. 真
- 9.
    ```text
    a. current->link->info = 52;
    b. current = temp->link;
    c. trail = current->link;
    d. temp = nullptr;
    e. temp->link->link->link->info = 36;
    f. while (current->info != 10)
           current = current->link;
    ```
- 11.
    ```text
    a. while (current != nullptr)
           current = current->link;

    b. temp = new nodeType;
       temp->info = 68;
       temp->link = last;
       trail->link = temp;

    c. delete last;
       trail->link = nullptr;
       last = trail;

    d. trail = temp->link;
       temp->link = trail->link;
       delete trail;
    ```
