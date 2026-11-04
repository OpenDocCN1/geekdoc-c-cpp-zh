```
```csharp
*pointer1 = *pointer1 - 1;
Console.WriteLine ("{0}    {1}", number1, number2);

number1 = number1*2;     // Multiplication
*pointer1 = *pointer1*2;
Console.WriteLine ("{0}    {1}", number1, number2);

number1 = number1/2;     // Division
*pointer1 = *pointer1/2;
Console.WriteLine ("{0}    {1}", number1, number2);

number1 = number1%3;     // Remainders
*pointer1 = *pointer1%3;
Console.WriteLine ("{0}    {1}", number1, number2);
}
}
}
```
```

# Example 4.29. Shorthand notation and the incrementing and decrementing operators.

```
```csharp
using System;

namespace Chapter4 {
    class Class1 {
        static unsafe void Main() {
            int number1 = 0, number2 = 0;
            int* pointer1 = &number2;

            for (int index = 0; index < 10; index++) {
                number1 = number1++;
                *pointer1 = (*pointer1)++;
            }
            Console.WriteLine ("{0}    {1}", number1, number2);
            number1 = number1 - 1;
            *pointer1 = (*pointer1)--;
            Console.WriteLine ("{0}    {1}", number1, number2);

            // number1 = number1 + number1
            number1 = number1 += number1;
            // *pointer1 = *pointer1 + *pointer1
            *pointer1 = *pointer1 += *pointer1;
```
```