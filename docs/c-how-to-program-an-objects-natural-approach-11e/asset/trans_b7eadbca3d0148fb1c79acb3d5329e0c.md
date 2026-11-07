

### multiset 成员函数 find

第21–28行使用成员函数find（第22行），该函数可用于所有关联容器，用于搜索multiset中值15和20的首次出现位置。基于范围的for循环遍历{15, 20}中的每个项，这会创建一个initializer_list。函数find返回迭代器或const_iterator，具体取决于multiset是否为const。迭代器指向找到该值的位置。如果未找到该值，find返回一个与容器end成员函数返回值相等的迭代器或const_iterator。通常，当你需要使用指向已找到元素的迭代器时，你会使用find。在这里，我们本可以使用count成员函数——如果它返回0，则该项不在multiset中。

```cpp
20 // search for 15 and 20 in ints; find returns an iterator
21 for (int i : {15, 20}) {
22   if (auto result{ints.find(i)}; result != ints.end()) {
23     std::cout << std::format("Found {} in ints\n", i);
24   }
25   else {
26     std::cout << std::format("Did not find {} in ints\n", i);
27   }
28 }
29
```

```text
Found 15 in ints
Did not find 20 in ints
```

### multiset 成员函数 contains (C++20)

第31–38行使用C++20成员函数contains（第32行）来确定值15和20是否在multiset中。该函数可用于所有关联容器，返回一个bool值，指示该值是否存在于容器中。基于范围的for循环遍历{15, 20}中的每个项。

```cpp
30 // search for 15 and 20 in ints; contains returns a bool
31 for (int i : {15, 20}) {
32   if (ints.contains(i)) {
33     std::cout << std::format("Found {} in ints\n", i);
34   }
35   else {
36     std::cout << std::format("Did not find {} in ints\n", i);
37   }
38 }
39
```

```text
Found 15 in ints
Did not find 20 in ints
```

### 将另一个容器的元素插入到 multiset 中

第42行使用成员函数`insert`将vector的元素插入到multiset中，然后第44行将multiset的元素复制到标准输出。这些值按升序显示，因为multiset是一个有序容器，默认会按升序维护元素。在第44行，请注意下面的表达式：

```cpp
std::ostream_iterator<int>{std::cout, " "}
```

这会创建一个临时ostream_iterator并立即将其传给copy。我们选择这种方法是因为ostream_iterator在该示例中只使用一次。

```cpp
// insert elements of vector values into ints
const std::vector<int> values{ 7, 22, 9, 1, 18, 30, 100, 22, 85, 13};
ints.insert(values.cbegin(), values.end());
std::cout << "\nAfter insert, ints contains:\n";
std::ranges::copy(ints, std::ostream_iterator<int>{std::cout, " "});
```

```text
After insert, ints contains:
1 7 9 13 15 15 18 22 22 30 85 100
```

### multiset 成员函数 lower_bound 和 upper_bound

第49行使用lower_bound和upper_bound函数（可用于所有有序关联容器）来定位multiset中值22的第一次出现位置以及multiset中值22最后一次出现之后的元素。这两个函数返回指向相应位置的迭代器或const_iterator，如果值不在multiset中，则返回end迭代器。lower_bound和upper_bound共同表示包含值22的元素的范围。

```cpp
// determine lower and upper bound of 22 in ints
std::cout << std::format(
    "\nlower_bound(22): {}\nupper_bound(22): {}\n",
    *ints.lower_bound(22), *ints.upper_bound(22));
```

```text
lower_bound(22): 22
upper_bound(22): 30
```

### pair 对象与 multiset 成员函数 equal_range

multiset的equal_range函数返回一个pair，其中包含调用lower_bound和upper_bound的结果。pair将两个值关联起来。第52行创建并初始化一个名为p的pair对象。我们使用auto从初始化器推断变量的类型。equal_range返回的pair将包含两个迭代器或const_iterator，具体取决于multiset是否为const。pair包含两个公有数据成员first和second，它们的类型取决于pair的初始化器。

```cpp
// use equal_range to determine lower and upper bound of 22 in ints
auto p{ints.equal_range(22)};
std::cout << std::format(
    "lower_bound(22): {}\nupper_bound(22): {}\n",
    *(p.first), *(p.second));
}
```

```text
lower_bound(22): 22
upper_bound(22): 30
```

第52行使用equal_range确定multiset中22的lower_bound和upper_bound。第55行使用p.first和p.second访问lower_bound和upper_bound。我们解引用迭代器以输出equal_range返回的位置处的值。虽然这里我们没有这样做，但在解引用之前，你应该始终确保lower_bound和equal_range返回的迭代器不等于容器的end迭代器。

### 异构查找

在C++14之前，在关联容器中搜索键时，提供给find等搜索函数的参数必须具有容器的键类型。例如，如果键类型是string，你可以传递一个基于指针的字符串来在容器中定位。在这种情况下，参数会被转换为键类型（string）的临时对象，然后传递给find。在C++14及更高版本中，find（以及其他类似函数）的参数可以是任何类型，前提是有重载的比较运算符可以将参数类型的值与容器键类型的值进行比较。如果有，就不会创建临时对象。这被称为异构查找。

## 13.11.2 set 关联容器

**set关联容器**（来自头文件 **<set>**）用于快速存储和检索唯一键。set的实现与multiset相同，只是**set必须具有唯一键**。插入重复值时会被忽略。这是set在数学上的预期行为，因此不算作错误。set支持双向迭代器。如果键的顺序不重要，可以考虑**unordered_set**（头文件 **<unordered_set>**），但请注意它仅支持前向迭代器，且其键必须可哈希。

### 创建 set

图13.7演示了一个double类型的set。第10行使用**类模板实参推导（CTAD）**创建set，以推断元素类型。第10行等价于

```cpp
std::set<double, std::less<double>> doubles{2.1, 4.2, 9.5, 2.1, 3.7};
```

set的**initializer_list**构造函数将所有元素插入到set中。第14行使用**std::ranges**算法copy输出set的内容。注意，初始化列表中出现两次的值2.1在doubles中只出现了一次。再次强调，**set不允许重复**。

```cpp
1 // Fig13_07.cpp
2 // Standard Library set class template.
3 #include <algorithm>
4 #include <format>
5 #include <iostream>
6 #include <iterator> // ostream_iterator
7 #include <set>
8
9 int main() {
10    std::set doubles{2.1, 4.2, 9.5, 2.1, 3.7}; // CTAD
11
12    std::ostream_iterator<double> output{std::cout, " "};
13    std::cout << "doubles contains: ";
14    std::ranges::copy(doubles, output);
15 }
```

```text
doubles contains: 2.1 3.7 4.2 9.5
```

**图 13.7** | 标准库 set 类模板。

### 向 set 中插入新值

第19行定义并初始化一个pair，用于存储调用set成员函数`insert`的结果。该pair包含一个指向set中该项的`iterator`和一个`bool`，指示该项是否被插入——如果该项之前不在set中则为true，否则为`false`。在本例中，第19行使用函数`insert`将值13.8放入set中，并返回一个`pair`，其中`p.first`指向set中的值13.8，`p.second`为`true`，因为该值已被插入。

```cpp
16 // insert 13.8 in doubles; insert returns pair in which
17 // p.first represents location of 13.8 in doubles and
18 // p.second represents whether 13.8 was inserted
19 auto p{doubles.insert(13.8)}; // value not in set
20 std::cout << std::format("\n{} {} inserted\n", *(p.first),
21    (p.second ? "was" : "was not"));
22 std::cout << "doubles contains: ";
23 std::ranges::copy(doubles, output);
24
```

```text
13.8 was inserted
doubles contains: 2.1 3.7 4.2 9.5 13.8
```

### 向 set 中插入已有值

第26行尝试插入9.5，而该值已在set中。输出显示9.5未被插入，因为set不允许重复键。在这种情况下，返回的`pair`中的`p.first`指向set中已有的9.5，`p.second`为`false`。

