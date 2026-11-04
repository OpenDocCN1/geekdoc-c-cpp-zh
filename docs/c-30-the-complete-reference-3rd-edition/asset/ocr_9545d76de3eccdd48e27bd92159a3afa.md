Here is an example that demonstrates Insert(), Remove(), and Replace():

```
// Inserting, replacing, and removing.
using System;

class InsRepRevDemo {
    static void Main() {
        string str = "This test";

        Console.WriteLine("Original string: " + str);

        // Insert
        str = str.Insert(5, "is a ");
        Console.WriteLine(str);

        // Replace string
        str = str.Replace("is", "was");
        Console.WriteLine(str);

        // Replace characters
        str = str.Replace('a', 'X');
        Console.WriteLine(str);

        // Remove
        str = str.Remove(4, 5);
        Console.WriteLine(str);
    }
}
```

The output is shown here:

```
Original string: This test
This is a test
Thwas was a test
ThwXs wXs X test
ThwX X test
```

# Changing Case

String offers two convenient methods that enable you to change the case of letters within a string. These are called ToUpper() and ToLower(). Here are their simplest forms:

```
public string ToLower()
public string ToUpper()
```

ToLower() lowercases all letters within the invoking string. ToUpper() uppercases all letters within the invoking string. The resulting string is returned. There are also versions of these methods that allow you to specify cultural settings.

Also available are the methods ToUpperInvariant() and ToLowerInvariant(), shown here:

```
public string ToUpperInvariant()
public string ToLowerInvariant()
```

These work like ToUpper() and ToLower() except that they use the invariant culture to perform the transformations to upper- or lowercase.