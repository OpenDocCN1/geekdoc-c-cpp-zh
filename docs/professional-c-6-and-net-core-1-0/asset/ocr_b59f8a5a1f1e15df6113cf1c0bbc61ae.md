# main properties:

+   - `Length`—Indicates the length of the string that it actually contains
+   - `Capacity`—Indicates the maximum length of the string in the memory allocation

Any modifications to the string take place within the block of memory assigned to the `StringBuilder` instance, which makes appending substrings and replacing individual characters within strings very efficient. Removing or inserting substrings is inevitably still inefficient because it means that the following part of the string has to be moved. Only if you perform an operation that exceeds the capacity of the string is it necessary to allocate new memory and possibly move the entire contained string. In adding extra capacity, based on our experiments the `StringBuilder` appears to double its capacity if it detects that the capacity has been exceeded and no new value for capacity has been set.

For example, if you use a `StringBuilder` object to construct the original greeting string, you might write this code:

```
var greetingBuilder =
    new StringBuilder("Hello from all the guys at Wrox Press.",
150);
greetingBuilder.AppendFormat("We do hope you enjoy this book as much" +
    "as we enjoyed writing it");
```

> **NOTE** *To use the `StringBuilder` class, you need a `System.Text` reference in your code.*

This code sets an initial capacity of `150` for the `StringBuilder`. It is always a good idea to set a capacity that covers the likely maximum length of a string, to ensure that the `StringBuilder` does not need to relocate because its capacity was exceeded. By default, the capacity is set to 16. Theoretically, you can set a number as large as the number you pass in an `int`, although the system will probably complain that it does not have enough memory if you actually try to allocate the maximum of two billion characters (the theoretical maximum that a `StringBuilder` instance is allowed to contain).

Then, on calling the `AppendFormat` method, the remaining text is placed in the empty space, without the need to allocate more memory. However, the real efficiency gain from using a `StringBuilder` is realized when you make repeated text substitutions. For example, if you try to encrypt the text in the same way as before, you can perform the entire encryption without allocating any more memory whatsoever:

```
var greetingBuilder =
    new StringBuilder("Hello from all the guys at Wrox Press.",
150);
greetingBuilder.AppendFormat("We do hope you enjoy this book as much" +
    "as we enjoyed writing it");
```