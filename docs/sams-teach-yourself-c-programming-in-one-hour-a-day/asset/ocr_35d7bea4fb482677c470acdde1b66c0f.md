Error-Handling

519

| EMFILE | 4 | Too many open files |
| ENOENT | 2 | No such file or directory. |
| ENOEXEC | 1001 | Exec format error. |
| ENOMEM | 8 | Not enough core (for example, not enough memory to execute the errno (function)). |
| ENOPATH | 3 | Path not found. |
| ERANGE | 1003 | Result out of range (for example, result returned by a math function is too large or too small for the return data type). |

You can use errno two ways. When an error occurs. If this happens, you can test the value of errno to determine the nature of the error and take appropriate action. Otherwise, when you have no specific indication that an error occurred, you can test errno. If it's nonzero, an error has occurred, and the specific value of errno indicates the nature of the error. Be sure to reset errno to zero after handling the error. The next section explains perror(), and then Listing 20.4 illustrates the use of errno.

# The perror() Function

perror() function is of C's error-handling tools. When called, perror() displays a message on stderr describing the most recent error that occurred during a library function call or system call. The prototype, in stdio.h, is

```
perror(const char *msg);
```

The argument msg points to an optional, user-defined message. This message is printed, followed by a call and the implementation-defined message that describes the most recent error. If you call perror() when no error has occurred, the message displayed is no error.

A call to perror() does nothing to deal with the error condition. It is up to the program to take action. The action might consist of prompting the user to do something as terminate the program. The action program takes be determined by testing the value of errno and by the nature of the error. Note that a program need not include the header file errno.h to use the external variable errno. That header file is required only if your program uses the symbolic constants listed in Table 20.2. Listing 20.4 illustrates the use of perror() and errno for handling runtime errors.

20