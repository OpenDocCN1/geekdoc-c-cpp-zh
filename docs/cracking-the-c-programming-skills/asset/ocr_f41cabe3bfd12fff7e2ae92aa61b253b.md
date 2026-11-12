```
```cpp
};
int main()
{
    cons S(3.34);
    cons S(3); }
```
```

+   (a) 3.34　　　 (b) 3  
+   (c) Unpredictable　 (d) Error

**Answer: (a)** Now this is correct. The arguments matches to the appropriate definitions and gets called appropriately.

# **32.** What is the output of the code? (L3)

```
```cpp
#include<iostream>
using namespace std;
class cons
{
  public:
    int m;
    cons(int d)
    { cout<< d << " "; }
};
int main()
{
  cons S(3.34);
  cons S(3); }
```
```

+   (a) 3.34　　　 (b) 3  
+   (c) Unpredictable　 (d) Error

**Answer: (b)** As there is only one overloaded definition of the constructor, various data types gets mapped to internally and type cast takes place. Here, no ambiguity is present as only one definition is available.

# **33.** What is the output of the code? (L3)

```
```cpp
#include<iostream>
using namespace std;
class cons
{
  public:
    int m;
    cons(int d)
    { cout<< d<< " "; }
    cons(int f)
    { cout<< f<< " "; }
};
int main()
{
  cons S(3); }
```
```

+   (a) 3 3　　　 (b) 3  
+   (c) Unpredictable　 (d) Error

**Answer: (d)** Changing the variable name of the parameter doesn’t change the two definitions. Internally, both the definitions are considered same and the error “`cons::cons(int)` cannot be overloaded”.

# **34.** What is the output of the code? (L3)

```
```cpp
#include<iostream>
using namespace std;
class cons
{
  public:
    int m;
    cons(int d)
    { cout<< d<< " "; }
    cons(void f)
    { cout<< "basic constructor"; }
};
int main()
{ cons S; }
```
```

+   (a) basic constructor  
+   (b) Prints nothing  
+   (c) Unpredictable  
+   (d) Error

**Answer: (d)** A variable cannot have ‘void’ type. So it throws a set of errors in consequence of this.

# **35.** What will be the error thrown by the code? (L4)

```
```cpp
#include<iostream>
using namespace std;
class cons
{
  public:
    int m;
    cons(int d)
    { cout<< d << " "; }
    cons(void f)
    { cout<< "basic constructor"; }
};
int main()
{ cons S; }
```
```