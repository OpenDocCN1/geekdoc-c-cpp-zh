or, alternatively, one could pass an exception-handling procedure into the procedure as a parameter:

```
enum ErrorKind {OutOfInput, BadChar, Normal};
typedef void (*ErrorProc)(ErrorKind);
...
unsigned value;
...
void handler (ErrorKind error)
{
...
}
...
unsigned getNumber (ErrorProc handle)
{ unsigned result;
  int ch = fgetc(input);
  if (ch == EOF) handle(OutOfInput);
  else if (! isdigit(ch)) handle(BadChar);
  /* continue to compute */
  ...
  return result;
}
...
...
value = getNumber (handler);
```

Explicit exception testing makes a program more difficult to write, since the programmer must test in advance for all possible exceptional conditions. We would like to make this task easier by declaring exceptions in advance of their occurrence and specifying what a program is to do if an exception occurs. In designing such program behavior we must consider the following questions:

*Exceptions.* What exceptions are predefined in the language? Can they be disabled? Can user-defined exceptions be created? What is their scope?
*Exception handlers.* How are they defined? What is their scope? What default handlers are provided for predefined exceptions? Can they be replaced?
*Control.* How is control passed to a handler? Where does control pass after a handler is executed? What runtime environment remains after an error handler executes?

We will discuss each of these topics in turn with examples from C++, Ada, and ML.

# 9.5.1 Exceptions

Typically an exception occurrence in a program is represented by a data object that may be either predefined or user-defined. Not surprisingly, in a functional language this data object is a value of some type, while in a structured or object-oriented language it is a variable or object of some structured type. Typically, the type of an exception value or object is predefined, with exceptions themselves given in