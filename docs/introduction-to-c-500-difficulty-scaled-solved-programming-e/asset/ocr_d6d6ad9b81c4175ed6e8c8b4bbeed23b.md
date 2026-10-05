# 324 Introduction to C++

# PASSING DATA TO main()

When we run a program from the command line, we'll often need to pass information to it. For example, suppose that the executable file hello.exe is stored in the C disk. The command line:

```
C:\hello 100 200
```

executes the program hello and passes the values 100 and 200 to main(). To get the data, main(i) must be defined like this:

```
int main(int argc, char *argv[])
```

Although you can use any names, argc (argument count) and argv (argument vector) are by convention the typical choice. And because the compiler translates an array parameter to pointer, many prefer to use **argv instead of "argv".

The value of argc is equal to the number of the command line arguments, including the name of the program itself. For example, in the previous command line, argc is 3. The arguments are separated by space(s), to distinguish the values:

The argv parameter is an array of pointers to the command line arguments, while the other pointers up to argv[argc-1] point to the name of the program. The last argument is argv[argc], which is always nullptr. In our example, hello, 100, and 200 are passed to main() as strings. In particular, argv[0] points to the string "hello", argv[1] points to "100", argv[2] points to "200", and argv[3] is nullptr.

The following program checks if the user entered the correct user name and password. Suppose that these are used and parsed, respectively.

```
#include <iostream> // Example 11.27
#include <string>
```

```
int main(int argc, char *argv[]) {
    if(argc == 1) {
        std::cout << "Error: missing user name and password\n";
    } else if(argc == 2) {
        std::cout << "Error: missing password\n";
    } else if(argc == 3) {
        if(strcmp(argv[1], "user") == 0 && strcmp(argv[2], "pswd") == 0) {
            std::cout << "Valid user. The program " << argv[0] << " will be executed\n";
        } else {
            std::cout << "Wrong input\n";
        }
    } else {
        std::cout << "Error: too many parameters\n";
    }
    return 0;
}
```

The if statements check the value of argc. If it is 3, the program checks if the entered user name and password are correct. If not, the program displays a related message.