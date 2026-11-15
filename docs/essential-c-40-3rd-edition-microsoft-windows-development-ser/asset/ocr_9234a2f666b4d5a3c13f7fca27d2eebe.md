```
return first < second;
}
}
```

In this example, an anonymous method is converted into a separately declared static method that is then instantiated as a delegate and passed as a parameter.

# Outer Variables

Local variables declared outside a lambda expression (including parameters), but captured (accessed) within the lambda expression, are outer variables of that lambda. this is also an outer variable. Outer variables captured by anonymous functions live on until after the anonymous function's delegate is destroyed. In Listing 12.21, it is relatively trivial to use an outer variable to count how many times BubbleSort( ) performs a comparison. Output 12.2 shows the results of this listing.

# LISTING 12.21: Using an Outer Variable in a Lambda Expression

```
class DelegateSample
{
    // ...

    static void Main(string[] args)
    {
        int i;
        int[] items = new int[5];
        int comparisonCount=0;

        for (i=0; i<items.Length; i++)
        {
            Console.Write("Enter an integer:");
            items[i] = int.Parse(Console.ReadLine());
        }

        BubbleSort(items,
            (int first, int second) =>
            {
                comparisonCount++;
                return first < second;
            }
```