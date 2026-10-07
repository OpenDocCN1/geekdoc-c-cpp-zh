can do something doesn't mean you should do it." Here, however, nesting structures is a
good idea.

Using our Person structure example, every person has a birthday. A birthday is a date.
in turn, may be defined by a structure that contains three members, all
integers, which represent the month, day, and year of the particular date. The Date
structure could be declared as follows:

```
struct Date
{
    int month;
    int day;
    int year;
};
```

The Person structure declaration would then be modified to add a member variable, of the
structure named, bDay, to represent the person's birthday:

```
struct Person {
    string name;
    int height;
    Date bDay;
};
```

The following code modifies the previous one by adding the Date structure and the bDay
Date member to the Person structure, as well as modifying the setValues
function to assign a value to the bDay member variable and the getValues
function to output the value of that member variable:

```
#include <iostream>
#include <string>
using namespace std;
struct Date
{
    int month;
    int day;
    int year;
};
struct Person {
    string name;
    int height;
    Date bDay;
    void setValues(Person&);
    void getValues(const Person&);
};
int main()
{
    Person p1;
    setValues(p1);
    cout << "Outputing person data\n";
    cout << "==================================\n";
    getValues(p1);
    return 0;
}
void setValues(Person& pers)
{
```