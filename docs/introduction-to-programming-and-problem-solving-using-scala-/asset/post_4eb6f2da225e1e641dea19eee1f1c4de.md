
# Introduction to Programming and Problem-Solving Using Scala

This line involves three tokens. Each character in this case is a separate token. If you space out, it will not change the result. However, if you use a number with multiple digits, all the digits are a single token and inserting spaces change the meaning.

There should not be anything surprising about the result of 5+6. We get back a value of 11, and it has a type of Int. Try the basic arithmetic operations of -, \*, and /. You will notice that you are keeping values of type Int. This makes sense for addition, subtraction, and multiplication. However, the result of 5/2 might surprise you a little bit. Normally you would think of this expression as a Double, if you ask Scala for the result of 5/2 it will tell you that the Int is 2. Why is it, and what happened to the 0.5? When both operands are of type Int, Scala keeps everything intact. In the case of division, the fractional part is thrown away. Note that it is not rounded, but truncated. Why? It is because in integer arithmetic, the value of 5/2 is not 2.5. It is 1. That is what says when you divide five by two, you get two groups of two with one remainder. At some point in your elementary education, when you first learned about division, at that time you only had integers to work with this is what made sense.

Scala is doing what you did when you first learned division. It is giving you the whole part of the quotient with the fractional part removed. This fractional part is normally expressed as a remainder. There is another operation called modulo that gives the remainder after division. Here we can see it in action.

```scala
scala> 5/2
res3: Int = 1
```

The modulo operator is used quite a bit in computing because it is rather handy for presenting ideas. You should take some time to re-familiarize yourself with it. You might be tempted to say that this would be your first time dealing with it, but in reality, this is exactly how you did division before you learned about decimal notation for fractions.

What if you really wanted 2.5 for the division? Well, 2.5 in Scala is a Double. We can get this by doing division on Doubles.

```scala
scala> 5.0/2.0
res4: Double = 2.5
```

All of our numeric operations work for Doubles as well. Play around with them and see how they work. You can also build larger expressions. In multiple operators, use some parentheses.

What happens when you combine a Double and an Int in an expression. Consider this example:

```scala
scala> 5.0/2
res5: Double = 2.5
```

Here we have a Double divided by an Int. The result is a Double. When you combine numeric values in expressions, Scala will change one to match the other. The choice of which to change is fairly simple. It changes the one that is more restrictive. In this case, anything that is an Int is also a Double, but not all values that are Doubles are Ints. So the logical path is to make the Int into a Double and do the operation that way.

## 2.3 Objects and Methods

One of the features of the Scala language is that all values in Scala are OBJECTS. The term object in reference to programming language means something that combines data and the functionality on data in a single entity. In Scala we refer to the things that object knows how to do as METHODS. The normal syntax for calling a method on an object is to follow the object by a period (".dot") and the name of the method. Some methods need extra information, which we called arguments. If a method needs ARGUMENTS they are put after the method in parentheses.

In Scala, even the most basic literals are treated as objects in our program, and we can therefore call methods on them. An example of when we need this is when to convert one type to another. In the sample below we convert the Double 5.6 into an Int by calling the toInt method. In this context we would generally use an Int literal, but there will be situations we encounter later on where we are given values that are Doubles and we need to convert them to Ints. We will be able to do that with the toInt method.

```scala
scala = 5.6.toInt
res: Int = 5
```

One thing you should note about this example is that converting a Double to an Int does not round. This operation performs a truncation. Any fractional part of the number is cut off and only the whole integer is left.

We saw at the beginning of this chapter that Scala is flexible when it comes to the requirement of putting semicolons at the end of statements. Scala will insert a semicolon at the end of a line if one makes a sense. This type of behavior makes code easier to write.

Methods that take one argument can be called using "infix" notation. This notation leaves off the dot and parentheses, and simply places the method between the object it is called on and the argument. If the method name uses letters, space will be required by the programmer with significant flexibility. Though you did not realize it, you were using "infix" notation in the last section. To see this, which makes certain parts of Scala more coherent and provides, go into Scala and type "5." then press Tab. The REPL has tab completion just like the command, so what you see is a list of all the methods that could be called on the Int. It should look like the following.

```scala
scala = 5.
% + >>> isInstanceOf Double toLong unary_
& - >= isInstanceOf Byte toFloat toShort unary_
* / >> isInstanceOf Char toInt toString unary\_
```

You have already seen and used some of these methods. We just finished using toInt on a Double. We can call Double on an Int as well. The things that stand out are the basic math operations that were used in the previous section. The +, -, *, /, and % we above are nothing more than methods on the Int type. The example 5+6 is really 5 .+ (6). In fact, you can type this into Scala and see that you get the same result.

```scala
scala = 5 . + (6)
res: Int = 11
```

## 2.4 Other Basic Types

Not everything in Scala is a number. There are other non-numeric types in Scala which also have literals. We will start simple and move up in complexity. Perhaps the simplest type in Scala is the Boolean type. Objects of the Boolean type are either true or false, and those are also valid literals for Booleans.

```scala
scala true
res8: Boolean = true
```

```scala
scala false
res9: Boolean = false
```

We will see a lot of Booleans and what we can do with them in chapter 3 when we introduce Boolean logic.

Another type that is not explicitly numeric is the Char type. This type is used to represent single characters. We can make characters literals by placing the character inside single quotes like we see here.

```scala
scala 'a'
res10: Char = a
```

The way computers work, all character data is really numbers, and different numbers correspond by by using the toInt method. As you can see from the line below, the lowercase “a” has a numeric value of 97.

```scala
scala 'a'.toInt
res11: Int = 97
```

Because characters have numeric values associated with them, we can also do math with them. When we do this, Scala will convert the character to its numeric value as an Int and then do the math with the Int. The result will be an Int, as seen in this example.

```scala
scala 'a'+1
res12: Int = 98
```

In the last section you might have noticed that the Int type has a method called toChar. We can use this to get back from an integer value to a character. You can see from the following example that you add 1 to “a” you get the logical result of “b”.

```scala
scala ('a'+1).toChar
res13: Char = b
```

## Scala Basics

An object of the String type can be a single character. If you try to put more than one character inside single quotes you will get an error. There are lots of situations when you want to represent many characters. String literals are formed by putting double quotes like we see here.

```scala
scala= "Scala is a programming language"
res14: String = Scala is a programming language
```

Notice that the type is listed as String. Certain operations that look like mathematical operations are supported for Strings. For example, when you use + with Strings, it does concatenation. That is to say it gives back a new string that is the combined characters of the two. This type of operation works with other types as well. The next example shows what happens when we concatenate a String with an Int. The Int is converted to a String, using the toString method, and normal concatenation.

```scala
scala= "abc"+123
res16: String = abc123
```

This works when the String is the first or second argument of the +.

```scala
scala= 123+"abc"
res17: String = 123abc
```

In addition to concatenation, you can multiply a string by an integer, and you will get back a new string that has the original string repeated the specified number of times.

```scala
scala= "abc"*6
res18: String = abcabcabcabc
```

This can be helpful for things such as padding values with the proper number of spaces to make a string a specific length. You can do this by "multiplying" the string " " by the number of spaces you need.

The infix notation for calling a method was introduced earlier. We can show another example of this using the String type and the substring method. As names implies, substring returns a portion of a String. There are two versions of it. One takes a Int argument and returns everything from that index to the end of the String. Here you can see that being called both regular notation and the infix notation.

```scala
scala= "abcd".substring(2)
res19: String = cd
```

```scala
scala= "abcd" substring 2
res20: String = cd
```

> The way you are running this, the real type is a java.lang.String. Scala integrates closely with Java and uses some of the Java library elements in standard code. This allows you to freely call code from the Java libraries, a fact that has been significant in the adoption of Scala.
