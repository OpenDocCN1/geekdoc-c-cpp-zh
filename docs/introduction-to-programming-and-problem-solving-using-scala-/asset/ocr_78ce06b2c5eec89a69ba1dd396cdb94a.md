+   - s – a string,

+   - x – hexadecimal formatting for an integer.

Here is an example using the variables above with spaces between them.

```
printf("%%e %s %d",g,name,classSize)
6.670000e-11 Mark 20
```

By default, the scientific notation displays a significant number of trailing zeros. It is possible to specify the width, characters, of values by putting a number between the percent sign and the conversion. For fractional numbers, precision can also be specified by putting a dot and the number of digits of precision that are desired. Here are some examples showing:

```
printf("%.2e %s %d",g,name,classSize)
6.67e-11 Mark 20
printf("%.19e %s %d",g,name,classSize)
6.67e-11 Mark 20
printf("%.19f %s %d",math.Pi,name,classSize)
3.141593 Mark 20
```

By default, values are right-aligned when the width is larger than the number of characters displayed. This can be changed by putting a flag after the percent sign. The comma flag says that you want proper regional separators in you of numbers. Examples of these are shown here:

```
printf(\%-19d %s %d",math.Pi,name,classSize)
3.141593 Mark 20
printf("%,19d %s %d",Int.MaxValue,name,classSize)
2,147,483,647 Mark 20
```

# 9.5 Use Case: Simple Encryption

To demonstrate the use of files, we will write some very basic encryption and decryption scripts. At this point we will not be using any cryptography methods. There are some end of chapter exercises and projects that build up to. The approach we will take probably show others from reading your stuff, but you would not want to use them to access your bank accounts.

# 9.5.1 Command Line Arguments

We want to write scripts that us specify all the information needed, including the names of the input and output files, on the command line. In order to do we need to discuss how we can get the command line arguments into our programs in Scala.

When you run a program as a script in Scala, anything that appears on the command line after the name of the script file is available in the program as an element of the Arrayargs,