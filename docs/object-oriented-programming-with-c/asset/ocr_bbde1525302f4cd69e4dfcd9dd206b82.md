p = (int *) q;

Alternatively, we can use **typedef** to create an identifier of the required type and use it in the functional notation.

```
typedef int * int_pt;
p = int_pt(q);
```

# Program 3.5  Explicit Type Casting

```
#include <iostream>
#include <conio.h>
using namespace std;

int main()
{
        int intvar=25;
        float floatvar=35.87;

        cout<<"intvar = "<<intvar;
        cout<<"\nfloatvar = "<<floatvar;
        cout<<"\nfloat(intvar) = "<<float(intvar);
        cout<<"\nint(floatvar) = "<<int(floatvar);

        getch();
}
```

The output of Program 3.5 would be:

```
intvar = 25
floatvar = 35.87
float(intvar) = 25
int(floatvar) = 35
```