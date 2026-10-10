
In this example, we have two namespaces, `NS1` and `NS2`, each with a variable `x`. The variable `x` in `NS2` is defined within the scope of the main function, while the variable `x` in `NS1` is defined outside of any function and is therefore in the global scope.

We use the scope resolution operator `::` to specify the namespace when accessing the variables `x` in `NS1` and `NS2`. Without the scope resolution operator, the local variable `x` in `NS2` would be accessed instead.

### sizeof operator

In C++, the `sizeof` operator is used to determine the size, in bytes, of a data type or an expression. It is often used to allocate memory dynamically or to determine the size of an array.

Here is an example of how the `sizeof` operator can be used:

```
#include <iostream>
#include <array>
int main()
{
std::cout << "sizeof(int) = " << sizeof(int) << " bytes" << std::endl;
std::cout << "sizeof(double) = " << sizeof(double) << " bytes" << std::endl;
std::array<int, 10> arr;
std::cout << "sizeof(arr) = " << sizeof(arr) << " bytes" << std::endl;
int* p = new int[10];
std::cout << "sizeof(p) = " << sizeof(p) << " bytes" << std::endl;
delete [] p;
return 0;
}
```

The output of this program will depend on the machine and compiler being used, but it might look something like this:

```
sizeof(int) = 4 bytes
sizeof(double) = 8 bytes
sizeof(arr) = 40 bytes
sizeof(p) = 8 bytes
```

In this example, we use the `sizeof` operator to determine the size of various data types and expressions. We use it to determine the size of an `int` and a `double`, as well as the size of an `std::array` of `int`s and a dynamically-allocated array of `int`s.

It's important to note that the `sizeof` operator does not evaluate the expression that it is applied to. It simply determines the size of the data type or expression, regardless of its value.

For example:

```
int x = 10;
std::cout << "sizeof(x + 20) = " << sizeof(x + 20) << " bytes" << std::endl;
```

The output of this program would be:
`sizeof(x + 20) = 4 bytes`

In this example, the expression `x + 20` is not evaluated. The `sizeof` operator simply determines the size of an `int`, which is 4 bytes.

### Subscript operator:

In C++, the subscript operator (`[]`) is used to access an element of an array or a container class. It is used to specify the index of the element that is being accessed.

Here is an example of how the subscript operator can be used with an array:

```
#include <iostream>
int main()
{
    int arr[10] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    std::cout << "arr[0] = " << arr[0] << std::endl;
    std::cout << "arr[1] = " << arr[1] << std::endl;
    std::cout << "arr[2] = " << arr[2] << std::endl;
    std::cout << "arr[9] = " << arr[9] << std::endl;
    return 0;
}
```

The output of this program would be:
`arr[0] = 1`
`arr[1] = 2`
`arr[2] = 3`
`arr[9] = 10`

In this example, we have an array of `int`s called `arr`, with 10 elements. We use the subscript operator `[]` to access the elements of the array, specifying the index of the element that we want to access. The first element of the array has an index of 0, the second element has an index of 1, and so on.

The subscript operator can also be used with container classes that provide subscript operator overloads, such as `std::vector` and `std::map`. For example:

```
#include <iostream>
#include <vector>
#include <map>
int main()
{
    std::vector<int> vec = {1, 2, 3, 4, 5};
    std::map<std::string, int> m = {{"one", 1}, {"two", 2}, {"three", 3}};
    std::cout << "vec[0] = " << vec[0] << std::endl;
    std::cout << "vec[1] = " << vec[1] << std::endl;
    std::cout << "m[\"one\"] = " << m["one"] << std::endl;
    std::cout << "m[\"two\"] = " << m["two"] << std::endl;
    return 0;
}
```

The output of this program would be:

`vec[0] = 1`
`vec[1] = 2`
`m["one"] = 1`
`m["two"] = 2`

In this example, we have a `std::vector` of `int`s called `vec` and a `std::map` of `int`s called `m`. We use the subscript operator `[]` to access the elements of the vector and map, specifying the index of the element that we want to access. The indices for a vector are integer values starting from 0, while the indices for a map are keys of the appropriate type (in this case, `std::string`).

It's important to note that the subscript operator can be used to both read from and write to the elements of an array or container. For example:

`arr[0]`

### typeid operator in

在 C++ 中，`typeid` 运算符用于在运行时确定表达式的类型。它返回一个 `std::type_info` 对象，该对象描述表达式的类型。

以下是 `typeid` 运算符用法的示例：

```
#include <iostream>
#include <typeinfo>
int main()
{
    int x = 10;
    double y = 3.14;
    std::string z = "hello";
    std::cout << "typeid(x).name() = " << typeid(x).name() << std::endl;
    std::cout << "typeid(y).name() = " << typeid(y).name() << std::endl;
    std::cout << "typeid(z).name() = " << typeid(z).name() << std::endl;
    return 0;
}
```

此程序的输出取决于实现，但可能看起来像这样：

`typeid(x).name() = i`
`typeid(y).name() = d`
`typeid(z).name() = NSt3__112basic_stringIcNS_11char_traitsIcEENS_9allocatorIcEEEE`

在此示例中，我们有三个变量：`x` 的类型为 `int`，`y` 的类型为 `double`，`z` 的类型为 `std::string`。我们使用 `typeid` 运算符在运行时确定每个变量的类型，并使用返回的 `std::type_info` 对象的 `name` 成员函数获取类型的名称。

需要注意的是，`typeid` 运算符只能与具有已定义类型的表达式一起使用。它不能与具有未定义或不完整类型的表达式一起使用，例如未初始化的变量或具有不完整类类型的变量。

例如：

```
int x;
std::cout << "typeid(x).name() = " << typeid(x).name() << std::endl; // error: x has an undefined type
```

在此示例中，变量 `x` 的类型未定义，因为它未初始化。对 `x` 使用 `typeid` 运算符将导致编译时错误。

### Unary plus and negation operators: + and -

在 C++ 中，一元加法和取反运算符（ `+` 和 `-` ）用于对单个操作数执行算术运算。一元加法运算符返回操作数的值，而一元取反运算符返回操作数值的取反。

以下是这些运算符用法的示例：

```
#include <iostream>
int main()
{
    int x = 10;
    int y = -20;
    std::cout << "+x = " << +x << std::endl;
    std::cout << "-x = " << -x << std::endl;
    std::cout << "+y = " << +y << std::endl;
    std::cout << "-y = " << -y << std::endl;
    return 0;
}
```

此程序的输出将为：

`+x = 10`
`-x = -10`
`+y = -20`
`-y = 20`

在此示例中，我们有两个变量：`x` 和 `y`。`x` 的值为 10，而 `y` 的值为 -20。

我们使用一元加法运算符 `+` 返回 `x` 的值，即 10。我们使用一元取反运算符 `-` 返回 `x` 值的取反，即 -10。

我们使用一元加法运算符 `+` 返回 `y` 的值，即 -20。我们使用一元取反运算符 `-` 返回 `y` 值的取反，即 20。

需要注意的是，一元加法运算符实际上并没有执行任何算术运算，它只是返回操作数的值。它通常用于明确指出一个值为正值，尤其是在该值被其他算术运算符包围时。

例如：

```
int a = 10;
int b = 20;
int c = -30;
```

```
std::cout << a + b - c << std::endl; // output: 40
std::cout << a + +b - c << std::endl; // output: 50
```

在第一个示例中，表达式 `a + b - c` 被计算为 `10 + 20 - (-30)`，结果为 40。

在第二个示例中，表达式 `a + +b - c` 被计算为 `10 + (+20) - (-30)`，结果为 50。一元加法运算符用于明确指出 `b` 的值为正值，即使它已经是正值。

### Expressions

在 C++ 中，表达式是由一个或多个操作数和运算符组合而成，可以求值为单个值的组合。表达式可以很简单，例如常量值或变量，也可以很复杂，涉及多个操作和函数调用。

以下是 C++ 中表达式的一些示例：

```
1 + 2 // simple expression, evaluates to 3
x + y // simple expression, evaluates to the sum of x and y
f(x) // function call expression, evaluates to the return value of the function f
x + y * z // complex expression, evaluates to the sum of x and the product of y and z
```

表达式可以在 C++ 的多种上下文中使用，包括作为赋值语句的右手边、作为函数的参数，或作为更大表达式的一部分。

例如：

```
int x = 1 + 2; // assignment statement, x is assigned the value 3
int y = f(x + 3); // function call, y is assigned the return value of f(x + 3)
if (x > 0 && y < 10) // conditional statement, tests whether x is greater than 0 and y is less than 10
    std::cout << "x is positive and y is less than 10" << std::endl;
```

需要注意的是，表达式可能具有副作用，例如修改变量的值或执行其他操作。例如：

```
int x = 1;
int y = x++; // y is assigned the value of x before x is incremented
std::cout << "x = " << x << " y = " << y << std::endl; // output: x = 2 y = 1
```
