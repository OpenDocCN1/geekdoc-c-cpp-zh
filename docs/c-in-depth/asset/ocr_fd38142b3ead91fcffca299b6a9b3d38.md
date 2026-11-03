```
~~~
077
0324
~~~
```

In hexadecimal integer constants, first two characters should be 0x or 0X. Some examples are as-

```
~~~
0x
0X23
0x515
0XA15B
0xFFF
0xac
~~~
```

By default the type of an integer constant is int. But if the value of integer constant exceeds the range of values represented by int type, the type is taken to be unsigned int or long int. We can also explicitly mention the type of the constant by suffixing it with l or L ( for long), u or U (for unsigned), ul or UL (for unsigned long). For example-

```
~~~
6453                          Integer constant of type int
45238722UL or 45238722ul      Integer constant of type unsigned long int
6655U or 6655u                Integer constant of type unsigned int
~~~
```

# ### 2.8.1.2 Real (floating point) Constants

Floating point constants are numeric constants that contain decimal point. Some valid floating point constants are-

```
~~~
0.5
5.3
4000.0
0.0073
5597.
39.0807
~~~
```

For expressing very large or very small real constants, exponential (scientific) form is used. Here the number is written in the mantissa and exponent form, which are separated by 'e' or 'E'. The mantissa can be an integer or a real number, while the exponent can be only an integer (positive or negative). For example the number 1800000 can be written as 1.8e6, here 1.8 is mantissa and 6 is the exponent. Some more examples are as-

| Number | | | Exponential form |
|---|---|---|---|
| 2500000000 | → | 2.5*10^9 | 2.5e9 |
| 0.0000076 | → | 7.6*10^-6 | 7.6e-6 |
| -670000 | → | -6.7*10^5 | -6.7E5 |

By default the type of a floating point constant is double. We can explicitly mention the type of constant by suffixing it with a f or F (for float type), l or L ( for long double). For example-

```
~~~
2.3e5                         floating point constant of type double
2.4e-9l or 2.4e-9L            floating point constant of type long double
3.52f or 3.52F                floating point constant of type float
~~~
```