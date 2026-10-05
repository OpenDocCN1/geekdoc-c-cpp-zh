# C++ main Function

Every C and C++ program must contain a main function. Program execution starts from the main function. The signature of main is predefined by the compiler, it is:

```
int main(void)
or int main(argc, char *argv[])
```

main cannot be called from within a C++ program and it cannot be qualified with the virtual, static or inline attributes.

argc is a count of the number of elements in argv. It is always greater than or equal to one.

The first element argv[0] is the command to start execution of the program. By convention, argv[0] is the name of the program. argv[0] does not have to be specified, it is implicitly taken from the command line. The rest of the arguments of argv are null-terminated strings representing command-line arguments passed by the user on the command line to the program.