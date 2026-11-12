+   (a) Expected `';'` before `'extern'`
+   (b) Expected primary-expression before `'extern'`
+   (c) Both 'a' and 'b'
+   (d) No error

**Answer: (c)** `'extern int b;'` is declaration. It should be done separately and then `'s.b'` should be initiated.

**60.** What is the output of the code? (L2)

```
```cpp
#include<iostream>
using namespace std;
int main ()
{
    register int b = 9;
    cout<<b;
}
```
```

+   (a) 9
+   (b) Prints nothing
+   (c) Unpredictable
+   (d) Error

**Answer: (a)** `register` storage class means the value is requested to be stored in register instead of RAM. It doesn't have any effect on the behavior of the variable.

**61.** What is the output of the following code snippet? (L3)

```
```cpp
# include <iostream>
using namespace std;
int main ()
{
    auto int p;
    auto int q = 10;
    cout <<"default value " <<p <<"\n";
    cout <<"default value " <<q <<"\n";
    getchar ();
    return 0;
}
```
```

+   (a) Compiler dependent
+   (b) Garbage and 10
+   (c) 1 and 10
+   (d) Compilation fault

**Answer: (a)** The behavior of the code will be different for different compilers. The modern-day compilers assign zero and the concept of garbage is avoided at most of the places. But, the traditional compilers and compilers like Dev C++ will initialize p with garbage and q with 10. And hence, the answer is compiler dependent.

**62.** What is the output of the code?

```
```cpp
# include <iostream>
using namespace std;
int main ()
{
    int p;
    auto int q;
    cout <<"default value " <<p <<"\n";
    cout <<"default value " <<q <<"\n";
    getchar ();
    return 0;
}
```
```

+   (a) Compiler dependent
+   (b) Garbage and 0
+   (c) 1 and 0 0
+   (d) Compilation fault

**Answer: (a)** The behavior of the code will be different for different compilers. The modern-day compilers assign zero and the concept of garbage is ruled out. But, the traditional compilers and compilers like Dev C++ will initialize with garbage. Hence, the answer is compiler dependent.

**63.** What is the output of the below piece of code snippet, assuming the compiler as Dev C++ or traditional one? (L3)

```
```cpp
# include <iostream>
using namespace std;
int main ()
{
    int p;
```
```