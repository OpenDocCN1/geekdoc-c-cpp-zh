```
cout << "************" << s << "************" << endl;
cout << typeid(par).name( ) << " parameter= " << par << endl;
}

void main( )
{
    show(12);
    show(35.46);
}
```

# OUTPUT :

**********Good Morning**********
int parameter= 12
**********Good Morning**********
double parameter= 35.46

![](bbox=[0.23, 0.43, 0.77, 0.59])

Figure 13.8. Output screen of program 13.10

# EXPLANATION :

The program is similar to previous one but here we have taken second argument to function template show as default argument of char* type. Thus, you may have default argument to function template.

# /* PROG 13.11 OVERLOADING OF FUNCTION TEMPLATE */

```
#include <iostream.h>
#include <typeinfo.h>
template <class T>
void show(T par)
{
    cout << "Function template show \n";
    cout << "par :=" << par << endl;
}
```