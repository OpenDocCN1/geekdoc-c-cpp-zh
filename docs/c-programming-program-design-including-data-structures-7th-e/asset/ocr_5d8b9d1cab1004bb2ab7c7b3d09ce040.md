```
```cpp
private:
    string courseName;
    string courseNo;
    int courseCredits;
};
```
```

Let us note the following:

+   - If a member of a class is a variable, you declare it just like any other variable. Also, in the definition of the class, you cannot initialize a variable when you declare it.
+   - If a member of a class is a function, you typically use the function prototype to declare that member.
+   - If a member of a class is a function, it can (directly) access any member of the class—member variables and member functions. That is, when you write the definition of a member function, you can directly access any member variable of the class without passing it as a parameter. The only condition is that you must declare an identifier before you can use it.

In C++, `class` is a reserved word, and it defines only a data type; no memory is allocated. It announces the declaration of a class. Moreover, note the semicolon (`;`) after the right brace. The semicolon is part of the syntax. A missing semicolon, therefore, will result in a syntax error.

The members of a `class` are classified into three categories: `private`, `public`, and `protected`. This chapter mainly discusses the first two types, `private` and `public`.

In C++, `private`, `protected`, and `public` are reserved words and are called member access specifiers.

Following are some facts about `public` and `private` members of a class:

+   - By default, all members of a class are `private`.
+   - If a member of a class is `private`, you cannot access it directly from outside of the class. (Example 10-1 illustrates this concept.)
+   - A `public` member is accessible outside of the `class`. (Example 10-1 illustrates this concept.)
+   - To make a member of a class `public`, you use the member access specifier `public` with a colon, `:`.

Suppose that we want to define a class to implement the time of day in a program. Because a clock gives the time of day, let us call this class clockType. Furthermore, to represent time in computer memory, we use three `int` variables: one to represent the hours, one to represent the minutes, and one to represent the seconds.

Suppose these three variables are:

```
```cpp
int hr;
int min;
int sec;
```
```