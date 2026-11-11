```
public class TemperatureClass {
    int temp = 0;

    public void displayTemperature() {
        if (temp == 0) {
            throw (new TempIsZeroException("We found Zero Temperature"));
        } else {
            Console.WriteLine("Temperature is: {0}", temp);
        }
    }
}
```

The code will return the following:

![](bbox=[0.036, 0.383, 0.967, 0.455])

# Nested try-catch

C# allows us to create a block of nested try-catch. In such a case, the exception will be caught in the catch block following the try block in which the exception occurred. Consider the following example:

```
using System;
public class NestedtryCatch
{
    public static void Main()
    {
        Employee emp = null;

        try
        {
            try
            {
                emp.EmployeeName = "";
            }
        }
    }
```