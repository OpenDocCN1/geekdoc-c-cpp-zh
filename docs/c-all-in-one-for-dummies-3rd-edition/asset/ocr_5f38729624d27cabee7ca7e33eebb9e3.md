# # Listing 7-11: A Function Cannot Change the Original Variables Passed into It

```
    #include <iostream>

    using namespace std;

    void ChangesAreGood(int myparam)
    {
        myparam += 10;
        cout << "Inside the function:" << endl;
        cout << myparam << endl;
    }

    int main()
    {
        int mynumber = 30;
        cout << "Before the function:" << endl;
        cout << mynumber << endl;

        ChangesAreGood(mynumber);
        cout << "After the function:" << endl;
        cout << mynumber << endl;

        return 0;
    }
```

Listing 7-11 includes a function called ChangesAreGood() that modifies the parameter it receives. (It adds 10 to its parameter called *myparam*.) It then prints the new value of the parameter.

The main() function initializes an integer variable, *mynumber*, to 30 and prints its value. It then calls the ChangesAreGood() function, which changes its parameter. After coming back from the ChangesAreGood() function, main() prints the value again.

When you run this application, you see the following output:

```
    Before the function:
    30
    Inside the function:
    40
    After the function:
    30
```

Before the function call, *mynumber* is 30. And after the function call, it's still 30. But the function added 10 to its parameter. This means that when the function modified its parameter, *the original variable remained untouched*. The two are separate entities. Only the value 30 went into the function. The actual variable did not. It stayed in main().

That keeps mean and nasty functions from messing things up in the outside world. But what if you write a function that you *want* to modify the original variable?