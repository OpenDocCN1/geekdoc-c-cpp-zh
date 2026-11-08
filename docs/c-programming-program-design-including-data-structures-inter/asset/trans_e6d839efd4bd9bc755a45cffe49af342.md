

**5.** 考虑以下语句：

```cpp
class molecules: atom
{
    ...
};
```

- a. 在此声明中，哪个类是基类，哪个类是派生类？
- b. 这是哪种类型的继承？

**6.** 考虑以下语句：

```cpp
class pigeon: public bird
{
    ...
};
```

- a. 在此声明中，哪个类是基类，哪个类是派生类？
- b. 这是哪种类型的继承？

**7.** 考虑以下类定义：

```cpp
class circle
{
public:
    void print() const;
    void setRadius(double);
    void setCenter(double, double);
    double getRadius();
    double area();
    circle();
    circle(double, double);
    circle(double, double, double);
private:
    double xCoordinate;
    double yCoordinate;
    double radius;
};
```

```cpp
class cylinder: public circle
{
public:
    void print() const;
    void setHeight(double);
    double getHeight();
    double volume();
    double area();
    cylinder();
    cylinder(double, double);
private:
    double height;
};
```

假设你有以下声明：

```cpp
cylinder newCylinder;
```

确定对象 newCylinder 的私有成员。

**8.** 假设你有习题 7 中的声明。编写类 circle 和 cylinder 的成员函数的定义。指出类 cylinder 中哪些成员函数重写了类 circle 的成员函数。

**9.** 考虑以下类定义：

```cpp
class temp
{
public:
    void print() const;
    void setDescription(string);
    void setX(double);
    string getDescription();
    double getX();
    temp();
    temp(string, double);

private:
    string description;
    double x;
};
```

以下类定义有什么错误？

```cpp
class derivedFromTemp public temp
{
public:
    void print();
    void setX(double);
    double getZ();
    double power();
        //returns z to the power of z.

private:
    double z;
};
```

**10.** 假设类 temp 的定义如习题 9 所示。考虑以下类定义：

```cpp
class derivedFromTemp: public temp;
{
public:
    void print();
        //outputs the values of all the instance variables.
    void setZ(double);
        //sets the value of z according to the parameter.
    double getZ();
        //returns the value of z.
    double power() const;
        //returns z to the power of z.

    derivedFromTemp();
        //sets the values of instance variables to "",
        //0.0, and 0.0, respectively.
    derivedFromTemp(string, double, double);
        //sets the values of instance variables according
        //to the parameters.
private:
    double z;
};
```

- a. 找出并改正类 `derivedFromTemp` 定义中的错误（如果有）。同时给出该类的正确声明。
- b. 在改正类 `derivedFromTemp` 定义中的错误（如果有）之后，编写类 `derivedFromTemp` 的成员函数的定义。

**11.** 考虑以下语句：

```cpp
class base
{
public:
    void print() const;
    void set(int, int);
    void get(int&, int&);
    base();
    base(int, int);

private:
    int a;
    int b;
};

class derived: public base
{
public:
    :
    :
    :
    :

private:
    int c;
};
```

- a. 假设类 `derived` 重写了类 `base` 的函数 `print`。类 `derived` 中函数 `print` 的函数头是什么？
- b. 假设类 `derived` 重载了类 `base` 的函数 `set` 和 `get`。这些函数在类 `derived` 中的函数头是什么？

**12.** 解释在派生类中重写基类成员函数与重载基类成员函数之间的区别。

**13.** 假设类 `three` 派生自类 `two`，类 `two` 派生自类 `one`，并且每个类都有实例变量。假设类 `three` 的一个对象进入其作用域，因此这些类的构造函数将执行。确定这些类的构造函数的执行顺序。

**14.** 考虑以下类定义：

```cpp
class smart
{
public:
    void print() const;
    void set(int, int);
    int sum();
    smart();
    smart(int, int);
private:
    int x;
    int y;
    int secret();
};

class superSmart: public smart
{
public:
    void print() const;
    void set(int, int, int);
    int manipulate();
    superSmart();
    superSmart(int, int, int);
private:
    int z;
};
```

- a. smart 的哪些私有成员（如果有）是 superSmart 的公有成员？
- b. 类 smart 的哪些成员、函数和/或数据在类 superSmart 中可直接访问？

**15.** 假设类 smart 和 superSmart 的定义如习题 14 所示。假设以下语句位于用户程序（客户端代码）中：

```cpp
smart smartObject;
superSmart superSmartObject;
```

将以下语句标记为有效或无效。如果语句无效，请解释原因。

- a.

```cpp
int smart::sum()
{
    return x + y + z;
}
```

- b.

```cpp
smartObject.secret();
superSmartObject.z = 0;
```

- c.

```cpp
void superSmart::set(int a, int b, int c)
{
    smart::set(a, b);
    z = c;
}
```

- d. 假设以下语句位于用户程序中：

```cpp
smart.print();
```

- e. 假设以下语句位于用户程序中：

```cpp
cout << superSmart.sum() << superSmart.z << endl;
```

**16.** 假设有习题 14 中的声明。

- a. 编写 `smart` 的默认构造函数的定义，使 `smart` 的实例变量初始化为 0。
- b. 编写 `superSmart` 的默认构造函数的定义，使 `superSmart` 的实例变量初始化为 0。
- c. 编写 `smart` 的成员函数 `set` 的定义，使实例变量根据参数初始化。
- d. 编写类 `smart` 的成员函数 `sum` 的定义，使其返回实例变量之和。
- e. 编写类 `superSmart` 的成员函数 `manipulate` 的定义，使其返回 `(x + y)^z`，即返回 `x` 加 `y` 的 `z` 次方。

**17.** 解释在私有继承中，基类的成员是如何被派生类继承的。

**18.** 解释在保护继承中，基类的成员是如何被派生类继承的。

**19.** 解释在公有继承中，基类的成员是如何被派生类继承的。

**20.** 解释类的私有成员与保护成员之间的区别。

**21.** 解释类的保护成员与公有成员之间的区别。

**22.** 考虑以下类定义：

```cpp
class first
{
public:
    void setX();
    void print() const;
protected:
    int y;
    void setY(int a);
private:
    int x;
};
```

假设类 `second` 使用以下语句派生自类 `first`：

```cpp
class second: private first
```

确定类 `first` 的哪些成员在类 `second` 中是私有、保护和公有的。

**23.** 假设有习题 22 中的声明。假设类 `third` 使用以下语句派生自类 `first`：

```cpp
class third: protected first
```

确定类 `first` 的哪些成员在类 `third` 中是私有、保护和公有的。

**24.** 假设有习题 22 中的声明。假设类 `fourth` 使用以下语句派生自类 `first`：

```cpp
class fourth: public first
```

确定类 `first` 的哪些成员在类 `fourth` 中是私有、保护和公有的。

**25.** 假设有习题 22 中的声明。假设类 `fifth` 使用以下语句派生自类 `first`：

```cpp
class fifth: first
```

确定类 `first` 的哪些成员在类 `fifth` 中是私有、保护和公有的。

**26.** 以下代码有什么错误？

```cpp
class classA
{
protected:
    void setX(int a);              //Line 1
        //Postcondition: x = a;     //Line 2

private:
    int x;                          //Line 3
};                                  //Line 4

.
.
.

int main()
{
    classA aObject;                 //Line 5

    aObject.setX(4);                //Line 6
    return 0;                       //Line 7
}
```

