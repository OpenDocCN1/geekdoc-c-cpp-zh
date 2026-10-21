```
3
4
5
6
7
8
9
10
```

![](bbox=[0.37, 0.3, 0.63, 0.56])

Figure 12.8. Output screen of program 12.18.

EXPLANATION : The program is simple. We input 10 numbers into the file and later display it back. Note there is no special function available in C++ for handling numbers using files.

# 12.7 COMMAND LINE ARGUMENTS

In all the programs we have used so far we have written main( ) without arguments but in reality main ( ) does take arguments and also have a return type. The prototype of main( ) in C++ is given as :

```
int main(int argc, char * argv[])
```

or

```
int main(int argc, char ** argv)
```

Number of parameters are passed are collected into the parameter argc which stands for argument count. Value of each argument is stored in string array argv which stands for argument value. All arguments are of string type whether they are int, float or even a character. By default return type of any function if not specified int is assumed that's why int before main( ) is optional. For better understanding point of view see the following examples.