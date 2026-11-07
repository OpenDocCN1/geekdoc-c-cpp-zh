
`<concepts>`、`<iterator>`、`<ranges>`、`<compare>` 和 `<random>`。我们将 `<concepts>` 头文件的 31 个概念划分为子类别——核心语言概念、比较概念、对象概念和可调用概念。许多概念的名称不言自明。有关每个概念的详细信息，请参见 cppreference.com 上相应头文件的页面。

### 74 个预定义 C++20 概念

**`<concepts>` 头文件核心语言概念**

|  |  |  |
|---|---|---|
| assignable_from | default_initializable | same_as |
| common_reference_with | derived_from | signed_integral |
| common_with | destructible | swappable |
| constructible_from | floating_point | swappable_with |
| convertible_to | integral | unsigned_integral |
| copy_constructible | move_constructible |  |

**`<concepts>` 头文件比较概念**

|  |  |  |
|---|---|---|
| equality_comparable | totally_ordered | totally_ordered_with |
| equality_comparable_with |  |  |

**`<concepts>` 头文件对象概念**

|  |  |  |
|---|---|---|
| copyable | regular | semi_regular |
| movable |  |  |

**`<concepts>` 头文件可调用概念**

|  |  |  |
|---|---|---|
| equivalence_relation | predicate | relation |
| invocable | regular_invocable | strict_weak_order |

**`<iterator>` 头文件概念**

|  |  |  |
|---|---|---|
| bidirectional_iterator | indirectly_copyable_storable | input_or_output_iterator |
| contiguous_iterator | indirectly_movable | mergeable |
| forward_iterator | indirectly_movable_storable | output_iterator |
| incrementable | indirectly_readable | permutable |
| indirect_binary_predicate | indirectly_regular_unary_invocable | random_access_iterator |
| indirect_equivalence_relation | indirectly_swappable | sentinel_for |
| indirect_strict_weak_order | indirectly_unary_invocable | sized_sentinel_for |
| indirect_unary_predicate | indirectly_writable | sortable |
| indirectly_comparable | input_iterator | weakly_incrementable |
| indirectly_copyable |  |  |

**`<ranges>` 头文件概念**

|  |  |  |
|---|---|---|
| bidirectional_range | forward_range | random_access_range |
| borrowed_range | input_range | sized_range |
| common_range | output_range | view |
| contiguous_range | range | viewable_range |

**`<compare>` 头文件概念**

|  |  |  |
|---|---|---|
| three_way_comparable | three_way_comparable_with |  |

**`<random>` 头文件概念**

|  |  |  |
|---|---|---|
| uniform_random_bit_generator |  |  |

## 15.5 类型特征

`<type_traits>` 头文件<sup>40</sup> 用于

- 在编译时测试类型是否具有各种特征，以及
- 基于这些特征生成模板代码。

例如，你可以检查一个类型是

- 像 `int` 这样的基础类型（使用类型特征 `std::is_fundamental`），还是
- 类类型（使用类型特征 `std::is_class`）

并使用不同的模板代码处理每种情况。后续每个 C++ 版本都添加了更多类型特征，少数已被弃用或移除。

### 在 C++20 之前使用类型特征

在概念出现之前，你会在无约束的模板定义中使用类型特征来检查类型实参是否满足模板的要求。与概念一样，这些检查在编译时执行，但*是在模板实例化期间*，通常会导致许多晦涩的错误消息。另一方面，编译器在*实例化模板之前*测试概念，通常比在无约束模板中使用类型特征产生更少、更精确的错误消息。

### C++20 预定义概念通常使用类型特征

C++20 概念通常基于类型特征实现。例如：

- 概念 `std::integral` 基于类型特征 `std::is_integral` 实现，
- 概念 `std::floating_point` 基于类型特征 `std::is_floating_point` 实现，以及
- 概念 `std::destructible` 基于类型特征 `std::is_nothrow_destructible` 实现。

### 演示类型特征

图 15.6 展示了与图 15.5 中概念对应的类型特征。

```cpp
1  // fig15_06.cpp
2  // Using type traits to test whether types are
3  // integral types, floating-point types or arithmetic types.
4  #include <format>
5  #include <iostream>
6  #include <string>
7  #include <type_traits>
```

**图 15.6** | 使用类型特征测试类型是否为整型、浮点型或算术类型。（第 1 部分，共 2 部分）

40. “标准库头文件 `<type_traits>`。” 访问于 2023 年 4 月 18 日。https://en.cppreference.com/w/cpp/header/type_traits。

### 按类别划分的类型特征（续）

| 类别 | 第 1 列 | 第 2 列 | 第 3 列 |
|---|---|---|---|
| **主要类型类别** | `is_void`<br>`is_null_pointer`<sup>14</sup><br>`is_integral`<br>`is_floating_point`<br>`is_array` | `is_enum`<br>`is_union`<br>`is_class`<br>`is_function`<br>`is_pointer` | `is_lvalue_reference`<br>`is_rvalue_reference`<br>`is_member_object_pointer`<br>`is_member_function_pointer` |
| **复合类型类别** | `is_fundamental`<br>`is_arithmetic`<br>`is_scalar` | `is_object`<br>`is_compound` | `is_reference`<br>`is_member_pointer` |
| **类型属性** | `has_unique_object_representations`<sup>17</sup><br>`is_const`<br>`is_volatile`<br>`is_trivial`<br>`is_trivially_copyable`<sup>17</sup> | `is_standard_layout`<br>`is_empty`<br>`is_polymorphic`<br>`is_abstract`<br>`is_final`<sup>14</sup><br>`is_aggregate`<sup>17</sup> | `is_signed`<br>`is_unsigned`<br>`is_bounded_array`<sup>20</sup><br>`is_unbounded_array`<sup>20</sup><br>`is_scoped_enum`<sup>23</sup> |
| **支持的操作** | `is_constructible`<br>`is_trivially_constructible`<br>`is_nothrow_constructible`<br>`is_default_constructible`<br>`is_trivially_default_constructible`<br>`is_nothrow_default_constructible`<br>`is_copy_constructible`<br>`is_trivially_copy_constructible`<br>`is_nothrow_copy_constructible` | `is_move_constructible`<br>`is_trivially_move_constructible`<br>`is_nothrow_move_constructible`<br>`is_assignable`<br>`is_trivially_assignable`<br>`is_nothrow_assignable`<br>`is_copy_assignable`<br>`is_trivially_copy_assignable`<br>`is_nothrow_copy_assignable`<br>`is_move_assignable` | `is_trivially_move_assignable`<br>`is_nothrow_move_assignable`<br>`is_destructible`<br>`is_trivially_destructible`<br>`is_nothrow_destructible`<br>`is_swappable_with`<sup>17</sup><br>`is_swappable`<sup>17</sup><br>`is_nothrow_swappable_with`<sup>17</sup><br>`is_nothrow_swappable`<sup>17</sup> |
| **属性查询** | `alignment_of` | `rank` | `extent` |
| **类型关系** | `is_same`<br>`is_base_of`<br>`is_convertible`<br>`is_nothrow_convertible`<sup>20</sup> | `is_layout_compatible`<sup>20</sup><br>`is_pointer_interconvertible_base_of`<sup>20</sup><br>`is_invocable`<sup>17</sup> | `is_invocable_r`<sup>17</sup><br>`is_nothrow_invocable`<sup>17</sup><br>`is_nothrow_invocable_r`<sup>17</sup> |
| **const-volatile 说明符** | `remove_cv`<br>`remove_const` | `remove_volatile`<br>`add_cv` | `add_const`<br>`add_volatile` |
| **引用** | `remove_reference` | `add_lvalue_reference` | `add_rvalue_reference` |
| **指针** | `remove_pointer` | `add_pointer` |  |
| **符号修饰符** | `make_signed` | `make_unsigned` |  |
| **数组** | `remove_extent` | `remove_all_extents` |  |
| **杂项变换** | `aligned_storage` | `conditional` | `underlying_type` |
|  | `aligned_union` | `common_type` | `invoke_result`<sup>17</sup> |
|  | `decay` | `common_reference`<sup>20</sup> | `void_t`<sup>17</sup> |
|  | `remove_cvref`<sup>20</sup> | `basic_common_reference`<sup>20</sup> | `type_identity`<sup>20</sup> |
|  | `enable_if` |  |  |
| **对特征的操作** | `conjunction`<sup>17</sup> | `disjunction`<sup>17</sup> | `negation`<sup>17</sup> |
| **函数** |  |  |  |
| **成员关系** | `is_pointer_interconvertible_with_class`<sup>20</sup> | `is_corresponding_member`<sup>20</sup> |  |

## 15.6 C++20 概念：深入探讨

既然我们已经介绍了如何通过 `requires` 子句和预定义概念来约束模板参数，接下来我们将创建一个自定义概念，它聚合两个预定义概念，并介绍概念的其他特性。

### 15.6.1 创建自定义概念

C++20 的预定义概念通常聚合多个约束，有时包括来自其他预定义概念的约束，实际上创建了一些开发者所称的类型类别。<sup>43</sup> 你也可以使用模板定义自己的自定义概念。让我们创建一个自定义概念，它聚合我们在图 15.5 中使用的预定义概念 `std::integral` 和 `std::floating_point`，以约束 multiply 函数模板：

```cpp
template<typename T>
concept Numeric = std::integral<T> || std::floating_point<T>;
```

概念以模板头开始，后面跟着

- C++20 关键字 `concept`，
- 概念名称（`Numeric`），
- 等号（`=`），以及
- 约束表达式（`std::integral<T> || std::floating_point<T>`）。

43. Inbal Levi，《C++20 元编程探索》，2020 年 9 月 29 日。访问于 2023 年 4 月 18 日。https://www.youtube.com/watch?v=XgrjjbKaIV8。

