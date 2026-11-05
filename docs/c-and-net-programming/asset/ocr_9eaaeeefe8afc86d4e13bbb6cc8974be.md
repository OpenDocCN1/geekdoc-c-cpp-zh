```
Console.WriteLine("The removed value: {0}", ch);
}
}
}
```

# Output

```
Queue Elements A B C D
Current queue
E F
Removing value from Queue
The removed value A
Removing value from Queue
The removed value B
```

# 12.9 BitArray Class

# Properties of the BitArray Class

| Property | Description |
|---|---|
| Count | Gets the number of elements contained in the BitArray. |
| IsReadOnly | Gets a value indicating whether the BitArray is read-only. |
| Item | Gets or sets the value of the bit at a specific position in the BitArray. |
| Length | Gets or sets the number of elements in the BitArray. |

# Methods of the BitArray Class

| Sr. No. | Methods |
|---|---|
| 1 | **public BitArray And(BitArray value);**<br>Performs the bitwise AND operation on the elements in the current BitArray against the corresponding elements in the specified BitArray. |
| 2 | **public bool Get(int index);**<br>Gets the value of the bit at a specific position in the BitArray. |
| 3 | **public BitArray Not();**<br>Inverts all the bit values in the current BitArray, so that elements set to true are changed to false, and elements set to false are changed to true. |