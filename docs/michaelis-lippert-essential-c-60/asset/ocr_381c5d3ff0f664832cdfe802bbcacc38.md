a list of references to objects, so adding an integer or floating-point number to the list will box the value so that a reference can be obtained.

# LISTING 8.5: Subtle Box and Unbox Instructions

```
class DisplayFibonacci
{
    static void Main()
    {
        int totalCount;
        System.Collections.ArrayList list =
            new System.Collections.ArrayList();

        Console.Write("Enter a number between 2 and 1000:");
        totalCount = int.Parse(Console.ReadLine());

        // Execution-time error:
        // list.Add(0);  // Cast to double or 'D' suffix required.
        //                       Whether cast or using 'D' suffix,
        //                       CIL is identical.
        list.Add((double)0);
        list.Add((double)1);
        for (int count = 2; count < totalCount; count++)
        {
            list.Add(
                ((double)list[count - 1] +
                 (double)list[count - 2]));
        }

        foreach (double count in list)
        {
            Console.Write("{0}, ", count);
        }
    }
}
```

# OUTPUT 8.1

```
Enter a number between 2 and 1000:42
0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233, 377, 610, 987, 1597,
2584, 4181, 6765, 10946, 17711, 28657, 46368, 75025, 121393, 196418,
317811, 514229, 832040, 1346269, 2178309, 3524578, 5702887, 9227465,
14930352, 24157817, 39088169, 63245986, 102334155, 165580141,
```

The code shown in Listing 8.5, when compiled, produces five box and three unbox instructions in the resultant CIL.