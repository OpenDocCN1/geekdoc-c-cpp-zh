# EXAMPLE 3.18

```
```csharp
/* Parameters.cs
 * Author    Doyle
 * This class demonstrates the
 * differences between the
 * default, ref, and out
 * parameter types */
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
namespace Parameters
{
    public class Parameters
    {
        public static void Main( )
        {
            int testValue = 1;

            Console.WriteLine("Original "
                              + " Value: {0} ",
                              testValue);
            TestDefault(testValue);
            Console.WriteLine("Upon return from "
                              + "TestDefault Value: {0}",
                              testValue);
            Console.WriteLine( );

            Console.WriteLine("Original Value: {0}",
                              testValue);
            TestRef(ref testValue);
            Console.WriteLine("Upon return from "
                              + "TestRef Value: {0}",
                              testValue);
            Console.WriteLine( );

            // variable does not have to be initialized
            // for out parameter type
            int testValue2;
            // however, you cannot display its value yet!
            // Console.WriteLine("Original "
            //                   + " Value: {0}", testValue2);
            TestOut(out testValue2);
            Console.WriteLine("Upon return from "
                              + "TestOut Value: {0}",
                              testValue2);
            Console.Read( );
        }
    }
}
```
```