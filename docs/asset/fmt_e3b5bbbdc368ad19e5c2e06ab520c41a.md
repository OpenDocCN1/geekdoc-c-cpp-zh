
## 代码解读

- 在这段代码中，我们类的`display`函数以多种形式存在。
- 这种类型的多态性是通过`display`方法的函数重载实现的。
- 这些函数都具有相同的名称，但签名不同。也就是说，它们的参数组合和参数数量不同。
- 在调用`display`函数时，请记住哪个签名将调用哪个函数。

## 7.2 动态绑定与静态绑定

表 7.1 动态绑定和静态绑定

| 动态绑定 | 静态绑定 |
| --- | --- |
| 动态绑定（或延迟绑定）在运行时确定将调用哪个过程。 | 静态绑定（或早期绑定）在编译时确定将调用哪个过程。 |
| 过程内部的代码直到执行时才已知，因此称为延迟绑定。 | 过程内部的代码在执行前已知，并在执行时结合到一起，因此称为早期绑定。 |
| 在 C++ 中通过虚函数实现。 | 在 C++ 中通过普通函数调用、函数重载和运算符重载实现。 |
| 程序执行速度较慢。 | 程序执行速度较快。 |
| 它也被称为运行时多态性。 | 它也被称为编译时多态性。 |

### 代码：静态绑定

```cpp
#include <iostream>
using namespace std;
class person
{
    public:
    int age;
    void display1()
    {
        cout<<"Enter your age"<<endl;
        cin>>age;
    }
};
class student : public person
{
    public:
    int ugYear;
    void display2()
    {
        cout<<"Enter your Undergraduate Year "<<endl;
        cin>>ugYear;
    }

};
class exam: public student
{
    public:
    void check()
    {
        if((age>18) && (ugYear== 2021 || ugYear== 2022))
            cout<<"You can appear for Common Admission Test 2022"<<endl;
        else
            cout<<"Sorry, you cannot appear "<<endl;
    }

};

int main()
{
    exam e;
    cout<<"Enter your valid information"<<endl;
    e.display1();
    e.display2();
    e.check();
    return 0;
}
```

### 输出

```text
Enter your valid information
Enter your age
```

```text
21
Enter your Undergraduate Year
2024
Sorry, you cannot appear
```

### 代码解读

- 此代码表明我们类的显示函数具有多种形式。
- 静态绑定是通过函数重载实现的。
- 这些函数名称相同，但签名不同。也就是说，它们具有不同的参数组合和参数数量。
- 在调用显示函数时，请记住哪个签名调用哪个函数。
- 在这里，编译器仅在编译时才知道与函数调用关联的代码。

### 代码：动态绑定

```cpp
#include <iostream>
using namespace std;
class person
{
    public:
    virtual void display()
    {
        cout<<"Enter your age"<<endl;
    }
};
class student : public person
{
    public :
    void display()//overridden
    {
        cout<<"Enter your Undergraduate Year"<<endl;
    }
};

int main()
{
    person e;
    student s;
    cout<<"Please enter your information "<<endl;
    s.display();
    e.display();
    return 0;
}
```

### 输出

```text
Please enter your information
Enter your Undergraduate Year
Enter your age
```

### 代码解读

- 此代码表明我们类的显示函数具有多种形式。
- 静态绑定是通过函数重载实现的。
- 这些函数名称相同，但签名不同。也就是说，它们具有不同的参数组合和数量。
- 在调用显示函数时，请记住哪个签名调用哪个函数。
- 在这里，编译器仅在运行时才知道与函数调用关联的方法。

## 7.3 接口与实现

有时，由于子类的需求，代码块必须一次又一次地重新定义。为此，C++提供了接口，这些接口没有直接实现，只声明方法。让我们来看一下接口的一些特征：

- a. 不提供任何方法的实现；它们只处理声明部分。
- b. 实现接口的类也有责任实现这些方法。
- c. 我们不能在接口内部定义变量。

### 代码：使用接口

```cpp
#include <iostream>
using namespace std;
class myInterface
{
public:
virtual void Purely() = 0;
void method1()
{
cout<<"\nParent class method"<<endl;
}
};
class child1: public myInterface
{
public:
void Purely()
{
cout<<"\nParent method redefined"<<endl;
}
};

int main()
{
cout<<"\nInterfaces"<<endl;
child1 c1;
c1.Purely();
c1.method1();
return 0;
}
```

### 输出

```text
Interfaces
Parent method redefined
Parent class method
```

### 代码解读

- 这里应用了接口的概念。
- 静态绑定是通过函数重载实现的。
- 该方法在子类中重新定义，因为子类可以继承并修改属性。

以下是一些额外的术语及其定义，以使C++中的接口概念更加清晰。

- a. *虚函数*是一种在父类或基类中声明并定义、在子类中重新定义的函数类型。
- b. *纯虚函数*是一种仅声明但从未实现或重新定义的函数类型。
- c. 抽象类（ABC）是一种只有纯虚函数的类。这意味着它只被声明而从未被定义，这有助于所有子类根据需要继承和重新定义成员。这种类型的类不能通过直接创建对象来实例化，但可以通过实现接口来实例化。类的所有纯虚函数都需要被重写，否则可能会出现错误。其语法如下：

`virtual void functionName() = 0;`

### 代码：

```cpp
#include <iostream>
using namespace std;
class parentc
{
    public :
        virtual int pro()=0;
    protected:
        int avgSal=230000;
};
class PublicChild1 : public parentc
{
    public:
    virtual int pro()
    {
        return (avgSal+9000);
    }
};

class PublicChild2: public parentc
{
    public:
    virtual int pro()
    {
        return (avgSal+12000);
    }
};

int main()
{
    PublicChild1 obj1;
    PublicChild2 obj2;
    cout << "\nPublic child 1 average salary is "
         << obj1.pro() << endl;
    cout << "\nPublicchild2 average Salary is " << obj2.pro()
         << endl;
    cout<< "\n";

    return 0;
}
```

### 输出

```text
Public child 1 average salary is 239000
Publicchild2 average Salary is 242000
```

### 代码解读

- 在此代码中，我们类的虚函数具有多种形式。
- 在调用显示函数时，请记住哪个签名调用哪个函数。

### 代码：

```cpp
#include <iostream>
using namespace std;
class ABC
{
public:
virtual void Purely() = 0;
};
class child1: public ABC
{
public:
void Purely()
{
cout<<"\nParent method redefined by child1"<<endl;
}
};
class child2: public ABC
{
public:
void Purely()
{
cout<<"\nParent method redefined by child2"<<endl;
}
};
int main()
{
child1 c1;
child2 c2;
c1.Purely();
c2.Purely();
return 0;
}
```

### 输出

```text
Parent method redefined by child1
Parent method redefined by child2
```

## 7.4 函数重写与重载

现在我们转向一种我们将会经常使用的多态类型，它通过函数及其不同状态来实现。（你应该通过重新定义所创建函数的状态和类型，并观察如何使用对象进行调用来练习这个概念。）

表7.2 函数重载与函数重写

| 函数重载 | 函数重写 |
| --- | --- |
| 编译时多态实现 | 运行时多态实现 |
| 不需要继承 | 始终需要继承 |
| 函数以相同的名称但不同的签名重载 | 函数以相同的名称和签名被重写 |
| 参数类型、数量和顺序可以更改 | 参数类型、数量和顺序不需要更改 |
| 函数调用根据签名在编译时确定 | 函数调用根据签名在运行时确定 |
| 重载可以发生多次 | 重写在一个C++程序中只发生一次 |

以下示例展示了C++中函数如何被重载和重写。

### 代码：使用重载函数

```cpp
#include <iostream>
using namespace std;
void display(int i)
{
    cout << " Integer  is " << i << endl;
}
void display(double f)
{
    cout << "Float is " << f << endl;
}
void display(char const *c)
{
    cout << " The number of characters is  " << c << endl;
}

int main()
{
    cout<<"To show function overloading "<<endl;
    display(11);
    display(11.11);
    display("Eleven");
    return 0;
}
```

### 输出

```text
To show function overloading
Integer is 11
Float is 11.11
The number of characters is Eleven
```

### 代码解读

- 在此代码中，我们类的显示函数具有多种形式。
- 多态是通过函数重载实现的。
- 这些函数名称相同，但签名不同。也就是说，它们具有不同的参数组合和数量。
- 在调用显示函数时，请记住哪个签名调用哪个函数。

### 代码：加法方法的函数重载

```cpp
#include <iostream>
using namespace std;
int add(int num1, int num2) {
    return num1 + num2;
}
double add(float num1, double num2) {
    return num1 + num2;
}
int add(int num1, float num2, int num3) {
    return num1 + num2 + num3;
}
int main() {
    cout << "Addition method 1 = " << add(87, 45) << endl;
    cout << "Addition method 2 = " << add(90.5, 63.6) << endl;
    cout << "Addition method 3 = " << add(51, 5.6, 33) << endl;
    return 0;
}
```

### 输出

```text
Addition method 1 = 132

Addition method 2 = 154.1

Addition method 3 = 89
```

### 代码解读

- 此代码表明我们类的加法函数具有多种形式。
- 这种多态是通过加法方法的函数重载实现的。
- 这些函数名称相同，但签名不同。也就是说，它们具有不同的参数组合和数量。
- 在调用显示函数时，请记住哪个签名调用哪个函数。

### 代码：

```cpp
#include <iostream>
using namespace std;
```

## 7.5 友元函数和泛型函数

### 7.5.1 友元函数

友元函数是类的非成员函数，它可以像普通函数一样访问，但使用关键字`friend`声明。

### 友元函数的特性

- 使用`friend`关键字仅声明一次，可以在全局作用域或另一个类中声明。
- 它可以在类中具有任何类型的访问权限：`public`、`private`或`protected`。
- 友元函数无需任何对象或点运算符即可调用。
- 对象可以作为参数传递。
- 即使它是非成员函数，它也可以访问类的所有数据成员（包括`private`）。
- 友元关系不能被继承。

友元函数的语法如下：

```cpp
class OurClass
{
    //body
    friend returnType Myfunction(Parameters list...);
};
```

### 代码：使用友元函数

```cpp
#include <iostream>
using namespace std;
class myclass
{
    friend int myfriend(int a, int b);
};
int myfriend(int a, int b)
{
    return a+b;
}
int main()
{
    int a,b;
    cout<<"Enter numbers to add"<<endl;
    cin>>a>>b;
    cout<<"Addition gives "<<myfriend(a,b)<<endl;
    return 0;
}
```

### 输出

```text
Enter numbers to add
23
567
Addition gives 590
```

### 代码解读

- 此代码展示了如何创建友元函数。
- 此函数可以在类内声明，并在类外定义。

### 7.5.2 泛型函数

当一个普通函数需要多次使用，并且函数所作用的参数需要具有不同的数据类型时，我们可以使用 C++ 中的泛型函数来实现。这些函数充当模板，以便不同类型的参数产生所需的结果。

### 泛型函数的特性

- 类似于宏，函数体在编译时展开以接收参数。
- 源代码作为模板，因此所有函数的代码相同，但在编译不同副本时，由于参数类型不同，会产生不同的结果。
- 类模板也可以像泛型函数一样使用。
- 这些函数有助于减少函数重载。
- 如果需要，参数也可以具有默认值。

泛型函数的语法如下：

```cpp
template <typename T> T mytemplate(T parameter1, T parameter2)
{
    //template body
}
```

### 代码：泛型函数与数字交换
