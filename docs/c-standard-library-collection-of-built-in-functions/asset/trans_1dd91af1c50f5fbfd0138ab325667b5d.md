
此函数在成功注册时返回零值，否则在失败时返回非零值。

### 示例
以下示例展示了 atexit() 函数的用法。

```c
#include <stdio.h>
#include <stdlib.h>

void functionA ()
{
    printf("This is functionA\n");
}

int main ()
{
    /* register the termination function */
    atexit(functionA );

    printf("Starting  main program...\n");

    printf("Exiting main program...\n");

    return(0);
}
```

让我们编译并运行上述程序，将会产生以下结果：

```
Starting main program...
Exiting main program...
This is functionA
```

## void exit(int status)
### 描述
C 库函数 **void exit(int status)** 会立即终止调用进程。进程拥有的任何打开文件描述符都会被关闭，进程的任何子进程都将被进程 1、init 继承，并且向进程父进程发送 SIGCHLD 信号。

### 声明
以下是 exit() 函数的声明。

```c
void exit(int status)
```

### 参数
- **status** -- 这是返回给父进程的状态值。

### 返回值
此函数不返回任何值。

### 示例
以下示例展示了 exit() 函数的用法。

```c
#include <stdio.h>
#include <stdlib.h>

int main ()
{
    printf("Start of the program....\n");
    printf("Exiting the program....\n");
    exit(0);
    printf("End of the program....\n");
    return(0);
}
```

让我们编译并运行上述程序，将会产生以下结果：

```
Start of the program....
Exiting the program....
```

## char *getenv(const char *name)
### 描述
C 库函数 char *getenv(const char *name) 按名称搜索指向的环境字符串并返回该字符串关联的值。

### 声明
以下是 getenv() 函数的声明。

```c
char *getenv(const char *name)
```

### 参数
- name -- 这是包含所请求变量名称的 C 字符串。

### 返回值
此函数返回一个以空字符结尾的字符串，其中包含所请求环境变量的值，如果该环境变量不存在则返回 NULL。

### 示例
以下示例展示了 getenv() 函数的用法。

```c
#include <stdio.h>
#include <stdlib.h>

int main ()
{
    printf("PATH : %s\n", getenv("PATH"));
    printf("HOME : %s\n", getenv("HOME"));
    printf("ROOT : %s\n", getenv("ROOT"));

    return(0);
}
```

让我们编译并运行上述程序，将会产生以下结果：

```
PATH : /sbin:/usr/sbin:/bin:/usr/bin:/usr/local/bin
HOME : /
ROOT : (null)
```

## int system(const char *string)
### 描述
C 库函数 int system(const char *command) 将 command 指定的命令名称或程序名称传递给主机环境，由命令处理器执行，并在命令完成后返回。

### 声明
以下是 system() 函数的声明。

```c
int system(const char *command)
```

### 参数
- **command** -- 这是包含所请求变量名称的 C 字符串。

### 返回值
返回值在出错时为 -1，否则为命令的返回状态。

### 示例
以下示例展示了 system() 函数的用法，用于在 unix 机器上列出当前目录下的所有文件和目录。

```c
#include <stdio.h>
#include <string.h>

int main ()
{
    char command[50];

    strcpy( command, "ls -l" );
    system(command);

    return(0);
}
```

让我们编译并运行上述程序，将会在我的 unix 机器上产生以下结果：

```
drwxr-xr-x 2 apache apache 4096 Aug 22 07:25 hsperfdata_apache
drwxr-xr-x 2 railo railo 4096 Aug 21 18:48 hsperfdata_railo
rw------- 1 apache apache   8 Aug 21 18:48 mod_mono_dashboard_XXGLOBAL_1
rw------- 1 apache apache   8 Aug 21 18:48 mod_mono_dashboard_asp_2
srwx----- 1 apache apache   0 Aug 22 05:28 mod_mono_server_asp
rw------- 1 apache apache   0 Aug 22 05:28 mod_mono_server_asp_1280495620
srwx----- 1 apache apache   0 Aug 21 18:48 mod_mono_server_global
```

以下示例展示了 system() 函数的用法，用于在 windows 机器上列出当前目录下的所有文件和目录。

```c
#include <stdio.h>
#include <string.h>

int main ()
{
    char command[50];

    strcpy( command, "dir" );
    system(command);

    return(0);
}
```

让我们编译并运行上述程序，将会在我的 windows 机器上产生以下结果：

```
a.txt
amit.doc
sachin
saurav
file.c
```

## void *bsearch(const void *key, const void *base, size_t nitems, size_t size, int (*compar)(const void *, const void *))
### 描述
C 库函数 void *bsearch(const void *key, const void *base, size_t nitems, size_t size, int (*compar)(const void *, const void *)) 在由 base 指向的 nitems 个对象的数组中搜索与 key 指向的对象匹配的成员。数组中每个成员的大小由 size 指定。

数组的内容应根据 compar 引用的比较函数按升序排序。

### 声明
以下是 bsearch() 函数的声明。

```c
void *bsearch(const void *key, const void *base, size_t nitems, size_t size, int (*compar)(const void *, const void *))
```

### 参数
- **key** -- 这是指向用作搜索键的对象的指针，类型强制转换为 void*。
- **base** -- 这是指向执行搜索的数组第一个对象的指针，类型强制转换为 void*。
- **nitems** -- 这是由 base 指向的数组中的元素数量。
- **size** -- 这是数组中每个元素的字节大小。
- **compar** -- 这是比较两个元素的函数。

### 返回值
此函数返回数组中与搜索键匹配的条目的指针。如果未找到 key，则返回 NULL 指针。

### 示例
以下示例展示了 bsearch() 函数的用法。

```c
#include <stdio.h>
#include <stdlib.h>

int cmpfunc(const void * a, const void * b)
{
    return ( *(int*)a - *(int*)b );
}

int values[] = { 5, 20, 29, 32, 63 };

int main ()
{
    int *item;
    int key = 32;

    /* using bsearch() to find value 32 in the array */
    item = (int*) bsearch (&key, values, 5, sizeof (int), cmpfunc);
    if( item != NULL )
{
    printf("Found item = %d\n", *item);
}
else
{
    printf("Item = %d could not be found\n", *item);
}

return(0);
}
```

让我们编译并运行上述程序，将会产生以下结果：

```
Found item = 32
```

## void qsort(void *base, size_t nitems, size_t size, int (*compar)(const void *, const void *))
### 描述
C 库函数 void qsort(void *base, size_t nitems, size_t size, int (*compar)(const void *, const void *)) 对数组进行排序。

### 声明
以下是 qsort() 函数的声明。

```c
void qsort(void *base, size_t nitems, size_t size, int (*compar)(const void *, const void *));
```

### 参数
- **base** -- 这是指向要排序的数组第一个元素的指针。
- **nitems** -- 这是由 base 指向的数组中的元素数量。
- **size** -- 这是数组中每个元素的字节大小。
- **compar** -- 这是比较两个元素的函数。

### 返回值
此函数不返回任何值。

### 示例
以下示例展示了 qsort() 函数的用法。

```c
#include <stdio.h>
#include <stdlib.h>

int values[] = { 88, 56, 100, 2, 25 };

int cmpfunc (const void * a, const void * b)
{
    return ( *(int*)a - *(int*)b );
}

int main()
{
    int n;

    printf("Before sorting the list is: \n");
    for( n = 0 ; n < 5; n++ ) {
        printf("%d ", values[n]);
    }

    qsort(values, 5, sizeof(int), cmpfunc);

    printf("\nAfter sorting the list is: \n");
    for( n = 0 ; n < 5; n++ ) {
        printf("%d ", values[n]);
    }

    return(0);
}
```

让我们编译并运行上述程序，将会产生以下结果：

```
Before sorting the list is:
88 56 100 2 25
After sorting the list is:
2 25 56 88 100
```
