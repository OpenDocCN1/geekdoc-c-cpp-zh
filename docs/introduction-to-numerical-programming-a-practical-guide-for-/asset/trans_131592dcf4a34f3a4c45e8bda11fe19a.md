

## 附录 C：在 C/C++ 中嵌入 Python

在 C/C++ 程序中嵌入 Python 代码这一主题实际上超出了本书的范围，不过下面会简要介绍相关内容，以概述在 C/C++ 程序中创建 Python 图形所依据的核心机制，正如第 3.6 节所述。

从更广泛的角度来看，*混合语言编程*是指使用两种或更多种语言开发程序。这当然可能很有价值，因为它能够结合不同语言的互补优势（易用性、可移植性、运行时性能等），或者让一种语言编写的代码调用另一种语言中已有的代码（库）。不过，这是一项复杂的工作，只有在理由充分时才应采用。

通过插件嵌入 Python 可以扩展 C/C++ 程序的功能，而插件通常更容易开发、调试和使用（例如，参见 Du 2005；Fötch 2012；Python 3.x 2013a,b）。具体来说，嵌入 Python 图形库（例如第 3 章开发的 `graphlib.py` 模块）尤其值得关注，因为它结合了两者的优势：Python 图形的可移植性，以及已编译 C/C++ 代码的高效性。

下面我们将采用循序渐进的方式介绍嵌入 Python 的基本思想。我们将使用清单 C.1 中的 Python 模块 `operations.py`，其中包含两个函数：Sum——返回参数 x 和 y 的和；Average——返回通过向量 x 传入的 n 个值的平均值。第一个函数旨在演示如何处理标量参数，第二个函数则演示如何处理向量参数。

C++ 程序（清单 C.2）的功能仅仅是计算两个值的和，并将这两个值以*元组*的形式传递给 Python 函数 Sum。为此，程序包含头文件 `Python.h`，并定义了几个 `PyObject` 类型的对象：`pModule`——Python 模块对象，`pFunc`——Python 函数引用，`pArgs`——参数元组，`pValue`——返回值。

通过调用函数 `Py_Initialize` 启动 Python 解释器。随后，程序通过调用 `PyImport_Import` 方法导入模块 `operations.py`（模块名转换为 Python Unicode 格式的操作由函数 `PyUnicode_FromString` 完成）。导入模块后，`PyObject_GetAttrString` 方法使用其引用 `pModule` 获取 Python 函数 Sum 的引用 `pFunc`。

```python
def Sum(x, y):                 # returns the sum of x and y
    s = x + y
    return s


def Average(x, n):             # returns the average of x[1] through x[n]
    s = 0e0
    for i in range(1,n+1): s += x[i]
    s /= n
    return s
```

### 清单 C.2 从 C++ 代码中调用带标量参数的 Python 函数（C/C++ 编码）

```cpp
// Calling Python functions with scalar arguments from C++ code
#include <iostream>
#include <Python.h>

int main()
{
    PyObject *pModule, *pFunc, *pArgs, *pValue;  // pointers to Python objects
    double x, y;

    x = 2.0; y = 3.0;                                      // values to be added

    Py_Initialize();                                       // initialize Python
                                                          // import module "operations.py"
    pModule = PyImport_Import(PyUnicode_FromString("operations"));
    if (!pModule) std::cout << "Failed to load <operations.py>";
                                                          // get reference to function Sum
    pFunc = PyObject_GetAttrString(pModule, "Sum");

    pArgs = PyTuple_New(2);                               // define tuple of 2 arguments
    PyTuple_SetItem(pArgs, 0, PyFloat_FromDouble(x));       // set 1st argument
    PyTuple_SetItem(pArgs, 1, PyFloat_FromDouble(y));       // set 2nd argument

    pValue = PyObject_CallObject(pFunc, pArgs);             // call Python function

    std::cout << x << " + " << y << " = " << PyFloat_AsDouble(pValue);

    Py_DECREF(pArgs);                                      // clean up
    Py_DECREF(pFunc);
    Py_DECREF(pModule);

    Py_Finalize();                                         // finish Python
}
```

传递给 Python 函数的参数元组通过 `PyTuple_SetItem` 方法填充。C/C++ 的 `double` 类型转换为 Python 的浮点类型，则通过函数 `PyFloat_FromDouble` 完成。

Python 函数 Sum 的实际调用由 `PyObject_CallObject` 完成，其参数为函数对象 `pFunc` 和参数列表 `pArgs`。返回值 `pValue` 在进一步使用前，需通过调用 `PyFloat_AsDouble` 转换为 `double` 类型。

按照面向对象编程的原则，必须按照创建顺序的逆序释放所有 Python 对象，这通过 `Py_DECREF` 方法完成。最后，调用 `Py_Finalize()` 释放 Python 解释器。

概念相似的程序 C.3 的不同之处在于，被调用函数 Average 的一个参数是向量。为处理这一差异，程序额外创建了一个指向 Python 列表的指针 `px`。列表通过 `PyList_New` 实际分配，其元素则由 `PyList_SetItem` 方法设置。

要在 C/C++ 程序中方便地使用 Python 函数（例如 Sum），需要通过一个包装函数为其提供接口，以隐藏所有通信细节（清单 C.3）。实现这种机制的稳健方法实际上是使用两个 C++ 类，即一个用于封装 Python

### 清单 C.3 从 C++ 代码中调用带向量参数的 Python 函数（C/C++ 编码）

```cpp
// Calling Python functions with vector arguments from C++ code
#include <iostream>
#include <Python.h>

int main()
{
    PyObject *pModule, *pFunc, *pArgs, *pValue;  // pointers to Python objects
    double x[10];
    int i, n;
    PyObject *px;                                  // pointer to Python list

    Py_Initialize();                                // initialize Python
                                                    // import module "operations.py"
    pModule = PyImport_Import(PyUnicode_FromString("operations"));
    if (!pModule) std::cout << "Failed to load operations.py";
                                                    // get reference to function Average
    pFunc = PyObject_GetAttrString(pModule, "Average");

    n = 5;                                          // values to be averaged:
    for (i=1; i<=n; i++) { x[i] = 0.1 * i; }       // x[1] to x[n]
                                                    // prepare Python list
    px = PyList_New(n+1);                            // pointer to list (offset 0 => n+1 components)
    for (i=1; i<=n; i++) {
        PyList_SetItem(px, i, PyFloat_FromDouble(x[i])); // populate list
    }

    pArgs = PyTuple_New(2);                         // define tuple of 2 arguments
    PyTuple_SetItem(pArgs, 0, px);                  // set 1st argument
    PyTuple_SetItem(pArgs, 1, PyLong_FromLong(n));  // set 2nd argument

    pValue = PyObject_CallObject(pFunc, pArgs);     // call Python function

    std::cout << " Average = " << PyFloat_AsDouble(pValue);

    Py_DECREF(pArgs);                               // clean up
    Py_DECREF(pFunc);
    Py_DECREF(pModule);

    Py_Finalize();                                  // finish Python
}
```

解释器本身，以及用于调用 Python 模块中各函数的包装器。相应的实现见清单 C.4。

类 `PyOperations` 的构造函数负责初始化 Python 解释器，而类 `PyOperations` 的构造函数会创建一个 Python 解释器实例并导入 `operations.py` 模块。获取 Python 函数引用、准备并传递参数元组以及获取结果的整套操作，都已移至 C++ 包装函数中，该函数与 Python 函数同名，即 `Sum`。

主程序只需声明一个 `PyOperations` 类型的对象，并调用其 `Sum` 方法来完成求和。

