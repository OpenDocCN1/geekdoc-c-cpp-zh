

### 清单6-1：仅使用原型调用函数

```cpp
#include <iostream>

using namespace std;

void BigDog(int KibblesCount);

int main()
{
    BigDog(3);
    return 0;
}
```

### 清单6-2：从单独的文件中使用函数

```cpp
#include <iostream>

using namespace std;

void BigDog(int KibblesCount)
{
    cout << "I'm a lucky dog" << endl;
    cout << "I have " << KibblesCount << " pieces of food" << endl;
}
```

在清单6-1和6-2中，我们把函数定义与原型分开了。当你将这两个文件编译为一个应用程序时（无论是在Code::Blocks中按F9，还是使用本章前面“其他编译器中的多个源文件”一节中描述的方法），它们会完美地组合在一起。然后你可以运行该应用程序，并看到如下有点有趣的输出：

```text
I'm a lucky dog
I have 3 pieces of food
```

还要注意，我们必须在mystuff.cpp文件的开头放置相同的#include行。这是因为mystuff.cpp使用了cout，而要使用cout，它需要`#include <iostream>`这一行。

![](img/6ba99460b0feb3585671a4612ff5fabb_154_0.png)

## 命名空间快速概述

清单6-1和6-2中的`using namespace std;`行告诉编译器使用一个特定的命名空间std。命名空间是一组类和函数的集合。`std`命名空间（即标准命名空间）包含许多有用的类和函数，例如`string`。如果不包含这条声明，你就需要在使用std中的类或函数时，通过键入`std::<class or function>`来加上前缀。例如，要使用string，你需要键入`std::string`。由于这是一种令人痛苦的编写代码方式，因此你需要添加`using namespace std;`这一行。

## 使用头文件共享

将源代码拆分为多个文件很容易，但很快你可能会遇到一个问题。如果你有一个函数——比如说SafeCracker()——而这个函数非常有用，并且可能会在多个其他源代码文件中被多次调用，那么你需要在每个调用它的文件中为SafeCracker()提供一个原型。该原型可能如下所示：

```cpp
string SafeCracker(int SafeID);
```

但与其在每个使用该函数的文件中都键入这一行，我们知道有一个更简单的方法。（我们计算机人员总是在寻找更简单的方法，这样我们最终就能退休了。）只需将这一行放到自己的文件中，称为头文件，并给该文件一个.h或.hpp扩展名。（使用哪个扩展名由你决定，因为真的无所谓；我们通常用.h。）例如，我们可以将`string SafeCracker(int SafeID);`这一行保存到一个名为`safestuff.h`的文件中。

然后，与其在每个需要该函数的文件开头键入这行头文件行，你只需键入

```cpp
#include "safestuff.h"
```

这样你就有了用于MultipleSourceFiles2示例的三个源代码文件，我们已在清单6-3、6-4和6-5中展示。第一个是main.cpp，它调用函数。第二个是safestuff.h，它包含函数原型。第三个是safestuff.cpp，它包含原型出现在头文件中的函数的实际代码。文件很多，但现在代码被拆分成了易于管理的部分。另外，确保将这三个文件保存在同一目录中。

### 清单6-3：在主文件中包含头文件

```cpp
#include <iostream>
#include "safestuff.h"

using namespace std;

int main()
{
    cout << "Surprise, surprise!" << endl;
    cout << "The combination is (once again)" << endl;
    cout << SafeCracker(12) << endl;
    return 0;
}
```

### 清单6-4：在头文件中包含函数原型

```cpp
using namespace std;

#ifndef SAFESTUFF_H_INCLUDED
#define SAFESTUFF_H_INCLUDED

string SafeCracker(int SafeID);

#endif // SAFESTUFF_H_INCLUDED
```

### 清单6-5：包含实际的函数代码

```cpp
#include <iostream>

using namespace std;

string SafeCracker(int SafeID)
{
    return "11-26-16";
}
```

不过，在编译这个应用程序之前，我们需要给你几点提示。首先，编译器*不会*将头文件编译成单独的`.o`或`.obj`文件。对于清单6-3到6-5中的应用程序，编译器只编译两个文件：`main.cpp`和`safestuff.cpp`。编译器并不会编译头文件，而是在读取`main.cpp`文件并到达头文件的`#include`行时，临时切换去读取该文件，并假装它仍在读取同一个`main.cpp`文件。在继续过程中，它将所有内容都当作`main.cpp`文件的一部分来编译。如果你在其他源代码文件中包含这个头文件，它也会对这些源文件重复同样的操作。

要让这段代码编译通过，请记住以下规则：

- **Makefiles：** 如果你使用的是需要自己处理Makefiles的编译器，不要添加用于编译头文件的规则（头文件通常以`.hpp`或`.h`为扩展名）。只编译源文件（通常以`.cpp`或`.cc`为扩展名）。
- **Visual C++：** 尽管到目前为止我们对Microsoft Visual C++（VC++）谈论得很少，但如果你使用VC++，不要将头文件添加到项目中。只添加源文件。VC++会在一个称为依赖项的树中保留头文件列表，但你不需要自己添加。
- **Code::Blocks：** 还有什么能比这更简单？你只需创建文件，Code::Blocks会为你处理所有文件的关联——无需担心任何事情。头文件和源文件都会显示在项目列表中，Code::Blocks还会处理哪些文件需要被编译的细节。

遵循这些规则后，你就可以编译并运行清单6-3到6-5中的代码了。当你运行该应用程序时，会看到以下输出：

```text
Surprise, surprise!
The combination is (once again)
11-26-16
```

![](img/6ba99460b0feb3585671a4612ff5fabb_157_0.png)

如果你有一个包含某些函数的源文件，创建一个包含相关函数原型的头文件通常是一个好做法。然后你可以将头文件命名为与源文件相同的名称，只是扩展名不同。我们在清单6-4和6-5中就是这么做的：我们将头文件命名为safestuff.h，源文件命名为safestuff.cpp。

![](img/6ba99460b0feb3585671a4612ff5fabb_157_1.png)

有些人喜欢说 include file，而不是 header file（头文件）。我们通常说 header file，因为对我们来说，include 通常是一个动词，说下面这样的话会显得有点别扭：“我们非常确信我们包含了 include file，但如果我们没有包含正确的 include file，你能否把我们包含在你们的会议中；在讨论中，我们一定会包含一些关于如何包含正确的 include file 的问题。然后，你可以包含对我们关于 include file 包含内容的包含问题的回答。”你知道，这话确实很难说出口，所以我们说 header file。

### 只添加一次头文件

Code::Blocks默认会在头文件中包含几行代码。这些行创建一个符号，告诉编译器源文件中是否已经包含过该头文件，这样编译器就不会重复添加它。重复添加头文件是一个错误，因为那样你会为函数定义两次前向引用。以下是你在Code::Blocks中初始创建头文件时看到的内容：

```cpp
#ifndef SAFESTUFF_H_INCLUDED
#define SAFESTUFF_H_INCLUDED

#endif // SAFESTUFF_H_INCLUDED
```

当你在Code::Blocks中输入头文件代码时，要将其输入在`#define SAFESTUFF_H_INCLUDED`行和`#endif // SAFESTUFF_H_INCLUDED`行之间。本章后面的“使用神秘的头文件包装器”一节会详细描述这些自动生成的条目。

### 使用尖括号还是引号

你可能已经注意到清单6-3中的代码有特别之处。当我们包含`safestuff.h`文件时，我们没有像其他`#include`行那样将它放在尖括号内，而是放在引号中：

```cpp
#include "safestuff.h"
```

