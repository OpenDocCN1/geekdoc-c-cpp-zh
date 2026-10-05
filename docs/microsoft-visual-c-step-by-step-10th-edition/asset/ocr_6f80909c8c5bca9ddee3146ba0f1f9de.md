```
struct IntBits
{
    ...
    public override string ToString()
    {
        return (Convert.ToString(bits, 2);
    }
}
```

After you've created the indexer, you can use a variable of type IntBits instead of an int and apply the square bracket notation, as shown in the next example:

Click here to view code image

```
int adapted = 0b0_01111110;
IntBits bits = new IntBits(adapted);
bool peek = bits[6]; // retrieve bool at index 6; peek should be
true (1)
bits[0] = true; // set the bit at index 0 to true (1)
bits[3] = false; // set the bit at index 3 to false (0)
Console.WriteLine("$bits"); // displays 1110111 (0b0_01110111)
```

This syntax is muchlich easier to understand. It directly and succinctly captures the essence of the problem.

# Understanding indexer accesses

When you read an indexer, the compiler automatically translates your array-like code into a call to the get accessor of that indexer. Consider the following example:

```
bool peek = bits[6];
```

This statement is converted to a call to the get accessor for bits, and the index argument is set to 6.

Similarly, if you write to an indexer, the compiler automatically translates your array-like code into a call to the set accessor of that indexer, setting the index argument to the value enclosed in the square brackets, as illustrated here: