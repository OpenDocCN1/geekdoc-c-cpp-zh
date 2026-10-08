

```cpp
class Vector {
public:
    Vector(int s) :elem{new double[s]}, sz{s} {} // 构建一个 Vector
    double& operator[](int i) { return elem[i]; } // 元素：下标访问
    int size() { return sz; }
private:
    double* elem; // 指向元素的指针
    int sz; // 元素的个数
};

Vector v(6); // 一个包含 6 个元素的 Vector

double read_and_sum(int s)
{
    Vector v(s); // 创建一个包含 s 个元素的 vector
    double sum = 0;
    for (int i=0; i<v.size(); ++i) // 读取到元素
        sum+=v[i]; // 求元素的元素的和
    return sum;
}

enum Color { red, blue, green };
enum class Type { green, yellow, red };

Color col = Color::red;
Type light = Type::red;

Color x = Color::red; // 错误：哪一个 red？
Color y2 = Type::red; // 错误：那个 red 不是一个 Color
Color z3 = Color::red; // OK
auto x4 = Color::red; // OK：Color::red 是一个 Color

int i = Color::red;
Color c = 2; // 错误：Color::red 不是一个 int；初始化错误：2 不是一个 Color

Color x = {5}; // OK，但很冗长
Color y = {6}; // 也是

Type& operator(Type& t) // 前置自增：++
{
    switch (t) {
        case Type::green: return Type::yellow;
        case Type::yellow: return Type::red;
        case Type::red: return Type::green;
    }
}

auto signal = Type::red;
Type next = ++signal; // next 变为 Type::green

Type& operator(Type& t) // 前置自增：++
{
    using enum Type; // 这里，我们使用了 Type
    switch (t) {
        case green: return yellow;
        case yellow: return red;
        case red: return green;
    }
}

enum Color { red, green, blue };
Color col = green;

enum class Type { ptr, num }; // Type 可以持有值 ptr 和 num (§2.4)
struct Entry {
    string name; // string 是标准库的类型
    Type t;
    Node* p; // 如果 t==Type::ptr，使用 p
    int i; // 如果 t==Type::num，使用 i
};

void f(Entry* pe)
{
    if (pe->t == Type::num)
        cout << pe->i;
    // ...
}

struct Entry {
    string name;
    Type t;
    Value v; // 如果 t==Type::ptr，使用 v.p；如果 t==Type::num，使用 v.i
};

void f(Entry* pe)
{
    if (pe->t == Type::num)
        cout << pe->v.i;
    // ...
}

struct Entry {
    string name;
    variant<Node*,int> v;
}

void f(Entry* pe)
{
    if (holds_alternative<int>(pe->v)) // *pe 是否持有一个 int？（见 §15.4.1）
    cout << get<int>(pe->v); // 获取 int
    // ...
}

double sqrt(double); // 平方函数接收一个 double 并返回一个 double

class Vector {
// 使用 Vector 所需
public:
    Vector(int s);
    double& operator[](int i);
    int size();

private:
    double* elem; // elem 指向一个包含 sz 个 double 的数组
    int sz;
};

double sqrt(double d) // sqrt() 的定义
{
    // ... 数学教科中的算法 ...
}

Vector::Vector(int s)
    :elem{new double[s]}, sz{s}
{}
// 构造函数的定义
// 初始化成员

double& Vector::operator[](int i)
{
    return elem[i];
}
// 下标访问的定义

int Vector::size()
{
    return sz;
}
// size() 的定义

// Vector.h:
class Vector {
public:
    Vector(int s);
    double& operator[](int i);
    int size();
private:
    double* elem; // elem 指向一个包含 sz 个 double 的数组
    int sz;
};

// user.cpp:
include "Vector.h" // 获取 Vector 的接口
#include <cmath> // 获取标准库数学函数，包括 sqrt()

double sqrt_sum(const Vector& v)
{
    double sum = 0;
    for (int i=0; i<v.size(); ++i)
        sum+=std::sqrt(v[i]); // 平方根之
    return sum;
}

// Vector.cpp:
include "Vector.h" // 获取 Vector 的接口
Vector::Vector(int s)
    :elem{new double[s]}, sz{s} // 初始化成员
{}

double& Vector::operator[](int i)
{
    return elem[i];
}

int Vector::size()
{
    return sz;
}

export module Vector; // 定义模块 "Vector"
export class Vector {
public:
    Vector(int s);
    double& operator[](int i);
    int size();
private:
    double* elem; // elem 指向一个包含 sz 个 double 的数组
    int sz;
};

