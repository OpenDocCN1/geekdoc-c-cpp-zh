

现在让我们更详细地了解这些非修改性序列操作。对于每个函数，讨论将展示其原型（可能不止一个），随后进行简要说明。成对的迭代器表示范围，所选的模板参数名表示迭代器的类型。通常，`[first,last)` 形式表示的范围从 `first` 开始，一直到 `last`（但不包括 `last`）。有些函数接受两个范围，这两个范围不必位于同一种容器中。例如，你可以使用 `equal()` 来比较 list 和 vector。作为参数传递的函数是函数对象，可以是指针（函数名就是此类指针的一个例子），也可以是定义了 `()` 操作的对象。与第 16 章一样，谓词是带一个参数的布尔函数，二元谓词是带两个参数的布尔函数。（这些函数不必是 `bool` 类型，只要它们对 false 返回 0，对 true 返回非零值即可。）

**表 G.13 — 非修改性序列操作**

| 函数 | 描述 |
|---|---|
| `all_of()` | 如果谓词测试对所有元素都为 true，则返回 true。(C++11) |
| `any_of()` | 如果谓词测试对任一元素为 true，则返回 true。(C++11) |
| `none_of()` | 如果谓词测试对所有元素都为 false，则返回 true。(C++11) |
| `for_each()` | 将非修改性函数对象应用于范围中的每个元素。 |
| `find()` | 在范围中查找值的第一次出现。 |
| `find_if()` | 在范围中查找满足谓词测试标准的第一个值。 |
| `find_if_not()` | 在范围中查找不满足谓词测试标准的第一个值。(C++11) |
| `find_end()` | 查找值与第二个序列的值匹配的子序列的最后一次出现。匹配可以通过相等性判断，也可以通过应用二元谓词实现。 |
| `find_first_of()` | 查找第二个序列中与第一个序列中的值匹配的任一元素的第一次出现。匹配可以通过相等性判断，也可以通过二元谓词求值。 |
| `adjacent_find()` | 查找与紧随其后的元素匹配的第一个元素。匹配可以通过相等性判断，也可以通过二元谓词求值。 |
| `count()` | 返回给定值在范围中出现的次数。 |
| `count_if()` | 返回给定值与范围中的值匹配的次数，匹配由一元谓词确定。 |
| `mismatch()` | 在第一个范围中查找与第二个范围中对应元素不匹配的第一个元素，并返回指向两者的迭代器。匹配可以通过相等性判断，也可以通过二元谓词求值。 |
| `equal()` | 如果第一个范围中的每个元素都与第二个范围中的对应元素匹配，则返回 `true`。匹配可以通过相等性判断，也可以通过二元谓词求值。 |
| `is_permutation()` | 如果第一个范围中的每个元素都与第二个范围的某个排列中的对应元素匹配，则返回 `true`。匹配可以通过相等性判断，也可以通过二元谓词求值。(C++11) |
| `search()` | 查找值与第二个序列的值匹配的子序列的第一次出现。匹配可以通过相等性判断，也可以通过应用二元谓词实现。 |
| `search_n()` | 查找由 `n` 个元素组成且每个元素都与给定值匹配的第一个子序列。匹配可以通过相等性判断，也可以通过应用二元谓词实现。 |

### all_of() (C++11)

```cpp
template<class InputIterator, class Predicate>
bool all_of(InputIterator first, InputIterator last,
            Predicate pred);
```

`all_of()` 函数对范围 `[first,last)` 中的每个迭代器，如果 `pred(*i)` 都为 `true`，或者该范围为空，则返回 `true`。否则函数返回 `false`。

### any_of() (C++11)

```cpp
template<class InputIterator, class Predicate>
bool any_of(InputIterator first, InputIterator last,
            Predicate pred);
```

`any_of()` 函数对范围 `[first,last)` 中的每个迭代器，如果 `pred(*i)` 都为 `false`，或者该范围为空，则返回 `false`。否则函数返回 `true`。

### none_of() (C++11)

```cpp
template<class InputIterator, class Predicate>
bool none_of(InputIterator first, InputIterator last,
             Predicate pred);
```

`none_of()` 函数对范围 `[first,last)` 中的每个迭代器，如果 `pred(*i)` 都为 `false`，或者该范围为空，则返回 `true`。否则函数返回 `false`。

### for_each()

```cpp
template<class InputIterator, class Function>
Function for_each(InputIterator first, InputIterator last,
                  Function f);
```

`for_each()` 函数将函数对象 f 应用于范围 [first,last) 中的每个元素。它还会返回 f。

### find()

```cpp
template<class InputIterator, class T>
InputIterator find(InputIterator first, InputIterator last,
                   const T& value);
```

`find()` 函数返回一个迭代器，指向范围 [first,last) 中第一个值为 value 的元素；如果未找到该项，则返回 last。

### find_if()

```cpp
template<class InputIterator, class Predicate>
InputIterator find_if(InputIterator first, InputIterator last,
                      Predicate pred);
```

`find_if()` 函数返回一个迭代器，指向范围 [first,last) 中第一个使函数对象调用 pred(*i) 为 true 的元素；如果未找到该项，则返回 last。

### find_if_not()

```cpp
template<class InputIterator, class Predicate>
InputIterator find_if_not(InputIterator first, InputIterator last,
                          Predicate pred);
```

`find_if_not()` 函数返回一个迭代器，指向范围 [first,last) 中第一个使函数对象调用 pred(*i) 为 false 的元素；如果未找到该项，则返回 last。

### find_end()

```cpp
template<class ForwardIterator1, class ForwardIterator2>
ForwardIterator1 find_end(
    ForwardIterator1 first1, ForwardIterator1 last1,
    ForwardIterator2 first2, ForwardIterator2 last2);

template<class ForwardIterator1, class ForwardIterator2,
    class BinaryPredicate>
ForwardIterator1 find_end(
    ForwardIterator1 first1, ForwardIterator1 last1,
    ForwardIterator2 first2, ForwardIterator2 last2,
    BinaryPredicate pred);
```

`find_end()` 函数返回一个迭代器，指向范围 [first1, last1) 中标记某个子序列起始位置的最后一个元素，该子序列与范围 [first2, last2) 的内容匹配。第一个版本使用值类型的 == 运算符来比较元素。第二个版本使用二元谓词函数对象 pred 来比较元素。也就是说，如果 `pred(*it1, *it2)` 为 true，则 it1 和 it2 指向的元素匹配。如果未找到该项，两者都返回 last1。

### find_first_of()

```cpp
template<class ForwardIterator1, class ForwardIterator2>
ForwardIterator1 find_first_of(
        ForwardIterator1 first1, ForwardIterator1 last1,
        ForwardIterator2 first2, ForwardIterator2 last2);

template<class ForwardIterator1, class ForwardIterator2,
        class BinaryPredicate>
ForwardIterator1 find_first_of(
        ForwardIterator1 first1, ForwardIterator1 last1,
        ForwardIterator2 first2, ForwardIterator2 last2,
        BinaryPredicate pred);
```

`find_first_of()` 函数返回一个迭代器，指向范围 [first1, last1) 中与范围 [first2, last2) 中任何元素匹配的第一个元素。第一个版本使用值类型的 == 运算符来比较元素。第二个版本使用二元谓词函数对象 pred 来比较元素。也就是说，如果 `pred(*it1, *it2)` 为 true，则 it1 和 it2 指向的元素匹配。如果未找到该项，两者都返回 last1。

### adjacent_find()

```cpp
template<class ForwardIterator>
ForwardIterator adjacent_find(ForwardIterator first,
                              ForwardIterator last);

template<class ForwardIterator, class BinaryPredicate>
ForwardIterator adjacent_find(ForwardIterator first,
                              ForwardIterator last, BinaryPredicate pred);
```

`adjacent_find()` 函数返回一个迭代器，指向范围 [first,last) 中与下一个元素匹配的第一个元素。如果找不到这样的元素对，函数返回 last。第一个版本使用值类型的 == 运算符来比较元素。第二个版本使用二元谓词函数对象 pred 来比较元素。也就是说，如果 `pred(*it1, *it2)` 为 true，则 it1 和 it2 指向的元素匹配。

