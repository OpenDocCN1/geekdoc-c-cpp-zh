

```cpp
key[level] - 'a'; (!pCrawl->children[index]) = pCrawl->children[index];
(pCrawl != NULL && pCrawl->isEndOfWord); }
```

# 前缀匹配：

为了确定一个字符串是否是字典树中任何单词的前缀，我们执行搜索操作，但放宽对末节点 `isEndOfWord` 标记的要求。

```cpp
bool startsWith(TrieNode* root, const string prefix) { 
    int level, index, length = strlen(prefix); 
    pCrawl = root; 
    for (level = 0; level < length; level++) {
        index = prefix[level] - 'a';
        if (!pCrawl->children[index]) return false;
        pCrawl = pCrawl->children[index];
    }
    return true;
}
```

# 代码输出：

插入单词："hello", "world"
查找 "hello": 找到
查找 "world": 找到
查找 "trie": 未找到
检查前缀 "wo": 前缀存在

字典树高效地简化了字符串搜索、前缀检查和补全建议的过程，使其成为搜索引擎、文本编辑软件以及处理大型字符串数据集应用的理想选择。通过详细讨论和实际示例，本节阐明了字典树数据结构的机制及其在 C 语言编程中实现快速高效字符串搜索的关键作用。

3.9

# 空间数据结构：四叉树（Quad-Trees）与 KD 树

空间数据结构旨在高效地组织和查询多维空间中的数据。它们在计算机图形学、地理信息系统（GIS）和游戏开发等领域至关重要，这些领域经常需要搜索、插入和删除操作。在各种空间数据结构中，四叉树和 KD 树（k维树）因其独特的空间划分方法和快速搜索能力脱颖而出。本节将探索四叉树和 KD 树，详细介绍它们在 C 中的实现以及高效处理空间数据的应用。

# 四叉树：

四叉树是一种树数据结构，通过将二维空间递归地划分为四个象限或区域来划分空间。每个节点对应于空间的一部分，并有四个子节点。

# 四叉树节点结构：

```c
typedef struct QuadTreeNode {
    int x, y; // 点坐标
    struct QuadTreeNode* NW;
    struct QuadTreeNode* NE;
    struct QuadTreeNode* SW;
    struct QuadTreeNode* SE;
} QuadTreeNode;
```

# 四叉树中的插入：

插入涉及确定要插入节点的象限并递归向下执行。以下是一个简化的表示：

```c
void insertQuadTree(QuadTreeNode* root, int x, int y) {
    if (root == NULL) {
        createQuadTreeNode(x, y);
    } else // 确定象限
    if (x < root->x) {
        if (y < root->y) insertQuadTree(root->SW, x, y);
        else insertQuadTree(root->NW, x, y);
    } else {
        if (y < root->y) insertQuadTree(root->SE, x, y);
        else insertQuadTree(root->NE, x, y);
    }
}
```

# KD 树：

KD 树（k维树）将二叉搜索树推广到 k 空间，实现了高效的点定位、最近邻搜索和范围搜索。树的每个节点对应于一个维度，我们在沿着树向下移动时切换维度。

# KD 树节点结构：

```c
typedef struct KDTreeNode {
    int point[2]; // 假设为2D 空间
    struct KDTreeNode* left;
    struct KDTreeNode* right;
} KDTreeNode;
```

# KD 树中的插入：

插入根据点相对于当前维度的中位数在左或右之间切换。

```cpp
void insertKDTree(KDTNode* root, int point[], unsigned depth) {
    if (root == NULL) {
        createKDTreeNode(point);
    }
    int cd = depth % 2; // 当前维度
    if (point[cd] < root->point[cd])
        insertKDTree(root->left, point, depth+1);
    else
        insertKDTree(root->right, point, depth+1);
}
```

# 应用：

- 用于图像处理、GIS 和游戏中的碰撞检测，以高效管理空间对象。
- 用于最近邻搜索、范围搜索以及多维数据的快速浏览。

通过在 C 语言中实现四叉树和 KD 树，软件开发者可以更有效地处理空间数据，优化多维空间中的搜索、插入和删除操作。这些数据结构赋予了许多应用，从加速渲染到在地图服务中实现空间查询。

3.10

# 理解与实现布隆过滤器

布过滤器是一种空间高效的概率数据结构，提供了一种测试元素是否为集合成员的高效方法。布过滤器由 Burton Howard Bloom 于 1970 年提出，允许可能的假阳性匹配，但保证零假阴。这意味着它可能会错误地断言元素存在，但永远不会误报元素不存在。由于其高效性和低内存需求，布过滤器被广泛应用于网络流量过滤、拼写检查器和数据库缓存机制。

# 布隆过滤器的工作原理

布过滤器由一个初始化为零的位向量（位数组）和多个独立的哈希函数组成。每个元素通过多个函数映射到位向量。检查成员性时应用相同的哈希函数；如果所有对应的位都被设置为 1，则假设该元素在集合中，否则不在。

# 关键特性：

- 布隆过滤器比哈希表等其他数据结构更节省空间。
- 插入和查询操作非常高效。
- 布隆过滤器不支持删除元素。然而，计数布隆过滤器等变体解决了这个问题。

# 用 C 实现简单的布隆过滤器：

```c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

#define FILTER_SIZE 1024

typedef struct {
    unsigned char bits[FILTER_SIZE];
} BloomFilter;

unsigned int hash1(const char* key) {
    unsigned int hash = 0;
    while (*key) hash = hash * 31 + *key++;
    return hash % FILTER_SIZE;
}

unsigned int hash2(const char* key) {
    unsigned int hash = 0;
    while (*key) hash = hash * 37 + *key++;
    return hash % FILTER_SIZE;
}

void insert(BloomFilter* filter, const char* key) {
    unsigned int pos1 = hash1(key);
    unsigned int pos2 = hash2(key);
    filter->bits[pos1] = 1;
    filter->bits[pos2] = 1;
}

int query(BloomFilter* filter, const char* key) {
    unsigned int pos1 = hash1(key);
    unsigned int pos2 = hash2(key);
    return filter->bits[pos1] && filter->bits[pos2];
}

int main() {
    BloomFilter filter = {0};
    insert(&filter, "hello");
    insert(&filter, "world");
    printf("Query for 'hello': %d\n", query(&filter, "hello"));
    printf("Query for 'world': %d\n", query(&filter, "world"));
    printf("Query for 'bloom': %d\n", query(&filter, "bloom"));
    return 0;
}
```

