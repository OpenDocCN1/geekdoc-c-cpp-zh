

+   5. **友元**函数的参数通常是其作为**友元**的类的对象。
+   6. **友元**函数不是类的成员函数，通常被称为普通函数。
+   7. **友元**函数可以是多个类的**友元**。
+   8. 一个类的函数可以是另一个类的**友元**。
+   9. 可以将整个类作为另一个类的**友元**。
+   10. 我们通常将**友元**函数用于多个类，但也可以用于单个类。
+   11. **友元**函数可以在**公有或私有**可见性模式下声明，而不影响其含义。
+   12. 一个类可以有任意数量的**友元**函数。

创建**友元**函数（作为**友元**类）的一般语法是：

```
class demo
{
  data members :
  public :
    members functions;
  // friend function declaration
  friend data_type function_name (parameters);
};
data_type function_name (parameters)
//definition
{
  function definition;
}
```

现在，让我们来看一些使用`friend`关键字的程序。

```
/*PROG 6.37 DEMO OF FRIEND FUNCTION WITH SINGLE CLASS VER 1*/

#include <iostream.h>
#include <conio.h>
class demo
{
  int fx;
  public :
  void inputf(int x)
{
fx = x;
}
friend int findsqr(demo);
};
int findsqr(demo d)
{
    return d.fx * d.fx;
}
void main()
{
    demo F;
    clrscr();
    F.inputf(30);
    cout << "Square is=" << findsqr(F);
    getch();
}
```

# 输出：

Square is=900

说明：类内部的声明`friend int findsqr(demo);`告诉编译器，函数`findsqr`是`demo`类的友元。这是借助`friend`关键字实现的。由于函数`findsqr`是`demo`类的友元，它可以接受`demo`类的对象，并利用点号成员访问访问`demo`类的公有和私有成员。注意，该函数在类外部定义时没有使用作用域解析运算符（`::`），因为该函数不属于基类，而是`demo`类的友元。在函数定义中不存在`friend`关键字。注意，在`main`中，值30被赋给对象`F`的数据成员`fx`。随后，调用函数`findsqr`时没有使用点运算符与对象`F`关联，而是通过传值机制将对象`F`传递给函数`findsqr`。对象`F`被复制到`d`，函数`findsqr`计算`fx`的平方并返回给`main`。

# /*程序 6.38 单类友元函数演示 版本2*/

```
#include <iostream.h>
#include <conio.h>
#include <string.h>
class demo
{
    char str[15];
    public :
    void inputf(char s[])
    {
    strcpy(str,s);
    }
friend char* toupper(demo d)
{
 static char temp[15];
 strcpy(temp,strupr(d.str));
 return temp;
};
void main()
{
 demo F;
 clrscr();
 F.input("hari mohan");
 cout << "String in upper case \n";
 cout << toupper(F);
 getch();
};
```

输出：
String in upper case

HARI MOHAN

这是单类友元函数的另一个示例。注意，该函数是在类内声明和定义的。之所以可以这样做，是因为函数`toupper`仅仅是`demo`类的友元。在友元函数中，我们使用了一个大小为15的静态字符数组`temp`。我们使用内置字符串函数`strupr`将原始字符串（数据成员）`str`转换为大写，并复制到`temp`中。由于我们不能返回局部变量的地址（当控制流离开代码块时局部变量就会消亡），所以我们将数组`temp`声明为静态的。

上述两个程序本可以简单地将友元函数作为类的一部分写在类内，从而无需使用友元函数。友元的真正用途体现在当我们有多个类，并且希望友元函数同时是两个类的友元（在两个类的情况下）时，这样两个类的数据成员都可以被访问，并且可以在友元函数中进行处理。

```
/*PROG 6.39 FINDING MAXIMUM OF TWO DATA OF TWO DIFFERENT CLASS WITH FRIEND FUNCTION */
#include <iostream.h>
#include <conio.h>
class second;
class first
{
 int fx;
public :
    void inputf(int x)
    {
        fx = x;
    }
    friend void findmax(first,second);
};
class second
{
    int sx;
    public :
    void inputs(int x)
    {
        sx = x;
    }
    friend void findmax(first,second);
};
void findmax(first A, second B)
{
    if(A.fx > B.sx)
        cout << A.fx << "of class first is greater than " << B.sx << "of class second\n";
    else
        cout << B.sx << "of class second is greater than" << A.fx << "of class first\n";
}
void main()
{
    first F;
    second S;
    clrscr();
    F.inputf(40);
    S.inputs(70);
    findmax(F,S);
    getch();
}
```

# 输出：

70of class second is greater than40of class first

**说明**：这是`friend`发挥其作用的真实示例。程序开头的语句`class second;`是前向声明，因为我们在`friend`函数声明中使用了类`second`，而此时类`second`尚未创建。注意，友元函数在两个类中都有声明，这告诉编译器它是类`first`和`second`的友元。它接受一个类`first`对象作为第一个参数，第二个参数是类`second`类型的对象。函数定义在类外部给出。在`main`中，我们调用函数`findmax`并传递类`first`和`second`的两个对象A和B。

# /* 程序6.40 使用友元函数交换两个类的数据 */

```
#include <iostream.h>
#include <conio.h>

class second;            // global declaration of class
class first
{
    int fx;

public :

    void inputf(int x)
    {
        fx=x;
    }

    void showf()
    {
        cout<<"fx :="<<fx<<endl;
    }

    friend void swap(first &, second &);    //declaration of
                                            //friend function
};

class second
{
    int sx;

public :
    void inputs(int x)
    {
        sx=x;
    }
```

# Object-Oriented Programming C++ Simplified

```
```cpp
void shows( )
{
cout << "sx=" << sx << endl;
}
friend void swap(first &, second &); //declaration of 
//friend function
};
void swap(first &A, second &B) //definition of friend of 
//friend function
{
int t;
t = A.fx;
A.fx = B.sx;
B.sx = t;
}
void main( )
{
first F;
second S;
clrscr( );
F.input(20);
S.input(40);
cout << "Before swapping \n";
F.showf( );
S.show( );
swap(F,S);
cout << "AFTER SWAPPING \n";
F.showf( );
S.show( );
getch( );
}
```
```

输出：

Before swapping
fx := 20
sx = 40
AFTER SWAPPING
fx := 40
sx=20

**说明：** 在该程序中，我们使用`friend`函数交换两个类**first**和**second**的数据成员。该函数是两个类的友元，接受第一个参数（类型为`first`类）和第二个参数（类型为`second`类），都通过引用传递。如果不按引用传递参数，那么交换将在类型为`first`类和`second`类的局部变量上进行，因此更改不会反映到**main**中的对象**F**和**S**上。

```
/* PROG 6.41 FUNCTION OF ONE CLASS FRIEND OF ANOTHER CLASS */

#include <iostream.h>
#include <conio.h>

class second;
class first
{
    int num;
public :
    void input_first()
    {
        num = 20;
    }
    void show(second);
};

class second
{
    int num;
public :
    void input_second(int x)
    {
        num = x;
    }
    friend void first ::show(second);
};
void first ::show(second s)
{
    cout << "NUM OF CLASS FIRST := " << num << endl;
    s.input_second(num*num);

cout<<"NUM OF CLASS SECOND :="<<s.num<<endl;
}

void main()
{
    first f;
    clrscr();
    f.input_first();
    second s;
    f.show(s);
    getch();
}
```

输出：
NUM OF CLASS FIRST :=20
NUM OF CLASS SECOND :=400

说明：在该程序中，我们希望在类`first`中创建一个函数，使其成为类`second`的友元。由于该函数将成为类的友元，我们可以在类`first`的函数中拥有类`second`的对象。在类`first`中，我们希望函数`show`成为类`second`的友元。由于函数`show`接受一个类`second`的参数，我们必须在定义类`first`之前对类`second`进行前向声明。

行`class second;`就起到了这个作用。注意类`second`中函数`show`的声明。

```
friend void first :: show (second);
```

这一行告诉编译器，类`first`（由于`first ::show`）的一个函数`show`，返回空（`void`），并且按值接受一个类`type second`的参数，是类`second`的友元。

由于函数`show`是类`second`的友元，类`second`的私有成员函数只能在`show`函数中通过对象使用点运算符来访问。但由于函数`show`属于类`first`，类`first`的私有数据成员可以直接使用。在`main`中，使用类`first`的对象调用该函数，并传递一个类`second`的对象。在函数中，`num * num`（`num`属于类`first`）通过调用函数`input_second`赋给类`second`对象的`num`。

```
/*PROG 6.42 WHOLE CLASS AS A FRIEND OF ANOTHER CLASS VER 1*/

#include <iostream.h>
#include <conio.h>
```

