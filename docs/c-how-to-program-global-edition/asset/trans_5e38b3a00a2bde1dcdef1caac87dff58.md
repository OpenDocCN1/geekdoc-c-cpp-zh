
```c
// if character is found, remove it
if (delete(&startPtr, item)) { // remove item
    printf("%c deleted.\n", item);
    printList(startPtr);
} else {
    printf("%c not found.\n\n", item);
}
} else {
    puts("List is empty.\n");
}

break;
default:
    puts("Invalid choice.\n");
    instructions();
    break;
}

printf("%s", "? ");
scanf("%u", &choice);
}

puts("End of run.");
}

// display program instructions to user
void instructions(void)
{
    puts("Enter your choice:\n"
         " 1 to insert an element into the list.\n"
         " 2 to delete an element from the list.\n"
         " 3 to end.");
}

// insert a new value into the list in sorted order
void insert(ListNodePtr *sPtr, char value)
{
    ListNodePtr newPtr = malloc(sizeof(ListNode)); // create node

    if (newPtr != NULL) { // is space available?
        newPtr->data = value; // place value in node
        newPtr->nextPtr = NULL; // node does not link to another node

        ListNodePtr previousPtr = NULL;
        ListNodePtr currentPtr = *sPtr;

        // loop to find the correct location in the list
        while (currentPtr != NULL && value > currentPtr->data) {
            previousPtr = currentPtr; // walk to ...
            currentPtr = currentPtr->nextPtr; // ... next node
        }

101        // insert new node at beginning of list
102        if (previousPtr == NULL) {
103            newPtr->nextPtr = *sPtr;
104            *sPtr = newPtr;
105        }
106        else { // insert new node between previousPtr and currentPtr
107            previousPtr->nextPtr = newPtr;
108            newPtr->nextPtr = currentPtr;
109        }
110    }
111    else {
112        printf("%c not inserted. No memory available.\n", value);
113    }
114 }
115
116 // delete a list element
117 char delete(ListNodePtr *sPtr, char value)
118 {
119     // delete first node if a match is found
120     if (value == (*sPtr)->data) {
121         ListNodePtr tempPtr = *sPtr; // hold onto node being removed
122         *sPtr = (*sPtr)->nextPtr; // de-thread the node
123         free(tempPtr); // free the de-threaded node
124         return value;
125     }
126     else {
127         ListNodePtr previousPtr = *sPtr;
128         ListNodePtr currentPtr = (*sPtr)->nextPtr;

130         // loop to find the correct location in the list
131         while (currentPtr != NULL && currentPtr->data != value) {
132             previousPtr = currentPtr; // walk to ...
133             currentPtr = currentPtr->nextPtr; // ... next node
134         }
135
136         // delete node at currentPtr
137         if (currentPtr != NULL) {
138             ListNodePtr tempPtr = currentPtr;
139             previousPtr->nextPtr = currentPtr->nextPtr;
140             free(tempPtr);
141             return value;
142         }
143     }
144
145     return '\0';
146 }
147
148 // return 1 if the list is empty, 0 otherwise
149 int isEmpty(ListNodePtr sPtr)
150 {
151     return sPtr == NULL;
152 }
```

图 12.3 | 在列表中插入和删除节点。 (第 3 部分，共 4 部分。)

```c
154
155 // print the list
156 void printList(ListNodePtr currentPtr)
157 {
158    // if list is empty
159    if (isEmpty(currentPtr)) {
160       puts("List is empty.\n");
161    }
162    else {
163       puts("The list is:");
164
165       // while not the end of the list
166       while (currentPtr != NULL) {
167          printf("%c --> ", currentPtr->data);
168          currentPtr = currentPtr->nextPtr;
169       }
170
171       puts("NULL\n");
172    }
173 }
```

**图 12.3** | 在列表中插入和删除节点。 (第 4 部分，共 4 部分。)

```text
Enter your choice:
 1 to insert an element into the list.
 2 to delete an element from the list.
 3 to end.
? 1
Enter a character: B
The list is:
B --> NULL

? 1
Enter a character: A
The list is:
A --> B --> NULL

? 1
Enter a character: C
The list is:
A --> B --> C --> NULL

? 2
Enter character to be deleted: D
D not found.

? 2
Enter character to be deleted: B
B deleted.
The list is:
A --> C --> NULL
```

**图 12.4** | 图 12.3 程序的示例输出。 (第 1 部分，共 2 部分。)

```text
? 2
Enter character to be deleted: C
C deleted.
The list is:
A --> NULL
? 2
Enter character to be deleted: A
A deleted.
List is empty.
? 4
Invalid choice.
Enter your choice:
 1 to insert an element into the list.
 2 to delete an element from the list.
 3 to end.
? 3
End of run.
```

图 12.4 | 图 12.3 程序的示例输出。 (第 2 部分，共 2 部分。)

链表的主要函数是 insert（第 85–115 行）和 delete（第 118–147 行）。函数 isEmpty（第 150–153 行）被称为谓词函数——它不会以任何方式改变列表；相反，它确定列表是否为空（即列表第一个节点的指针为 NULL）。如果列表为空，则返回 1；否则返回 0。 [注意：如果您使用的是符合 C99 标准的编译器，可以使用 _Bool 类型（第 4.10 节）而不是 int。] 函数 printList（第 156–173 行）打印列表。

### 12.4.1 函数 insert

字符按字母顺序插入列表中。函数 insert（第 85–115 行）接收列表的地址和要插入的字符。列表的地址在要在列表开头插入值时是必要的。提供地址使得可以通过引用调用来修改列表（即列表第一个节点的指针）。因为列表本身是一个指针（指向其第一个元素），传递其地址会创建一个指向指针的指针（即双重间接）。这是一个复杂的概念，需要仔细编程。插入字符到列表中的步骤如下（见图 12.5）：

- 1. 通过调用 malloc 创建一个节点，将分配的内存地址赋给 newPtr（第 87 行），将要插入的字符赋给 newPtr->data（第 90 行），并将 NULL 赋给 newPtr->nextPtr（第 91 行）。
- 2. 将 previousPtr 初始化为 NULL（第 93 行），将 currentPtr 初始化为 *sPtr（第 94 行）——指向列表开始的指针。指针 previousPtr 和 currentPtr 分别存储插入点之前和之后的节点位置。
- 3. 当 currentPtr 不为 NULL 且要插入的值大于 currentPtr->data 时（第 97 行），将 currentPtr 赋给 previousPtr（第 98 行），并使 currentPtr 前进到列表中的下一个节点（第 99 行）。这会定位该值的插入点。
- 4. 如果 previousPtr 为 NULL（第 103 行），则将新节点作为列表中的第一个插入（第 104–105 行）。将 *sPtr 赋给 newPtr->nextPtr（新节点的链接指向以前的第一个节点）并将 `newPtr` 赋给 `*sPtr`（`*sPtr` 指向新节点）。否则，如果 `previousPtr` 不为 NULL，则将新节点就地插入（第 108–109 行）。将 `newPtr` 赋给 `previousPtr->nextPtr`（前一个节点指向新节点）并将 `currentPtr` 赋给 `newPtr->nextPtr`（新节点的链接指向当前节点）。

### 错误预防提示 12.3

将 NULL 分配给新节点的链接成员。指针在使用前应进行初始化。

图 12.5 说明了将包含字符 'C' 的节点插入有序列表。图的部分 (a) 显示了插入前列表和新节点。图的部分 (b) 显示了插入新节点的结果。重新分配的指针为虚线箭头。为简单起见，我们使用 `void` 返回类型实现了函数 `insert`（以及本章中的其他类似函数）。函数 `malloc` 可能无法分配请求的内存。在这种情况下，最好让我们的 `insert` 函数返回一个状态，以指示操作是否成功。

![](img/bf54db922e6fa8319cba11069e785521_513_0.png)

**图 12.5** | 按顺序在列表中插入节点。

### 12.4.2 函数 delete

函数 delete（第 118–147 行）接收指向列表开始的指针的地址和要删除的字符。删除字符的步骤如下（见图 12.6）：
