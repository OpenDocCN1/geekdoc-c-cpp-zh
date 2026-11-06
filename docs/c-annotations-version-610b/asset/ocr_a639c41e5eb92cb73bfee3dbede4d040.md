```
Hello by ’local object‘ (copy) (copy)
```

Then the program terminates and its remaining objects are now destroyed, reversing their order of creation:

```
Destructor of ’local object‘ (copy) (copy)
Destructor of ’local object‘ (copy)
Destructor of ’main object‘
```

The copy created by the catch clause clearly is superficial. It can be avoided by defining object reference parameters in catch clauses: ‘catch (Object &o)’. The program now produces the following output:

```
Constructor of ’main object‘
Constructor of ’local object‘
Calling fun of ’main object‘
Copy constructor for ’local object‘ (copy)
Destructor of ’local object‘
Caught exception
Hello by ’local object‘ (copy)
Destructor of ’local object‘ (copy)
Destructor of ’main object‘
```

Only a single copy of toThrow was created.

It’s a bad idea to throw a pointer to a locally defined object. The pointer is thrown, but the object to which the pointer refers ceases to exist once the exception is thrown. The catcher receives a wild pointer. Bad news....

Let’s summarize the above findings:

+   - Local objects are thrown as copied objects;
+   - Don’t throw pointers to local objects;
+   - It is possible to throw pointers to *dynamically* generated objects. In this case one must take care that the generated object is properly deleted by the exception handler to prevent a memory leak.

Exceptions are thrown in situations where a function can’t complete its assigned task, but the program is still able to continue. Imagine a program offering an interactive calculator. The program expects numeric expressions, which are evaluated. Expressions may show syntactic errors or it may be mathematically impossible to evaluate them. Maybe the calculator allows us to define and use variables and the user might refer to non-existing variables: plenty of reasons for the expression evaluation to fail, and so many reasons for exceptions to be thrown. None of those should terminate the program. Instead, the program’s user is informed about the nature of the problem and is invited to enter another expression. Example:

```
if (!parse(expressionBuffer))          // parsing failed
    throw "Syntax error in expression";

if (!lookup(variableName))             // variable not found
    throw "Variable not defined";

if (divisionByZero())                  // unable to do division
    throw "Division by zero is not defined";
```

Where these throw statements are located is irrelevant: they may be found deeply nested inside the program, or at a more superficial level. Furthermore, *functions* may be used to generate the exception