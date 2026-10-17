
test1: 1.23 and 123

Instantiating the class template as test2 with int and char data types...

test2: 100 and W

就像我们为函数参数指定默认值一样，我们也可以为模板类数据类型指定默认值。程序 12.4 修改了程序 12.3 以演示默认类型指定：

## 程序 12.4 类定义中使用默认数据类型

```
#include <iostream>

using namespace std;

template<class T1=int, class T2=int> //default data types specified as int
class Test
{
    T1 a;
    T2 b;
  public:
    Test(T1 x, T2 y)
    {
        a = x;
        b = y;
    }
    void show()
    {
        cout<<a<<" "<<b<<"\n";
    }

};

int main()
{
    Test <float,int> test1(1,23,123);
    Test <int, char> test2 (100, 'W');
    Test <> test3 ('a', 12.983); //declaration of class object
    without types specification
    test1.show();
    test2.show();
    test3.show();
    return 0;
}
```

程序 12.4 的输出结果为：

1.23 and 123

100 and W

97 and 12

上述程序在未指定任何类型的情况下声明了 `test3` 对象，因此 `T1` 和 `T2` 的默认数据类型被视为 `int`。`test3` 传递的参数值被强制转换为 `int` 并作为输出显示。

### 12.4 函数模板

与类模板类似，我们也可以定义函数模板，用于创建具有不同参数类型的函数族。函数模板的一般格式为：

## 358 面向对象程序设计 C++

```
template<class T>
returntype functionname (arguments of type T)
{
    // Body of function
    // with type T
    // wherever appropriate
    //...
}
```

函数模板语法与类模板相似，只是我们定义的是函数而不是类。我们必须在函数体中以及其参数列表中按需使用模板参数 `T`。

以下示例声明了一个 `swap()` 函数模板，它将交换给定数据类型的值。

```
template<class T>
void swap(T&x, T&y)
{
    T temp = x;
    x = y;
    y = temp;
}
```

这本质上声明了一组重载函数，用于每种数据类型。我们可以像使用普通函数一样调用 `swap()` 函数。例如，我们可以按如下方式应用 `swap()` 函数：

```
void f(int m, int n, float a, float b)
{
    swap(m,n); // swap two integer values
    swap(a,b); // swap two float values
    //....
```

这将为每组参数类型从函数模板生成一个 `swap()` 函数。程序 12.5 显示了如何定义和实现函数模板。

## 程序 12.5 函数模板 - 一个示例

```
#include <iostream>

namespace std;
template <class T>
void swap(T &x, T &y)
{
    T temp = x;
    x = y;
    y = temp;
}
```

```
void fun(int m,int n,float a,float b)
{
    cout << "m and n before swap: " << m << " " << n << "\n";
    swap(m,n);
    cout << "m and n after swap: " << m << " " << n << "\n";

    cout << "a and b before swap: " << a << " " << b << "\n";
    swap(a,b);
    cout << "a and b after swap: " << a << " " << b << "\n";
}

int main()
{
    fun(100,200,11.22,33.44);

    return 0;
}
```

程序 12.5 的输出结果为：

m and n before swap: 100 200

m and n after swap: 200 100

a and b before swap: 11.22 33.439999

a and b after swap: 33.439999 11.22

另一个使用的函数是 `sort()`，用于对各种类型的数组（如 `int` 和 `double`）进行排序。以下示例显示了冒泡排序的模板：

```
template<class T>
bubble(T v[], int n)
{
    for(int i=0;i<n-1; i++)
        for(int j=n-1; j>i; j--)
            if(v[j] < v[j-1])
                T temp = v[j];
                v[j] = v[j-1];
                v[j-1] = temp;
}
```

请注意，交换语句

```
T temp = v[j];
v[j] = v[j-1];
v[j-1] = temp;
```

可以用语句

```
swap(v[j],v[j-1]);
```

替换，其中 `swap()` 已定义为函数模板。

这里是另一个函数返回值的示例。

```
template<class T>
T max(T x, T y)
{
}
```

由函数模板生成的函数称为模板函数。程序 12.6 演示了以嵌套形式使用两个模板函数来实现冒泡排序算法。程序 12.7 显示了应用模板函数的另一个示例。

## 程序 12.6 使用模板函数的冒泡排序

```
#include <iostream>
using namespace std;
template<class T>
void bubble(T arr[], int n)
{
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            swap(arr[j], arr[j+1]); // calls template function
        }
    }
}
template<class X>
void swap(X &a, X &b)
{
    X temp = a;
    a = b;
    b = temp;
}
int main()
{
    int x[5] = {10, 50, 30, 40, 22};
    float y[5] = {1.5, 5.5, 3.3, 4.4, 2.2};
    bubble(x, 5); // calls template function for int values
    bubble(y, 5); // calls template function for float values

    cout << "Sorted x-array: ";
    for (int i=0; i<5; i++) cout << x[i] << " ";
    cout << endl;

    cout << "Sorted y-array: ";
    for (int i=0; i<5; i++) cout << y[i] << " ";
    cout << endl;

    cout << y[i] << " ";
    cout << endl;

    return 0;

}
```

程序 12.6 的输出为：

- Sorted x-array: 10 20 30 40 50

- Sorted y-array: 1.1 2.2 3.3 4.4 5.5

## 程序 12.7 模板函数的应用

```
#include <iostream>
using namespace std;

#define ARR_MAX 5 //Maximum number of elements in an array
template <class T>
T find_min(T ARR[])
{
  int i = 0;
  T MIN=ARR[0];
  for (i=1;i<ARR_MAX;i++)
    if (ARR[i]<MIN)
      MIN=ARR[i];
  return (MIN);
}
int main() {
  int I_MIN;
  float F_MIN;
  char C_MIN;
  //Defining different array types
  int I[5]={20,4,2,38,97};
  float F[5]={-9.9,12.2,3.1,9.9,8.9};
  char C[5]={'A','B','C','D','E'};

//Finding minimum value in each array
  I_MIN=find_min(I);
  F_MIN=find_min(F);
  C_MIN=find_min(C);
  //Printing the results
  cout<<"Minimum value in integer array = "<<I_MIN<<"\n";
  cout<<"\nminimum value in float array = "<<F_MIN<<"\n";
  cout<<"\nminimum value (as ASCII) in character array = "<<C_MIN<<"\n";
  return(0);
}
```

## 面向对象 C++ 编程

程序 12.7 的输出为：

Minimum value in integer array = 2

Minimum value in float array = -9.9

Minimum value (as per ASCII) in character array = A

### 12.5 具有多个参数的函数模板

与类模板一样，我们可以使用逗号分隔的列表在模板语句中使用一个以上的通用数据类型，如下所示：

```
template<class T1, class T2, ...>
returntype functionname(arguments of types T1, T2,...)
{
    (Body of function)
}
```

程序 12.8 说明了在函数模板中使用两种通用类型的概念。

## 程序 12.8 具有两种通用类型的函数

```
#include <iostream>
#include <string>

using namespace std;
template<class T1, class T2>
void display(T1 x, T2 y)
{
    cout << x << " " << y << "\n";
}
int main()
{
    cout<<"Calling function template with int and character string type...\n";
    display(1999, "EBG");
    cout<<"Calling function template with float and integer type parameters...\n";
    display(12.34, 1234);

    return 0;
}
```

程序 12.8 的输出为：

Calling function template with int and character string type parameters...

1999 EBG

Calling function template with float and integer type parameters...

12.34 1234

### 12.6 模板函数的重载

模板函数可以由模板函数或其名称的普通函数重载。在这种情况下，重载解析按如下方式完成：

- 1. 调用具有精确匹配的普通函数。
- 2. 调用可以用精确匹配创建的模板函数。
- 3. 尝试对普通函数的正常重载解析并调用匹配的函数。

如果找不到匹配项，则会生成错误。请注意，不会对模板函数的参数应用自动转换。程序 12.9 显示了模板函数与显式函数重载的方式。

## 程序 12.9 具有显式函数的模板函数

```
#include <iostream>
#include <cstring>

using namespace std;

template <class T>
void display(T x)               //overloaded template function display
{
    cout<<"Overloaded Template Display 1: "<<x<<"\n";
}
template <class T, class T1>
void display(T x, T y)          //overloaded template function display
{
    cout<<"Overloaded Template Display 2: "<<x<<""<<y<<"\n";
}

void display(int x)             //overloaded generic display function
{
    cout<<"Explicit display: "<<x<<"\n";
}
int main()
{
    display(100);
    display(12.34);
    display(100,12.34);
    display('C');

    return 0;
}
```

## 面向对象编程 with C++

程序 12.9 的输出为：

Explicit display: 100

Overloaded Template Display 1: 100

Overloaded Template Display 2: 100, 12.34

Overloaded Template Display 1: C

## 限制

很多时候模板可能会导致能力问题。

注意 调用 `display(100)` 引发的是 `display()` 的普通版本，而不是模板版本。

### 12.7 成员函数模板

当我们为 `vector` 创建类模板时，所有成员函数都被定义为内联，这不是必要的。我们也可以在类外定义它们。记住，模板类的成员函数本身就是由类型参数参数化的，因此这些函数必须由函数模板定义。它采用以下形式：

```
Template<class T>
returntype typename <T> :: functionname(arglist)
{
    // Function body
    //
}
```

`vector` 类模板及其成员函数重新定义如下：

```
// Class template .............
template<class T>
class vector
{
    T* v;
    int size;
public:
    vector(int m);
    vector(const vector& other);
    T operator*(const vector& y);
}
```

```
// Member function templates ....
template<class T>
vector<T> :: vector(int m)
{
    v = new T[size = m];
    for(int i=0; i<size; i++) {
        //
    }
}
```

```
template<class T>
vector<T> :: vector(T* a)
{
    for(int i=0; i<size; i++)
        v[i] = a[i];
}
template<class T>
T vector<T> :: operator*(const vector & y)
{
    T sum = 0;
    for(int i = 0; i < size; i++)
        sum += this->v[i] * y.v[i];
    return sum;
}
```

### 12.8 非类型模板参数

我们已经看到模板可以有多个参数。也可以使用非类型参数。也就是说，除了类型参数 `T` 之外，我们还可以使用其他参数，例如字符串、函数名、常量表达式和内置类型。考虑以下示例：

```
template<class T, int size>
class array
{
    T a[size]; // automatic array initialization
    // ...
    // ...
};
```

此模板将数组的大小作为参数提供。这意味着数组的大小在编译时对编译器已知。创建模板类时必须指定参数。示例：

```
array<int,10> a1; // Array of 10 integers
array<float,5> a2; // Array of 5 floats
array<char,20> a3; // String of size 20
```
