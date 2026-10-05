

## 第 4 节 列表、栈与队列

是或否。这足以能够对记录数据库进行顺序搜索，并找到与给定键匹配的记录。然而，我们通常希望键能够定义一个全序（见第 2.1 节），这意味着我们可以判断两个键中哪一个更大。使用具有全序的键类型可以让数据库解释器有机会以一种更高效搜索的方式组织记录集合。例如，将记录按排序顺序存储在数组中，这允许进行二分查找。幸运的是，在实践中，记录的大多数字段都是具有自然全序的简单数据类型。例如，整数、浮点数、双精度浮点数和字符串都是全有序。对于天然多维的字段（例如三维空间中的点），我们希望利用其多维特性。这个问题在第 13.3 节中讨论。

图 4.28 显示了一个简单抽象字典类的定义。`insert` 和 `find` 方法是该类的核心。`insert` 方法接收一个记录并将其插入字典。`find` 方法接收一个键值并从字典中返回与提供的值匹配的记录。如果字典中有多个具有该键值的记录，则不要求返回哪一个。

`clear` 方法简单地重新初始化字典。`remove` 方法与 `find` 类似，不同之处它还会删除从字典返回的记录。如果字典中有多个匹配所需键的记录，不要求实际移除并返回哪一个。`size` 方法返回字典中的元素数量。

剩余的方法是 `removeAny`。它与 `remove` 类似，不同之处它不接收键值。相反，如果存在，它会从字典中移除一条任意记录。该方法的目的是允许用户能够遍历字典中的所有元素（当然，字典在此过程中将变为空）。如果没有 `removeAny` 方法，用户可能会获取到一条他恰且不知道其键的字典记录。有了 `removeAny` 方法，用户可以像下面的代码片段所示处理字典中的所有记录。

```
while (dict.size() > 0) {
  it = dict.removeAny();
  doSomething(it);
}
```

还有其他方法在遍历字典时可能看起来更自然，例如使用“first”和“next”函数。但并不是所有想要实现字典的数据结构都能够高效地执行“first”。例如，哈希表的实现无法高效地定位表中键值最小的记录。使用 `RemoveAny`，我们有了一个提供通用访问的机制。

```
// Dictionary 抽象类。
template <typename Key, typename E>
class Dictionary {
private:
    void operator=(const Dictionary&) {}
    Dictionary(const Dictionary&) {}

public:
    Dictionary() // 构造函数
    virtual ~Dictionary() {} // 基析构函数

    // 重新初始化字典
    virtual void clear() = 0;

    // 插入记录
    // k: 插入记录的键。
    // e: 插入的记录。
    virtual void insert(const Key& k, const E& e) = 0;

    // 移除并返回记录。
    // k: 要移除记录的键。
    // 返回: 匹配的记录。如果有多个记录匹配
    // 移除任意一个。如果不存在键为 "k" 的记录
    // 则返回 NULL。
    virtual E remove(const Key& k) = 0;

    // 从字典中移除并返回任意记录。
    // 返回: 移除的记录，如果不存在则返回 NULL。
    virtual E removeAny() = 0;

    // 返回: 匹配 "k" 的记录（如果不存在则返回 NULL）。
    // 如果有多个匹配，返回任意一个。
    // k: 要查找的记录的键
    virtual E find(const Key& k) const = 0;

    // 返回字典中的记录数。
    virtual int size() = 0;
};
```

图 4.28 简单字典的 ADT（抽象数据类型）。

```
// 带有 ID、姓名、地址字段简单的工资条目
class Payroll {
private:
    int ID;
    string name;
    string address;
public:
    // 构造函数
    Payroll(int inID, string inname, string inaddr) {
        ID = inID;
        name = inname;
        address = inaddr;
    }
    Payroll() {} // 析构函数
    // 本地数据成员访问函数
    int getID() { return ID; }
    string getName() { return name; }
    string getaddress() { return address; }
}
```

**图 4.29** 工资条记录实现。

给定一个特定类型的记录数据库存储，我们可能希望以多种方式搜索记录。例如，我们可能希望将工资记录存储在一个字典中，允许我们通过 ID 搜索，同时将相同的记录存储在第二个字典中，允许我们通过姓名搜索。

4.29 显示了工资条记录的实现。`Payroll` 类有多个字段，这些字段可以用搜索键。通过改变键的类型，并使用每条记录中的相应字段作为值，我们可以定义一个字典，其搜索键是 ID 字段，另一个搜索键是姓名字段，第三个搜索键是地址字段。图 4.30 显示了一个示例，其中 `Payroll` 对象存储在两个独立的字典中，一个使用 ID 作为键，另一个使用姓名作为键。

字典的基本操作是查找匹配给定键的记录。这引发了如何从记录中提取键的问题。我们希望字典实现能支持任意记录类型，因此我们需要一种足够通用的提取机制。一种方法是要求所有记录类型支持支持返回键值的特定方法。例如，在 Java 中可以使用 `Comparable` 接口来实现效果。遗憾的是，当同一个记录类型旨在存储在多个由不同字段键值的字典中时，这种方法不起作用。这在数据库应用中很典型。另一种更通用的方法是提供一个从记录中提取键的类。遗憾的是，

## 4.4 节 字典

```cpp
int main() {
    // IDdict 按 ID 组织工资记录
    IDdict<int, Payroll*> IDdict;
    // namedict 按姓名组织工资记录
    namedict<string, Payroll*> namedict;
    Payroll *fool1, *foof2, *findpool, *find2;

    fool1 = new Payroll(5, "Joe", "Anytown");
    fool2 = new Payroll(10, "John", "Mytown");

    IDdict.insert(fool1->getID(), footer1);
    IDdict.insert(footer2->getID(), footer2);
    namedict.insert(fool1->getName(), footer1);
    namedict.insert(footer2->getName(), footer2);

    findpool = IDdict.find(5);
    if (findpool != NULL) cout << findpool;
    else cout << "NULL ";
    find2 = namedict.find("John");
    if (find2 != NULL) cout << find2;
    else cout << "NULL ";
}
```

![](img/0ae21f56d72533acf0527c86ba21e1e6_157_0.png)

这种情况的一个例子出现在我们拥有一个描述图书馆书籍的记录字典时。此类记录的一个字段可能是主题关键词列表，其中典型的记录存储了几个关键词。我们的字典可以实现为按关键词排序的记录列表。如果一本书包含三个关键词，它将在列表中出现三次，每个关联的关键词出现一次。然而，给定记录，没有简单的方法可以确定列表中的哪一个关键词触发了该记录的出现。因此，我们无法编写一个从此类记录中提取键的函数。

