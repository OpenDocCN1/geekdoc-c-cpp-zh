# Program 13.1

```
// a program that defines and populates a structure
#include <iostream>
using namespace std;

int main()
{
  struct {
    int month;
    int day;
    int year;
  } birth;

  birth.month = 12;
birth.day = 28;
birth.year = 86;

  cout << "* My date is *"
    << birth.month << " /"
    << birth.day << " /"
    << birth.year << endl;

  return 0;
}
```

As in C++ statements, the spacing of a structure definition isn't rigid. For example, the birth structure could just as well have been defined as the following:

struct {int month; int day; int year;} birth;

Also, as with all C++ definition statements, multiple variables can be defined in the same statement. For example, the definition statement

```
struct {
  int month;
  int day;
  int year;
} birth, current;
```