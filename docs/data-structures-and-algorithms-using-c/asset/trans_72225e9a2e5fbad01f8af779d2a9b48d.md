

} else {
//Operator.pop two operands
operand2 = pop_int();
operand1 = pop_int();
switch(ch) {
case '+':
push_int(operand1+operand2); break;
case '-':
push_int(operand1-operand2); break;
case '*':
push_int(operand1*operand2); break;
case '/':
push_int(operand1/operand2); break;
}
}
return stack_int[top_int]; }

void main() {
char infix[25] = "1*(2+3)", postfix[25];
convert(infix, postfix);
printf("Infix expression is: %s\n", infix);
printf("Infix expression is: %s\n", postfix);
printf("Evaluated expression is: %d\n", evaluate(postfix));
}

如果编译并运行上述程序，它将产生以下结果 –

中缀表达式为: 1*(2+3) 后缀表达式为: 123+* 结果是: 5

## 15. 队列：数据结构与算法

队列是一种抽象数据结构，与栈有些相似。与栈不同，队列在两端都开放。一端始终用于插入数据（入队），另一端用于删除数据（出队）。队列遵循先进先出（First-In-First-Out）方法，即先存入的数据项将首先被访问。

![](img/30fc9e3f8ee01facfae8d1c9621936b3_118_0.png)

队列的现实例子可以是单行道单向车道，车辆先进入，先退出。更多现实例子可以在售票窗口和公交车站看到排队。

### 队列表示

现在我们了解到，在队列中，我们出于不同原因访问两端。下面的图表试图解释队列作为数据结构的表示 –

![](img/30fc9e3f8ee01facfae8d1c9621936b3_119_0.png)

与栈一样，队列也可以使用数组、链表、指针和结构体实现。为求简单，我们将使用一维数组实现队列。

### 基本操作

队列操作可能涉及初始化或定义队列、使用它，然后将其从内存中完全删除。这里我们将尝试理解与队列相关的基本操作 –

- enqueue() – 向队列添加（存储）一个项目。
- dequeue() – 从队列中删除（访问）一个项目。

为了使上述队列操作更高效，还需要一些其他函数。这些函数是 –

- peek() – 获取队列前端的元素，但不删除它。
- isfull() – 检查队列是否已满。
- isempty() – 检查队列是否为空。

在队列中，我们始终由 front 指针指向的数据进行出队（或访问），而在向队列中入队（或存储）数据时，我们借助 rear 指针。

首先，让我们了解一下队列的辅助函数 –

### peek()

此函数有助于查看队列前端的数据。peek() 函数的算法如下 –

```
begin procedure peek
return queue[front]
end procedure
```

C 语言中 peek() 函数的实现 –

```
int peek() {
return queue[front];
}
```

### isfull()

由于我们使用一维数组实现队列，只需检查 rear 指针是否达到 MAXSIZE 即可判断队列是否已满。如果我们使用循环链表维护队列，算法将有所不同。isfull() 函数的算法 –

```
begin procedure isfull
if rear equals to MAXSIZE return true
else
return false
endif
end procedure
```

C 语言中 isfull() 函数的实现 –

```
bool isfull() {
if(rear == MAXSIZE - 1) return true;
else
return false;
}
```

### isempty()

isempty() 函数的算法 –
begin procedure isempty

if front is less than MIN OR front is greater than rear return true
else
return false
endif

end procedure

如果 **front** 的值小于 MIN 或 0，则表示队列尚未初始化，因此为空。

这是 C 语言代码 –

```
bool isempty() {
if(front < 0 || front > rear) return true;
else
return false;
}
```

### 入队操作

队列维护两个数据指针，**front** 和 **rear**。因此，其实现相对于栈来说比较困难。

向队列中入队（插入）数据应采取以下步骤 – 步骤 1 – 检查队列是否已满。步骤 2 – 如果队列已满，产生溢出错误并退出。步骤 3 – 如果队列未满，递增 rear 指针以指向下一个空位。步骤 4 – 将数据元素添加到 rear 指向的队列位置。步骤 5 – 返回成功。

![](img/30fc9e3f8ee01facfae8d1c9621936b3_124_0.png)

### 队列入队

有时，我们还会检查队列是否已初始化，以处理任何意外情况。

### 入队操作的算法

```
procedure enqueue(data) if queue is full return overflow endif
rear ← rear + 1 queue[rear] ← data return true
end procedure
```

C 语言中 enqueue() 的实现 –

```
int enqueue(int data) {
if(isfull())
return 0;
rear = rear + 1;
queue[rear] = data;
return 1;
}
```

### 出队操作

从队列中访问数据是一个包含两个任务的过程 – 访问 front 指向的数据，并在访问后删除数据。执行出队操作的步骤如下 –

- 步骤 1 – 检查队列是否为空。
- 步骤 2 – 如果队列为空，产生下溢错误并退出。
- 步骤 3 – 如果队列不为空，访问 front 指向的数据。
- 步骤 4 – 递增 front 指针以指向下一个可用数据元素。
- 步骤 5 – 返回成功。

![](img/30fc9e3f8ee01facfae8d1c9621936b3_125_0.png)

### 出队操作的算法

```
procedure dequeue
if queue is empty
return underflow
end if
data = queue[front]
front <- front + 1
return true
end procedure
```

C 语言中 dequeue() 的实现 –

```
int dequeue() {
if(isempty())
return 0;
int data = queue[front];
front = front + 1;
return data;
}
```

有关 C 语言中完整的队列程序，请单击此处。

### C 语言中的队列程序

我们将在这里看到 C 语言中的栈实现。您可以单击 Try-it 按钮尝试该程序。要了解栈的理论方面，请单击访问上一页。

### C 语言实现

```
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <stdbool.h>
#define MAX 6
int intArray[MAX];
int front = 0;
int rear = -1;
int itemCount = 0;
int peek(){
return intArray[front];
}
bool isEmpty(){
return itemCount == 0;
}
bool isFull(){
return itemCount == MAX;
}
int size(){
return itemCount;
}
void insert(int data){
if(!isFull()){
if(rear == MAX-1){
rear = -1;
}
intArray[++rear] = data;
itemCount++;
}
}
int removeData(){
int data = intArray[front++];
if(front == MAX){
front = 0;
}
itemCount--;
return data;
}
int main() {
/* insert 5 items */
insert(3);
insert(5);
insert(9);
insert(1);
insert(12);
// front : 0
// rear : 4
// \______// index : 0 1 2 3 4 // \______// queue : 3 5 9 1 12
insert(15);
// front : 0
// rear : 5
// \______// index : 0 1 2 3 4 5 // \______// queue : 3 5 9 1 12 15
if(isFull()){
printf("Queue is full!\n");
}
// remove one item
int num = removeData();
printf("Element removed: %d\n",num);
// front : 1
// rear : 5
// index : 1 2 3 4 5
// \______
// queue : 5 9 1 12 15
// insert more items
insert(16);
// front : 1
// rear : -1
// \______// index : 0 1 2 3 4 5 // \______// queue : 16 5 9 1 12 15
// As queue is full, elements will not be inserted. insert(17);
insert(18);
// \______// index : 0 1 2 3 4 5 // \______// queue : 16 5 9 1 12 15
printf("Element at front: %d\n",peek());
printf("\\______\\n");
printf("index : 5 4 3 2 1 0\n");
printf("\\______\\n");
printf("Queue: ");
}
while(!isEmpty()){
int n = removeData();
printf("%d ",n);
}
```
如果编译并运行上述程序，它将产生以下结果 -

队列已满！
已移除的元素：3 前端元素：5
\______index : 5 4 3 2 1 0
\______队列: 5 9 1 12 15 16

## 搜索技术

## 16. 线性搜索：数据结构与算法

线性搜索是一种非常简单的搜索算法。在这种搜索中，会对所有项目逐一进行顺序搜索。每个项目都会被检查，如果找到匹配项，则返回该特定项目，否则搜索将持续到数据集合的末尾。

![](img/30fc9e3f8ee01facfae8d1c9621936b3_128_0.png)

### 算法

- 线性搜索（数组 A，值 x）
- 步骤 1：将 i 设置为 1
- 步骤 2：如果 i > n，则转到步骤 7
- 步骤 3：如果 A[i] = x，则转到步骤 6
- 步骤 4：将 i 设置为 i + 1
- 步骤 5：转到步骤 2
- 步骤 6：打印在索引 i 处找到元素 X，并转到步骤 8
- 步骤 7：打印未找到元素
- 步骤 8：退出

### 伪代码

```
procedure linear_search (list, value)
for each item in the list
if match item == value
return the item's location
end if
end for
end procedure
```

要了解 C 语言中线性搜索的实现，请单击此处。

