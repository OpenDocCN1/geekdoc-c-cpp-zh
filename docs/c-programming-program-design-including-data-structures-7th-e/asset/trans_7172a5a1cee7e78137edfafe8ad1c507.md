
## 27. 考虑以下类 MyClass 的定义：（11）

```cpp
class myClass
{
public:
    void setX(int a);
        //Function to set the value of x.
        //Postcondition: x = a;
    void printX() const;
        //Function to output x.
    static void printCount();
        //Function to output count.
    static void incrementCount();
        //Function to increment count.
        //Postcondition: count++;
    myClass(int a = 0);
        //constructor with default parameters
        //Postcondition: x = a;
        //If no value is specified for a, x = 0;

private:
    int x;
    static int count;
};
```

- a. 编写一条 C++ 语句，将成员变量 count 初始化为 0。
- b. 编写一条 C++ 语句，将 count 的值增加 1。
- c. 编写一条 C++ 语句，输出 count 的值。
- d. 按照类 myClass 定义中的描述，编写该类函数的定义。
- e. 编写一条 C++ 语句，声明 myObject1 为一个 myClass 对象，并将其成员变量 x 初始化为 5。
- f. 编写一条 C++ 语句，声明 myObject2 为一个 myClass 对象，并将其成员变量 x 初始化为 7。
- g. 以下哪些语句是合法的？（假设 myObject1 和 myObject2 如 e 和 f 部分所声明。）

```cpp
myObject1.printCount();    //Line 1
myObject1.printX();        //Line 2
myClass.printCount();      //Line 3
myClass.printX();          //Line 4
myClass::count++;          //Line 5
```

- h. 假设 myObject1 和 myObject2 如 e 和 f 部分所声明。以下 C++ 代码的输出是什么？

```cpp
myObject1.printX();
cout << endl;
myObject1.incrementCount();
myClass::incrementCount();
myObject1.printCount();
cout << endl;
myObject2.printCount();
cout << endl;
myObject2.printX();
cout << endl;
myObject1.setX(14);
myObject1.incrementCount();
myObject1.printX();
cout << endl;
myObject1.printCount();
cout << endl;
myObject2.printCount();
cout << endl;
```

## 28. 在示例 10–9 中，我们设计了类 die。使用这个类，声明一个名为 rolls、包含 100 个 die 类型分量的数组。编写 C++ 语句来掷数组 rolls 中的每个 die，找出并输出掷出的最大数字以及该数字被掷出的次数，并找出并输出被掷出次数最多的数字及其次数。还要编写一个程序来测试你的语句。（1, 3）

## 编程练习

- 1. 第 9 章定义了结构体 studentType，以实现学生的基本属性。定义一个类 studentType，其组成部分与结构体 studentType 相同，并添加成员函数来操作数据成员。（注意，类 studentType 的数据成员必须是私有的。）编写一个程序说明如何使用类 studentType。

- 2. 编写一个程序，使用练习 11 和 12 中定义的类 houseType。

- 3. 编写一个程序，说明如何使用本章练习 13 和 14 中设计的类 temporary。你的程序不应使用练习 15 和 16 中给出的语句。此外，你的程序必须包含这样的语句：要求用户输入某个对象的数据，并使用成员函数 set 初始化该对象。

- 4. 编写一个程序，将输入的罗马数字转换为正整数。你的程序应包含一个类，例如 romanType。romanType 类型的对象应执行以下操作：

  - a. 将该数字存储为罗马数字。
  - b. 将该数字转换并存储为正整数。
  - c. 根据用户要求，将该数字打印为罗马数字或正整数。

  罗马数字的整数值如下：

  | 罗马数字 | 值 |
  |---|---:|
  | M | 1000 |
  | D | 500 |
  | C | 100 |
  | L | 50 |
  | X | 10 |
  | V | 5 |
  | I | 1 |

  - d. 使用以下罗马数字测试你的程序：MCXIV、CCCLIX、MDCLXVI。

- 5. 设计并实现一个**类** `dayType`，在程序中实现星期几。**类** `dayType` 应存储星期几，例如用 Sun 表示星期日。程序应能对 `dayType` 类型的对象执行以下操作：

  - a. 设置星期几。
  - b. 打印星期几。
  - c. 返回星期几。
  - d. 返回下一天。
  - e. 返回前一天。
  - f. 通过向当前日期加上若干天来计算并返回星期几。例如，如果当前天是星期一，加上 4 天，则返回的天是星期五。类似地，如果今天是星期二，加上 13 天，则返回的天是星期一。
  - g. 添加适当的构造函数。

- 6. 编写函数定义，以实现编程练习 5 中定义的**类** `dayType` 的操作。还要编写一个程序来测试这个**类**的各种操作。

- 7. 本章定义了**类** `clockType`，在程序中实现时间。向这个**类**添加函数，使得使用这个**类**的程序可以仅设置小时、分钟或秒，并仅获取小时、分钟或秒。还要编写一个程序来测试你的**类**。

- 8. 增强编程练习 7，向**类** `clockType` 添加函数，使得使用这个类的程序可以执行以下操作：

  - a. 返回时钟当天已经过的时间（以秒为单位）。
  - b. 返回时钟当天剩余的时间（以秒为单位）。

  ![](img/d0be7fc6d804b63484835c6c8bc67a07_781_0.png)

  - c. 确定并输出两个时钟在时间上相差多少。以 `hr:min:sec` 的形式输出时间。

  还要编写一个程序来测试你的类。

- 9. 示例 10-10 定义了类 `personType` 来存储一个人的姓名。我们包含的成员函数仅打印姓名和设置一个人的姓名。重新定义类 `personType`，使得除了现有类所做的之外，还可以：

  - a. 仅设置名。
  - b. 仅设置姓。
  - c. 存储并设置中间名。
  - d. 检查给定的名是否与此人的名相同。
  - e. 检查给定的姓是否与此人的姓相同。

  编写成员函数的定义，以实现这个类的操作。还要编写一个程序来测试这个类的各种操作。

- 10.
  - a. 一本书的一些特征包括书名、作者、出版社、ISBN、价格和出版年份。设计一个类 `bookType`，将书定义为 ADT。
    - i. 类 `bookType` 的每个对象可以保存一本书的以下信息：书名、最多四位作者、出版社、ISBN、价格和库存副本数。为了跟踪作者数量，再添加一个成员变量。
    - ii. 包含成员函数，以对 `bookType` 类型的对象执行各种操作。例如，可以对书名执行的常见操作包括显示书名、设置书名，以及检查某个书名是否与书的实际书名相同。类似地，可以对库存副本数执行的典型操作包括显示库存副本数、设置库存副本数、更新库存副本数，以及返回库存副本数。为出版社、ISBN、书价和作者添加类似操作。添加适当的构造函数和析构函数（如果需要）。
  - b. 编写类 `bookType` 的成员函数的定义。
  - c. 编写一个程序，使用类 `bookType` 并测试类 `bookType` 对象上的各种操作。声明一个包含 100 个 `bookType` 类型分量的数组。你应该执行的一些操作包括按书名查找一本书、按 ISBN 查找，以及更新一本书的副本数。

- 11. 在本练习中，你将设计一个类 `memberType`。
  - a. `memberType` 的每个对象可以保存某人的姓名、会员 ID、已购书籍数量和消费金额。

