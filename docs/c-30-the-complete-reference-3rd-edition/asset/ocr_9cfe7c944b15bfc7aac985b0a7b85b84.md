To create an XML output file when using the Visual Studio 2008 IDE, you must activate the Properties page. Next, select Build. Then, check the XML Documentation File box and specify the name of the XML file.

# An XML Documentation Example

Here is an example that demonstrates several documentation comments. It uses both the multiline and the single-line forms. As a point of interest, many programmers use a series of single-line documentation comments rather than a multiline comment even when a comment spans several lines. (Several of the comments in this example use this approach.) The advantage is that it is clearly identifies each line in a longer documentation comment as being part of a documentation comment. This is, of course, a stylistic issue, but it is common practice.

```
// A documentation comment example.

using System;

/** <remark>
This is an example of multiline XML documentation.
The Test class demonstrates several tags.
</remark>
*/

class Test {
/// <summary>
/// Main is where execution begins.
/// </summary>
static void Main() {
int sum;

sum = Summation(5);
Console.WriteLine("Summation of " + 5 + " is " + sum);
}

/// <summary>
/// Summation returns the summation of its argument.
/// <param name="val">The value to be summed is passed in val.</param>
/// <see cref="int" /> </see>
/// <returns> The summation is returned as an int value.</returns>
/// </summary>
static int Summation(int val) {
int result = 0;

for(int i=1; i <= val; i++)
result += i;

return result;
}
}
```

![](bbox=[0.92, 0.35, 0.99, 0.6])