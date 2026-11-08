|  | `multiset` | `map` | `multimap` | `unordered_set` | `unordered_multiset` | `unordered_map` | `unordered_multimap` |
|---|---|---|---|---|---|---|---|
|  | ↔ | ↔ | ↔ | → | → | → | → |
|  |  | `at`<br>`operator[]` |  |  |  | `at`<br>`operator[]` |  |
|  | `empty`<br>`size`<br>`max_size` | `empty`<br>`size`<br>`max_size` | `empty`<br>`size`<br>`max_size` | `empty`<br>`size`<br>`max_size` | `empty`<br>`size`<br>`max_size` | `empty`<br>`size`<br>`max_size` | `empty`<br>`size`<br>`max_size` |
|  |  |  |  | `reserve` | `reserve` | `reserve` | `reserve` |
|  | `clear`<br>`insert`<br>`emplace`<br>`emplace_hint`<br>`erase` | `clear`<br>`insert`<br>`emplace`<br>`emplace_hint`<br>`erase` | `clear`<br>`insert`<br>`emplace`<br>`emplace_hint`<br>`erase` | `clear`<br>`insert`<br>`emplace`<br>`emplace_hint`<br>`erase` | `clear`<br>`insert`<br>`emplace`<br>`emplace_hint`<br>`erase` | `clear`<br>`insert`<br>`emplace`<br>`emplace_hint`<br>`erase` | `clear`<br>`insert`<br>`emplace`<br>`emplace_hint`<br>`erase` |
|  | `swap`<br>`<algo>³` | `swap`<br>`<algo>³` | `swap`<br>`<algo>³` | `swap` | `swap` | `swap` | `swap` |
|  | `(sorted)` | `(sorted)` | `(sorted)` |  |  |  |  |
|  | `count`<br>`find`<br>`lower_bound`<br>`upper_bound`<br>`equal_range` | `count`<br>`find`<br>`lower_bound`<br>`upper_bound`<br>`equal_range` | `count`<br>`find`<br>`lower_bound`<br>`upper_bound`<br>`equal_range` | `count`<br>`find`<br>`equal_range` | `count`<br>`find`<br>`equal_range` | `count`<br>`find`<br>`equal_range` | `count`<br>`find`<br>`equal_range` |
|  | `O(n)` | `O(n log n)` | `O(1) or O(n)` | `O(1) or O(log n)` |  |  |  |