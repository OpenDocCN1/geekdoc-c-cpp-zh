foreach(type loopvar in collection) statement;

Here, type loopvar specifies the type and name of an iteration variable. The iteration variable receives the value of the next element in the collection each time the foreach loop iterates. The collection being cycled through is specified by collection, which, for the rest of this discussion, is an array. Thus, type must be the same as (or compatible with) the element type of the array. Beginning with C# 3.0, type can also be var, in which case the compiler determines the type based on the element type of the array. This can be useful when working with certain queries, as described later in this book. Normally, you will explicitly specify the type.

Here is how foreach works. When the loop begins, the first element in the array is obtained and assigned to loopvar. Each subsequent iteration obtains the next element from the array and stores it in loopvar. The loop ends when there are no more elements to obtain. Thus, the foreach cycles through the array one element at a time, from start to finish.

One important point to remember about foreach is that the iteration variable loopvar is read-only. This means you can't change the contents of an array by assigning the iteration variable a new value.

Here is a simple example that uses foreach. It creates an array of integers and gives it some initial values. It then displays those values, computing the summation in the process.

```
```csharp
// Use the foreach loop.

using System;

class ForeachDemo {
 static void Main() {
 int sum = 0;
 int[] nums = new int[10];

 // Give nums some values.
 for(int i = 0; i < 10; i++)
 nums[i] = i;

 // Use foreach to display and sum the values.
 foreach(int x in nums) {
 Console.WriteLine("Value is: " + x);
 sum += x;
 }
 Console.WriteLine("Summation: " + sum);
 }
}
```
```

The output from the program is shown here:

Value is: 0
Value is: 1
Value is: 2
Value is: 3
Value is: 4
Value is: 5
Value is: 6
Value is: 7