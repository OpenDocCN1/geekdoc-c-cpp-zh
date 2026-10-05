# SYNTAX

```
try {
  Some_Statements
  <Either some code with a throw statement or
  a function invocation that might throw an exception>
  Some_More_Statements
}
catch (Type e) {
  <Code to be performed if a value of
  catch-block parameter type is thrown in the try block>
}
```

# EXAMPLE

See Display 18.2 for an example.

# Self-Test Exercises

+   1. What output is produced by the following code?
int waitTime = 46;
{
  cout << "Try block entered.\\n";n  if (waitTime > 30)
    throw waitTime;
  cout << "Leaving try block.\\n";
}
catch(int thrownValue) {
  cout << "Exception thrown with\n"
  << "waitTime equal to " << thrownValue << endl;
}
2. What would be the output produced by the code in Self-Test Exercise 1 if we made the following change?
int waitTime = 46;
to
int waitTime = 12;