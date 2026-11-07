

## 修改序列算法

图 16.17 展示了许多**修改序列算法**——即修改它们所操作的容器的算法。C++11 中新增的算法在图 16.17–16.20 中以 * 标记。本章介绍的算法以**粗体**显示。

![](img/b42ba5cd262b1358d16610173f975e4d_766_0.png)

| 来自头文件 `<algorithm>` 的修改序列算法 |  |  |  |
| --- | --- | --- | --- |
| **`copy`** | **`copy_n*`** | **`copy_if*`** | **`copy_backward`** |
| `move*` | `move_backward*` | **`swap`** | **`swap_ranges`** |
| **`iter_swap`** | **`transform`** | **`replace`** | **`replace_if`** |
| **`replace_copy`** | **`replace_copy_if`** | **`fill`** | **`fill_n`** |
| **`generate`** | **`generate_n`** | **`remove`** | **`remove_if`** |
| **`remove_copy`** | **`remove_copy_if`** | **`unique`** | **`unique_copy`** |
| **`reverse`** | **`reverse_copy`** | **`rotate`** | **`rotate_copy`** |
| **`random_shuffle`** | `shuffle*` | **`is_partitioned*`** | **`partition`** |
| **`stable_partition`** | **`partition_copy*`** | **`partition_point*`** |  |

**图 16.17** | 来自头文件 `<algorithm>` 的修改序列算法

## 非修改序列算法

图 16.18 展示了**非修改序列算法**——即*不*修改它们所操作的容器的算法。

| 来自头文件 `<algorithm>` 的非修改序列算法 |  |  |  |
| --- | --- | --- | --- |
| **`all_of*`** | **`any_of*`** | **`none_of*`** | **`for_each`** |
| **`find`** | **`find_if`** | **`find_if_not*`** | **`find_end`** |
| **`find_first_of`** | **`adjacent_find`** | **`count`** | **`count_if`** |
| **`mismatch`** | **`equal`** | **`is_permutation*`** | **`search`** |
| **`search_n`** |  |  |  |

**图 16.18** | 来自头文件 `<algorithm>` 的非修改序列算法

## 排序及相关算法

图 16.19 展示了*排序及相关算法*。

| 来自头文件 `<algorithm>` 的排序及相关算法 |  |  |  |
| --- | --- | --- | --- |
| **`sort`** | **`stable_sort`** | **`partial_sort`** | **`partial_sort_copy`** |
| `is_sorted*` | `is_sorted_until*` | `nth_element` | `lower_bound` |
| `upper_bound` | `equal_range` | `binary_search` | `merge` |
| `inplace_merge` | `includes` | `set_union` | `set_intersection` |
| `set_difference` | `set_symmetric_difference` | `push_heap` | `pop_heap` |
| `make_heap` | `sort_heap` | `is_heap*` | `is_heap_until*` |
| `min` | `max` | `minmax*` | `min_element` |
| `max_element` | `minmax_element*` | `lexicographical_compare` | `next_permutation` |
| `prev_permutation` |  |  |  |

**图 16.19** | 来自头文件 `<algorithm>` 的排序及相关算法

## 数值算法

图 16.20 展示了头文件 `<numeric>` 中的数值算法。

| 来自头文件 `<numeric>` 的数值算法 |  |  |
| --- | --- | --- |
| `accumulate` | `partial_sum` | `iota*` |
| `inner_product` | `adjacent_difference` |  |

**图 16.20** | 来自头文件 `<numeric>` 的数值算法

## 16.7 本章小结

在本章中，我们演示了标准库中的许多算法，包括数学算法、基本的搜索和排序算法以及集合操作。你学习了每种算法所需的迭代器类型，并且了解了每种算法都可以与支持该算法所需的最低迭代器功能的任何容器一起使用。我们介绍了函数对象，它们在语法和语义上类似于普通函数，但具有性能和存储数据能力等优势。最后，你使用 lambda 表达式内联地创建函数对象，然后将它们传递给标准库算法。

我们在本书前面讨论数组时介绍了异常处理。在下一章中，我们将更深入地研究 C++ 丰富的异常处理功能。

## 小结

### 16.1 节 引言

- 标准库算法是执行常见数据操作（如搜索、排序以及比较元素或整个容器）的函数。

### 16.3.1 节 fill、fill_n、generate 和 generate_n

- 算法 fill 和 fill_n（第 693 页）将容器元素范围内的每个元素设置为特定值。
- 算法 generate 和 generate_n（第 693 页）使用生成器函数（第 693 页）或函数对象为容器元素范围内的每个元素创建值。

### 16.3.2 节 equal、mismatch 和 lexicographical_compare

- 算法 equal（第 696 页）比较两个值序列是否相等。
- 算法 mismatch（第 697 页）比较两个值序列，并返回一对迭代器，指示两个序列中不匹配元素的位置。
- 算法 lexicographical_compare（第 697 页）比较两个序列的内容。

### 16.3.3 节 remove、remove_if、remove_copy 和 remove_copy_if

- 算法 remove（第 699 页）消除某个范围内所有具有特定值的元素。
- 算法 remove_copy（第 699 页）复制某个范围内所有不具有特定值的元素。
- 算法 remove_if（第 699 页）删除某个范围内满足 if 条件的所有元素。
- 算法 remove_copy_if（第 700 页）复制某个范围内满足 if 条件的所有元素。

### 16.3.4 节 replace、replace_if、replace_copy 和 replace_copy_if

- 算法 replace（第 702 页）替换某个范围内所有具有特定值的元素。
- 算法 replace_copy（第 702 页）复制一个范围内的所有元素，并将一种值的所有元素替换为另一种值。
- 算法 replace_if（第 702 页）替换某个范围内满足 if 条件的所有元素。
- 算法 replace_copy_if（第 702 页）复制一个范围内的所有元素，并替换该范围内满足 if 条件的所有元素。

### 16.3.5 节 数学算法

- 算法 random_shuffle（第 704 页）随机重新排列某个范围内的元素。
- 算法 count（第 705 页）统计某个范围内具有特定值的元素个数。
- 算法 count_if（第 705 页）统计某个范围内满足 if 条件的元素个数。
- 算法 min_element（第 705 页）定位某个范围内最小的元素。
- 算法 max_element（第 705 页）定位某个范围内最大的元素。
- 算法 minmax_element（第 705 页）定位某个范围内最小和最大的元素。
- 算法 accumulate（第 705 页）对某个范围内的值求和。
- 算法 for_each（第 706 页）将普通函数或函数对象应用于范围内的每个元素。
- 算法 transform（第 706 页）将普通函数或函数对象应用于范围内的每个元素，并用函数的结果替换每个元素。

### 16.3.6 节 基本搜索和排序算法

- 算法 find（第 708 页）定位某个范围内的特定值。
- 算法 find_if（第 709 页）定位某个范围内第一个满足 if 条件的值。
- 算法 sort（第 709 页）按升序或谓词指定的顺序排列某个范围内的元素。
- 算法 binary_search（第 709 页）确定特定值是否在已排序的元素范围内。
- 算法 all_of（第 709 页）确定一元谓词函数是否对范围内的所有元素返回 true。
- 算法 any_of（第 709 页）确定一元谓词函数是否对范围内的任意元素返回 true。
- 算法 none_of（第 709 页）确定一元谓词函数是否对范围内的所有元素返回 false。
- 算法 find_if_not（第 710 页）定位某个范围内第一个不满足 if 条件的值。

### 16.3.7 节 swap、iter_swap 和 swap_ranges

- 算法 swap（第 711 页）交换两个值。
- 算法 iter_swap（第 711 页）交换两个迭代器参数所指向的两个元素。
- 算法 swap_ranges（第 711 页）交换某个范围内的元素。

### 16.3.8 节 copy_backward、merge、unique 和 reverse

- 算法 copy_backward（第 712 页）复制一个范围内的元素，并将这些元素从末尾开始向前放入容器。
- 算法 move（第 713 页）将一个范围内的元素从一个容器移动到另一个容器。
- 算法 move_backward（第 713 页）将一个范围内的元素从一个容器移动到另一个容器，从末尾开始向前移动。
- 算法 merge（第 713 页）将两个已按升序排列的值序列合并为第三个升序序列。
- 算法 unique（第 713 页）移除已排序序列中某个范围内的重复元素。
- 算法 copy_if（第 714 页）如果一元谓词函数对某个元素返回 true，则从该范围复制该元素。
- 算法 reverse（第 714 页）反转某个范围内的所有元素。
- 算法 copy_n（第 714 页）从指定位置开始复制指定数量的元素，并将它们放入从指定位置开始的容器中。

### 16.3.9 节 inplace_merge、unique_copy 和 reverse_copy

- 算法 inplace_merge（第 715 页）合并同一容器中两个已排序的元素子序列。
- 算法 unique_copy（第 715 页）复制某个范围内已排序值序列中的所有唯一元素。
- 算法 reverse_copy（第 715 页）生成某个范围内元素的逆序副本。

### 16.3.10 节 集合操作

- 集合算法 includes（第 717 页）比较两组已排序的值，以确定第二组中的每个元素是否都在第一组中。
- 集合算法 set_difference（第 718 页）找出第一组已排序值中不在第二组已排序值中的元素（两组值都必须按升序排列）。
- 集合算法 set_intersection（第 718 页）确定第一组已排序值中同时也出现在第二组已排序值中的元素（两组值都必须按升序排列）。
- 集合算法 set_symmetric_difference（第 718 页）确定第一组中不在第二组中的元素，以及第二组中不在第一组中的元素（两组值都必须按升序排列）。

