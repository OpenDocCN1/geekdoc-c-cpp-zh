could be replaced with:
all
or:
none
or:
some

# 7.4 FIELDS

As a knowledge base is constructed, CLIPS must read input from the keyboard and files in order to execute commands and load programs. As CLIPS reads characters from the keyboard or files, it groups them together into tokens. Tokens represent groups of characters that have special meaning to CLIPS. Some tokens such as left and right parentheses consist of only one character.

The group of tokens known as fields is of particular importance. There are eight types of fields, also called the CLIPS primitive data types: float, integer, symbol, string, external address, fact address, instance name, and instance address.

The first two types of fields, floats and integers, are called numeric fields or simply numbers. A numeric field consists of three parts: the sign, the value, and the exponent. The sign and the exponent are optional. The sign is either + or -. The value contains one or more digits with a single optional decimal point contained with the digits. The exponent consists of the letter e or E followed by an optional + or - followed by one or more digits. Any number consisting of an optional sign followed by only digits is stored as an integer. All other numbers are stored as floats.

The following are examples of valid CLIPS floats:

```
1.5
1.0
0.7
9e+1
3.5e10
```

The following are examples of valid CLIPS integers:

```
1
+3
-1
65
```