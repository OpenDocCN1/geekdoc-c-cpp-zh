| Type traits by category (Cont.) |  |  |\n|---|---|---|\n| Pointers | `remove_pointer` | `add_pointer` |\n| Sign modifiers | `make_signed` | `make_unsigned` |\n| Arrays | `remove_extent` | `remove_all_extents` |\n| Miscellaneous transformations | `aligned_storage` | `conditional` · `underlying_type` |\n|  | `aligned_union` | `common_type` · `invoke_result`<sup>17</sup> |\n|  | `decay` | `common_reference`<sup>20</sup> · `void_t`<sup>17</sup> |\n|  | `remove_cvref`<sup>20</sup> | `basic_common_reference`<sup>20</sup> · `type_identity`<sup>20</sup> |\n|  | `enable_if` |  |\n| Operations on traits | `conjunction`<sup>17</sup> | `disjunction`<sup>17</sup> · `negation`<sup>17</sup> |\n| Functions |  |  |\n| Member relationships | `is_pointer_interconvertible_with_class`<sup>20</sup> | `is_corresponding_member`<sup>20</sup> |

# 15.6 C++20 Concepts: A Deeper Look

Now that we’ve introduced how to constrain a template parameter via the `requires` clause and predefined concepts, we’ll create a custom concept that aggregates two predefined ones and present additional concepts features.

# 15.6.1 Creating a Custom Concept

C++20’s predefined concepts often aggregate multiple constraints, sometimes including those from other predefined concepts, effectively creating what some developers refer to as a type category.<sup>43</sup> You also can use templates to define your own custom concepts. Let’s create a custom concept that aggregates the predefined concepts `std::integral` and `std::floating_point` we used in Fig. 15.5 to constrain the multiply function template:

```
template<typename T>\nconcept Numeric = std::integral<T> || std::floating_point<T>;
```

A concept begins with a template header followed by

+   - the C++20 keyword `concept`,\n- the concept name (`Numeric`),\n- an equal sign (`=`) and\n- the constraint expression (`std::integral<T> || std::floating_point<T>`).

43. Inbal Levi, “Exploration of C++20 Metaprogramming,” September 29, 2020. Accessed April 18, 2023. https://www.youtube.com/watch?v=XgrjjbKaIV8.