Since an object can be assigned the value of another object of the same class, we can use statements like:

```
s1 = s2;
```

to assign one string to another.

The first constructor:

```
String::String();
```

is the default constructor that takes no arguments. It places a '\0' in the first array element to create an empty string. It is invoked by:

```
String s1;
```

The second constructor creates the String object s2 and copies the characters in the constant into the data member str. It is invoked by:

```
String s2("Hello, world.");
```

Two alternate formats for calling this one-arg constructor are:

```
String s2 = "Hello, world.";
String s2 = String("Hello, world.");
```

Whichever format is used, this constructor effectively converts a string to a String, i.e., a normal string constant to an object of class String.