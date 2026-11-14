
```c
p_new_node = p_free_head;
p_free_head = p_free_head->p_next;
p_new_node->p_next = NULL;
/* Find the old end node. */
while (NULL != p_end_node->p_next)
{
    p_end_node = p_end_node->p_next;
}
/* Add the new node to the end of the list. */
p_end_node->p_next = p_new_node;
}
return p_new_node;
/* Remove a node from the list and put it back
* into the free list. This function does not
* check that p_node actually points to a valid
* node in the list. */
void list_remove_node(list_node_t * p_node)
{
    list_node_t * p_prev_node = p_list_head;
    list_node_t * p_end_free = p_free_head;
    /* Find the node before the one to be
    * removed. */

    while ((NULL != p_prev_node->p_next)
        && (p_node != p_prev_node->p_next))
    {
        p_prev_node = p_prev_node->p_next;
    }
    /* Remove the node from the list. */
    p_prev_node->p_next = p_node->p_next;
    p_node->p_next = NULL;
    /* Add the node to the end of the free
    * list. */
    if (NULL != p_end_free)
    {
        /* If the free list is not empty, find the
        * last node of the free list and point it
        * to the freed node. */
        while (NULL != p_end_free->p_next)
        {
            p_end_free = p_end_free->p_next;
        }
        p_end_free->p_next = p_node;
    }
    else
    {
        /* If the free list is empty, start a new
        * one. */
        p_free_head = p_node;
    }
}

## Fig 3.2 基本链表数据结构易于实现。列表中的每个元素都包含一个指向下一个元素的指针，这提供了“链接”——最后一个链接指向 NULL。双向链表在每个条目中添加一个指向前一个元素的链接。在循环链表中，列表最终会回到自身——而不是链接到最后一个元素，它链接回第一个元素，尽管在这种情况下“第一个”和“最后一个”基本上变得没有意义。列表通常仅旨在包含一种类型，尽管类型泛型实现是可能的。

尽管链表本身是有用的数据结构，但它们也是实现队列和池的重要基础块，而队列和池是管理内存最有用的结构之一。也可以使用链表实现栈，不过，这也可以仅使用数组来实现。

## 栈

栈（偶尔称为 LIFO，即后进先出）是一种简单的数据结构，允许变量以与写入相反的顺序进行读取和移除。读取和写入操作通常分别称为“pop”和“push”。由于 pop 操作也会从栈中移除变量，因此通常还有一个“peek”操作，用于在不移除值的情况下读取值。

大多数软件已经包含一个栈，通常简称为栈，尽管这并非由程序员直接管理。相反，由于它用于局部变量分配以及处理函数调用和返回，管理它的代码由编译器生成。在这些情况下，大部分工作是使用硬件完成的。

需要时，栈易于实现且效率高。可以使用数组存储数据，并使用指向下一个空闲元素的指针。pop 和 push 函数只需将数据复制到栈中或从栈中复制，并根据需要递增或递减指针。还建议包含额外逻辑以防止栈上溢或下溢。如果栈仅需要存储一种数据类型，则可以使用整数来跟踪下一个空闲位置，而不是使用指针；如果栈旨在存储多种数据类型，则应将其实现为

```c
/* Create a generic stack. */
static char stack_array[STACK_SIZE];
static char *p_stack_end = stack_array;
static int stack_free_space = STACK_SIZE;
/* Push data on to the stack. Returns 'true' if
 * the data is successfully added to the
 * stack. */
bool stack_push(char *p_data, int size)
{
    bool success = false;
    int bytes_to_copy = size;
    /* If the stack has space, copy the data on
     * to it. */
    if (stack_free_space >= size)
    {
        while (0 < bytes_to_copy)
        {
            *p_stack_end++ = *p_data++;
            --bytes_to_copy;
        }
    }
    stack_free_space -= size;
    success = true;
    return success;
}
/* Pop data from the stack. Returns true if the
 * data is successfully copied from the
 * stack. */
bool stack_pop(char *p_data, int size)
{
    bool success = false;
    int bytes_to_copy = size;
    /* Get a pointer to the end of p_data. */
    char * p_data_end = &(p_data[size - 1]);
    /* If there is enough data on the stack, copy
    * it. */
    if (STACK_SIZE >= (size + stack_free_space))
    {
        while (0 < bytes_to_copy)
        {
            *p_data_end-- = *p_stack_end--;
            --bytes_to_copy;
        }
        stack_free_space += size;
        success = true;
    }
    return success;
}
```

## Fig 3.3 栈

当数据必须以与写入相反的顺序读取时，栈是一种高效的存储方式，即最近写入的元素是第一个被读取的。

栈对于以与写入相反的顺序读取数据很有用；它们可用于回滚事件并将应用程序返回到早期状态——许多桌面软件包中的“撤销”和“后退”操作就是常见示例。这种行为对于实现诊断功能也很有用，因为在出现意外行为时，最近的事件通常最引人关注。这也对实现某些类型的数据解析和搜索算法很重要。

## 队列

与栈不同，队列是先进先出（FIFO）数据结构（在调度算法的上下文中也称为先来先服务，FCFS）；只有在所有先前写入的元素都被读取后，最近写入的元素才能从队列中读取。与栈类似，从队列中读取元素也会将其从队列中移除。写入和读取操作通常称为入队（enqueue）和出队（dequeue）。队列是一种常用的缓冲区实现，特别是在需要在异步任务之间共享数据时；例如，管理 UART 的中断服务例程在接收数据时可以将数据写入队列，以便主应用程序在需要时读取，而不是立即处理。队列对于实现某些类型的任务调度器也很有用。

队列可以以多种方式高效实现；双向链表天然适合实现队列（以及双端队列），尽管最简单的实现可能是使用循环缓冲区并存储读写索引以跟踪元素。循环缓冲区可以使用标准数组实现；通过计算数组索引对数组长度取模来实现元素环绕，使最后一个元素看起来与第一个元素相邻（取模运算符是 % 符号；因此，计算可以表示为 index % QUEUE_SIZE。如果缓冲区长度是 2 的幂，则可以将取模计算替换为单个按位与操作，使此实现更加高效。通过专用的入队和出队函数访问队列可确保索引得到维护，且访问始终有效。

```c
/* Implements a simple queue of 32-bit ints. */
static int32_t queue_data[QUEUE_SIZE];
static int queue_write_index = 0;
static int queue_read_index = 0;
/* Write data to the queue. Return true if there
 * is space in the queue and the write is
 * successful. */
bool write_queue(int32_t data)
{
    bool success = false;
    /* Check for space in the queue. Then write
     * the data, increment the index, wrapping if
     * necessary. */
    if (((QUEUE_SIZE + queue_read_index - 1) % QUEUE_SIZE) != queue_write_index)
    {
        queue_data[queue_write_index] = data;
        queue_write_index =
        (queue_write_index + 1) % QUEUE_SIZE;
        success = true;
    }
    return success;
}
/* Read data from the queue. Return true if the
 * queue contains some data to read. */
bool read_queue(int32_t * p_data)
{
    bool success = false;
```
