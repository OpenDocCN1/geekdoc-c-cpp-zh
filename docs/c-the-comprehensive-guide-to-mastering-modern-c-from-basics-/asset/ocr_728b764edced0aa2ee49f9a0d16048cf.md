| Operation | atkey | next | insert_list | access | → | ++ | set | multiset | map | unordered_set | multiset_map | ordered_map | unordered_map |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| (begin)/end | contig. | contag. | rand access | | | | ++ | | | | | | | |
| (begin)/end | contig. | contag. | rand access | | | | ++ | | | | | | | |
| assign | assign | assign | | | | | | | | | | | | |
| operator[] | operator[] | operator[] | | | | | | | operator[] | | | | | |
| front | front | front | | | | | | | | | | | |
| back | back | back | | | | | | | | | | | |
| empty | empty | empty | | | | | | empty | empty | empty | empty | empty | empty |
| size | size | size | | | | | | size | size | size | size | size | size |
| max_size | max_size | max_size | max_size | size | | | | | | max_size | max_size | max_size | max_size | max_size |
| resize | resize | | | | | | | | | | reserve | reserve | reserve |
| capacity | capacity | | | | | | | | | | | | |
| shrink_to_fit | shrink_to_fit | shrink_to_fit | | | | | | | | | | | |
| clear | clear | clear | | | | | | clear | clear | clear | clear | clear | clear |
| insert | insert | insert | insert_after | | | | | insert | insert | insert | insert | insert | insert |
| replace | replace | replace | replace_after | | | | | | | | | | | |
| erase_front | erase_front | | | | | | | erase_front | erase_front | erase_front | erase_front | erase_front | erase_front |
| erase | erase | erase | | | | | | | | erase | erase | erase | erase |
| push | push | push | push_front | | | | | push | push | push | push | push | push |
| push_front | push_front | push_front | push_front | | | | | push_front | push_front | push_front | push_front | push_front | push_front |
| pop_front | pop_front | pop_front | | | | | | | | | | | |
| push_back | push_back | push_back | push_back | | | | | push_back | push_back | push_back | push_back | push_back | push_back |
| erase_back | erase_back | erase_back | | | | | | | | | | | |
| pop_back | pop_back | pop_back | | | | | | | | | | | |
| swap | swap | swap | | | | | | swap | swap | swap | swap | swap | swap |
| merge | merge | merge | merge | | | | | | | merge | merge | merge | merge |
| splice | splice | splice | splice_after | | | | | | | | | | | |
| remove | remove | remove | remove | | | | | | | | | | | |
| remove_if | remove_if | remove_if | | | | | | | | | | | | |
| reverse | reverse | | | | | | | | | | | | | |
| unique | unique | unique | unique | | | | | | | | | | | |
| sort | sort | sort | sort | | | | | | | | | | | |
| count | count | count | count | | | | | count | count | count | count | count | count |
| find | find | find | find | | | | | find | find | find | find | find | find |
| lower_bound | lower_bound | lower_bound | lower_bound | | | | | | lower_bound | lower_bound | lower_bound | lower_bound | lower_bound |
| upper_bound | upper_bound | upper_bound | upper_bound | | | | | | upper_bound | upper_bound | upper_bound | upper_bound | upper_bound |
| equal_range | equal_range | equal_range | equal_range | | | | | | | | | equal_range or range |

*complexity* must be sorted. as source

![](bbox=[0.368, 0.808, 0.683, 0.823])