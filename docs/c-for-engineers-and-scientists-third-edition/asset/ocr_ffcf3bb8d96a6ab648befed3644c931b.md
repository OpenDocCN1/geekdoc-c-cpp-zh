# Point of Information

# A Notational Inconsistency

All the character class functions listed in Table 9.6 use the standard object-oriented notation of preceding the function's name with an object name, as in cin.get(). However, the string class getline() function uses the notation getline(cin, var). In this notation, the object (cin) appears as an argument, which is how procedural-based functions pass variables. For consistency, you would expect getline() to be called as cin.getline(). Unfortunately, this notation was already in use for getline() function created for C-style strings (which are simply one-dimensional arrays of characters, as discussed in Section 7.2), so a notational inconsistency was created.

![](bbox=[0.115, 0.313, 0.185, 0.355])

```
#include <iostream>
using namespace std;

int main()
{
    char fkey;

    cout << "Type in a character: ";
    cin.get(fkey);
    cout << " The key accepted is * " << int(fkey) << endl;

    return 0;
}
```

When Program 9.15 runs, the character entered in response to the prompt Type a character: is stored in the character variable fkey, and the decimal code for the character is displayed by explicitly casting the character into an integer to fix its display as an integer value. The following sample run illustrates this technique:

Type in a character: m
The key just accepted is 109

At this point, everything seems to be working, although you might be wondering why the decimal value of m is displayed instead of the character. In typing m, two keys are usually pressed, the m key and the Enter key. As in the previous section, these two characters are stored in a buffer after they're pressed (refer back to Figure 9.12). The first key pressed, m in this case, is taken from the buffer and stored in fkey, but the code for the Enter key is still in the buffer. Therefore, a subsequent call to get() for a character input picks up the code for the Enter key as the next character automatically. For example, take a look at Program 9.16.