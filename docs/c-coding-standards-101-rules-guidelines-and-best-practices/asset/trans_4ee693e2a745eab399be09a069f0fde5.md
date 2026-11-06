

## 86. 使用正确的 STL 排序算法。

### 摘要

只需“适量排序”：理解每种排序算法的功能，并使用能满足需求的开销最低的算法。

### 讨论

你并不总是需要完整排序；通常你需要更少的排序，很少需要更多。一般来说，从开销最低到开销最高，标准排序算法选项有：`partition`、`stable_partition`、`nth_element`、`partial_sort`（及其变体 `partial_sort_copy`）、`sort` 和 `stable_sort`。使用能满足实际需求的开销最低的算法；使用更强大的算法是一种浪费。

`partition`、`stable_partition` 和 `nth_element` 在线性时间内运行，这很理想。

`nth_element`、`partial_sort`、`sort` 和 `stable_sort` 需要随机访问迭代器。如果你只有双向迭代器（例如 `list<T>::iterators`），则无法使用它们。如果你需要这些算法但没有随机访问迭代器，可考虑使用索引容器惯用法：创建一个支持随机访问迭代器的容器（例如 `vector`），其中存放指向你所拥有范围的迭代器，然后使用谓词的解引用版本（即在通常比较之前解引用迭代器的版本）对该容器应用更强大的算法。

仅当你需要保留相等元素的相对顺序时，才使用 `stable_...` 版本。注意 `partial_sort` 和 `nth_element` 不是稳定的（这意味着它们不会保持等价元素在排序前相同的相对顺序），并且它们没有标准化的稳定版本。如果你本想要这些算法，但又需要稳定性，那么你可能应该使用 `stable_sort`。

当然，如果并非必需，就不要使用任何排序算法：如果你使用标准关联容器（`set/multiset` 或 `map/multimap`）或 `priority_queue` 适配器，并且只需要一种排序顺序，那么容器中的元素会始终保持有序。

### 示例

*示例 1：`partition`。* 使用 `partition` 将范围分成两组：满足谓词的所有元素在前，不满足的所有元素在后。这就是你回答以下问题所需的全部：

- “所有成绩为 B+ 或更好的学生是谁？”例如，`partition( students.begin(), students.end(), GradeAtLeast("B+") );` 完成工作并返回指向第一个成绩低于 B+ 的学生的迭代器。
- “所有重量小于 10kg 的产品有哪些？”例如，`partition( products.begin(), products.end(), WeightUnder(10) );` 完成工作并返回指向第一个重量为 10kg 或更重的产品的迭代器。

*示例 2：`nth_element`。* 使用 `nth_element` 将单个元素放到如果范围完全排序时它应占据的第 n 个位置，并且所有其他元素正确地排在该第 n 个元素之前或之后。这就是你回答以下问题所需的全部：

- “谁是我最顶尖的 20 名销售员？”例如，`nth_element( s.begin(), s.begin()+19, s.end(), SalesRating );` 将最好的 20 个元素放到前面。
- “这批生产批次中质量中位数的物品是哪个？”该元素将位于排序范围的中间位置。要找到它，请执行 `nth_element( run.begin(), run.begin()+run.size()/2, run.end(), ItemQuality );`
- “质量位于第 75 百分位的物品是哪个？”该物品将位于排序范围的四分之一处。要找到它，请执行 `nth_element( run.begin(), run.begin()+run.size()*0.25, run.end(), ItemQuality );`

*示例 3：`partial_sort`。* `partial_sort` 完成 `nth_element` 的工作，并且第 n 个元素之前的元素均已按正确排序位置排列。使用 `partial_sort` 回答与 `nth_element` 类似的问题，但你需要匹配的元素已经排序（而不匹配的元素无需排序）。这就是你回答“谁是一、二、三等奖获得者？”这类问题所需的全部。例如，`partial_sort( contestants.begin(), contestants.begin()+3, contestants.end(), ScoreCompare );` 将前三名参赛者按顺序放在容器前面——仅此而已。

### 例外

尽管 `partial_sort` 通常比完整排序更快，因为它需要做的工作更少，但如果你要对范围的大部分（或全部）进行排序，它可能比完整的 `sort` 更慢。

### 参考文献

[Austen99] §13.1 • [Bentley00] §11 • [Josuttis99] §9.2.2 • [Meyers01] §3.1 • [Musser01] §5.4, §22.26 • [Stroustrup00] §17.1.4.1, §18.7

始终将谓词类型的 `operator()` 声明为 const 成员函数。这样，如果你试图修改谓词类型可能拥有的任何数据成员，编译器就会通过报错来帮助你避免这个错误。这不会阻止所有滥用——例如，它不会标记对全局数据的访问——但它至少能帮助编译器让你避免最常见的错误。

### 示例

*示例：`FlagNth`。* 以下是 [Sutter02] 中的经典示例，旨在从容器 v 中移除第三个元素：

```
class FlagNth {
public:
  FlagNth( size_t n ) : current_(0), n_(n) { }

  // evaluate to true if and only if this is the n-th invocation
  template<typename T>
  bool operator()( const T& ) { return ++current_ == n_; }    // bad: non-const

private:
  size_t current_, n_;
};

// ... later ...

v.erase( remove_if( v.begin(), v.end(), FlagNth(3) ) );
```

这不能保证移除第三个元素，尽管这是预期目的。在大多数实际的 STL 实现中，它会同时擦除第三个和第六个元素。为什么？因为 `remove_if` 通常是根据 `find_if` 和 `remove_copy_if` 实现的，并且它会将谓词的副本传递给这些函数，可能在此之前它已经自己做了一些影响谓词状态的工作。

从概念上讲，这个示例是反常的，因为 `remove_if` 只保证它会移除满足某个条件的所有元素。它没有说明范围内元素被访问或移除的顺序，因此代码依赖于一个假设的、但未记录且未被满足的假设。

移除特定元素的正确方法是迭代到该元素，然后调用 `erase`。

### 参考文献

[Austern99] §4.2.2 • [Josuttis99] §5.8.2, §8.1.4 • [Meyers01] §39 • [Stroustrup00] §10.2.6 • [Sutter02] §2-3

## 88. 更倾向于使用函数对象而非函数作为算法和比较器参数。

### 摘要

对象比函数更容易“即插即用”：更倾向于向算法传递函数对象，而非函数。关联容器的比较器必须是函数对象。函数对象是可适配的，而且与直觉相反，它们通常生成的代码比函数更快。

### 讨论

首先，函数对象易于使其可适配，并且始终应该如此（参见第 89 条）。即使你已有一个函数，有时你仍然必须用 `ptr_fun` 或 `mem_fun` 包装它以增加适配性。例如，为了使用绑定器构建更复杂的表达式，你必须这样做（另请参见第 84 条）：

```
inline bool IsHeavy( const Thing& ) { /*...*/ }
find_if( v.begin(), v.end(), not1( IsHeavy ) );          // error: isn’t adaptable
```

通常的解决方法是插入 `ptr_fun`（对于成员函数，使用 `mem_fun` 或 `mem_fun_ref`），但不幸的是，在这种特定情况下并不能正常工作：

```
inline bool IsHeavy( const Thing& ) { /*...*/ }
find_if( v.begin(), v.end(), not1( ptr_fun( IsHeavy ) ) );  // a valiant attempt
```

即使你显式指定了 `ptr_fun` 的模板参数，这仍然行不通，真是令人头疼。简而言之，问题在于 `ptr_fun` 准确推导出参数和返回类型（特别是参数类型被推导为 `const Thing&`），接着继续创建内部机制，这些机制在此过程中又善意地尝试添加另一个 `&`，而 ISO C++ 目前不允许引用的引用。有一些方法可以修复标准语言和/或库，从而使其正确工作（例如，允许引用的引用折叠为单个引用；或参见第 89 条），但目前标准尚未这样做。

如果你使用一个正确编写的函数对象（参见第 89 条），则无需记住这些东西，它从一开始就是可适配的，无需特殊语法：

```
struct IsHeavy : unary_function<Thing, bool> {
    bool operator()( const Thing& ) const { /*...*/ }
};
find_if( v.begin(), v.end(), not1( IsHeavy() ) );          // ok: adaptable
```

