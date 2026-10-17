
`void *aligned_alloc(size_t alignment, size_t size);`

### 描述

`aligned_alloc` 函数分配对齐由 `alignment` 指定、大小由 `size` 指定且表示不定的空间。如果 `alignment` 值不是实现支持的对齐方式，应失败并返回空指针。

### 返回

`aligned_alloc` 返回空指针或指向分配空间的指针。

## 72.4.4.3 calloc 函数

### 摘要

```
#include <stdlib.h>

void *calloc(size_t nmemb, size_t size);
```

### 描述

`calloc` 函数为 `nmemb` 个大小为 `size` 的对象数组分配空间。空间初始化为全零。

### 返回

`calloc` 返回指向分配空间的指针，或者在无法分配空间或 `nmemb * size` 溢出 `size_t` 值时返回空指针。

## 72.4.4.4 free 函数

### 摘要

```
#include <stdlib.h>

void free(void *ptr);
```

### 描述

`free` 函数导致 `ptr` 指向的空间被释放，即变为可分配。如果 `ptr` 是空指针，则不发生任何操作。否则，如果参数不匹配早期内存管理函数返回的指针，或者该空间已通过 `free` 或 `realloc` 释放，则行为是未定义的。

### 返回

`free` 返回空。

## 72.4.4.5 free_sized 函数

### 摘要

```
#include <stdlib.h>

void free_sized(void *ptr, size_t size);
```

### 描述

如果 `ptr` 是空指针或从 `malloc`、`realloc` 或 `calloc` 获得的结果，且 `size` 等于请求的分配大小，则此函数等同于 `free(ptr)`。否则，行为是未定义的。`aligned_alloc` 的结果可能传递给 `free_sized`。
注意：符合标准的实现可以忽略 `size` 并调用 `free`。

# ISO/IEC 9899:2024(en)

# 推荐实践

实现可以提供扩展以查询分配的可用大小，或确定如果对其他大小的分配请求成功，将产生什么可用分配大小。此类实现应允许将得到的可用大小作为 `size` 参数传递，并在这种情况下提供等于 `free` 的功能。

# 返回值

`free_aligned_sized` 函数不返回任何值。

## 7.24.4.6 The free_aligned_sized 函数

# 概要

```
#include <stdlib.h>

void free_aligned_sized(void *ptr, size_t alignment, size_t size);
```

# 描述

如果 `ptr` 是空指针，或者是从调用 `aligned_alloc` 获得的结果（其中 `alignment` 等于请求的分配大小且 `size` 等于请求的分配大小），则这等同于 `free(ptr)`。否则，其行为是未定义的。`malloc` 或 `realloc` 的结果可能被传递给 `free_aligned_sized`。

符合标准的实现可以忽略 `alignment` 和 `size` 并调用 `free`。

# 推荐实践

实现可以提供扩展以查询分配的可用大小，或确定如果对其他大小的分配请求成功，将产生什么可用分配大小。此类实现应允许将得到的可用大小作为 `size` 参数传递，并在这种情况下提供等于 `free` 的功能。

# 返回值

`free_aligned_sized` 函数不返回任何值。

## 7.24.4.7 The malloc 函数

# 概要

```
#include <stdlib.h>

void *malloc(size_t size);
```

# 描述

`malloc` 函数为对象分配空间，该对象的大小由 `size` 指定，其表示是不确定的。

# 返回值

`malloc` 函数返回空指针或指向分配内存的指针。

## 7.24.4.8 The realloc 函数

# 概要

```
#include <stdlib.h>

void *realloc(void *ptr, size_t size);
```

# 描述

`realloc` 函数释放 `ptr` 指向的对象，并返回指向新对象的指针，该对象的大小由 `size` 指定。新对象的内容将与释放前的对象的内容相同，直到新旧大小的较小者为止。新对象中超出旧对象大小的任何字节具有未指定的值。

如果 `ptr` 是空指针，`realloc` 函数的行为类似于对指定大小执行 `malloc` 函数。

否则，如果 `ptr` 不匹配内存管理函数返回的指针，或者该空间已通过调用 `free` 或 `realloc` 函数被释放，或者 `size` 为零，则其行为是未定义的。不分配新对象的内存，旧对象不被分配且其值不变。

# 返回值

`realloc` 函数返回指向新对象的指针（该值可以与指向旧对象的指针值相同），或者在未分配到新对象时返回空指针。

## 7.24.5 与环境的通信

### 7.24.5.1 The abort 函数

# 概要

```
#include <stdlib.h>

[[noreturn]] void abort(void);
```

# 描述

`abort` 函数导致程序异常终止，除非信号 `SIGABRT` 被捕获且同一个处理程序没有返回。带有无缓冲数据的打开流将被刷新，打开的流将被关闭，或临时文件被删除取决于实现定义。函数通过调用 `raise(SIGABRT)` 向主环境返回一个由实现的未终止状态。

# 返回值

`abort` 函数不返回给其调用者。

### 7.24.5.2 The atexit 函数

# 概要

```
#include <stdlib.h>

int atexit (*func)(void);
```

# 描述

`atexit` 函数注册由 `func` 指向的函数，该函数将在程序正常结束时不带参数地被调用。在 `atexit` 函数被调用之前，是否发生对 `atexit` 函数的调用是未确定的。

# 环境限制

实现应支持至少注册 32 个函数。

# 返回值

`atexit` 函数在注册成功时返回零，失败时返回非零。

前向引用：`at_quick_exit` 函数 (`7.24.5.3`)，`exit` 函数 (`7.24.5.4`)。

## 7.24.5.3 The at_quick_exit 函数

# 概要

```
#include <stdlib.h>

int at_quick_exit (*func)(void);
```

# 描述

`at_quick_exit` 函数注册由 `func` 指向的函数，在应该被调用时不带参数地调用。在 `quick_exit` 函数被调用之前，对 `at_quick_exit` 函数的调用是否成功是未确定的。

> ³45 `atexit` 函数注册不同于 `at_quick_exit` 注册，因此应用程序可能需要使用相同的参数调用这两个注册函数。

> ³46 `at_quick_exit` 注册不同于 `atexit` 注册，因此应用程序可能需要使用相同的参数调用这两个注册函数。

# 环境限制

实现应支持至少注册 32 个函数。

# 返回值

`at_quick_exit` 函数在注册成功时返回零，失败时返回非零。

前向引用：`quick_exit` 函数 (`7.24.5.7`)。

## 7.24.5.4 The exit 函数

# 概要

```
#include <stdlib.h>

[[noreturn]] void exit(int status);
```

# 描述

`exit` 函数导致程序终止。如果程序多次调用 `exit` 函数，或者在调用 `exit` 函数的同时调用了 `quick_exit` 函数，则其行为是未定义的。

首先，所有通过 `atexit` 函数注册的函数按注册的反序被调用。接下来，带有无缓冲数据的流将被刷新，打开的流将被关闭，临时文件被删除取决于实现。最后，控制返回主环境。如果 `status` 的值为 `EXIT_SUCCESS`，则返回一个实现的定义的状态。如果 `status` 的值为 `EXIT_FAILURE`，则返回一个实现的定义的状态。

`exit` 函数不能返回。

## 7.24.5.5 The _Exit 函数

# 概要

```
#include <stdlib.h>

[[noreturn]] void _Exit(int status);
```

# 描述

`_Exit` 函数导致程序终止并将控制返回主环境。带有无缓冲数据的流将被刷新，打开的流将被关闭，或临时文件被删除取决于实现。

# 返回值

`_Exit` 函数不返回给其调用者。

## 7.24.5.6 The getenv 函数

# 概要

```
#include <stdlib.h>

char *getenv(const char *name);
```

# 描述

`getenv` 函数在主环境提供的环境变量列表中搜索与 `name` 指向字符串匹配的字符串。更改环境列表的方法取决于实现。`getenv` 函数不避免与修改环境列表的其他线程产生数据竞争。

# 返回值

`getenv` 函数返回指向匹配列表字符串的指针。指向的字符串不应被程序修改，但可以被随后的 `getenv` 调用覆盖。如果找不到指定的名称，则返回空指针。

## 7.24.5.7 The quick_exit 函数

# 概要

```
#include <stdlib.h>

noreturn void quick_exit(int status);
```

# 描述

`quick_exit` 函数导致程序终止。如果程序多次调用 `quick_exit` 函数，或者在调用 `quick_exit` 函数的同时调用了 `exit` 函数，则其行为是未定义的。如果在 `quick_exit` 执行期间触发了信号，其行为是未定义的。

`quick_exit` 函数首先调用通过 `at_quick_exit` 函数注册的所有函数，按执行的反序。如果在调用任何此类函数期间注册了，将调用 `longjmp` 函数，这将终止对注册函数的调用，其行为是未定义的。

然后通过 `_Exit(status)` 将控制返回主环境。

# 返回值

`quick_exit` 函数不返回给其调用者。

## 7.24.5.8 The system 函数

# 概要

```
#include <stdlib.h>

int system(const char *string);
```

# 描述

如果 `string` 是空指针，`system` 函数确定主环境是否有命令处理器。如果 `string` 不是空指针，`system` 函数将 `string` 指向的字符串传递给命令处理器以一种实现应记录的方式进行执行；这可能导致调用 `system` 的程序以非标准的方式运行或终止。

# ISO/IEC 9899:2024(en)

返回值

如果参数为空指针，则仅当命令处理器可用时，`system` 函数才返回非零值。如果参数不是空指针，`system` 函数不返回，而是返回一个由实现定义的数值。

## 7.24.6 搜索和排序工具

### 7.24.6.1 通用说明

这些工具使用比较函数来搜索或排序未指定类型的数组。声明为 `size_t nmemb` 的参数指定了函数所需的数组长度，`nmemb` 在调用时可以为零；如果函数未被调用，则搜索将找不到任何匹配的元素；而排序将不执行任何重排。根据 `7.1.4` 的规定，在此类调用中，该的指针将仍具有有效值。

实现过程应确保比较函数的第二个参数（当从 `bsearch` 调用时）或两个参数（当从 `qsort` 调用时）都是指向数组元素的指针。³ 当从 `bsearch` 调用时，第一个参数应等于 `key`。

比较函数不应改变数组的内容。实现过程可以在多次调用比较函数之间重新排列数组元素，但不应改变任何单个元素的内容。

当对象（由 `size` 字节组成，无论它们在数组中的当前位置）被多次传递给比较函数时，其结果应当相互一致。例如，对于 `qsort`，它们定义了数组的一个全序；而对于 `bsearch`，同一个对象与其他对象的比较应始终以相同的方式。

在每次调用比较函数之前和紧之后都会发生一个序列点，同时也发生在任何比较函数的调用与任何作为参数传递的对象的移动之间。

### 7.24.6.2 bsearch 泛型函数

### 概要

```
#include <stdlib.h>

void *bsearch(const void *key, void *base, size_t nmemb,
               int (*)(const void *, const void *));
```

### 描述

`bsearch` 泛型函数搜索包含 `nmemb` 个对象的数组，其初始元素由 `base` 指向，寻找与 `key` 指向的对象匹配的元素。数组中每个元素的大小由 `size` 指定。

用于比较的比较函数接收两个参数，分别指向 `key` 和一个元素；因此，如果 `key` 对象被认为分别小于、等于或大于数组元素，则函数应返回小于、等于或大于零的整数。数组应包含：所有小于 `key` 的元素、所有等于 `key` 的元素以及所有大于 `key` 对象的元素，按上述顺序排列.³

### 返回值

`bsearch` 泛型函数返回指向数组元素的指针，如果没有找到匹配项，则返回空指针。如果两个元素比较结果相等，则匹配的元素是不确定的。

> ³50⁹如果值为 `p`，则以下表达式始终为非零：

```
((char*)p - (char*)base) % size == 0
((char*)p >= (char*)base)
((char*)p < (char*)base + nmemb * size)
```

³⁵¹⁰在实践中，整个数组会根据比较函数进行排序。

`bsearch` 函数对于参数 `base` 所指向的类型是泛型的。如果该参数指向一个带有 `const` 修饰符的对象类型，则返回的指针将是指向 `const` 修饰 `void` 的指针。否则，该参数指向一个未修饰的对象类型指针或空指针，${352}且返回的指针将是指向未修饰 `void` 的指针。

`bsearch` 的外部声明类型如下：

```
void * (const void *, const void *, size_t, size_t,
int (*)(const void *, const void *));
```

它支持所有正确的用法。该泛型函数的宏定义被抑制以访问实际函数，该外部声明使用此${353}

### 7.24.6.3 qsort 函数

### 概要

```
#include <stdlib.h>

void qsort(void *base, size_t nmemb, size_t size,
int (*compare)(const void *, const void *));
```

### 描述

`qsort` 函数对包含 `nmemb` 个元素的数组进行排序，其初始元素由 `base` 指向。每个对象的大小由 `size` 指定。

数组的内容根据指向用于比较的比较函数按升序排列，该函数接收两个指向被比较对象的参数。如果第一个参数被认为分别小于、等于或大于第二个参数，则该函数应返回小于、等于或大于零的整数。

如果两个元素比较结果相等，它们在结果排序数组中的顺序是不确定的。

### 返回值

`qsort` 函数不返回任何值。

## 7.24.7 整数算术函数

### 7.24.7.1 abs, labs 和 llabs 函数

### 概要

```
#include <stdlib.h>

int abs(int j);
long int labs(long int j);
long int llabs(long long int j);
```

### 描述

`abs`, `labs`, `llabs` 函数计算整数 `j` 的绝对值。如果结果无法表示，则行为是未定义的.${354}

### 返回值

`abs`, `labs`, `llabs` 函数返回绝对值。

## 7.24.7.2 div, ldiv 和 lldiv 函数

### 概要

```
#include <stdlib.h>

div_t div(int numer, int denom);
ldiv_t ldiv(long int numer, long int denom);
lldiv_t lldiv(long long int numer, long long int denom);
```

### 描述

`div`, `ldiv` 和 `lldiv` 函数在一次操作中计算 `numer/denom`。

### 返回值

`div`, `ldiv` 和 `lldiv` 函数分别返回 `div_t`, `ldiv_t` 和 `lldiv_t` 结构，包含商和余数，每个类型与 `numer` 和 `denom` 相同。

## 7.24.8 多字节/宽字符转换函数

### 7.24.8.1 通用说明

多字节函数受当前区域 `LC_CTYPE` 类别的影响。对于状态依赖编码，`mbtowc` 和 `mcomb` 函数在第一次调用前进入其初始状态，并通过空指针调用返回该状态。实现过程决定状态是否具有线程持续，以及新创建的线程是否与创建时的线程状态相同。以 `s` 为空指针会导致这些函数在编码依赖时返回非零值，否则返回零。

更改 `LC_CTYPE` 类别会导致描述状态的内部对象具有不定的表示。

### 7.24.8.2 mblen 函数

```
#include <stdlib.h>

int mblen(const char *s, size_t n);
```

### 描述

如果 `s` 不是空指针，`mblen` 函数返回 `s` 指的多字节字符包含的字节数。除了 `mbtowc` 函数转换状态不受影响外，它等同于

```
mbtowc((wchar_t *)0, (const char *)0);
mbtowc((wchar_t *)0, s, n);
```
