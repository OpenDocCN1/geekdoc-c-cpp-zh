Here's the program's output:

```
First execution
-----------------
87
49
45
13
3
Second execution
-----------------
87
49
45
13
3
```

The output of the first and second execution is the same, proving that the query is executed immediately after it's defined.

To force a LINQ query to execute immediately, you can use aggregate functions so that the query must iterate over the elements at once. An aggregate function takes a collection of values and returns a scalar value.

> Aggregate functions are discussed in more detail later in this chapter.

Following is an example that uses the Count() aggregate function. The program selects all the odd numbers from an array and then counts the total number of odd numbers. Each number is then multiplied by two (which makes them all become even numbers).

```
static void Main(string[] args)
{
    int[] nums = { 12, 34, 10, 3, 45, 6, 90, 22, 87, 49, 13, 32 };
    var oddNumsCount = nums.Where
        (n => n % 2 == 1).OrderByDescending(n => n).Count();

    Console.WriteLine("First execution");
    Console.WriteLine("----------------");
    Console.WriteLine("Count: {0}", oddNumsCount);

    //---add 20 to each number in the array---
    for (int i = 0; i < 11; i++)
        nums[i] *= 2; //---all number should now be even---

    Console.WriteLine("Second execution");
    Console.WriteLine("----------------");
    Console.WriteLine("Count: {0}", oddNumsCount);

    Console.ReadLine();
}
```