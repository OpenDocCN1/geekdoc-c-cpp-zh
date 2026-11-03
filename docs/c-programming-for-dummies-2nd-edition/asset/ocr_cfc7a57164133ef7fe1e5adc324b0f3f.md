Unintentional endless loops do happen. I've run code many times, only to watch a blank screen for a few moments. Oops.

![](bbox=[0.176, 0.159, 0.236, 0.228])

Console applications, such as the kind created throughout this book, are halted by pressing the Ctrl+C key combination in a terminal window. This trick may not always work, so you can try closing the window. You can also kill the task, which is a process that's handled differently by every operating system. For example, in a Unix operating system, you can open another terminal window and use the kill command to rub out a program run amok in the first terminal window.

# ## scanf() Blunders

The `scanf()` function is a handy way to read specific information from standard input. It's not, however, ideal for all forms of input.

For example, `scanf()` doesn't understand when a user types something other than the format that's requested. Specifically, you cannot read in a full string of text. This issue is because `scanf()` discards any part of the string after the first whitespace character.

![](bbox=[0.176, 0.516, 0.236, 0.595])

Though the `fgets()` function is a great alternative for capturing text, keep in mind that it can capture the newline that ends a line of text. This character, `\n`, becomes part of the input string.

The other thing to keep in mind when using `scanf()` is that its second argument is an address, a pointer. For standard variable types — such as `int`, `float`, and `double` — you must prefix the variable name with the &, the address operator:

```
```c
scanf("%d",&some_int);
```
```

The & prefix isn't necessary for reading in an array:

```
```c
scanf("%s", first_name);
```
```

Individual array elements, however, aren't memory locations, and they still require the & prefix:

```
```c
scanf("%c",&first_name[0]);
```
```

Pointer variables do not require the & prefix, which could result in unintended consequences.