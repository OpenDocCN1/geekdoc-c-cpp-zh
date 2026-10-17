

```cpp
}
friend ostream &operator<<( ostream &output,
                            const Distance &D )
{
    output << "F : " << D.feet << " I : " << D.inches;
    return output;
}

friend istream &operator>>( istream &input, Distance &D )
{
    input >> D.feet >> D.inches;
    return input;
}
};
int main()
{
    Distance D1(11, 10), D2(5, 11), D3;

    cout << "Enter the value of object : " << endl;
    cin >> D3;
    cout << "First Distance : " << D1 << endl;
    cout << "Second Distance :" << D2 << endl;
    cout << "Third Distance :" << D3 << endl;

    return 0;
}
```

当上面的代码被编译并执行时，会产生以下结果：

```text
$ ./a.out
Enter the value of object :

70

10

First Distance : F : 11 I : 10
Second Distance :F : 5 I : 11
Third Distance :F : 70 I : 10
```

## ++ 和 -- 运算符重载

自增（++）和自减（--）运算符是 C++ 中两个重要的单目运算符。

下面的示例解释了如何为前缀和后缀用法重载自增（++）运算符。类似地，你也可以重载运算符（--）。

```cpp
#include <iostream>

using namespace std;


class Time
{
    private:
        int hours;             // 0 to 23
        int minutes;           // 0 to 59
    public:
        // required constructors
        Time(){
            hours = 0;
            minutes = 0;
        }
        Time(int h, int m){
            hours = h;
            minutes = m;
        }
        // method to display time
        void displayTime()
        {
            cout << "H: " << hours << " M:" << minutes <<endl;
        }
        // overloaded prefix ++ operator
        Time operator++ ()
        {
            ++minutes;             // increment this object

            if(minutes >= 60)
            {
                ++hours;
                minutes -= 60;
            }
            return Time(hours, minutes);
        }

        // overloaded postfix ++ operator
        Time operator++( int )
        {
            // save the original value
            Time T(hours, minutes);
            // increment this object
            ++minutes;
            if(minutes >= 60)
            {
                ++hours;
                minutes -= 60;
            }
            // return old original value
            return T;
        }
};
int main()
{
    Time T1(11, 59), T2(10,40);

    ++T1;                  // increment T1
    T1.displayTime();      // display T1
    ++T1;                  // increment T1 again
    T1.displayTime();      // display T1

    T2++;                  // increment T2
    T2.displayTime();        // display T2
    T2++;                    // increment T2 again
    T2.displayTime();        // display T2
    return 0;
}
```

当上面的代码被编译并执行时，会产生以下结果：

```text
H: 12 M:0

H: 12 M:1

H: 10 M:41

H: 10 M:42
```

## 赋值运算符重载

你可以重载赋值运算符（=），就像重载其他运算符一样，它可以像拷贝构造函数一样用来创建对象。

下面的示例解释了如何重载赋值运算符。

```cpp
#include <iostream>
using namespace std;

class Distance
{
   private:
      int feet;              // 0 to infinite
      int inches;            // 0 to 12
   public:
      // required constructors
      Distance(){
         feet = 0;
         inches = 0;
      }
      Distance(int f, int i){
         feet = f;
         inches = i;
      }
      void operator=(const Distance &D )
      {
            feet = D.feet;
            inches = D.inches;
      }
      // method to display distance
      void displayDistance()
      {
            cout << "F: " << feet << " I:" << inches << endl;
      }
};
int main()
{
    Distance D1(11, 10), D2(5, 11);

    cout << "First Distance : ";
    D1.displayDistance();
    cout << "Second Distance :";
    D2.displayDistance();

    // use assignment operator
    D1 = D2;
    cout << "First Distance :";
    D1.displayDistance();

    return 0;
}
```

当上面的代码被编译并执行时，会产生以下结果：

```text
First Distance : F: 11 I:10
Second Distance :F: 5 I:11
First Distance :F: 5 I:11
```

## 函数调用（）运算符重载

```cpp
int arr[SIZE];
public:
    safearray()
    {
        register int i;
        for(i = 0; i < SIZE; i++)
        {
            arr[i] = i;
        }
    }
    int &operator[](int i)
    {
        if( i >= SIZE )
        {
            cout << "Index out of bounds" << endl;
            // return first element.
            return arr[0];
        }
        return arr[i];
    }
};
int main()
{
    safearray A;

    cout << "Value of A[2] : " << A[2] << endl;
    cout << "Value of A[5] : " << A[5]<<endl;
    cout << "Value of A[12] : " << A[12]<<endl;

    return 0;
}
```

当上面的代码被编译并执行时，会产生以下结果：

```text
Value of A[2] : 2
Value of A[5] : 5

Index out of bounds

Value of A[12] : 0
```

## 类成员访问运算符 -> 重载

类成员访问运算符（->）可以被重载，但它有点棘手。它被定义为给类类型一种“指针式”的行为。运算符 -> 必须是成员函数。如果使用，其返回类型必须是指针或可以应用的类的对象。

运算符 -> 通常与指针解引用运算符 * 结合使用来实现“智能指针”。这些指针是像普通指针一样行为的对象，只是当你通过它们访问对象时执行其他任务，例如在指针被销毁时或指针被用来指向另一个对象时自动删除对象。

解引用运算符 -> 可以被定义为一元后缀运算符。也就是说，给定一个类：

```cpp
class Ptr{

    //...

    X * operator->();

};
```

**Ptr** 类的对象可以用非常类似于指针使用的方式来访问 **X** 类的成员。例如：

```cpp
void f(Ptr p )
{

    p->m = 10 ; // (p.operator->())->m = 10

}
```

语句 p->m 被解释为 (p.operator->())->m。使用相同的概念，下面的示例解释了如何重载类访问运算符 ->。

```cpp
#include <iostream>

#include <vector>

using namespace std;


// Consider an actual class.
class Obj {
    static int i, j;
public:
    void f() const { cout << i++ << endl; }
    void g() const { cout << j++ << endl; }
};

// Static member definitions:
int Obj::i = 10;
int Obj::j = 12;

// Implement a container for the above class
class ObjContainer {
    vector<Obj*> a;
public:
    void add(Obj* obj)
    {
        a.push_back(obj);  // call vector's standard method.
    }
    friend class SmartPointer;
};

// implement smart pointer to access member of Obj class.
class SmartPointer {
    ObjContainer oc;
    int index;
public:
    SmartPointer(ObjContainer& objc)
    {
        oc = objc;
        index = 0;
    }

    // Return value indicates end of list:
    bool operator++() // Prefix version
    {
}
```

当上面的代码被编译并执行时，会产生以下结果：

```text
10
12
11
13
12
14
13
15
14
16
15
17
16
18
17
19
18
20
19
21
```

## 26. 多态

单词 **polymorphism** 的意思是具有多种形式。通常，多态发生在存在类层次结构并且它们通过继承相关联时。

C++ 多态意味着对成员函数的调用会根据调用该函数的对象的类型执行不同的函数。

考虑下面的示例，其中基类已被另外两个类派生：

```cpp
#include <iostream>

using namespace std;

class Shape {

    protected:

        int width, height;

    public:

        Shape( int a=0, int b=0)
        {
            width = a;
            height = b;
        }

        int area()
        {
            cout << "Parent class area :" <<endl;
            return 0;
        }
};
class Rectangle: public Shape{
    public:
        Rectangle( int a=0, int b=0):Shape(a, b) { }
        int area ()
        {
            cout << "Rectangle class area :" <<endl;
```
