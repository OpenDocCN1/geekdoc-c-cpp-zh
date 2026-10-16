# Introducing the Inventory Referencer Program

The Inventory Referencer program demonstrates returning references. The program displays the elements of a vector that holds a hero’s inventory by using returned references. Then the program changes one of the items through a returned reference. Figure 6.4 shows the results of the program.

![](bbox=[0.112, 0.263, 0.758, 0.51])

# Figure 6.4

The items in the hero’s inventory are displayed and changed by using returned references.

You can download the code for this program from the Course Technology website (www.courseptr.com/downloads). The program is in the Chapter 6 folder; the filename is inventory_referencer.cpp.

```
// Inventory Referencer
// Demonstrates returning a reference

#include <iostream>
#include <string>
#include <vector>

using namespace std;

//returns a reference to a string
string& refToElement(vector<string>& inventory, int i);
```