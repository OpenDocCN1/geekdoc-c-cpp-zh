
#include <iostream>

int main(int argc, char* argv[])

{

    int i;

    int length;

    int sum = 0;

    char char_array[10] = {'p', 's', 'y', 'c', 'h', 'o', 'o', 'g', 'y'}; // 为该数组分配的字节总数

    // 每个 char  own一个字节：元素数量 = 字节数

    length = sizeof(char_array);

    std::cout << "Size of array of characters is " << length << std::endl;

    for (int i = 0; i<length; i++)

        std::cout << char_array[i];

    std::cout << "\n";

    std::cout << "\n";

    std::cout << "\n";

    int numbers[10] = {1, 5, 9, 4, 2, 7, 6, 3, 8, 0};

    // 为该数组分配的字节总数。

    length = sizeof(numbers);

    std::cout << "Size of numbers array=" << length << std::endl;

    // 为数组分配的字节总数/每个元素分配的字节数

    length = sizeof(numbers) / sizeof(numbers[0]);

    std::cout << "Numbers of elements=" << length << std::endl; for (int i = 0;

    i<length; i++)

    {

        sum = sum + numbers[i];

        std::cout << "Sum of numbers=" << sum << std::endl;

    }

    int *p = numbers;

    std::cout << "Address of the first element is " << p << std::endl;

```
```cpp

std::cout << "The value in the address is " << *p << std::endl;

p++;将指针移动到下一个元素

std::cout << "Address of the second element is " << p << std::endl;

std::cout << "The value in the address is " << *p << std::endl;

int hold = 1;

std::cin >> hold;

return 0;

```
```

`sizeof` 函数返回数组分配的字节数。由于 `char` 数据类型占用一个字节，`sizeof` 返回的字节数等于元素的数量。整数数据类型占用 4 个字节，10 个整数存储在 40 个字节中。因此，`sizeof` `数组返回 40 个字节。

要计算数组中存储了多少元素，我们可以用整个数组分配的字节数除以每个元素分配的字节数；

```cpp

length=sizeof(numbers) / sizeof(numbers[0]);

40 / 4 = 10

```

要访问单个元素的值，必须使用数组索引。C++ 的索引从 0 开始。第一个元素的索引是 0，第二个元素的索引是 1，依此类推。

要访问数组的所有元素，必须使用 `for` 循环。

```cpp

for(i=0; i<length; i++)

cout<<char_array[i];

```

如果我们一个指针并将数组赋值给指针，指针将持有数组第一个元素的地址：

```cpp

int *p=numbers; cout<<"Address of the first element is "<<p<<endl;

```

使用指针访问数组第一个元素存储的值，运行以下行代码：

```cpp

cout<<"The value in the address is "<<*p<<std::endl;

```

代码的输出是：地址的值为1。要移动到数组的下一个元素，必须增加 `p`。现在它将指向数组的第二个元素：

```cpp

p++;

cout<<"Address of the second element is " <<p<<endl;

cout<<"The value in the address is "<<*p<<std::endl;

```

第二个元素的地址是 5。

## 字符串

## 字符串函数

我将向你展示如何使用字符串函数。

- `strcpy_s()` - 将字符串的内容复制到另一个字符串。
- `strcat_s()` - 将源字符串附加到目标字符串。
- `strlen()` - 返回字符串的长度。

我们的应用程序将从用户输入读取字符串，复制到另一个字符串，然后反序将原始字符复制到临时字符串。例如，如果用户输入“Concatenation”，应用程序将输出“noitanaceC”。

```cpp

main.cpp 中必须包含以下头文件：

#include "stdafx.h"

#include <stdio>

#include <cctype>

#include <iostream>

#include <cstring>

```

`<cstring>` 头文件用于字符串函数 `strcpy_s()`、`strcat_s()` 和 `strlen()`。`cctype` 头文件用于 `toupper()` 函数。

我想解释如何反序将字符从原始字符串复制到临时字符串。首先，我使用 `strlen()` 函数获取原始字符串的长度。

```cpp

length=strlen(aWord);

```

然后在循环中，我将原始字符串最后一个字符复制到临时字符串的第一个位置，依此类推。让我们检查循环中的代码。

```cpp

for(i=0; i<length; i++)

temp[i]=aWord[length-(i+1)];

```

如果用户输入单词“Concatenation”，单词长度将为 13。字符串第一个字符的索引是 0，那么最后一个字符的索引将是 12。这意味着最后一个字符的索引是 `length - 1`。

放在循环中的行代码是：

```cpp

temp[i]=aWord[length-(i+1)];

```

当 `i=0` 时，`temp[i]` 指临时字符串的第一个字符。同时（当 `i=0` 时），`aWord[length-(i+1)]` 指 `aWord[13] – (0 + 1)` 字符，即 `aWord[12]`，这是“Concatenation”字符串的最后一个字符。

当 `i=1` 时，`temp[1]` 指临时字符串的第二个字符，`aWord [length-(1+1)]` 指“Concatenation”字符串倒数第二个字符。这样，我们可以反序复制所有字符。

当我们从原始字符串复制所有字符到临时字符串时，我们需要在临时字符串末尾添加空字符，因为 C++ 中的字符串必须以空字符终止。

```cpp

代码行 temp[length]="0"; 将完成工作。

```

整个代码包含在 `visual_studio_2017.zip` 中。

```cpp

#include "stdafx.h"

#include <stdio>

#include <cctype>

#include <cstring>

#include <iostream>

int main()

{

    char more = 'Y';

    char prompt1[] = "\nEnter不超过20个字符的单词并按回车：\n";

    char prompt3[] = "\n你想继续吗？Y/N\n";

    char aWord[20];

    char aCopy[40]; int length = 0;

    char temp[20];

    int i;

    while (toupper(more) == 'Y')

    {

        std::cout << prompt1;

        std::cin >> aWord;

        std::cout << "aWord=" << aWord << std::endl;

}
```
```cpp

strcpy_s(aCopy, aWord);

std::cout << "aCopy" << aCopy << std::endl; length = strlen(aWord);

//fill temp[] array with the word characters in opposite order.

for (int i = 0; i<length; i++) {

    temp[i] = aWord[length - (i + 1)]; 

}

temp[length] = '\0';

std::cout << "Temp=" << temp << std::endl;

strcat_s(aCopy, temp);

std::cout << "aCopy after concatenation of temp=" << aCopy << std::endl;

std::cout << prompt3;

std::cin >> more;

}

return 0;

```

![](img/e2f3f34087ff6d96a5bbdf0800714545_188_0.png)

图 字符串操作。

## 列表

让我们想象一个谜题。你有一排盒子。每个盒子里有一张有一个字母的卡片。你必须弄出字母的顺序，使得这些字母组成一个单词。

| T | C | O | N | E | L | Y | G | O | H |
|---|---|---|---|---|---|---|---|---|---|
| 5 | 10| 6 | 3 | 2 | 9 | 1 | 7 | 8 | 4 |

图 A 链表

在上面的表格中，你可以看到每个盒子都有一个数字。你可能猜到这些数字是谜题的关键。第一个盒子正面有一个字母 T 和数字 5。取走带有字母 T 的卡片并把它放在一边。你会得到 'E'。数字 5 可能指向下一个字母。取走带有字母 E 的卡片并把它放在 T 旁边。你会得到 "TE"。字母 E 盒子侧面写有数字 2。所以，从第 2 个盒子取出卡片并把它放在 "TE" 旁边。你会得到 "TEC"

字母 C 盒子上的数字是 10，所以从第 10 个盒子取出卡片。你会得到 "TECH"。字母 H 盒子上的数字是 4，所以从第 4 个盒子取出卡片。你得到了 "TECHN"。继续按照数字寻找，你将得到整个单词：TECHNOLOGY。

这就是链表的工作原理。它由节点组成。每个节点至少有一个变量（文本、数字或对象）和一个存储下一个节点地址的变量（指针）。这个系统就像你在谜题中做的那样遍历节点列表。最后一个节点的指针具有空值（null），或者它可能指向第一个节点。

然后我们就有了一个环形链表。

## 添加节点

如果你想在链表的末尾添加一个新节点，你必须创建一个新节点。然后将最后一个节点的指针指向新节点的地址，并将新指针赋值为空（null）。

![](img/e2f3f34087ff6d96a5bbdf0800714545_190_0.png)

连接到链表的末尾。
如果你想在链表的开头添加一个新节点，你必须创建一个新节点。将新节点的指针指向第一个节点，即可。

![](img/e2f3f34087ff6d96a5bbdf0800714545_190_1.png)

连接到链表的头部。

如果你需要在链表的中间添加一个节点，你必须创建一个新节点，然后断开链：将节点（断开之前的节点）重定向到新节点，并将新节点的指针指向下一个节点（断开位置之后的节点）。

![](img/e2f3f34087ff6d96a5bbdf0800714545_190_2.png)

图 在链表的中间添加节点。

## 删除节点

要删除具有特定键（key）的节点，你沿着列表移动直到找到该键。然后将键节点赋值给 temp 节点。接着，将键节点之前的节点指向键节点的下一个节点。见图 60。结果是 temp 键从列表中孤立了。现在你可以删除 temp。

![](img/e2f3f34087ff6d96a5bbdf0800714545_191_0.png)

图 删除节点。

下面是 Node 类的代码。为了简单起见，我创建了一个包含整数和指向下一个节点指针的节点。两个类成员变量都声明为私有（private）。不使用全局变量是良好的编程习惯，因为私有成员从类的外部不可见。我们仍然需要设置和读取这些私有成员变量。公共函数 set 和 get 将完成这项工作。

## 第3 章：

二叉树

二叉树是所有基础数据结构中最实用的，而且到目前为止是最有趣的。它们是递归和指针工作的完美范例。二叉树是一种树结构，其中每个节点最多有两个孩子，称为左孩子和右孩子。

树的顶端节点称为根（root）。没有孩子的节点称为叶（leaves）。有一个孩子的节点称为内部节点。

二叉树可以执行许多操作：

- 插入：向树中添加新节点。
- 查找：在树中寻找特定值。
- 删除：从树中移除节点。
- 遍历：按照某种顺序访问树的所有节点。

二叉树遍历包括：

- 中序：访问左子树、根、然后右子树。
- 前序：访问根、左子树、然后右子树。
- 后序：访问左子树、右子树、然后根。

二叉树的一种常见类型是二叉搜索树（BST）。在 BST 中，对于任何节点，左子树的所有值都小于节点的值。

```

      10

     /  \

    5    15

   / \   / \

  2   7 12  20

```

二叉搜索树的属性允许高效的查找、插入和删除。这些操作平均时间复杂度为 O(log n)，其中 n 是树中的节点数。然而在最坏情况下，如果树变得不平衡，时间复杂度可能会变成 O(n)。为了防止树变得不平衡，存在自平衡二叉树，例如 AVL 树，其中任何节点的两个子子树的高度差不超过 1。另一种常见的自平衡树是红黑树，它使用颜色方案和一套规则在操作期间保持树的平衡。

二叉树被应用于许多领域，包括：

- 数据库索引
- 用于求值的表达式树
- 机器学习中的决策树
- 数据压缩算法（例如霍夫编码）




这是因为你可以按照你想要的方式构造内存。

## 实现二叉树

要实现一个二叉树，首先要声明节点结构：
```cpp

struct node

{

  int key_value;

  node *p_left; node *p_right;

}

```

该节点可以存储一个简单的整数 `key_value` 作为值，并有两个子节点——`p_left` 和 `p_right`。

你的二叉树中可能需要一些常用函数：插入、搜索、删除和销毁：

```cpp

node* insert(node* p_tree, int key);

node *search(node* p_tree, int key);

void destroyTree(node* p_tree);

node *remove(node* p_tree, int key);

```

## 插入

我们将使用递归算法将元素插入到树中。递归对于树来说是非常完美的，因为每棵树都包含两个更小的树；这使得整棵树在本质上是递归的。该函数接收一个键（key）和一个已经存在的树（即使是空的），并返回一个包含已插入值的新树。

```cpp

node* insert(node* p_tree, int key)

{

  // 基基础情况——我们到达了一个空树，我们的新节点

  // 需要插入到这里

  if ( p_tree == NULL )

  {

    node* p_new_tree = new node;

    p_new_tree->p_left = NULL;

    p_new_tree->p_right = NULL;

    p_new_tree->key_value = key;

    return p_new_tree;

  }

  // 决定——插入左子树还是右子树

  // 取决于节点的值

  if( key < p_tree->key_value )

  {

    // 从 p_tree->left 构建一个新树，并添加键

    // 将现有的 p_tree->left 指针替换为指向新节点的指针

    // 设置 p_tree->p_left 指针

    // 以防 p_tree->left 为空。（如果它不为空，// p_tree->p_left 不会

    // 改变，但这只是为了确保）。

    p_tree->p_left = insert( p_tree->p_left, key);

  }

  else

  {

    // 插入到右侧与插入到左侧是对称的

    p_tree->p_right = insert( p_tree->p_right, key);

    return p_tree;

  }

}
```
