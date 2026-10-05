

## 第 2 章 C/C++：库与 Makefile

在更简单的语境下使用伪目标（phony targets）。makevars.mk 的第三部分也是最后一部分列如下所示。

```
21 .PHONY: clean cleanxx
22 clean:
23     rm *.o rm *.exe rm a.*
24 cleanxx:
25     rm *.o rm *.a rm *.so rm *.exe rm *.d
```

带有目标 `.PHONY` 的规则将 `clean` 和 `cleanxx` 定义为前置条件（第 22 行）。这些被视为伪目标。通常情况下，`make` 期望找到与目标同名的文件，并检查文件的最后修改时间来确定目标是否过期。对于伪目标，`make` 不会查找同名文件。伪目标始终被假设为已过期的。

在这个示例中，执行 `make clean` 将删除当前目录（调用 `make` 的目录）中的所有对象文件和可执行文件。执行目标 `cleanxx` 还会删除其他特定的文件。`.d` 文件（见下文）用于捕获 C++ 源文件对头文件的依赖关系，它们会随 `cleanxx` 一起被删除。

### 2.3.6 递归 make 和 .d 文件

我们之前讨论过的，`make` 工具适用于所有源文件都位于单个目录的情况。这种假设对于中等规模的程序失效了。当构建单个可执行文件所需的源文件和对象文件存在多个子目录中时，可能需要递归 make 来完成构建。

递归 make 是一个直观的概念。它包含在伪目标的配方（recipe）中调用 `make`。`linking/linalg` 模块定义了指向 LAPACK LU 分解例程的接口，如前一节所述。这些接口存在于源文件 `lusolve.cpp` 中。源文件 `test_lusolve.cpp` 测试该接口。它使用了如 `utils/utils.cpp` 中定义的 `verify_dir()` 等工具。构建可执行文件 `test_lusolve.exe` 为递归 make 提供了一个简单的示例。

```
1 include ../../makevars.mk
2 CFLAGS := $(CFLAGS) $(MKLINC)
3 LIBS := $(LIBS) $(MKLIBS)
4 ######
5 .PHONY: ../utils obj
```

### 2.3 使用 GNU Make 编译程序

```
6 ../../utils:
7   make --directory=$@ objl
8 #####
9 objl: lusolve.o
10 lusolve.o: lusolve.cpp
11  -include lusolve.d
12 test_lusolve.o: test_lusolve.cpp
13  -include test_lusolve.d
14 #####
15 test_lusolve.exe: test_lusolve.o lusolve.o \
16     ../../utils ../../../utils/utils
```

此 Makefile 被用作三个略有不同的构建的基础：

- 第一个是 `../../utils`，它通过第 5 行启用了递归构建。第一个 `../../utils` 使用 `../../utils` 中的 Makefile 启用了递归构建。另一个伪目标 `objl` 是 Makefile 中的一个目标，用于构建所有可能对外部有用的对象文件和库。事实上，我们通常在 Makefile 中使用 `objl` 作为目标名称，用于构建与 Makefile 处于相同目录下所有可能对外部有用的对象文件和库。

因此，伪目标 `../../utils` 的配方（第 6 行和第 7 行）是

```
make --directory=$@ objl
```

`--directory` 选项意味着派生一个新的 shell 进程

```
../../../utils
```

作为当前目录，并在该目录内调用 `make objl`（`$$` 的含义见表 2.2）。`../utils` 中的 Makefile 将 `objl` 定义为伪目标。它的配方更新了所有可能被从外部使用的对象文件和库，包括 `utils.o`，它将在此 Makefile 中使用。

带有伪目标 `objl` 的规则（第 9 行）更新 `lusolve.o`，它是 `linking/linalg/` 文件夹中唯一可以从外部链接的对象文件。因此，当其他模块递归调用 `linking/linalg` 中的 Makefile 并以 `objl` 为目标时，唯一会被构建的对象文件是 `lusolve.o`。

`make` 的递归调用是第 15 行和第 16 行依赖的结果。可执行文件 `test_lusolve.exe` 使用三个对象文件构建（第 15 行和第 16 行）。其中两个对象文件 `test_lusolve.o` 和 `lusolve.o` 在当前目录中构建。然而，对象文件 `utils.o` 位于 `../utils`。为了正确构建该对象文件，伪目标 `../utils` 被列为前置条件。更新 `../utils` 将导致递归调用 `make`，构建 `utils.o`（第 6 行和第 7 行）。`makevars.mk` 中定义的链接配方过滤掉了伪目标。

第二个讨论是关于 `.d` 文件以及头文件依赖的方式：第 10 行给出 `lusolve.o` 对源文件 `lusolve.cpp` 的依赖。每个对象文件主要依赖一个源文件是典型情况。然而，源文件 `lusolve.cpp` 通常包含多个头文件，这些头文件又包含了其他文件：

```
#include <math>
#include <iostream>
#include <mkl.h>
#include "../utils/utils.hh"
#include "lusolve.hh"
```

然而，命令

```
icpc -O3 -M -c lusolve.cpp
```

显示了所有包含的文件，按数量计算。此命令使用 `icpc` 支持的选项来寻找 MKL 头文件。`-M` 选项告诉编译器给出所有包含文件的列表。如果这些头文件中任何一个被修改，必须重新构建对象文件 `lusolve.o`，尽管 `lusolve.cpp` 未更改。

第 11 行和第 13 行分别负责跟踪 `lusolve.o` 和 `test_lusolve.o` 对头文件的依赖。要理解这些行如何工作，回到 `makevars.mk` 的第 4 行，它在 `CFLAGS` 中包含了 `-MMD` 和 `-MP` 选项。当使用 `-MMD -MP` 调用 `icpc` 时，它会同对象文件一起创建一个 `.d` 文件。`.d` 文件包含了对头文件的依赖。例如，生成的 `lusolve.d` 包含以下内容

```
lusolve.o: lusolve.cpp
```

```
lusolve.o: lusolve.cpp
```

因此，`lusolve.o` 依赖于头文件。

因此，对于伪目标 `../../utils` 的配方是

```
make --directory=$@ objl
```

`--directory` 选项意味着派生了一个新的 shell 进程

```
../../../utils
```

作为当前目录，并在该目录内调用 `make objl`（`$$` 的含义见表 2.2）。`../utils` 中的 Makefile 将 `objl` 定义为伪目标。它的配方更新了所有可能从外部使用的对象文件和库，包括 `utils.o`，它将在此 Makefile 中使用。

带有伪目标 `objl` 的规则（第 9 行）更新 `lusolve.o`，它是 `linking/linalg/` 文件夹中唯一可以从外部链接的对象文件。因此，当其他模块递归调用 `linking/linalg` 中的 Makefile 并以 `objl` 为目标时，唯一会被构建的对象文件是 `lusolve.o`。

`make` 的递归调用是第 15 行和第 16 行依赖的结果。可执行文件 `test_lusolve.exe` 使用三个对象文件构建（第 15 行和第 16 行）。其中两个对象文件 `test_lusolve.o` 和 `lusolve.o` 在当前目录中构建。然而，对象文件 `utils.o` 位于 `../utils`。为了正确构建该对象文件，伪目标 `../utils` 被列为前置条件。更新 `../utils` 将导致递归调用 `make`，构建 `utils.o`（第 6 行和第 7 行）。`makevars.mk` 中定义的链接配方过滤掉了伪目标。

第二个讨论是关于 `.d` 文件以及头文件依赖的方式：第 10 行给出 `lusolve.o` 对源文件 `lusolve.cpp` 的依赖。每个对象文件主要依赖一个源文件是典型情况。然而，源文件 `lusolve.cpp` 通常包含多个头文件，这些头文件又包含了其他文件：

```
#include <math>
#include <iostream>
#include <mkl.h>
#include "../utils/utils.hh"
#include "lusolve.hh"
```

然而，命令

```
icpc -O3 -M -c lusolve.cpp
```

显示了所有包含的文件，按数量计算。此命令使用 `icpc` 支持的选项来寻找 MKL 头文件。`-M` 选项告诉编译器给出所有包含文件的列表。如果这些头文件中任何一个被修改，必须重新构建对象文件 `lusolve.o`，尽管 `lusolve.cpp` 未更改。

第 11 行和第 13 行分别负责跟踪 `lusolve.o` 和 `test_lusolve.o` 对头文件的依赖。要理解这些行如何工作，回到 `makevars.mk` 的第 4 行，它在 `CFLAGS` 中包含了 `-MMD` 和 `-MP` 选项。当使用 `-MMD -MP` 调用 `icpc` 时，它会同对象文件一起创建一个 `.d` 文件。`.d` 文件包含了对头文件的依赖。例如，生成的 `lusolve.d` 包含以下内容

```
lusolve.o: lusolve.cpp
```

```
lusolve.o: lusolve.cpp
```

因此，`lusolve.o` 依赖于头文件。

