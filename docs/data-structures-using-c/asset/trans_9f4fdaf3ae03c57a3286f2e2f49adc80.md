

如果条目数量超过最小数量，则可以将其中一个移入父节点，并将父节点中的条目移入发生删除的叶节点。

图 13.9 显示了从图 13.8(b) 中删除叶节点 r 时的 B 树。

![](img/a99ec79093c067f0bed8f1086197950e_617_0.png)

图 13.9 删除 r 并将 s 移至父节点后的树

图 13.10 显示了删除 p 后的树。

![](img/a99ec79093c067f0bed8f1086197950e_617_1.png)

图 13.10 删除 p 后的树，s 向下移动，t 向上移动到父节点

如果相邻叶节点只有最小数量的条目，则可以将两个叶节点和父节点中的中位条目合并为一个新叶节点，该新叶节点将包含不超过允许的最大条目数量。

如有需要，该过程将重复。

从图 13.10 的 B 树中删除叶节点 d。删除和合并过程如图 13.11(a)-(c) 所示。

![](img/a99ec79093c067f0bed8f1086197950e_617_2.png)

![](img/a99ec79093c067f0bed8f1086197950e_618_0.png)

![](img/a99ec79093c067f0bed8f1086197950e_618_1.png)

图 13.11 删除和合并操作（a）删除节点 d（b）合并（c）最终 B 树

这是删除 d 后的最终 B 树。合并过程重复了两次。

让我们看看如何使用 C++ 实现删除操作，如程序代码 13.8 所示。

### PROGRAM CODE 13.8
```
// DeleteBtree() deletes targetkey from the B-tree and
// returns the root
btree *btree :: del(int key, btree *root)
{
    bnode *oldroot;
    del_node(key, root);
    if(root->count == 0)
    {
        oldroot = root;
        root = root->child[0];
        delete oldroot;
    }
    return root;
}
```

在程序代码 13.9 中，del_node() 在 *当前节点* 中搜索目标键。如果找到且该节点是叶节点，则找到该键的直接后继并将其放入当前节点，并删除后继。删除后，该函数检查相应节点中是否仍有足够的条目，如果没有，则按需要移动条目。

```
void btree :: del_node(int key, btnode *curr)
{
    int pos;
    if(!curr)
    {
        cout << "\nTarget Not Found";
        return ;
    }
    else
    {
        if(search_node(key, curr, &pos))
        {
            if(curr->child[pos - 1])
            {
                /* targetkey found, replace data [pos] by
                it successor */
                successor(curr, pos);
                del_node(curr->data[pos], curr->child[pos]);
            }
            else
                remove_key(curr,pos); /* removes key from
                pos of *current */
        }
        else /* Target key not found in the current
        node, search a subtree */
        del_node(key, curr->child[pos]);
        if(curr->child[pos])
        {
            if(curr->child[pos]->count < min)
                restore(curr, pos);
        }
    }
}
```

remove_key() 函数从 *当前节点* 的 pos 位置删除目标键，并将剩余键向前移动一个位置。该操作的实现如程序代码 13.10 所示。

### PROGRAM CODE 13.10
```
void btree :: remove_key (btnode *curr, int pos)
{
int p;
for(p = pos + 1; p <= curr->count; p++)
{
curr->data[p - 1] = curr->data[p];
curr->child[p - 1] = curr->child[p];
}
curr->count--;
}

void btree :: successor (btnode *curr, int pos)
{
btnode *leaf;
leaf = curr->child[pos];
while(leaf->child[0])
leaf = leaf->child[0];
curr->data[pos] = leaf->data[1];
}
```

restore() 函数恢复最小条目数量。它首先搜索左侧兄弟节点以获取一个条目，只有在左侧兄弟节点没有多余条目时才使用右侧兄弟节点。其工作原理如程序代码 13.11 所示，使用了 restore() 函数。

### PROGRAM CODE 13.11
```
void btree :: restore (btnode *curr, int pos)
{
if(pos == 0) /* leftmost key */
{
if(curr->child[1]->count > min)
move_left(curr, 1);
else
combine_nodes(curr, 1);
}
else if(pos == curr->count)
{
if(curr->child[pos - 1]->count > min)
move_right(curr, pos);
else
combine_nodes(curr, pos);
}
else if(curr->child[pos - 1]->count > min)
    move_right(curr, pos);
else if(curr->child[pos + 1]->count > min)
    move_left(curr, pos + 1);
else
    combine_nodes(curr, pos);
}
```

图 13.12 显示了 move_right() 函数的工作原理。

![](img/a99ec79093c067f0bed8f1086197950e_621_0.png)

图 13.12 向右移动函数

程序代码 13.12 中的 move_right() 函数将数据从 *当前节点* 移入 child[pos]，然后将 child[pos - 1] 中的最右侧数据移入当前节点。

### PROGRAM CODE 13.12
```
void btree :: move_right (btnode *curr, int pos)
{
    int p;
    btnode *temp;
    /* Set temp to right node of current */
    temp = curr->child[pos];
    for(p = temp->count; p > 0; p--)
    {
        /* Shift all keys in the right node one position
        ahead */
        temp->data[p + 1] = temp->data[p];
        temp->child[p + 1] = temp->child[p];
    }
    temp->child[1] = temp->child[0];
    /* Increase count of right node */
    temp->count++;
    /* Move data from current to first place of right
    node */
    temp->data[1] = curr->data[pos];
    temp = curr->child[pos - 1];
    /* Move last data from left node into current */
    curr->data[pos] = temp->data[temp->count];
    curr->child[pos]->child[0] = temp->child[temp->count];
    /* Decrease count of left node */
    temp->count--;
}
```

同样，我们可以编写程序代码 13.13 中给出的 move_left() 函数，它将数据从 *当前节点* 移入 child[pos - 1]，然后将 child[pos] 中的最左侧条目移入 *当前节点*。

### PROGRAM CODE 13.13
```
void btree :: move_left (btnode *curr, int pos)
{
    int p;
    btnode *temp;
    temp = curr->child[pos - 1];
    /* Increase count of right node */
    /* * Move data from current into last place of left
    node and increase its count */
    temp->count++;
    temp->data[temp->count] = curr->data[pos];
    temp->child[temp->count] = curr->child[pos]->child[0];
    /* Set temp to right node of current */
    temp = curr->child[pos];
    /* * Move data from first place of right node
    into last place of current and decrease count of
    right node */
    curr->data[pos] = temp->data[1];
    temp->child[0] = temp->child[1];
    temp->count--;
    /* Shift all keys in right node one position left */
    for(p = 1; p <= temp->count; p++)
    {
        temp->data[p] = temp->data[p + 1];
        temp->child[p] = temp->child[p + 1];
    }
}
```

图 13.13 说明了节点的合并。

![](img/a99ec79093c067f0bed8f1086197950e_623_0.png)

图 13.13 合并节点

程序代码 13.14 详细说明了 combine_nodes() 函数的工作原理。

### PROGRAM CODE 13.14
```
void btree :: combine_nodes (btnode *curr, int pos)
{
    int p;
    btnode *left, *right;
    left = curr->child[pos - 1];
    right = curr->child[pos];
    /* Move data from current into left node and
    increase count of left, decrease count of current
    */
    left->count++;
    left->data[left->count] = curr->data[pos];
    left->child[left->count] = right->child[0];
    /* Copy all data and child pointers from right node
    into node */
    for(p = 1; p <= right->count; p++)
    {
        left->count++;
        left->data[left->count] = right->data[p];
        left->child[left->count] = right->child[p];
    }
    /* Delete the data from current which is moved into
    left node and shift the remaining data one position
    left */
    for(p = pos; p < curr->count; p++)
    {
        curr->data[p] = curr->data[p + 1];
        curr->child[p] = curr->child[p + 1];
    }
    curr->count--;
    delete right;
}
```

该函数将 *当前节点* 中 child[pos - 1] 和 child[pos] 处的相邻节点合并为一个节点。此外，*当前节点* 中 pos 处的数据被移入合并后的节点。

## 作为抽象数据类型的 B 树

我们已学习了 B 树的各种函数实现。作为 ADT 的 B 树在程序代码 13.15 中定义。

### PROGRAM CODE 13.15
```
/*****Implementation of B-tree*****/
#include<iostream.h>
#include<conio.h>
#include<stdio.h>
#include<process.h>
#define max 4
#define min 2
class btree
class qnode
{
    public:
    btnode* data;
    qnode* next;
    qnode(btnode* t) { data = t; next = NULL; }
};
class queue
{
    qnode* front;
    qnode* rear;

