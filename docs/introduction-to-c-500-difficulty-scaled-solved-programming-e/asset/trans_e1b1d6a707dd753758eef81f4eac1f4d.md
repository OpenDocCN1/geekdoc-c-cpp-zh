

# 586 C++ 导论

```cpp
cin >> s1 >> s2;
i = (s1 > s2);
if(i == 1)
    s1.show();
else if(i == 2)
    s2.show();
else
    cout << "\n通过的课程数量\n";
return 0;
```

**C.18.6** 定义一个 *Triangle*（三角形）类，包含三个整数以及一个 `!=` 运算符，这些整数对应三角形的边（例如 a、b 和 c）。重载 `!=` 运算符，以便我们可以比较两个三角形的周长（例如，编写语句 `t1!= t2;` 来比较 t1 和 t2 的周长）。还要重载 `[]` 运算符，以便将新值赋值给三角形的边（例如，语句 `t1[0] = 3;` 应该让 t1 的边 a 等于 3，而语句 `t1[1] = 5;` 应该让 t1 的边 b 等于 5）。在类中添加适当的函数。编写一个程序来测试 Triangle 类的功能。

```cpp
#include <iostream>
#include <cstdlib>
using std::cout;
class Triangle {
private:
    int a;
    int b;
    int c;
public:
    Triangle(int dim1, int dim2, int dim3);
    bool operator!=(const Triangle& t) const;
    int& operator[](int dim);
    void show() const;
};
Triangle::Triangle(int dim1, int dim2, int dim3) {
    a = dim1;
    b = dim2;
    c = dim3;
}
bool Triangle::operator!=(const Triangle& t) const {
    if(a+b+c != t.a+t.b+t.c)
        return true;
    else
        return false;
}
int& Triangle::operator[](int dim) {
    if(dim == 0)
        return a;
}
```

```cpp
else if(dim == 1)
    return b;
else if(dim == 2)
    return c;
else
{
    cout << "Error: 错误的索引\n";
    exit(EXIT_FAILURE); // 终止程序。
}

void Triangle::show() const
{
    cout << a << ' ' << b << ' ' << c << '\n';
}

int main()
{
    Triangle t1(1, 2, 3), t2(4, 1, 1);
    if(t1 != t2) // if(t1.operator!=(t2))
        cout << "周长不同\n";
    else
        cout << "周长相同\n";

    t1[0] = 4; // t1.operator(0);
    t1[1] = 5;
    t1[2] = 6;
    t1.show();
    return 0;
}
```

注释：关于类的设计，我将三角形的边声明为私有成员。将它们设为公共并不是错误的，但使用类的主要目的是隐藏数据，将敏感信息声明为私有是一种良好的做法。为了与类通信，我声明了公共函数 `show()`。为了初始化成员，我声明了一个构造函数。或者，我可以声明一个公共函数 `set()` 并在对象创建后调用它进行初始化。由于前面关于构造函数的理由，我更倾向于使用构造函数。没有必要定义析构函数，默认的即可。`operator[]` 函数的工作方式与类 C18.5 一。例如，语句 `t1[0] = 4;` 调用了 `operator()`，它返回 `a` 的引用。因此，`a` 变成了 4。注意，如果返回类型是 `int`，编译器将显示错误信息，说明赋值中的左操作不是左值。

C18.7 完成模板函数 `sum()` 的声明和定义，以返回包含整数的 vector 元素的和，以及包含对象的 vector 的和。在 `Product` 类中添加适当的函数，以便以下程序运行。

```cpp
template <typename T>
T sum(const vector<T>& v) // 找到原型
{
    T t;
    for(int i = 0; i < v.size(); i++) /* v 可能包含类型为 Product 的整数元素。 */
        t = t + v[i]; // 计算和。
    return t;
}

...
```

```cpp
class Product
{
    int code;
    float prc;
    ...
};
```

```cpp
int main()
{
    vector<int> v_i = {1, 2, 3};
    vector<Product> v_p = {Product(100, 5), Product(200, 10), Product(15), Product(400, 20)};

    int i = sum(v_i); /* sum() 应该返回 v_i 元素的和，
    即为 6； */
    cout << i << '\n'; // 程序输出 6。
    Product p = sum(v_p); /* p.prc 的值应该等于 v_p 元素中
    p.prc 成员的和，即为 50。 */
    cout << p.prc << '\n'; // 程序输出 50。
    return 0;
}
```

答案：

```cpp
#include <iostream>
#include <vector>
using namespace std;

template <typename T>
T sum(const vector<T>& v)
{
    T t = {}; /* 分配初始值。例如，如果 t 的类型
    是 int，t 将变为 0。如果类型是 Product，构造函数将
    初始化 t 的成员为 0。无论何种情况，为了计算和，
    0 这个初始值都是必要的。 */
    for (int i = 0; i < v.size(); i++)
        t = t + v[i];
    return t;
}

class Product
{
    private:
    int code;
    float prc;
public:
    Product(int c = 0, float p = 0);
    Product& operator=(const Product& p);
    Product& operator+(const Product& p);
};

Product::Product(int c, float p) {
    code = c;
    prc = p;
}

Product& Product::operator+(const Product& p) {
    prc += p.prc;
    return *this;
}
```

**C.18.8** 考虑以下 Product 和 Employee 类：

```cpp
class Product {
    private:
    int code;
    float prc; // 价格。
public:
    ...
}

class Employee {
    private:
    string name;
    float sal; // 工资。
public:
    ...
}
```

定义模板函数 `sort()`，其参数为 vector 对象（例如 v），它包含 Product 或 Employee 元素并排序。如果是 Product 元素，应按价格排序；如果是 Employee 元素，应按字母顺序排序。每个类应包含一个内联构造函数、一个名为 `show()` 的内联函数来显示成员，以及一个必要的比较元素的函数。编写一个程序声明 Product 和 Employee 的 vector 对象，调用 `sort()` 并显示它们的元素。

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>
using std::cout;
using std::string;
using std::vector;

template <typename T>
void sort(vector<T>& v);

class Product
{
    private:
    int code;
    float prc;
public:
    Product(int c = 0, float p = 0) : code = c, prc = p {}
    bool operator>(const Product& p) const;
    void show() const {cout << "C:" << code << " P:" << prc << '\n'; }
};

bool Product::operator>(const Product& p) const
{
    return prc > p.prc;
}

class Employee
{
    private:
    string name;
    float sal;
public:
    Employee(const string& n = "", float s = 0) : name = n, sal = s {}
    bool operator>(const Employee& e) const;
    void show() const {cout << "N:" << name << "S:" << sal << '\n'; }
};

bool Employee::operator>(const Employee& e) const
{
    return name > e.name;
}

template <typename T>
void sort(vector<T>& v)
{
    for (int i = 0; i < v.size(); i++) {
        for (int j = i + 1; j < v.size(); j++) {
            if (v[j] > v[i]) {
                std::swap(v[i], v[j]);
            }
        }
    }
}

int main()
{
    vector<Product> v_prd = {Product(10, 3.5), Product(20, 2.5), Product(30, 2.5)};
    vector<Employee> v_emp = {Employee("Mike", 100), Employee("John", 200), Employee("Nick", 300)};

    sort(v_prd);
    sort(v_emp);
    for (int i = 0; i < v_prd.size(); i++) v_prd[i].show();
    for (int i = 0; i < v_emp.size(); i++) v_emp[i].show();
    return 0;
}
```

