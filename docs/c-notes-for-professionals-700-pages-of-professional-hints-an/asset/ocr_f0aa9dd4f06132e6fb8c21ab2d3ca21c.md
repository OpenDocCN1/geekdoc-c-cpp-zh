```
}
Console.WriteLine(s); // The variable 's' still refers to the same System.String
// value in memory, but the contents at that location were
// changed by the unsafe write above.
// Displays: "aaaaa"
```

# Section 152.3: Unsafe Array Index

```
void Main()
{
    unsafe
    {
        int[] a = {1, 2, 3};
        fixed(int* b = a)
        {
            Console.WriteLine(b[4]);
        }
    }
}
```

Running this code creates an array of length 3, but then tries to get the 5th item (index 4). On my machine, this printed 1910457872, but the behavior is not defined.

Without the unsafe block, you cannot use pointers, and therefore cannot access values past the end of an array without causing an exception to be thrown.