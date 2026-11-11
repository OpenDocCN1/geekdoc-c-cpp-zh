```
```cpp
char var2[20];
double var3;
};

int main()
{
    Test1 t1;
    Test2 t2;

    cout<<"Memory occupied by the variable of a Union: "<<sizeof(t1)<<endl;
    cout<<"Memory occupied by the variable of a Structure:
    "<<sizeof(t2)<<endl;
    return 0;
}
```
```

Ans.  Output of the preceding program is as follows:

```
```text
Memory occupied by the variable of a Union: 20
Memory occupied by the variable of a Structure: 30
```
```

# Q9.  What will be the output of the following program?

```
```cpp
#include <iostream.h>

int main ()
{
    struct myStruct
    {
        int var1;
        float var2;
    }ms;

    ms.var1 = 123;
    ms.var2 == 123.123;

    cout<<"value of var1: "<<ms.var1<<endl;
    cout<<"value of var2: "<<ms.var2<<endl;

    return 0;
}
```
```

Ans.  The output of the preceding program is as follows:

```
```text
value of var1: 123
value of var2: 123.123
```
```

# Q10.  What will be the output of the following program?

```
```cpp
#include <iostream.h>

union MyUnion
{
```
```