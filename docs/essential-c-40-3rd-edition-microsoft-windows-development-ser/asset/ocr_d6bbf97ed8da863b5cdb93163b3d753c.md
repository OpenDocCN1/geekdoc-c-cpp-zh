# Table 2.7: Common Array Coding Errors

| Common Mistake | Error Description | Corrected Code |
| :--- | :--- | :--- |
| `int numbers[];` | The square braces for declaring an array appear after the data type, not after the variable identifier. | `int[] numbers;` |
| `int[] numbers; numbers = { 42, 84, 168 };` | When assigning an array after declaration, it is necessary to use the new keyword and then specify the data type. | `int[] numbers; numbers = new int[] { 42, 84, 168 };` |
| `int[3] numbers = { 42, 84, 168 };` | It is not possible to specify the array size as part of the variable declaration. | `int[] numbers = { 42, 84, 168 };` |
| `int[] numbers = new int[];` | The array size is required at initialization time unless an array literal is provided. | `int[] numbers = new int[];` |
| `int[] numbers = new int[3]{}` | The array size is specified as 3, but there are no elements in the array literal. The array size must match the number of elements in the array literal. | `int[] numbers = new int[3] { 42, 84, 168 };` |
| `int[] numbers = new int[3]; Console.WriteLine( numbers[3] );` | Array indexes start at zero. Therefore, the last item is one less than the array size. (Note that this is a runtime error, not a compile-time error.) | `int[] numbers = new int[3]; Console.WriteLine( numbers[2] );` |