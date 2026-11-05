# 13.6 User defined exceptions

Users can create their own exception classes when the situation arises where the user needs to handle an exception in a special way using custom code. These exceptions are known as user defined exceptions.

The user defined exceptions classes are derived from the ApplicationException class.

# Example 52:

```
```csharp
using System;
namespace userdefined
{
    class Average
    {
        static void Main(string[] args)
        {
            Perform p = new Perform();
            try
            {
                p.CalAverage();
            }
            catch(CountZeroException e)
            {
                Console.WriteLine("CountZeroException: {0}",e.Message);
            }
            Console.Read();
        }
    }
    public class CountZeroException:ApplicationException
    {
        public CountZeroException(string message):base(message)
        {
        }
    }
    public class Perform
    {
        int no1 = 0;
        int count = 0;
        float average;
        public void CalAverage()
        {
            if(count == 0)
            {
                throw(new CountZeroException("Count is zero in calculation"));
            }
        }
    }
```
```