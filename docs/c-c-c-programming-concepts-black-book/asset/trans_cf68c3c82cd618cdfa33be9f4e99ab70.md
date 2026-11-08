
正如前面代码片段中的注释所示，该语句不会引发任何错误，因为 C++ 会自动将字符 ‘a’ 转换为其对应的 double 值。尽管自动类型转换很方便，但它们是歧义的主要来源。让我们考虑一个示例：两个函数同名，且每个函数都接受一个参数。假设其中一个接受浮点变量作为参数，另一个接受 double 变量作为参数。现在，由于 C++ 的自动类型转换机制，当使用小数参数调用该函数时，编译器将无法决定调用哪一个，从而产生歧义。让我们通过以下程序进一步理解这个概念：

```cpp
1:/* Function Overloading Example Program 3 */
2:#include <iostream.h>
3:using namespace std;
4:
5:float example(float i);
6:double example(double n);
7:
8:int main()
9:{
10:    cout<< example(10.32)<<endl;    //Unambiguous, calls example(double)
11:    cout<< example(12)<<endl;       //Ambiguous
12:
13:    return 0;
14:}
15:
16:float example(float i)
17:{
18:    return i;
19:}
20:
21:double example(double n)
22:{
23:    return n;
24:}
```

在前面的程序中，example() 函数被重载，因此它可以接受 float 类型或 double 类型的参数。在第 10 行，对 example(10.32) 函数的调用没有歧义，因为除非另行指定为 float，否则 C++ 中的所有浮点常量都自动为 double 类型。然而，当在第 11 行使用整数值调用 example() 时，就会引入歧义，因为编译器无法知道该参数应转换为 float 类型还是 double 类型。因此，在这种情况下，编译器会显示错误消息，导致编译过程失败，并将歧义解决留给程序员。

```cpp
1:/* Function Overloading Example Program 4 */
2:#include <iostream.h>
3:using namespace std;
4:
5:int example(char c);
6:int example(unsigned char c);
7:
8:int main()
9:{
10:    cout<< example('c')<<endl;    //Unambiguous, calls example(char)
11:    cout<< example(88)<<endl;     //Ambiguous
12:
13:    return 0;
14:}
15:
16:int example(char c)
17:{
18:    return c-1;
19:}
20:
21:int example(unsigned char c)
22:{
23:    return c+1;
24:}
```

在 C++ 中，char 和 unsigned char 本质上并不具有歧义。然而，当在第 11 行使用整数值 88 调用 example() 时，编译器不知道应调用哪个版本的 example()。

类似地，在重载函数中使用默认参数可能会在不知不觉中造成歧义。考虑以下示例，它展示了将默认参数与函数重载一起使用如何造成歧义：

```cpp
1:/* Function Overloading Example Program 5 */
2:#include <iostream.h>
3:using namespace std;
4:
5:int example(int a);
6:int example(int a, int b=1);
7:
8:int main()
9:{
10:  cout<< example(19,21)<<endl; //unambiguous
11:  cout<< example(15)<<endl;       //Ambiguous
12:
13:    return 0;
14:}
15:
16:int example(int a)
17:{
18:    return a;
19:}
20:
21:int example(int a, int b)
22:{
23:    return (a+b);
24:}
```

在第 10 行，example() 中指定了两个参数；因此，在这种情况下不会引入歧义，调用的是 example(int a, int b)。然而，当在第 11 行进行第二次 example() 调用时，就会出现歧义，编译器无法决定处理哪个函数调用。也就是说，是调用带一个参数的函数，还是调用带两个参数的函数（其中一个参数为默认值）。在这种情况下，编译器会发出错误并使编译过程失败。

现在让我们了解 C++ 中函数重载的基本步骤。

## 函数重载的步骤

函数调用首先尝试寻找参数数量和类型与原型匹配的函数，然后调用相应的函数执行。最佳匹配必须唯一。函数选择涉及以下步骤：

- 1. 编译器首先尝试寻找精确匹配，即实际参数的类型与形式参数的类型相同，然后使用该函数。
- 2. 如果未找到精确匹配，则编译器会对实际参数使用自动类型提升（例如 char 到 int 或 float 到 double）来寻找匹配。
- 3. 当前述任一步骤失败时，编译器会尝试对实际参数使用内置转换，然后使用匹配唯一的函数。如果转换后匹配到多个函数定义，则编译器会生成错误消息并使编译过程失败。假设我们使用以下两个函数定义：
  - `long square(long n);`
  - `double square(double x);`

  在这种情况下，像 square(19) 这样的函数调用将导致错误，因为 int 参数可以转换为 long 或 double；从而产生歧义，使编译器不知道该使用哪个版本的 square。
- 4. 如果前述所有步骤都失败，则编译器会尝试用户定义转换以寻找唯一匹配。用户定义转换常用于处理类对象。

现在让我们了解为什么重载在定义类的构造函数和成员函数时很有用。

### 重载构造函数

构造函数是一种特殊类型的函数，它存在于类定义中，并且每当程序中实例化对象时都会被调用。构造函数的主要好处是使程序员无需在程序中创建每个对象后显式初始化它。程序员可以在类定义中编写构造函数来初始化对象的数据成员；每当对象被实例化时，该类的构造函数就会自动触发，并执行构造函数函数体内的代码块。现在，在本节中，我们将学习如何重载类的构造函数，以及它能带来哪些好处。在实际编程中，重载构造函数非常常见。让我们创建一个以 hour:mins:sec 格式保存时间的类，如下所示：

```cpp
1:/* Constructor Function Overloading Example Program 6 */
2:#include <iostream.h>
3:using namespace std;
4:
5:class Time {
6:    int hour;
7:    int mins;
8:    int secs;
9:public:
10:    Time()
11:    {
12:        hour=mins=secs=0;
13:    }
14:    Time(int hr, int min, int sec)
15:    {
16:        hour = hr;
17:        mins = min;
18:        secs = sec;
19:    }
20:    void show_time()
21:    {
22:        cout<<"Time: "<<hour<<":"<<mins<<":"<<secs<<endl;
23:    }
24:};
25:
26:int main()
27:{
28:    Time time_obj1;
29:    Time time_obj2 (12, 30, 52);
30:
31:    time_obj1.show_time ();
32:    time_obj2.show_time ();
33:
34:    return 0;
35:}
```

在前面的程序中，我们可以通过向构造函数显式指定小时、分钟和秒的值来初始化 Time 类型的对象，也可以使用默认构造函数将 Time 的三个成员变量设置为零。重载构造函数的基本优势在于，它使我们无需每次创建对象时都进行对象特定的初始化。在只想定义 Time 类型对象并在程序中稍后设置其值的情况下，我们可以使用默认构造函数将每个成员的值设置为零来初始化它。另一方面，当我们想创建一个 Time 对象并使用特定值（例如系统时间）初始化它时，可以使用带参构造函数，设置用户输入的成员变量值。这为程序员提供了充分的灵活性，可处理与内务相关的任务，例如在实例化时对变量进行垃圾值初始化。此外，重载构造函数在创建类库时提供了易用性，其他用户可以使用这些类库，而无需担心对象成员的分配和释放。

现在让我们了解 C++ 中的运算符重载。

## 运算符重载

现在，既然我们几乎已经涵盖了函数重载是什么以及它在 C++ 中如何实现，接下来介绍 C++ 中另一种形式的多态。与函数重载密切相关的是 C++ 中的运算符重载，其中不同运算符会根据调用它们时所带的参数表现出不同行为。我们可以重载大多数运算符，使它们能够针对我们创建的类执行特殊操作。例如，在 C++ 中我们通常使用加法运算符 ‘+’ 来相加两个整数或实数值，但也可以用它来连接两个字符串。让我们考虑另一个维护栈的类的示例。该类可能重载加法运算符 ‘+’ 以将值压入栈，并重载运算符 ‘-’ 以从栈中弹出值。注意，当运算符被重载时，其原有含义不会丢失。这意味着，当在程序中使用 ‘+’ 运算符连接两个字符串时，并不妨碍我们在同一程序中使用 ‘+’ 运算符进行算术加法。相反，随着重载，它可以应用到的对象类型会变得更广。

我们可以通过创建**运算符**函数来重载 C++ 中的运算符。**运算符函数**定义重载运算符相对于其设计要操作的类将执行的具体操作。运算符函数可以是其所要操作的类的成员函数或非成员函数。对于非成员函数，它必须是该类的**友元**函数。运算符重载的好处是能够将晦涩的程序转换为直观的程序。例如，考虑以下两条语句：

```cpp
obj3.addObject (obj1, obj2);
obj3 = obj1.addObject (obj2);
```

前面两条语句可以使用同一操作改为更易读的格式，如下所示：

```cpp
obj3 = obj1 + obj2;
```

现在，让我们在接下来的几节中进一步了解运算符重载的更多细节。
