```
printf("Farewell! thou art too dear for my possessing,\n");
printf("%c%d\n", '$', 2 * cost);

return 0;
}
```

The output, of course, is

```
The 7 contestants ate 12.750000 berry pies.
The value of pi is 3.141593.
Farewell! thou art too dear for my possessing,
$15600
```

This is the format for using printf():

```
printf(Control-string, item1, item2,...);
```

Item1, item2, and so on, are the items to be printed. They can be variables or constants, or even expressions that are evaluated first before the value is printed. Control-string is a character string describing how the items are to be printed. As mentioned in Chapter 3, the control string should contain a conversion specifier for each item to be printed. For example, consider the following statement:

```
printf("The %d contestants ate %f berry pies.\n", number,
    pies);
```

Control-string is the phrase enclosed in double quotes. This particular control string contains two conversion specifiers corresponding to number and pies—the two items to be displayed. Figure 4.6 shows another example of a printf() statement.

![](bbox=[0.25, 0.7, 0.8, 0.75])

Figure 4.6 Arguments for printf().

Here is another line from the example:

```
printf("The value of pi is %f.\n", PI);
```

This time, the list of items has just one member—the symbolic constant PI.

As you can see in Figure 4.7, Control-string contains two distinct forms of information:

+   - Characters that are actually printed
+   - Conversion specifications