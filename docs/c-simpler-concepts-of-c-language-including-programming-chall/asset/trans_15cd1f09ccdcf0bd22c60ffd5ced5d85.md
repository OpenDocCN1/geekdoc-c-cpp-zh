

# 指针

```c
#include<stdio.h>
void main() {
    int *p, size;
    printf("Enter the array size...\n");
    scanf("%d", &size);
    p = (int *) calloc(size, sizeof(int));
    if(p == NULL) {
        printf("OUT OF MEMORY error!\n");
    } else {
        printf("\nEnter the array elements one by one...\n");
        for(i = 0; i < size; i++) {
            scanf("%d", &p[i]);
        }
        printf("\nThe array elements are...\n");
        for(i = 0; i < size; i++) {
            printf("%d->", p[i]);
        }
        free(p);
        getch();
    }
}
```

# 程序 7.11 calloc()

## realloc()
在某些情况下，你可能会觉得为数组分配的内存不足。在这种情况下，realloc() 将有助于在重新分配已分配内存的同时，同时保留已初始化的值。

### 语法
`void *realloc(void *p, size_t new_size);` -> 用新大小重新分配指针 p。

程序 7.11 完美地使用了 `realloc(0)`。该程序最初为数组分配了一些内存。如果用户想向数组中插入更多元素，可以通过 `realloc()` 重新分配内存。

```c
#include<stdio.h>
void main() {
    int *p, oldsize, options, rem;
    printf("Enter the array size...\n");
    scanf("%d", &oldsize);
    p = (int *) calloc(oldsize, sizeof(int));
    if(p == NULL) {
        printf("OUT OF MEMORY error!\n");
    } else {
        printf("\nEnter the array elements one by one...\n");
        for(i = 0; i < oldsize; i++) {
            scanf("%d", &p[i]);
        }
        printf("\nThe array elements are...\n");
        for(i = 0; i < oldsize; i++) {
            printf("%d->", p[i]);
        }
        printf("\nDo you want to increase the size of the array? (0:NO ;1:YES)\n");
        scanf("%d", &options);
    }
}
```

# 程序 7.11 Realloc 第一部分

```c
if(options)
{
    printf("enter the new size.\n");
    scanf("%d", &newsize);
    rem = newsize - oldsize;
    p = (int*)realloc(p, (oldsize + rem) * sizeof(int));
    printf("Enter the %d elements.", rem);
    for(i = oldsize; i < newsize; i++)
        scanf("%d", &p[i]);
    printf("\nNow the contents are.\n");
    for(i = 0; i < newsize; i++)
        printf("%d->%d\n", i, p[i]);
}
else
    printf("\nThank YOU!");
free(p);
getch();
```

# 程序 7.11 Realloc 第二部分

上述程序的输出如下：

```
Enter the array size..:3
Enter the array elements one by one.
10
20
30
The array elements are..
10-->20-->30->
Do you want to increase the size of the array? (0 - NO; 1 - YES)
enter the new size..
7
Enter the 4 elements..
40
50
60
70
Now the contents are..
10-->20-->30-->40-->50-->60-->70->
```

# 输出 7.11

到此为止，动态内存分配讲解结束。读者现在应该对指针相关的概念有了基本的理解。

# 注意要点

- 指针持有相同类型的另一个变量的地址。
- 指针变量在声明时前面带有有 `*`；通过 `&variable` 获取变量的地址，通过 `*pointer variable` 获取指针指向的值。
- 已声明但未初始化的指针被称为“野指针”（bad pointers），它们指向随机的内存位置。
- 任意数量的指针可以指向同一个变量，这意味着许多指针可以共享同一个变量。

- 指针在引用传递（by reference）中非常有帮助。
- 指针可以执行加增、递减、加、减、比较操作。
- 指针变量占用 4 字节。还有其他类型的指针称为近指针（near）和远指针（far），它们分别占用 16 位（2 字节）和 32 位。近远指针在 Linux GCC 和 Visual C++ 中无效。
- 动态内存分配结构包括 `malloc()`、`calloc()`、`realloc()`、`free()`。
- 动态分配的内存在使用后应该释放（free）。
- 指针和数组之间存在内在联系。当数组作为参数传递给函数时，它的基地址会被传递给函数。
- 函数指针是可以指向函数的指针。

# 7.9. 练习题

1. 什么是空指针（NULL pointer）？
2. 什么是空指针（void pointer）？
3. 指针上可以执行哪些操作？
4. 当两个指向同一个数组的指针相减时会发生什么？
5. 指针和数组之间存在什么内在联系？

# 7.10. 编程练习

以下代码的输出将会是什么？
（此处省略重复的代码块，已按要求去重）

