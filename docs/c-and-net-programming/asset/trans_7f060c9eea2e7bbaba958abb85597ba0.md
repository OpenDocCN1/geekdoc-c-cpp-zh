

## 7. 程序集提供更好的代码管理与维护。

当**使用组件化**时，如果需要更改代码，则需要更改组件代码并编译它。对于较小的更改，无需更改所有代码引用。这节省了大量维护时间。

## 26.1.4 为程序集提供高安全性

可以借助 **文件签名工具 signcode.exe** 为程序集提供安全性。它会将发布者的数字签名附加到程序集。

**可以使用强名称工具和文件签名工具对程序集进行签名。**

当同时使用强名称工具和文件签名工具时，应确保在使用文件签名工具之前使用强名称工具。

## 26.1.5 程序集清单

- 1. 程序集清单包含程序集的元数据。
- 2. 程序集清单包含
  - 程序集的名称和版本信息。
  - 组成程序集的文件（或资源）。
  - 程序集正常运行所需的一组权限。
  - 以及其他一些取决于程序集的详细信息。
- 3. 程序集清单的用途

当公共语言运行时 (CLR) 加载程序集时，它首先读取清单以获取有关程序集的信息。

## 26.1.6 PE 文件（可移植可执行 (PE) 文件）格式

### 概念

可移植可执行 (PE) 格式是一种用于可执行文件、目标代码和 DLL 的文件格式，用于 32 位和 64 位版本的 Windows 操作系统，以便 Windows 加载和执行该文件。

## 26.1.7 多模块程序集

### 概念

- 多模块程序集由多个文件组成（零个或一个 EXE 以及零个或多个 DLL 文件，不过必须至少有一个 EXE 或 DLL）。

### 说明

- 在这种情况下，程序集清单可以位于独立文件中，也可以嵌入到其中一个模块中。当引用程序集时，运行时会加载包含清单的文件，然后根据需要加载所需模块。
- 多模块程序集对实际程序具有优势，特别是当它们由多个开发人员开发或非常大时。
- 生成多模块程序集
- 为了演示多模块程序集的用法，以下示例创建了几个非常简单的模块，这些模块可以合并到单个程序集中。
- 示例：第一个模块是 Facto 类。这个简单的类将允许创建和操作普通分数。

## 示例

```
//The Facto class
#region Using directives

using System;
using System.Collections.Generic;
using System.Text;

#endregion

namespace ProgMModule
{
    public class Facto
    {
        private int no;
        private int ft;

        public Facto(int n, int f)
        {
            this.no = n;
            this.ft = f;
        }

        public int CheckRange( Facto f )
        {
            if (f.ft<5000)
                return 1;
            else
                return 0;
        }
        public override string ToString()
        {
            return numerator + "/" + denominator;
        }
    }
}
```

- 第二个模块是 NumOps 类，用于数字运算。

## 示例

```
//The NumOps class
#region Using directives
using System;
using System.Collections.Generic;
using System.Text;

#endregion
namespace ProgMModule
{
public class NumOps
{
public int Add( int n1, int n2 )
{
return n1 + n2;
}
public int Mult( int n1, int n2 )
{
return n1 * n2;
}
}
}
```

- **创建程序集**
- 请注意，**Facto 和 NumOps 类**位于 **ProgMModule** 命名空间中。该类的完整名称为 ProgMModule.Facto。这足以创建程序集。
- 现在，使用 **AssemblyInfo.cs** 文件向程序集添加一些元数据。可以编写自己的 AssemblyInfo.cs 文件，但最简单的方法是让 Visual Studio 自动生成它。
- Visual Studio 仅创建**单模块程序集**。
- 多模块资源通过 **/addModules** 命令行选项创建。编译和生成多模块程序集的简单方法是使用 makefile，它可以用 **记事本或任何文本编辑器** 创建。
- 以下示例显示了完整的 makefile（紧接着会详细解释）。要**运行此示例，请将 makefile（名称为 makefile）**与 NumOps.cs、Facto.cs 和 AssemblyInfo.cs 的副本放在同一目录中。启动 .NET 命令窗口并 cd 到该目录。不带任何命令开关调用 nmake。可以在 \bin 子目录中找到 MySharedAssembly.dll。

## 示例

```
//Illustration of The complete makefile for a multimodule assembly

ASSEMBLY= MySharedAssembly.dll    // defining the assembly being build

/* defining the directories going to be used, putting the output in a bin directory beneath
   the current directory and retrieving the source code from the current directory*/

BIN=.\bin
SRC=.
DEST=.\bin

CSC=csc /nologo /debug+ /d:DEBUG /d:TRACE

MODULETARGET=/t:module
LIBTARGET=/t:library
EXETARGET=/t:exe

REFERENCES=System.dll

/*The two modules are defined as the two DLLs*/
MODULES=$(DEST)\Facto.dll $(DEST)\NumOps.dll

/* The metadata is defined now.*/
METADATA=$(SRC)\AssemblyInfo.cs

/* Build the assembly */
all: $(DEST)\MySharedAssembly.dll

# Assembly metadata placed in same module as manifest

/* below statement places the assembly (MySharedAssembly.dll) in the destination
   directory (bin). It tells nmake (the program that executes the makefile) that the
   $(DEST)\$(ASSEMBLY) build target depends upon the three other build targets listed,
   and it provides the command line required to build the assembly.*/
/*The compile line builds the library and adds the modules, putting the output into the
   assembly file MySharedAssembly.dll*/

$(DEST)\$(ASSEMBLY): $(METADATA) $(MODULES) $(DEST)
    $(CSC) $(LIBTARGET) /addmodule:$(MODULES: =,) /out:$@ %s

/*Making Module
   nmake should know how to make the modules. Start by telling nmake how to create
   NumOps.dll. NumOps.cs source file is required for this; tell nmake using command line
   to build that DLL*/

# Add NumOps.dll module to this dependency list
$(DEST)\NumOps.dll: NumOps.cs $(DEST)
    $(CSC) $(MODULETARGET) /r:$(REFERENCES: =,) /out:$@ %s

/* same process for Facto.dll*/
# Add Facto
$(DEST)\Facto.dll: Facto.cs $(DEST)
    $(CSC) $(MODULETARGET) /r:$(REFERENCES: =,) /out:$@ %s

$(DEST):
!if !EXISTS($(DEST))
    mkdir $(DEST)
!endif

/*The result of running nmake on this makefile is to create three DLLs: NumOps.dll,
   Facto.dll, and MySharedAssembly.dll. If MySharedAssembly.dll is opened with ILDasm,
   one can see manifest, .*/
```

## 文件版本

生成程序集文件版本属性应在执行生成时自动递增。在生成过程开始时，文件版本的内部版本号部分会在将生成标签应用到源代码管理之前递增。它由 Windows 资源管理器显示，并且 .NET Framework 从不用它进行引用。

## 程序集版本

.NET 在链接程序集时使用程序集版本。当为发布进行代码分支时，程序集版本会手动递增。这应在“共享程序集信息”中指定，以确保解决方案中的所有各种程序集具有相同的程序集版本。CLR 在运行时查找此版本号。

## Web API 版本控制

随着站点规模（就编码而言）增长以及业务需求随时间变化，Web API 版本控制是必需的。由于 Web API 可以同时被多个客户端使用，Web API 的版本控制将必不可少，这样 API 中的业务变更不会影响正在使用/使用现有 API 的客户端。

Web API 版本控制可以通过以下方法完成，

- 1. URI
- 2. QueryString 参数
- 3. 自定义标头参数
- 4. Accept 标头参数

- 1. **使用 URI 的 Web API 版本控制：** 在此方法中，借助路由更改 Web API URI，并且更具可读性。假设存在一个正在运行的现有 API，其中一个 URI 返回某些响应。所有客户端都在使用同一 API，而一个客户端希望通过请求添加新属性来进行某些更改。通过版本控制，可以在不破坏现有 API 流的情况下实现相同目的。在这种情况下，使用 URI 的 Web API 版本控制是实现此目的的最佳方法之一。
- 2. **使用 QueryString 参数的 Web API 版本控制：** 在使用查询字符串的 Web API 版本控制中，会向查询字符串添加一个查询字符串参数，以便查找请求所发送到的控制器或操作。每当请求到达时，DefaultHttpControllerSelector 类的 SelectController() 方法会从 URI 中传递的信息中选择控制器信息。为了通过查询字符串实现版本控制，我们需要创建自定义 DefaultHttpControllerSelector 并重写 SelectController() 方法。

