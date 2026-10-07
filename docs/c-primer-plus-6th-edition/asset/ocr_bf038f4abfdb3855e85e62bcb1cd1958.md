# 32 Chapter 2 Setting Out to C++

# Why main() by Any Other Name Is Not The

There's an extremely compelling reason to name the function in the myfirst.cpp program main():You must do so. Ordinarily, a C++ program requires a function called main().(And not by the way, main() or MAIN() or mane. Remember, case and spelling count the myfirst.cpp program has only one function, that function must bear the responsibility of being main().When you run a C++ program, execution always begins at the beginning of the main() function. Therefore, if you don't have main(), you don't have a complete program, and the compiler points out that you haven't defined a main() function.

There are exceptions. For example, in Windows programming you can write a dynamic library (DLL) module. This is code that other Windows programs can use. Because a DLL module is not a standalone program, it doesn't need a main(). For specialized environments, such as a controller chip in a robot, might not need a main(). Some programming environments provide a skeleton program called some nonstandard function, such as _main();in that case there is a hidden main() that calls _main().But your ordinary standalone program does need a main(); this discusses sorts of

# C++ Comments

The double slash (// introduces a C++ comment. A comment is a remark from the programmer to the reader that identifies a section of a program or explains some aspect of the code. The compiler ignores comments. After all, C++ at least as well as you do, and, in any case, it's incapable of understanding comments. As far as the compiler is concerned, Listing 2.1 looks as if it were written without comments, like this:

```
#include <iostream>
int main()
{
	using namespace std;
	cout << "Come up and C++ me some time.\n	cout << endl;
	cout << "You won't regret it!" << endl;
	return 0;
}
```

C++ comments run from the // to the end of a line. A comment can be on its own line, or it can be on the same line as code. Incidentallyally, note the first line in Listing 2.1:
// myfirst.cpp -- displays a message

In this book all programs begin with a comment that gives the filename for the source code and a brief program summary. As mentioned in Chapter 1, the filename extension for source code depends on your C++ system. Other systems might use myfirst.C or myfirst.cxx for names.