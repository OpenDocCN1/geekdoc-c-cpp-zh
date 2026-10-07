assigns it to the variable ch. By replacing cin>>ch with this function call, you can fix
Listing 5.16. Listing 5.17 shows the result.

# Listing 5.17 textin2.cpp

```
// textin2.cpp -- using cin.get(char)
#include <iostream>
int main()
{
    using namespace std;
    char ch;
    int count = 0;

    cout << "Characters: enter # to quit:\n";
    cin.get(ch); // use the cin.get(ch)
    while (ch != '#')
    {
        cout << ch;
        ++count;
        cin.get(ch); // use it again
    }
    cout << endl << count << " characters read\n";
    return 0;
}
```

Here is a sample run of the program in Listing 5.17:
Enterter characters: enter # to quit:

+   - Did you use a # pencil?
- Did you use a
  14 characters read

Now the program echoes and counts every character, including the spaces. Input is still
buffer, but it is still possible to type more input than what eventually reaches the program.
If you are familiar with C, this program may strike you as terribly wrong. The
c.get(ch) calls a value in the ech variable, which alters the value of the
variable. In C you must pass the address of a variable to a function if you want to change
t value of that variable. But the call to cin.get(ch) in Listing 5.17 passes ech, not &ch. In
code like this does not work. In C++ it can work, provided the function declares the
argument as a reference. The reference type is something that C++ added to C.
iostream header file declares the argument to cin.get(ch) as a reference type, so this
function can alter the value of its argument. You'll learn the details in Chapter 8. Mean-
while, the C mavens among you can relax; ordinarily, argument passing in C++ just works
as it does in C. For cin.get(ch), however, it doesn't.