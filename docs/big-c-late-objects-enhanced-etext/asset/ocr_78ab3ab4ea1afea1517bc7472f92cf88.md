# Syntax 1.2 Output Statement

![](bbox=[0.25, 0.14, 0.92, 0.44])

# Common Error 1.1

# Omitting Semicolons

![](bbox=[0.13, 0.51, 0.18, 0.65])

In C++, statements such as output or return statements end in a semicolon. Forgetting to type a semicolon is a common error. It confuses the compiler because the compiler uses the semicolon to find where one statement ends and the next one starts. The compiler does not use line ends or closing braces to recognize the ends of statements. For example, the compiler considers

```
cout << "Hello, World!" << endl
return 0;
```

a single statement, as if you had written

```
cout << "Hello, World!" << endl return 0;
```

and then it doesn't understand that statement, because it does not expect the word return in the middle of an output command. The remedy is simple. Just scan every statement for a terminating semicolon, just as you would check that every English sentence ends in a period.

Sometimes, the error message that flags the missing semicolon is displayed in the following line. When you see such a message, be sure to check the preceding line as well.

# Special Topic 1.1

# Escape Sequences

![](bbox=[0.12, 0.83, 0.18, 0.92])

How can you display a string containing quotation marks, such as

Hello, "World"

You can't use

```
cout << "Hello, "World"";
```

As soon as the compiler reads "Hello, ", it thinks the string is finished, and then it gets all confused about World. Compilers have a one-track mind, and if a simple analysis of the input doesn't make sense to them, they just refuse to go on, and they report an error. In contrast, a human would probably realize that the second and third quotation marks were supposed to be part of the string.