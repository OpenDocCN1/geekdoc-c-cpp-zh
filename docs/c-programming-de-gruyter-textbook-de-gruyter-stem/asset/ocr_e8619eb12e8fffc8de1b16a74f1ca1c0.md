# 6.5 Strings — 247

```
char c[]="China";ncout<<c;
```

When inputting/outputting a whole string, we should note that:

+   1. Output characters do not contain '\0';
2. We use the character array name to specify the string to be output, and the outputting ends when meeting '\0';
3. When inputting multiple strings, we should separate them by spaces; when inputting a single string, there should not be spaces within it.

For example, there are the statements in the program follows:

```
static char str[5],str2[5],str3[5];ncin>>str1>>str2>>str3;
```

If we input the following data in the runtime:

```
How are you?
```

The states of the variables in memory are as:

| str1: | H | o | w | \0 |
| str2: | a | e | \0 |
| str3: | y | o | u | ? | \0 |

If we modify the code to:

```
static char str[13];ncin>>str;
```

And input the following data in the runtime:

```
How are you?
```

The content of variable str in memory is:

| str: | H | o | w | \0 |

Since the reading of inputs stops when meeting a space, we can only receive the first word.

We can use string-processing system functions to process strings, such as strcat(concat), strcpy(copy), strcmp(compare), strlen(get the length), strl(convert to lowercase), and strupr(vert to uppercase). We should include the header file cstring to the source program before using these functions. Readers can find instructions for these functions with the help of the compiling system.