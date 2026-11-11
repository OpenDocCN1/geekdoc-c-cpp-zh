

```cpp
virtual void area()
{}
virtual void display()
{}
};

class Rectangle:public Shape
{
    public:
    void get_data()
    {
        cout<<"Enter the length of rectangle"<<endl;
        cin>>x;
        cout<<"Enter the breadth of rectangle"<<endl;
        cin>>y;
    }
    void area()
    {
        arearect=x*y;
    }
    void display()
    {
        cout<<"Area of rectangle = "<<arearect<<endl;
    }
};

class Triangle:public Shape
{
    public:
    void get_data()
    {
        cout<<"Enter the height of the triangle"<<endl;
        cin>>x;
        cout<<"Enter the base of the triangle"<<endl;
        cin>>y;
    }
    void area()
    {
        areatri=(x*y)/2;
    }
    void display()
    {
        cout<<"Area of triangle = "<<areatri<<endl;
    }
};

void main()
{
    Shape *p;
    Rectangle r1;
    Triangle t1;
    p=&r1;
    p->get_data();
    p->area();
    p->display();
    p=&t1;
    p->get_data();
    p->area();
    p->display();
}
```

```text
Output:

Enter the length of rectangle
20
Enter the breadth of rectangle
5
Area of rectangle = 100
Enter the height of the triangle
50
Enter the base of the triangle
35
Area of triangle = 875
```

**第10题.** 创建一个程序，使用基类的引用来访问虚函数。

答案：

```cpp
#include <iostream.h>

class A {
public:
    virtual void myFunc() {
        cout << "This is A's myFunc().\n";
    }
};
class B1 : public A {
public:
    void myFunc() {
        cout << "This is B1's myFunc().\n";
    }
};
class B2 : public A {
public:
    void myFunc() {
        cout << "This is B2's myFunc().\n";
    }
};
// Use a A class reference parameter.
void f(A &r) {
    r.myFunc();
}
int main()
{
    A aObj;
    B1 b1Obj;
    B2 b2Obj;
    f(aObj);  // passing A object to f()
    f(b1Obj); // passing B1 object to f()
    f(b2Obj); // passing B2 object to f()
    return 0;
}
```

```text
Output:

This is A's myFunc().
This is B1's myFunc().
This is B2's myFunc().
```

**第11题.** 创建一个程序，使用基类的引用来访问虚函数。

答案：

```cpp
#include <iostream.h>

class Book
{
public:
    virtual void getDescription() { cout<<"Book"<<endl; }
};
class Suspense : public Book
{
public:
    virtual void getDescription() {
        cout<<"Suspense ";
        Book::getDescription();
    }
};
class Thriller : public Suspense
{
public:
    virtual void getDescription() {
        cout<<"Thriller ";
        Suspense::getDescription();
    }
};
class Technical : public Thriller
{
public:
    virtual void getDescription() {
        cout<<"Technical ";
        Thriller::getDescription();
    }
};
void main()
{
    Technical tech;
    Book book;
    tech.getDescription();
    book.getDescription();
}
```

```text
Output:

Technical Thriller Suspense Book
Book
```

### 解释静态绑定与动态绑定之间的区别

静态绑定是指在编译时将函数调用与正确的函数定义相匹配的绑定。而动态绑定是指在运行时将函数调用与正确的函数定义相匹配的绑定。如果你希望编译器对特定函数使用动态绑定，可以使用 virtual 关键字声明该函数。

静态绑定被认为更高效，而动态绑定更灵活。在动态绑定中，对函数各种形式的调用会在程序执行时动态解析。如你所知，术语“后期绑定”指的是在运行时而非编译时解析函数。这一特性允许根据上下文调用适当的方法，从而提高了程序的灵活性。

对于动态绑定，函数调用在运行时解析，从而使用户无需修改代码即可更改调用。对于程序员来说，效率和性能可能是首要关注点，但用户可能更看重灵活性和可维护性。静态绑定是静态多态概念的实际实现，而动态绑定则代表动态多态。静态绑定通过函数和运算符的重载实现。它受作用域约束，包括局部作用域（块作用域）和类作用域。另一方面，动态绑定基于重写原则，该原则与类作用域相关，并基于继承。

## 创建纯虚函数

可以观察到，基类的虚函数常常不会被使用。例如，让我们考虑包含三个类的情况：Polygon、Rectangle 和 Triangle。Polygon 是 Rectangle 和 Triangle 类的基类，并有一个虚函数 `area()`。在现实场景中，只有定义了多边形的具体形状（例如三角形或矩形），才能计算多边形的面积。因此，除非我们定义多边形的形状，否则多边形的面积没有意义。因此，如果在示例中需要计算多边形的面积，我们必须指明它是矩形还是三角形。这样，我们实际上使用的是派生类（Rectangle 或 Triangle）的 `area()` 函数。

请注意，在这种情况下，基类可以不定义虚函数的主体。

没有主体结构的虚函数称为纯虚函数。你可以通过在虚函数声明中添加 `=0` 表示法来声明纯虚函数。例如，`area()` 是一个虚函数，但当它像下面的表达式那样声明时，就变成了纯虚函数：

```cpp
virtual int area() = 0;
```

清单39演示了如何在基类中编写纯虚函数（你可以在 CD 的 Code\Chapter7 文件夹中找到 PureVirtualFunction.cpp 文件）：

**清单39：** 在基类中创建纯虚函数

```cpp
#include <iostream.h>

class Polygon
{
protected:
    int width, height;
public:
    void setup (int first, int second)
    {
        width= first;
        height= second;
    }
    virtual int area() = 0;
};

class Rectangle: public Polygon
{
public:
    int area()
    {
        return (width * height);
    }
};

class Triangle: public Polygon
{
    public:
        int area()
        {
            return (width * height / 2);
        }
};
int main ()
{
    Rectangle rectangle;
    Triangle triangle;
    Polygon *polygon;
    Polygon * ptr_polygon1 = &rectangle;
    Polygon * ptr_polygon2 = &triangle;
    ptr_polygon1->setup(2,2);
    ptr_polygon2->setup(2,2);
    cout << ptr_polygon1->area () << endl;
    cout << ptr_polygon2->area () << endl;

    return 0;
}
```

```text
Output:

4
2
```

在清单39中，`area()` 函数被声明为基类 Polygon 中的纯虚函数。它被 Rectangle 和 Triangle 类重写。

## 测试你的知识

**第12题.** 创建一个可以将升转换为加仑、华氏度转换为摄氏度的程序。（提示：使用多重继承。）

答案：

```cpp
#include <iostream.h>
class Converter {
    protected:
        double val1;  // initial value
        double val2;  // Converted value
    public:
        Converter(double i) {
            val1 = i;
        }
        double getConvertedValue() { return val2; }
        double setvalue() { return val1; }
        virtual void compute() = 0;
};
// Liters to gallons.
class LitreToGallon : public Converter {
public:
    LitreToGallon(double i) : Converter(i) { }
    void compute() {
        val2 = val1 / 3.7854;

    }
};
// Fahrenheit to Celsius
class FahrenheitToCelsius : public Converter {
public:
    FahrenheitToCelsius(double i) : Converter(i) { }
    void compute() {
        val2 = (val1-32) / 1.8;
    }
};
int main()
{
    Converter *p;  // pointer to base class
    LitreToGallon lgb(10);
    FahrenheitToCelsius fcb(100);
    // use virtual function mechanism to Converter
    p = &lgb;
    cout << p->setvalue() << " liters is ";
    p->compute();
    cout << p->getConvertedValue() << " gallons\n";
    p = &fcb;
    cout << p->setvalue() << " in Fahrenheit is ";
    p->compute();
    cout << p->getConvertedValue() << " Celsius\n";
    return 0;
}
```

```text
Output:

10 liters is 2.641729 gallons
100 in Fahrenheit is 37.777778 Celsius
```

### 创建抽象类

在现实世界中，并非所有对象都能以同样的方式建模。事实上，有些类过于抽象，无法独立存在。例如，如果有人让你画一个形状，你可能会要求指定具体形状。术语“形状”是一个抽象概念；它可以是圆形、正方形等等。在 C++ 中，我们将基类创建为抽象基类。

