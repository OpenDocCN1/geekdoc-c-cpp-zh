+   20
+   a
+   (d) None of the above

Answer: (c) is the answer and this concept is referred to as Default Arguments.

```
```
return 0;
}
```
```

+   (a) obj1[0]: 0
+       obj2[0]: 1
+       obj1[1]: 0
+       obj2[1]: 0
+   (b) Compilation error
+   (c) Segmentation fault
+   (d) obj1[0]: 0
+       obj2[0]: 1
+       obj1[1]: 1
+       obj2[1]: 1

Answer: (a) Is the correct answer as destructor can be at the top of the code as well.

# ### 22. What is the output of the following code? (L3)

```
```cpp
#include <iostream>
using namespace std;
void func (int a=0, float b =0.000, char c = 'a')
{
    cout <<"\n" << a;
    cout <<"\n" << b;
    cout << "\n" << c;
}
int main() {
    func ();
    func (10);
    func (10,20.000);
    return 0;
}
```
```

+   (a) Compilation fault
+   (b) Overloading error
+   (c) 0
+       0
+       a
+       10
+       0
+       a
+       10

# ### 23. What is the output of the following code? (L4)

```
```cpp
#include <iostream>
using namespace std;
void func (int a=0, int b, char c = 'a')
{
    cout <<"\n" << a;
    cout <<"\n" << b;
    cout << "\n" << c;
}
int main() {
    func ();
    func (10);
    func (10,20.000);
    return 0;
}
```
```

+   (a) Compilation error
+   (b) 0
+       0
+       a
+   (c) Syntax error
+   (d) 10
+       20
+       000

Answer: (a) Compilation error. Default argument missing for parameter 2 of 'void func (int, int, char)'

# ### 24. What is the output of the following code? (L4)

```
```cpp
#include <iostream>
using namespace std;
void func (int a=0, int b=0, char c = 'a')
{
    int a=1;
```
```