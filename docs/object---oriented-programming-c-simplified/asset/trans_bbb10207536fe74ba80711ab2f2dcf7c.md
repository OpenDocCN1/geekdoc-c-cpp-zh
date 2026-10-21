

```cpp
void show(T1 par1, T2 par2)
{
    cout << typeid(par1).name() << " parameter=" << par1 << "\t";
    cout << typeid(par2).name() << " parameter=" << par2 << endl;
}

void main()
{
    show(14,'B');
    show("NMIMS",35.67);
}
```

### OUTPUT :

```
int parameter=14 char parameter=B
char * parameter=NMIMS double parameter=35.67
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_636_0.png)

### Figure 13.3. Output screen of program 13.5

### EXPLANATION :

在程序中我们有一个函数模板 `show`，它接受两种通用类型作为参数。注意在下面的模板中，两种通用类型都声明为 `<class T1, class T2>`。可以声明更多通用类型，用逗号分隔，但每个都必须使用 `class` 关键字声明。在函数模板 `show` 中，我们只是显示参数的类型和值。由于我们两次以不同参数调用 `show`，内存中会创建该函数模板的两个不同定义。

### PROG 13.6 CHECKING EQUALITY OF DATA TYPE OF TWO VARIABLES USING FUNCTION TEMPLATE VER 1

```cpp
#include <iostream.h>
#include <typeinfo.h>
#include <string.h>

template<class T1, class T2>
void equal(T1 x, T2 y)
{
    const char *p1 = typeid(x).name();
    const char *p2 = typeid(y).name();
    if(strcmp(p1,p2) == 0)
        cout << "Data type " << p1 << " and " << p2
             << " is same " << endl;
    else
        cout << "Data type " << p1 << " and " << p2
             << " is not same " << endl;
}

void main()
{
    int a = 10, b = 20;
    float c = 23.45;
    char ch = 'A';
    char *s1 = "string", *s2 = "string";
    equal(a,c);
    equal(ch,b);
    equal(a,b);
    equal(s1,s2);
}
```

### OUTPUT :

```
Data type int and float is not same
Data type char and int is not same
Data type int and int is same
Data type char * and char * is same
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_637_0.png)

### Figure 13.4. Showing the output of the program 13.6

### EXPLANATION :

在函数模板中，我们尝试检查两个通用数据类型是否相同。这将在传递实际类型作为参数创建函数模板实例时进行检查。对于第一次调用 `equal(a,c)`，函数模板被实例化并创建了如下所示的函数定义。

```cpp
void equal(T1 x, T2 y)
{
    const char *p1 = typeid(x).name();
    const char *p2 = typeid(y).name();
    if(strcmp(p1,p2) == 0)
        cout << "Data type " << p1 << " and " << p2 << " is same " << endl;
    else
        cout << "Data type " << p1 << " and " << p2 << " is not same" << endl;
}
```

`typeid(x).name()` 返回数据类型作为常量字符串，因此 `p1` 存储 `"int"` 而 `p2` 存储 `"float"`，两者都作为字符串。之后我们通过使用 `strcmp()` 比较两个字符串来比较它们是否相同。如果 `strcmp` 返回 0，则两个数据类型相同；否则不相同。对 `equal` 的其他调用也同样适用。

### PROG 13.7 CHECKING EQUALITY OF DATA TYPE OF TWO VARIABLES USING FUNCTION TEMPLATE VER 2

```cpp
#include <iostream.h>
#include <typeinfo.h>
#include <string.h>

template <class T1, class T2>
void equal(T1 x, T2 y)
{
    const char *p1 = typeid(x).name();
    const char *p2 = typeid(y).name();
    if(strcmp(p1,p2) == 0)
        cout << "Data type " << p1 << " and " << p2 << " is same" << endl;
    else
        cout << "Data type " << p1 << " and " << p2 << " is not same" << endl;
}

void main()
{
    equal(23.45, 23.45);
    equal('A', 65);
    equal(2.0, 2.0f);
    equal("str", (int*)"str");
}
```

### OUTPUT :

```
Data type double and double is same
Data type char and int is not same
Data type double and float is not same
Data type char * and int * is not same
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_639_0.png)

### Figure 13.5. Showing the output of program 13.7

### EXPLANATION :

该程序与之前的程序相似，只是 `main` 有所更改。在之前的程序中我们声明了不同数据类型的变量然后传递给函数 `equal`。但在这里我们将它们作为常量传递，如下所示：

```cpp
equal(23.45, 23.45);
equal('A', 65);
equal(2.0, 2.0f);
equal("str", (int*)"str");
```

在上面显示的第一个语句中，两个参数都被视为 `double`。在第二个中，一个是 `char`，第二个是 `int`。在第三个中，第一个是 `double`，第二个是 `float`（由于 `f`）。在对 `equal` 的第四次调用中，第一个参数的类型为 `char*`，第二个参数的类型为 `int*`（显式类型转换）。将生成四个不同的函数定义。

### PROG 13.8 TO CHECK EQUALITY OF THREE DATA TYPES USING FUNCTION TEMPLATE

```cpp
#include <iostream.h>
#include <typeinfo.h>
#include <string.h>

template<class T1, class T2, class T3>
void equal(T1 x, T2 y, T3 z)
{
    const char *p1 = typeid(x).name();
    const char *p2 = typeid(y).name();
    const char *p3 = typeid(z).name();
```

```cpp
{
    cout << "* + * + * + * +" << s << "* + * + * + * + * +" << endl;
    cout << typeid(par).name() << " parameter=" << par << endl;
}

void main()
{
    show(12,"good Morning");
    show(34.45,"Good Morning");
}
```

### OUTPUT :

```
* + * + * + * + good Morning* + * + * + * +
int parameter=12
* + * + * + * + Good Morning* + * + * + * +
double parameter=34.45
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_641_0.png)

### Figure 13.7. Showing the output of program 13.9

### EXPLANATION :

你可以将函数模板的一些参数固定，如上所示。这里在函数 `show` 中，第一个参数可以是任意类型，但第二个参数是固定的，必须为 `char*` 类型。类似地，你可以在函数模板中固定任意数量的参数。但请注意，固定的参数不得写入模板声明中。像在上述情况下写 `template <class T, char* s>` 将是错误的。它必须作为函数参数编写。

### PROG 13.10 MIXING BUILT-IN TYPE WITH GENERIC TYPES VER 2

```cpp
#include <iostream.h>
#include <typeinfo.h>

template <class T>
void show(T par, char* s = "Good Morning")
{
    cout << "************" << s << "************" << endl;
    cout << typeid(par).name() << " parameter= " << par << endl;
}

void main()
{
    show(12);
    show(35.46);
}
```

### OUTPUT :

```
**********Good Morning**********
int parameter= 12
**********Good Morning**********
double parameter= 35.46
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_642_0.png)

### Figure 13.8. Output screen of program 13.10

### EXPLANATION :

该程序与之前的程序相似，但这里我们将函数模板 `show` 的第二个参数作为 `char*` 类型的默认参数。因此，你可以为函数模板提供默认参数。

### PROG 13.11 OVERLOADING OF FUNCTION TEMPLATE

```cpp
#include <iostream.h>
#include <typeinfo.h>

template <class T>
void show(T par)
{
    cout << "Function template show \n";
    cout << "par :=" << par << endl;
}

void show(char* s)
{
    cout << "Explicit function show\n";
    cout << "s=" << s << endl;
}

void main()
{
    show(12);
    show(34.78);
    show("Explicit");
}
```

### OUTPUT :

```
Function template show
par :=12
Function template show
par :=34.78
Explicit function show
s=Explicit
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_643_0.png)

### Figure 13.9. Output screen of program 13.11

### EXPLANATION :

当使用与函数模板相同的名称为特定数据类型编写显式函数时，显式函数会优先于为该特定数据类型实例化函数模板而被调用。这里我们有一个函数模板 `show`，它只有一个通用数据类型的参数，我们有一个 `show` 函数，它接受一个 `char*` 类型的单个参数。当执行 `show("Explicit")` 时，函数模板不会被实例化，而是调用 `show(char*)`。对于所有其他类型的参数，函数模板将被实例化。

## 13.3 CLASS TEMPLATE

与函数模板类似，我们可以创建类模板。区别仅在于之前我们为函数创建了模板；现在我们将为类创建它。类模板主要用于创建容器类，即可以包含任意类型各种对象的类。对于类模板，定义方法保持不变但实例化方式改变。

举例说明：

```cpp
template<class T>
class demo
{
  T x, y;
  public :
  ............;
  ............;
};
```

类模板可以在创建类的对象时实例化。即：

```cpp
demo<int> d1;
```

创建类模板 `demo` 的整数数据类型的实例。类似地

```cpp
demo<float> d2;
```

将创建类模板 `demo` 的浮点数据类型的实例。在此实例中，内存中将存在两个不同的 `demo` 类。一个将使用整数数据成员，另一个使用浮点数据成员。

### PROG 13.12 SUM OF TWO NUMBER USING CLASS TEMPLATE

```cpp
#include <iostream.h>
#include <conio.h>

template <class PAR>

class demo
{
    PAR n1,n2;
public :
    demo(PAR x, PAR y)
    {
        n1 = x;
```

