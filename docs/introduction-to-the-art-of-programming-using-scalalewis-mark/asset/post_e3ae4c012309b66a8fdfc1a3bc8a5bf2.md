
An object of the Char type can only be a single character. If you try to put more than one character inside of single quotes you will get an error. It is also an error to try to make a Char with empty single quotes. However, there are lots of situations when you want to be able to represent many characters, or even zero characters. This includes words, sentences, and many other things. For this there is a different type called a String. String literals are formed by putting zero or more characters inside of double quotes like we see in this example.

```
scala> "Scala is a programming language"
res14: java.lang.String = Scala is a programming language
```

Notice that the type is listed as java.lang.String. Scala integrates closely with Java and uses some of the Java library elements in standard code. It also allows you to freely call code from the Java libraries. The type String has a full name of java.lang.String, but Scala will automatically provide the java.lang part so we will generally leave it out.

Certain operations that look like mathematical operations are supported for Strings. For example, when you use + with Strings, it does string concatenation. That is to say it gives back a new string that is the combined characters of the two that are being put together as shown here:

```
scala> "abc"+"def"
res15: java.lang.String = abcdef
```

This type of operation works with other types as well. This example shows what happens when we concatenate a String with an Int. The Int is converted to a String, using the toString method, and normal string concatenation is performed.

```
scala> "abc"+123
res16: java.lang.String = abc123
```

This works whether the String is the first or second argument of the +.

```
scala> 123+"abc"
res17: java.lang.String = 123abc
```

In addition to concatenation, you can multiply a string by an integer and you will get back a new string that has the original string repeated the specified number of times.

```
scala> "abc"*6
res18: String = abcabcabcabcabcabc
```

This can be helpful for things such as padding values with the proper number of spaces to make a string a specific length. You can do this by “multiplying” the string " " by the number of spaces you need.

There are other types that are worth noting before we move on. One is the type Unit. The Unit type in Scala basically represents a non-value or a meaningless value. The equivalent in many other languages is called void. We have actually seen an example of code that uses Unit. The first program we saw in chapter 2 used a function called println. When we called println Scala did something, but did not give us back a value. This is what happens when we type in an expression that gives us back a value of Unit in the REPL.

The last type in Scala that we will deal with here is a grouping of different types called a tuple. A tuple is a sequence of a specified number of specific types. It is basically, a collection of values that is strict about how many and what type of values it has. We can

```
scala> 1500000000+1500000000
res9: Int = -1294967296
```

Mathematicians would consider this to be an error. It is actually a reflection of the way that numbers are implemented on computers. The details of this implementation can impact how your programs work, so it is worth taking a bit of time to discuss it.

At a fundamental level, all information on computers is represented with numbers. We saw this with the characters being numbers. On modern computers all these numbers are represented in BINARY, or base two. The electronics in the computer alternate between two states that represent 1 and 0 or on and off. Collections of these represent numbers. A single value of either a 0 or a 1 is called a BIT. It is a single digit in a binary number. The term BYTE refers to a grouping of 8 bits, which can represent 256 different numbers. In Scala these will be between -128 and 127. To understand this, we need to do a little review of how binary numbers work.

You have likely spent your life working with decimal numbers, or base ten. In this system, there are ten possible values for each digit: 0, 1, 2, 3, 4, 5, 6, 7, 8, and 9. Digits in different positions represent different power of ten. So the number 365 is really 3×10²+6×10¹+5×10⁰. There is nothing particularly unique about the base ten other than perhaps it relates well to the number of digits on human hands. You can just as well use other bases in which case you need an appropriate number of symbols for each digit and each position represents a power of that base.

Binary uses a base of two. For this we only need two different digits: 0 and 1. This is convenient on computers where the electronics can efficiently represent two states. The different positions represent powers of two: 1, 2, 4, 8, 16, 32, ... So the number 110101=32+16+4+1=53. This example shows how you convert from binary to decimal. Simply add together the powers of two for which the bits are one. A byte stores eight bits that would represent powers of two from 128 down to 1. The word “would” is used here because there is a significant nuance to this dealing with negative numbers that we will discuss shortly.

There are two basic approaches to converting from decimal to binary. One involves repeated subtraction of powers of two while the other involves repeated division by two. We will start with the first one and use the value 296 in decimal for the conversion. We start by finding the largest power of 2 that is smaller than our value. In this case it is 256 = 2⁸. So we will have a one in the 2⁸ position or the 9ᵗʰ digit.¹ Now we subtract and get 296 − 256 = 40 and repeat. The largest power of 2 smaller than 40 is 32 = 2⁵. So the digits for 2⁷ and 2⁶ are 0. Subtract again to get 40 − 32 = 8. We now have 8 = 2³ so the final number in binary is 100101000. This procedure is written out the way you might actually do it in figure 3.1.

The other approach is a bit more algorithmic in nature and is probably less prone to error. It works based on the fact that in binary, multiplying and dividing by 2 moves the “binary point” the same way that multiplying or dividing by 10 moves the decimal point in the decimal number system. The way it works is you look at the number and if it is odd you write a 1. If it is even you write a 0. Then you divide the number by 2, throwing away any remainder or fractional part, and repeat with each new digit written to the left of those before it. Do this until you get to 0. You can also think of this as just dividing by two repeatedly and writing the remainder as a bit in the number with the quotient being what you keep working with.

The number 296 is even so we start off by writing a 0 and divide by 2 to get 148. That is also even so write another 0. Divide to get 74. This is also even so write another 0. Divide to get 37. This is odd so write a 1. Divide to get 18, which is even so you write a

¹Remember that the first digit is 2⁰ = 1.

| Value | Power of 2 | Digit |
| 296 | 256 | 1 |
| 40 | 128 | 0 |
| 40 | 64 | 0 |
| 40 | 32 | 1 |
| 8 | 16 | 0 |
| 8 | 8 | 1 |
| 0 | 4 | 0 |
| 0 | 2 | 0 |
| 0 | 1 | 0 |

FIGURE 3.1: Illustration of the conversion from decimal to binary using the subtraction method. This method works from the top down. To get the number in binary just read down the list of digits.

| Value | Digit |
| 1 | 1 |
| 2 | 0 |
| 4 | 0 |
| 9 | 1 |
| 18 | 0 |
| 37 | 1 |
| 74 | 0 |
| 148 | 0 |
| 296 | 0 |

FIGURE 3.2: Illustration of the conversion from decimal to binary using the repeated division method. This method works from the bottom up so you get the bits in the result starting with the smallest.

## 3.4.1 Binary Arithmetic

Now that you know how to go from binary to decimal and decimal to binary, let’s take a minute to do a little arithmetic with binary numbers. It is certainly possible to do this by converting the binary to decimal, doing the arithmetic in decimal, then convert back to binary. However, this is quite inefficient and not worth it because it really is not hard to work in binary. If anything, it is easier to work in binary than in decimal. Let us begin with the operation of addition. Say we want to add the numbers 110101 and 101110. To do this you do exactly what you would do with long addition in decimal. The difference is that two in binary is 10 so there is a lot more carrying.

```
110101
+ 101110
------
1100011
```
