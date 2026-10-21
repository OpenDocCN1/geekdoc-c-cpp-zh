![](bbox=[0.251, 0.143, 0.754, 0.252])

**Figure 14.3.** *output screen of program 14.3*

**EXPLANATION:** In the program we are checking if x>y if this is so we do the subtraction x-y. If y>x we do not perform subtraction instead we throw an exception “Subtraction not possible”. This exception is caught by the catch block in variable E.

```
/*PROG 14.4 MULTIPLE CATCH STATEMENT WITH SINGLE TRY */

#include <iostream.h>
void main( )
{
        int num = 10;
        for(num = 10; num < 30; num += 10)
        {
                try
                {
                        if(num == 20)
                                throw("GOOD");
                        else if(num < 20)
                                throw num;
                        else if (num > 20)
                                throw 2.25f;
                }
                catch(int E)
                {
                        cout << "Caught int Exception E=" << E << endl;
                }
                catch(char* E)
                {
                        cout << "Caught string Exception E=" << E << endl;
                }
                catch(float E)
                {
                        cout << "Caught float Exception E=" << E << endl;
                }
        }
}
```