

```cpp
public :
    second (int a) : first (a%10), sa(a/10)
    {
        cout<<"Con of second called"<<endl;
    }
    void sshow()
    {
        fshow();
        cout<<"sa="<<sa<<endl;
    }
};

void main()
{
    clrscr();
    second s(234);
    s.sshow();
    getch();
}

OUTPUT :
Con of first called
Con of second called
fa=4
sa=23
```

**EXPLANATION :** 该程序与前一个程序相同，但这里我们没有为类 second 的构造函数取两个参数。在此程序的早期版本中，通过计算两个类中的参数数量，我们选择在派生类 second 的构造函数中保留参数数量。但在这里，我们只在类 second 的构造函数中取一个参数 234，该参数被收集在形式参数 a 中。从 second 类的此构造函数中，first 类的构造函数被调用并传递 a%10 作为参数，而 a/10 被赋给 second 类的 sa。

```cpp
/*PROG 9.37 DEMO OF PARAMETERIZED CONSTRUCTOR IN INHERITANCE VER 3 */

#include <iostream.h>
#include <conio.h>
#include <string.h>
class first
{
    int fa;
public :
    first(int x)
    {
        fa=x;
        cout<< "Con of first called"<< endl;
    }
    void fshow()
    {
        cout<< "fa="<< fa<< endl;
    }
};
class second
{
    int sa;
    float sb;
public :
    second(int a, float b) :sa(a),sb(b)
    {
        cout<< "Con of second called"<< endl;
    }
    void sshow()
    {
        cout<< "sa="<< sa<< endl;
        cout<< "sb="<< sb<< endl;
    }
};
class third :public first, public second
{
    char str[10];
public :
    third(char*s, int x, int y, float z) :first(x),
        second(y,z)
    {
        strcpy(str,s);
        cout<< "Con of third called"<< endl;
    }
    void tshow()
    {
        fshow();
        sshow();
        cout << "str = " << str << endl;
    }
};

void main()
{
    clrscr();
    third t("Welcome",10,20,34.5f);
    t.tshow();
    getch();
}

OUTPUT :
Con of first called
Con of second called
Con of third called
fa=10
sa=20
sb=34.5
str=Welcome
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_471_0.png)

### Figure 9.14. Output screen of program 9.36

当语句 `third t("Welcome", 10, 20, 34.5f);` 执行时，类 third 的参数化构造函数被调用并传递 `("Welcome", 10, 20, 34.5f)`。在类 third 的构造函数内部，它们分别被收集在形式参数 s、x、y 和 z 中。从类 third 的构造函数中，使用 x 作为参数调用类 first 的构造函数。在类 first 中，此 x 被赋给 fa，并且 cout 显示 Con of first called。控制权返回到类 third 的构造函数，该构造函数现在调用类 second 的构造函数并传递参数 y 和 z。在类 second 的构造函数内部，它们被赋给 sa 和 sb，并且显示 Con of second called。当控制权返回到类 third 的构造函数时，它进入其主体，将 s 赋给 str 并显示 Con of third called。

## 9.8 CONTAINERSHIP

我们可以在一个类中创建另一个类的对象，并且该对象将成为该类的成员。这种类之间的关系称为 **has_a** 关系，因为一个类包含另一个类的对象。我们到目前为止看到的继承被认为是 **kind_of** 或 **is_a** 关系。

```cpp
/*PROG 9.38 DEMO OF CONTAINERSHIP VER 1*/

#include <iostream.h>
#include <conio.h>
class first
{
    public :
        void showf( )
        {
            cout<<"Hello from first"<<endl;
        }
};
class second
{
    first f;
    public :
    second( )
    {
        f.showf( );
    }
};
void main( )
{
    clrscr( );
    second s;
    getch( );
}

OUTPUT :
Hello from first
```

### EXPLANATION

在类 second 中我们有一个类 first 的对象。这是我们见证的另一种类型的继承。这种继承称为 has_a 关系，因为我们说类 second 具有类 first 的对象作为其成员。从此对象 f 我们调用类 first 的函数。

```cpp
/*PROG 9.39 DEMO OF CONTAINERSHIP VER 2*/

#include <iostream.h>
#include <conio.h>

class first
{
    private :
        int num;
    public :
        void showf( )
        {
            cout << "Hello from first" << endl;
            cout << "num=" << num << endl;
        }
        int &getnum( )
        {
            return num;
        }
};
class second
{
    first f;
    public :
        second( )
        {
            f.getnum( ) = 20;
            f.showf( );
        }
};
void main( )
{
    clrscr( );
    second s;
    getch( );
}

OUTPUT:
Hello from first
num=20
```

### EXPLANATION

借助 containership 我们只能使用类的 public 数据成员/函数，而不能使用 protected 或 private。在第一个类中，我们借助 getnum 函数返回引用。在类 second 的默认构造函数中，我们通过调用函数 getnum 将 20 的值赋给 first 类的 num。然后我们通过调用 showf 显示它。

```cpp
/* PROG 9.40 DEMO OF CONTAINERSHIP VER 3 */
#include <iostream.h>
#include <conio.h>

class first
{
private :
    int num;
public :
    void showf( )
    {
        cout<< "Hello from first"<<endl;
        cout<< "num="<<num<<endl;
    }
    int &getnum( )
    {
        return num;
    }
};

class second
{
    first f;
public :
    second( )
    {
        f.getnum()=200;
        f.showf( );
    }
};

void main( )
{
    clrscr( );
    second s;
    getch( );
}

OUTPUT :

Hello from first
num=200
```

### EXPLANATION

借助 containership 我们只能使用类的 public 数据成员/函数，而不能使用 protected 或 private。在第一个类中，我们借助 getnum 函数返回引用。在类 second 的默认构造函数中，我们通过调用函数 getnum 将 200 的值赋给 first 类的 num。然后我们通过调用 showf 显示它。

1. 继承是从现有类派生新类的机制。旧类和新类以一对的形式为人所知：super-sub、base-derived、parent-child。
2. 继承提供了重用的思想。一旦编写的代码可以在多个不同的类中反复使用。
3. C++ 提供了对以下内容的支持：单级和多级继承、多重继承、层次继承、混合继承。
4. 私有成员永远不会被继承。
5. 虚基类用于避免目标派生类中数据成员的重复。
6. 在继承层次结构中，首先调用基类的构造函数，然后调用派生类的构造函数。
7. 在继承层次结构中，首先调用派生类的析构函数，然后调用基类的析构函数。
8. Containership 允许我们将一个类的对象用作另一个类的成员。这种 containership 提供了 has_a 关系或类的嵌套的思想。

> EXERCISE

1. 公共变量可以从程序的任何地方访问。
2. 继承有助于代码维护。
3. 派生类通常被称为子类，因为它代表其基类的子集。
4. 基类的指针可以指向该基类的派生类的对象。
5. 如果未为派生类指定构造函数，则派生类的对象将使用基类中的构造函数。
6. 派生类的对象不能使用点运算符访问基类的公共成员。
7. 在多重继承中，所有构造函数都以派生顺序的逆序被调用，而析构函数以相同顺序被调用。
8. 不可能将基类指针分配给派生类对象。
9. 子类可以访问基类的 protected 成员，但不能访问 private 成员。
10. 当在多重继承中发生名称冲突时，歧义通过使用作用域解析运算符来解决。
11. 被声明为基类的友元的函数可以被派生类继承。
12. 子类可以访问父类的私有成员，但不能访问受保护成员。

