# Creating and Concatenating Strings

The `String` class in the .NET Framework provides a number of methods that enable you to create or concatenate strings.

The most direct way of concatenating two strings is to use the “+” operator, like this:

```
    string str1 = "Hello ";
    string str2 = "world!";
    string str3 = str1 + str2;
    Console.WriteLine(str3); //---Hello world!---
```

The `String.Format()` static method takes the input of multiple objects and creates a new string. Consider the following example:

```
    string Name = "Wei-Meng Lee";
    int age = 18;
    string str1 = string.Format("My name is {0} and I am {1} years old",
                            Name, age);

    //---str1 is now "My name is Wei-Meng Lee and I am 18 years old"---
    Console.WriteLine(str1);
```

Notice that you supplied two variables of `string` and `int` type and the `Format()` method automatically combines them to return a new string.

The preceding example can be rewritten using the `String.Concat()` static method, like this:

```
    string str1 = string.Concat("My name is ", Name, " and I am ", age ,
                            " years old");
    //---str1 is now "My name is Wei-Meng Lee and I am 18 years old"---
    Console.WriteLine(str1);
```

> > **Strings Are Immutable**
> >
> > In .NET, all string objects are *immutable*. This means that once a string variable is initialized, its value cannot be changed. And when you modify the value of a string, a new copy of the string is created and the old copy is discarded. Hence, all methods that process strings return a copy of the modified string — the original string remains intact.
> >
> > For example, the `Insert()` instance method inserts a string into the current string and returns the modified string:
> >
> >     str1 = str1.Insert(10, "modified ");
> >
> > In this statement, you have to assign the returned result to the original string to ensure that the new string is modified.