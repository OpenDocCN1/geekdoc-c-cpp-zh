
## 类析构函数

**析构函数**是类的一种特殊成员函数，当该类的对象离开作用域，或者对指向该类对象的指针应用 delete 表达式时，它都会被执行。

析构函数与类名完全相同，只是在前面加上波浪号（~），它既不能返回值，也不能接受任何参数。析构函数对于在程序退出前释放资源非常有用，例如关闭文件、释放内存等。

下面的示例解释了析构函数的概念：

```
#include <iostream>

using namespace std;

class Line
{
   public:
      void setLength( double len );
      double getLength( void );
      Line();   // This is the constructor declaration
      ~Line();  // This is the destructor: declaration

   private:
      double length;
};

// Member functions definitions including constructor
Line::Line(void)
{
   cout << "Object is being created" << endl;
}
Line::~Line(void)
{
cout << "Object is being deleted" << endl;
}

void Line::setLength( double len )
{
    length = len;
}

double Line::getLength( void )
{
    return length;
}

// Main function for the program
int main( )
{
    Line line;

    // set line length
    line.setLength(6.0);
    cout << "Length of line : " << line.getLength() << endl;

    return 0;
}
```

当上述代码被编译并执行时，会产生以下结果：

```
Object is being created

Length of line : 6

Object is being deleted
```

## 拷贝构造函数

```
return 0;
}
```

当上述代码被编译并执行时，会产生以下结果：

```
Normal constructor allocating ptr
Copy constructor allocating ptr.
Length of line : 10
Freeing memory!
Freeing memory!
```

让我们看看同一个示例，但做了一点修改，使用现有同类型对象来创建另一个对象：

```
#include <iostream>

using namespace std;

class Line
{
   public:
      int getLength( void );
      Line( int len );            // simple constructor
      Line( const Line &obj);     // copy constructor
      ~Line();                    // destructor

   private:
      int *ptr;
};

// Member functions definitions including constructor
Line::Line(int len)
{
      cout << "Normal constructor allocating ptr" << endl;
      // allocate memory for the pointer;
      ptr = new int;
*ptr = len;
}

Line::Line(const Line &obj)
{
    cout << "Copy constructor allocating ptr." << endl;
    ptr = new int;
    *ptr = *obj.ptr; // copy the value
}

Line::~Line(void)
{
    cout << "Freeing memory!" << endl;
    delete ptr;
}

int Line::getLength( void )
{
    return *ptr;
}

void display(Line obj)
{
    cout << "Length of line : " << obj.getLength() <<endl;
}

// Main function for the program
int main( )
{
    Line line1(10);

    Line line2 = line1; // This also calls copy constructor

    display(line1);
    display(line2);
```

```
friend class ClassTwo;
```

请考虑以下程序：

```
#include <iostream>

using namespace std;

class Box
{
    double width;
public:
    friend void printWidth( Box box );
    void setWidth( double wid );
};

// Member function definition
void Box::setWidth( double wid )
{
    width = wid;
}

// Note: printWidth() is not a member function of any class.
void printWidth( Box box )
{
    /* Because printWidth() is a friend of Box, it can
       directly access any member of this class */
    cout << "Width of box : " << box.width << endl;
}

// Main function for the program
int main( )
{
    Box box;
```

```
int main( )
{

    cout << "Max (20,10): " << Max(20,10) << endl;

    cout << "Max (0,200): " << Max(0,200) << endl;

    cout << "Max (100,1010): " << Max(100,1010) << endl;

    return 0;
}
```

当上述代码被编译并执行时，会产生以下结果：

```
Max (20,10): 20

Max (0,200): 200

Max (100,1010): 1010
```

## this 指针

C++ 中的每个对象都可以通过一个名为 **this** 指针的重要指针来访问其自身地址。**this** 指针是所有成员函数的隐式参数。因此，在成员函数内部，this 可用于指代调用该函数的对象。

友元函数没有 **this** 指针，因为友元不是类的成员。只有成员函数拥有 **this** 指针。

让我们尝试以下示例来理解 this 指针的概念：

```
#include <iostream>

using namespace std;

class Box
{
    public:

        // Constructor definition
        Box(double l=2.0, double b=2.0, double h=2.0)
        {
            cout << "Constructor called." << endl;
            length = l;
            breadth = b;
height = h;
}
double Volume()
{
    return length * breadth * height;
}
int compare(Box box)
{
    return this->Volume() > box.Volume();
}
private:
    double length;     // Length of a box
    double breadth;    // Breadth of a box
    double height;     // Height of a box
};

int main(void)
{
    Box Box1(3.3, 1.2, 1.5);    // Declare box1
    Box Box2(8.5, 6.0, 2.0);    // Declare box2

    if(Box1.compare(Box2))
    {
        cout << "Box2 is smaller than Box1" <<endl;
    }
    else
    {
        cout << "Box2 is equal to or larger than Box1" <<endl;
    }
    return 0;
}
```

当上述代码被编译并执行时，会产生以下结果：

```
Constructor called.
```

```
Constructor called.
Box2 is equal to or larger than Box1
```

## 指向 C++ 类的指针

指向 C++ 类的指针与指向结构的指针完全一样，要访问指向类的指针的成员，可以使用成员访问运算符 -> 运算符，这与访问指向结构的指针完全一样。另外，与所有指针一样，必须先初始化指针，然后才能使用它。

让我们尝试以下示例来理解指向类的指针的概念：

```
#include <iostream>

using namespace std;

class Box
{
    public:
        // Constructor definition
        Box(double l=2.0, double b=2.0, double h=2.0)
        {
            cout <<"Constructor called." << endl;
            length = l;
            breadth = b;
            height = h;
        }
        double Volume()
        {
            return length * breadth * height;
        }
    private:
        double length;    // Length of a box
        double breadth;   // Breadth of a box
        double height;    // Height of a box
};
```

让我们尝试以下示例来理解静态数据成员的概念：

```
#include <iostream>

using namespace std;

class Box
{
    public:
        static int objectCount;
        // Constructor definition
        Box(double l=2.0, double b=2.0, double h=2.0)
        {
            cout << "Constructor called." << endl;
            length = l;
            breadth = b;
            height = h;
            // Increase every time object is created
            objectCount++;
        }
        double Volume()
        {
            return length * breadth * height;
        }
    private:
        double length;      // Length of a box
        double breadth;     // Breadth of a box
        double height;      // Height of a box
};

// Initialize static member of class Box
int Box::objectCount = 0;

int main(void)
{

    Box Box1(3.3, 1.2, 1.5);    // Declare box1

    Box Box2(8.5, 6.0, 2.0);    // Declare box2


    // Print total number of objects.
    cout << "Total objects: " << Box::objectCount << endl;


    return 0;
}
```

当上述代码被编译并执行时，会产生以下结果：

```
Constructor called.

Constructor called.

Total objects: 2
```

## 静态函数成员

通过将函数成员声明为 static，可以使其独立于类的任何特定对象。即使类的对象不存在，也可以调用静态成员函数，并且**static** 函数只能使用类名和作用域解析运算符 **::** 来访问。

静态成员函数只能访问静态数据成员、其他静态成员函数以及类外部的任何其他函数。

静态成员函数具有类作用域，它们无法访问类的 **this** 指针。您可以使用静态成员函数来确定是否已创建该类的某些对象。

让我们尝试以下示例来理解静态函数成员的概念：

```
#include <iostream>

using namespace std;

class Box
{

    public:

        static int objectCount;

        // Constructor definition
```
