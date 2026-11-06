Look at that code! No more pointers! In `main()`, you don't need to take the address of anything, and you don't need to use that *dereference* word, which the spelling checker insists is wrong. And the function itself has no pointers, either. You just throw the old ampersand-thing in front of the parameter name in the function header.

![](bbox=[0.141, 0.235, 0.214, 0.295])

If you have `string` parameters, and you use the `&` to pass them by reference, skip the shortcut `->` notation to call the `string` functions. And don't dereference anything. There are no pointers. Just type the dot (or period) and the function. No asterisks needed.

![](bbox=[0.141, 0.334, 0.214, 0.394])

If you write a function that uses a reference and somebody else uses your function in code (see Book I, Chapter 6, for information on how to do this), you could end up making that other person angry. The other person may not realize that, “Hey, man — this thing just messed up my variable!” WHAM! The variable gets changed. How do you avoid this? Warn the other person. Make it clear to anybody using your function that it uses references and will modify variables, even the unsuspecting little ones.

# ## Passing By const Reference

In Listing 7-13, you see how to modify a `string` by passing it to a function by reference. Let’s say that you still want to pass the `string` by reference, but you don’t want to allow anyone to modify it. Maybe you intend to use the `string` later for some other purpose. Of course, you could just pass the `string` by value, and the caller couldn’t modify it. The problem is that strings can get rather large, and moving all that data to a function is really time consuming — passing a reference is simpler and faster. Using a `const` reference makes it possible to get the speed benefits of using a reference, with the unchangeable nature of passing by value. The `VariablePointer4` example, shown in Listing 7-17, demonstrates how to perform this task.

# ### Listing 7-17: Using a `const` Reference to Get Speed and Unchangeable Data

```
```cpp
#include <iostream>

using namespace std;

string Paranoid(const string *realMessage)
{
    string NewString = *realMessage;
    NewString[6] = '!';
    NewString.replace(9, 1, "");
    NewString.insert(18, "Ad");
    NewString.replace(15, 2, "in");
    NewString.replace(23, 7, "!");
    NewString.replace(4, 3, "ali");

    return NewString;
}
```
```