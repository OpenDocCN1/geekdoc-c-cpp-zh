

```cpp
box.length = this->length + b.length;
box.breadth = this->breadth + b.breadth;
box.height = this->height + b.height;
return box;
}
private:
double length;      // Length of a box
double breadth;     // Breadth of a box
double height;      // Height of a box
};

// Main function for the program
int main( )
{
    Box Box1;                 // Declare Box1 of type Box
    Box Box2;                 // Declare Box2 of type Box
    Box Box3;                 // Declare Box3 of type Box
    double volume = 0.0;      // Store the volume of a box here

    // box 1 specification
    Box1.setLength(6.0);
    Box1.setBreadth(7.0);
    Box1.setHeight(5.0);

    // box 2 specification
    Box2.setLength(12.0);
    Box2.setBreadth(13.0);
    Box2.setHeight(10.0);

    // volume of box 1
    volume = Box1.getVolume();
    cout << "Volume of Box1 : " << volume << endl;

    // volume of box 2
    volume = Box2.getVolume();
cout << "Volume of Box2 : " << volume <<endl;

// Add two object as follows:
Box3 = Box1 + Box2;

// volume of box 3
volume = Box3.getVolume();
cout << "Volume of Box3 : " << volume <<endl;

return 0;
}
```

当上面的代码被编译并执行时，会产生以下结果：

```
Volume of Box1 : 210

Volume of Box2 : 1560

Volume of Box3 : 5400
```

## 可重载/不可重载的运算符

以下是可重载运算符的列表：

| + | - | * | / | % | ^ |
|---|---|---|---|---|---|
| & | \| | ~ | ! | , | = |
| < | > | <= | >= | ++ | -- |
| << | >> | == | != | && | \|\| |
| += | -= | /= | %= | ^= | &= |
| \|= | *= | <<= | >>= | [] | () |
| -> | ->* | new | new [] | delete | delete [] |

以下是不可重载运算符的列表：

| :: | .* | . | ?: |
|---|---|---|---|

## 运算符重载示例

以下是一些运算符重载示例，帮助您理解这个概念。

| 序号 | 运算符与示例 |
|---|---|
| 1 | 一元运算符重载 |
| 2 | 二元运算符重载 |
| 3 | 关系运算符重载 |
| 4 | 输入/输出运算符重载 |
| 5 | ++ 和 -- 运算符重载 |
| 6 | 赋值运算符重载 |
| 7 | 函数调用 () 运算符重载 |
| 8 | 下标 [] 运算符重载 |
| 9 | 类成员访问运算符 -> 重载 |

## 一元运算符重载

一元运算符作用于单个操作数，以下是一元运算符的示例：

+   - 自增（++）和自减（--）运算符。
+   - 一元负号（-）运算符。
+   - 逻辑非（!）运算符。

一元运算符作用于调用它们的对象，通常，该运算符出现在对象的左侧，如 !obj、-obj、和 ++obj，但有时它们也可以用作后缀，如 obj++ 或 obj--。

下面的示例说明了如何为前缀和后缀用法重载负号（-）运算符。

### C++

```cpp
#include <iostream>
using namespace std;

class Distance
{
    private:
        int feet;          // 0 to infinite
        int inches;        // 0 to 12
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
        // method to display distance
        void displayDistance()
        {
            cout << "F: " << feet << " I:" << inches << endl;
        }
        // overloaded minus (-) operator
        Distance operator- ()
        {
            feet = -feet;
            inches = -inches;
            return Distance(feet, inches);
        }
};
int main()
{
    Distance D1(11, 10), D2(-5, 11);
-D1;                         // apply negation
D1.displayDistance();   // display D1

-D2;                         // apply negation
D2.displayDistance();   // display D2

return 0;
}
```

当上面的代码被编译并执行时，会产生以下结果：

```
F: -11 I:-10

F: 5 I:-11
```

希望上面的示例能让你清楚地理解这个概念，你可以应用类似的概念来重载逻辑非运算符（!）。

## 自增（++）和自减（--）运算符

自增（++）和自减（--）运算符是 C++ 中两个重要的一元运算符。

下面的示例说明了如何为前缀和后缀用法重载自增（++）运算符。类似地，你可以重载运算符（--）。

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
    ++minutes;          // increment this object
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
```

```cpp
class Box
{
    double length;      // Length of a box
    double breadth;     // Breadth of a box
    double height;      // Height of a box
public:

    double getVolume(void)
    {
        return length * breadth * height;
    }

    void setLength( double len )
    {
        length = len;
    }

    void setBreadth( double bre )
    {
        breadth = bre;
    }

    void setHeight( double hei )
    {
        height = hei;
    }

    // Overload + operator to add two Box objects.
    Box operator+(const Box& b)
    {
        Box box;
        box.length = this->length + b.length;
        box.breadth = this->breadth + b.breadth;
        box.height = this->height + b.height;
        return box;
}
};

// Main function for the program
int main( )
{
    Box Box1;              // Declare Box1 of type Box
    Box Box2;              // Declare Box2 of type Box
    Box Box3;              // Declare Box3 of type Box
    double volume = 0.0;   // Store the volume of a box here

    // box 1 specification
    Box1.setLength(6.0);
    Box1.setBreadth(7.0);
    Box1.setHeight(5.0);

    // box 2 specification
    Box2.setLength(12.0);
    Box2.setBreadth(13.0);
    Box2.setHeight(10.0);

    // volume of box 1
    volume = Box1.getVolume();
    cout << "Volume of Box1 : " << volume << endl;

    // volume of box 2
    volume = Box2.getVolume();
    cout << "Volume of Box2 : " << volume << endl;

    // Add two object as follows:
    Box3 = Box1 + Box2;

    // volume of box 3
    volume = Box3.getVolume();
    cout << "Volume of Box3 : " << volume << endl;
}
```

```cpp
void displayDistance()
{
    cout << "F: " << feet << " I: " << inches <<endl;
}

// overloaded minus (-) operator
Distance operator- ()
{
    feet = -feet;
    inches = -inches;
    return Distance(feet, inches);
}

// overloaded < operator
bool operator <(const Distance& d)
{
    if(feet < d.feet)
    {
        return true;
    }
    if(feet == d.feet && inches < d.inches)
    {
        return true;
    }
    return false;
}
};
int main()
{
    Distance D1(11, 10), D2(5, 11);

    if( D1 < D2 )
    {
        cout << "D1 is less than D2 " << endl;
    }
    else
{
    cout << "D2 is less than D1 " << endl;
}
return 0;
}
```

当上面的代码被编译并执行时，会产生以下结果：

```text
D2 is less than D1
```

## 输入/输出运算符重载

C++ 能够使用流提取运算符 >> 和流插入运算符 << 来输入和输出内置数据类型。流插入和流提取运算符也可以被重载，以对用户定义的类型（如对象）执行输入和输出操作。

这里，将运算符重载函数设为类的友元非常重要，因为它将在不创建对象的情况下被调用。

下面的示例说明了提取运算符 >> 和插入运算符 << 的用法。

```cpp
#include <iostream>

using namespace std;

class Distance
{
    private:
        int feet;             // 0 to infinite
        int inches;           // 0 to 12
    public:
        // required constructors
        Distance(){
            feet = 0;
            inches = 0;
        }
        Distance(int f, int i){
            feet = f;
            inches = i;
```

