
```
string precise = value.ToString("R");
Console.WriteLine(precise);    // 0.33333333333333331
double res2 = double.Parse(precise);
Console.WriteLine(res2);
Console.WriteLine(value == res2);    // True
```

As you can see from the output for the preceding fragment, the precise ToString text does contain additional digits that the default ToString output doesn't have. Because of this, round-tripping doesn't produce the precise same value for the first example. When using the R style, though, things work just fine. Whenever you need to persist data (in particular, floating-point numbers or a BigInteger) as text and expect to be able to read it back, use the round-trip style.

## Regular Expressions

Parsing of text into a primitive value is easy enough using the various kinds of Parse methods. However, a more complex parsing task often needs to be accomplished. In that case, the BCL's support for regular expressions enters the picture. Because regular expressions are a language of their own, we just touch on some of the capabilities, deferring a thorough discussion to MSDN once more.

The first thing to make sure when working with regular expression facilities is to have a using directive to import the System.Text.RegularExpressions namespace. When this is done, you have unqualified access to the Regex class, which is the entry point of the API. First, you create a new instance of this class, specifying the regular expression pattern and an optional set of RegexOptions flags. Let's ignore this detail for now and go with a plain regular expression without special options:

```
var regex = new Regex("^0|([1-9][0-9]*)");

while (true)
{
    Console.Write("> ");
    string input = Console.ReadLine();
    Match match = regex.Match(input);
    if (match.Success)
        Console.WriteLine(match.Value);
}
```

This read-eval-print loop (REPL) takes in a user input string and matches it against the specified pattern. Upon success, the first match found within the user input string is printed. Notice a match is the longest sequence in the input string that conforms to the specified pattern. In this case, the pattern states that valid input is either 0 or (using a vertical bar) a digit in the range 1 through 9 ([1-9]) followed by any number of digits in the range 0 through 9 ([0-9]*).

### WHEN PERFORMANCE NEEDS IMPROVEMENT

Regular expressions lend themselves very well for precompilation. In fact, compiler theory starts with this very fact, covering principles of lexing and parsing, which makes heavy use of finite automata. A regular expression is nothing more than some kind of textual representation of such an automaton. Using the Compiled flag on the Regex constructor, you can ask the API to "compile" the regular expression such that it performs very well.

Under the hood, the regular expression compiler emits code that gets turned into an assembly that's loaded into the current application domain. I leave it to your imagination to think about the infrastructure used to achieve this. Real geeks may even have an attempt at using lightweight code generation or even the System.Linq.Expressions namespace to build such a compiler themselves.

Obviously, a cost is associated with such a compilation phase, so its benefits likely only outweigh the cost if you're going to reuse the Regex object over and over again (for example, when parsing a large input set of data).

Regular expressions can do more than just find matches for a given pattern; they can also be used to capture what's known as groups. A group is simply a part of a bigger regular expression pattern that can be extracted from the match. For example, assume you expect the user to enter a numeric range using the hyphen as a separator symbol. In that case, you really want to capture both the from and to parts of the range during regular expression matching. That's where groups come in handy:

```
var regex = new Regex(@"(?<from>0|[1-9][0-9]*)\-(?<to>0|[1-9][0-9]*)");

while (true)
{
    Console.Write("> ");
    string input = Console.ReadLine();
    Match match = regex.Match(input);
    if (match.Success)
    {
        Console.WriteLine("from {0} to {1}",
            match.Groups["from"].Value,
            match.Groups["to"].Value);
    }
}
```

In the pattern used for the example, two groups are specified using the rather cryptic (as not unusual for regular expressions) (?<group>pattern) syntax. The group part is a friendly name for the group, which can be omitted, allowing access to it by index. The pattern part speaks for itself and is a regular expression by itself. In this case, we use the

a string for a certain structure. Those two methods could be regarded as a way to do a wildcard search, but Contains can, too. The following observations hold:

- `s.StartsWith("B")` — `s` matches `B*`
- `s.EndsWith("t")` — `s` matches `*t`
- `s.Contains("a")` — `s` matches `*a*`

Other ways to achieve similar effects exist (for example, by leveraging IndexOf kind of methods). Those return an index of the first (or last, for LastIndexOf) occurrence of a given fragment in the string. A negative return value denotes failure and therefore can be interpreted as a “doesn’t contain” condition. For tasks more sophisticated than the ones discussed here, regular expressions likely provide a good angle of attack.

## Mutation? Not So Much

You might recall the immutable nature of strings from our first encounter with this data type. Contrary to a lot of unmanaged or native languages, managed strings do not permit in-place mutation of the value (for example, by changing characters). Despite this intrinsic limitation, lots of instance methods exist on System.String that seem to hint at possible mutation. This isn’t the case, though, because all of those methods return an entirely new string object.

A few examples are shown here:

```
string s = "world.";
s.Insert(0, "Hello ");
s.Replace('.', '!');
Console.WriteLine(s); // Contrary to what you may expect, this prints "world."
```

Why does this code print "world." as opposed to "Hello world!"? If we had looked more closely at the IntelliSense for Insert and Replace (or other methods, like Remove, for that matter), we would have seen them return a System.String object themselves. That’s the new object that contains the modified copy of the original string value. So to achieve the expected effect, you would write the following:

```
string s = "world.";
s = s.Insert(0, "Hello ");
s = s.Replace('.', '!');
Console.WriteLine(s); // Prints "Hello world!"
```

Notice, though, that this little piece of code has created no less than three copies of the string value, all of which could be very large if we were dealing with input coming from some file or another source that tends to be lengthy. It should be clear that this excessive use of copying puts quite a bit of pressure on the GC. If this turns out to be a problem for your application’s performance, a StringBuilder should be used (as discussed next).

### WHAT ABOUT +=?

Some people believe the += operator on strings to be magical. They think it's using secret tricks to append a value to an existing string without creating copies. This simply is not the case either. The following fragment really deals with a total of three string objects:

```
string s = "Hello";
s += " world!";
Console.WriteLine(s);
```

The two literals will be embedded in the assembly and loaded from there, using the ldstr instruction. The += operation is roughly turned into the following:

```
s = s + " world!";
```

This in its turn gets compiled into a String.Concat static method call, which will indeed produce a third string object containing the concatenation of both. Now because the two parts of the concatenation are known at compile time, you might think the compiler is smart enough to perform the concatenation by itself. This isn't the case, though, for this particular example. However, for some uses of the + operator involving string literals, the compiler can be smarter and perform such simple and straightforward optimizations. If we had written the following, such a trick would be carried out, only having to load a single string object:

```
string s = "Hello" + " world!";
Console.WriteLine(s);
```

This may be surprising because the compiler is dealing with constants that can be folded at compile time. Similarly, when using lots of + operators to perform concatenations, the knowledge of associativity of the operator can be leveraged to concatenate the constant parts at compile time. A trip to ILDASM can be a good learning experience from time to time.

## Trimming and Padding

Two common operations are to rip off excessive or introduce desired padding. The Trim and Pad methods are precisely what's needed to achieve those goals. Similar to the methods discussed earlier, they don't mutate the string object in-place but create whole new copies. As stated earlier, if this hurts performance because a lot of such operations are done or big strings are involved, the StringBuilder methods can be a good alternative. Having said that, the following code shows a few uses of those methods:

```
Console.Write("Enter your name: ");
string input = Console.ReadLine();
string name = input.Trim(' ', '\t');
Console.WriteLine("Welcome {0}!", name);
```

Here, the Trim method takes away any space or tab characters (specified using a params array parameter) at the start or the end of the given string. If only one side of the string
