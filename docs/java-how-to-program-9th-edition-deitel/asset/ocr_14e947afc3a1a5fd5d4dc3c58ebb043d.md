```
42      catch ( ArithmeticException arithmeticException )
43      {
44          System.err.printf( "\nException: %s\n", arithmeticException );
45          System.out.println(
46          "Zero is an invalid denominator. Please try again.\n" );
47      } // end catch
48  } while ( continueLoop ); // end do...while
49  } // end main
50 } // end class DivideByZeroWithExceptionHandling
```

```
Please enter an integer numerator: 100
Please enter an integer denominator: 7

Result: 100 / 7 = 14
```

```
Please enter an integer numerator: 100
Please enter an integer denominator: 0

Exception: java.lang.ArithmeticException: / by zero
Zero is an invalid denominator. Please try again.

Please enter an integer numerator: 100
Please enter an integer denominator: 7

Result: 100 / 7 = 14
```

```
Please enter an integer numerator: 100
Please enter an integer denominator: hello

Exception: java.util.InputMismatchException
You must enter integers. Please try again.

Please enter an integer numerator: 100
Please enter an integer denominator: 7

Result: 100 / 7 = 14
```

# Fig. 11.2 | Handling ArithmeticExceptions and InputMismatchExceptions. (Part 2 of 2.)

The first sample execution in Fig. 11.2 is a successful one that does not encounter any problems. In the second execution the user enters a zero denominator, and an ArithmeticException exception occurs. In the third execution the user enters the string "hello" as the denominator, and an InputMismatchException occurs. For each exception, the user is informed of the mistake and asked to try again, then is prompted for two new integers. In each sample execution, the program runs successfully to completion.

Class InputMismatchException is imported in line 3. Class ArithmeticException does not need to be imported because it’s in package java.lang. Line 18 creates the boolean variable continueLoop, which is true if the user has not yet entered valid input. Lines 20–48 repeatedly ask users for input until a valid input is received.