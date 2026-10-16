# Hint

Although a default case isn’t required, it’s usually a good idea to have one as a catchall.

Here’s an example to cement the ideas. Suppose choice is equal to value2. The program will first test choice against value1. Because they’re not equal, the program will continue. Next, the program will test choice against value2. Because they are equal, the program will execute statement2. Then the program will hit the break statement and exit the switch structure.

# Trap

You can use the switch statement only to test an int (or a value that can be treated as an int, such as a char or an enumerator). A switch statement won’t work with any other type.

# Introducing the Menu Chooser Program

The Menu Chooser program presents the user with a menu that lists three difficulty levels and asks him to make a choice. If the user enters a number that corresponds to a listed choice, then he is shown a message confirming the choice. If the user makes some other choice, he is told that the choice is invalid. Figure 2.5 shows the program in action.

![](bbox=[0.115, 0.565, 0.857, 0.852])

Figure 2.5
Looks like I took the easy way out.