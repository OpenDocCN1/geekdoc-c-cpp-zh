Notice the `SetUserName()` function header: It starts with the word `void`, which means that it returns nothing at all. It’s like outer space: There’s just a big void with nothing there, and nothing is returned, except for static from the alien airwaves, but we won’t go there. Also notice that, because this function does not return anything, there is no `return` statement.

Now, of course, this function really doesn’t do a whole lot other than print the new username to the console, but that’s okay; it shows you how you can write a function that does not return anything.

![](bbox=[0.115, 0.276, 0.21, 0.349])

A function of return type `void` returns nothing at all.

Do not try to return something in a function that has a return type of `void`. *Void* means that the function returns nothing at all. If you try to put a `return` statement in your function, you get a compile error.

# ### Keeping your variables local

Everybody likes to have their own stuff, and functions are no exception. When you create a variable inside the code for a function, that variable will be known only to that particular function. When you create such variables, they are called *local variables*, and people say that they are local to that particular function. (Well, *computer* people say that, anyway.)

To see a local variable at work, consider the code in the `PrintName` example:

```
```cpp
#include <iostream>

using namespace std;

void PrintName(string first, string last)
{
    string fullname = first + " " + last;
    cout << fullname << endl;
}

int main()
{
    PrintName("Thomas", "Jefferson");
    return 0;
}
```
```

Notice in the `PrintName()` function that you declare a variable called `fullname`. You then use that variable in the second line in the function, the one starting with `cout`. But you cannot use the variable inside `main()`. If you try to do, as in the following code, you get a compile error:

```
```cpp
int main()
{
    PrintName("Thomas", "Jefferson");
    cout << fullname << endl;
    return 0;
}
```
```