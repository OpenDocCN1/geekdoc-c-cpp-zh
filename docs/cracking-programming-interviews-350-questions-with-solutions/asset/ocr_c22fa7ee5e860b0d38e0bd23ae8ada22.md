```
20        {
21            current_col_index = j;
22            while(current_col_index >=0 &&
23                  a[i][current_col_index] == x)
24            {
25                ++count;
26                current_col_index--;
27            }
28            ++i;
29        }
30    }
31
32    return count;
33 }
```

# Program 1.27: Using Saddleback Count

```
1#include "saddleback_count_correct.hpp"
2#include <iostream>
3
4 int main()
5 {
6     TwoDimArray<4, 4> a = { 2, 2, 3, 5,
7                            3, 4, 6, 6,
8                            3, 5, 6, 6,
9                            3, 6, 6, 9
10                        };
11
12     size_t count
13         = saddleback_count<4, 4>(a, 6);
14
15     std::cout << "Count of 6 is: "
16               << count << std::endl;
17 }
18 }
```

It prints :

```
Count of 6 is: 6
```

# Program 1.28: another Usage of Saddleback Count

```
1#include "saddleback_count_correct.hpp"
2#include <iostream>
3
4 int main()
5 {
6     TwoDimArray<4, 4> a = {
7         6, 6, 6, 6,
8         6, 6, 6, 6,
9         6, 6, 6, 6,
10        6, 6, 6, 6
11    };
12
```