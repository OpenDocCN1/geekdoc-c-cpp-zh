

# 动态数组及其自动扩容

动态数组为 C 语言编程中静态数组的局限性提供了一种优雅的解决方案，主要是要求在编译前声明数组大小以及在运行时无法更改该大小的限制。与静态数组不同，动态数组可以在运行时调整大小，以根据需要容纳更多元素。这种能力显著增强了在元素总数无法先知的情况下管理集合的效率和灵活性。在本节中，我们将深入探讨 C 语言动态数组的实现细节，包括它们如何自动调整大小以处理增加或减少的数据集。

## 概念与实现：

动态数组在达到容量时会自动增加大小，在可选情况下，当删除了大量元素时，会减小大小。高效调整动态数组大小的关键在于最小化内存使用与减少调整操作频率（该操作的计算开销很大）之间取得平衡。

结构定义：C 语言中典型的动态数组可以使用结构体定义，它封装了数组、容量和当前元素数量，如下：

```c
typedef struct {
    int *array;
    size_t capacity;
    size_t size;
} DynamicArray;
```

初始创建与扩容：动态数组最初以预定义的容量创建。当添加的元素超过容量时，数组的容量会增加（通常是翻倍），为为更多元素留出空间。

```c
void initDynamicArray(DynamicArray *dArray, size_t initialCapacity) {
    dArray->array = malloc(initialCapacity * sizeof(int));
    dArray->capacity = initialCapacity;
    dArray->size = 0;
}

void resizeIfNecessary(DynamicArray *dArray) {
    if (dArray->size == dArray->capacity) {
        dArray->capacity *= 2;
        dArray->array = realloc(dArray->array, dArray->capacity * sizeof(int));
    }
}
```

添加与删除元素：添加或删除元素的函数涉及是否需要通过增加或减少数组容量来完成调整。

```c
void addElement(DynamicArray *dArray, int element) {
    resizeIfNecessary(dArray);
    dArray->array[dArray->size] = element;
    dArray->size++;
}

void removeElement(DynamicArray *dArray, size_t index) {
    for (size_t i = index; i < dArray->size - 1; i++) {
        dArray->array[i] = dArray->array[i + 1];
    }
    dArray->size--;
    // 可选：如果 size 远小于 capacity 则减小容量
}
```

访问元素：访问动态数组中的元素与访问静态数组类似，利用数组索引即可。

```c
int getElement(DynamicArray *dArray, size_t index) {
    if (index < dArray->size) {
        return dArray->array[index];
    }
    return -1; // 错误值
}
```

销毁：为了避免内存泄漏，动态数组在不再需要时必须被妥善释放。

```c
void freeDynamicArray(DynamicArray *dArray) {
    free(dArray->array);
    dArray->array = NULL;
    dArray->size = 0;
    dArray->capacity = 0;
}
```

代码输出：

添加元素：10, 20, 30
数组大小：3, 数组容量：4
删除索引为 1 的元素
数组大小：2, 数组容量：4

动态数组展现了尺寸管理上的灵活性与数据访问效率的结合，使其成为解决数据集合动态的现实问题的不可或缺的工具。通过精心的实现，动态数组可以显著优化 C 程序中的内存使用和性能。

# 3.7

# 用于调度应用的优先级队列与二叉堆

优先级队列是许多计算机科学领域的关键数据结构，特别是在需要根据紧急程度或重要性管理任务的调度应用。与遵循先进先出（FIFO）原则的典型队列不同，优先级队列确保优先级最高的元素首先取出，无论其在队列中的位置如何。本节深入探讨使用二叉堆实现优先级队列，这是一种极其高效的方法，它利用完全二叉树的属性来确保根据优先级进行最优入队和出队操作。

二叉堆：二叉堆是一种满足堆属性的完全二叉树；每个节点都大于或等于（最大堆）或小于或等于（最小堆）其子节点。该属性确保优先级最高（或最低）的元素始终位于树的根。二叉堆通常使用数组实现，其中索引为 $i$ 的元素的节点位于索引 $2i+1$（左孩子）和 $2i+2$（右孩子），索引为 $i$ 的元素的父节点位于

优先级队列操作：

- 向优先级队列入队元素，保持堆属性。
- 从队列中返回优先级最高（或最低）的元素。
- 查看（peek）优先级最高（或最低）的元素但不将其移除。

使用最小堆实现优先级队列：为了说明，我们将实现一个最小堆优先级队列，其中值越小的元素优先级越高。

```c
#define MAX_SIZE 100
typedef struct {
    int data[MAX_SIZE];
    int size;
} MinHeap;

void swap(int *x, int *y) {
    int temp = *x;
    *x = *y;
    *y = temp;
}
```
*(后续文本内容为乱码/重复，跳过翻译)*

