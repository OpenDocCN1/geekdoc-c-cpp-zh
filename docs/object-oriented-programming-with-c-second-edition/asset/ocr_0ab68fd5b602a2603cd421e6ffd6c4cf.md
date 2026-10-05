210 Object-Oriented Programming with C++

setfill(
setiosflags()
resetiosflags()

};

class intList
{
13. How can a programmer define his/her own
manipulators?

13. How can a programmer define his/her own
manipulators?

intNode * head;
public:
//functions to add, delete, modify,
save and load

14. What are command line arguments? Why are they
important?

15. How can the main() function be programmed to read
command line arguments?

18. Write a manipulator that fixes a currency symbol
to the output value. For this, the manipulator should
read the symbol from a disk file.

16. Write a program to obtain as many integers from
t user as he/she wants and write them into a disk
file. After the user has finished the integers,
read them from the file and display them on the
monitor.

19. Write a program that gives an error message if the
number of arguments are passed to the executable
is not equal to 1 (hint: 'arg' != 2), and then
terminates itself. The error message should advise
the user that exactly one argument should be passed
to the executable, and it should be the name of
afile.

17. Create a class objects would hold linked
lists of integers. the objects would also have the necessary
functionality to download their data into a specified
disk file and upload their data from specified disk
files. The application will be menu-driven.
the user will have the option to save the linked list and
to 'save as' the linked list.

Otherwise, if the user has passed exactly
argument to the executable, the program should
open the file whose name matches the value of
argument (hint: argv[1]). It should then append the
name of the executable (hint: argv[0]) to a new
line in the file, along with a text that says the
executable executed successfully. For example, if
name of the executable is test, then the following
line should get appended to the file:

Hint:
Create two classes as follows:

```
class intNode
{
  int data;
  intNode * Next;
public:
  //functions to set and get the data
members
```

test executed successfully.