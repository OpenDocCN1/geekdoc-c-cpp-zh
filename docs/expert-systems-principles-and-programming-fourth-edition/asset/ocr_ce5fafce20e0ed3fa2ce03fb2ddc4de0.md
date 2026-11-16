The read function defaults to reading from the standard input device, t, if it is given no arguments. The previous example of the read function made use of this default logical name. The following example shows how a logical name can be used with the read function to retrieve the values from the "example.dat" file:

```
CLIPS> (open "example.dat" example "r").]
TRUE
CLIPS> (read example).]
green
CLIPS> (read example).]
7
CLIPS> (read example).]
EOF
CLIPS> (close example).]
TRUE
CLIPS>
```

First the file "example.dat" is opened, but with read access this time. Note that the "r" option did not have to be used for opening the "example.dat" file with the second call to the open function since that is the default. Once the file is open, the read function is used to retrieve the values green and 7 from the file associated with the logical name example. Notice that the third call of the read function returns the symbol EOF. CLIPS returns this value for input functions when an attempt is made to read past the end of the file. By checking the return value of the read (or other input) function it is possible to determine when there are no more data left in the file.

# # The Format Function

There are times when it is desirable to format output from a CLIPS program, such as when arranging data in tables. Although the printout function is useful, there is a function specifically designed for formatting, called format, which provides a wide variety of formatting styles. The syntax of the format function is:

```
{format <logical-name> <control-string>
<parameters>*}
```

The format function has several parts. The <logical-name> is the logical name where the output is sent. The default standard output device can be specified with the logical name t. Next comes a control string, which must be contained within double quotes. The control string consists of format flags, which indicate how the parameters to the format function should be printed. Following the control string is a list of parameters. The number of format flags in the control string will determine how many parameters should be specified. Parameters can be either constant values or expressions. The return value of the format function is the formatted string. If the logical name nil is used with the format command, then no output is printed (either to the terminal or a file), but the formatted string is still returned.