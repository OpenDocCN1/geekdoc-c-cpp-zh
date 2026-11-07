```
"@" object deleted, -1 left
"-" object deleted, -2 left
End of main()
```

Because automatic storage objects are deleted in an order opposite to that in which they are created, the first three objects deleted are knots, sailor, and sport. The knots and sailor deletions look okay, but for sport, Dollars has become Dollars. The only thing the program does with sport is use it to initialize sailor, but that appears to have altered sport. And the last two objects deleted, headline2 and headline1, are unrecognizable. Something messes up these strings before they are deleted. Also the counting is bizarre. How can there be −2 objects left?

Actually, the peculiar counting is a clue. Every object is constructed once and destroyed once, so the number of constructor calls should equal the number of destructor calls. Because the object count (num_strings) is decremented two times more than it is incremented, a constructor that doesn’t increment num_strings must be creating two objects. The class definition declares and defines two constructors (both of which increment num_strings), but it turns out that the program uses three constructors! For example, consider this line:

```
StringBad sailor = sport;
```

What constructor is used here? Not the default constructor, and not the constructor with a const char * parameter. Remember, initialization using this form is another syntax for the following:

```
StringBad sailor = StringBad(sports); // constructor using sports
```

Because sports is type StringBad, a matching constructor could have this prototype:

```
StringBad(const StringBad &);
```

And it turns out that the compiler automatically generates this constructor (called a copy constructor because it makes a copy of an object) if you initialize one object from another. The automatic version would not know about updating the num_strings static variable, so it would mess up the counting scheme. Indeed, all the problems exhibited by this example stem from member functions that the compiler generates automatically, so let’s look at that topic now.

# Special Member Functions

The problems with the StringBad class stem from special member functions. These are member functions that are defined automatically. In the case of StringBad, the behavior of these member functions is inappropriate to this particular class design. In particular, C++ automatically provides the following member functions:

+   - A default constructor if you define no constructors
+   - A default destructor if you don’t define one
+   - A copy constructor if you don’t define one