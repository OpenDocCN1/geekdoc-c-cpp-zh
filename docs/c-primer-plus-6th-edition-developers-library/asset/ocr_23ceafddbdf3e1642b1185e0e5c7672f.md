```
Buy low, sell high.
Enter the letter of your choice:
a. advice        b. bell
c. count         q. quit
count
Count how far? Enter an integer:
two
two is not an integer.
Please enter an integer value, such as 25, -178, or 3: 5
1
2
3
4
5
Enter the letter of your choice:
a. advice        b. bell
c. count         q. quit
d
Please respond with a, b, c, or q.
q
```

It can be hard work getting a menu interface to work as smoothly as you might want, but after you develop a viable approach, you can reuse it in a variety of situations.

Another point to notice is how each function, when faced with doing something a bit complicated, delegated the task to another function, thus making the program much more modular.

# Key Concepts

C programs see input as a stream of incoming bytes. The getchar() function interprets each byte as being a character code. The scanf() function sees input the same way, but, guided by its conversion specifiers, it can convert character input to numeric values. Many operating systems provide redirection, which allows you to substitute a file for a keyboard for input and to substitute a file for a monitor for output.

Programs often expect a particular form of input. You can make a program much more robust and user friendly by anticipating entry errors a user might make and enabling the program to cope with them.

With a small program, input validation might be the most involved part of the code. It also opens up many choices. For example, if the user enters the wrong kind of information, you can terminate the program, you can give the user a fixed number of chances to get the input right, or you give the user an unlimited number of chances.