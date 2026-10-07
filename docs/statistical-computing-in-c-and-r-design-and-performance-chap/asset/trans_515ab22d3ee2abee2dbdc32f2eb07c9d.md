
# 指针算术、迭代器与模板 383

```cpp
template <class Key, class Data> typename LTC<Key, Data>::iterator
    LTC<Key, Data>::begin() {
        return iterator(*this);
    }
```

```cpp
template <class Key, class Data> typename LTC<Key, Data>::iterator
    LTC<Key, Data>::end() {
        return iterator();
    }
```

`begin` 方法返回一个迭代器对象，其当前指针指向链表的头节点，而 `end` 则产生一个成员为空指针的迭代器对象。

LTC 类的 `push` 方法在接下来的列表中所示。

```cpp
template <class Key, class Data> void
    LTC<Key, Data>::push(const Data& data, const Key& key) {
    Node<Key, Data>* newNode = new Node<Key, Data>(data, key, Head);
    Head = newNode;
    Size++;
}
```

除了模板参数外，这只是链表的的 `push` 方法。它没有使用迭代器，因为不需要在类内部执行操作。相比之下，`lookup` 迭代器的衍生如下：

```cpp
template <class Key, class Data> typename LTC<Key, Data>::iterator
    LTC<Key, Data>::lookup(const Key& key) {
    iterator iter(*this);
    while (iter != end()) {
        if (iter->keyValue == key)
            return iter;
        iter++;
    }
    return 0;
    }
```

这具有列表类 `lookup` 方法的基本形式。不同的是，现在使用指向 `Node` 的指针来遍历链表的具体细节被封装在一个迭代器对象中。迭代器通过构造函数创建，该构造函数接受一个 `LTC` 对象作为参数，结果是当前成员指向头节点。它通过递增运算符在链表中移动，直到找到所需的键或到达末尾。与目标进行比较的键是通过对迭代器 `iter` 进行解引用获取的。

LTC 结构体的 `insert` 方法为：

```cpp
template <class Key, class Data> typename LTC<Key, Data>::iterator
    LTC<Key, Data>::insert(const Data& data, const Key& key) {
    const Key& key = key;
    if (lookup(key) == end()) //key 不存在
    iterator iter = lookup(key);
    if (iter != end()) {
        Node<Key, Data>* newNode = new Node<Key, Data>(data, key, iter->Next);
        newNode->Next = iter->Next;
        iter->Next = newNode;
    }
    Size++;
}
```

# 384 抽象数据结构

```cpp
return iter;
}
else{
    std::cout << "Key not found!" << std::endl;
    return end();
}
else{
    std::cout << "Duplicate key!" << std::endl;
    return end();
}
```

在大多数情况下，这重复了本节的主题，即 LTC 类的 `insert` 模拟了我们之前的 `LinkedList`，除了为了包含模板参数而进行的一些修改以及将指向 `Node` 对象的指针替换为迭代器之外。做了一处细小的调整，即在插入操作完成后，LTC 的 `insert` 方法返回一个指向插入处的迭代器。

现在让我们回到另一个迭代器：`const_iterator`。正如名称所示，该类提供了可以用于 `LTC` 对象只读访问的迭代器。为了理解这种类型迭代器的必要性，考虑下面 LTC 类构造函数的非操作实现。

```cpp
template <class Key, class Data> LTC<Key, Data>::LTC(const LTC<Key, Data>& L){
if(L.Size == 0){
    Head = 0;
    Size = 0;
}else{
    Size = L.Size;
    iterator iter;
    Node<Key, Data>* temp = 0;
    for(iter iter = L.begin(); iter != L.end(); iter++){
        if(temp == 0){
            Head = new Node<Key, Data>(iter->dataValue,
            iter->keyValue);
            temp = Head;
        }else{
            temp->Next = new Node<Key, Data>(iter->dataValue,
            iter->keyValue);
            temp = temp->Next;
        }
    }
    temp->Next = 0;//尾部节点的 Next 为空指针
}
```

解决方案是创建另一个可以访问但不能修改节点的迭代器类。受类似的 STL 概念启发，该类被命名为 `const_iterator`。

# 指针算术、迭代器与模板 385

用于比较和递增的基础迭代器类方法对于我们的新类将完美工作。因此，`const_iterator` 被制为 `iterator` 类的派生类。变化发生在解引用运算符上，它们现在的形式为：

```cpp
template <class Key, class Data> const Node<Key, Data>&
TCKey, Data>::const_iterator::operator*(){
    if(iterator::current != 0)
        return *iterator::current;
}
```

```cpp
template <class Key, class Data> const Node<Key, Data*>
TCKey, Data>::const_iterator::operator->(){
    if(iterator::current != 0)
        return iterator::current;
    else return;
}
```

这两个方法都被指定为 `const` 返回类型，禁止修改底层对象中的数据。除了这两个方法外，`begin` 和 `end` 方法的重载版本将返回 `const_iterator` 对象而不是 `iterator` 对象，即：

```cpp
template <class Key, class Data> typename LTC<Key, Data>::const_iterator
TCKey, Data>::begin() const {
    return const_iterator(*this);
}
```

```cpp
template <class Key, class Data> typename LTC<Key, Data>::const_iterator
TCKey, Data>::end() const {
    return const_iterator();
}
```

为了修复 LTC 构造函数，现在只需将之前的代码替换为 `const_iterator`；相同的基本原理适用于下方所示的赋值运算符。

```cpp
template <class Key, class Data> LTC<Key, Data>&
TCKey, Data>::operator=(const LTC<Key, Data>& L){
if(this == &L)
    return *this;
if(L.Head == 0){
    Head = 0; Size = 0;
    return *this;
}
Size = L.Size;
Node<Key, Data>* temp = 0;
for(const_iterator iter = L.begin(); iter!=L.end(); iter++){
    if(temp == 0){
        Head = new Node<Key, Data>(iter->dataValue,
        iter->keyValue);
        temp = Head;
    }else{
        temp->Next = new Node<Key, Data>(iter->dataValue,
        iter->keyValue);
        temp = temp->Next;
    }
}
temp->Next = 0;//尾部节点的 Next 为空指针
}
return *this;
}
```

# 402 抽象数据结构

```cpp
void f(const LTC<int, int>& L) {
    std::cout << L.Head->data << std::endl;
}

int main() {
    LTC<int, int> L;
    L.push(10, 1); L.push(20, 2); L.push(30, 3);
    L.push(40, 4); L.push(50, 5); L.push(60, 6);
    L.push(70, 7); L.push(80, 8); L.push(90, 9);
    L.push(100, 10);
    f(L);
    LTC<int, int> L2 = L;
    for (auto iter = L2.begin(); iter != L2.end(); ++iter) {
        std::cout << iter->keyValue << " " << iter->dataValue << std::endl;
    }
    LTC<int, int> L3 = L;
    L3.insert(250, 5);
    for (auto iter = L3.begin(); iter != L3.end(); ++iter) {
        std::cout << iter->keyValue << " " << iter->dataValue << std::endl;
    }
    LTC<int, int> L4 = L;
    L4.insert(250, 5);
    for (auto iter = L4.begin(); iter != L4.end(); ++iter) {
        std::cout << iter->keyValue << " " << iter->dataValue << std::endl;
    }
    return 0;
}
```

```解决方案是创建另一个可以访问但不能修改节点的迭代器类。受类似的 STL 概念启发，该类被命名为 const_iterator。

# 指针算术、迭代器与模板 385

基础迭代器类方法（用于比较和递增）对于我们的新类将完美工作。因此，const_iterator 被制为 iterator 类的派生类。变化发生在解引用运算符上，它们现在的形式为：

```cpp
template <class Key, class Data> const Node<Key, Data>&
TCKey, Data>::const_iterator::operator*(){
    if(iterator::current != 0)
        return *iterator::current;
}
```

```cpp
template <class Key, class Data> const Node<Key, Data*>
TCKey, Data>::const_iterator::operator->(){
    if(iterator::current != 0)
        return iterator::current;
    else return;
}
```

这两个方法都被指定为 const 返回类型，禁止修改底层对象中的数据。除了这两个方法外，`begin` 和 `end` 方法的重载版本将返回 const_iterator 对象而不是 iterator 对象，即：

```cpp
template <class Key, class Data> typename LTC<Key, Data>::const_iterator
TCKey, Data>::begin() const {
    return const_iterator(*this);
}
```

```cpp
template <class Key, class Data> typename LTC<Key, Data>::const_iterator
TCKey, Data>::end() const {
    return const_iterator();
}
```

为了修复 LTC 构造函数，现在只需将之前的代码替换为 const_iterator；相同的基本原理适用于下方所示的赋值运算符。

```cpp
template <class Key, class Data> LTC<Key, Data>&
TCKey, Data>::operator=(const LTC<Key, Data>& L){
if(this == &L)
    return *this;
if(L.Head == 0){
    Head = 0; Size = 0;
    return *this;
}
Size = L.Size;
Node<Key, Data>* temp = 0;
for(const_iterator iter = L.begin(); iter!=L.end(); iter++){
    if(temp == 0){
        Head = new Node<Key, Data>(iter->dataValue,
        iter->keyValue);
        temp = Head;
    }else{
        temp->Next = new Node<Key, Data>(iter->dataValue,
        iter->keyValue);
        temp = temp->Next;
    }
}
temp->Next = 0;//尾部节点的 Next 为空指针
}
return *this;
}
```

# 402 抽象数据结构

```cpp
void f(const LTC<int, int>& L) {
    std::cout << L.Head->data << std::endl;
}

int main() {
    LTC<int, int> L;
    L.push(10, 1); L.push(20, 2); L.push(30, 3);
    L.push(40, 4); L.push(50, 5); L.push(60, 6);
    L.push(70, 7); L.push(80, 8); L.push(90, 9);
    L.push(100, 10);
    f(L);
    LTC<int, int> L2 = L;
    for (auto iter = L2.begin(); iter != L2.end(); ++iter) {
        std::cout << iter->keyValue << " " << iter->dataValue << std::endl;
    }
    LTC<int, int> L3 = L;
    L3.insert(250, 5);
    for (auto iter = L3.begin(); iter != L3.end(); ++iter) {
        std::cout << iter->keyValue << " " << iter->dataValue << std::endl;
    }
    LTC<int, int> L4 = L;
    L4.insert(250, 5);
    for (auto iter = L4.begin(); iter != L4.end(); ++iter) {
        std::cout << iter->keyValue << " " << iter->dataValue << std::endl;
    }
    return 0;
}
```

```解决方案是创建另一个可以访问但不能修改节点的迭代器类。受类似的 STL 概念启发，该类被命名为 const_iterator。

# 9.6 练习

9.1. 写构造函数、析构函数和赋值运算符的定义，并通过示例 9.1 证明它们可以工作。

9.2. 编写一个程序，使用输入来处理不适当的索引并实现 []。

9.3. 为 Section 9.2 中的链表类编写 remove 和 clear 方法，以删除特定节点或移除所有节点。

9.4. 为了实现动态数组，让 dArray 类能够增长和收缩。当容器数量低于固定比例时，重命名 resize 方法为 grow 和 shrink。

9.5. 创建一个允许用户输入的 way，然后使用 push 方法实现 9.7。

9.6. 让 ai,...,an 是数组中的元素。考虑一种在每个递归层都均匀选择基元的随机化快速排序算法，假设 i < j 是任意一对索引。

- a) 证明在算法执行期间，ai 和 aj 被比较的期望次数为 2/(j-i)。
- b) 使用你在 a 部分的结果证明，如果元素是随机排列的，Section 9.2 中确定性快速排序的期望时间为 O(n log n)。

9.7. 为 Section 9.7 编写 C++ 代码，使用 9.1 中的递归合并。

9.8. 使用通用比较函数为 6.4 中的 gList 对象实现快速排序。

9.9. 证明当 n = 2^k 时，合并排序的最坏运行时间为 O(n log n)。

9.10. 为 Section 9.2.4 中的 hashTable 类编写拷贝构造函数和重载的 == 运算符。为什么这里需要 == 运算符？

9.11. 为 Section 9.2.2 中的链表类编写赋值运算符的代码。

9.12. 开发 Algorithm 9.5 的一个版本，在指定对象之前（即之前）向列表中插入对象。

9.13. 为 Section 9.2.2 中的链表添加一个 pop 方法，以移除并返回头节点。

9.14. 为链表类编写另一种 push 方法，通过将节点附加到列表尾部来构建列表。

9.15. 某些节点的访问比其他节点频繁。在这种情况下，可以通过将“热门”节点移动到列表头部使查找操作更高效。这种结果被称为自组织列表。创建一个自组织的链表类（Listing 9.2）。为了实现自组织属性，使用查找方法将具有键的节点移动到头部。

9.16. 证明在链式哈希表中，元素 a 的平均时间（对所有插入和查找操作排列取平均）是哈希到相同位置的元素数量的一半。

9.17. 双重哈希使用了两个函数 h1 和 h2，在开放寻址方案中第 i 次尝试用键填充空位是在 (h1(k) + ih2(k)) mod m 处进行的，其中 m 是表的大小。讨论这种方法的优缺点。特别是，你能预见到在什么情况下这种方法无法产生有效的探测序列？

