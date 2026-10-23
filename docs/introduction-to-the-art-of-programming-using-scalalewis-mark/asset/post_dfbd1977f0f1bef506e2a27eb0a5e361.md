
| Type | e Bits | m Bits | bias | Min | Max |
|------|--------|--------|------|-----|-----|
| Float | 8 | 23 | 127 | -3.4028235E38 | 3.4028235E38 |
| Double | 11 | 52 | 1023 | -1.7976931348623157E308 | 1.7976931348623157E308 |

## TABLE 3.2: Floating point types with sizes and ranges.

means that comparisons between floating point values can be done with the same logic used for integer values with the same number of bits. All remaining bits are used to store a MANTISSA, m. The stored mantissa is the fractional part of the number in normalized binary. So the highest value bit is ½, the next is ¼, and so on. Table 3.2 below gives the number of bits used for e and m, the bias, and the range of numbers they can represent in the Double and Float types. The E notation is short for multiplication by 10 to that power.

As we have seen, floating point literals are by default considered to be of type Double. If you specifically need a Float you can append an f to the end of the literal. There are many other details associated with floating point values. There is only one main point that will be stressed here though. That is the fact that floating point values, whether Double or Float, are not Real numbers in the sense you are used to in math with arbitrary precision. Floating point numbers have limited precision. Like the integers, they can be overflowed. Unlike the integers, they are fundamentally imprecise because they represent fractional values with a finite number of bits.

To understand this, let us look at a situation where you should have seen this before. Consider the simple fraction, ⅓. Now consider the representation of this value as a decimal. The decimal representation is 0.33333... In order to write this fraction accurately in decimal, you need an infinite number of digits. In math we can denote things like this by putting in three dots or putting a line over the digits that are repeated. For floating point values though, the digits simply cut off when you get to the end of the mantissa. As such, they are not exact and the circuitry in the computer employs a rounding scheme to deal with this. This imprecision is not visible most of the time, but one immediate implication of it is that you can not trust two floating point numbers to be equal if they were calculated using arithmetic. It also means that you should not use floating point numbers for programs that involve money. The decimal value 0.1 is a repeating fraction in binary and as such, is not perfectly represented. That is generally considered a bad thing when dealing with people's money. Instead you should use an integer type and store cents instead of dollars.

## 3.5 The math Object

While on the topic of numbers, there are quite a few standard functions that you might want to do with numbers beyond addition, subtraction, multiplication, and division. There are a few other things you can get from operators that we will discuss later. Things like square root, logarithms, and trigonometric functions are not operators. They are found as methods in the math object. You can use tab completion in the REPL to see all the different methods that you can call on math.

```
scala> math.
```

BigDecimal

BigInt

- E
- Fractional
- Integral
- Numeric
- Ordering
- PartiallyOrdered
- ScalaNumber
- abs
- asin
- atan2
- ceil
- cosh
- expm1
- hypot
- log10
- max
- package
- random
- round
- sin
- sqrt
- tanh
- toRadians
- Equiv
- IEEEremainder
- LowPriorityOrderingImplicits
- Ordered
- PartialOrdering
- Pi
- ScalaNumericConversions
- acos
- atan
- cbrt
- cos
- exp
- floor
- log
- log1p
- min
- pow
- rint
- signum
- sinh
- tan
- toDegrees
- ulp

Many of these probably do not make sense right now and you should not worry about them. However, many of them should be identifiable by the name. So if we wanted to take a square root of a number, we could do the following.

```
scala> math.sqrt(9)
res15: Double = 3.0
```

You would use a similar syntax for taking cosines and sines. The functions provided in the math object should be sufficient for the needs of most people. Only two of the contents of math that start with capital letters are worth noting at this point. Pi and E are numeric constants for π and e.

```
scala> math.Pi
res16: Double = 3.141592653589793
```

## 3.6 Details of Char and String

There is a lot more to Char and String than we covered in section 3.3. Some of it you really should know before we go further. We saw how we can make character literals or string literals that contain keys that appear on the keyboard and that go nicely into a text file. What about things that we can not type as nicely or that have other meanings? For example, how do you put double quotes in a String? Typing the double quote closes off the string literal instead of putting one in. How would you make a character of a single quote? How do you get a new line? You are not allowed to have a normal string break across lines.

We can do all of these things and more with ESCAPE CHARACTERS. These are denoted by a backslash in front of one or more characters. For example, if you want to put a double

quote in a string, simply put a backslash in front of the double quote. The same thing is true for a single quote in a character. You can insert a newline with a \n. What if you want to insert a backslash itself? Simply put in two backslashes. Table 3.3 shows other commonly used escape characters.

| Literal | Meaning | Unicode Hex Encoding |
| :--- | :--- | :--- |
| `\b` | backspace | `\u0008` |
| `\f` | form feed | `\u000C` |
| `\n` | line feed | `\u000A` |
| `\r` | carriage return | `\u000D` |
| `\t` | tab | `\u0009` |
| `\"` | double quote | `\u0022` |
| `\'` | single quote | `\u0027` |
| `\\` | backslash | `\u005C` |

**TABLE 3.3:** Table of special character escape sequences in Scala.

In addition to escape characters, the backslash can be used to put any type of special character into a string. If you know the Unicode value for a special character, you can put \u followed by four hexadecimal digital in a string to specify that character. For characters from the lower 256 characters that are represented in ASCII you can follow the backslash by an octal number between 0 and 377.

There are some times when using the escape characters becomes a pain. For example, there are times when you need to build strings that have a number of backslashes. Each one you want requires you to put in two. This can get unwieldy. In addition, if you have a long, multiline string, it can be difficult to format the string the way you want. For these types of situations, Scala includes a special form of string that begins and ends with three double quotes. Anything you type between the set of three double quotes is taken to be literally part of the string without alteration. The following shows an example of using this to enter a long string in the REPL.

```
scala> """This is a long string.
| It spans multiple lines.
| If I put in \n and \\ or \" they are taken literally."""
res8: java.lang.String =
This is a long string.
It spans multiple lines.
If I put in \n and \\ or \" they are taken literally.
```

## 3.7 Naming Values and Variables

We have seen enough that you can solve some simple problems. For example, if you were given a number of different grades and asked to find the average, you could type in an expression to add them all up and divide by the number of them to get the average. We basically have the ability to use Scala now to solve anything we could solve with a calculator. We will develop a lot more over time, but we have to start somewhere. As it stands we are not just limited to solving problems we could do with a calculator, we are solving them the way we would with a calculator. We type in mathematical expressions the way we would write them on paper and get back an answer. Real programming involves tying together multiple lines of instructions to solve larger problems. In order to do this, we need to have a way to give names to the work we have done and refer back to them.

There are three keywords in Scala that give names to values. We will see the first two here: val and var. To begin with, let us look at the full syntax of val and var in two samples. Then we can pull them apart, talk about what they do, see how they are different, and discuss what parts of them are optional.

```
scala> val age:Int=5
age: Int = 5
```

```
scala> var average:Int=(2+3+4+5)/4
average: Int = 3
```

Syntactically the only difference between these two is that one says val and the other says var. That is followed by a name with a colon and a type after it. The rules for names in Scala are that they need to start with a letter or an underscore followed by zero or more letters, numbers, and underscores. Scala is also case sensitive. So the names AGE, age, Age, and agE are all different. In general it is considered very poor style to use names that differ only in capitalization. Scala borrows a standard naming convention from Java called camel case. The names of values begin with a lower case letter and the first letter of subsequent words are capitalized. For example, theClassAverage is a name that follows this convention. Type names use the same convention except that the first letter is capitalized. This is called camel case because the capital letters look like humps.

The types in both of these examples are followed by an equals sign and an expression. Unlike many other programming languages, this is not optional in Scala. In Scala, when you declare a val or var, you must give it an initial value at that point.³

While the initial value is not optional, the type generally is. This too is unlike most programming languages. As we have already seen, Scala is able to figure out the types of things for us in many situations. If we leave off the colon and the type, Scala will simply use whatever type it determines is appropriate for the expression in the initial value. Most of the time, the type that it gives us will be exactly what we want. Using this we could instead have the following shorter forms of these declarations.

```
scala> val age=5
age: Int = 5
```

```
scala> var average=(2+3+4+5)/4
average: Int = 3
```

The reason for using a val or var declaration is that they give a name to the value that we can refer back to later. For example, we could now type in age+10 and Scala would give us 15. The names serve two purposes. They prevent us from typing in expressions over and over again. They also help give meaning to what we are doing. You should try to pick names that help you or other readers figure out what is going on with a piece of code.

So far we have discussed all the similarities between val and var and you might be wondering in what way they are different. The declarations themselves are basically identical. The difference is not in the syntax, but in the meaning, or semantics. A val declaration gives a name to a reference to a value. That reference can not be changed. It will refer to

> 3 There are very good reasons for requiring initialization of variables. Even in languages that do not require it, a programmer can make his/her life a lot easier by initializing all variables at creation. The declaration and initialization should ideally happen at the point where you have a real value to put into the variable. This prevents many errors and as a result, can save you a lot of time in your programming.
