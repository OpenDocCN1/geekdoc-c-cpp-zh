```
break;
case 'P': // Print the contents of the list
case 'p':
   list.print();
   break;
case 'L': // Print the list's length
case 'l':
   std::cout << "Number of elements: " << list.length() << '\n';
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

Listing 19.11 (stringlistmain.cpp) adds the extra #include directive for the string library, but observe that the only executable statements that differ from Listing 19.10 (intlistmain.cpp) are

```
std::string value;
LinkedList<std::string> list; // Instantiated for strings
```

vs.

```
int value;
LinkedList<int> list; // Instantiated for integers
```

All the other code in both programs is identical.

Just as we can instantiate function templates with multiple different types within the same program, we can do the same for class templates. The class template LinkedList in Listing 19.9 (linkedlist.h) makes the following client code possible:

```
LinkedList<int> intlist;
LinkedList<std::string> strlist;
intlist.insert(5);
strlist.insert("Wow");
intlist.print();
strlist.print();
```

This code fragment simultaneously manages lists of integers and lists of string objects.

Listing 19.12 (listoflists.cpp) shows how we can use our generic list to build a list of lists.

```
Listing 19.12: listoflists.cpp

#include <iostream>
#include "linkedlist.h"

int main() {
   // First build some lists that contain integers
```