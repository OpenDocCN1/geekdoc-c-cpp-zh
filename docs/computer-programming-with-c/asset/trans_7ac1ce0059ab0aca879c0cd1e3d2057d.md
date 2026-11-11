
将 long 类型变量 grams 的值赋给 Weight 对象 w2。在这种情况下，编译器会调用一个参数类型为 long 的构造函数，来初始化 w2 的 kilogram 和 gram 值，如图 13.24 所示。

![](img/57c0d966bb33c67a5a188e6bf39e4e02_753_0.png)

**图 13.24：** 将基本类型转换为对象类型的选项

如果不是构造函数，而是编写了运算符函数，那么语句

```cpp
w2 = grams;
```

将使用对象 w2 调用在 Weight 类中定义的 operator= 函数，并将 long 变量 grams 作为参数传递给它。

**注意**

- 1. 任何对象类型都可以通过重载**类型转换运算符函数**转换为基本类型，就像我们将 Weight 对象转换为 long 值一样。
- 2. 任何基本类型都可以使用**构造函数**或**operator= 函数**转换为对象类型。这些选项可以互换使用。

## 13.12 一种用户定义类型到另一种的转换

类型转换运算符也可以被重载，用于将一个类的对象转换为另一个类的对象。为了展示一种对象类型到另一种的转换，我们创建了一个 Gram 类，其中有

```cpp
Weight(int p,int q)
{
    kilogram=p;
    gram=q;
}
operator Gram()
{
    Gram res(kilogram*1000+gram);
    return res;
}
void output()
{
    cout<<"Weight is "<<kilogram<<" kgs and "<<gram<<" grams"<<endl;
}
};
```

语句

```cpp
Gram o1 = (Gram)w1;
```

对 Weight 对象 w1 应用强制转换运算符，将其转换为 Gram 对象。因此，编译器将使用对象 w1 调用在 Weight 类中定义的运算符函数。该函数返回一个 Gram 对象，并赋值给对象 o1。对象 w1 的成员 kilogram 和 gram 可以在运算符函数内直接访问，因为 w1 是调用该函数的对象。因此，运算符函数中编写的下面这条语句创建了一个名为 res 的 Gram 类对象，通过将值 kilogram*1000+gram（在本例中计算结果为 50,800）传递给 Gram 类中的一个单参数构造函数来实现。

```cpp
Gram res(kilogram*1000+gram);
```

因此，对象 res 的成员 g 被设置为 50,800，然后返回到 main() 函数，如图 13.26 所示。

类似地，如果我们需要将 Gram 对象转换回 Weight 对象，

```cpp
w1 = (Weight)o1;
```

必须在 Gram 类中定义以下运算符函数

```cpp
operator Weight()
{
    Weight res(g/1000,g%1000);
    return res;
}
```

![](img/57c0d966bb33c67a5a188e6bf39e4e02_756_0.png)

**图 13.26：** 执行 operator `Gram()` 函数

## 13.13 创建全局运算符函数

到目前为止，我们创建的所有运算符函数都是某个特定类的成员函数。运算符函数也可以定义为全局函数，而不放入任何类中。由于全局运算符函数不属于任何类，编译器不需要任何对象来调用它。当我们需要对基本类型和对象类型执行运算，且基本类型出现在运算符左侧时，可以使用全局运算符函数。例如，考虑这样一个需求：我们需要将 100 g 加到 Weight 对象 `w1` 上，并使用以下语句将结果 Weight 存储在 `w2` 中。

```cpp
w2 = 100+w1;
```

因此，我们决定重载运算符 `+`，使其能够处理 `Weight` 对象。但是，我们不能将 `operator+` 创建为 `Weight` 类的成员函数，因为运算符左侧是常量整数值，而编译器需要一个类对象来调用成员函数。如果将 `operator+` 创建为成员函数，只有在以另一种方式编写语句时才有效：

```cpp
w2 = w1+100;
```

在这种情况下，`w1` 出现在 `+` 的左侧，因此编译器可以使用 `w1` 调用 `operator+` 函数，并将 100 作为参数传递。该运算符函数总是可以返回一个 `Weight` 类型对象作为结果，并赋值给 `w2`。然而，将语句写成另一种形式并不总是解决方案。如果运算不满足交换律怎么办？例如，`100-w1` 和 `w1-100` 是不同的。因此，更普遍的问题仍然是如何让语句 `w2 = 100+w1;` 工作。为了解决这个问题，C++ 支持创建全局运算符函数。这些运算符函数不需要任何对象即可调用，所有操作数都被视为函数的参数。因此，如果 `operator+` 函数被全局定义，那么对于语句 `w2 = 100+w1;`，编译器将通过传递 100 和 w1 作为参数来调用它。因此，程序员有责任定义这个运算符函数，使其接受两个参数：一个为整数类型，另一个为 Weight 类型。我们在下面的代码中定义了这样一个运算符函数：

> **注意**
>
> 由于全局运算符函数**不是类的成员函数**，它们无法访问类的**私有**成员。因此，程序员有责任在类中提供必要的方法，使运算符函数在需要时能够访问私有成员。在下面给出的程序中，operator +() 函数需要访问私有成员 kilogram 和 gram。因此，我们在 Weight 类中定义了两个公有函数 getKiloGr() 和 getGr()。getKiloGr() 函数在类外返回 kilogram 的值，getGr() 函数返回成员 gram 的值。

以下是完整的源代码，它重载了运算符 + 来执行一个整数和一个 Weight 对象的加法。

```cpp
#include<iostream.h>
class Weight
{
private:
    int kilogram;
    int gram;
public:
    Weight()
    {
    kilogram =0;
    gram =0;
    }
    Weight(int p,int q)
    {
    kilogram=p;
    gram=q;
    }
    void output()
    {
    cout<<kilogram<<" kgs and "<<gram<<" grams"<<endl;
    }
    int getKiloGr()
    {
    return kilogram;
    }
    int getGr()
    {
    return gram;
    }
};
```

```cpp
Weight operator+(int g, Weight& t)
{
    int kilogram,gram;
    kilogram=t.getKiloGr();
    gram=g + t.getGr(); /*Add g value to gram*/
    while(gram>=1000)
    {
        gram=gram-1000;
        kilogram++;
    }
    Weight res(kilogram,gram);
    return res;
}
void main()
{
//create Weight objects
Weight w1(50,800),w2 ;
//Adding 100 grams to w1
w2=100+w1;
cout<<"The result Weight ";
w2.output();
}
```

语句 `w2=100+w1;` 通过将 100 和 w1 作为参数传递来调用 operator+ 函数，如图 13.27 所示。形式参数 g 被初始化为 100，形式参数 t 是对 Weight 对象 w1 的引用。因此，t.getKiloGr() 将返回 w1 的 kilogram 值，t.getGr() 返回 w1 的 gram 值，如图 13.27 所示。运算符函数返回一个对象 res，这是在将 100 g 加到 w1 后构造出的结果 Weight 对象。operator+ 函数返回的对象被赋值给 w2，并打印在计算机屏幕上。

![](img/57c0d966bb33c67a5a188e6bf39e4e02_758_0.png)

请注意，以下语句将无法工作：

```cpp
w2 = w1 + 100;
```

这是因为参数传递给运算符函数的顺序不同。在这条语句中，第一个参数是 Weight 类型对象，第二个参数是整数。为了支持这些类型的语句，我们必须定义另一个运算符函数，它接受 Weight 对象作为第一个参数，整数作为第二个参数。由于 + 是可交换运算，我们只需从此函数中调用 operator+(int, Weight&)，如下所示：

```cpp
Weight operator+(Weight& t, int g)
{
Weight res = g+t; /*invokes operator+(int g, Weight& t)*/
return res;
}
```

> **注意**
>
> 运算符函数也可以创建为*友元函数*，在这种情况下，不需要函数 **getKiloGr()** 和 **getGr()**，因为运算符函数本身可以访问类的私有成员。回忆第 11 章的内容，创建友元函数并不总是一个好选择，因为它违反了数据隐藏和封装的原则。因此，你应该尽量在程序中减少友元函数的使用。
>
> 作为示例，为了展示将运算符函数创建为友元函数，我们重写上述程序，将 **operator+()** 函数创建为 Weight 类的友元函数。以下是完整的源代码，展示了将**全局运算符函数**创建为**友元函数**。
>
> ```cpp
> #include<iostream.h>
> class Weight
> {
> private:
>         int kilogram;
>         int gram;
> public:
>         Weight()
>         {
>         kilogram=60;
>         gram=0;
>         }
>         Weight(int p,int q)
>         {
>         kilogram=p;
>         gram=q;
>         }
> ```

