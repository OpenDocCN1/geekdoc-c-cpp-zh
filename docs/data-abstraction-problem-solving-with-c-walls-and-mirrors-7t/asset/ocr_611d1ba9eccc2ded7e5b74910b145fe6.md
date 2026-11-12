+   • In an interactive environment, the program should always prompt the user for input in a manner that makes it quite clear what it expects. For example, the prompt “?” is not nearly as enlightening as the prompt “Please enter your account number.” You should never assume that the users of your program know what response the program requires.

+   • A program should always echo its input. Whenever a program reads data, either from a user or from a file, the program should include the values it reads in its output. This inclusion serves two purposes: First, it gives the user a check on the data entered—a safeguard against typos and errors in data transmission. This check is particularly useful in the case of interactive input. Second, the output is more meaningful and self-explanatory when it contains a record of what input generated the output.

+   • The output should be well labeled and easy to read. An output of

```
1800 6 1
Jones, Q. 223 2234.00 1088.19 N, J Smith, T. 111
110.23 T I, Harris, V. 44 44000.00 22222.22
```

is more prone to misinterpretation than

```
CUSTOMER ACCOUNTS AS OF 1800 HOURS ON JUNE 1
```

```
Account status codes: N=new, J=joint, I=inactive
```

```
NAME ACCT# CHECKING SAVINGS STATUS
Jones, Q. 223 $ 2234.00 $ 1088.19 N, J
Smith, T. 111 $ 110.23 I
Harris, V. 44 $4400.00 $22222.22 -------
```

These characteristics of a good user interface are only the basics. Several more subtle points separate a program that is merely usable from one that is user-friendly. Students tend to ignore a good user interface, but by investing a little extra time here, you can make a big difference: the difference between a good program and one that only solves the problem. For example, consider a program that requires a user to enter a line of data in some fixed format, with exactly one blank between the items. A free-form input that allows any number of blanks between the items would be much more convenient for the user. It takes so little time to add code that skips blanks, so why require the user to follow an exact format? Once you have made this small additional effort, the code is a permanent part of both your program and your library of techniques, and the user of your program will never have to think about input format.

# B.5 Fail-Safe Programming

A fail-safe program is one that will perform reasonably no matter how anyone uses it. Unfortunately, this goal is usually unattainable. A more realistic goal is to anticipate the ways that people might misuse the program and to guard carefully against these abuses.

This discussion considers two types of errors. The first type is an error in input data. For example, suppose that a program expects a nonnegative integer but reads –12. When a program encounters this type of problem, it should not produce incorrect results or abort with a vague error message. Instead, a fail-safe program provides a message such as

```
-12 is not a valid number of children.
Please enter this number again.
```

The second type of error is an error in the program logic. Although a discussion of this type of error belongs in the next section about debugging, detecting errors in program logic is also a characteristic of