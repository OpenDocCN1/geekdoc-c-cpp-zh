
将变量 `arr` 声明为包含 100 个浮点数的数组。如果我们以后需要将数组的类型改为 `double`，只需将 `float` 改为 `double` 即可。变量 `arr` 的声明保持不变；我们不需要修改它们。

由于为现有类型创建了别名，你可能会认为这是多余的。不，事实并非如此。例如，如果你要在数据类型取决于系统的系统上运行，使用别名将非常有帮助。例如，语句：

```cpp
typedef short int size_i;
```

这使得所有 `size_i` 变量的类型都变为 `short int`。在这种情况下，如果变量在另一个平台上必须是 `int`，我们只需要将 `short int` 改为 `int`，它们就会变成 `int`。使用别名有助于我们根据不同的需求方便地调整类型。

另一个常见用途是创建复杂类型的别名，这样我们就不重复它们。例如：

```cpp
typedef int (*pcpy) (const char *s1, const char *s2, int len);
```

`pcpy` 是一个指向函数的别名，该函数返回一个整数，并接受两个 `const char*` 类型参数和一个整数类型参数。要创建该别名，我们编写原型，并在函数的位置填入表达式 `(*pointer_name)`。现在我们可以使用该别名来声明该类型的变量。例如：

```cpp
pcpy p_cpy1, p_cpy2, p_cpy3;
```

如你所见，与传统方法相比，变量类型的读写要容易得多。或者，与其创建一个指向指针的别名（尽管这是最流行的方法），我们不如先创建相应函数的别名，然后声明指针。例如：

```cpp
typedef int (*pfunc)(const char *s1, const char *s2, int len);
pfunc *p_cpy1, p_cpy2, p_cpy3;
```

通常，别名的创建被放在头文件中，以便我们可以在任何源文件中包含它。C++11 提供了另一种使用 `using` 关键字创建别名的方法。例如：

```cpp
using pint = int*;
```

这使得名称 `pint` 成为 `int*` 类型的别名。另一个例子是：

```cpp
using fp = void(*)(int);
```

名称 `fp` 成为指向函数的指针类型，该函数接受一个 `int` 不返回任何内容。使用 `typedef` 的相同声明为：

```cpp
typedef void (*)(int);
```

`using` 语法与 `typedef` 相比更加直观，因为它类似于普通的赋值。此外，`using` 允许我们为模板创建清晰的别名（例如，我们将在第 16 章看到它们），这是 `typedef` 无法实现的。

## 270 C++ 导论

## 函数参数

函数可以接受一个由逗号分隔的参数列表。每个参数前面都有其类型。正如我们稍后看到的，参数本质上是函数的变量，在调用函数时会用一个值进行初始化。

如果函数没有参数，我们使用空括号 `()`。注意，在 C 中，当我们想声明一个函数不接受参数时，我们会在参数内部添加 `void` 单词。在 C 中，空参数表示函数接受未知数量的参数，而不是一个都不接受。在 C++ 中，空参数表示函数不接受参数，我们可以省略 `void`。让我们看一些函数声明示例：

```cpp
void show(); /* 声明一个没有参数且不返回值的函数。 */
double show(char ch, int a, float b); /* 声明一个接受一个 char 参数、一个整数和一个 float 参数并返回 double 值的函数。 */
double *show(int *p1, int *p2); /* 声明一个接受两个整数指针并返回一个 double 指针的函数。 */
```

注意，我们可以省略参数名，只有类型就足够。例如，我们可以写：

```cpp
void show(char, int, float);
```

然而，通常倾向于使用名称，这样阅读原型或意图使用该函数的人就可以了解传递的信息、传递的顺序以及每个参数的目的。例如，一个与点坐标相关的函数，如果声明为如下形式，将让读者更容易理解参数的目的和顺序：

```cpp
void show(int x, int y); 而不是 void show(int, int);
```

每个参数的类型都必须指定，即使几个参数具有相同的类型。例如，写成以下形式是非法的：

```cpp
void test(int a, b, c); 而不是 void test(int a, int b, int c);
```

## 函数定义

函数定义包含了函数的代码。函数定义的通用形式为：

```cpp
return_type function_name(parameter_list)
{
  /* 函数体 */
}
```

函数的定义不允许拆分在不同的文件中。此外，每个函数必须有唯一的定义。如果使用了库函数，则该函数已经定义并编译。例如，参数的名称不需要与函数声明中给出的名称相同。此外，注意在代码末尾（即函数体之后）不添加分号，函数体是两个大括号括内的所有内容。函数体可以是空的。函数体只有在函数被调用时才会执行。如果调用了退出语句（例如 `return`）或执行了最后一条语句，函数的执行将终止。让我们看一个函数的示例：

```cpp
#include <iostream>

void test() {
    std::cout << "Hello World";
}

int main() {
    test();
    return 0;
}
```

```cpp
#include <iostream>

void test() {
    std::cout << "Hello World";
}

int main() {
    test();
    return 0;
}
```

```cpp
#include <iostream>

void test() {
    std::cout << "Hello World";
}

int main() {
    test();
    return 0;
}
```

```cpp
#include <iostream>

void test() {
    std::cout << "Hello World";
}

int main() {
    test();
    return 0;
}
```

```cpp
#include <iostream>

void test() {
    std::cout << "Hello World";
}

int main() {
    test();
    return 0;
}
```
