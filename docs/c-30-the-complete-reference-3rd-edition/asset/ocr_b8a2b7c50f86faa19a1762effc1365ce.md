```
```csharp
// Demonstrate the index-range array.
class RangeArrayDemo {
    static void Main() {
        RangeArray ra = new RangeArray(-5, 5);
        RangeArray ra2 = new RangeArray(1, 10);
        RangeArray ra3 = new RangeArray(-20, -12);

        // Demonstrate ra.
        Console.WriteLine("Length of ra: " + ra.Length);

        for(int i = -5; i <= 5; i++)
            ra[i] = i;

        Console.Write("Contents of ra: ");
        for(int i = -5; i <= 5; i++)
            Console.Write(ra[i] + " ");

        Console.WriteLine("\n");

        // Demonstrate ra2.
        Console.WriteLine("Length of ra2: " + ra2.Length);

        for(int i = 1; i <= 10; i++)
            ra2[i] = i;

        Console.Write("Contents of ra2: ");
        for(int i = 1; i <= 10; i++)
            Console.Write(ra2[i] + " ");

        Console.WriteLine("\n");

        // Demonstrate ra3.
        Console.WriteLine("Length of ra3: " + ra3.Length);

        for(int i = -20; i <= -12; i++)
            ra3[i] = i;

        Console.Write("Contents of ra3: ");
        for(int i = -20; i <= -12; i++)
            Console.Write(ra3[i] + " ");

        Console.WriteLine("\n");
    }
}
```
```

The output from the program is shown here:

```
```text
Length of ra: 11
Contents of ra: -5 -4 -3 -2 -1 0 1 2 3 4 5

Length of ra2: 10
Contents of ra2: 1 2 3 4 5 6 7 8 9 10

Length of ra3: 9
Contents of ra3: -20 -19 -18 -17 -16 -15 -14 -13 -12
```
```