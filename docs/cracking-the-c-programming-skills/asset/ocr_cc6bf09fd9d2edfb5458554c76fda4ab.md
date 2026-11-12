(a) 2    (b) 2.5
(c) 2.25  (d) Error
**Answer:** (a) `">>"` is shift right for numbers. `'a>>n'` means shift the bits of 'a' to right by n bits. This is equivalent to division by 2 power n. Here, 9/2 = 4 and 4/2 gives 2 as the final output.

41. What is the output of the code? (L3)

```
#include<iostream>
using namespace std;
    int main()
    { int a=9;
cout<<a<<2;  }
```

(a) 92    (b) 36
(c) Error  (d) Unpredictable

**Answer:** (a) Here the `'<<'` in between 'a' and 2 gets associated with the `cout`. This shows that cout maintains priority over `'<<'`.

42. What is the output of the code? (L3)

```
#include<iostream>
using namespace std;
int main()
{ int a=9;
cout<<(a<<2); }
```

(a) 92    (b) 36
(c) Error  (d) Unpredictable

**Answer:** (b) The parenthesis changes the associativity.

43. What is the output of the code? (L3)

```
#include<iostream>
using namespace std;
int a=3;
int main()
{ int a=9;
cout<<::a;  }
```

(a) 3    (b) 9
(c) Error  (d) Unpredictable

**Answer:** (a) The operator `'::'` is called scope resolution operator. It is used to access the global variable even if there is a local variable of the same name.

44. What is the output of the code? (L3)

```
#include<iostream>
using namespace std;
struct tea
{ int rate;
void bonus()
{ cout<<"festival"; }
};
int main()
{ t.rate=9;
cout<<t.rate;
t.bonus();  }
```

(a) 9    (b) 9festival
(c) Error  (d) Unpredictable

**Answer:** (b) Unlike 'C' Structure in C++ can have functions.

45. What is the output of the code? (L3)

```
#include<iostream>
using namespace std;
struct tea
{ int rate;
float f;
void bonus()
{ cout<<"festival"; }
};
int main()
{ t.rate=9;
cout<<sizeof(t);  }
```

(a) 4    (b) 8
(c) Error  (d) Unpredictable

**Answer:** (b) Functions do not consume any memory allocation of structure and union is similar to 'C'.