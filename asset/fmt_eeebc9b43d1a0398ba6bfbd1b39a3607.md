
## 第10章 什么是树？

### 构造函数与析构函数

`BinarySearchTree` 类的构造函数将 `BinarySearchTree` 类的成员变量 `root` 初始化为 `NULL`。正如你在上一节中所回忆的，`root` 是元数据结构的实例，当节点被添加到树时，它指向二叉搜索树的根节点。

构造函数还将 `size` 成员初始化为 0。这意味着树上没有任何节点。每当向树插入一个新节点时，`size` 成员就会增加，当从树中删除一个节点时就会减少。你将在本章稍后部分看到这些步骤是如何实现的。

析构函数从树中移除所有节点并释放这些节点使用的内存。析构函数并不直接删除节点，而是调用 `removeAll()` 成员函数来实际处理删除节点和释放内存。

以下是 `BinarySearchTree` 类构造函数和析构函数的定义：

```cpp
BinarySearchTree() {
    root = NULL;
    size = 0;
}

~BinarySearchTree() {
    removeAll();
}
```

### add() 和 addNode()

你通过调用下一个代码段所示的 `BinarySearchTree` 类的 `add()` 成员函数向树添加节点。`add()` 函数需要两个参数：指向新节点键的指针和另一个指向节点值的指针。在示例中，我们称这些键为 `key` 和 `value`。

在节点被添加到树之前，`add()` 函数会验证 `key` 和 `value` 都不是 `NULL` 值。接下来，它会测试 `key` 和 `value` 的大小都不会超过为 `key` 分配的数组大小。它是通过比较 `key` 的长度和 `value` 的长度与 `#define` 预处理器定义的对应值来实现的。如果这些任何测试失败，`add()` 函数将向调用它的应用程序语句返回一个布尔值 `false`。

```cpp
bool add(char* key, char* value) {
    // (基于 OCR 上下文实现)
}
```
（注意：第207-208页的 OCR 内容严重损坏，已为了可读性进行了清理。）

### remove(), removeNode(), 和 removeRootNode()

从树中删除节点是一个多步过程，从应用程序调用 `remove()` 成员函数开始，如下一个代码段所示。`remove()` 函数需要被删除节点的键（key）。它调用了 `removeNode()` 成员函数。`removeNode()` 是 `BinarySearchTree` 类的一个私有成员，应用程序无法直接调用它。

`removeNode()` 函数需要两个参数。第一个是当前正在评估的节点的引用，搜索从这里开始。你通过传递树的根节点来开始搜索，随后的调用将传递子树的根。你必须将树看作一组子树的集合——每个节点都是其下方所有节点的根。第二个参数是 `remove()` 函数接收到的键。

```cpp
bool remove(char* key) {
    return removeNode(&root, key);
}
```

接下来的代码段所示，`removeNode()` 函数使用 `remove()` 函数传递的值来找到要删除的节点。搜索开始，`removeNode()` 确定传递给 `remove()` 的根节点是否为 `NULL`。如果这是函数的第一次调用，这可能是树的根，也可能是某个子树的根。如果是 `NULL`，则返回布尔值 `false`，因为没有找到节点。

如果根节点不是 `NULL`，搜索继续。`removeNode()` 函数的目标是在树中找到与 `remove()` 函数传递的键匹配的节点。一旦找到，包含该键的节点引用将被传递给 `removeRootNode()`，由它实际上从树中删除该节点。`removeRootNode()` 函数：

通过比较 `remove()` 函数传递的根节点的键开始搜索。如果键匹配，则将根节点传递给 `removeRootNode()` 函数，在该函数中删除该节点。`size` 数据成员减一，以反映从树中删除了一个节点。`removeNode()` 返回布尔值 `true`。

如果没有匹配，则 `removeNode()` 函数将确定根节点的键是否小于 `remove()` 函数传递的键。如果是，则 `removeNode()` 函数将左节点的键与 `remove()` 函数传递的键进行比较。`removeNode()` 函数会被递归调用，直到找到匹配，此时调用 `removeRootNode()` 函数并传递匹配节点的引用。

如果键大于根节点的键，则将根节点的右节点的键与该键进行比较。同样，`removeNode()` 函数会被递归调用，直到找到匹配，此时调用 `removeRootNode()` 函数并传递匹配节点的引用。

```cpp
bool removeNode(METADATA** node, char* key) {
    if (*node != NULL) {
        if (strcmp(key, (*node)->key) == 0) {
            removeRootNode(node);
            size--;
            return true;
        } else if (strcmp(key, (*node)->key) < 0) {
            return removeNode(&(*node)->left, key);
        } else {
            return removeNode(&(*node)->right, key);
        }
    } else {
        return false;
    }
}
```

`removeRootNode()` 成员函数是实际上将节点从树中移动的函数。“根节点”一词有时会令人困惑，因为你直觉上认为根节点是树上的第一个节点。实际上，任何节点都可以是其树中下方所有节点的根。即使该节点是一个叶子节点，它仍然是一个子树的根。只是这个子树恰好包含一个节点。因此，我们在函数名称中使用“根节点”。

`removeRootNode()` 函数需要一个参数，即指向要删除节点的指针。删除过程从声明一个指向元数据结构的指针开始。在接下来的代码示例中，我们将此指针命名为 `temp`。

在删除节点之前，`removeRootNode()` 函数确定该节点是否有右子节点和左子节点。如果左右子节点均为 `NULL`，则不存在子节点，并且会调用 `delete` 操作符来释放与该节点相关的内存。然后，父节点中的指针字段被设置为 `NULL`，因为该子节点已被删除。请注意，如果这是树中的唯一节点，这将把树的根设置为 `NULL`，这是合理的，因为树变为空。

如果其中一个不是 `NULL`，则将右节点与 `NULL` 进行比较。如果被删除的节点没有右节点，就是这种情况。在这种情况下，你将父节点中的指针字段指向被删除节点的左侧节点。根节点赋值给 `temp` 指针，以记住从树中移除节点的位置。接下来，将左节点分配给父节点。`delete` 操作符移除 `temp` 指针引用的节点，以释放与被删除节点相关的内存。

如果右节点不是 `NULL`，则 `removeRootNode()` 确定左节点是否为 `NULL`。逻辑与上一个示例类似，但被删除的节点没有左节点，因此父节点中的指针被设置为被删除节点的右侧节点。根节点的引用赋值给 `temp`。然后将根节点的引用赋值给父节点。随后，`delete` 操作符释放与移除的节点相关的内存。

最后也是最复杂的情况是被删除的节点既有左子节点又有右子节点。在这种情况下，`removeRootNode()` 调用 `moveLeftNode()` 函数并传递右节点的地址。

```cpp
void removeRootNode(METADATA** root) {
    METADATA* temp;

    if ((*root)->left == NULL && (*root)->right == NULL) {
        delete(*root);
        *root = NULL;
    } else if ((*root)->right == NULL) {
        temp = *root;
        *root = (*root)->left;
        delete(temp);
    } else if ((*root)->left == NULL) {
        temp = *root;
        *root = (*root)->right;
        delete(temp);
    } else {
        moveLeftNode(&(*root)->right, *root);
    }
}
```

`moveLeftNode()` 函数的目标是找到替换当前子树根的节点。为了实现这一目标，你必须向右移动并尽可能向下，直到找到右侧的节点。向右移动发生在第一次调用 `moveLeftNode()` 时。随后调用函数。当找到最小值，包含最小值的节点成为根节点。

让我们通过遍历 `moveLeftNode()` 函数的定义来看它是如何工作的。该函数需要两个参数：正在评估的节点和将替换的节点。记住，此函数会将右侧最小节点的键和值复制到被删除节点中。这会将被删除节点替换为叶子节点，然后删除该叶子节点。

如果被移动节点的引用不是 `NULL` 且节点的左指针为 `NULL`，则你找到了要移动到位置的节点。声明一个指针并赋值给该节点。接下来，将节点的键和值复制到根的键和值。在这种情况下，根节点是从树中移除的节点。由于你移动的是右子树的最左节点，该最左节点的右侧可能有节点。被移动节点的父节点的指针值被设置为被删除节点的右指针。这保持了这些子节点的完好。最后，`delete` 操作符移除节点。

如果你还没有找到右子树的最左节点，则再次调用 `moveLeftNode()`。这次，将左孩子作为要移动到根位置的节点传递进去。

```cpp
void moveLeftNode(METADATA** node, METADATA* root) {
    if (*node != NULL && (*node)->left == NULL) {
        METADATA* temp = *node;
        strcpy(root->key, (*node)->key);
        strcpy(root->value, (*node)->value);
        *node = (*node)->right;
        delete(temp);
    } else {
        moveLeftNode(&(*node)->left, root);
    }
}
```

### removeAll() 和 removeAllNodes()

上一节向你展示了几个从树中删除节点的函数。要执行此操作，你需要调用 `removeAll()` 函数。

下一个代码段展示了 `removeAll()` 函数，它执行了两个操作。首先，它调用了 `removeAllNodes()` 函数，该函数定义在 `BinarySearchTree` 类的私有访问修饰符中。第二个操作是重置 `BinarySearchTree` 类的 `root` 和 `size` 数据成员。`root` 实际上删除了树中的所有节点。它被设置为 `NULL`，表示树上没有任何节点。`size` 数据成员被设置为 0，表示树为空。`removeAll()` 函数也会被析构函数调用。

```cpp
void removeAll() {
    removeAllNodes(root);
    root = NULL;
    size = 0;
}
```

接下来显示的 `removeAllNodes()` 函数需要一个参数，即指向根节点的引用。只要根节点不是 `NULL`，`removeAllNodes()` 函数就会每次调用自身，并将左子节点和右子节点作为根节点传递。这些调用的顺序非常重要。记住，根节点要么是树的根，要么是子树的根。必须在删除父节点之前删除所有节点。递归处理左树，递归处理右树，然后当返回给调用者时，删除当前节点（根节点）就是安全的，因为所有子节点都已经被删除。对于所有递归函数，你都必须定义一个停止点。在这种情况下，如果你处于叶子节点，左指针和右指针将为 `NULL`，对 `removeAllNodes()` 的调用将返回（它们不会继续递归），因为节点将是 `NULL`。

屏幕上会显示一条消息，说明从树中删除的节点的键和值。然后使用 `delete` 操作符删除该节点。

```cpp
void removeAllNodes(METADATA* node) {
    if (node != NULL) {
        removeAllNodes(node->left);
        removeAllNodes(node->right);
        cout << "Removing node key: " << node->key << "\t"
             << node->value << endl;
        delete(node);
    }
}
```

### get() 和 getNode()

每当应用程序想要检索节点的值时，就会调用 `BinarySearchTree` 类的 `get()` 成员函数。要检索值，你必须为 `get()` 函数提供搜索键以及一个在找到键后用于存储值的变量。

以下是其工作原理。如下一个代码段所示，你传递一个搜索键的引用。在这个示例中，键是一个字符串。因此，你将 `get()` 函数指针传递给一个 `char`，该指针指向字符串的第一个字符。第二个参数也是一个 `char` 指针。它指向字符数组的第一个元素，`get()` 函数使用该数组来存储与搜索键关联的节点值。

假设搜索键是学生 ID "1234"，关联的值是 "Bob Smith"。你传递 `get() "1234"`，`get()` 函数将 "Bob Smith" 复制到树节点中找到键 "1234" 的节点所在的字符数组中。然后你可以在整个应用程序中使用该字符数组。

`get()` 函数定义在 `BinarySearchTree` 类的公共访问修饰符中，因此应用程序可以访问。然而，`get()` 函数简单地调用了定义在类私有访问修饰符中的 `getNode()` 成员函数。`getNode()` 函数在找到搜索键时返回布尔值 `true`；否则返回 `false`。该返回值也成为 `get()` 函数的返回值。

```cpp
bool get(char* key, char* value) {
    return getNode(root, key, value);
}
```

`getNode()` 函数是所有操作发生的地方。在这里进行搜索，并将节点的值复制到值数组中。如所示，`getNode()` 函数需要三个参数。第一个参数是指向根节点的引用。根节点是搜索的起点，通常是树的最顶端节点，但也可以是任何节点。第二个参数是搜索键的引用，在本示例中是一个 `char` 指针。第三个参数是存储包含搜索键的节点值的变量引用。搜索键和值数组与传递给 `get()` 函数的相同。

`getNode()` 开始验证根节点。如果根为 `NULL`，则 `value` 参数将为空字符串（它将第一个字符设置为 `NULL`），`getNode()` 函数将返回一个布尔值 `false`，表示树中未找到该键。

如果根不是 `NULL`，则继续搜索。`getNode()` 函数被递归调用。每次调用时，它都会比较搜索键与根节点的键。如果它们匹配，则将根节点的值复制到 `value` 变量，并返回布尔值 `true`。

如果搜索键与根节点的键不匹配，则 `getNode()` 函数将判断搜索键小于还是大于根节点的键。根据此比较的结果，`getNode()` 函数会调用自身并使用左节点或右节点。

```cpp
bool getNode(METADATA* node, char* key, char* value) {
    if (node == NULL) {
        value[0] = '\0';
        return false;
    }

    if (strcmp(key, node->key) == 0) {
        strcpy(value, node->value);
        return true;
    }

    if (strcmp(key, node->key) < 0) {
        return getNode(node->left, key, value);
    } else {
        return getNode(node->right, key, value);
    }
}
```

### contains() 和 containsNode()

```cpp
bool containsNode(METADATA* node, char* key) {
    if (node == NULL) {
        return false;
    }
    if (strcmp(key, node->key) == 0) {
        return true;
    }
    if (strcmp(key, node->key) < 0) {
        return containsNode(node->left, key);
    } else {
        return containsNode(node->right, key);
    }
}
```
