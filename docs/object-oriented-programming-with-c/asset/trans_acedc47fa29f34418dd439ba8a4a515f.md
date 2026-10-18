

```cpp
void show_a(void);
};
class D : private B// private derivation
{
int c;
public:
void mul(void);
void display(void);
};
//--------------------------------------------------
void B :: get_ab(void)
{
cout << "Enter values for a and b: ";
cin >> a >> b;
}
int B :: get_a()
{
return a;
}
void B :: show_a()
{
cout << "a = " << a << "\n";
}
void D :: mul()
{
get_ab();
c = b * get_a();// 'a' cannot be used directly
}
void D :: display()
{
show_a();// outputs value of 'a'
cout << "b = " << b << "\n" << "c = " << c << "\n";
}
//
int main()
{
D d;
// d.get_ab(); WON'T WORK
d.mul();
// d.show_a(); WON'T WORK
d.display();
// d.b = 20; WON'T WORK; b has become private
d.mul();
d.display();
return 0;
}
```

程序 8.2 的输出为：

```
Enter values for a and b: 5 10
a = 5
b = 10 c = 50
Enter values for a and b: 12 20
a = 12
b = 20 c = 240
```

假设一个基类和一个派生类定义了同名函数。当派生类对象调用该函数时会发生什么？在这种情况下，派生类的函数会取代基类的定义。但是，如果派生类没有重新定义该函数，那么将调用基类的函数。

## 8.4 使私有成员可继承

我们刚刚了解了如何在不修改现有类的情况下增强其功能。我们也看到，基类的私有成员不能被继承，因此派生类无法直接使用它。如果私有数据需要被派生类继承，我们该怎么办？可以通过将私有成员的可见性限制改为公有来实现。但这会使程序中的所有其他函数都能访问它，从而失去数据隐藏的优势。

C++ 提供了第三种可见性修饰符 protected（受保护），它在继承中具有有限的作用。声明为 protected 的成员可以被其类内的成员函数以及直接从其派生的任何类的成员函数访问。这两个类之外的函数不能访问它。一个类现在可以使用如下所示的全部三种可见性模式：

```cpp
class alpha
{
    private: // optional
    .....// visible to member functions
    .....// within its class
    protected:
    .....// visible to member functions
    .....// of its own and that of derived class
    public:
    .....// visible to all functions
    .....// in the program
};
```

当一个 protected 成员以公有模式被继承时，它在派生类中也成为 protected，因此可以被派生类的成员函数访问。同时它也准备好被进一步继承。protected 成员以私有模式派生继承时，会成为派生类中的私有成员。虽然派生类的成员函数可以使用它，但它不能用于进一步继承（因为私有成员不能被继承）。图 8.4 是这两种派生级别的图示。

关键字 private、protected 和 public 在类的声明中可以按任意顺序、任意次数出现。例如，

```cpp
protected:
public:
};
```

也可以在 **保护**模式下继承基类（称为_保护派生_）。在保护派生中，基类的 **公有**和**保护**成员都成为派生类的 **保护**成员。表 8.1 总结了在全部三种派生类型中基类成员的可见性会如何变化。

| 基类可见性 | | 公有派生 | 私有派生 | 保护派生 |
|---|---|---|---|---|
| 私有 | → | 不被继承 | 不被继承 | 不被继承 |
| 保护 | → | 保护 | 私有 | 保护 |
| 公有 | → | 公有 | 私有 | 保护 |

1. 类的友元函数。
2. 友元类的成员函数。
3. 派生类的成员函数。

友元函数和友元类的成员函数可以直接访问 **私有**和**保护**数据，而派生类的成员函数只能直接访问 **保护**数据。但是，它们可以通过基类的成员函数访问 **私有**数据。图 8.5 展示了在各种情况下访问控制机制是如何工作的。图 8.6 给出了对类成员访问控制的一种简化视图。

![](img/62b7c32e48e4f960a8dc2825a7119fb2_322_0.png)

## 8.5 多级继承

如图 8.7 所示，从一个派生类再派生出另一个类的情况并不少见。类 A 作为派生类 B 的基类，而 B 又作为派生类 C 的基类。类 B 被称为_中间基类_，因为它为 A 和 C 之间的继承提供了链接。链 ABC 被称为继承路径。

![](img/62b7c32e48e4f960a8dc2825a7119fb2_322_1.png)

图 8.6 对类成员访问控制的一种简化视图

![](img/62b7c32e48e4f960a8dc2825a7119fb2_323_0.png)

图 8.7 多级继承

![](img/62b7c32e48e4f960a8dc2825a7119fb2_323_1.png)

具有多级继承的派生类声明如下：

```cpp
class A{ }; // Base class
class B: public A { }; // B derived from A
class C: public B { }; // C derived from B
```

这个过程可以扩展到任意级数。

让我们看一个简单的例子。假设一批学生的测试结果存储在三个不同的类中。类 **student** 存储学号，类 **test** 存储两门科目取得的分数，类 **result** 包含测试中取得的**总**分。类 **result** 可以通过多级继承获得测试成绩的详细信息以及学生的学号。示例：

```cpp
class student
{
protected:
int roll_number;
public:
void get_number(int);
void put_number(void);
};
void student :: get_number(int a)
{
roll_number = a;
}
void student :: put_number( )
{
cout << "Roll Number: " << roll_number << "\n";
}
class test : public student// First level derivation
{
protected:
float sub1;
float sub2;
public:
void get_marks(float, float);
void put_marks(void);
};
void test :: get_marks(float x, float y)
{
sub1 = x;
sub2 = y;
}
void test :: put_marks()
{
cout << "Marks in SUB1 = " << sub1 << "\n";
cout << "Marks in SUB2 = " << sub2 << "\n";
}
class result : public test// Second level derivation
{
float total; // private by default
public:
void display(void);
};
```

类 **result** 经过从“祖父”经“父亲”的继承后，将包含以下成员：

```cpp
private:
float total; // own member
protected:
int roll_number; // inherited from student
// via test
float sub1; // inherited from test
float sub2; // inherited from test
public:
void get_number(int); // from student via test
void put_number(void); // from student via test
void get_marks(float, float); // from test
void put_marks(void); // from test
void display(void); // own member
```

继承的函数 `put_number()` 和 `put_marks()` 可用于 `display()` 函数的定义中：

```cpp
void result :: display(void)
{
    total = sub1 + sub2;
    put_number(); put_marks();
    cout << "Total = " << total << "\n";
}
```

下面是一个简单的 `main()` 程序：

```cpp
int main()
{
    result student1; // student1 created
    student1.get_number(111);
    student1.get_marks(75.0, 59.5);
    student1.display();
    return 0;
}
```

这将显示 **student1** 的结果。完整程序见程序 8.3。

```cpp
{
cout << "Marks in SUB1 = " << sub1 << "\n";
cout << "Marks in SUB2 = " << sub2 << "\n";
}
class result : public test // Second level derivation
{
float total; // private by default
public:
void display(void);
};
void result :: display(void)
{
total = sub1 + sub2;
put_number();
put_marks();
cout << "Total = " << total << "\n";
}
int main()
{
result student1; // student1 created
student1.get_number(111);
student1.get_marks(75.0, 59.5);
student1.display();
return 0;
}
```

程序 8.3 的输出为：

```
Roll Number: 111
Marks in SUB1 = 75
Marks in SUB2 = 59.5
Total = 134.5
```

## 8.6 多重继承

