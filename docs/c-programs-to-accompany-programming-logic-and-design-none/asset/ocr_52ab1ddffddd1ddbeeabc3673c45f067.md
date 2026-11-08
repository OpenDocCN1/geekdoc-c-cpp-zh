# WRITING CONTROL BREAK PROGRAMS

```
```text
endwhile
print CATEGORY_FOOTER, categoryTotal
grandTotal = grandTotal + categoryTotal
print FOOTER, grandTotal
stop

num categoryChange(num categoryTotal, num grandTotal)
    string CATEGORY_FOOTER = "Category count "
    print CATEGORY_FOOTER, categoryTotal
    grandTotal = grandTotal + categoryTotal
return grandTotal
```
```

Figure 8-2 Bookstore program pseudocode *(continued)*

```
```cpp
// Bookstore.cpp – This program creates a report that lists
// all of the books carried by a bookstore with a count
// for each book category and a grand total.
// Input:  Interactive.
// Output: Report
#include <iostream>
#include <string>
using namespace std;
int categoryChange(int, int);
int main()
{
    double price;
    string title, author, category;
    const string HEADING = "Book List";
    const string FOOTER = "Total number of book titles ";
    const string CATEGORY_FOOTER = "Category count ";
    const string SENTINEL = "done";
    int grandTotal = 0;
    string prevCategory = "";
    int categoryTotal = 0;
    bool notDone = true;

    cout << "\t\t\t\t\t" << HEADING << endl;
    cout << "Enter a book title or done to quit: ";
    cin >> title;
    if(title == SENTINEL)
    {
        notDone = false;
    }
}
```
```

Figure 8-3 Bookstore program written in C++