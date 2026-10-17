
```cpp
float cost;
public:
void getdata()
{
    cout<<"Enter Seat Section & Cost: "<<endl;
    cin>>ss>>cost;
}
void showdata()
{
    cout<<"Seat : "<<ss<<endl;
    cout<<"Cost: "<<cost<<endl;
}
};
class ring2
{
private:
    float spectators[3];
public:
void getdata()
{
    int i;
    for(i=0;i<3;i++)
    {
        cout<<"\nEnter "<<i+1<<" Section Spectators ";
        cin>> spectators[i];
    }
}
void showdata()
{
    int i;
    for(i=0;i<3;i++)
    {
        cout<<"\n"<<i+1<<" Section Spectators = "<<spectators[i];
    }
}
};

class arena:public ring1,public ring2
{
private :
    int guest;
public:
ring1 r1;
ring2 r2;
void getdata()
{
    r1.getdata();
    cout<<"Enter guest";
    cin>>guest;
    r2.getdata();
}
void showdata()
{
    cout<<"\nGuest count = "<<guest<<endl;
    r2.showdata();
}
};

int main()
{
    arena obj1;
    obj1.getdata();
    obj1.showdata();

    return 0;
}
```

### 输出

```text
Enter Seat Section & Cost:
4
3500
Enter guest4

Enter 1 Section Spectators 230

Enter 2 Section Spectators 345

Enter 3 Section Spectators 445

Guest count = 4
1 Section Spectators = 230
2 Section Spectators = 345
3 Section Spectators = 445
```

### 代码解读

- 在这段代码中，我们使用多重继承在三个类之间建立了关系。

- 在这里，子类将能够继承甚至修改两个父类的属性，因为它们的访问权限在基类中声明。

- 子类的对象可以访问所有成员，除了基类或父类中的私有成员。

### 4. 虚拟继承

*虚拟继承*在多重继承中出现这样的情形时发挥作用：两个不同的基类继承自同一个超类，并且它们从超类继承的成员名称相同。此时，这两个基类的子类将同时拥有来自两个父类的超类方法副本，这被称为*菱形问题*。菱形问题会导致当对象按名称访问某个方法时，无法确定实际调用的是超类的哪个继承方法。解决此问题的方法是使用 C++ 中的虚拟继承特性，即让两个父类以虚拟方式继承超类。

![](img/4d9a4ae4efedabe01be6e6c44bad2dc1_130_0.png)

*图 6.5 虚拟继承*

虚拟继承的语法如下：

```cpp
class A
{
    // class body
};
class B : accessMode virtual A
{
    // class body
};
class C : accessMode virtual A
{
    // class body
};
class D : accessMode B, accessMode C
{
    // class body
};
```

#### 代码：使用虚拟继承

```cpp
#include <iostream>
using namespace std;
class pg
{
    public:
    int age;
    void display1()
    {
        cout<<"Enter your age"<<endl;
        cin>>age;
    }
};

class student : public virtual pg
{
    public :
    string name;
    void display2()
    {
        cout<<"Enter your name"<<endl;
        cin>>name;
    }
};
class exam: public virtual pg
{
    public :
    int ecode;
    void display3()
    {
        cout<<"Enter exam code"<<endl;
        cin>>ecode;
    }
};
class external : public student, public exam
{
    public :
    int marks;
    void display4()
    {
        cout<<"Enter your Level 1 marks"<<endl;
        cin>>marks;
    }
    void check()
    {
        if ((age>17)&&(marks>65))
        {
            cout<<"\nAllowed for Level 2 Examination\n";
        }
        else
            cout<<"Start looking for backups";
    }
};
int main()
{
    external e;
    cout<<"Enter your valid information"<<endl;
    e.display1();
    e.display2();
    e.display3();
    e.display4();
    e.check();
    return 0;
}
```

#### 输出

```text
Enter your valid information
Enter your age
20
Enter your name
Yash
Enter exam code
23099
Enter your Level 1 marks
68

Allowed for Level 2 Examination
```

#### 代码解读

- 在这段代码中，我们使用虚拟继承在两个类之间建立了关系。

- 这是解决多重继承问题所必需的。

- 在这里，只有子类现在能够从父类继承并修改属性，因为所有成员在基类中声明的访问权限相同。

- 子类的对象可以访问所有成员，除了基类或父类中的私有成员。

### 5. 层次继承

*层次继承*是指多个派生类继承自同一个基类的情况。这种继承具有树状结构，因为每个类都作为一个或多个子类的基类。层次继承的语法如下：

```cpp
class A
{
    // class body
};
class B : accessMode  A
{
    // class body
};
class C : accessMode A
{
    // class body
};
class D : accessMode B
{
    // class body
};
class E : accessMode C
{
    // class body
};
```

![](img/4d9a4ae4efedabe01be6e6c44bad2dc1_134_0.png)

*图 6.6 层次继承*

#### 代码：使用层次继承

```cpp
#include <iostream>
using namespace std;
class f1Car
{
    protected :
        string team;
    public:
    void getdata()
    {
        cout<<"Enter team name"<<endl;
        cin>>team;
    }
    void showdata()
    {
        cout<<"Team Name : "<<team<<endl;
    }
};
class engine : public f1Car
{
    protected :
        int LmotrNO;
    public:
    void getdata()
    {
        f1Car :: getdata();
        cout<<"Enter light motor number: ";
        cin>>LmotrNO;
    }
    void showdata()
    {
        f1Car:: showdata();
        cout<<"LMotor No = "<<LmotrNO<<endl;
    }

};
class hydraulic : public f1Car
{
protected:
    float price;
public :
    void getdata()
    {
        f1Car :: getdata();
        cout<<"Enter heavy motor price: ";
        cin>>price;
    }
    void showdata()
    {
        f1Car :: showdata();
        cout<<"HMotor Price = "<<price<<endl;
    }

};
class fuel: public engine
{
protected :
    int capacity;
public:
    void getdata()
    {
        engine :: getdata();
        cout<<"Enter Gear motor capacity: ";
        cin>>capacity;
    }
    void showdata()
    {
        engine :: showdata();
        cout<<"GMotor Capacity = "<<capacity<<endl;
    }

};
class nofuel : public engine
{
    protected :
    int capacity;
    public:
    void getdata()
    {
        engine :: getdata();
        cout<<"Enter Non Gear motor capacity: ";
        cin>>capacity;
    }
    void showdata()
    {
        engine :: showdata();
        cout<<"NonGMotor Capacity = "<<capacity<<endl;
    }
};
class race : public hydraulic
{
    protected :
    int passNo;
    public:
    void getdata()
    {
        hydraulic :: getdata();
        cout<<"Enter passenger capacity: ";
        cin>>passNo;
    }
    void showdata()
    {
        hydraulic:: showdata();
        cout<<"Passenger Capacity = "<<passNo<<endl;
    }
};
class sprint : public hydraulic
{
    protected :
        int maxLoad;
    public:
        void getdata()
        {
            hydraulic :: getdata();
            cout<<"Enter max goods load: ";
            cin>>maxLoad;
        }
        void showdata()
        {
            hydraulic :: showdata();
            cout<<"GMotor Capacity = "<<maxLoad<<endl;
        }

};
int main()
{
    fuel f1;
    race r1;
    cout<<"Enter details of vehicle: "<<endl;
    f1.getdata();
    r1.getdata();
    cout<<"Vehicle Specifications are: "<<endl;
    f1.showdata();
    r1.showdata();
}
```

#### 输出

```text
Enter details of vehicle:
Enter team name
Redbull
Enter light motor number: 27789
Enter Gear motor capacity: 4900
Enter team name
Redbull
Enter heavy motor price: 4500000
Enter passenger capacity: 1
Vehicle Specifications are:
Team Name : Redbull
LMotor No = 27789
GMotor Capacity = 4900
Team Name : Redbull
HMotor Price = 4500000
Passenger Capacity = 1
```

### 6. 混合继承

最后，*混合继承*是我们所学过的所有继承类型的混合。

#### 代码：使用混合继承

```cpp
#include <iostream>
using namespace std;
class pg
{
    public:
    int age;
    void display1()
    {
        cout<<"Enter your age"<<endl;
        cin>>age;
    }
};

class student : public pg
{
    public :
    string name;
    void display2()
    {
        cout<<"Enter your name"<<endl;
        cin>>name;
    }
};
class exam
{
    public :
    int ecode;
    void display3()
{
    cout<<"Enter exam code"<<endl;
    cin>>ecode;
}
};
class external : public student, public exam
{
    public :
    int marks;
    void display4()
    {
        cout<<"Enter your Level1 marks"<<endl;
        cin>>marks;
    }
    void check()
    {
        if ((age>17)&&(marks>65))
        {
            cout<<"\nAllowed for Level 2 Examination :)\n";
        }
        else
            cout<<"Start looking for backups :(( \n";
    }
};
int main()
{
    external e;
    cout<<"Enter your valid information"<<endl;
    e.display1();
    e.display2();
    e.display3();
    e.display4();
    e.check();
    return 0;
}
```

#### 输出

```text
Enter your valid information
Enter your age
20
Enter your name
Mick
Enter exam code
203
Enter your Level1 marks
24
Start looking for backups :((
```

## 6.4 构造函数调用

在上一章中，我们讨论了类的创建和方法，以及构造函数等特殊方法及其各种类型。在那里，我们只涉及单个类，但在继承中，总会涉及多个类。构造函数调用是如何工作的？让我们来看看。

### 记住

- 无论创建何种对象，基类构造函数总是首先被调用。

- 创建派生类对象会初始化其所有成员，但它也有继承来的成员。因此，先调用基类构造函数，以便派生类中的所有成员都能初始化。

- 在多重继承中，基类的放置顺序将决定调用哪个构造函数。

- 析构函数总是以与构造函数相反的顺序被调用。

调用构造函数的语法如下：
