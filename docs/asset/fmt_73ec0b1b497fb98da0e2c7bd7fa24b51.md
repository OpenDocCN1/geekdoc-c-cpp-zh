
```
    int n = strlen(t.p);

    if(m <= n) return(1);

    else return(0);

}

void show(const string s)

{

    cout << s.p;

}

int main()

{

    string s1 = "New ";

    string s2 = "York";

    string s3 = "Delhi";

    string t1,t2,t3;

    t1 = s1;

    t2 = s2;

    t3 = s1+s3;

    cout << "\nt1 = "; show(t1);

    cout << "\nt2 = "; show(t2);

    cout << "\n";

    cout << "\nt3 = "; show(t3);

    cout << "\n\n";
```

```
if(t1 <= t3)

{

    show(t1);

    cout << " smaller than ";

    show(t3);

    cout << "\n";

}

else

{

    show(t3);

    cout << " smaller than ";

    show(t1);

    cout << "\n";

}

return 0;

}
```

以下是程序7.4的输出：

```
t1 = New

t2 = York

t3 = New Delhi

New smaller than New Delhi
```

## 7.7 重载运算符的规则

虽然重新定义运算符看起来很简单，但在重载它们时存在一些限制和约束。下面列出其中一些：

- 1. 只能重载现有的运算符，不能创建新的运算符。
- 2. 重载的运算符必须至少有一个操作数是用户定义类型。
- 3. 我们不能改变运算符的基本含义。也就是说，不能重新定义加号（`+`）运算符来从一个值中减去另一个值。
- 4. 重载运算符遵循原运算符的语法规则，它们不能被覆盖。
- 5. 有些运算符不能被重载（见表7.1）。
- 6. 我们不能使用友元函数来重载某些运算符（见表7.2）。不过，可以使用成员函数来重载它们。
- 7. 通过成员函数重载的一元运算符不接收显式参数，也不返回显式值；而通过友元函数重载的一元运算符接收一个引用参数（相关类的对象）。
- 8. 通过成员函数重载的二元运算符接收一个显式参数；通过友元函数重载的二元运算符接收两个显式参数。
- 9. 使用通过成员函数重载的二元运算符时，左操作数必须是相关类的对象。
- 10. 诸如 `+`、`-`、`*` 和 `/` 等二元算术运算符必须显式返回一个值，且不得试图更改自身参数。

### 表7.1 不能被重载的运算符

|  |  |
|---|---|
| `Sizeof` | 求字节数运算符 |
| `.` | 成员运算符 |
| `.*` | 指向成员的指针运算符 |
| `::` | 作用域解析运算符 |
| `?:` | 条件运算符 |

### 表7.2 不能使用友元函数的情形

|  |  |
|---|---|
| `=` | 赋值运算符 |
| `()` | 函数调用运算符 |
| `[]` | 下标运算符 |
| `->` | 类成员访问运算符 |

## 7.8 类型转换

我们知道，当不同类型常量和变量混合在表达式中时，C 会按照一定规则对操作数进行自动类型转换。类似地，赋值操作也会引起自动类型转换。赋值运算符右侧的数据类型会自动转换为左侧变量的类型。例如，语句

```
int m;

float x = 3.14159;

m = x;
```

会在 `x` 的值赋给 `m` 之前将其转换为整数。因此，小数部分被截断。只要所涉及的数据类型是内置类型，类型转换就是自动的。

当数据类型是用户自定义类型时，会发生什么？

考虑下面的语句，它将两个对象相加，然后把结果赋给第三个对象。

```
v3 = v1 + v2;        // v1, v2 and v3 are class type objects
```

当对象属于同一个类类型时，加法和赋值操作能够顺利执行，编译器不会提出任何异议。我们已经看到，对于类对象，右侧对象的所有数据成员的值都会被简单地复制到左侧对象的对应成员中。如果其中一个操作数是对象，而另一个是内置类型变量，又该怎么办？或者，如果它们分别属于两个不同的类呢？

由于用户自定义数据类型是我们为了满足自身需求而设计的，编译器并不支持对这类数据类型进行自动类型转换。因此，如果需要进行此类操作，我们必须自己设计转换例程。

在不兼容类型之间进行数据转换时，可能会出现三种情况：

- 1. 从基本类型转换为类类型。
- 2. 从类类型转换为基本类型。
- 3. 从一种类类型转换为另一种类类型。

我们将详细讨论这三种情况。

### 基本类型到类类型

从基本类型到类类型的转换很容易实现。或许你还记得，在许多示例中已经展示了使用构造函数来初始化对象。例如，使用构造函数从 `int` 类型数组构建了一个 `vector` 对象。类似地，我们使用另一个构造函数从 `char*` 类型变量构建了 `string` 类型对象。这些都是构造函数执行从参数类型到构造函数类类型的实际类型转换的示例。

考虑下面的构造函数：

```
string :: string(char *a)

{

    length = strlen(a);

    P = new char[length+1];

    strcpy(P,a);

}
```

该构造函数从 `char*` 类型变量 `a` 构建一个 `string` 类型对象。变量 `length` 和 `p` 是 `string` 类的数据成员。一旦定义了这个构造函数，

其中 `V1` 是 `vector` 类型的对象。这两条语句的效果完全相同。当编译器遇到需要将类类型转换为基本类型的语句时，它会自动调用类型转换运算符函数来完成这项工作。

类型转换运算符函数应满足以下条件：

- 它必须是类成员。
- 它不能指定返回类型。
- 它不能有任何参数。

由于它是成员函数，因此由对象调用它；所以，函数内部用于转换的值属于调用该函数的对象。这意味着该函数不需要参数。

在上一节描述的 `string` 示例中，我们可以按如下方式完成从 `string` 到 `char*` 的转换：

```
string :: operator char*()

{

    return(p);

}
```

### 一种类类型到另一种类类型

我们刚刚了解了从基本类型到类类型以及从类类型到基本类型的数据转换技术。但有些情况下，我们需要将一种类类型的数据转换为另一种类类型。

示例：

```
objX = objY;    // objects of different types
```

`objX` 是类 `X` 的对象，`objY` 是类 `Y` 的对象。类 `Y` 类型的数据被转换为类 `X` 类型的数据，转换后的值被赋给 `objX`。由于转换发生在从类 `Y` 到类 `X` 的过程中，`Y` 被称为源类，`X` 被称为目标类。

不同类对象之间的这种转换可以通过构造函数或转换函数来完成。编译器对它们的处理方式相同。那么，我们如何决定使用哪种形式呢？这取决于我们希望类型转换函数位于源类中，还是位于目标类中。

我们知道类型转换运算符函数

```
operator typename()
```

converts the class object of which it is a member to `typename`. The `typename` may be a built-in type or a user-defined one (another class type). In the case of conversions between objects, `typename` refers to the destination class. Therefore, when a class needs to be converted, a casting operator function can be used (i.e. source class). The conversion takes place in the source class and the result is given to the destination class object.

Now consider a single-argument constructor function which serves as an instruction for converting the argument's type to the class type of which it is a member. This implies that the argument belongs to the source class and is passed to the destination class for conversion. This makes it necessary that the conversion constructor be placed in the destination class. Figure 7.2 illustrates these two approaches.

![](img/58ab8f034e2127e80560390a921c2523_195_0.png)

### Table 7.3 Type conversions

| Conversion required | Source class | Destination class |
| --- | --- | --- |
| Basic → class | Not applicable | Constructor |
| Class → basic | Casting operator | Not applicable |
| Class → class | Casting operator | Constructor |

When a conversion using a constructor is performed in the destination class, we must be able to access the data members of the object sent (by the source class) as an argument. Since data members of the source class are private, we must use special access functions in the source class to facilitate its data flow to the destination class.

### A Data Conversion Example

Let us consider an example of an inventory of products in store. One way of recording the details of the products is to record their code number, total items in the stock and the cost of each item. Another approach is to just specify the item code and the value of the item in the stock. The example shown in Program 7.5 uses two classes and shows how to convert data of one type to another.

```
DATA CONVERSIONS

#include <iostream>

using namespace std;

class invent2        // destination class declared

class invent1        // source class

{

    int code;        // item code

    int items;       // no. of items

    float price;     // cost of each item

public:

    invent1(int a, int b, float c)

    {

        code = a;

        items = b;

        price = c;

    }

    void putdata()

    {

        cout << "Code:  " << code  << "\n";

        cout << "Items: " << items << "\n";

        cout << "Value: " << price << "\n";

    }

    int getcode() {return code;}

    int getitems() {return items;}

    float getprice() {return price;}

    operator float() {return(items * price);}

    /* operator invent2()    // invent1 to invent2

    {

        invent2 temp;

        temp.code = code;

        temp.value = price * items;

        return temp;

    }*/

};  // End of source class

class invent2      // destination class

{

    int code;

    float value;

    public:

    invent2()

    {

        code = 0; value = 0;

    }

    invent2(int x, float y)      // constructor for

                                 // initialization

    {

        code = x;

        value = y;

    }

    void putdata()

    {

        cout << "Code:  " << code << "\n";

        cout << "Value: " << value << "\n\n";

    }

    invent2(invent1 p)           // constructor for conversion

    {

        code = p.getcode();

        value = p.getitems() * p.getprice();

    }

};  // End of destination class

int main()

{

    invent1 s1(100,5,140.0);

    invent2 d1;

    float total_value;

    /* invent1 To float */

    total_value = s1;

    /* invent1 To invent2 */

    d1 = s1;

    cout << "Product details - invent1 type" << "\n";

    s1.putdata();

    cout << "\nStock value" << "\n";

    cout << "Value = " << total_value << "\n\n";

    cout << "Product details-invent2 type" << "\n";

    d1.putdata();

    return 0;

}
```

Following is the output of Program 7.5:

```
Product details-invent1 type

Code: 100

Items: 5

Value: 140

Stock value

Value = 700

Product details-invent2 type

Code: 100

Value: 700
```

### note

We have used the conversion function

```
operator float( )
```

in the class `invent1` to convert the `invent1` type data to a `float`. The constructor

```
invent2 (invent1)
```

is used in the class `invent2` to convert the `invent1` type data to the `invent2` type data.

Remember that we can also use the casting operator function

```
operator invent2()
```
