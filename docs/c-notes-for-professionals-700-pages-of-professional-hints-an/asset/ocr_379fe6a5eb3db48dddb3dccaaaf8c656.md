```
//Warning CS3003 Type of 'Car.YearOfCreation' is not CLS-compliant
public UInt16 YearOfCreation
{
    get { return _yearOfCreation; }
}

//Warning CS3002 Return type of 'Car.CalculateDistance()' is not CLS-compliant
public UInt64 CalculateDistance()
{
    return 0;
}

//Warning CS3002 Return type of 'Car.TestDummyUnsignedPointerMethod()' is not CLS-compliant
public UIntPtr TestDummyUnsignedPointerMethod()
{
    int[] arr = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
    UIntPtr ptr = (UIntPtr)arr[0];

    return ptr;
}

//Warning CS3003 Type of 'Car.age' is not CLS-compliant
public sbyte age = 120;

}
}
```

# Section 146.3: Violation of CLS rule: Same naming

```
using System;

[assembly:CLSCompliant(true)]
namespace CLSDoc
{
    public class Car
    {
        //Warning CS3005 Identifier 'Car.CALCULATEAge()' differing only in case is not CLS-compliant
        public int CalculateAge()
        {
            return 0;
        }

        public int CALCULATEAge()
        {
            return 0;
        }
    }
}
```

Visual Basic is not case sensitive