```
Widget *p1 = new Widget(10);
Widget *p2 = new Widget(20);
Widget *p3 = new Widget(30);
Widget *p4 = new Widget(40);
delete p2;
delete p1;
delete p4;
// Not deleting p3, introducing a memory leak
std::cout << "Leaving test_widget_pointers" << '\n';
}
```

```
int main() {
  std::cout << "Entering main" << '\n';
  test_widget_objects();
  test_widget_pointers();
  std::cout << "Leaving main" << '\n';
}
```

Listing 18.12 (testdestructors.cpp) prints the following:

```
Creating widget 100 (2707068)
Creating widget 200 (2707064)
Entering main
Entering test_widget_objects
Creating widget 1 (14024180)
Creating widget 2 (14024184)
Creating widget 3 (14024188)
Creating widget 4 (14024192)
Entering test_widget_objects
Destroying widget 4 (14024192)
Destroying widget 3 (14024188)
Destroying widget 2 (14024184)
Destroying widget 1 (14024180)
Entering test_widget_pointers
Creating widget 10 (14790752)
Creating widget 20 (14790816)
Creating widget 30 (14790832)
Creating widget 40 (14791760)
Destroying widget 20 (14790816)
Destroying widget 10 (14790752)
Destroying widget 40 (14791760)
Leaving test_widget_pointers
Leaving main
Destroying widget 200 (2707064)
Destroying widget 100 (2707068)
```

Adding a destructor to the IntList1 class is a significant step in correcting its deficiencies, but its successors, IntList2 and IntList3, still are not ready for general release. Consider Listing 18.13 (listassign.cpp) that uses the IntList3 class that properly automatically cleans up its memory.

# Listing 18.13: listassign.cpp

```
#include "intlist3.h"
#include <iostream>
```