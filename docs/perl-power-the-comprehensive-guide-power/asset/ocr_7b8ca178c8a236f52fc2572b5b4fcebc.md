# # Functions with No Arguments

The most fundamental type of function in Perl can be characterized as taking no arguments and providing no return values. Such a function resembles the blocks developed in Chapter 11, with the difference that they can be used more flexibly. Listing12_01 employs functions to replace the opening, menu, and display options. All the functions used employ no arguments and do not explicitly return values.

```
```perl
#Listing12_01
#Functions without arguments
system('cls');
$NL = "\n" ;
$ML = $NL x 5; #Multiple line returns for displays
```
```

accommodates abstraction because it allows the person who maintains the program to understand it according to the functions it uses. It accommodates development because it allows you to create programs in a staging area at the top of the program, thus avoiding the necessity of digging into what might amount to hundreds or thousands of lines of code that constitute the program.

![](bbox=[0.115, 0.108, 0.55, 0.306])

![](bbox=[0.203, 0.332, 0.568, 0.511])

> > Figure 12.5
> > The development of the program takes place at the top of the program.

> > Figure 12.6
> > Programs consisting of multiple files place defined functions in modules or packages.