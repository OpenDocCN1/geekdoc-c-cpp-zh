```
new int[] { 1, 3 },
new int[] { 1, 2, 4 },
new int[] { 1, 5 },
new int[] { 1, 2, 3, 6 },
new int[] { 1, 7 },
new int[] { 1, 2, 4, 8 },
new int[] { 1, 3, 9 },
new int[] { 1, 2, 5, 10 } );
```

The following code will fail:

```
foreach (int divisor in divisorsTo10)
{
    WriteLine(divisor);
}
```

The failure occurs because the array divisorsTo10 contains int[] elements, not int elements. Instead, you have to loop through every sub-array, as well as through the array itself:

```
foreach (int[] divisorsOfInt in divisorsTo10)
{
    foreach(int divisor in divisorsOfInt)
    {
        WriteLine(divisor);
    }
}
```

As you can see, the syntax for using jagged arrays can quickly become complex! In most cases, it is easier to use rectangular arrays or a simpler storage method. Nonetheless, there may well be situations in which you are forced to use this method, and a working knowledge can't hurt. An example of this happens when working with XML documents where some elements have sub-children and other do not.

# STRING MANIPULATION

Your use of strings so far has consisted of writing strings to the console, reading strings from the console, and concatenating strings using the + operator. In the course of programming more interesting applications, you will discover that manipulating strings is something that you end up doing a lot. Therefore, it is worth spending a few pages looking at some of the more common string-manipulation techniques available in C#.

To start with, a string type variable can be treated as a read-only array of char variables. This means that you can access individual characters using syntax like the following:

```
string myString = "A string";
char myChar = myString[1];
```

However, you can't assign individual characters this way. To get a char array that you can write to, you can use the following code. This uses the ToCharArray() command of the array variable:

```
string myString = "A string";
char[] myChars = myString.ToCharArray();
```