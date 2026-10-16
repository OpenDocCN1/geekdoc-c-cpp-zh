in advance according to the kind of error or interrupt. It is reasonable to try to build such a feature into a language, since it is often unacceptable for a program to allow the underlying machine or operating system to take control. This usually means that the program is aborted, or “crashes.” Programs that exhibit this behavior fail the test of robustness, which is part of the design criteria of security and reliability. A program must be able to recover from errors and continue execution.

Even in a language with a good exception mechanism, however, it is unreasonable to expect a program to be able to catch and handle every possible error that can occur. The reason is that too many possible failures can occur at too low a level—the failure of a hardware device, memory allocation problems, communication problems—all can lead to situations in which the underlying operating system may need to take drastic action to terminate a program, without the program being able to do anything about it. Such errors are sometimes referred to as asynchronous exceptions, since they can occur at any moment, not just in response to the execution of program code. By contrast, errors that a program can definitely catch are called synchronous exceptions and are exceptions that occur in direct response to actions by the program (such as trying to open a file, perform a particular calculation, or the like). User-defined exceptions can only be synchronous (since they must be raised directly in program code), but predefined or library exceptions may include a number of asynchronous exceptions, since the runtime environment for the language can cooperate with the operating system to allow a program to trap some asynchronous errors.

It is helpful in studying exception-handling mechanisms to recall how exceptions can be dealt with in a language without such facilities. Exception conditions in such languages have to be found before an error occurs, and this assumes it is possible to test for them in the language. One can then attempt to handle the error at the location where it occurs, as in the following C code:

```
if (y == 0)
            handleError("denominator in ratio is zero");
else
    ratio = x / y;
```

Or, if the error occurs in a procedure, one can either pass an error condition back to the caller, as in the C code

```
enum ErrorKind {OutOfInput, BadChar, Normal};
...
ErrorKind getNumber ( unsigned* result)
{ int ch = fgetc(input);
  if (ch == EOF) return OutOfInput;
  else if (! isdigit(ch)) return BadChar;
  /* continue to compute */
  ...
  *result = ... ;
  return Normal;
}
```