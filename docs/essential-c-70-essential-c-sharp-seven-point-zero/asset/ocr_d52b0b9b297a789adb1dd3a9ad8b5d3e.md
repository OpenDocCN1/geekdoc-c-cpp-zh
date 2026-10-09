# # Increment and Decrement Operators (++、--)

C# includes special unary operators for incrementing and decrementing counters. The **increment operator**, ++, increments a variable by one each time it is used. In other words, all of the code lines shown in Listing 4.13are equivalent.

# LISTING 4.13: Increment Operator

```
```
spaceCount = spaceCount + 1;
spaceCount += 1;
spaceCount++;
```
```

Similarly, you can decrement a variable by one using the **decrement operator**, --. Therefore, all of the code lines shown in Listing 4.14are also equivalent.

# LISTING 4.14: Decrement Operator

```
```
lines = lines - 1;
lines -= 1;
lines--;
```
```

# ## BEGINNER TOPIC

# ### A Decrement Example in a Loop

The increment and decrement operators are especially prevalent in loops, such as the *while loop* described later in the chapter. For example, Listing 4.15 uses the decrement operator to iterate backward through each letter in the alphabet.

# LISTING 4.15: Displaying Each Character’s Unicode Value in Descending Order

```
```
char current;
int unicodeValue;

// Set the initial value of current
current = 'z';

do
{
    // Retrieve the Unicode value of current
    unicodeValue = current;
    System.Console.Write($"{current}={unicodeValue}	");

    // Proceed to the previous letter in the alphabet
    current--;
}
while(current >= 'a');
```
```