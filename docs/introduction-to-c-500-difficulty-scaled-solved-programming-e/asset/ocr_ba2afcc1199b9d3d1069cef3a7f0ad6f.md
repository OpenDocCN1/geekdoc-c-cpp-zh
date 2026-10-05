The word void explicitly states that main() does not accept parameters; however it is unnecessary because the empty parentheses () indicate the name. In Chapter 11 we will see another declaration of main(), where main() takes parameters. Note that the return statement can be omitted. If it is omitted, the program will automatically return the value 0. The result is the same, my preference is to use the return statement so that it is clearly shown.

cout is an object that is declared in the std namespace and it is associated with the standard output (e.g., screen). cout knows how to display a variety of data including strings, numbers, and individuals. In C++, characters enclosed in " are a string literal. Note indicates that the string is set to cout. As we will see in Chapter 3, the new line character\n moves the cursor to the beginning of the next line. The main reason I add\n at the end of the string is that messages like Press any key to continue, which may be displayed by some compilers after the program is finished, appear on the next line.

# Writing Style

Regarding the syntax of the program, the braces {} do not have to be placed in separate lines. For example, we can add the next to main() and write main() or the next to the return statement. Also, it is not necessary to indent the code. As you wish, there are many ways to write the program. For example, we could write main() and put the code in a single large line; however, that option would make our program illegible. A line may contain multiple statements. For example, it is legal to write:

```
std::cout << "Hey Ho, Let's Go\n"; return 0;
```

Aside from the people who may have, what really matters is that a program should be written in such a way that it is easy to read not only by the person who wrote it, but also by others who are going to read it. For readability, the writing style I prefer is to use the {} in separate lines, each statement in one line, and indent the code.

# Namespaces

Let's make a short introduction to namespaces. C++ allows the grouping of data (e.g., classes, functions, variables, ...) in a common namespace. The namespace is a part of the program, in which certain names (e.g., variables) are declared. These names are not known outside of this area. For example, all the names of the standard library are defined in a namespace called std. As we will see in Chapter 25, in order to access an element, we must write the namespace followed by the scope operator :: For example, when we write std::cout we access the cout object that is declared in the std namespace. If we want to make available all the names of the std namespace, we write:

```
using namespace std;
```

Now, we don't need to add the prefix std:: before the names we use, that is, we can write:

```
cout << "Hey Ho, Let's Go\n";
```

Alternatively, we can make available only the names that we use. This is achieved by corresponding std:: declarations. For example:

```
using std::cout;
```

Now, we don't need to add the prefix std:: when we use the cout, while we have to add it when using other std names. The convention I usually follow is to separate declarations for the