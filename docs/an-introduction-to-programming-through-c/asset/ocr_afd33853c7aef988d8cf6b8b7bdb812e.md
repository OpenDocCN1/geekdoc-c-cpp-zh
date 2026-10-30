```
int lcm(int m, int n);
int gcd(int m, int n);
```

The names of the parameters can be omitted from declarations, e.g. you may write just int lcm(int,int); in the declaration. The declaration is also called a prototype, or even a signature.

Suppose a compiler is processing a file containing the statement cout << lcm(24,36);. When it reaches this statement, it needs to be sure that lcm is indeed a function, and not some typing mistake. It also needs to know the type of the value returned by lcm – depending upon the type the printing will happen differently. Both these needs are met by the declaration. A declaration of a function f provides (a) an assurance that f as used later in the program is indeed a function, and that in case it has not been defined so far, it will be defined later in this file itself or in some other file, (b) a description of the types of the parameters to the function and the type of the value returned by the function. Given the declaration, the file can be compiled except for the code for executing the function itself, which can be supplied later (Section 11.2.3). Notice that a function definition also provides the information in (a), (b) mentioned above, and hence is a also considered to be a declaration.

# 11.2.2 Splitting a program into multiple files

Using the notion of a declaration, we can break up programs into multiple files. As an example, consider the main program of Section 9.2 that calls our function lcm to find the LCM of 36 and 24. Thus there are 3 functions in our program overall: the function main, the function lcm and the function gcd. Figure 11.1 shows how we could form 3 files for the program.

First consider the file gcd.cpp, which contains the function gcd. It does not call any other function, and so does not need to have any additional declaration. Next consider the file lcm.cpp. This contains the function lcm which contains a call to gcd. So this file has a declaration of gcd at the very beginning. Finally the file main.cpp contains the main program. This calls the function lcm, so it contains a declaration of lcm at the beginning. Note that the main program uses the identifier cout to write to the console. For this it needs to include simplecpp. The other files do not contain anything which needs services from simplecpp, so those do not have the line #include <simplecpp> at the top.

There are various ways in which we can compile this program. The simplest possibility is to issue the command

```
s++ main.cpp lcm.cpp gcd.cpp
```

This will produce an executable file which will indeed find the LCM of 36,24 when run.

# 11.2.3 Separate compilation and object modules

But there are other ways of compiling as well. We can separately compile each file. Since each file does not contain the complete program by itself, an executable file cannot be produced. What the compiler will produce is called an object module, and this can be produced by issuing the command