Additionally, this vector initializes a `std::span` (line 18). Finally, the `for` loop (line 22) uses the function `subspan` to create all the subspans starting at `first` and having `count` elements until `mySpan` is consumed.

![](bbox=[0.263, 0.166, 0.737, 0.334])

Use of the member function subspan

Kilian Henneberger reminded me of a particular use case of `std::span`. A `std::span` can be a constant range of modifiable elements.

# 5.2.6 A Constant Range of Modifiable Elements

For simplicity, I name a `std::vector` and a `std::span` range. A `std::vector`, like a `std::string` models a modifiable range of modifiable elements: `std::vector<T>`. When you declare this `std::vector` as const, range models a constant range of constant objects: `const std::vector<T>`. You cannot model a constant range of modifiable elements. This is where `std::span` comes into play. A `std::span` models a constant range of modifiable objects: `std::span<T>`. The following table emphasizes the variations of (constant/modifiable) ranges and (constant/modifiable) elements.

|  | Modifiable Elements | Constant Elements |
|---|---|---|
| Modifiable Range | `std::vector<T>` |  |
| Constant Range | `std::span<T>` | `const std::vector<T>`<br>`std::span<const T>` |

The program `constRangeModifiableElements.cpp` exemplifies each combination.