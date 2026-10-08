```
```
int main()                // C++ programs start by executing the function main
{
    cout << "Hello, World!\n";        // output "Hello, World!"
    return 0;
}
```
```

Every C++ program must have a function called main to tell it where to start executing. A function is basically a named sequence of instructions for the computer to execute in the order in which they are written. A function has four parts:

+   - A return type, here int (meaning “integer”), which specifies what kind of result, if any, the function will return to whoever asked for it to be executed. The word int is a reserved word in C++ (a keyword), so int cannot be used as the name of anything else (see §A.3.1).

+   - A name, here main.

+   - A parameter list enclosed in parentheses (see §8.2 and §8.6), here (); in this case, the parameter list is empty.

+   - A function body enclosed in a set of “curly braces” {}, which lists the actions (called statements) that the function is to perform.

It follows that the minimal C++ program is simply

```
```c
int main() { }
```
```

That’s not of much use, though, because it doesn’t do anything. The main() (“the main function”) of our “Hello, World!” program has two statements in its body:

```
```c
cout << "Hello, World!\n";            // output "Hello, World!"
return 0;
```
```

First it’ll write Hello, World! to the screen, and then it will return a value 0 (zero) to whoever called it. Since main() is called by “the system,” we won’t use that return value. However, on some systems (notably Unix/Linux) it can be used to check whether the program succeeded. A zero (0) returned by main() indicates that the program terminated successfully.

A part of a C++ program that specifies an action and isn’t an #include directive (or some other preprocessor directive; see §4.4 and §A.17) is called a statement.

# ### 2.3 Compilation

C++ is a compiled language. That means that to get a program to run, you must first translate it from the human-readable form to something a machine can