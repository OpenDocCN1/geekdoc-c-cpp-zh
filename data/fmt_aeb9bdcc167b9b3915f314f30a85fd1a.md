
## 内置类型

核心数据模型定义在 `PyTypeObject` 中，而函数定义在：

每个源文件在 `Include` 中都有一个对应的头文件。例如，`Objects/rangeobject.c` 对应的头文件是 `Include/rangeobject.h`。

| 源文件 | 类型 |
| :--- | :--- |
| Objects/object.c | 内置方法和基础对象 |
| Objects/boolobject.c | bool 类型 |
| Objects/typeobject.c | byte[] 类型 |
| Objects/bytesobjects.c | bytes 类型 |
| Objects/cellobject.c | cell 类型 |
| Objects/classobject.c | 抽象类类型，用于元编程 |
| Objects/codeobject.c | 内置代码对象类型 |
| Objects/complexobject.c | 复数数值类型 |
| Objects/iterobject.c | 迭代器 |
| Objects/listobject.c | list 类型 |
| Objects/longobject.c | long 数值类型 |
| Objects/memoryobject.c | 基础内存类型 |
| Objects/methodobject.c | 类方法类型 |
| Objects/namespaceobject.c | 模块类型 |
| Objects/moduleobject.c | 命名空间类型 |
| Objects/dictobject.c | 有序字典类型 |
| Objects/rangeobject.c | 范围生成器 |
| Objects/setobject.c | set 类型 |
| Objects/sliceobject.c | 切片引用 |
| Objects/structseq.c | struct.Struct 类型 |
| Objects/tupleobject.c | tuple 类型 |
| Objects/typeobject.c | type 类型 |
| Objects/unicodeobject.c | str 类型 |
| Objects/weakrefobject.c | weakref 类型 |

你将在本章探索这些类型。

## 对象和变量对象类型

由于 C 不像 Python 那样面向对象，C 中的对象并不互相继承。`PyObject` 是每个 Python 对象的初始数据段，`PyObject *` 代表指向它的指针。

在定义 Python 类型时，`typedef` 使用以下两个宏之一：

- `PyObject_HEAD` `PyObject` 用于简单类型
- `PyObject_VAR_HEAD` `PyVarObject` 用于容器类型

简单类型 `PyObject` 具有以下字段：

| 字段 | 类型 | 目的 |
| :--- | :--- | :--- |
| ob_refcount | Py_ssize_t | 实例引用计数 |
| ob_type | _pyobject* | 对象类型 |

例如，`cellobject` 声明了一个额外的字段 `ob_ref`，以及基础字段：

```c
typedef struct {
    PyObject_HEAD
    PyObject *ob_ref; /* cell 的内容，为空时为 NULL */
} PyCellObject;
```

变量类型 `PyVarObject` 扩展了 `PyObject` 类型并具有以下字段：

| 字段 | 类型 | 目的 |
| :--- | :--- | :--- |
| ob_base | PyObject | 基础类型 |
| ob_size | Py_ssize_t | 包含的项数 |

例如，`int` 类型 `PyLongObject` 有如下声明：

```c
struct _longobject {
    PyObject_VAR_HEAD
    digit ob_digit[1];
}; /* PyLongObject */
```

### Type 类型

在 Python 中，对象具有 `ob_type` 属性，你可以使用内置函数 `type()` 获取该属性的值：

```python
>>> t = type("hello")
>>> t
<class 'str'>
```

`type()` 的返回结果是 `PyTypeObject` 实例：

```python
>>> type(t)
<class 'type'>
```

类型对象用于定义抽象基类的实现。

例如，对象始终实现了了 `__repr__()` 方法：

```python
>>> class example:
... x = 1
>>> i = example()
>>> repr(i)
'<__main__.example object at 0x10b418100'
```

`__repr__()` 方法的实现在任何对象的类型定义中始终位于相同的地址。这个位置被称为类型槽（type slot）。

### 类型槽（Type Slots）

所有的类型槽都定义在 `Include/cpython object.h` 中。

每个类型槽都有一个属性名和一个函数签名。例如，`__repr__()` 函数被命名为 `tp_repr`，并具有签名 `reprfunc`：

```c
struct PyTypeObject
---
typedef struct _object {
    typedef char (*reprfunc)(PyObject*);
    reprfunc tp_repr;
    ...
};
```

### 类型字典（Type Dictionaries）

Python 支持使用 `class` 关键字定义新类型。用户定义的类型通过 `type` 模块中的 `type_new()` 创建。用户定义的类型将有一个属性字典，通过 `__dict__()` 访问。当在自定义类上访问属性时，默认的 `__getattr__` 实现会在该字典中查找。类方法、实例方法、类属性和实例属性位于该字典。

`PyObject_GenericGetDict()` 函数实现了获取对象字典的逻辑。`PyObject_GetAttr()` 函数实现了默认的 `__getattr__()` 实现，而 `PyObject_SetAttr()` 实现了 `__setattr__()`。

`bool` 值的 `and` 运算实现首先检查 `a` 和 `b` 是否为布尔值。如果不是，它们会被强制转换为数字，并在两个数字上执行该操作：

`Objects boolobject.c` line 61

```c
static PyObject *a, PyObject *b;
bool_and(PyObject *a, PyObject *b)
{
    if (!PyBool_Check(a) || !PyBool_Check(b))
        return PyLong_Type.tp_as_number->nb_and(a, b);
    return PyBool_FromLong(a == Py_True && (b == Py_True));
}
```

### Long 类型

`long` 类型比 `bool` 复杂得多。在从 Python 2 到 3 的过渡过程中，CPython 放弃了对 `int` 的支持，转而使用 `long` 类型作为主要的整数类型。Python 的 `long` 类型非常特殊，它可以存储变长度的数字。最大长度设置在编译后的二进制文件中。

一个 Python `long` 的数据结构由 `PyObject` 变量头部和一个数字列表组成。数字列表 `ob_digit` 初始化时设置为一个数字，但在初始化后会扩展到更长的长度：

`Include longintrepr.h` line 885

```c
struct _longobject {
    PyObject_VAR_HEAD
    digit ob_digit[1];
};
```

例如，数字 1 将拥有 `ob_digits [1]`，而（某个较大数字）可能会拥有 `ob_digits [2, 4, 6, 0, 1]`。

通过 `_PyLong_New()` 为新的 `long` 分配内存。该函数接收一个固定长度并确保它小于 `MAX_LONG_DIGITS`。

然后它会重新分配 `ob_digit` 的内存以匹配长度。

### Bool 和长整数类型

要将 C `long` 类型转换为 Python `long` 类型，会将 C `long` 转换为数字列表，分配 Python `long` 的内存，并设置每个数字。如果数字小于 10（1 位数字），则初始化 `long` 对象时 `ob_digit` 的长度已为 1。然后在不重新分配内存的情况下设置值：

`Objects ► longobject.c` line 297

```c
PyObject *
PyLong_FromLong(long ival)
{
    PyObject *v;
    unsigned long abs_ival;
    unsigned long t; /* 无符号类型以确保 >> 不会传播符号位 */
    int ndigits = 0;
    int sign;
    CHECK_SMALL_INT(ival);
    /* 单位整数的快速路径 */
    if (!abs_ival >> PyLong_SHIFT) {
        v = _PyLong_New(1);
        if (v) {
            Py_SIZE(v) = sign;
            v->ob_digit[0] = Py_SAFE_DOWNCAST(
                abs_ival, unsigned long, digit);
        }
        return (PyObject*)v;
    }
    /* 较大的数字：循环确定位数 *
    t = abs_ival;
    while (t) {
        ++ndigits;
        t >>= PyLong_SHIFT;
    }
}
```

```c
v = _PyLong_New(ndigits);
if (v != NULL) {
    digit *p = v->ob_digit;
    Py_SIZE(v) = ndigits*sign;
    t = abs_ival;
    while (t) {
        *p++ = Py_SAFE_DOWNCAST(
            t & PyLong_MASK, unsigned long, digit);
            t >>= PyLong_SHIFT;
        }
    }
    return (PyObject*)v;
}
```

要将双精度浮点数转换为 Python `long`，`PyLong_FromDouble()` 会为你完成数学计算。

### 示例

`longobject.c` 中的实现函数包含实用工具，例如通过 `PyLong_FromUnicode` 将字符串转换为数字。

`long` 的富比较槽设置为 `long_richcompare`。该函数封装了 `long_compare`：

`Objects longobject.c` line 303

```c
static long_richcompare(PyObject *self, PyObject *other, int op)
{
    Py_ssize_t result;
    CHECK_BINOP(self, other);
    if (self == other)
        result = 0;
    else
        result = long_compare((PyLongObject*)self, (PyLongObject*)other);
    Py_RETURN_RICHCOMPARE(result, 0, op);
}
```

`long_compare` 函数首先检查变量 `a` 和 `b` 的长度（位数）。如果长度相同，它会遍历每个数字以检查它们是否相等。

`long_compare()` 返回：

- `a < b` 时返回负数
- `a == b` 时返回 0
- `a > b` 时返回正数

例如，当你执行 `1 == 5` 时，结果为 `-4`。`5 == 1` 时，结果为 `4`。

你可以在 `Py_RETURN_RICHCOMPARE` 宏之前实现以下代码块，以便在绝对值小于 1 时返回 True，这里使用了 `Py_ABS()` 宏，它返回有符号整数的绝对值：

```c
if (op == Py_EQ) {
    if (Py_ABS(result) <= 1) {
        return Py_RETURN_RICHCOMPARE(1, 0, op);
    }
}
Py_RETURN_RICHCOMPARE(result, 0, op);
```

## Unicode 字符串类型

XML 和 HTML 都支持带有特殊转义字符 `&#val;` 的 Unicode 点，其中 val 是代码点的十进制值。如果你需要将 Unicode 代码点编码为 XML 或 HTML，可以使用 `.encode()` 方法中的 `xmlcharreplace` 错误处理器：

```python
>>> 'ć'.encode('ascii', 'xmlcharreplace')
b'&#263;'
```

输出将包含 HTML/XML 转义的代码点。所有现代浏览器都将将此转义序列解码为正确的字符。

### ASCII 兼容性

如果你正在处理 ASCII 编码的文本，理解 UTF7/8 和 UTF16 之间的区别至关重要。UTF8 的一个主要优势是与 ASCII 编码的文本兼容。ASCII 编码是一种 7 位编码。

Unicode 标准中的前 128 个代码点表示了 ASCII 标准中现有的 128 个字符。例如，拉丁字母 'a' 是 ASCII 中的第 97 个字符，也是 Unicode 中的第 97 个字符。十进制的 97 等于十六进制的 61，因为该 Unicode 代码点是 U+0061。

在 REPL 中，如果你复制字母 'a' 的二进制代码：

```python
>>> letter_a = b'a'
>>> letter_a.decode('utf8')
'a'
```

这可以被正确解码为 UTF8。

UTF16 处理 2-4 字节的代码点。字母 'a' 的 1 字节表示将无法解码：

```python
>>> letter_a.decode('utf16')
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
```

### Unicode 字符串类型

```
UnicodeDecodeError: 'utf-16-le' codec can't decode byte 0x61 in position 0: truncated
```

在选择编码机制时，这一点非常重要。如果你需要导入 ASCII 编码的数据，UTF8 是一个更安全的选项。

### 宽字符类型

在 CPython 源码中处理未知编码的 Unicode 字符串输入时，将使用 `wchar_t` C 类型。`wchar_t` 是 C 标准中宽字符字符串的标准，足以在内存中存储 Unicode 字符串。在 PEP 393 之后，`wchar_t` 类型被选为 Unicode 存储格式。

Unicode 字符串对象提供了一个实用函数 `PyUnicodeFromWideChar()`，它将将 `wchar_t` 常量转换为字符串对象。例如，`python -c` 使用的 `pymain_run_command()` 将 `-c` 参数转换为 Unicode 字符串：

```c
Modules > main.c line 226
static int pymain_run_command(wchar_t *command, PyCompilerFlags *cf)
{
PyObject *unicode, *bytes;
int ret;
unicode = PyUnicodeFromWideChar(command, -1);
```

### 字节序标记 (BOM)

在解码输入（如文件）时，CPython 可以通过字节序标记（BOM）检测字节序。BOM 是出现在 Unicode 字节流开头的特殊字符。它们告诉接收者数据存储的字节序。不同的计算机可以使用不同的字节序进行编码。如果使用了错误的字节序，即使编码正确，数据也会乱码。

# 大端序将最高有效字节放在前面。小端序将最低有效字节放在前面。

UTF8 规范确实支持 BOM，但它没有影响。UTF8 BOM 可以出现在 UTF 编码数据序列的开头，表示为 `b'\xef\xbb\xbf'`，并将指示 Python 数据流很可能是 UTF8。UTF16 和 UTF32 支持小端和大端序 BOM。

CPython 中的默认字节序由 `sys.byteorder` 设置：

```python
>>> import sys; print(sys.byteorder)
little
```
