

## 练习

- 1. 判断下列陈述为真还是假。
  - a. 类的成员变量必须是相同类型。
  - b. 类的成员函数必须是公有的。
  - c. 一个类可以有多个构造函数。
  - d. 一个类可以有多个析构函数。
  - e. 构造函数和析构函数都可以有参数。

- 2. 找出以下类定义中的语法错误：

```
class mystery                         //Line 1
{
public:                                //Line 3
    void print() const;                //Line 4
    void setNum(double, double);       //Line 5
    int power();                        //Line 6
    double mystery();                   //Line 7
    double mystery(double, double);     //Line 8
private:                               //Line 9
    double x;                           //Line 10
    double y;                           //Line 11
};                                     //Line 12
```

- 3. 找出以下类定义中的语法错误：

```
class secret                         //Line 1
{
public:                                //Line 3
    bool multiply();                    //Line 4
    print() const;                      //Line 5
    secret(int = 0, int = 0);           //Line 6
private:                                //Line 7
    int one;                             //Line 8
    int two;                             //Line 9
};                                     //Line 10
```

- 4. 找出以下类定义中的语法错误：

```
class secret                         //Line 1
{
public:                                //Line 3
    bool compare();                     //Line 4
    void print() const;                 //Line 5
    secret(int = 0, int = 0) const;     //Line 6
private:                                //Line 7
    string str;                          //Line 8
    int one;                             //Line 9
    int two;                             //Line 10
};                                     //Line 11
```

- c. 编写类 `bagType` 的默认构造函数定义，使私有成员变量分别初始化为 `""`、`0.0`、`0.0`、`0.0`、`0.0`。

- d. 编写一条 C++ 语句，打印对象 `newBag` 的值。

- e. 编写一条 C++ 语句，声明 `bagType` 类型的对象 `tempBag`，并将 `tempBag` 的成员变量分别初始化为 `"backPack"`、`15`、`8`、`20` 和 `49.99`。

- 8. 考虑以下类的定义：

```
class employee                                      //Line 1
{
public:                                             //Line 3
    employee();                                     //Line 4
    employee(string, int, double);                  //Line 5
    employee(int, double);                          //Line 6
    employee(string);                               //Line 7

    void setData(string, int, double);              //Line 8
    void print() const;                             //Line 9
    void updatePay(double x);                       //Line 10
    int getNumOfServiceYears() const;               //Line 11
    double getPay() const;                          //Line 12

private:                                            //Line 13
    string name;                                    //Line 14
    int numOfServiceYears;                          //Line 15
    double pay;                                     //Line 16
};                                                  //Line 17
```

  - a. 对于以下每个声明，给出其所执行的构造函数所在的行号：
    - i. `employee tempEmployee;`
    - ii. `employee newEmployee("Harry Miller", 0, 25000);`
    - iii. `employee oldEmployee("Bill Dunbar", 15, 55000);`
  - b. 编写第4行中构造函数的定义，使实例变量分别初始化为 `""`、`0` 和 `0.0`。
  - c. 编写第5行中构造函数的定义，使实例变量根据参数进行初始化。
  - d. 编写第6行中构造函数的定义，使实例变量 `name` 被初始化为空字符串，其余实例变量根据参数进行初始化。

- 9. 考虑习题8中给出的类 `employee` 的定义。哪些函数成员是访问器，哪些是修改器？

- 10. 考虑习题8中给出的类 `employee` 的定义。回答以下问题：

  - a. 编写函数 setData 的定义，使实例变量根据参数进行设置。
  - b. 编写函数 print 的定义，输出实例变量的值。
  - c. 编写函数 updatePay 的定义，将参数的值加到实例变量 pay 上以更新其值。
  - d. 编写函数 getNumOfServiceYears 的定义，返回实例变量 numOfServiceYears 的值。
  - e. 编写函数 getPay 的定义，返回实例变量 pay 的值。
  - f. 编写一个程序来测试类 employee。

- 11. 考虑以下语句：

```cpp
class temporary
{
public:
    void set(string, double, double);
    void print();
    double manipulate();
    void get(string&, double&, double&);
    void setDescription(string);
    void setFirst(double);
    void setSecond(double);
    string getDescription() const;
    double getFirst() const;
    double getSecond() const;

    temporary(string = "", double = 0.0, double = 0.0);

private:
    string description;
    double first;
    double second;
};
```

  - a. 类 temporary 有多少个成员？
  - b. 类 temporary 有多少个私有成员？
  - c. 类 temporary 有多少个构造函数？这个构造函数能否在不指定任何参数的情况下用于初始化对象？如果可以，请举例说明；否则，请解释为什么不能在不指定任何参数的情况下用于初始化对象。

- 12. 假设类 temporary 的定义如习题11所示。回答以下问题：

  - a. 编写成员函数 set 的定义，使实例变量根据参数进行设置。
  - b. 编写成员函数 `manipulate` 的定义，返回一个小数，规则如下：如果 `description` 的值为 "rectangle"，则返回 `first * second`；如果 `description` 的值为 "circle"，则返回半径为 `first` 的圆的面积；如果 `description` 的值为 "sphere"，则返回半径为 `first` 的球的体积；如果 `description` 的值为 "cylinder"，则返回半径为 `first`、高为 `second` 的圆柱的体积；否则返回 `-1`。
  - c. 编写函数 `print` 的定义，打印实例变量的值以及函数 `manipulate` 返回的值。例如，如果 `description = "rectangle"`、`first = 8.5`、`second = 5`，则应打印：

```
rectangle: length = 8.50, width = 5.00, area = 42.50
```

  - d. 编写构造函数的定义，使其使用函数 set 初始化实例变量。
  - e. 编写其余用于设置或获取实例变量值的函数定义。请注意，函数 `get` 返回所有实例变量的值。

- 13. 假设类 `temporary` 的定义如习题11所示。以下语句的效果是什么？

```
temporary object1;
temporary object2("rectangle", 3.0, 5.0);    //Line 2
temporary object3("circle", 6.5, 0.0);       //Line 3
temporary object4("cylinder", 6.0, 3.5);     //Line 4
```

- 14. 假设类 `temporary` 的定义如习题11所示，且成员函数和构造函数的定义如习题12所指定。以下语句的输出是什么？

```
temporary object1;
temporary object2("rectangle", 8.5, 5);
temporary object3("circle", 6, 0);
temporary object4("cylinder", 6, 3.5);

cout << fixed << showpoint << setprecision(2);

object1.print();
object2.print();
object3.print();
object4.print();

object1.set("sphere", 4.5, 0);
object1.print();
```

- 15. 类的内置操作有哪些？

- 16. `struct` 和 `class` 之间的主要区别是什么？

