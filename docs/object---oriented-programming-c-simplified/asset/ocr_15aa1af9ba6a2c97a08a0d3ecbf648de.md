# # 616 Object-Oriented Programming C++ Simplified

```
input(f);
sort(f);
cout << "SORTED ARRAY IS" << endl;
show(f);
}
```

OUTPUT :
Enter5 intnumber
10 5 26 17 80
SORTED ARRAY IS
5 10 17 26 80
Enter5 floatnumber
56.8 4.5 2.3 90.634.56
SORTED ARRAY IS
0.56 2.3 4.5 56.8 90.634

![](bbox=[0.55, 0.11, 0.95, 0.45])

In the program we have three function templates :

+   1. One for inputting array elements.
+   2. Second for showing the array elements.
+   3. Third for sorting array element.

As we have array of two different data types, total 2 × 3 = 6 function definition are generated when specific call is made to each function i.e., 3 for integer data type int : input, show and sort and 3 for float data type. Rest is simple to understand.

```
/* PROG 13.5 WORKING WITH TWO GENERIC DATA TYPE AT A TIME */
#include <iostream.h>
#include <typeinfo.h>
template<class T1, class T2>
```