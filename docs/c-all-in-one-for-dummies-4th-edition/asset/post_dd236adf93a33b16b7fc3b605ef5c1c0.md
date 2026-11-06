
## Passing Pointer Variables to Functions

One of the most important uses for pointers is this: If a pointer points to a variable, you can pass the pointer to a function, and the function can modify the original variable. This functionality lets you write functions that can actually modify the variables passed to them. Even though this section discusses raw pointers, the same techniques work with smart pointers.

Normally, when you call a function and you pass a few variables to the function, the computer just grabs the values out of the variables and passes those values. Take a close look at the VariablePointer example, shown in Listing 8-13.

### LISTING 8-13: A Function Cannot Change the Original Variables Passed into It

```cpp
#include <iostream>

using namespace std;

void ChangesAreGood(int myparam) {
    myparam += 10;
    cout << "Inside the function:" << endl;
    cout << myparam << endl;
}

int main() {
    int mynumber = 30;
    cout << "Before the function:" << endl;
    cout << mynumber << endl;

    ChangesAreGood(mynumber);
    cout << "After the function:" << endl;
    cout << mynumber << endl;

    return 0;
}
```

Listing 8-13 includes a function called ChangesAreGood() that modifies the parameter it receives. (It adds 10 to its parameter called myparam.) It then prints the new value of the parameter.

The main() function initializes an integer variable, mynumber, to 30 and prints its value. It then calls the ChangesAreGood() function, which changes its parameter.

### LISTING 8-14: *(continued)*

```cpp
    cout << *myparam << endl;
    }

    int main() {
        int mynumber = 30;
        cout << "Before the function:" << endl;
        cout << mynumber << endl;

        ChangesAreGood(&mynumber);
        cout << "After the function:" << endl;
        cout << mynumber << endl;

        return 0;
    }
```

When you run this application, you see the following output:

```text
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

```cpp
(*myparam) += 10;
```

### PASSING BY VALUE VERSUS BY REFERENCE

If you work with other languages, you’ll come across the terms *passing by value* and *passing by reference*. The first term, *passing by value*, means sending the actual value of a variable to a function when you call it. When working with C++, you accomplish this task by calling the function with the variable, as shown in Listing 8-13. The second term, *passing by reference*, means sending the address of the variable to the function so that the function can modify the original content of that variable. When working with C++, you accomplish this task by calling the function with a pointer, as shown in Listing 8-14. C++ uses the terminology it does because C++ can work with pointers directly rather than hide the underlying mechanics of what is happening using special techniques or keywords.

![](img/128ab511de4e7360e167e3b15cdd5dd0_240_0.png)

The `ChangesAreGood()` function in Listing 8-14 no longer modifies its own parameter. The parameter holds the address of the original mynumber variable, and that never changes. Throughout the function, the pointer variable myparam holds the mynumber address. And any changes the function performs are on the dereferenced variable, which is mynumber.

## Returning Pointer Variables from Functions

Functions can return values, including pointers. To set up a function to return a pointer, specify the type followed by an asterisk at the beginning of the function header. The ReturnPointer example, shown in Listing 8-15, demonstrates this technique. The function returns a pointer that is the result of a new operation.

### LISTING 8-15: Returning a Pointer from a String Involves Using an Asterisk in the Return Type

```cpp
#include <iostream>
#include <sstream>
#include <stdlib.h>

using namespace std;

string *GetSecretCode() {
    string *code = new string;
    code->append("CR");

    int randomnumber = rand();
    ostringstream converter;
    converter << randomnumber;
    code->append(converter.str());

    code->append("NQ");
    return code;
}

int main() {
    string *newcode;

    for (int index = 0; index < 5; index++) {
        newcode = GetSecretCode();
        cout << *newcode << endl;
    }

    return 0;
}
```

The `main()` function creates a pointer to a string named `newcode`. `GetSecretCode()` returns a pointer to a string, so `newcode` and the function return value match. When you use `newcode`, you must dereference it.

When you run this application, you see something like the following output:

```text
CR41NQ
CR18467NQ
CR6334NQ
CR26500NQ
CR19169NQ
```

![](img/128ab511de4e7360e167e3b15cdd5dd0_241_0.png)

**WARNING** — Never return from a function the address of a local variable in the function. The local variables live in the stack space allocated for the function, not in the heap. When the function is finished, the computer frees the stack space used for the function, making room for the next function call. If you try this, the variables will be okay for a while, but after enough function calls follow, the variable’s data will get overwritten.

### RANDOM NUMBERS AND STRINGS

Some special code appears in GetSecretCode() that requires explanation. The call to int randomnumber = rand(); generates a random number. To obtain a random number and convert it to a string, you add two more include lines:

```cpp
#include <stdlib.h>
#include <sstream>
```

The first line provides access to the rand() function. The second line provides access to the ostringstream type. Here are the three lines that perform the magic:

```cpp
int randomnumber = rand();
ostringstream converter;
converter << randomnumber;
```

The first of these creates a random number by calling rand(), which returns an int. The next line creates a variable of type ostringstream, which is a type that’s handy for converting numbers to strings. A variable of this type has features similar to that of a console. You can use the insertion operator (<<), except that instead of going to the console, anything you write goes into a string of type ostringstream (which comes from the words output, string, and stream; usually, things that allow the insertion operator << or the extraction operator >> to perform input and output are called streams). You can add the resulting string onto the code string variable using:

```cpp
code->append(converter.str());
```

The part inside parentheses — converter.str() — returns an actual string version of the converter variable. You use the append() function to add the string to code.

![](img/128ab511de4e7360e167e3b15cdd5dd0_242_0.png)

Just as the parameters to a function are normally values, a function normally returns a value. In the case of returning a pointer, the function is still returning just a value — it is returning the value of the pointer, which is a number representing an address.

## Referring to Your Data Through Pointers
