To the properties specified by the interfaces that it implements, BitArray adds Length, which is shown here:

```
public int Length { get; set; }
```

Length sets or obtains the number of bits in the collection. Thus, Length gives the same value as does the standard Count property, which is defined for all collections. However, Count is read-only, but Length is not. Thus, Length can be used to change the size of a BitArray. If you shorten a BitArray, bits are truncated from the high-order end. If you lengthen a BitArray, false bits are added to the high-order end.

BitArray defines the following indexer:

```
public bool this[int idx] { get; set; }
```

You can use this indexer to get or set the value of an element.

Here is an example that demonstrates BitArray:

```
// Demonstrate BitArray.
using System;
using System.Collections;

class BADemo {
    public static void ShowBits(string rem, BitArray bits) {
        Console.WriteLine(rem);
        for(int i=0; i < bits.Count; i++)
            Console.Write("{0, -6} ", bits[i]);
        Console.WriteLine("\n");
    }
    static void Main() {
        BitArray ba = new BitArray(8);
        byte[] b = { 67 };
        BitArray ba2 = new BitArray(b);
        ShowBits("Original contents of ba:", ba);
        ba = ba.Not();
        ShowBits("Contents of ba after Not:", ba);
        ShowBits("Contents of ba2:", ba2);
        BitArray ba3 = ba.Xor(ba2);
        ShowBits("Result of ba XOR ba2:", ba3);
    }
}
```

The output is shown here:

```
Original contents of ba:
False False False False False False False False
```