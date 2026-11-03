The scanf() function is prototyped in the stdio.h header file. Here's the format:

```
int scanf(const char *restrict format, ...);
```

Scary, huh? Just ignore it for now. Here's my less frightening version of the format:

```
scanf("placeholder", variable);
```

In this version, placeholder is a conversion character, and variable is a variable that matches the conversion character's data type. Unless variable is a string (char array), it's prefixed by the & operator.

Here are some scanf() examples:

```
scanf("%d", &highscore);
```

The preceding statement reads an integer value from standard input into the variable highscore, an int variable.

```
scanf("%f", &temperature);
```

The preceding scanf() statement waits for a floating-point value to be input, which is stored in the temperature variable.

```
scanf("%c", &key);
```

In the preceding statement, scanf() accepts the first character read from standard input and stores it in the key variable.

```
scanf("%s", firstname);
```

![](bbox=[0.15, 0.75, 0.25, 0.88])

The %s placeholder is used to read in text, but only until the first whitespace character is encountered. So a space, a tab, or the Enter key terminates the string. Also, firstname is a char array, so it need not be prefixed by the & operator.

# Reading a string with scanf()

It's rare to use the scanf() function to read a string, because input is terminated at the first whitespace character. Still, it's worth a try.

To use the scanf() function to read in a chunk of text, the %s conversion character is used — just like in printf() but with input instead of output, as shown in Listing 7-5.