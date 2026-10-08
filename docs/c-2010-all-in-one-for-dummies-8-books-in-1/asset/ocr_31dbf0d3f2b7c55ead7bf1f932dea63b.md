# 70 StringBuilder: Manipulating Strings More Efficient

Avoid such costs when you're doing lots of modifications to strings, use the companion class StringBuilder. Be sure to add this line at the top of your file:

```
using System.Text; // The compiler where to find StringBuilder.
```

Unlike StringBuilder manipulations, the manipulations you do on a StringBuilder directly change the underlying string. Here's an example:

```
StringBuilder builder = new StringBuilder("012");
builder.Append("34");
builder.Append("56");
string result = builder.ToString(); // result = 0123456
```

Create a StringBuilder instance initialized with an existing string, just as shown. Create an empty StringBuilder with no initial value:

```
StringBuilder builder = new StringBuilder(); // Defaults to 16 characters
```

You can also create the StringBuilder with the capacity you expect it to, which reduces the overhead of increasing the builder's capacity frequently:

```
StringBuilder builder = new StringBuilder(256); // 256 characters.
```

Use the Append() method to add text to the end of the current contents. ToString() to retrieve the string inside the StringBuilder when you finish your modifications. Here's the StringBuilder version of the low loop just, with retrieval of the final concatenated string in bold:

```
StringBuilder sb = new StringBuilder(20000); // Allocate a bunch.
for (int i = 0; i < 1000; i++) {
    sb.Append(listOf[i]); // Same list of names as earlier
}
string result = sb.ToString(); // Retrieve the results.
```

StringBuilder has a number of other string methods, including Insert(), Remove(), and Replace(). It lacks many of string's methods, though such as Substring(), CopyTo(), and IndexOf().

Suppose that you want to uppercase just the first character of a string, as in the earlier section "Converting a string to upper- or lowercase." With StringBuilder, it's much cleaner looking than the code I gave.

```
StringBuilder sb = new StringBuilder('jones');
sb[0] = char.ToUpper(sb[0]);
string fixedString = sb.ToString();
```

This puts the lowercase string "jones" into a StringBuilder, accesses the first char in the StringBuilder's string directly, uses the char.ToUpper() method to uppercase the character.

![](bbox=[0.143, 0.206, 0.213, 0.263])