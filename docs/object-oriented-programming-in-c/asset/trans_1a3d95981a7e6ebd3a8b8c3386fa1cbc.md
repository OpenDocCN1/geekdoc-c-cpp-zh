

# 构造函数动态初始化

```
// Long-term fixed deposit system
#include <iostream>
using namespace std;
class Fixed_deposit
{
    long int P_amount;      // Principal amount
    int      Years;         // Period of investment
    float    Rate;          // Interest rate
    float    R_value;       // Return value of amount
public:
    Fixed_deposit(){ }
    Fixed_deposit(long int p, int y, float r=0.12);
    Fixed_deposit(long int p, int y, int r);
    void display(void);
};
Fixed_deposit :: Fixed_deposit(long int p, int y, float r)
{
    P_amount = p;
    Years = y;
    Rate = r;
    R_value = P_amount;
    for(int i = 1; i <= y; i++)
        R_value = R_value * (1.0 + r);
}
Fixed_deposit :: Fixed_deposit(long int p, int y, int r)
{
    P_amount = p;
    Years = y;
    Rate = r;
    R_value = P_amount;
    for(int i=1; i<=y; i++)
        R_value = R_value*(1.0+float(r)/100);
}
void Fixed_deposit :: display(void)
{
    cout << "\n"
         << "Principal Amount = " << P_amount << "\n"
         << "Return Value     = " << R_value << "\n";
}
```

```
int main()
{
    Fixed_deposit FD1, FD2, FD3;  // deposits created

    long int p;                 // principal amount

    int     y;                  // investment period, years
    float   r;                  // interest rate, decimal form
    int     R;                  // interest rate, percent form

    cout << "Enter amount,period,interest rate(in percent)"<<"\n";
    cin >> p >> y >> R;
    FD1 = Fixed_deposit(p,y,R);

    cout << "Enter amount,period,interest rate(decimal form)" << "\n";
    cin >> p >> y >> r;
    FD2 = Fixed_deposit(p,y,r);

    cout << "Enter amount and period" << "\n";
    cin >> p >> y;
    FD3 = Fixed_deposit(p,y);

    cout << "\nDeposit 1";
    FD1.display();

    cout << "\nDeposit 2";
    FD2.display();

    cout << "\nDeposit 3";
    FD3.display();

    return 0;
}
```

程序 6.3 的输出为：

```
Enter amount,period,interest rate(in percent)
10000 3 18
Enter amount,period,interest rate(in decimal form)
10000 3 0.18
Enter amount and period
10000 3

Deposit 1
Principal Amount = 10000
Return Value      = 16430.3
```

Deposit 2
Principal Amount = 10000
Return Value      = 16430.3

Deposit 3
Principal Amount = 10000
Return Value      = 14049.3

该程序使用了三个重载的构造函数。这些构造函数的参数值在运行时提供。用户可以以下列其中一种形式提供输入：

- 1. 金额、期限和以小数形式表示的利率。
- 2. 金额、期限和以百分比形式表示的利率。
- 3. 金额和期限。

note
由于构造函数根据适当的参数进行了重载，因此与输入值匹配的构造函数将被调用。例如，第二构造函数用于形式 (1) 和 (3)，第三构造函数用于形式 (2)。请注意，对于形式 (3)，使用了带默认参数的构造函数。由于第三个参数的输入缺失，因此使用 r 的默认值。

# 6.7 拷贝构造函数

我们在第 6.3 节中简要提到了拷贝构造函数。我们在第 6.4 节中使用了拷贝构造函数

```
integer(integer &i);
```

作为重载构造函数之一。

如前所述，拷贝构造函数用于从另一个对象声明并初始化一个对象。例如，语句

```
integer I2(I1);
```

将定义对象 I2，同时将其初始化为 I1 的值。此语句的另一种形式为

```
integer I2 = I1;
```

通过拷贝构造函数初始化的过程称为拷贝初始化。请记住，语句

```
I2 = I1;
```

不会调用拷贝构造函数。然而，如果 I1 和 I2 是对象，则该语句是合法的，并且只是逐成员地将 I1 的值赋给 I2。这是重载赋值运算符(=) 的任务。我们稍后会看到更多相关内容。

拷贝构造函数以同一类对象的引用作为参数。让我们考虑一个简单的构造和使用拷贝构造函数的示例，如程序 6.4 所示。

# 拷贝构造函数

```
#include <iostream>

using namespace std;

class code
{
    int id;
public:
    code() { }                      // constructor
    code(int a) { id = a; }         // constructor again
    code(code & x)                  // copy constructor
    {
        id = x.id;                  // copy in the value
    }
    void display(void)
    {
        cout << id;
    }
};
int main()
{
    code A(100);    // object A is created and initialized
    code B(A);      // copy constructor called
    code C = A;     // copy constructor called again

    code D; // D is created, not initialized
    D = A;          // copy constructor not called

    cout << "\n id of A: "; A.display();
    cout << "\n id of B: "; B.display();
    cout << "\n id of C: "; C.display();
    cout << "\n id of D: "; D.display();

    return 0;
}
```

# 程序 6.4

# 面向对象 C++ 编程

程序 6.4 的输出如下所示

```
id of A: 100
id of B: 100
id of C: 100
id of D: 100
```

> 拷贝构造函数的参数使用了引用变量。我们不能按值将参数传递给拷贝构造函数。

当未定义拷贝构造函数时，编译器提供其自己的拷贝构造函数。

构造函数也可以在创建对象时分配内存。这将使系统在对象大小不相同时为每个对象分配适当数量的内存，从而节省内存。在对象构造时为对象分配内存称为对象的动态构造。内存是借助 new 运算符分配的。程序 6.5 显示了 new 在用于在对象中构造字符串的构造函数中的使用。

```
#include <iostream>
#include <string>
using namespace std;

class String
{
  char *name;
  int length;
public:
  String()  // constructor-1
  {
    length = 0;
    name = new char[length + 1];
  }
  String(char *s)  // constructor-2
  {
    length = strlen(s);
  }

(Contd)
```

```
name = new char[length + 1];       // one additional
                                      // character for \0
strcpy(name, s);
}

void display(void)
{cout << name << "\n";}
void join(String &a, String &b);
};

void String :: join(String &a, String &b)
{
    length = a.length + b.length;
    delete name;
    name = new char[length+1];        // dynamic allocation

    strcpy(name, a.name);
    strcat(name, b.name);
};

int main()
{
        char *first = "Joseph ";
        String name1(first), name2("Louis "),name3("Lagrange"),s1,s2;

        s1.join(name1, name2);
        s2.join(s1, name3);
        name1.display();
        name2.display();
        name3.display();
        s1.display();
        s2.display();

        return 0;
}
```

程序 6.5 的输出将为：

```
Joseph
Louis
Lagrange
Joseph Louis
Joseph Louis Lagrange
```

# note

该程序使用了两个构造函数。第一个是空构造函数，允许我们声明字符串数组。第二个构造函数初始化字符串的长度，为字符串存储分配必要的空间并创建字符串本身。请注意，为容纳结束字符串字符 '\0' 分配了一个额外的字符空间。

成员函数 join() 连接两个字符串。它估计要连接的字符串的组合长度，为组合字符串分配内存，然后使用字符串函数 strcpy() 和 strcat() 创建该字符串。请注意，在函数 join() 中，length 和 name 是调用该函数的对象的成员，而 a.length 和 a.name 是参数对象 a 的成员。main() 函数程序将三个字符串连接成一个字符串。输出如下所示：

Joseph Louis Lagrange

# 6.9 构造二维数组

我们可以使用类类型对象构造矩阵变量。程序 6.6 中的示例说明了如何构造大小为 m x n 的矩阵。

```
CONSTRUCTING MATRIX OBJECTS
#include <iostream>

using namespace std;

class matrix
{
    int **p; // pointer to matrix
    int d1,d2;      // dimensions
public:
    matrix(int x, int y);
    void get_element(int i, int j, int value)
    {p[i][j]=value;}
    int & put_element(int i, int j)
    {return p[i][j];}
};
matrix :: matrix(int x, int y)
{
    d1 = x;
    d2 = y;
    p = new int *[d1];      // creates an array pointer
    for(int i = 0; i < d1; i++)
```

