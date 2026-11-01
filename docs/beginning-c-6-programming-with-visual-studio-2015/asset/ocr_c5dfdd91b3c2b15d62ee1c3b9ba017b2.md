Each exception may be configured using the check boxes next to the exception type. When checked, the debugger will (break when) Thrown, causing a break into the debugger even for exceptions that are handled.

# EXERCISES

7.1 "Using Trace.WriteLine() is preferable to using Debug.WriteLine(), as the Debug version works only in debug builds." Do you agree with this statement? If so, why?

7.2 Provide code for a simple application containing a loop that generates an error after 5,000 cycles. Use a breakpoint to enter break mode just before the error is caused on the 5,000th cycle. (Note: A simple way to generate an error is to attempt to access a nonexistent array element, such as myArray[1000] in an array with 100 elements.)

7.3 "finally code blocks execute only if a catch block isn't executed." True or false?

7.4 Given the enumeration data type orientation defined in the following code, write an application that uses structured exception handling (SEH) to cast a byte-type variable into an orientation-type variable in a safe way. (Note: You can force exceptions to be thrown using the checked keyword, an example of which is shown here. This code should be used in your application.)

```
enum Orientation : byte
{
    North = 1,
    South = 2,
    East = 3,
    West = 4
}
myDirection = checked((Orientation)myByte);
```

Answers to these exercises are in Appendix A.