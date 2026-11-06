|  |  |  |
|---|---|---|
| `bidirectional_range` | `common_range` | `contiguous_range` |
| `forward_range` | `input_range` | `output_range` |
| `random_access_range` | `range` | `sized_range` |
| `view` | `viewable_range` |  |

After you have a range, an idea of how you want to see it, and a task in mind, you can use the various <ranges> header classes to perform work. The following table shows the classes associated with the standard for this header.

|  |  |  |
|---|---|---|
| `borrowed_iterator_t` | `borrowed_subrange_t` | `dangling` |
| `iterator_t` | `range_difference_t` | `range_reference_t` |
| `range_value_t`<br>`reference_t` | `range_size_t` | `range_value_t` |
| `ref_view` | `sentinel_t` | `subrange` |
| `view_interface` | `views::all` | `views::all_t` |
| `views::common`<br>`(common_view)` | `views::counted` | `views::empty`<br>`(empty_view)` |
| `views::filter`<br>`(filter_view)` | `views::iota(iota_view)` | `views::join`<br>`(join_view)` |
| `views::reverse`<br>`(reverse_view)` | `views::single`<br>`(single_view)` | `views::split`<br>`(split_view)` |
| `views::take`<br>`(take_view)` | `views::transform`<br>`(transform_view)` |  |

You can also customize the manner in which ranges work using customization point objects. The following table lists these objects found in the `std::ranges` namespace.

|  |  |  |
|---|---|---|
| `ranges::begin` | `ranges::data` | `ranges::empty` |
| `ranges::end` | `ranges::rbegin` | `ranges::rend` |
| `ranges::size` |  |  |

![](bbox=[0.917, 0.464, 1.0, 0.631])