# BRANCHING

# 121

# Output if condition is “True”

# "else” condition output

Run the program and type in “y”. The program shows your New Year message. It doesn’t show the other message.

Type in “n”, or any other character, and the New Year message isn’t shown. Instead, the “Not yet!” appears.

Type in “n”

Is it New Year? (y/n)
Happy New Year!
Time for Fireworks.

Is it New Year? (y/n)
Not yet!

A different message appears

# Do one of these things

The “elif” command is short for “else-if”. It means that if something is “True”, do one thing; otherwise, check if something else is “True” and do something else if it is. The following calculator program uses the “elif” command.

![](bbox=[0.665, 0.285, 0.845, 0.405])

# if-elif-if condition

# Output for the condition that’s “True”

This program checks what is typed in. If is “add”, “sub”, “mul”, or “div”, the result of the sum is shown.

Test the program. Enter two numbers and in “sub”. The answer will be the first number minus the second number.

Ask the user to input a number

Remember to add quote marks and brackets

| a = int(input('a = ')) |
| b = int(input('b = ')) |
| op = input('add/mul/div: ') |
| if op == 'add': |
| c = a + b |
| elif op == 'sub': |
| c = a - b |
| elif op == 'mul': |
| c = a * b |
| elif op == 'div': |
| c = a / b |

| a = 7 | Enter two numbers | Type in “sub” |
| b = 5 | to subtract |
| add/mul/div:sub | 5 from 7 |
| Answer = 2 | |

Type “add” to add the variables together

Answer is calculated by subtracting variable “a” from “b”

Type “div” to divide the variables

# "else” condition output

The “else” condition runs if something other than “add”, “sub”, “mul”, or “div” is typed in, and an error message displayed.

Shows an error message in “c” if something else is typed in

| a = 7 | Type something different here |
| b = 5 | |
| add/mul/div:try | Error message displays |
| Answer = Error | |

```
else:
  c = 'Error'
print('Answer = ' ,c)
```

Shows the answer or error message