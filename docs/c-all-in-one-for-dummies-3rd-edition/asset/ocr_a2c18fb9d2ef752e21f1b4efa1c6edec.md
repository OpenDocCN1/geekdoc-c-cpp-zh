# Using the auto keyword with other types

The auto keyword can be used in any situation where you want to define the type of a variable. For example, you could use it in a for loop should you wish to do so, as shown in the AutoKeyword example:

```
for (auto i = 0; i < 8; i++)
    cout << i << endl;
```

Depending on your compiler, when you view i in the debugger, you find that the compiler has made it an int — the same type you would have used when choosing the type manually. Of course, you probably won't use the auto keyword in this manner because typing int is actually shorter than typing auto. Even so, you can use auto anywhere the compiler can determine the type of a variable based on the variable's context. Even something as simple as this following code (also part of the AutoKeyword example) works just fine.

```
auto Greeting = "Hello";
cout << Greeting << endl;
```

In this case, the compiler will create a const char * variable for you. However, there is a problem with this particular bit of code. If you were to assume that the compiler has created a string instead, you might write code like this:

```
auto Greeting = "Hello";
cout << Greeting.length() << endl;
```

Making the wrong assumption means the code won’t compile. You receive an error message stating, error: request for member ‘length’ in ‘Greeting’, which is of non-class type ‘const char*’. To obtain the string that you need, you must specifically declare the variable as type string.

Sometimes you also get the wrong type in situations that aren’t quite so clear. For example, the following code should rely on a long long data type.

```
auto LargeNumber = 15;
LargeNumber += 2147483647;
cout << LargeNumber << endl;
```

When you run the code and get an answer of -2147483634, which is clearly wrong. The problem here is that the compiler assumes you want an int variable. To obtain the long long variable you need, you must specifically declare the variable as type long long. When you run the example using a long long variable, you get the correct output of 2147483662.

# Developing Applications with Lambda Expressions

The previous section of the chapter acquaints you with the essentials of working with lambda expressions. There are a number of ways in which you can expand a lambda expression to meet specific needs. The following sections show how to use some of the more common methods.

# Creating lambda expressions with multiple inputs

Some lambda expressions require that you provide multiple inputs. The two most common examples are checks for equality and sorting algorithms. However, any instance where you must compare one value to another in

+   - Book IV
+   - Chapter 7
+   - Working with Lambda Expressions