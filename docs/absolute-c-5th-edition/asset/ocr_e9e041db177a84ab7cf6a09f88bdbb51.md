# Self-Test Exercises (continued)

```
return;

namespace Outer {
    void message() {
        cout << "Outer.\
";
    }
    namespace Inner {
        void message() {
            cout << "Inner.\
";
        }
    }
}
```

# Chapter Summary

+   - You can define a class and place the definition of the class and the implementation of its member functions in separate files. You can then compile the class separately from any program that uses it, and you can use this class in any number of different programs.
- A namespace is a collection of name definitions, such as class definitions and variable declarations.
- There are three ways to use a name in namespace: by making all the names in the namespace available with a using directive, by making the single name available with a using declaration for the one, or by qualifying the name with the name of the namespace and the scope resolution operator.
- You place a definition in a namespace by placing the definition in a namespace grouping for that namespace.
- The unnamed namespace can be used to make a name definition local to a compilation unit.

# Answers to Self-Test Exercises

+   - Parts a, b, and c go in the interface file; parts d through h go in the implementation file. (All the definitions of class operations of any sort go in the implementation file.) Part i (that is, the main part of your program) goes in the application file.