6. As noted in the text, defining a date class instead of a date structure is more consistent with the notion of object-oriented programming. Define such a class with appropriate setter and getter methods. Also add a method called dateUpdate to return the day after its argument.

Do you see any advantages of defining a Date as a class instead of a structure? Do you see any disadvantages?

7. Given the following definitions

```
char *message = "Programming in Objective-C is fun";nchar message[] = "You said it";
int x = 100;
```

determine whether NSLog call from the following sets will produces the same output as others from the set.

```
*** set 1 ***
NSLog("@Programming in Objective-C is fun");
NSLog("@%s", "Programming in Objective-C is fun");
NSLog("@%s", message);
```

```
*** set 2 ***
NSLog("@You said it");
NSLog("@%s", message, 2);
NSLog("@%s", &message2[0]);
```

```
*** set 3 ***
NSLog("@said it");
NSLog("@%s", message + 4);
NSLog("@%s", &message2[4]);
```

8. Write a program that prints all its command-line arguments, one per line at the terminal. Note the effect of enclosing arguments that contain space characters inside quotation marks.

9. Which of the following statements produce the output This is a test? Explain.

```
NSLog("@This is a test");
NSLog("@This is a test");
```

```
NSLog("@%s", "This is a test");
NSLog("@%s", @@This is a test");
```

```
NSLog("@"s", "This is a test");
NSLog("@"s", "This is a test");
```

```
NSLog("@%@", "This is a test");
NSLog("@%@", "This is a test");
```

10. Rewrite the exchange function from Program 13.14 as a block and test it out.