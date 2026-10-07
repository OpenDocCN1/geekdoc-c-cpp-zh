
## Chapter 2 Setting Out to C++

This statement provides two kinds of information: the type of memory storage needed and a label to attach to that storage. In particular, the statement declares that the program requires enough storage to hold an integer, for which C++ uses the label int. The compiler takes care of the details of allocating and labeling memory for that. C++ can handle several cases, or types, of data, and the int is the most basic data type. It corresponds to an integer, with no fractional part. The C++ int can be positive or negative, the size range depends on the implementation. Chapter 3 provides the details on int and the other basic types.

Naming the storage is the second task achieved. In this case, the statement declares henceforth the program will use some carrots to identify the value stored at location. However, carrots is called a variable because you can change its value. In C++ you must declare all variables. If you were to omit the declaration in carrots.cpp, the compiler would report an error when the program attempts to use carrots further. On, you might want to try omitting the declaration to see how your compiler responds. Then if you see that response in the future, you'll know to check for omitted declarations.

## Why Must Variables Be Declared?

Some languages, notably BASIC, create a new variable whenever you use a new name, without the aid of explicit declarations. That might seem unfamiliar to the user, and it is—in the short term. The problem is that if you missp the name of a variable, you inadvertently create a new variable without realizing it. That is, in BASIC, you can do something like the following:

```
CastleDark = 34

CastleDank = CastleDark + MoreGhosts
...
PRINT CastleDark
```

Because CastleDank is misspelled (the r was typed as an n), the changes you make to leave CastleDank unchanged. This kind of error can be hard to trace because it breaks rules in BASIC. However, in C++, CastleDank would be declared while the misspelled CastleDank would not be declared. Therefore, the equivalent C++ code breaks the rule about the need to declare a variable for you to use it, the compiler catches the error and stomps the potential bug.

In general, a declaration indicates the type of data to be stored and the name the program will use for that data's stored there. In this particular case, the program creates a variable called carrots in which it can store an integer (see Figure 2.4).

The declaration statement in the program is called a defining statement, or definition, for short. This means that its presence causes the compiler to allocate space for the variable. In more complex situations, you can also have reference declarations. These tell the computer to use a variable that has already been defined elsewhere. In general, a declaration need not be a definition, but in this example it is.

C++ Statements

43

```
int carrots;
type of name of
data variable
stored
semicolon
marks end of
statement
```

Figure 2.4 A variable declaration.

If you're familiar with C or Pascal, you're already familiar with variable declarations. You might also have a modest surprise in store for you. In C and Pascal, all variable declarations normally come at the very beginning of a function or procedure. But C++ has no such restriction. The usual C++ style is to declare a variable before it is first used. That way, you don't have to rummage back through a program to see what the type is. You will see an example of this later in this chapter. This style has the disadvantage of not gathering all your variable names in one place; thus, you can't tell at a glance what variables a function uses. (Incidentally, C99 now makes the rules for C declarations much the same as for C++).

Tip

The C++ style for declaring variables is to declare a variable as close to its first use as possible.

## Assignment Statements

An assignment statement assigns a value to a storage location. For example, the following statement assigns the integer 25 to the location represented by the variable carrots:

```
carrots = 25;
```

The symbol is called the assignment operator. One unusual feature of C++ (and C) is that you can use the assignment operator serially. For example, the following is valid code:

```
int steinway;
int baldwin;
int yamaha;
yamaha = steinway = 88;
```

The assignment works from right to left. First, 88 is assigned to steinway; then the value of steinway is assigned to baldwin; then baldwin's value is assigned to yamaha. (C++ follows C's penchant for allowing weird-appearing code.)

The second assignment in Listing 2.2 demonstrates that you can change the variable:

```
carrots = carrots - 1; // modify the variable
```

## Chapter 2 Setting Out to C++

The expression to the right of the assignment operator (carrots - 1) is an example of an arithmetic expression. The computer will subtract 1 from 25, the value of carrots, obtaining 24. The assignment operator stores this new value in the carrots location.

## A New Trick for cout

Up until now, the examples in this chapter have given cout strings to print. Listing 2.2 gives cout a variable whose value is an integer:

```
cout << carrots;
```

The program doesn't print the word carrots; instead, it prints the integer value stored in carrots, which is 25. Actually, this is two tricks in one. First, cout replaces carrots with its current value of 25. Second, it translates the value to the proper output characters.

As you see, cout works with both strings and integers. This might not seem particularly remarkable, but keep in mind that the integer 25 is something different from the string "25". The string holds the characters with which you write the number (that is, a 2 character and a 5 character). The program internally stores the numeric codes for the 2 and the 5 character. To print the string, cout simply prints each character in the string. But the computer stores the integer 25 as a binary number. (Appendix A, "Number Bases," details this representation.) The main point is that cout must translate a number in integer format into character form before it can print it. Furthermore, cout is smart enough to recognize that carrots is an integer that requires conversion.

Perhaps the contrast with C will indicate how clever cout is. To print the string "25" and the integer 25 in C, you could use C's multipurpose output function printf():

```
printf("Printing a string: %s\n", "25\n");
printf("Printing an integer: %d\n", 25);
```

Without going into the intricacies of printf(), you must use special codes (%s and %d) to indicate whether you are going to print a string or integer. And if you tell printf() to print a string but give it an integer by mistake, printf() is terrific to notice your mistake. It just goes ahead and displays garbage.

## cout and printf()

If you used C and printf(), you might think cout looks odd. You might even prefer to cling to your hard-won mastery of printf(). But cout is actually no stranger in appearance to printf(), with all its conversion specifications. More importantly, cout has significant advantages. Its capability to recognize types reflects a more intelligent and foolproof design. Also, it is extensible. That is, you can redefine the << operator so that cout can recognize new types you develop. And if you relish the fine control printf() provides, you can accomplish the same effects with more advanced uses of cout (see Chapter 17. “Input, Output, and Files”).

## More C++ Statements

Let's look at a couple more examples of statements. The program in Listing 2.3 expands on the preceding example by allowing you to enter a value while the program is running. To do so, you use cin (pronounced "see-in"), the input counterpart to cout. Also the program grows yet another way to use that versatility, the cout object.

Listing 2.3 getinfo.cpp

```
// getinfo.cpp -- input and output
#include <iostream>

int main()
{
    using namespace std;

    int carrots;

    cout << "How many carrots do you have?" << endl;
    cin >> carrots; // C++ input
    cout << "Here are two more.";
    carrots = carrots + 2;
    // the next line concatenates output
    cout << "Now you have " << carrots << " carrots." << endl;
    return 0;
}
```

## Program Adjustments

If you found you had to add a cin.get() statement in the earlier listings, you will need to add two cin.get() statements to this listing to keep the program visible onscreen. The first one will read the newlined when you press the Enter or Return key after typing a number, the second will cause the program to pause until you hit Return or Enter again.

Here is an example of output from the program in Listing 2.3:

How many carrots do you have?
12
Here are two more. Now you have 14 carrots.
