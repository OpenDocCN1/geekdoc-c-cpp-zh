Permissions:      -rwxr-xr-x
Size (bytes):     245
$

In the preceding script, the first if statement displays an error message and exits the program if you run the script without any command line argument. The second if statement displays an error message and exits the program if you run the script with more than one argument. The third if statement is executed if conditions for the first two are false—that is, if you run the script with one argument only. This if statement produces the desired results if the command line argument is an ordinary file. If the passed argument is not an ordinary file, the condition for the third if statement is false and the error message if_demo1: argument must be an ordinary file is displayed. The exit command is used to take control out of the script. We normally use 1 as the argument (i.e., exit status) of exit when a script is to be terminated because of an erroneous condition. The exit status 0 is used for normal termination of the script.

We can rewrite the script in if_demo1 using the alternative syntax for the test command and the logical AND operator, -a, as shown in Tables 12.5 and 12.6.

```
$ cat if_demo10
#!/bin/bash
if [ "$#" -eq 1 -a -f "$1" ]
    then
        ...
fi
echo "$0: Specify exactly one command line argument that"
echo " must be an ordinary file."
exit 1
$
```

# TABLE 12.6

Precedence of Bash Operators (High to Low)

| Operator | Precedence |
|---|---|
| var++ var-- | C-style postincrement, postdecrement |
| ++var --var | C-style preincrement, predecrement |
| ! ~ | Negation logical/bitwise, inverts sense of following operator |
| ** | Exponentiation |
| * / % | Multiplication, division, modulo |
| + - | Addition, subtraction |
| << >> | Bitwise shift left, shift right |
| -z -n | Unary comparison for a string is or is-not null |
| -e -f -t -x, etc. | Unary comparison for file-test |
| < -lt > -gt <= -le >= -ge | Compound comparison for strings and integers |
| -nt -ot -ef | Compound comparison for file test |
| == -eq != -ne | Equality/inequality test operators for strings and integers |
| & | Bitwise AND |
| ^ | Bitwise XOR (exclusive-OR) |
| | | Bitwise OR |
| && -a | Logical AND |
| || -o | Logical OR |
| ?: | C-style trinary operator (a conditional statement) |
| = | Assignment |
| *= /= %= += -= <<= >>= &= | Combination assignment: times-equal, divide-equal, mod-equal |
| , | For linking a sequence of operations |