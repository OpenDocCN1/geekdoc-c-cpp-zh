

# /*PROG 10.21 DEMO OF PURE VIRTUAL FUNCTION VER 4*/

```
#include <iostream.h>
#include <conio.h>
class first
{
public :
    void virtual show( ) =0;
};
class second :public first
{
public :
    void show( )
    {
        cout<<"Show of second"<<endl;
    }
};
class third :public first
{
public :
    void show( )
    {
        cout<<"Show of third"<<endl;
    }
};
void main( )
{
    clrscr( );
    second s;
    third t;
    int i;
    first &ref1 =s;
    first &ref2 =t;
    ref1.show( );
    ref2.show( );
    getch( );
}
```

# OUTPUT :

Show of second

Show of third

EXPLANATION : 该程序与前一个程序类似，不同之处在于我们没有使用指针，而是创建了两个类 first 类型的引用变量，并在其中分配了类 second 和类 third 的引用对象，如下所示：
first & ref1 = s;
first & ref2 = t;
因此当 ref1.show () ; 执行时，会调用类 second 的 show，而当 ref2.show () ; 执行时，会调用类 third 的 show。

```
/*PROG 10.22 DEMO OF PURE VIRTUAL FUNCTION VER 5 */
#include <iostream.h>
#include <conio.h>

class first
{
public :
void virtual show() =0;
void disp()
{
cout << "Display of first" << endl;
}
virtual void silly ()
{
cout << "Silly of first" << endl;
}
};

class second :public first
{
public :
void show ()
{
cout << "Show of second" << endl;
}
void disp ()
{
cout << "Display of second" << endl;
}
};

class third :public first
{
public :
void show ()
{
cout << "Show of third" << endl;
}
void disp ()
{
cout << "Display of third" << endl;
}
};
```

```
public :
    void show( )
    {
        cout<<"Show of third"<<endl;
    }
    void silly( )
    {
        cout<<"silly of third"<<endl;
    }
};

void main( )
{
    clrscr( );
    second s;
    third t;
    int i;
    first *ptr[ ] ={&s,&t};
    for(i=0;i<2;i++)
    {
        ptr[i]->show( );
        ptr[i]->silly( );
        ptr[i]->disp( );
    }
    getch( );
}
```

# OUTPUT :

Show of second
Silly of first
Display of first
Show of third
silly of third
Display of first

EXPLANATION : 该程序演示了这样一个事实：除了创建纯虚函数使类成为抽象类之外，我们还可以在抽象类中编写普通的函数。类 first 中有三个函数：

+   (a) show( ) 是一个纯虚函数，
+   (b) disp ( ) 是一个普通函数
+   (c) silly ( ) 是一个虚函数。

## Object-Oriented Programming C++ Simplified

类 second 提供了函数 show 的实现并重写了函数 disp。类 third 也提供了函数 show 的实现并重写了在类 first 中存在的 silly 函数。

在 main 中，我们将类 second 和类 third 的对象地址分配给 first 类指针的数组，如下所示：

```
first *ptr [] = (&s, &t);
```

在 for 循环中对于 i=0; ptr[0] 引用一个类 second 类型的对象，现在对于以下函数调用。

```
ptr[0]->show( );
ptr[0]->silly( );
ptr[0]->disp ( );
```

会调用类 second 的 show，这从代码中显而易见。Silly 在类 first 中是虚函数，且在类 second 中未被重写，因此会调用类 first 的 silly。disp 在类 second 中未被重写且 disp 在类 first 中不是虚函数，所以会调用类 first 的 disp。

现在对于 i = 1, ptr[1] 引用一个类 third 类型的对象。对于以下函数调用

```
ptr[1]->show();
ptr[1]->silly();
ptr[1]->disp();
```

```
/*PROG 10.23 FINDING FLYING STATUS OF VARIOUS INSECTS */
#include <iostream.h>
#include <conio.h>

class Insect
{
public :
	virtual void flystatus()=0;
};
class Cockroach :public Insect
{
public :
	void flystatus()
	{
		cout << "Cockroach can fly" << endl;
	}
};
```

```
class Termite :public Insect
{
public :
    void flystatus( )
    {
        cout<< "Termite cannot fly"<<endl;
    }
};
class Grasshopper :public Insect
{
public :
    void flystatus( )
    {
        cout<< "Grasshopper can fly"<<endl;
    }
};
class Ant : public Insect
{
public :
    void flystatus( )
    {
        cout<< "Ant cannot fly"<<endl;
    }
};
void main( )
{
    clrscr( );
    Insect *ptr[4];
    ptr[0]=new Cockroach;
    ptr[1]=new Termite;
    ptr[2]=new Grasshopper;
    ptr[3]=new Ant;
    for(int i=0;i<4;i++)
        ptr[i]->flystatus( );
    getch( );
}

OUTPUT :
Cockroach can fly
Termite cannot fly
Grasshopper can fly
Ant cannot fly
```

**EXPLANATION** : 类 **Insect** 声明了一个 **纯虚函数 flystatus**。任何继承该类的类都必须重新定义此函数并说明其飞行状态 *即*，是否能飞行。该类 **Insect** 被 **4 个不同的类** 继承，分别是 **Cockroach, Termite, Grasshopper** 和 **Ant**。每个类都提供了函数 **flystatus** 的实现。在 **main** 函数中我们创建一个类 **Insect** 类型的指针数组 **ptr**。在这个数组的每个位置我们分配动态创建的各种派生类对象，如下所示：

```
ptr[0] = new Cockroach;
ptr[1] = new Termite;
ptr[2] = new Grasshopper;
ptr[3] = new Ant;
```

在 **for** 循环中当我们使用此指针数组 **ptr** 调用 **flystatus** 函数时，会调用每个类的相应 **flystatus** 函数。

```
/*PROG 10.24 TO FIND THE COLOR OF VEGETABLE AND WHERE THEY GROW*/

#include <iostream.h>
#include <conio.h>

class Vegetable
{
public :
    virtual void color( ) = 0;
    virtual void wh_grow( ) = 0;
};
class Spinach :public Vegetable
{
public :
    void color( )
    {
        cout << "Color of spinach is green" << endl;
    }
    void wh_grow( )
    {
        cout << "Spinach grows above ground" << endl;
    }
};
class Potato :public Vegetable
{
public :
    void color( )
    {
        cout << "Color of Potato is white" << endl;
    }
```

```
void wh_grow()
{
    cout<<"Potato grows underground"<<endl;
}
};
class Onion :public Vegetable
{
public :
    void color()
    {
        cout<<"Color of Onion is red "<<endl;
    }
    void wh_grow()
    {
        cout<<"Onion grows underground"<<endl;
    }
};
class Tomato :public Vegetable
{
public :
    void color()
    {
        cout<<"Color of Tomato is red"<<endl;
    }
    void wh_grow()
    {
        cout<<"Tomato grows above ground"<<endl;
    }
};
void main()
{
    clrscr();
    Vegetable *ptr[4];
    ptr[0]=new Spinach;
    ptr[1]=new Potato;
    ptr[2]=new Onion;
    ptr[3]=new Tomato;
    for(int i=0;i<4;i++)
    {
        ptr[i]->color();
        ptr[i]->wh_grow();
```

## Object-Oriented Programming C++ Simplified

```
}

getch( );

}
```

+   OUTPUT :
+   Color of spinach is green
+   Spinach grows above ground
+   Color of Potato is white
+   Potato grows under ground
+   Color of Onion is red
+   Onion grows under ground
+   Color of Tomato is red
+   Tomato grows above ground

类 vegetable 声明了两个纯虚函数。函数 color 用于查找蔬菜的颜色，wh_grow 用于查找蔬菜生长在地下还是地上。任何继承 Vegetable 类的类都必须重新定义这些函数并说明蔬菜的颜色是什么以及它生长在哪里。该类 Vegetable 被 4 个不同的类继承，分别是 Spinach, Potato, Onion 和 Tomato。每个类都提供了两个函数的实现。在 main 中我们创建一个类 Vegetable 类型的指针数组。在这个数组的每个位置我们分配动态创建的各种派生类对象，如下所示：

ptr[0]=new Spinach;
ptr[1]=new Potato;
ptr[2]=new Onion;
ptr[3]=new Tomato;

/*PROG 10.25 CHECKING WHETHER SWEET CONTAINS MAWA AS ITS MAIN INGREDIENT */
#include <iostream.h>
#include <conio.h>

class Sweet 
{
public :
virtual void mawastatus( ) = 0;
};

class Burfi :public Sweet 
{
public :
void mawastatus( )
{
}
}
```

```
cout<<"Burfi has mawa as one of its main ingredient"<<endl;
}
};
class Kajukatli :public Sweet
{
public :
    void mawastatus( )
    {
        cout<<"Kajukatli does not have mawa as one of its main ingredient"<<endl;
    }
};
class Jalebee :public Sweet
{
public :
    void mawastatus( )
    {
        cout<<"Jalebee does not have mawa as one of its main ingredient"<<endl;
    }
};
class Rasgulla :public Sweet
{
public :
    void mawastatus ( )
    {
        cout<<"Rasgulla does not have mawa as one of its main ingredient "<<endl;
    }
};
void main( )
{
    clrscr( );
    Burfi B;
    Kajukatli k;
    Jalebee J;
    Rasgulla R;
    Sweet *ptr[4]={&B,&k,&J,&R};
    for(int i=0;i<4;i++)
    {
        ptr[i]->mawastatus( );
    }
    getch( );
}
```
