Console.WriteLine(string.Format("Your full name is {0} {1}", args));

This leaves place support for localization in the same way it works with composite strings and doesn’t introduce any post-compile injection of code within strings.

# String Methods

The string type, like the Console type, includes several methods. There are methods, for formatting, concatenating, and comparing strings.

The Format() method in Table 2.6 behaves similarly to the Console.Write() and Console.WriteLine() methods, except instead of displaying the result in the console window, string.Format() returns the result to the caller. Of course, with string interpolation, the need for string.Format() is significantly reduced (except for localization support). Under the covers, however, string interpolation compiles down a CIL combination of constants (C# 11) plus string.Concat and string.Format() invocations whenever the string combination is not made of string literals.

All of the methods in Table 2.6 are static. This means that, to call the method, it is necessary to prefix the method name (e.g., Concat) with the type that contains the method (e.g., string). As illustrated later in this chapter, however, some of the methods in the string class are instance methods. Instead of prefixing the method with the type, instance methods use the variable name (or some other reference to an instance). Table 2.7 shows a few of these methods, along with examples of their use.

TABLE 2.6: string Static Methods

| Statement | Example |
| --- | --- |
| static string string.Format(format, ...) | string text, firstName, lastName; //... text = string.Format("Your full name is {0} {1}", firstName, lastName); // Display "Your full name is <name> <lastName>." Console.WriteLine(text); |