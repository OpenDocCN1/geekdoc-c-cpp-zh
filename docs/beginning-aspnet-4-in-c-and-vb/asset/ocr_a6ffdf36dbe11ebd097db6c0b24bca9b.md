The example to demonstrate the BitArray class creates a bit array with 8 bits, indexed from 0 to 7. The SetAll() method sets all 8 bits to true. Then the Set() method changes bit 1 to false. Instead of the Set method, you can also use an indexer, as shown with index 5 and 7;

```
var bits1 = new BitArray(8);
bits1.SetAll(true);
bits1.Set(1, false);
bits1[5] = false;
bits1[7] = false;
Console.Write("initialized: ");
DisplayBits(bits1);
Console.WriteLine();
```

This is the displayed result of the initialized bits:

```
initialized: 10111010
```

The Not() method generates the inverse of the bits of the BitArray:

```
Console.Write(" not ");
DisplayBits(bits1);
bits1.Not();
Console.Write(" not = ");
DisplayBits(bits1);
Console.WriteLine();
```

The result of Not() is all bits inversed. If the bit was true, it is false, and if it was false, it is true:

```
not 10111010 = 01000101
```

Here, a new BitArray is created. With the constructor, the variable bits1 is used to initialize the array, so the new array has the same values. Then the values for bits 0, 1, and 4 are set to different values. Before the Or() method is used, the bit arrays bits1 and bits2 are displayed. The Or() method changes the values of bits1:

```
var bits2 = new BitArray(bits1);
bits2[0] = true;
bits2[1] = false;
bits2[4] = true;
DisplayBits(bits1);
Console.Write(" or ");
DisplayBits(bits2);
Console.Write(" = ");
bits1.Or(bits2);
DisplayBits(bits1);
Console.WriteLine();
```

With the Or() method, the set bits are taken from both input arrays. In the result, the bit is set if it was set with either the first or the second array:

```
01000101 or 10001101 = 11001101
```

Next, the And() method is used to operate on bits2 and bits1:

```
DisplayBits(bits2);
Console.Write(" and ");
DisplayBits(bits1);
Console.Write(" = ");
bits2.And(bits1);
DisplayBits(bits2);
Console.WriteLine();
```

The result of the And() method only sets the bits where the bit was set in both input arrays:

```
10001101 and 11001101 = 10001101
```