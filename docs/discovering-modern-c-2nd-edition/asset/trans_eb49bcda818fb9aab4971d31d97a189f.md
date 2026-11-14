

令人惊讶的是，汇编代码（92行）对于此示例来说比预处理后的C++要短得多，因为它只包含实际执行的操作。汇编程序的典型扩展名为`.s`和`.asm`。

编译是构建过程中最复杂的部分，C++的所有语言规则都适用。编译本身由多个阶段组成：前端、中端和后端，而这些阶段又可以包含多个遍。

除了代码生成之外，C++程序的名称还会用类型和命名空间（§3.2.1）信息进行修饰。这种修饰称为*名称修饰*。

## 7.2.1.3 汇编

汇编是从汇编语言到机器语言的简单一对一转换，其中命令被十六进制代码替换，标签被真实（相对）地址替换。生成的文件称为*目标代码*，其扩展名通常是`.o`，在Windows上为`.obj`。目标文件中的实体（代码和变量）称为*符号*。

目标文件可以打包到存档中（扩展名`.a`、`.so`、`.lib`、`.dll`等）。此过程部分仅仅是代码结构化。

## 7.2.1.4 链接

最后，目标文件和存档被*链接*在一起。链接器的主要任务是：

- 匹配不同目标文件的符号，以及
- 将相对于每个目标文件的地址映射到应用程序的地址空间。

- 静态链接：存档完全包含在可执行文件中。这种链接应用于Unix系统上的.a库和Windows上的.lib库。
- 动态链接：链接器仅检查所有符号的存在，并保留对存档的某种引用。这用于.so（Unix）和.dll（Windows）库。

影响显而易见：与动态库链接的可执行文件要小得多，但依赖于执行二进制文件的机器上是否存在这些库。当Unix/Linux上找不到动态库时，可以将其目录添加到环境变量LD_LIBRARY_PATH的搜索路径中。在Windows上，这需要多做一些工作。相反，较大的静态链接可执行文件包含完整代码，并独立于现有库运行。

## 7.2.1.5 完整构建

图7-4说明了如何生成流模拟器的应用程序。首先，我们预处理主应用程序fluxer.cpp，它包含标准库（如<iostream>）以及用于网格划分和求解的领域特定库。然后，展开的源代码被编译为目标文件fluxer.o。最后，应用程序的目标文件与标准库（如libstdc++.so）以及我们之前包含过头文件的领域库进行链接。这些库可以像libsolver.a一样静态链接，也可以像libmesher.so一样动态链接。像系统库这样的常用库通常同时提供这两种形式。

## 7.2.2 构建工具

当我们从程序源代码和已编译的库构建应用程序和库时，可以反复输入大量命令，也可以使用合适的工具。在本节中，我们将介绍其中两种工具：make和CMake。作为案例研究，我们考虑类似于图7-4的场景：一个与网格库和求解器库链接的fluxer应用程序，而这些库又是从相应的源文件和头文件构建的。

### 7.2.2.1 make

```
-> makefile_example/makefile
```

我们不知道你对make有过怎样的了解，但它并不像它的名声那么糟糕。6 实际上，它对小型项目效果相当好。基本思想是，我们表达目标及其源文件之间的依赖关系，当目标比其源文件旧或缺失时，将使用给定命令生成该目标。这些依赖关系写入makefile，并由make自动解析。在我们的示例中，我们需要将fluxer.cpp编译为相应的目标文件fluxer.o：

```
fluxer.o: fluxer.cpp mesher.hpp solver.hpp
    g++ fluxer.cpp -c -o fluxer.o
```

6. 传闻说，作者在度假前将其展示给了同事。当他回来时，已经后悔这种设计，但make已经在整个公司使用，为时已晚，无法收回。

包含命令的行必须以制表符开头。由于所有目标文件的规则足够相似，我们可以为所有C++源文件编写一个通用规则：

![](img/5682e787fc967e93d7e33e8bac5f58a0_630_0.png)

```
.cpp.o:
    ${CXX} ${CXXFLAGS} $^ -c -o $@
```

命令包含自动变量：$@表示规则的目标，$^表示其源文件。变量${CXX}预设为默认C++编译器，${CXXFLAGS}预设为默认标志。我们可以更改这些变量：

![](img/5682e787fc967e93d7e33e8bac5f58a0_630_1.png)

```
CXX=    g++-10
CXXFLAGS= -O3 -DNDEBUG    # Release
# CXXFLAGS= -O0 -g    # Debug
```

在这里，我们更改了编译器并应用了激进优化（用于发布模式）。作为注释，我们还演示了无优化且包含调试工具所需的目标文件符号表的调试模式。接下来，我们需要构建库：

![](img/5682e787fc967e93d7e33e8bac5f58a0_630_2.png)

```
libmesher.a: mesher.o # more mesher sources
    ar cr $@ $^
libsolver.a: solver.o # more solver sources
    ar cr $@ $^
```

为简单起见，我们两者都使用静态链接构建（与图7-4略有偏差）。最后，我们将应用程序和库链接在一起：

点击此处查看代码图像

```
fluxer: fluxer.o libmesher.a libsolver.a
	$(CXX) $(CXXFLAGS) $^ -o $@
```

如果我们在这里使用默认链接器而不是C++编译器，则需要添加C++标准库以及可能特定于C++链接的一些标志。现在，我们可以使用单个命令构建项目：

```
make fluxer
```

这将触发以下命令：

点击此处查看代码图像

```
g++ fluxer.cpp -c -o fluxer.o
	g++ mesher.cpp -c -o mesher.o
	ar cr libmesher.a mesher.o
	g++ solver.cpp -c -o solver.o
	ar cr libsolver.a solver.o
	g++ fluxer.o libmesher.a libsolver.a -o fluxer
```

如果我们更改mesher.cpp，下一次构建过程将仅生成依赖于它的目标：

点击此处查看代码图像

```
g++ mesher.cpp -c -o mesher.o
	ar cr libmesher.a mesher.o
	g++ fluxer.o libmesher.a libsolver.a -o fluxer
```

按照惯例，第一个不以点开头的目标被视为默认目标：

```
all: fluxer
```

因此，我们可以直接运行make。

![](img/5682e787fc967e93d7e33e8bac5f58a0_632_0.png)

图7-4：复杂构建

### 7.2.2.2 CMake

=> CMake_example/CMakeLists.txt

CMake是比make更高抽象级别的工具，我们将在本节中演示。我们的构建项目在名为CMakeLists.txt的文件中指定。它通常以声明所需的最低工具版本和命名项目开始：

点击此处查看代码图像

```
cmake_minimum_required (VERSION 2.6)
project (Fluxer)
```

生成新库非常简单，只需声明其源文件即可：

点击此处查看代码图像

```
add_library(solver solver.cpp)
```

除非我们坚持指定，否则使用哪些命令以及如何参数化由CMake决定。带有动态链接的库也可以同样轻松地生成：

点击此处查看代码图像

```
add_library(mesher SHARED mesher.cpp)
```

我们的最终目标是创建fluxer应用程序，并将其与这两个库链接：

点击此处查看代码图像

```
add_executable(fluxer fluxer.cpp)
target_link_libraries(fluxer solver mesher)
```

在单独的目录中构建项目是良好实践，这样我们可以一次性丢弃所有生成的文件。通常创建一个名为build的子目录，并在其中运行所有命令：

```
cd build
cmake ..
```

CMake可以被视为元构建系统：它并不实际构建项目，而是为另一个构建系统（如make或ninja）生成输入。它还可以为某些IDE（如Eclipse或Visual Studio）生成项目文件。生成过程从搜索编译器和其他工具（包括它们的标志）开始：

点击此处查看代码图像

```
-- The C compiler identification is GNU 4.9.2
-- The CXX compiler identification is GNU 4.9.2
-- Check for working C compiler: /usr/bin/cc
-- Check for working C compiler: /usr/bin/cc -- works
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working CXX compiler: /usr/bin/c++
-- Check for working CXX compiler: /usr/bin/c++ -- works
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Configuring done
```

