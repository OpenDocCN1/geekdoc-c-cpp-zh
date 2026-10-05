# EXERCISES

C.11.26 What is the output of the following program?

```
#include <iostream>
int main(int argc, char *argv[]) {
    while (--argc)
        (argc > 1) ? std::cout << ++argv << ' ' : std::cout << ++argv << '\n';
    return 0;
}
```

**Answer:** argc is equal to the number of command line arguments. If the only argument is the name of the program, the loop will not be executed because its value becomes 0. If there are more arguments, the program displays their values, separated by a space, and it adds a new line character after the last one.

For example, suppose the command line arguments are one and two. So, argc would be 3 and the loop condition makes it 2. If true, the program displays the value of ++argv and argv points to argv[0], the expression ++argv makes point to argv[1]. Therefore, ++argv is equivalent to argv[1], and the program outputs one. In the next iteration, argc becomes 1, so the program displays the value of argv[2]. As a result, the program outputs two and a new line character.

Now answer this one. What would be the output if we write *argv instead of ++argv?

**Answer:** The program would display the name of the program and the command line arguments, the last one.

C.11.27 The popular ping command is used to test the communication between two systems in an IP network. For example, www.atua.gr. Write a program that reads the command line argument and checks if it corresponds to a valid destination. To be valid, assume that it should have the form of the example, that is, with "www.", and the part after the second dot should be two or three characters long (e.g., gr).

```
#include <iostream> // Exercise 11.27
#include <cstring>
using std::cout;
int main(int argc, char *argv[]) {
    int i, len;
    if (argc != 2) {
        cout << "Wrong number of arguments\n";n        return 0;
    }
    if (strcmp(argv[1], "www.", 4) != 0) {
        cout << "Name must begin with www.\\n";n        return 0;
    }
}
```