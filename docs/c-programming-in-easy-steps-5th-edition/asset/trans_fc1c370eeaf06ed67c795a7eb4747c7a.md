
- 4. 新建一个程序，使用条件测试查找 `_WIN32` 和 `__linux` 宏，以识别平台

  ```cpp
  #ifdef _WIN32
      #define PLATFORM "Windows"
  #elif defined __linux
      #define PLATFORM "Linux"
  #endif
  ```

- 5. 指定要包含的库类和命名空间

  ```cpp
  #include <iostream>
  using namespace std ;
  ```

- 6. 现在，添加一个 main 函数，其中包含最后的 `return` 语句和一条识别主机平台的语句

  ```cpp
  int main()
  {
      cout << PLATFORM << " System" << endl ;
      return 0 ;
  }
  ```

- 7. 在 main 函数中，插入针对特定平台执行的语句

  ```cpp
  if ( PLATFORM == "Windows" )
      cout << "Performing Windows-only tasks..." << endl ;
  if ( PLATFORM == "Linux" )
      cout << "Performing Linux-only tasks..." << endl ;
  ```

- 8. 保存、编译并运行程序，查看特定于平台的输出

![](img/bf8dbdfb89042fadbaa73b4160c74bac_158_0.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_158_1.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_158_2.png)

预定义的 `_WIN32` 宏有一个下划线，而 `__linux` 宏有两个下划线字符。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_158_3.png)

对预定义宏的条件测试可以扩展为查找其他操作系统的宏，并添加最后的 `#else` 指令来指定 "Unknown" 默认值。

## 包含保护

通常，一个 C++ 程序会有许多 **.h** 头文件和一个包含主程序的 **.cpp** 实现文件。头文件通常可能包含一个或多个 **#include** 指令，以使其他头文件中的其他类或函数可用，并且当定义出现在两个文件中时可能导致重复。例如，当头文件包含另一个含有函数定义的头文件时，编译器会认为该定义出现在每个文件中——因此编译将失败。

解决这种重定义问题的常用方案是使用预处理指令，确保编译器只接触到一个定义。这些被称为“包含保护”，并为每个头文件创建一个唯一的宏名。传统上，名称是文件名的大写版本，并将点改为下划线。例如，文件 **rum.h** 的宏名为 **RUM_H**。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_159_0.png)

包含保护也称为“宏保护”，或简称为“包含守卫”。

在创建用于防止重复的宏时，**#ifndef** 指令首先检查该定义是否已由同一程序中包含的另一个头文件创建。如果定义已存在，编译器会忽略重复定义；否则，**#define** 指令将允许编译器使用该头文件中的定义：

![](img/bf8dbdfb89042fadbaa73b4160c74bac_159_1.png)

add.h

![](img/bf8dbdfb89042fadbaa73b4160c74bac_159_2.png)

triple.h

![](img/bf8dbdfb89042fadbaa73b4160c74bac_159_3.png)

guard.cpp

- 1. 创建一个名为 "add.h" 的头文件，其中包含 "add" 函数的内联声明

  ```cpp
  inline int add ( int x, int y ) { return ( x + y ) ; }
  ```

- 2. 现在，创建一个名为 "triple.h" 的头文件，其中包含一条预处理指令，使 add 函数可用于 "triple" 函数的内联声明

  ```cpp
  #include "add.h"

  inline int triple ( int x ) { return add( x, add( x, x ) ) ; }
  ```

- 3. 新建一个程序，使用预处理指令使 add 和 triple 函数都可用

  ```cpp
  #include "add.h"
  #include "triple.h"
  ```

- 4. 指定要包含的库类和命名空间

  ```cpp
  #include <iostream>
  using namespace std ;
  ```

- 5. 添加一个 main 函数，其中包含调用所包含头文件中 **add()** 和 **triple()** 函数的语句

  ```cpp
  int main()
  {
      cout << "9 + 3 = " << add(9, 3) << endl ;
      cout << "9 x 3 = " << triple(9) << endl ;
      return 0 ;
  }
  ```

- 6. 保存文件，然后尝试编译程序，会看到编译失败，因为 add 函数似乎被定义了两次——一次在 "add.h" 中，一次通过 "triple.h" 的包含引入

![](img/bf8dbdfb89042fadbaa73b4160c74bac_160_0.png)

- 7. 编辑头文件 "add.h"，将内联函数声明包含在预处理包含保护中

  ```cpp
  #ifndef ADD_H
  #define ADD_H

  inline int add ( int x, int y ) { return ( x + y ) ; }

  #endif
  ```

- 8. 保存修改后的文件，然后编译并运行程序——现在编译成功，因为包含保护防止了 add 函数看似重定义

![](img/bf8dbdfb89042fadbaa73b4160c74bac_160_1.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_160_2.png)

使用常规命名方案，使宏名类似于文件名，以避免冲突。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_160_3.png)

所有头文件都应包含头文件保护——向 triple.h 文件添加 **TRIPLE_H** 宏。

## 使用宏函数

**#define** 指令可用于创建宏函数，这些宏函数将在编译前在源代码中被替换。

预处理函数声明由宏名组成，宏名后紧跟包含函数参数的括号——重要的是不要在名称和括号之间留任何空格。声明之后是另一组括号中的函数定义。例如，一个将参数减半的预处理宏函数如下所示：

```cpp
#define HALF(n) (n / 2)
```

使用宏函数时应小心，因为与常规 C++ 函数不同，它们不执行任何类型的类型检查——因此很容易创建导致错误的宏。因此，内联函数通常比宏函数更可取，但由于宏直接替换其代码，它们避免了函数调用的开销——因此程序运行得更快。由此产生的差异可以在编译过程中创建的第一个临时文件中看到：

![](img/bf8dbdfb89042fadbaa73b4160c74bac_161_0.png)

- 1. 通过定义两个宏函数来操作单个参数，开始一个新程序

  ```cpp
  #define SQUARE(n) (n * n)
  #define CUBE(n) (n * n * n)
  ```

- 2. 在宏函数定义之后，指定要包含的库类和要使用的命名空间前缀

  ```cpp
  #include <iostream>
  using namespace std;
  ```

- 3. 接下来，声明两个内联函数来操作单个参数——就像上面定义的宏函数一样

  ```cpp
  inline int square(int n) { return (n * n); }
  inline int cube(int n) { return (n * n * n); }
  ```

- 4. 添加一个包含最后 return 语句的 main 函数

  ```cpp
  int main()
  {
      // Program code goes here.
      return 0;
  }
  ```

- 5. 在 main 函数块的开头，声明并初始化一个整数变量

  ```cpp
  int num = 5;
  ```

- 6. 现在，插入语句以调用每个宏函数和每个可比较的内联函数

  ```cpp
  cout << "Macro SQUARE: " << SQUARE(num) << endl;
  cout << "Inline square: " << square(num) << endl;
  cout << "Macro CUBE: " << CUBE(num) << endl;
  cout << "Inline cube: " << cube(num) << endl;
  ```

- 7. 保存文件，然后编译程序并保存临时文件，再运行程序

  ```bash
  c++ macro.cpp -save-temps -o macro.exe
  ```

## 构建字符串

预处理器的 # 运算符被称为“字符串化”运算符，因为它将作为宏参数传入的一系列字符转换为字符串——并添加双引号将字符串括起来。

作为宏参数传递给字符串化运算符的字符序列前后的所有空白都会被忽略，字符之间的多个空格会缩减为仅一个空格。

字符串化运算符可用于将字符串值传递给预处理器 #define 指令，而无需用双引号括住每个字符串。

宏定义可以使用 ## 合并运算符将两个项合并为一个项。当合并后的项是变量名时，其值不会被宏展开——它只是允许该变量名被宏替换。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_163_0.png)

strung.cpp

- 1. 通过定义一个宏来开始一个新程序，该宏从作为其参数传入的一系列字符创建字符串，以替换到输出语句中

  ```cpp
  #define LINEOUT( str ) cout << #str << endl
  ```

- 2. 定义第二个宏，将作为其参数传入的两个项合并为变量名，以替换到输出语句中

  ```cpp
  #define GLUEOUT( a, b ) cout << a##b << endl
  ```

- 3. 在宏定义之后，指定要包含的库类和要使用的命名空间前缀

  ```cpp
  #include <string>
  #include <iostream>
  using namespace std ;
  ```

- 4. 添加一个包含最后 return 语句的 main 函数

  ```cpp
  int main()
  {
      // Program code goes here.
      return 0 ;
  }
  ```

- 5. 在 main 函数块的开头，声明并初始化一个字符串变量，然后追加另一个字符串

  ```cpp
  string longerline = "They carried a net " ;
  longerline += "and their hearts were set" ;
  ```

- 6. 现在，添加使用宏输出文本的语句

  ```cpp
  LINEOUT(In a bowl to sea went wise men three) ;
  LINEOUT(On a brilliant night in June) ;
  GLUEOUT( longer, line ) ;
  LINEOUT(On fishing up the moon.) ;
  ```

- 7. 保存文件，然后编译程序并保存临时文件，再运行程序

  ```bash
  c++ strung.cpp -save-temps -o strung.exe
  ```

![](img/bf8dbdfb89042fadbaa73b4160c74bac_163_1.png)

- 8. 在纯文本编辑器（如记事本）中打开临时 ".ii" 文件，以查看该字符串

