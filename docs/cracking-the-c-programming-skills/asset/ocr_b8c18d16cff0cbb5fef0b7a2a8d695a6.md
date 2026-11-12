```
```cpp
cout<<x+y<< " ";
}
void add(double x, double y, int z) {
cout<<x+y+z<<" ";
}
};
int main(void)
{
function_add foo;
foo.add(76, 45);
foo.add(1.0000, 2.000, 2);
return 0;
}
```
```

```
```cpp
{
public:
void add(int x, int y, int z) {
cout<<x+y+z<<" ";
}
void add(int a, int b, int c) {
cout<<a+b+c<<" ";
}
};
int main(void)
{
function_add foo;
foo.add(1, 2, 3);
foo.add(4, 5, 6);
return 0;
}
```
```

+   (a) Compilation fault  
+   (b) Syntax error  
+   (c) 121 5  
+   (d) 5.0 121

**Answer: (c)** This is the right way of using function overloading and will work fine. The number of arguments are different for both the functions hence, the call will be made based on the number of arguments. 2 arguments for the former and 3 for the latter.

+   (a) 6 15  
+   (b) 15 6  
+   (c) Compilation error (Cannot be overloaded)  
+   (d) None of the above

**Answer: c)** The number and type of arguments remain the same for both the functions while name of the function being the same. This is ambiguous and shall fail the compilation saying cannot overload.

**6.** Which of the following points about function overloading are true? (L2)

+   (a) Number of arguments can be the same for the functions.  
+   (b) Number of arguments must be different for all the functions.  
+   (c) Number of arguments or type of the arguments shall be different.  
+   (d) There is no requirement on data types or number of arguments.

**Answer: (c)** Number of arguments or type of the arguments shall be different for overloading to be performed.

**7.** What is the output of the following piece of code? (L3)

```
```cpp
#include <iostream>
using namespace std;
class function_add
```
```

**8.** What is the output of the following code snippet? (L3)

```
```cpp
#include <iostream>
using namespace std;
void show(char []);
void show(char [], char []);
void show(char [], char [], char []);
int main()
{
char one[] = "I LOVE INDIA";
char two[] = "INDIA IS MY COUNTRY";
char three[] = "JAIHIND";
show(one);
show(one, two);
```
```