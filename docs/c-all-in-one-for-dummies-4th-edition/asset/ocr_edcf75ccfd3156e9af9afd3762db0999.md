# **LISTING 8-14:** *(continued)*

```
    cout << *myparam << endl;
    }

    int main() {
        int number = 30;
        cout << "Before the function:" << endl;
        cout << number << endl;

        ChangesAreGood(&number);
        cout << "After the function:" << endl;
        cout << number << endl;

        return 0;
    }
```

When you run this application, you see the following output:

```
    Before the function:
    30
    Inside the function:
    40
    After the function:
    40
```

Notice the important difference between this and the output from Listing 8-13: The final line of output is 40, not 30. The variable was modified by the function!

To understand how this happened, first look at `main()`. The only difference in `main()` is that it has an ampersand (&) in front of the `mynumber` argument in the call to `ChangesAreGood()`. `ChangesAreGood()` receives the address of `mynumber`.

Now the function has some major changes. The function header takes a pointer rather than a number. You perform this task by adding an asterisk (`*`) so that the parameter is a pointer variable. This pointer receives the address being passed into it. Thus, it points to the variable mynumber. Therefore, any modifications made by dereferencing the pointer will change the original variable. The following line changes the original variable.

```
    (*myparam) += 10;
```