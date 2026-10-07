# TABLE 3.3: Common Array Coding Errors (continued)

| Common Mistake | Error Description | Corrected Code |
|---|---|--|
| // 2.
int[] numbers = { 42, 84, 168 }; | When assigning an array after declaration, it is necessary to use the new keyword and then specify the data type. | int[] numbers;
numbers = new int[]{ 42, 84, 168 }; |
| // 3.
int[3] numbers = { 42, 84, 168 }; | It is not possible to specify the array size as part of the variable declaration. | int[] numbers =
{ 42, 84, 168 }; |
| // 4.
int[] numbers = new int[]; | The array size is required at initialization time unless an array literal is provided. | int[] numbers =
new int[3]; |
| // 5.
int[] numbers = new int[3]{}; | The array size is specified as 3, but there are no elements in the array literal. The array size must match the number of elements in the array literal. | int[] numbers =
new int[3]
{ 42, 84, 168 }; |
| // 6.
int[] numbers = new int[3];
Console.WriteLine(numbers[3]); | Array indices start at zero. Therefore, the last item is one less than the array size. (Note that this is not a runtime error, not a compile-time error.) | int[] numbers =
new int[3];
Console.WriteLine(
numbers[2]); |