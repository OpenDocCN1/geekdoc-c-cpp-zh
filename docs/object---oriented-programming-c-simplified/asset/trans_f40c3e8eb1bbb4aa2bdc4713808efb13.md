
# /*程序 9.3 单级继承演示 版本 3*/

```
#include <iostream.h>
#include <conio.h>
class super
{
    int sup_a;
    public :
        void sup_input(int x)
        {
            sup_a=x;
        }
        void sup_show()
        {
            cout<<"sup_a="<<sup_a<<endl;
        }
};
class sub :public super
{
};
void main()
{
    int i;
    clrscr();
    sub o1;
    cout<<"Enter a data member for class super :=";
    cin>>i;
    o1.sup_input(i);
    o1.sup_show();
    getch();
}
```

输出：
为类 super 输入一个数据成员：=1345
sup_a=1345

**解释**：类 super 包含一个私有数据成员 sup_a 和两个公有成员函数 sup_input 与 sup_show，它们分别负责接收输入并赋给 sup_a，以及显示 sup_a 的值。当子类 sub 以公有模式继承时，只有公有数据成员会被复制，并且它们在派生类中也是公有的，如前所述。但请记住，私有数据成员永远不会被继承，所以 sup_a 不会被复制到类 sub 中。在主函数中，我们通过类 sub 的对象调用 sup_input 和 sup_show 这两个函数。

## /*程序 9.4 单级继承演示 版本 4*/

```
#include <iostream.h>
#include <conio.h>
class super
{
    int sup_a;
public :
    void sup_input(int x)
    {
        sup_a = x;
    }
    void sup_show()
    {
        cout << "sup_a=" << sup_a << endl;
    }
};
class sub :public super
{
    int sub_a;
public :
    void sub_input(int x)
    {
        sub_a = x;
    }
    void sub_show()
    {
        cout << "sub_a=" << sub_a << endl;
    }
};
void main()
{
    int i,j;
    clrscr();
    sub o1;
    cout << "Enter the data member of super class i :=";
    cin >> i;
    cout << "Enter the data member of sub class j :=";
    cin >> j;
    o1.sup_input(i);
    o1.sub_input(j);
    o1.sup_show();
    o1.sub_show();
    getch();
}
```

输出：
为超类 i 输入数据成员：=123
为子类 j 输入数据成员：=134
sup_a=123
sub_a=134

**解释**：
在之前的所有程序中，类 sub 都是空的。但这里我们有一个私有数据成员 sub_a 和两个用于输入和显示的函数。在类 sub 中继承类 super 后，类 sub 总共有 4 个公有成员函数：
- ⇒ 两个是它自己的
- ⇒ 两个从类 super 继承而来。
类 sub 还有一个私有数据成员 sub_a。在主函数中，全部 4 个函数都由 sub 类的对象调用。

## /*程序 9.5 单级继承演示 版本 5 */

```
#include <iostream.h>
#include <conio.h>
class super
{
    int sup_a;
    public :
        void sup_input(int x)
        {
            sup_a=x;
        }
        void sup_show()
        {
            cout<<"sup_a="<<sup_a<<endl;
        }
};
class sub :public super
{
    int sub_a;
    public :
        void sub_input(int x)
        {
            sup_input(x*2);
            sub_a=x;
        }
        void sub_show()
        {
            sup_show();
            cout<<"sub_a="<<sub_a<<endl;
        }
};
void main()
{
    int i;
    clrscr();
    sub o1;
    cout<<"Enter the data member :=";
    cin>>i;
    o1.sub_input(i);
    o1.sub_show();
    getch();
}
```

输出：
输入数据成员：=145
sup_a=290
sub_a=145

**解释**：
在主函数中，我们只调用了 sub 类的函数。sup_input 函数是在 sub_input 中以 x*2 作为参数调用的。同样地，sup_show 也是从 sub 类中调用的。因此，当从主函数以 int 类型的 `i` 值调用 sub_input 时，该值被赋给变量 x，并以值 2*145（290）调用基类函数 sup_input，该值被赋给 super 类的 sup_a。当控制从 sup_input 返回时，x 的值被赋给 sub_a。当调用 sub_show 时，它首先调用 sup_show。在显示 sup_a 的值后，sup_show 返回，然后 sub_show 显示 sub_a 的值。

## /* 程序 9.6 单级继承演示 版本 6 */

```
#include <iostream.h>
#include <conio.h>

class super
{
int sup_a;
public :
    void sup_input()
    {
        cout<<"ENTER THE VALUE FOR SUP_A"<<endl;
        cin>>sup_a;
    }
    void sup_show()
    {
        cout<<"Sup_a="<<sup_a<<endl;
    }
};
class sub :public super
{
    int sub_a;
public :
    void sub_input()
    {
        sup_input();
        cout<<"Enter the value for sub_a"<<endl;
        cin>>sub_a;
    }
    void sub_show()
    {
        sup_show();
        cout<<"Sub_a="<<sub_a<<endl;
    }
};
void main()
{
    clrscr();
    sub obj;
    obj.sub_input();
    obj.sub_show();
    getch();
}
```

输出：
为 SUP_A 输入值
34
为 sub_a 输入值
45
Sup_a=34
Sub_a=45

![](img/ad5299318df8d4d7c6df5eaa86590ea3_425_0.png)

图 9.4 程序 9.6 的输出屏幕

**解释**：
该程序与前一程序类似，不同之处在于两个类的输入函数都是从用户键盘获取输入，而不是将固定值赋给数据成员。

## /*程序 9.7 单级继承演示 版本 7 */

```
#include <iostream.h>
#include <conio.h>

class super
{
    int sup_a;
public :
    void sup_input(int x)
    {
        sup_a=x;
    }
    void sup_show()
    {
        cout<<"sup_a="<<sup_a<<endl;
    }
};
class sub :public super
{
    int sub_a;
public :
    void sub_input(int x, int y)
    {
        sup_input(y);
        sub_a=x;
    }
```

```
```cpp
cout << "sup_a=" << sup_a << endl;
}
};
class sub :public super
{
    int sub_a;
public :
    void input(int x)
    {
        sub_a = x;
    }
    void show( )
    {
        cout << "sub_a=" << sub_a << endl;
    }
};
void main( )
{
    clrscr( );
    sub obj;
    obj.input(40);
    obj.show( );
    getch( );
}

输出：
sub_a=40
```

**解释**：这里两个类具有相同的函数签名，因此优先使用派生类的函数。所以将调用派生类的 input 和 show 函数。

```
```cpp
/* PROG 9.9 DEMO OF SINGLE LEVEL INHERITANCE VER 9 */
#include <iostream.h>
#include <conio.h>
class super
{
protected :
    void show( )
    {
        cout << "Hello from super" << endl;
    }
};
```

```
class sub :public super
{
};
void main()
{
    clrscr();
    sub obj;
    obj.show();
    getch();
}
```

输出：
错误：'show' 无法访问在类 'super' 中声明的受保护成员

![](img/ad5299318df8d4d7c6df5eaa86590ea3_428_0.png)

图 9.5 显示错误消息

**解释**：
在公有继承中，基类的受保护成员被派生类继承并保持受保护状态。受保护成员与私有成员类似，不能在类外部使用。因此出现了错误。

## /* 程序 9.10 单级私有继承演示 版本 1 */

```
#include <iostream.h>
#include <conio.h>

class super
{
public :
    void sup_show()
    {
        cout<<"Hello from super"<<endl;
    }
};
class sub :private super
{
};
void main()
{
    clrscr();
    sub obj;
    obj.sup_show();
    getch();
}
```

输出：
错误：'sup_show' 无法访问在类 'super' 中声明的公有成员。

**解释**：
在私有继承中，所有公有成员（数据和函数）对于派生类都变成私有的。由于 super 类的 sup_show 在 sub 类中变为私有，因此它不能在类外部被访问。

## /* 程序 9.11 单级私有继承演示 版本 2 */

```
#include <iostream.h>
#include <conio.h>
class super
{
public :
    void sup_show()
    {
        cout<<"Hello from super"<<endl;
    }
};

class sub :private super
{
public :
    void sub_show()
    {
        sup_show( );
        cout << "Hello from sub" << endl;
    }
};

void main( )
{
    clrscr( );
    sub obj;
    obj.sub_show( );
    getch( );
}
```

**输出：**
来自 super 的问候
来自 sub 的问候

**解释：** 继承来的函数 sup_show 在类 sub 中变为私有。类 sub 定义了自己的函数 sub_show。由于 sup_show 在类 sub 中是私有的，它可以在类 sub 的任何成员函数内被调用。在主函数中，我们通过类 sub 的对象调用 sub_show。该函数定义先调用 super 类的 sup_show 函数，然后执行自己的函数体。

```
```cpp
/*PROG 9.12 DEMO OF SINGLE LEVEL PRIVATE INHERITANCE VER 3 */

#include <iostream.h>
#include <conio.h>

class super
{
        int num;
};

class sub :super
{
public :
        void sub_show()
        {
                cout << "num =" << num << endl;
        }
};
```

