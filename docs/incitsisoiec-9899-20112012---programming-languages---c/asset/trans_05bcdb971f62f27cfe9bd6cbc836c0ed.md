

`aligned_alloc` 函数为对象分配空间，该对象的对齐方式由 `alignment` 指定，大小由 `size` 指定，且其值是不确定的。`alignment` 的值应该是实现支持的有效对齐方式，且 `size` 的值应该是 `alignment` 的整数倍。

## 返回

`aligned_alloc` 函数返回空指针或指向分配空间的指针。

## 7.22.3.2 calloc 函数

### 摘要

```
#include <stdlib.h>
void *calloc(size_t nmemb, size_t size);
```

### 描述

`calloc` 函数为一个包含 `nmemb` 个对象的数组分配空间，其中每个对象的大小为 `size`。该空间被初始化为所有位均为零。²296

## 返回

`calloc` 函数返回空指针或指向分配空间的指针。

## 7.22.3.3 free 函数

### 摘要

```
#include <stdlib.h>
void free(void *ptr);
```

### 描述

`free` 函数导致 `ptr` 所指向的空间被释放，即该空间可供进一步分配。如果 `ptr` 是空指针，则不发生任何操作。否则，如果参数与之前由内存管理函数返回的指针不匹配，或者该空间已经通过调用 `free` 或 `realloc` 被释放，则行为是未定义的。

## 返回

`free` 函数不返回值。

296 注意，这不需要等同于浮点零的表示或空指针常量。

## 7.22.3.4 malloc 函数

### 摘要

```
#include <stdlib.h>
void *malloc(size_t size);
```

### 描述

`malloc` 函数为一个大小由 `size` 指定且其值是不确定的对象分配空间。

### 返回

`malloc` 函数返回空指针或指向分配空间的指针。

## 7.22.3.5 realloc 函数

### 摘要

```
#include <stdlib.h>
void *realloc(void *ptr, size_t size);
```

### 描述

`realloc` 函数释放 `ptr` 所指向的旧对象，并返回一个指向新对象的指针，该新对象的大小由 `size` 指定。新对象的内容应与释放前的旧对象内容相同，直到达到新旧大小中的较小值。新对象中超出旧对象大小的任何字节，其值是不确定的。

如果 `ptr` 是空指针，`realloc` 函数的行为等同于指定大小的 `malloc` 函数。否则，如果 `ptr` 与之前由内存管理函数返回的指针不匹配，或者该空间已经通过调用 `free` 或 `realloc` 函数被释放，则行为是未定义的。如果无法为新对象分配内存，旧对象不会被释放，其值保持不变。

### 返回

`realloc` 函数返回指向新对象的指针（该指针可能与指向旧对象的指针相同），或者在无法分配新对象时返回空指针。

## 7.22.4 与环境的通信

### 7.22.4.1 abort 函数

### 摘要

```
#include <stdlib.h>
_Noreturn void abort(void);
```

### 描述

`abort` 函数导致程序异常终止，除非正在调用信号 `SIGABRT` 且信号处理程序没有返回。是否刷新带有未写入缓冲数据的打开流、关闭打开流或删除临时文件由实现定义。通过函数调用 `raise(SIGABRT)` 向宿主环境返回一种实现定义的非成功终止状态。

## 返回

`abort` 函数不返回给其调用者。

## 7.22.4.2 atexit 函数

### 摘要

```
#include <stdlib.h>
int atexit(void (*func)(void));
```

### 描述

`atexit` 函数注册一个函数在程序正常结束时被调用，该函数不带参数。(297) 如果在调用 `exit` 函数之前没有调用 `atexit` 函数，调用是否会成功是不确定的。

#### 环境限制

实现应至少支持 32 个函数的注册。

### 返回

`atexit` 函数在注册成功时返回零，失败时返回非零。

前向引用：`at_quick_exit` 函数 (7.22.4.3)，`exit` 函数 (7.22.4.4)。

> 297 `atexit` 注册与 `at_exit` 注册是不同的，因此应用程序可能需要两个都调用。

## 7.22.4.3 at_quick_exit 函数

### 摘要

```
#include <stdlib.h>
int at_quick_exit(void (*func)(void));
```

### 描述 

`at_quick_exit` 函数注册一个函数在程序正常结束时被调用，该函数不带参数。(298) 如果在调用 `at_exit` 函数之前没有调用 `at_quick_exit` 函数，调用是否会成功是不确定的。

#### 环境限制

实现应至少支持 32 个函数的注册。 

### 返回

`at_quick_exit` 函数在注册成功时返回零，失败时返回非零。

298 注意 `at_quick_exit` 注册与 `at_exit` 注册是不同的，因此应用程序可能需要两个都调用。

## 7.22.4.4 exit 函数

### 摘要

```
#include <stdlib.h>
_Noreturn void exit(int status);
```

### 描述 

`exit` 函数导致程序正常终止。是否刷新带有未写入缓冲数据的打开流、关闭打开流或删除临时文件由实现定义。通过函数调用 `raise(SIGABRT)` 向宿主环境返回一种实现定义的非成功终止状态。

首先，`exit` 函数按反序调用所有通过 `atexit` 注册的函数。然后，它按反序调用所有通过 `at_quick_exit` 注册的函数。最后，返回宿主环境。如果参数与之前由内存管理函数返回的指针不匹配，或者该空间已经通过调用 `free` 或 `realloc` 被释放，则行为是未定义的。

## 7.22.4.5 _Exit 函数

### 摘要

```
#include <stdlib.h>
_Noreturn void _Exit(int status);
```

### 描述

`_Exit` 函数导致程序正常终止。是否刷新带有未写入缓冲数据的打开流、关闭打开流或删除临时文件由实现定义。通过函数调用 `raise(SIGABRT)` 向宿主环境返回一种实现定义的非成功终止状态。

## 7.22.4.6 getenv 函数

### 摘要

```
#include <stdlib.h>
char *getenv(const char *name);
```

### 描述 

`getenv` 函数在宿主环境提供的列表中搜索与所指向字符串匹配的字符串。环境变量的集合和更改环境的方法由实现定义。`getenv` 函数不需要避免与修改环境变量的其他执行线程产生数据竞态。

`getenv` 函数返回指向匹配成员关联字符串的指针。所指向的字符串不应被程序修改，但可能会被后续的 `getenv` 调用覆盖。如果找不到指定的名称，则返回空指针。

## 7.22.4.7 quick_exit 函数

### 摘要

```
#include <stdlib.h>
Noreturn void quick_exit(int status);
```

### 描述 

`quick_exit` 函数导致程序正常终止。是否刷新带有未写入缓冲数据的打开流、关闭打开流或删除临时文件由实现定义。通过函数调用 `raise(SIGABRT)` 向宿主环境返回一种实现定义的非成功终止状态。

`quick_exit` 函数首先按反序调用所有通过 `at_quick_exit` 注册的函数。然后，它按反序调用所有通过 `atexit` 注册的函数。最后，返回宿主环境。如果 `status` 的值为 `EXIT_SUCCESS`，则返回一个实现定义的状态；如果 `status` 的值为 `EXIT_FAILURE`，则返回一个实现定义的状态。

