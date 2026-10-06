

## 14.2 类 531

当你声明一个变量并指定一个类的名称作为变量的数据类型时，你正在创建一个类变量。类变量是一种特殊的变量类型，它可以引用计算机内存中的一个对象并与该对象进行操作。第 4 行声明的 `myPhone` 可用于引用从 `CellPhone` 类创建的对象。

图 14-6 类变量的声明

![](img/c939132f78787c7f339c6977b3fc8c85_555_0.png)

在许多面向对象的语言中，声明类变量的行为实际上并没有在内存中创建对象。它只是创建了一个可以与你的对象一起使用的变量。下一步是创建对象。这是通过第 9 行中的以下赋值语句实现的：

```
Set myPhone = New CellPhone()
```

注意，在 `=` 运算符的右侧出现了 `new` 关键字。在许多编程语言中，`new` 关键字用于创建一个对象。紧接着出现类名（在本例中是 `CellPhone`），后面是一对括号。这指定了应该作为蓝图来创建对象的类。一旦创建了对象，`=` 运算符会将对象的内存地址分配给 `myPhone` 变量。该语句的操作如图 14-7 所示。

当给一个变量分配对象的地址时，称该变量引用该对象。如图 14-8 所示，在该语句执行后，`myPhone` 变量将引用一个 `CellPhone` 对象。

图 14-7 创建对象并将其地址赋值给类变量

![](img/c939132f78787c7f339c6977b3fc8c85_555_1.png)

图 14-8 myPhone 变量引用了一个 CellPhone 对象

![](img/c939132f78787c7f339c6977b3fc8c85_555_2.png)

## 第 14 章 面向对象编程

> 注意：在某些语言（如 C++）中，声明类变量的行为会在内存中创建一个对象。在这些语言中，没有必要像我们在程序 14-1 的第 9 行中那样使用 `New` 关键字来创建对象。

接下来是第 12 行的语句：

```
CallPhone.setManufacturer("Motorola")
```

该语句调用了 `phone.setManufacturer` 方法。表达式 `setManufacturer` 使用点符号表示法编写。点符号表示法中的“点”指的是那个点符号。点的左侧是引用对象的类变量名称。点的右侧是我们正在调用的方法名称。当该语句执行时，它使用 `phone` 引用的对象来调用 `setManufacturer` 方法，并将字符串 "Motorola" 作为参数传递。结果是字符串 "Motorola" 将赋值给对象的 `manufacturer`（制造商）字段。

第 13 行调用了 `phone.setModelNumber` 方法，将字符串 "M1000" 作为参数传递。在该语句执行后，字符串 "M1000" 将存储在对象的 `number` 字段中。第 14 行调用了 `phone.setRetailPrice` 方法，将 99.99 作为参数传递。这个 99.99 将赋值给 `retailPrice`（零售价）字段。图 14-9 显示了第 12 到 14 行语句执行后的对象状态。

图 14-9 myPhone 引用的对象状态

| 一个 CellPhone 对象 | |
|---|---|
| phone 变量地址 | manufacturer:"Motorola" |
| | modelNumber:"M1000" |
| | retailPrice:99.99 |

第 17 到 19 行的语句显示对象字段中的值。以下是第 17 行的语句：

```
Display "The manufacturer is ", phone.getManufacturer()
```

该语句调用了 `phone.getManufacturer` 方法，该方法返回字符串 "Motorola"。屏幕上显示以下消息：

The manufacturer is Motorola

接下来执行第 18 行的语句：

```
Display "The model number is ", phone.getModelNumber()
```

该语句调用了 `phone.getModelNumber` 方法，该方法返回字符串 "M1000"。屏幕上显示以下消息：

The model number is M1000

接下来执行第 19 行的语句：

```
Display "The retail price is ", phone.getRetailPrice()
```

该语句调用了 `myPhone.getRetailPrice` 方法，它返回值 199.99。屏幕上显示以下消息：

the retail price is 199.99

## 访问器和变变器方法

如前所述，将类的所有字段都设为私有（private），并提供公共方法来访问和更改这些字段是一种常见做法。这确保了拥有这些字段的对象能够控制对它们所进行的所有更改。从类字段中获取值的方法不会更改它，被称为**访问器方法**（accessor method）。在字段中存储值或以其他方式更改字段值的方法被称为**变变器方法**（mutator method）。在 `CellPhone` 类中，`getManufacturer`、`getModelNumber` 和 `getRetailPrice` 方法是访问器，而 `setManufacturer`、`setModelNumber` 和 `setRetailPrice` 方法是变变器。

> 注意：变变器有时被称为“setter”（set），访问器方法有时被称为“get”（get）。

## 构造函数

构造函数是在创建对象时自动调用的方法。在大多数情况下，构造函数用于用初始值初始化对象的字段。在许多语言中，这些方法被称为**构造函数**（constructors），构造函数与其所属的类同名。这是本书遵循的约定。例如，如果我们在 `CellPhone` 类中写一个构造函数，我们将写一个名为 `CellPhone` 的模块。类列表 14-4 中的伪代码显示了添加了构造函数的类版本。构造函数出现在第 8 到 13 行。

> 注意：在 Visual Basic 中，构造函数命名为 `New`。

## 类列表 14-4

```
Class CellPhone
// 字段声明
Private String manufacturer
Private String modelNumber
Private Real retailPrice
// 构造函数
Public Module CellPhone(
```

