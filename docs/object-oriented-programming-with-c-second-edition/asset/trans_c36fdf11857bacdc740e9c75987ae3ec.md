

# 类与对象 41

之后

```
int getFeet(Distance * const);
```

之前

```cpp
void setInches(float);
```

之后

```cpp
void setInches(Distance * const, float);
```

之前

```cpp
float getInches();
```

之后

```cpp
float getInches(Distance * const);
```

- 3. 它将此指针（this pointer）的定义作为所有成员函数定义中的领先形式参数，如下所示。它还修改了所有访问对象的语句，通过成员访问运算符（->）通过此指针来访问对象。

之前

```cpp
void Distance::setFeet(int x)
{
  iFeet=x;
}
```

之后

```cpp
void setFeet(Distance * const this, int x)
{
  this->iFeet=x;
}
```

之前

```cpp
int Distance::getFeet()
{
  return iFeet;
}
```

之后

```cpp
int getFeet(Distance * const this)
{
  return this->iFeet;
}
```

之前

```cpp
void Distance::setInches(float y)
{
  fInches=y;
}
```

之后

```cpp
void setInches(Distance * const this, float y)
{
  this->fInches=y;
}
```

# 之前

```cpp
float Distance::getInches()
{
    return fInches;
}
```

# 之后

```cpp
float getInches(Distance * const this)
{
    return this->fInches;
}
```

我们必须理解作用域解析运算符的工作原理。作用域解析运算符也是一种运算符。和任何其他运算符一样，它对其操作数进行操作。作用域解析运算符是一个二元运算符，它接受两个操作数。左侧的操作数是预定义类的名称。右侧是该类的成员函数。根据这些信息，作用域解析运算符将一个正确类型的常量运算符作为领先形式参数插入到右侧函数中。例如，如果类名是 Distance（如上述情况），编译器将插入一个类型为 `Distance * const` 的指针作为右侧函数的领先形式参数。

- 4. 它将调用对象的地址作为领先参数传递给每次成员函数的调用，如下文所示。
之前
d1.setFeet(1);
之后
setFeet(&d1,1);
之前
d1.setInches(1.1);
之后
setInches(&d1,1.1);
之前
cout<<d1.getFeet()<<endl;
之后
cout<<getFeet(&d1)<<endl;
之前
cout<<d1.getInches()<<endl;

# 类与对象

# 之后

```cpp
cout<<getInches(&d1)<<endl;
```

在 C++ 中，点运算符（dot operator）的定义被扩展了。它不仅像 C 那样接受数据成员，还将成员函数作为右侧的操作数。如果右侧的操作数是数据成员，点运算符的行为就和 C 语言中一样。然而，如果右侧的操作数是成员函数，点运算符会将左侧对象的地址作为隐式参数传递给函数调用。

显然，当在成员函数中通过任何限定符访问成员时，引用的是调用对象的成员。显而易见的是，成员数据存在多个副本（在每个对象内部），但每个成员函数只存在一个副本。

而可见的是，此指针在整个生命周期内应该一直指向同一个对象——即调用成员函数的对象。由于某种原因，编译器将其解释为常量指针。

隐式调用的访问性与作为参数传递的对象以及该函数内部局部对象的访问性相同。列表 2.9 说明了这一点。一个新函数——add() 已添加到 Distance 类的现有定义中。

+ 列表 2.9 访问成员函数内部局部对象和参数传递对象的成员

```cpp
/* Distance.h 开始 */
class Distance
{
    /*
      Distance 类剩余
    */
    Distance add(Distance);
};
/* Distance.h 结束 */

/* Distlib.cpp 开始 */
#include"Distance.h"
Distance Distance::add(Distance dd)
{
    Distance temp;
    temp.iFeet=iFeet+dd.iFeet; // 访问 temp.iFeet 和 dd.iFeet 是合法的
    temp.fInches=fInches+dd.fInches;
    return temp;
}
/*
  Distance 类类的定义
*/
/* Distlib.cpp 结束 */

/* main.cpp 开始 */
#include<iostream.h>
#include"Distance.h"

# C++ 面向对象编程

```cpp
void main()
{
    Distance d1,d2,d3;
    d1.setFeet(1);
    d1.setInches(1.1);
    d2.setFeet(2);
    d2.setInches(2.2);
    d3=d1.add(d2);
    cout<<d3.getFeet()<<"\n"<<d3.getInches();
}
```
/* main.cpp 结束 */

# 输出

3-3.3

编译器执行的 Distance :: add() 函数定义如下：

```cpp
Distance add(Distance * const this, Distance dd)
{
    Distance temp;
    temp.iFeet=this->iFeet+dd.iFeet;
    temp.fInches=this->fInches+dd.fInches;
    return temp;
}
```

当从 main() 函数调用此函数时，此指针指向 'd1'。因此，在 add() 函数的第三和第四行访问的是 'd1' 的私有成员。

所以，现在我们可以：

- 声明一个类
- 定义私有成员和成员函数
- 将成员设为私有
- 声明对象并调用对象

这带来了什么优势？库程序员现在从这种安排中获得的优势体现在以下观察中：

> 可执行文件不会从由成员函数访问对象私有成员的源代码创建。

再次强调编译时错误的重要性。假设设计 Distance 类的库程序员希望确保 fInches 永远不超过 12。如果应用程序员通过 Distance::setInches() 指定一个大于 12 的值，函数定义内部的逻辑应该自动增加 iFeet 的值并适当减少 fInches 的值。Distance::setInches() 的修改定义如下：

```cpp
void Distance::setInches(float y)
{
    fInches=y;
    if(fInches>=12)
    {
        iFeet+=fInches/12;
        fInches=((int)fInches/12)*12;
    }
}
```

在这里，我们注意到应用程序员不需要通过 Distance::setInches() 发送小于 12 的值。Distance::setInches() 函数内部的默认逻辑完成了必要的调整。数据抽象的一个示例。

上面的限制可能看起来不是强制性的。然而，我们将看到某些类，其中类似的限制是绝对必要的（也是复杂的）。

同样，库程序员应该如下修改 Distance::add() 函数的定义。在这里，可以假设调用对象或出现的对象 ('dd') 的 fInches 值都不会超过 12。

```cpp
Distance Distance::add(Distance dd)
{
    Distance temp;
    temp.iFeet=iFeet+dd.iFeet;
    temp.setInches(fInches+dd.fInches);
    return temp;
}
```

## 2.1.7 数据抽象 (58)

类结构提供了实现数据抽象的。数据抽象是一个重要概念，应该被正确理解。让我们以上一的 LCD 投影仪为例。它有成员数据（光和风扇）以及成员函数（控制光的开关）。这个真实世界的对象向外部世界隐藏了它的内部操作。因此，它避免了用户需要知道操作过程中可能遇到的陷阱。在操作期间，LCD 永远不会到达无效状态。

数据抽象是对象向程序其余部分隐藏内部操作的一种特性。它使得客户端程序没有知道数据内部是如何安排的。因此，它避免了客户端程序在创建对象时编写预防代码。

现在，为了理解这个概念，让我们来看一个 C++ 示例。设计 Distance 类的库程序员希望确保 fInches 永远不超过 12。如果应用程序员通过 Distance::setInches() 指定一个大于 12 的值，函数定义内部的逻辑应该自动增加 iFeet 的值并适当减少 fInches 的值。Distance::setInches() 的修改定义如下。

```cpp
void Distance::setInches(float y)
{
    fInches=y;
    if(fInches>=12)
    {
        iFeet+=fInches/12;
        fInches=((int)fInches/12)*12;
    }
}
```

在这里，我们注意到应用程序员不需要通过 Distance::setInches() 发送小于 12 的值。Distance::setInches() 函数内部的默认逻辑完成了必要的调整。这是数据抽象的一个示例。

上面的限制可能看起来不是强制性的。然而，我们将看到某些类，其中类似的限制是绝对必要的（也是复杂的）。

同样，库程序员应该如下修改 Distance::add() 函数的定义。在这里，可以假设调用对象或出现的对象 ('dd') 的 fInches 值都不会超过 12。

```cpp
Distance Distance::add(Distance dd)
{
    Distance temp;
    temp.iFeet=iFeet+dd.iFeet;
    temp.setInches(fInches+dd.fInches);
    return temp;
}
```

现在，如果我们写出列表 2.10 显示所示语句

