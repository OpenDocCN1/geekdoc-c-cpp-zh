```
}
catch (char CharEx)
{
    cout << "Character exception" << CharEx << "is caught \n";
}
```

```
catch (...)
{
    cout << "Anything thrown is caught here \n";
}
```

This is a better design because in this case it is possible to take care of exceptions of one’s interest in the usual manner. If anything other than what is expected is thrown, it can be taken care of as well by the catch all block. The catch all section is very useful in debugging and is as useful as a default statement in switch.

# 8.10 RESTRICTING EXCEPTIONS FROM FUNCTIONS: EXCEPTION SPECIFICATION

It is possible to specify what kind of exceptions can be thrown from the functions using a specific syntax. The function definition header can be appended with the keyword throw and the possible types of expressions to be thrown in the parenthesis. It is known as exception specification. In the following example, the function ExGen() is allowed to throw only int and char exceptions.

```
void ExGen() throw(int, char)
```

When ExGen() tries to throw some exception other than that allowed in exception specification, that is, other than int and char (or a function called by ExGen() throws such an exception and not catching it thereby passing it up to ExGen()), then a built-in function named as unexpected() is called, which in turn terminates the program.

One may wonder what the need for exception specification is. When a third-party function is used, the source code may not be available but the prototype may be available. The programmer can decide to write corresponding catch statements depending on those types that are possible to be thrown from that function. In a way, exception specification works similar to the possible errors that can occur during the use of that specific function and gives one a chance to decide what action one would like to provide in response to such errors.

Look at the following function. It would generate an error if the user selects either 3 or 4.

```
void ExGen() throw(int, char)
{
```

```
cout << "Inside the function \n";
cout << "Inside try block\n";
MyException Error1(20, "Error testing");
cout << "Press 1 for int, 2 for char, 3 for MyException, and 4 for string";
int reply;
cin >> reply;
cout << "Assuming error and throwing exception now \n";
switch(reply)
```

> Exception specification specifies what a function can throw. Looking at exception specification, a user decides to provide corresponding catch statements.