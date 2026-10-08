| <regex> | regex, smash | $10.4 |
| <string> | string, basic_string | $10.2 |
| <string_view> | string_view | $10.3 |
| <set> | set, multiset | $12.8 |
| <iostream> | istostream, ostringstream | $11.7.3 |
| <stdexcept> | length_error, out_of_range, runtime_error | $4.2 |
| <tuple> | tuple, get(), tuple_size<> | $15.3.4 |
| <thread> | thread | $18.2 |
| <unordered_map> | unordered_map, unordered_multimap | $12.6 |
| <utility> | move(), swap(), pair | Chapter 16 |
| <variant> | variant | $15.4.1 |
| <vector> | vector | $12.2 |

This listing is far from complete. 

Headers from the C standard library, such as <stdlib.h> are provided. For each header there is also a version with its name prefixed by € and a .h removed. This version, such as <stdlib> places its declarations in the std and global namespace.
The headers reflect the history of the development of the standard library. Consequently, they are not always logical and easy to remember as we would like. That's one reason to use a module, such as std ($9.3.3), instead.

# # 9.4 Advice

+   [1] Don't reinvent the wheel; use libraries; $9.1; [CG: SL.1.]
[2] When you have a choice, prefer the standard library over other libraries; $9.1; [CG: SL.2.]
[3] Do not think the standard library is ideal for everything; $9.1.
[4] If you don't use modules, remember to #include the appropriate headers; $9.3.1.
[5] Remember that standard-library facilities are defined in namespace std; $9.3.1; [CG: SL.3.]
[6] When using ranges, remember to explicitly qualify algorithm names; $9.3.2.
[7] Prefer importing modules over #including header files ($9.3.3).