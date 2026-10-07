# Programming Exercises

+   1. Write a program that reads keyboard input into the @ symbol and echoes the input except for digits, converting each uppercase character to lowercase, and vice versa. (Don't forget the ctype function.)

+   2. Write a program that reads up to 10 donation values into an array of double. (Or, if you prefer, use an array template object.) The program should terminate input on non-numeric input. It should report the average of the numbers and also report how many numbers in the array are larger than the average.

+   3. Write a precursor to a menu-driven program. The program should display a menu offering four choices, each labeled with a letter. If the user responds with a letter other than one of the four valid choices, the program should prompt the user to enter a valid response until the user complies. Then the program should use a switch to select a simple action based on the user's selection. A program run could look like this:

Please enter one of the following choices:
c) carnivore
p) pianist
t) tree
g) game
f
nPlease enter a c, p, t, or g: q
Please enter a c, p, t, or g: t
A maple is a tree.

+   4. When you join the Benevolent Order of Programmers, you can be known at BOP meetings by your real name, your job title, or your secret BOP name.Write a program that your real name can list members by real name, by job title, by secret name, or by a member's preference. Base the program on the following structure:

```
// Benevolent Order of Programmers name structure
struct b {
    char fullname[strsize]; // real name
    char title[strsize]; // job title
    char bopname[strsize]; // secret BOP name
    int preference; // 0 = fullname, 1 = title, 2 = bopname
};
```

In the program, create a small array of such structures and initialize it to suitable values. Have the program run a loop that lets the user select from different alternatives:

+   a. display by name
b. display by title
c. display by bopname
d. display by preference
q. quit