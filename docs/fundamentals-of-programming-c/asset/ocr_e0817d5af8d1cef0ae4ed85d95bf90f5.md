# 18. CLASS TEMPLATES

```
#include "llist.h" // Was => #include "intlist.h"
#include <iostream>

using namespace std;

int main() {
    bool done = false;
    char command;
    int value;
    LList<int> list; // Was => IntList list;

    while (!done) {
        cout << "Insert <item> P)rint L)length E)rase Q)uit >>";
        cin >> command;
        switch (command) {
            case 'I': // Insert a new element into the list
            case 'i':
                if (cin >> value)
                    list.insert(value);
                else
                    done = true;
                break;
            case 'P': // Print the contents of the list
            case 'p':
                list.print();
                break;
            case 'L': // Print the list's length
            case 'l':
                cout << "Number of elements: " << list.length() << endl;
                break;
            case 'E': // Erase the list
            case 'e':
                list.clear();
                break;
            case 'Q': // Exit the loop (and the program)
            case 'q':
                done = true;
                break;
        }
    }
}

```

The statement

LList<int> list;

instantiates an actual class where all occurrences of T become int. It also declares list to be an object of this instantiated class.

Just as we instantiate function templates with multiple different types within the same program, we can do the same for class templates. The class template LList in Listing 18.9 (llist.h) makes the following client code:

```
LList<int> intlist;
LList<string> strlist;

```