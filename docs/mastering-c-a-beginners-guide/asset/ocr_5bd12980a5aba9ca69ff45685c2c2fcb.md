method, then the compiler will select the most derived version method:

```
using System;
namespace oops
{
    class myBase
    {
        //virtual function
        public virtual void VirtualMethod()
        {
            Console.WriteLine("virtual method defined in the base class");
        }
    }

    class myDerived : myBase
    {
        // hiding the implementation of base class method
        public new void VirtualMethod()
        {
            Console.WriteLine("virtual method defined in the Derive class");

            //still access the base class method
            base.VirtualMethod();
        }
    }
    class virtualClass
```