# Classes 253

For the moment ignore the word public: shown in Display 6.3. The rest of the definition of the class DayOfYear is very much like a structure definition, except that it uses the keyword class instead of and lists the member function output (as well as the member variables month and day). Notice that the member function output is listed by giving its declaration (prototype). A class definition contains only the declaration for its members. The definitions for the member functions are usually given elsewhere. In a C++ class definition, you can intermix the member variables and functions in any way you wish, but the style we will follow has a tendency to list the member functions before the member variables.

member function

# Display 6.3 Class with a Member Function (part 1 of 3)

```
//Program to demonstrate a very simple example of a class.
//A better version of the class DayOfYear will be given in Display 6.4.
#include <iostream>
using namespace std;
Normally, member variables are private and not public, in this example. This is discussed bit later in this chapter.
class DayOfYear {
public:
    void output ( ); // Member function declaration
    int month;
    int day;
};
int main() {
    DayOfYear today, birthday;
    cout << "Today's date:\n";
    cout << "Enter month as a number: ";
    cin >> today.month;
    cout << "Enter the day of the month: ";
    cin >> today.day;
    cout << "Enter your birthday:\n";
    cout << "Enter month as a number: ";
    cin >> birthday.month;
    cout << "Enter the day of the month: ";
    cin >> birthday.day;
    cout << "Today's date is ";
    today.output((); // Calls to the member function
    cout << endl;
    cout << "Your birthday is ";
    birthday.output();
    cout << endl;
    if (today.month == birthday.month && today.day == birthday.day) 
        cout << "Happy Birthday!\n";
}
```

(continued)