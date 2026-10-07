The following code calls the `printMessage` function:

```
printMessage(str);
```

The string variable `str`, whose value previously was assigned by user input, is passed as an argument to the `printMessage` function. The value of `str` then passed to the string variable `s`, which is the argument name in the function header of the `printMessage` function:

```
void printMessage (string s)
```

The string variable `s` is then used in the body of the `printMessage` function to output the message:

```
cout << "You inputted " << s;
```

**Figure 9-2** shows how the value of the argument of the function call is passed to the argument in the function header and then used in the body of the called function.

```
int main()
{
    printMessage(str);
    return0;
}

void printMessage (string s)
{
    count<<"You inputted"<<s;
}
```

![](bbox=[0.513, 0.427, 0.663, 0.459])

The function header must include an argument name as well as a data type so the value which is being passed by the function, stored in `str` in `main`, may be stored in a variable that can be used in the `printMessage` function. Otherwise, the value passed would have no place to store for use in the `printMessage` function.

The argument name in the function header can be the same as the name of the variable `printMessage(str)` passed in the function argument:

```
printMessage(str);
void printMessage (string str)
```

Even if so, the `str` in `main` is a separate variable from the `str` in `printMessage`. Nevertheless, I recommend to avoid confusion, using different names in the program.

# Using Multiple Function Arguments

The program we discussed used one function argument. However, a function may have two or even more function arguments.
The following modification of the `printMessage` function uses two arguments, one for the first name and one for the last:

```
#include <iostream>
#include <string>
using namespace std;
void printMessage(string, string);
```