

## 5.5.2 AJAX 动态字符串对象

### 5.5.2.1 简介

The string object (`AjPStr`) is one of the simplest of all the AJAX objects. AJAX strings have more functions than any other datatype and are used by many other objects. Two features distinguish its use from standard C-type (`char *`) strings. First, AJAX strings are dynamic objects, meaning that memory is dynamically reallocated as needed so that you never run out of space when using the object functions; a string will grow automatically as required.

字符串对象（`AjPStr`）是所有 AJAX 对象中最简单的一种之一。AJAX 字符串的功能比任何其他数据类型都多，并且被许多其他对象使用。有两个特点使其用法与标准 C 类型（`char *`）字符串有所不同。首先，AJAX 字符串是动态对象，这意味着内存会根据需要动态重新分配，因此在使用对象函数时永远不会用完空间；字符串会根据需要自动增长。

Second, AJAX strings are reference counted. This means that the object itself keeps track of how many references (pointers) to the string there are in the code that have been requested by calling library functions. It is not until all references to a string are deleted that the string itself is freed. This ensures that broken references to a string do not occur and that you always have a handle on objects in memory.

其次，AJAX 字符串是引用计数的。这意味着对象本身会跟踪代码中对字符串的引用（指针）数量，这些引用是通过调用库函数请求的。只有当对字符串的所有引用都被删除时，字符串本身才会被释放。这确保了不会出现对字符串的损坏引用，并且你始终可以掌控内存中的对象。

### 5.5.2.2 字符串定义

The string definition is shown below:

字符串定义如下：

```c
typedef struct AjSStr
{
    ajuint Res;
    ajuint Len;
    char *Ptr;
    ajuint Use;
    ajint Padding;
} AjOStr;
#define AjPStr AjOStr*
typedef AjPStr* AjPPStr;
```

A structure is defined called `AjSStr` of four elements (`Len`, `Res`, `Use` and `Ptr`) and with three new datatype names, `AjOStr` for the object itself, `AjPStr` for the object pointer and `AjPPStr` for a pointer to an `AjPStr`.

定义了一个名为 `AjSStr` 的结构体，包含四个元素（`Len`、`Res`、`Use` 和 `Ptr`），以及三个新的数据类型名称：`AjOStr` 表示对象本身，`AjPStr` 表示对象指针，`AjPPStr` 表示指向 `AjPStr` 的指针。

The `Ptr` pointer is just a standard C one which holds a character string and `Len` is its length. In contrast to C-type strings, the character string may or may not be NULL terminated; the library functions for printing `AjPStr` objects use the length field (`Len`) for how many characters to print and won't stop at the first NULL if there is one.

`Ptr` 指针只是一个标准的 C 指针，用于保存字符串，而 `Len` 是其长度。与 C 类型字符串不同，字符串可能以 NULL 结尾，也可能不是；打印 `AjPStr` 对象的库函数使用长度字段（`Len`）来确定打印多少个字符，即使存在 NULL 也不会在第一个 NULL 处停止。

The `Res` element indicates how much reserved dynamic memory is associated with the object. This is always at least equal to `Len` but is often more. `Res` is and should be outside your direct control. If you use a library call to add anything to the string then, if it'll fit within the memory given by `Res` then the operation is performed immediately. If the memory required is larger than `Res` then more memory is allocated and the `Res` item is updated. More memory than required is usually allocated.

`Res` 元素指示与对象关联的保留动态内存量。这始终至少等于 `Len`，但通常更多。`Res` 是且应超出你的直接控制范围。如果你使用库调用向字符串添加任何内容，那么如果它能放入 `Res` 给出的内存中，则操作会立即执行。如果所需内存大于 `Res`，则会分配更多内存并更新 `Res` 项。通常会分配比所需更多的内存。

`Use` is the string usage counter. Sometimes you'll want two or more references to a single string rather than making a genuine copy. EMBOS functions that do this increment the string's usage counter. The usage counter is decremented when a call to destroy either the string itself, or a reference to it, is made. When the usage counter reaches zero the object will be deleted. All of this is function internals, so you don't need to worry about it as long as you don't change the object elements directly. If you intend altering the contents of an object then safety is guaranteed if you use the available library functions.

`Use` 是字符串使用计数器。有时你希望对单个字符串有两个或多个引用，而不是制作真正的副本。执行此操作的 EMBOS 函数会递增字符串的使用计数器。当销毁字符串本身或对其引用的调用发生时，使用计数器会递减。当使用计数器达到零时，对象将被删除。所有这些都是函数内部机制，因此只要你不直接更改对象元素，就不需要担心它。如果你打算修改对象的内容，那么只要使用可用的库函数，安全性就有保障。

Finally, the Padding element indicates the number of characters used to pad the string to its alignment boundary and is used only to keep pedantic compilers happy.

最后，Padding 元素指示用于将字符串填充到其对齐边界的字符数，仅用于让吹毛求疵的编译器满意。

### 5.5.2.3 字符串构造

Code for the default constructor function is shown below:

默认构造函数的代码如下：

```c
/* @func ajStrNew ****************************************************
**
** Default string constructor which allocates memory for a string.
**
** The null string usage pointer is incremented.
**
** @return [AjPStr] Pointer to an empty string
** @@
****************************************************************************/
AjPStr ajStrNew(void)
{
    return ajStrNewRef(strPNULL);
}
```

You can see that the ajStrNew is a wrapper function to ajStrNewRef. It passes to ajStrNewRef an internal string object called strPNULL which is defined in ajstr.c:

你可以看到 ajStrNew 是 ajStrNewRef 的包装函数。它将一个名为 strPNULL 的内部字符串对象传递给 ajStrNewRef，该对象在 ajstr.c 中定义：

```c
#define NULL_USE 1
char charNULL[1] = "";

AjOStr strONULL = { 1, 0, charNULL, NULL_USE, 0 };
AjPStr strPNULL = &strONULL;
```

strPNULL is a global variable for an empty object called the 'AJAX NULL string'. This has a single character of reserved memory, length of zero, a C-type string which is set to NULL, a reference count of 1 and zero padding.

strPNULL 是一个全局变量，用于一个名为“AJAX NULL 字符串”的空对象。它具有一个字符的保留内存，长度为零，一个设置为 NULL 的 C 类型字符串，引用计数为 1 以及零填充。

If you look at ajStrNewRef:

如果你查看 ajStrNewRef：

```c
/* @func ajStrNewRef *****************************************************
**
** String referencing function which returns a pointer to the string passed in
** and increases its reference count.
**
** Not a true string copy, but if modified the new string will behave
** as a copy.
**
** @param [u] refstr [AjPStr] AJAX string object
** @return [AjPStr] Pointer to the string passed as an argument,
**                 with its use count increased by 1.
** @@
*****************************************************************************/
AjPStr ajStrNewRef(AjPStr refstr)
{
    if(!refstr)
        ajFatal("ajStrNewRef source string NULL");

    refstr->Use++;

    return refstr;
}
```

All this function does is increase the reference count of the object that was passed and return the same pointer. It raises a fatal error if NULL was passed.

此函数所做的全部就是增加传递对象的引用计数并返回相同的指针。如果传递了 NULL，它会引发致命错误。

In other words, a call to ajStrNew doesn't immediately instantiate an AjSStr object, it just returns the address of the 'global AJAX NULL string'. It's only when the char * string (Ptr) is given a non-NULL value (by whatever means) that memory for the string object proper will be allocated. AJAX is programmed in this way for maximum speed and efficiency of string handling. You can see this for yourself if you print the reference count of a string which you have just allocated using ajStrNew but not yet used. You might be surprised at the value of the usage count which is higher than you might expect. The reference count may well be in the hundreds owing to the call to embInit in the application code, which itself makes, indirectly, many calls to ajStrNew. If true objects had been allocated for all these strings the code would be less efficient.

换句话说，调用 ajStrNew 不会立即实例化一个 AjSStr 对象，它只是返回“全局 AJAX NULL 字符串”的地址。只有当 char * 字符串（Ptr）被赋予非 NULL 值（通过任何方式）时，才会为字符串对象本身分配内存。AJAX 以这种方式编程，以实现字符串处理的最大速度和效率。你可以自己验证这一点：打印使用 ajStrNew 刚刚分配但尚未使用的字符串的引用计数。你可能会对使用计数的值感到惊讶，它比你预期的要高。引用计数可能高达数百，这是因为应用程序代码中的 embInit 调用本身间接地进行了许多 ajStrNew 调用。如果为所有这些字符串都分配了真正的对象，代码效率会更低。

Things are different if you call the alternative constructor function ajStrNewRes, which allocates memory for a string with an initial reserved size:

如果你调用替代构造函数 ajStrNewRes，情况就不同了，它会为具有初始保留大小的字符串分配内存：

```c
/* @func ajStrNewRes ************************************************************
**
** String constructor which allocates memory for a string of an initial
** reserved size (including a possible null).
**
** @param [r] size [ajuint] Reserved size (including a possible null).
** @return [AjPStr] Pointer to an empty string of specified size.
**
** @@
**********************************************************************************/
AjPStr ajStrNewRes(ajuint size)
{
    AjPStr thys;

    thys = ajStrNewResLenC("", size, 0);

    return thys;
}
```

The function declares an AJAX string object (thys) then calls ajStrNewResLenC to allocate the string, passing to that function the size (size) of the required string:

该函数声明一个 AJAX 字符串对象（thys），然后调用 ajStrNewResLenC 来分配字符串，将所需字符串的大小（size）传递给该函数：

```c
/* @func ajStrNewResLenC ************************************************************
**
** String constructor which allocates memory for a string of a given length
** and of an initial reserved size (including a possible null) and initialises
** it with the text string provided.
**
** @param [r] txt [const char*] Null-terminated character string to initialise
** the new string.
** @param [r] size [ajuint] Reserved size (including a possible null).
** @param [r] len [ajuint] Length of txt to save calculation time.
** @return [AjPStr] Pointer to a string of the specified size
** containing the supplied text.
** @@
********************************************************************************/
AjPStr ajStrNewResLenC(const char* txt, ajuint size, ajuint len)
{
    AjPStr thys;
    ajuint minlen;

    minlen = size;

    if(size <= len)
        minlen = len+1;

    thys = strNew(minlen);
    thys->Len = len;
    if(txt)
        memmove(thys->Ptr, txt, len+1);

    thys->Ptr[len] = '\0';

    return thys;
}
```

This function is an alternative constructor function. It sets a minimum string length (minlen) to the requested reserved size (size), or to the current length (len) plus 1 (for a terminating NULL character) if the requested size is not greater than the current length. It then calls strNew which is a static function in ajstr.c to allocate a string object (this function is shown below). The string length (thys->Len) is set, and the specified text (txt, which is an empty string when called by ajStrNewRes as in this example) is copied (using memmove) to the C-type string pointer (thys->Ptr) in the AJAX string object. A terminating NULL character is added.

这是一个替代构造函数。它将最小字符串长度（minlen）设置为请求的保留大小（size），或者如果请求的大小不大于当前长度，则设置为当前长度（len）加 1（用于终止 NULL 字符）。然后它调用 strNew，这是 ajstr.c 中的一个静态函数，用于分配字符串对象（此函数如下所示）。字符串长度（thys->Len）被设置，指定的文本（txt，在 ajStrNewRes 调用时为空字符串，如本示例所示）被复制（使用 memmove）到 AJAX 字符串对象中的 C 类型字符串指针（thys->Ptr）。添加了一个终止 NULL 字符。

Let's look at the static constructor function which actually allocates the string object:

让我们看看实际分配字符串对象的静态构造函数：

```c
/* @funcstatic strNew ***********************************************************
**
** Internal constructor for modifiable AJAX strings. Used by all the string
** parameterized constructors to allocate the space for the text string.
** The exception is ajStrNew which returns a clone of the null string.
**
** @param [rE] size [ajuint] size of the reserved space, including the
** terminating NULL character. Zero uses a default string size STRSIZE.
** @return [AjPStr] A pointer to an empty string
** @@
********************************************************************************/

static AjPStr strNew(ajuint size)
{
    AjPStr ret;

    if(!size)
        size = STRSIZE;

    AJNEW0(ret);
    ret->Res = size;
    ret->Ptr = AJALLOCO(size);
    ret->Len = 0;
}
```

