In Listing 9-1, later in this chapter, we show you how you can convert between numbers and strings. Book I, Chapter 7 shows some sample code for converting a number to a string. Here we employ that same technique along with a similar technique for converting a string back to a number.

Converting strings is an interesting concept in C++ because an outstanding feature lets you *write to* and *read from* a string just as you would to and from a console. For example, although you can write a number 12 out to a console by using code like this:

```
cout << 12;
```

you can actually do the same thing with strings: You can write a number 12 to a string, as in

```
mystring << 12;
```

After this line runs, the string contains the value "12". However, to do this, you need to use a special form of string called a stringstream. In the never-ending world of computer terminology, a stream is something that you can write to and read from a flowing fashion (think about bits flowing through a wire — much as a stream flows along a waterbed). For example, you might write the word "hello" to a stringstream, and then the number 87, and then the word "goodbye". After those three operations, the string contains the value "hello87goodbye".

And you can similarly read from a stream. In the section “Reading from the Console,” later in this chapter, we show you how you can read from a console by using the > notation. When you read from the console, although your application stops and waits for the user to enter something, the real stream technology takes place *after* the user types something: After the console has a series of characters, your application reads in the characters as a stream, one data type after other. You can read a string, and then a series of numbers, and another string, and so on.

With stringstream, you can do something similar. You would fill the string with something, rather than having the user fill it, as in the case of a console. From there, you can begin to read from the string, placing the values into variables of different types. One of these types is integer. But because the stringstream is, at heart, just a string, that’s how you convert a string of digits to an integer: You put the digit characters in the string and read the string as a stream into your integer. Snazzy!

The only catch to using these is that you need to know in advance which kind of streaming you want to do. If you want to write to the stringstream, you create an instance of a class called ostringstream. (The o is for output.) If you want to read from a stringstream, you create an instance of a class called istringstream. (The i is for input.)