
```
office.Area = 4200;
 office.Floors = 3;

Console.WriteLine("house has:\n " +
    house.Floors + " floors\n " +
    house.Occupants + " occupants\n " +
    house.Area + " total area");

Console.WriteLine();

Console.WriteLine("office has:\n " +
    office.Floors + " floors\n " +
    office.Occupants + " occupants\n " +
    office.Area + " total area");
    office.AreaPerPerson();
}
```

该程序生成以下输出，与之前相同：

```
house has:
  2 floors
  4 occupants
  2500 total area
  625 area per person

 office has:
  3 floors
  25 occupants
  4200 total area
  168 area per person
```

让我们来看看这个程序的关键元素，首先是 AreaPerPerson() 方法本身。AreaPerPerson() 的第一行是

```
public void AreaPerPerson() {
```

这一行声明了一个名为 AreaPerPerson 的方法，它没有参数。它被指定为 public，因此可以被程序的所有其他部分使用。它的返回类型是 void。因此，AreaPerPerson() 不会向调用者返回值。该行以方法体的左花括号结束。

AreaPerPerson() 的方法体仅由以下语句组成：

```
Console.WriteLine("  " + Area / Occupants + " area per person");
```

接下来，仔细观察 Main() 中的这一行代码：

```
house.AreaPerPerson();
```

该语句在 house 上调用 AreaPerPerson() 方法。也就是说，它通过点运算符相对于 house 所引用的对象调用 AreaPerPerson()。当方法被调用时，程序控制权转移到该方法。当方法终止时，控制权返回到调用者，并从调用后的下一行代码继续执行。

在这种情况下，对 house.AreaPerPerson() 的调用会显示由 house 定义的建筑物的人均面积。类似地，对 office.AreaPerPerson() 的调用会显示由 office 定义的建筑物的人均面积。每次调用 AreaPerPerson() 时，它都会为指定的对象显示人均面积。

在 AreaPerPerson() 方法内部，有一件非常重要的事情需要注意：实例变量 Area 和 Occupants 是直接引用的，没有使用点运算符。当一个方法使用其类定义的实例变量时，它直接使用，不需要显式引用对象，也不需要点运算符。仔细想想，这很容易理解。方法总是相对于其类的某个对象来调用。一旦发生调用，该对象就是已知的。因此，在方法内部，无需第二次指定对象。这意味着 AreaPerPerson() 内部的 Area 和 Occupants 隐式地引用调用 AreaPerPerson() 的对象中的那些变量副本。

> 注意：有趣的是，在 AreaPerPerson() 方法中，Occupants 不能等于零（在本章的所有示例中都不会为零）。如果 Occupants 为零，则会发生除零错误。在第13章中，你将学习异常，这是 C# 处理错误的方式，并了解如何留意运行时可能出现的错误。

## 从方法返回

一般来说，有两种条件会导致方法返回。第一种，如前面示例中的 AreaPerPerson() 方法所示，是遇到方法的右花括号时。第二种是执行 return 语句时。return 有两种形式：一种用于 void 方法（不返回值的方法），另一种用于返回值。这里讨论第一种形式。下一节将解释如何返回值。

在 void 方法中，可以使用以下形式的 return 来立即终止方法：

```
return;
```

当该语句执行时，程序控制权返回到调用者，跳过方法中剩余的代码。例如，考虑以下方法：

```
public void MyMeth() {
    int i;
    for(i=0; i<10; i++) {
        if(i == 5) return; // stop at 5
        Console.WriteLine();
    }
}
```

在这里，for 循环只会从 0 运行到 5，因为一旦 i 等于 5，方法就会返回。

方法中可以有多个 return 语句，尤其是在有两条或更多退出路径时。例如，

```
public void MyMeth() {
    // ...
    if(done) return;
    // ...
    if(error) return;
}
```

如果方法已完成或发生错误，则方法返回。但是要小心。方法中过多的出口点会破坏代码，因此不要随意使用它们。

回顾一下：void 方法可以通过两种方式返回——要么到达其右花括号，要么执行 return 语句。

## 返回值

虽然返回类型为 void 的方法并不少见，但大多数方法都会返回一个值。事实上，返回值的能力是方法最有用的特性之一。在第3章中使用 Math.Sqrt() 函数求平方根时，我们已经看到了返回值的示例。

返回值在编程中有多种用途。在某些情况下，例如 Math.Sqrt()，返回值包含某个计算的结果。在其他情况下，返回值可能只是表示成功或失败。还有一些情况，返回值可能包含状态代码。无论用途如何，使用方法返回值都是 C# 编程的一个组成部分。

方法使用以下形式的 return 将值返回给调用例程：

```
return value;
```

这里，value 是返回的值。

可以使用返回值来改进 AreaPerPerson() 的实现。更好的方法不是显示人均面积，而是让 AreaPerPerson() 返回该值。这种方法的好处之一是你可以将该值用于其他计算。下面的示例修改了 AreaPerPerson()，使其返回人均面积而不是显示它：

```
// Return a value from AreaPerPerson().
using System;

class Building {
    public int Floors;    // number of floors
    public int Area;      // total square footage of building
    public int Occupants; // number of occupants

    // Return the area per person.
    public int AreaPerPerson() {
        return Area / Occupants;
    }
}
```

```
// Use the return value from AreaPerPerson().
class BuildingDemo {
    static void Main() {
        Building house = new Building();
        Building office = new Building();
        int areaPP; // area per person

        // Assign values to fields in house.
        house.Occupants = 4;
        house.Area = 2500;
        house.Floors = 2;

        // Assign values to fields in office.
        office.Occupants = 25;
        office.Area = 4200;
        office.Floors = 3;

        // Obtain area per person for house.
        areaPP = house.AreaPerPerson();

        Console.WriteLine("house has:\n " +
            house.Floors + " floors\n " +
            house.Occupants + " occupants\n " +
            house.Area + " total area\n " +
            areaPP + " area per person");

        Console.WriteLine();

        // Obtain area per person for office.
        areaPP = office.AreaPerPerson();

        Console.WriteLine("office has:\n " +
            office.Floors + " floors\n " +
            office.Occupants + " occupants\n " +
            office.Area + " total area\n " +
            areaPP + " area per person");
    }
}
```

输出与之前相同。

在程序中，请注意当调用 AreaPerPerson() 时，它被放在赋值语句的右侧。左侧是接收 AreaPerPerson() 返回值的变量。因此，在

`areaPP = house.AreaPerPerson();`

执行之后，house 对象的人均面积就存储在 areaPP 中。

注意，AreaPerPerson() 现在的返回类型是 int。这意味着它将向调用者返回一个整数值。方法的返回类型很重要，因为方法返回的数据类型必须与方法指定的返回类型兼容。因此，如果你希望方法返回 double 类型的数据，那么它的返回类型必须是 double 类型。
