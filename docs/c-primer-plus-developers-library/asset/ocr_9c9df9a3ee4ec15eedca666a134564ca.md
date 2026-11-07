# ## Which cin.get() Should You Use?

Listing 4.5 in Chapter 4 uses this code:

```
~~~cpp
char name[ArSize];
...
cout << "Enter your name:\n";
cin.get(name, ArSize).get();
~~~
```

The last line is equivalent to two consecutive function calls:

```
~~~cpp
cin.get(name, ArSize);
cin.get();
~~~
```

One version of cin.get() takes two arguments: the array name, which is the address of the string (technically, type char*), and ArSize, which is an integer of type int. (Recall that the name of an array is the address of its first element, so the name of a character array is type char*.) Then the program uses cin.get() with no arguments. And most recently, we've used cin.get() this way:

```
~~~cpp
char ch;
cin.get(ch);
~~~
```

This time cin.get() has one argument, and it is type char.

Once again it is time for those of you familiar with C to get excited or confused. In C if a function takes a pointer-to-char and an int as arguments, you can't successfully use the same function with a single argument of a different type. But you can do so in C++ because the language supports an OOP feature called function overloading. Function overloading allows you to create different functions that have the same name, provided that they have different argument lists. If, for example, you use cin.get(name, ArSize) in C++, the compiler finds the version of cin.get() that uses a char* and an int as arguments. But if you use cin.get(ch), the compiler fetches the version that uses a single type char argument. And if the code provides no arguments, the compiler uses the version of cin.get() that takes no arguments. That's

Function overloading enables you to use the same name for related functions that perform the same basic task in different ways or for different types. This is another topic awaiting you in Chapter 8. Meanwhile, you can get accustomed to function overloading by using the get() examples that come with the iostream class. To distinguish between the different function versions, we'll include the argument list when referring to them. Thus, cin.get() means the version that takes no arguments, and cin.get(char) means the version that takes one argument.

# ## The End-of-File Condition

As Listing 5.17 shows, using a symbol such as # to signal the end of input is not always satisfactory because such a symbol might be part of legitimate input. The same is true of other arbitrarily chosen symbols, such as @ and $. If the input comes from a file, you can employ a much more powerful technique—detecting the end-of-file (EOF). C++ input