
```
DateTime thisYear = new DateTime(2011, 1, 1);
bool isLeapYear = DateTime.IsLeapYear(thisYear.Year);
```

The result for 2011 is false, but for 2012, it's true. (For now, don't worry about that first line of code, which uses some things you haven't gotten to yet.)

With the DateTime data type, you can do something like 80 different operations, such as pull out just the month; get the day of the week; add days, hours, minutes, seconds, milliseconds, months, or years to a given date; get the number of days in a given month; subtract two dates.

The following sample lines use a convenient property of DateTime called Now to capture the present date and time, and one of the numerous DateTime methods that let you convert one time into another:

```
DateTime thisMoment = DateTime.Now;
DateTime anHourFromNow = thisMoment.AddHours(1);
```

You can also extract specific parts of a DateTime:

```
int year = DateTime.Now.Year;          // For example, 2007
DayOfWeek dayOfWeek = DateTime.Now.DayOfWeek;  // For example, Sunday
```

If you print out that DayOfWeek object, it prints something like "Sunday." And you can do other handy manipulations of DateTimes:

```
DateTime date = DateTime.Today;          // Get just the date part.
TimeSpan time = thisMoment.TimeOfDay;    // Get just the time part.
TimeSpan duration = new TimeSpan(3, 0, 0);  // Specify duration in days.
DateTime threeDaysFromNow = thisMoment.Add(duration);
```

The first two lines just extract portions of the information in a DateTime. The next two lines add a duration to a DateTime. A duration, or amount of time, differs from a moment in time; you specify durations with the TimeSpan class, and moments with DateTime. So the third line sets up a TimeSpan of three days, zero hours, zero minutes, and zero seconds. The fourth line adds the three-day duration to the DateTime representing right now, resulting in a new DateTime whose day component is three greater than the day component for thisMoment.

Subtracting a DateTime from another DateTime (or a TimeSpan from a DateTime) returns a DateTime:

```
TimeSpan duration1 = new TimeSpan(1, 0, 0);  // One hour later.
// Since Today gives 12:00:00 AM (midnight), the following gives 1:00:00 AM:
DateTime anHourAfterMidnight = DateTime.Today.Add(duration1);
Console.WriteLine("An hour from midnight will be {0}", anHourAfterMidnight);
DateTime midnight = anHourAfterMidnight.Subtract(duration1);
Console.WriteLine("An hour before 1 AM is {0}", midnight);
```

The first line of the preceding code creates a TimeSpan of one hour. The next line gets the date (actually, midnight this morning) and adds the one-hour span to it, resulting in a DateTime representing 1:00 a.m. today. The next-to-last line subtracts a one-hour duration from 1:00 a.m. to get 12:00 a.m. (midnight).

For more information, search for DateTime structure in the Visual Studio Help system and take a look at the DateTimeExample program on this book's Web site.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_65_0.png)

## Declaring Numeric Constants

There are very few absolutes in life: however, I'm about to give you a C# absolute: Every expression has a value and a type. In a declaration such as int n, you can easily see that the variable n is an int. Further, you can reasonably assume that the type of a calculation n + 1 is an int. However, what type is the constant 1?

The type of a constant depends on two things: its value and the presence of an optional descriptor letter at the end of the constant. Any integer type less than 2 billion is assumed to be an int. Numbers larger than 2 billion are assumed to be long. Any floating-point number is assumed to be a double.

Table 2-4 demonstrates constants that have been declared to be of a particular type. The case of these descriptors is not important; 1U and 1u are equivalent.

Table 2-4 Common Constants Declared along with Their Types

| Constant | Type |
|---|---|
| 1 | int |
| 1U | unsigned int |
| 1L | long int (avoid lowercase l; it's too much like the digit 1) |
| 1.0 | double |
| 1.0F | float |
| 1M | decimal |
| true | bool |
| false | bool |
| 'a' | char |
| '\n' | char (the character newline) |
| '\x123' | char (the character whose numeric value is hex 123) |
| "a string" | string |
| "" | string (an empty string); same as String.Empty |

*'hex' is short for hexadecimal (numbers in base 16 rather than in base 10).

```
~~~
double doubleValue = 10.0;
long longValue = (long)doubleValue;
~~~
```

All conversions to and from a decimal require a cast. In fact, all numeric types can be converted into all other numeric types through the application of a cast. Neither bool nor string can be converted directly into any other type.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_67_0.png)

Built-in C# methods can convert a number, character, or Boolean into its string equivalent, so to speak. For example, you can convert the bool value `true` into the string "true"; however, you cannot consider this change a direct conversion. The bool `true` and the string "true" are completely different things.

## Letting the C# Compiler Infer Data Types

So far in this book — well, so far in this chapter — when you declared a variable, you *always* specified its exact data type, like this:

```
~~~
int i = 5;
string s = "Hello C#";
double d = 1.0;
~~~
```

You're allowed to offload some of that work onto the C# compiler, using the `var` keyword:

```
~~~
var i = 5;
var s = "Hello C# 4.0";
var d = 1.0;
~~~
```

Now the compiler *infers* the data type for you — it looks at the stuff on the right side of the assignment to see what type the left side is.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_67_1.png)

For what it's worth, Chapter 3 of this minibook shows how to calculate the type of an expression like the ones on the right side of the assignments in the preceding example. Not that you need to do that — the compiler mostly does it for you. Suppose, for example, you have an initializing expression like this:

```
~~~
var x = 3.0 + 2 - 1.5;
~~~
```

The compiler can figure out that `x` is a `double` value. It looks at `3.0` and `1.5` and sees that they're of type `double`. Then it notices that `2` is an `int`, which the compiler can convert *implicitly* to a `double` for the calculation. All of the addition terms in `x`'s initialization expression end up as doubles. So the *inferred type* of `x` is `double`.

But now, you can simply utter the magic word `var` and supply an initialization expression, and the compiler does the rest:

```
~~~
var aVariable = <initialization expression here>;
~~~
```

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_68_0.png)

If you've worked with a scripting language such as JavaScript or VBScript, you may have gotten used to all-purpose-in-one data types. VBScript calls them Variant data types — a variant can be anything at all. But does `var` in C# signify a Variant type? Not at all. The object you declare with `var` definitely has a C# data type, such as `int`, `string`, or `double`. You just don't have to declare what it is.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_68_1.png)

The `UsingVarForImplicitTypeInference` example on the Web site demonstrates with several examples. Here's a taste.

What's really lurking in the variables declared in this example with `var`? Take a look at this:

```
var aString = "Hello C# 3.0";
Console.WriteLine(aString.GetType().ToString());
```

The mumbo jumbo in that WriteLine statement calls the String.GetType() method on aString to get its C# type. Then it calls the resulting object's ToString() method to display the object's type. (Yadda yadda.) Here's what you see in the console window:

```
System.String
```

It proves that the compiler correctly inferred the type of aString.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_68_2.png)

Most of the time, I recommend that you don't use `var`. Save it for when it's necessary. Being explicit about the type of a variable is clearer to anyone reading your code than using `var`. However, common usage in the C# world may change so much that everybody uses `var` all the time, in spite of my good advice. In that case, you can go along with the crowd.

You see examples later in which `var` is definitely called for, and I use it part of the time throughout this book, even sometimes where it's not strictly necessary. You need to see it used, and use it yourself, to internalize it. I'm still getting used to it myself. (I can't help it if I'm a slow learner.)

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_68_3.png)

You can see `var` used in other ways: with arrays and collections of data, in Chapter 6 of this minibook, and with anonymous types, in Book II. Anonymous? Bet you can't wait.

What's more, a new type in C# 4.0 is even more flexible than `var`: The dynamic type takes `var` a step further.

The `var` type causes the compiler to infer the type of the variable based on expected input. The `dynamic` keyword does this at runtime, using a totally new set of tools called the Dynamic Language Runtime. You can find more about the dynamic type in Book VIII.
