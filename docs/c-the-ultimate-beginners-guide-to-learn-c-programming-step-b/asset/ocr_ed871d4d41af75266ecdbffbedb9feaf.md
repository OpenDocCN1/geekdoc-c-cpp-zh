```
```csharp
{
    public static void Main()
    {
        int[] array1 = new int[5];

        array1[0] = 1;

        array1[1] = 2;

        array1[2] = 3;

        array1[3] = 4;
        array1[4] = 5;
        Console.WriteLine(array1[0]);
        Console.WriteLine(array1[1]);
        Console.WriteLine(array1[2]);
        Console.WriteLine(array1[3]);
        Console.WriteLine(array1[4]);
    }
}
```
```

The code will return the following result:

+   1. 1
+   2. 2
+   3. 3
+   4. 4
+   5. 5

The retrieval or access to the array values is also done using the indexes. The index of the element is passed within brackets. Consider the example given below:

```
```csharp
array1[0];
array1[1];
```
```