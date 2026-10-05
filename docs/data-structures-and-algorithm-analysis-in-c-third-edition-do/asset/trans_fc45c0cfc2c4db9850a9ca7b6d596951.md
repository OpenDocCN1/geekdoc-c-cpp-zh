

526

第 16 章 算法模式

# head

![](img/0ae21f56d72533acf0527c86ba21e1e6_544_0.png)

(a)

# head

![](img/0ae21f56d72533acf0527c86ba21e1e6_544_1.png)

(b)

# head

![](img/0ae21f56d72533acf0527c86ba21e1e6_544_2.png)

(c)

**图 16.2** 跳跃表（Skip List）概念的图。(a) 一个简单的链表。(b) 通过为每隔一个节点添加额外的指针来增强列表。要找到键值为 62 的节点，我们访问值为 25、31、58 和 69 的节点，然后从键值为 58 的节点移动到键值为 62 的节点。(c) 理想的跳跃表，保证了 O(log n) 的搜索时间。要找到键值为 62 的节点，我们按照 31、69、58、69 最后是 62 的顺序访问节点。

```cpp
E find(const Key& k) const {
    SkipNode::Node * x = head; // Dummy header node
    for (int i=level; i>=0; i--){
        while (x->forward[i] != NULL &&
               k > x->forward[i]->k)
            x = x->forward[i];
    }
    x = x->forward[0]; // Move to实际记录，如果存在
    if (x != NULL && (k == x->key)) return x->data;
    return NULL;
}
```

**图 16.3** 跳跃表 **find** 函数的实现。

## 第 16.2 节 随机算法

```cpp
void insert(const Key &k, const E& it) {
    int i;
    SkipNode<Key, E> *x = head; // 从头节点开始
    int newLevel = randomLevel(); // 为新节点选择级别
    if (newLevel > level) // 新节点是列表中最深的
        AdjustHead(newLevel); // 向头节点添加空指针
        level = newLevel;
    }
    SkipNode<Key, E>* update[level+1]; // 跟踪层级边缘
    for (i=level; i>=0; i--) { // 查找插入位置
        while (x->forward[i] != NULL && (x->forward[i]->k < k))
            x = x->forward[i];
        update[i] = x; // 记录层级的末尾
    }
    x = new SkipNode<Key, E>(k, it, newLevel); // 新节点
    for (i=0; i<newLevel; i++) // 插入列表
        x->forward[i] = update[i]->forward[i]; // x 指向的地方
        update[i]->forward[i] = x; // 指向 x
    }
    recount++;
}
```

图 16.4 跳跃表插入的实现。

16.2(c) 中的理想跳跃表组织方式使得（假设不计算第一个和最后一个节点）一半的节点有一个指针，四分之一有两个指针，八分之一有三个，依此类推。这些间距是等距离的；实际上，这是一个“平衡”的跳跃表。在正常的插入和删除过程中，维护这种平衡是非常昂贵的。跳跃表的关键在于我们不需要担心其中任何一个问题。每当插入节点时，我们都会分配一个级别（即某些指针）。这种分配是随机的，使用几何分布，使得节点有 50% 的概率有一个指针，25% 的概率有两个指针，依此类推。以下函数根据这种分布确定级别：

```cpp
// 使用指数分布选择级别
int randomLevel(void) {
    int level = 0;
    while (random(2) == 0) level++;
    return level;
}
```

一旦确定了节点合适的级别，下一步是找到节点应该插入的位置，并在它在所有层级上以合适的方式将其连接起来。图 16.4 显示了向跳跃表插入新值的实现。16.5 举了跳跃表的插入过程。在这个例子中，我们首先向一个空跳跃表插入一个值为 10 的节点。假设 `randomLevel` 返回值为 1（即该节点位于级别 1，有 2 个指针）。因为空跳跃表没有节点，列表的级别（以及头节点的级别）必须设置为 1。插入新节点后生成图 16.5(a)所示的跳跃表。

接下来，插入值 20。假设这次 `randomLevel` 返回 0。跳跃表如图 16.5(b)所示。接下来，插入值 5。假设 `randomLevel` 返回 0。跳跃表如图 16.5(c)所示。接下来，插入值 2。假设 `randomLevel` 返回 3。跳跃表如图 16.5(d)所示。最后，在级别 2 插入一个值为 30 的节点。跳跃表如图 16.5(e)所示。

图 16.5 跳跃表插入图。(a) 插入初始值 10（级别 1）后的跳跃表。(b) 插入值 20（级别 0）后的跳跃表。(c) 插入值 5（级别 0）后的跳跃表。(d) 插入值 2（级别 3）后的跳跃表。(e) 插入值 30（级别 2）后的最终跳跃表。

![](img/0ae21f56d72533acf0527c86ba21e1e6_546_0.png)
![](img/0ae21f56d72533acf0527c86ba21e1e6_546_1.png)
![](img/0ae21f56d72533acf0527c86ba21e1e6_546_2.png)
![](img/0ae21f56d72533acf0527c86ba21e1e6_546_3.png)
![](img/0ae21f56d72533acf0527c86ba21e1e6_546_4.png)

