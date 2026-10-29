

换句话说，C++ 类提供了一种将数据和函数打包到一个自包含单元中的机制。本章解释了类的构造方式以及如何从中创建对象，包括对对象的初始化和赋值。表 10.1 中列出的数学和转换功能在应用于类时将在第 11 章中讨论。

## 类构造

类同时定义了数据和函数。这种定义通常通过将类构造为两个部分来实现：声明部分和实现部分。如以下代码示例所示，声明部分声明了类的所有数据类型和函数。实现部分随后定义了在声明部分中已声明原型的函数。

```
// class declaration section
class className
{
    data declarations
    function prototypes
};

// class implementation section
function definitions
```

类声明部分中列出的变量和函数统称为类成员。单独来看，变量被称为数据成员和实例变量（术语同义），函数被称为成员函数和方法。（术语“类方法”也使用。）方法不能与数据成员同名。

作为类的具体示例，请看下面名为 Date 的类的定义。这种类型的类在需要根据确切的日期确定设备交付日期和日程安排的应用中很重要。为了完成此任务，例如判断日期是否落在周末或假日，还需要向此类添加许多方法：

```
//class declaration section
class Date
{
private:      // notice the colon after the word private
    int month;  // a data member
    int day;    // a data member
    int year;   // a data member
```

```
public:      // again, notice the colon here
    Date(int = 7, int = 4, int = 2012); // a member method
    void setDate(int, int, int);      // a member method
    void showDate();                  // a member method
}; // this is a declaration - don't forget the semicolon

// class implementation section
// this is where methods are defined
Date::Date(int mm, int dd, int yyyy)
{
    month = mm;
    day = dd;
    year = yyyy;
}

void Date::setDate(int mm, int dd, int yyyy)
{
    month = mm; day = dd; year = yyyy;
    return;
}

void Date::showDate()
{
    cout << "The date is ";
    cout << setw(2) << setfill('0')
         << setw(2) << month << '/'
         << setw(2) << day << '/'
         << setw(2) << year % 100; // extract the last 2 year digits
    cout << endl;
    return;
}
```

由于此定义看起来可能令人不知所措，首先请注意它确实由两个部分组成——声明部分和实现部分。声明部分以关键字 class 开头，后跟类名。类名之后是类的变量声明和方法原型，用一对大括号括起来，以分号终止。此形式的一般结构如下：

```
//class declaration section
class Name
{
```

```
private:
    a list of variable declarations
public:
    a list of method prototypes
};
```

请注意 Date 类遵循此格式。为方便起见，它再次列出，但不带内部注释：

```
// class declaration section
class Date
{
    private:
        int month;
        int day;
        int year;
    public:
        Date(int = 7, int = 4, int = 2012);
        void setDate(int, int, int);
        void showDate();
};
```

此类的名称为 Date。尽管初始大写字母不是必需的，但按惯例使用它来指定一个类。类声明部分的主体，用大括号括起来，由变量和方法声明组成。在本例中，数据成员 month、day 和 year 被声明为整数，并且通过原型声明了三个名为 Date()、setDate() 和 showDate() 的方法。关键字 private 和 public 是访问说明符，定义访问权限。

private 关键字指定在其后跟随的类成员——在本例中为 month、day 和 year——只能通过使用类方法（或如第 11.1 节所述的友元函数）* 访问。private 指定旨在通过要求所有对私有数据成员的访问都必须通过提供的成员方法进行来强制执行数据安全性。这种访问方式防止用户看到数据实际如何存储，被称为数据隐藏。在指定了 private 等类类别之后，它一直有效，直到列出新的类别。

在此 Date 类中，日期使用三个整数存储月份、日和年。此外，年份将始终以四位数存储。例如，年份 1998 存储为 1998，而不是 98。确保所有年份都使用世纪标记存储可消除许多可能出现的问题，如果只存储最后两位数字就会出现这些问题。例如，2012 年和 1999 年之间的年数可以快速计算为 2012 - 1999 = 13 年，但使用年份值 12 和 99 就不容易得到同样的答案。此外，使用四位数可以清楚地知道年份 2012 指的是什么，但两位数字 12 可能指的是 1912 年或 2012 年。

在私有类数据成员之后，Date 类中列出的方法原型已声明为 public。这意味着这些类方法可以被类外的任何对象和函数调用（换句话说，从类外部）。通常，所有类方法都应为 public，以便它们提供从类外部操作类变量的能力。

Date 类提供了三个名为 Date()、setDate() 和 showDate() 的方法。请注意，其中一个成员方法 Date 与类名相同。它被称为构造函数方法，具有特殊用途：它可用于用值初始化类数据成员。此方法使用的默认值是数字 7、4 和 2012，正如您稍后看到的那样，它们用作默认的月份、日和年份值。请注意，默认年份表示为四位整数以保留世纪标记。此外，请注意构造函数方法没有返回类型，这是此特殊方法的必要条件。Date 类中声明的另外两个方法 setDate() 和 showDate() 已声明为不返回值（void）。

类实现部分是声明部分中声明的成员方法被编写以允许其名称所暗示的初始化、赋值和显示功能的地方。⁵ 以下示例显示了在实现部分编写的方法的一般形式。此格式适用于所有方法，除了构造函数，如前所述，它没有返回类型：

```
returnType className::methodName(parameter list)
{
    method body
}
```

正如本示例所示，在类实现部分中定义的成员方法与所有用户编写的 C++ 函数具有相同的格式，只是增加了类名和作用域解析运算符 ::，以标识该方法为特定类的成员。现在再看一下 Date 类的实现部分，为方便起见重复如下：

```
// class implementation section
Date::Date(int mm, int dd, int yyyy)
{
    month = mm;
    day = dd;
    year = yyyy;
}
```

```
void Date::setDate(int mm, int dd, int yyyy)
{
    month = mm;
    day = dd;
    year = yyyy;
    return;
}
```

```
void Date::showDate()
{
    cout << "The Date is ";
    cout << setfill('0')
         << setw(2) << month << '/'
         << setw(2) << day << '/'
         << setw(2) << year % 100; // extract the last 2 year digits
    cout << endl;
    return;
}
```

请注意，此实现部分中的第一个方法与类名相同，这使其成为构造函数方法。因此，它没有返回类型。Date:: 在头部的开头标识此方法为 Date 类的成员。头部的其余部分

```
Date(int mm, int dd, int yyyy)
```

定义该方法具有三个整数参数。此方法的主体只是将数据成员 month、day 和 year 分别赋值为参数 mm、dd 和 yyyy 的值。

下一个头部

```
void Date::setDate(int mm, int dd, int yyyy)
```

定义 setDate() 属于 Date 类（Date::）。此方法不返回值（void）并期望三个整数参数：mm、dd 和 yyyy。与 Date() 方法类似，此方法的主体将数据成员 month、day 和 year 赋值为其参数的值。

最后，类实现部分中的最后一个头部

```
void Date::showDate()
```

定义了一个名为 showDate() 的方法。此方法没有参数，不返回值，并且是 Date 类的成员。此方法的主体需要稍作解释。

尽管所有年份都已存储为四位数值以保留世纪信息，但用户习惯于看到年份表示为两位数值，例如 12/15/12 的日期。要显示年份值的最后两位数字，可以使用表达式 year % 100。例如，如果年份为 1999，则表达式 1999 % 100 产生值 99，如果年份为 2012，则表达式 2012 % 100 产生值 12。

如果你使用了 year = year % 100; 这样的赋值语句，则实际上会更改 year 的存储值以对应年份的最后两位数字

