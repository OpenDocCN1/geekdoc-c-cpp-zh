
```python
>>> spam
['bacon', 'and', 'eggs', 42, 10]
>>> del spam[1]
>>> spam
['bacon', 'eggs', 42, 10]
>>> spam[0]
'bacon'
>>> spam[1]
'eggs'
>>> spam[2]
42
>>> spam[3]
10
```

Lists automatically “fix” themselves after each item deletion. That means you won’t see any gap in the numbering of items.

## *Tuples*

Tuples and lists are similar except for one thing: tuples cannot be edited. After creating a tuple, you won't be able to change it in any way. You can't expand, edit, or delete the elements within a tuple. If you'll ignore this immutability, you can say that lists and tuples are identical.

You should use commas when declaring tuples:

```
unchanging = "rocks", 0, "the universe"
```

Sometimes, you have to differentiate tuples using parentheses. This process is similar to performing several assignments using the same line. Here's a simple example:

```
foo, bar = "rocks", 0, "the universe" # 3 elements here
foo, bar = "rocks", (0, "the universe") # 2 elements here because the second element is a tuple
```

## Strings

You’ve already learned about strings. However, it is important to discuss it again as a Python sequence. For other programming languages, you can access the characters elements inside strings using square brackets (known as the subscript operator). This method is also effective in Python:

```text
>>> "Hello, world!"[0]
'H'
>>> "Hello, world!"[1]
'e'
>>> "Hello, world!"[2]
'l'
>>> "Hello, world!"[3]
'l'
>>> "Hello, world!"[4]
'o'
```

Python assigns numbers to indices using this formula: 0 – n-1 (n represents the number of characters in the string). Check the screenshot below:

![](img/4fa8a5f30786d4f308acc92572dd6e8f_503_0.png)

Indices work with the characters that come right after them. For negative indices, you should count backwards:

```text
>>> "Hello, world!"[-2]
'd'
>>> "Hello, world!"[-9]
'o'
>>> "Hello, world!"[-13]
'H'
>>> "Hello, world!"[-1]
'!'
```

Unlike other programming languages, Python allows you to place up to 2 numbers inside square brackets. You can do this using a colon (i.e. “:” ). For sequences that concentrate on numeric indices, the combination of brackets and colons returns the portion between the indices. This technique is called “slicing.” If you’ll slice a string, you will get “substrings.” Analyze the screenshot below:

```
>>> "Hello, world!"[3:9]
'lo, wo'
>>> string = "Hello, world!"
>>> string[:5]
'Hello'
>>> string[-6:-1]
'world'
>>> string[-9:]
'o, world!'
>>> string[:-8]
'Hello'
>>> string[:]
'Hello, world!'
```

The statements given above show an important rule:

> “ If you ’ ll omit a number, Python assumes the missing number as the start or end of that particular sequence (depending on the position of the missing number). ”

## Dictionaries

Dictionaries are similar to lists. Unlike tuples, dictionaries allow users to modify their content. That means you may add, edit, and delete the elements of any dictionary. The main difference between lists and dictionaries is this: dictionaries don’t bind their elements to any number.

A dictionary’s element has two aspects: (1) the key and (2) the value. If you’ll call the key of a dictionary, you’ll get the values related to that particular key. Computer programmers consider lists as special dictionaries, where numbers represent the key of each element.

## How to Use a Dictionary

You should use curly braces when declaring a dictionary. Also, you should use the following format when declaring elements for a dictionary: (1) enter the key of the element, (2) add a colon, and (3) assign the value. Here’s an example:

```
>>> definitions = {"guava": "a tropical fruit", "python": "a programming language", "the answer": 42}
>>> definitions
{'python': 'a programming language', 'the answer': 42, 'guava': 'a tropical fruit'}
>>> definitions["the answer"]
42
>>> definitions["guava"]
'a tropical fruit'
>>> len(definitions)
3
```

Additionally, adding elements to dictionaries is simple and easy. It’s like adding an ordinary variable:

```
>>> definitions["new key"] = "new value"
>>> definitions
{'python': 'a programming language', 'the answer': 42, 'guava': 'a tropical fruit', 'new key': 'new value'}
```

## Chapter 5: The Different Types of Data

Basically, data types define an object ’ s capabilities. In other languages, the effectiveness of an operation is tested by ensuring that the object cannot be stored where the operation is going to be performed. This system is known as static typing.

However, Python uses a different approach. This programming language allows you to store the object ’ s data type inside that object. Python also checks the validity of each operation as soon as you run them. Programmers refer to this system as dynamic typing.

This chapter focuses on the different kinds of data that you can use with Python.

## The Standard Types

Python has a set of standard data types. These types are pre-installed into this programming language. Let ’ s divide these types into small groups. This section will use the hierarchy system used in Python ’ s official documentation:

## The Numeric Types

- int – This stands for integers. For Python 2.x, “ int ” is identical to C longs.
- long – It stands for long integers whose length is non-limited. You ’ ll find this type in systems that use Python 2.x.
- float – This stands for floating-point numbers. Float is the equivalent of doubles in C.
- complex – This type is composed of complex numbers.

## The Sequences

- list
- tuple
- byte – This is a sequence of numbers within the 0-255 range. You ’ ll find bytes in systems that use Python 3.x.
- byte array – This is the mutable version of bytes.
- str – This stands for " String." Python 2.x systems represent strings as sequences of 8-bit items. Python 3.x systems, however, represent them as sequences of Unicode items.

## The Sets

- set – This is an unorganized group of distinct objects.
- frozen set – This type is the immutable version of sets.

## The Mappings

- dict – This stands for Python dictionaries. Computer programmers refer to this type as a " hashmap " or " associative array." In general, each element of a dictionary has a corresponding definition.

## Mutable and Immutable Objects

In the Python language, data types are categorized based on the mutability of their contents. Keep in mind that immutable data types prevent you from changing the objects inside them. That means you ’ ll succeed in slicing or reassigning the objects of mutable data. Immutable ones, however, will give you an error message.

Here ’ s an important principle that you should remember: variables are simple references to the objects inside a machine ’ s memory. Let ’ s assume that you paired an object and a variable using the following statement:

```
a = 1
s = 'abc'
l = ['a string', 456, ('a', 'tuple', 'inside', 'a', 'list')]
```

With the statement given above, you are making variables (i.e. 1, a, and s) point to certain objects. Python stores this relationship between variables and objects in the machine ’ s memory. Thus, you can conveniently access objects whenever you want.

For the next example, let ’ s say you performed a reassignment using the code below:

```
a = 7
s = 'xyz'
l = ['a simpler list', 99, 10]
```

In this new statement, you linked the variables to other objects. As you ’ ve learned earlier, you can only change mutable objects (l [0] = 1 is good, but s [0] = “ a ” will give you an error message).

## How to Create Objects of a Defined Type

- *Literal Integers* – You can enter literal integers in three different ways:
  - For decimal numbers – You can enter these numbers directly.
  - For hexadecimal numbers – You have to prepend 0X or 0x to enter this kind of number.
  - For octal literals – The method of entering these integers depends on the Python version you are using:
    - For Python 2.x – You must prepend a zero to enter octals.
    - For Python 3.x – You should prepend 0o or 0O to enter octals.
- *Floating Point Integers* – You can enter these numbers directly.
- *Long Integers* – You can enter a long integer in two ways:
  - Directly (112233445566778899 is considered as a long integer)
  - By appending the letter “ L ” (1L is considered as a long integer).

If a computation that involves short integers overflows, it is automatically converted into a long integer.

- *Complex Numbers* – You can enter this object by adding two numbers (i.e. a real number and an imaginary number). Then, enter these numbers by appending the letter “ j .” That means 11+2j and 11j are complex numbers.
- *Strings* – You can enter strings as single- or triple-quoted objects. The difference between these two types lies in their delimiters and their potential length. Single-quoted strings are restricted to one line only. You can enter single-quoted strings using pairs of single quotation or double quotation marks. Check the following example:

```
'foo' works, and
"moo" works as well,
but
'bar" does not work, and
"baz' does not work either.
"quux'' is right out.
```
