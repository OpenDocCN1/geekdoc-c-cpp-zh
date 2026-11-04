Similarly, when applied to `0.12345`, the control `00.0%` outputs `12.3%`. The percent sign multiplies the number by 100 and adds `%`. The `00.0` indicates that the output should include at least two digits to the left of the decimal point and only one digit after the decimal point. The number `0.01` is displayed as `01.0%`, using the same `00.0%` specifier.

The mysterious `try . . . catch` catches any errors that spew forth in the event you enter an illegal format command such as a `D`, which stands for decimal. (I cover exceptions in Chapter 9 of this minibook.)

![](bbox=[0.1, 0.2, 0.22, 0.3])

# ### StringBuilder: Manipulating Strings More Efficiently

Building longer strings out of a bunch of shorter strings can cost you an arm and its elbow. Because a string, after it's created, can't be changed — it's immutable, as I say at the beginning of this chapter. This example doesn't tack "ly" onto `s1`:

```
```
string s1 = "rapid";
string s2 = s1 + "ly";          // s2 = rapidly.
```
```

It creates a new string composed of the combination. (`s1` is unchanged.) Similarly, other operations that appear to modify a string, such as `Substring()` and `Replace()`, do the same.

The result is that each operation on a string produces yet another string. Suppose you need to concatenate 1000 strings into one huge one. You're going to create a new string for each concatenation:

```
```
string[] listOfNames = ...  // 1000 pet names
string s = string.Empty;
for(int i = 0; i < 1000; i++)
{
    s += listOfNames[i];
}
```
```

To avoid such costs when you're doing lots of modifications to strings, use the companion class `StringBuilder`. Be sure to add this line at the top of your file:

```
```
using System.Text;  // Tells the compiler where to find StringBuilder.
```
```

![](bbox=[0.1, 0.73, 0.22, 0.83])

Unlike `String` manipulations, the manipulations you do on a `StringBuilder` directly change the underlying string. Here's an example:

```
```
StringBuilder builder = new StringBuilder("012");
builder.Append("34");
builder.Append("56");
string result = builder.ToString();  // result = 0123456
```
```

Create a `StringBuilder` instance initialized with an existing string, as just shown. Or create an empty `StringBuilder` with no initial value: