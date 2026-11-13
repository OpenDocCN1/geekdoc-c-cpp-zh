

## 基本操作

数据结构中的数据由某些操作处理。所选的特定数据结构在很大程度上取决于需要对数据结构执行的操作的频率。

- 遍历
- 搜索
- 插入
- 删除
- 排序
- 合并

## 9. 数组数据结构与算法

数组是一个容器，可以容纳固定数量的项目，这些项目应为相同类型。大多数数据结构都使用数组来实现其算法。以下是理解数组概念的重要术语。

**元素** – 存储在数组中的每个项目称为元素。

**索引** – 数组中每个元素的位置都有一个数值索引，用于标识元素。

### 数组表示

数组可以在不同语言中以多种方式声明。为示例，让我们看看 C 语言的数组声明。

```c
int array[10] = { 35, 33, 42, 10, 14, 19, 27, 44, 26, 31 }
```

| 元素 | 35 | 33 | 42 | 10 | 14 | 19 | 27 | 44 | 26 | 31 |
|------|----|----|----|----|----|----|----|----|----|----|
| 索引 | 0  | 1  | 2  | 3  | 4  | 5  | 6  | 7  | 8  | 9  |

以下是需要考虑的重要点。

索引从 0 开始。

数组长度为 10，这意味着它可以存储 10 个元素。

每个元素可以通过其索引访问。例如，我们可以获取索引 6 处的元素为 27。

### 基本操作

以下是数组支持的基本操作。

- **遍历** – 逐个打印所有数组元素。
- **插入** – 在给定索引处添加一个元素。
- **删除** – 删除给定索引处的一个元素。
- **搜索** – 使用给定索引或按值搜索元素。
- **更新** – 更新给定索引处的元素。

在 C 语言中，当数组按大小初始化时，它会按以下顺序为其元素分配默认值。

### 数据类型 默认值

| 数据类型 | 默认值 |
|----------|--------|
| bool     | false  |
| char     | 0      |
| int      | 0      |
| float    | 0.0f   |
| double   | 0.0    |
| wchar_t  | 0      |

### 插入操作

插入操作是将一个或多个数据元素插入数组。根据要求，新元素可以添加到数组的开头、结尾或任何给定索引处。

这里，我们看到插入操作的实际实现，其中我们在数组末尾添加数据 –

### 算法

设数组为包含 MAX 个元素的线性无序数组。

### 示例

### 结果

设 LA 为包含 N 个元素的线性数组（无序），K 是满足 K<=N 的正整数。以下是将 ITEM 插入 LA 第 K 个位置的算法 –

1. 开始
2. 设置 J=N
3. 设置 N = N+1
4. 当 J >= K 时重复步骤 5 和 6
5. 设置 LA[J+1] = LA[J]
6. 设置 J = J-1
7. 设置 LA[K] = ITEM
8. 停止

### 示例

以下是上述算法的实现 –

```c
#include <stdio.h>
main() {
int LA[] = {1,3,5,7,8};
int item = 10, k = 3, n = 5;
int i = 0, j = n;

printf("The original array elements are :\n");
for(i = 0; i<n; i++) {
printf("LA[%d] = %d \n", i, LA[i]);
}

n = n + 1;

while( j >= k){
LA[j+1] = LA[j]; j = j - 1;
}
LA[k] = item;
printf("The array elements after insertion \n");
for(i = 0; i<n; i++) {
printf("LA[%d] = %d \n", i, LA[i]);
}
}
```

当我们编译并执行上述程序时，它会产生以下结果 –

```
The original array elements are :
LA[0]=1
LA[1]=3
LA[2]=5
LA[3]=7
LA[4]=8
```

```
The array elements after insertion :
LA[0]=1
LA[1]=3
LA[2]=5
LA[3]=10
LA[4]=7
LA[5]=8
```

有关数组插入操作的其他变体，请单击此处

### 数组插入

在上一节中，我们学习了插入操作的工作原理。并非总是将元素插入数组末尾。以下可能是数组插入的情况 –

- 在数组开头插入
- 在数组给定索引处插入
- 在数组给定索引之后插入
- 在数组给定索引之前插入

### 在数组开头插入

当插入发生在开头时，会导致所有现有数据项向下移动一步。这里，我们设计并实现一个算法，将元素插入数组开头。

### 算法

我们假设 A 是包含 N 个元素的数组。它可以存储的最大元素数由 MAX 定义。我们首先检查数组是否有空闲空间来存储任何元素，然后再进行插入过程。

```
begin
IF N = MAX, return ELSE
N = N + 1
For All Elements in A
Move to next adjacent location
A[FIRST] = New_Element
end
```

### C 语言实现

```c
#include <stdio.h>
#define MAX 5

void main() {
int array[MAX] = { 2, 3, 4, 5 };
int N = 4; // number of elements in array
int i = 0; // loop variable
int value = 1; // new data element to be stored in array

// print array before insertion
printf("Printing array before insertion \n");
for(i = 0; i < N; i++) {
printf("array[%d] = %d \n", i, array[i]);
}

// now shift rest of elements downwards
for(i = N; i >= 0; i--) {
array[i+1] = array[i];
}

// add new element at first position
array[0] = value;
// increase N to reflect number of elements
N++;
// print to confirm
printf("Printing array after insertion \n");

for(i = 0; i < N; i++) {
printf("array[%d] = %d\n", i, array[i]);
}
}
```

该程序应产生以下输出 –

```
Printing array before insertion – array[0] = 2
array[1] = 3
array[2] = 4
array[3] = 5
Printing array after insertion – array[0] = 1
array[1] = 2
array[2] = 3
array[3] = 4
array[4] = 5
```

### 在数组给定索引处插入

在此场景中，我们给出了数组的确切位置（索引），需要在其中插入新数据元素（值）。首先我们检查数组是否已满，如果未满，则将该位置的所有数据元素向下移动一步。这将为新数据元素腾出空间。

### 算法

我们假设 A 是包含 N 个元素的数组。它可以存储的最大元素数由 MAX 定义。
begin
IF N = MAX, return ELSE
N = N + 1
SEEK Location index
For All Elements from A[index] to A[N] Move to next adjacent location
A[index] = New_Element end

### C 语言实现

```c
#include <stdio.h>
#define MAX 5
void main() {
int array[MAX] = {1, 2, 4, 5};

int N = 4;
int i = 0;
int index = 2;
int value = 3;

// print array before insertion
printf("Printing array before insertion \n");
for(i = 0; i < N; i++) {
printf("array[%d] = %d \n", i, array[i]);
}

// now shift rest of the elements downwards
for(i = N; i >= index; i--) {
array[i+1] = array[i];
}

// add new element at first position
array[index] = value;
// increase N to reflect number of elements
N++;
// print to confirm
printf("Printing array after insertion \n");
for(i = 0; i < N; i++) {
printf("array[%d] = %d \n", i, array[i]);
}
}
```

如果我们编译并运行上述程序，它将产生以下结果 –
Printing array before insertion – array[0] = 1
array[1] = 2
array[2] = 4
array[3] = 5
Printing array after insertion – array[0] = 1
array[1] = 2
array[2] = 3
array[3] = 4
array[4] = 5

### 在数组给定索引之后插入

在此场景中，我们给出了数组的一个位置（索引），需要在其后插入新数据元素（值）。只有查找过程不同，其余活动与前面的示例相同。

### 算法

我们假设 A 是包含 N 个元素的数组。它可以存储的最大元素数由 MAX 定义。
begin
IF N = MAX, return ELSE
N = N + 1
SEEK Location index
For All Elements from A[index + 1] to A[N] Move to next adjacent location
A[index + 1] = New_Element end

### C 语言实现

```c
#include <stdio.h>
#define MAX 5
void main() {
int array[MAX] = {1, 2, 4, 5};

int N = 4; // number of elements in array
int i = 0; // loop variable
int index = 1; // index location after which value will be inserted
int value = 3; // new data element to be inserted

// print array before insertion
printf("Printing array before insertion \n");
for(i = 0; i < N; i++) {
printf("array[%d] = %d \n", i, array[i]);
}

// now shift rest of the elements downwards
for(i = N; i >= index + 1; i--) {
array[i + 1] = array[i];
}

// add new element at first position
array[index + 1] = value;
// increase N to reflect number of elements
N++;
// print to confirm
printf("Printing array after insertion \n");
for(i = 0; i < N; i++) {
printf("array[%d] = %d\n", i, array[i]);
}
}
```

如果我们编译并运行上述程序，它将产生以下结果 –

