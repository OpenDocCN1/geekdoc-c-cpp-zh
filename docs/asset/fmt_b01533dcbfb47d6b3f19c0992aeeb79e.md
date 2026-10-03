
`const dynamicVector& operator+=(const dynamicVector&);`

`const dynamicVector& operator-=(const dynamicVector&);`

`const dynamicVector& operator*=(const T&);`

`const dynamicVector& operator/=(const T&);`

`dynamicVector` 类的块结束。

接下来，我们定义在上面类块中仅声明的函数。特别是下面定义的构造函数中，存储分量数组所需的内存是在初始化列表中使用 `new` 命令动态分配的：

# 第 17 章：动态向量与列表

```cpp
template<class T>
dynamicVector<T>::dynamicVector(
    int dim = 0, const T & a = 0)
    : dimension(dim), component(dim ? new T[dim] : 0){
    for(int i = 0; i < dim; i++)
    component[i] = a;
} // 构造函数
```

拷贝构造函数中使用了类似的方法：

```cpp
template<class T>
dynamicVector<T>::dynamicVector(const dynamicVector<T>& v)
    : dimension(v.dimension),
    component(v.dimension ? new T[v.dimension] : 0){
    for(int i = 0; i < v.dimension; i++)
    component[i] = v.component[i];
} // 拷贝构造函数
```

赋值运算符定义如下：

```cpp
template<class T>
dynamicVector<T>::operator=(const dynamicVector<T>& v){
```

然而，有一种情况赋值运算符需要什么都不做。这种情况是用户写了形如 `u = u` 的这种平凡的命令。为了排除这种情况，我们使用以下 `if` 问题判断：

```cpp
if(this != &v){
```

只有当当前动态向量与作为参数传递给函数的动态向量不同时，才会进入此 `if` 块，这确实是非平凡的情况，由编写形如 `u = v` 的有意义赋值命令的用户触发。一旦我们确保赋值运算符不会通过形如 `u = u` 的平凡调用触发，我们必须修改当前向量的维度，使其与参数向量 `v` 的维度一致：

```cpp
if(dimension != v.dimension)
    delete [] component;
    component = new T[v.dimension];
}
```

这样，数组 `component[]` 包含与数组 `v.component[]` 相同数量的条目，并准备好通过标准循环填充对应的值：

# 17.1 动态向量

```cpp
for(int i = 0; i < v.dimension; i++)
  component[i] = v.component[i];
  dimension = v.dimension;
}
return *this;
// 赋值运算符
```

完成了接收动态向量参数的赋值运算符的定义。接下来，我们还定义了另一个接收标量参数的赋值运算符，将相同的值赋予当前动态向量的所有分量：

```cpp
template<class T>
const dynamicVector<T>&operator=(const T& a){
for(int i = 0; i < dimension; i++)
  component[i] = a;
  return *this;
// 带标量参数的赋值运算符
```

此外，我们现在当前动态向量上实现了一些成员算术运算符：

```cpp
template<class T>
const dynamicVector<T>::operator+=(const dynamicVector<T>&v){
for(int i = 0; i < dimension; i++)
  component[i] += v[i];
  return *this;
// 将动态向量加到当前向量
```

通过此运算符，用户可以编写形如 `u = v` 的命令，其中 `u` 和 `v` 是相同维度的动态向量。

我们在这里没有验证参数向量的维度是否与当前向量相同。建议仔细的程序员在开始时确保这一点。上面的运算符现在用于添加两个动态向量：

```cpp
template<class T>
const dynamicVector<T>operator+(const dynamicVector<T>&u,
  const dynamicVector<T>&v){
}
```

# 第 17 章：动态向量与列表

通过此运算符，用户可以编写形如 `u = v` 的命令，其中 `u` 和 `v` 是相同维度的动态向量。接下来，我们实现一元运算符：

```cpp
template<class T>
const dynamicVector<T>operator-(const dynamicVector<T>&u){
  return u;
} // dynamicVector
```

通过此运算符，用户可以写 `-u` 来取负。最后，我们实现了一个将动态向量打印到屏幕的函数：

```cpp
template<class T>
void print(const dynamicVector<T>&v){
  printf("(");
  for(int i = 0; i < v.dim(); i++){
    printf("v[%d]=",i);
    print(v[i]);
  }
  printf("\n");
} // 打印动态向量
```

其他算术操作，如减法、标量乘和内积在练习中实现。假设它们已经可用，可以使用如下方式编写各种操作：

```cpp
int main(){
  dynamicVector<double> v(3,1.);
  dynamicVector<double> u;
  u=2.*v;
  printf("v:\n");
  print(v);
  printf("u:\n");
  print(u);
  printf("u+v:\n");
  print(u+v);
  printf("u-v:\n");
  print(u-v);
  printf("u*v=%f\n",u*v);
  return 0;
}
```

# 17.2 普通列表

上面的向量和动态向量是作为 `T` 组件数组实现的。根据定义，C（以及其他语言）中的数组必须包含相同类型和大小的条目。但在许多应用程序中，我们需要不同大小的序列。例如，我们可能需要实现不同维度的向量序列。这种序列无法用（甚至是动态）向量实现；需要更灵活的数据结构。

![](img/57402a72d6abfaa2dd5e70d5e16a53ab_379_0.png)

图 17.1 列表：箭头代表指针，符号代表类型 `T` 的对象（稍后将在编译时指定）。

所需的数据结构在下面的 `list` 中实现。该类包含一个指向 `T` 指针的数组，而不是 `T` 本身。虽然模板参数 `T` 必须在编译期间指定，但具体的 `T` 对象仅在运行时放置在数组中。例如，如果 `T` 在编译时指定为 `dynamicVector`，那么列表中的 `dynamicVector` 对象的维度仅在运行时指定。

# 第 17 章 动态向量与列表

列表的长度（数组中指向 `T` 的指针数量）也可以在运行时动态确定。事实上，在 `dynamicVector` 类中，有一个额外的整数字段用于存储列表中的项数。因此，`list` 类包含两个受保护的（protected）数据字段：`number` 用于指示列表中的项数，`item` 用于存储它们的地址。这些字段被声明为 `protected` 而不是 `private`（私有），以便稍后从派生类中访问它们。

```cpp
template<class T> class list{
protected:
    int number;
    T** item;
public:
```

第一个构造函数只接受一个整数参数 `n`，用于初始化列表中确定未来将包含的项数。如果 `n` 为 0，则不进行任何构造。（这也是默认情况）。另一方面，如果 `n` 不为 0，则使用 `new` 命令为 `n` 个指向 `T` 的指针分配足够的内存。这些指针尚未指向任何内容，它们不包含任何具体项的实际意义地址。

```cpp
list(int n=0):number(n), item(n ? new T*[n]):0{
    //构造函数
}
```

接下来，进入一个有意义的构造函数，它接受两个参数：`n` 用于指定构造列表中项的数量，`t` 用于用一个有意义的值初始化这些项。首先，`n` 像上面一样用于初始化列表，以为 `item`（地址数组）分配足够的内存。然后，在函数块中使用 `t`、`new` 命令和 `T` 类的拷贝构造函数来初始化列表中的项：

```cpp
list(int n, const T&t)
    :number(n), item(n ? new T*[n] : 0){
    for(int i=0; i<number; i++)
        item[i] = new T(t);
} // 带有 T 参数的拷贝构造函数
```

接下来，我们声明拷贝构造函数和赋值运算符。详细定义将推迟到以后。

```cpp
list(const list<T>&);
const list<T>& operator=(const list<T>&);
```

接下来，我们定义析构函数。首先，在标准循环中调用 `delete` 命令来删除列表中数组中的指针。一旦该指针被删除，就会隐式调用 `T` 类的析构函数来销毁它指向的项。一旦删除，这些指针将指向空，或包含无意义的（零）地址。尽管如此，它们仍然占据着宝贵的内存，应该将其释放供未来使用。为此，再次调用 `delete` 命令来删除整个指针数组：

```cpp
~list() {
    for(int i=0; i<number; i++)
        delete item[i];
    delete [] item; // 析构函数
}
```

由于 `number` 字段受保护的，因此无法从普通的（非成员、非友元）函数中读取。读取它的唯一方法是通过下面的公共 `size()` 函数：

```cpp
int size() const {
    return number;
} // 列表的大小
```

同样，列表中的项（地址存储在受保护的 `item` 中）只能通过下面的公共 `operator()`（用于读写）或 `operator[]`（只读）从普通函数访问：

```cpp
T& operator(int i) {
    if(item[i]) return *(item[i]);
} // 读写项

const T& operator[](int i) const {
    if(item[i]) return *(item[i]);
} // 只读项
```

用户应小心，仅对包含至少 `i` 项的列表 `l` 调用 `l(i)` 或 `l[i]`；否则可能会遇到错误。建议谨慎的程序员在这些运算符的开始验证 `i` 是否小于当前列表中的项数，如果不小于则发布错误消息。这些细节留作练习。

这结束了 `list` 类的块。`<class T>` 中声明的拷贝构造函数的定义与上面的构造函数相似：

```cpp
template<class T>
list(const list<T>& l) : number(l.number),
    item(l.number ? new T[l.number] : 0) {
    for(int i=0; i<l.number; i++)
        if(l.item[i])
            item[i] = new T(l.item[i]);
        else
            item[i] = 0;
} // 拷贝构造函数
```

这是上面声明的赋值运算符的定义：

```cpp
template<class T>
const list<T>&
list<T>::operator=(const list<T>& l) {
    if(this != &l){
        for(int i=0; i<number; i++)
            delete item[i];
        delete [] item;
        number = l.number;
        // 我们修改当前列表对象，使其包含与传递给函数的列表 'l' 相同数量的项
        item = new T*[number];
        for(int i=0; i<number; i++)
            if(l.item[i])
                item[i] = new T(l.item[i]);
            else
                item[i] = 0;
    }
    return *this;
} // 赋值运算符
```

## 17.2. 普通列表

## 17.3. 链表

## 17.4. 拷贝构造函数

链表中的第一个项可以被读取（尽管不修改），并且可以通过公共成员函数 `operator()` 在普通函数（非成员、非友元函数）的定义中使用：

```cpp
const T& operator() const {
    return item;
} // 读取 item 字段
```

事实上，通过这个运算符，用户可以编写 `l()` 来获取链表 `l` 中第一个项的引用。

同样，链表的其余部分可以通过以下公共函数读取（尽管不修改）：

```cpp
const linkedList* readNext() const {
    return next;
} // readNext
```

事实上，通过这个函数，用户可以编写 `l.readNext()` 来获取包含 `l` 的尾部项的链表地址。

接下来，我们声明了赋值运算符：

```cpp
const linkedList& operator=(const linkedList&);
```

该运算符将在稍后定义。

## 17.4 拷贝构造函数

链表的递归模式在下面定义的拷贝构造函数中特别有用。事实上，得益于这种模式，只需要拷贝链表中的第一个项（使用 `T` 类的拷贝构造函数），并使用递归来拷贝尾部：

```cpp
linkedList(const linkedList&l):item(l.item()),
    next(l.next ? new linkedList(*l.next):0){
} // 拷贝构造函数
```

事实上一切都在初始化列表中完成：首先，将 `l` 中的第一个项 `l()` 拷贝到构造列表的第一个项 `item` 中。然后，将 `l.next` 指向的 `l` 的尾部递归地拷贝到一个新的尾部，从而按要求将整个链表 `l` 拷贝到一个新的链表中。

## 17.5 析构函数

链表的递归结构在析构函数中同样有用。事实上，一旦删除指针 `next`，析构函数就会自动调用以递归销毁整个尾部。然后，`T` 类的析构函数被隐式调用以销毁第一个项 `item`：

```cpp
~linkedList(){
    delete next;
    next = 0;
} // 析构函数
```

## 17.6 递归成员函数

链表的递归模式也用于定义返回最后一个项（嵌入在一个仅有一个项的简单链表中）的函数：

```cpp
T& last() {
    return next ? next->last() : *this;
} // 最后一个项
```

事实上，通过对项的总数进行数学归纳法可以证明该函数返回最后一个项：如果项的总数为一，那么 `next` 必须是空指针，因此返回包含唯一项 `item` 的当前链表，符合要求。另一方面，如果项的总数大于一，那么归纳假设意味着返回了尾部中的最后一个项。该项也是原始链表中的最后一个项，符合要求。

类似的证明显示，以下函数统计了链表中项的总数：

```cpp
int length() const {
    return next ? next->length() + 1 : 1;
} // 项的数量
```

现在使用这两个函数来组成一个在链表末尾添加项的函数（即“在链表末尾追加一个项”）：

```cpp
void append(T& t) {
    last().next = new listItem(t);
} // 添加新项
```

## 17.7 插入新项

链表的递归结构在向其中插入新项时非常有用。以下函数将新项放置在链表第一个项之后：

```cpp
void insertNextItem(T&t){
  next = new linkedList(t,next);
} // 将项插入到第二个位置
```

上述命令行使用了第 17.3 节中的构造函数，将当前尾部替换为稍长的尾部，其开头包含新项 `t`，符合要求。

以下函数将新项放置在当前链表的开头：

```cpp
void insertFirstItem(T&t){
```

首先，使用第 17.3 节中的构造函数来复制第一个项 `item`：

```cpp
next = new linkedList(item,next);
```

现在，使用 `T` 类的赋值运算符将 `item` 的第一个拷贝替换为新项 `t`：
