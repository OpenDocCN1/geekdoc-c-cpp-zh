```
floatData
2.4      4.5
charData
P  T
char *Data
One      Two
```

![](bbox=[0.28, 0.27, 0.72, 0.44])

Figure 13.10. Output screen of program 13.13

EXPLANATION : Here, we have a class template which is similar to class template demo created in the earlier program with the difference that this class simply accepts and display the data members. In the main when demo<int>d1(10,20); executes a new demo class for int data type will be created and all occurrences of PAR will be replaced by int. Constructor of demo class be called and n1 will have value 10 and n2 will have 20. From the constructor we have called function show which displays data type of n1 and n2 and their values. Similar argument holds for other statements :

```
demo < float > d2(2.4f,4.5f);
demo < char > d3('P','T');
demo < char* > d4("One","Two");
```

# /*PROG 13.14 DISPLAY OF DIFFERENT TYPES OF DATA USING CLASS TEMPLATE VER 2*/

```
#include <iostream.h>
#include <typeinfo.h>
template <class T1,class T2>
class demo
{
    T1 n1;
    T2 n2;
public :
    demo(T1 x, T2 y)
```