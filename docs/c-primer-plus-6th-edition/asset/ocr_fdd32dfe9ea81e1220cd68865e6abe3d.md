Again, because the example reuses the string and valarray code, relatively little new code is needed, aside from the private helper method.

# Using the Revised Student Class

Once again, it's time to test a new class. Note that the two versions of the Student class have exactly the same public interface, so you can test the two versions with exactly the same program. The only difference is that you have to include studenti.h instead of studentc.h, and you have to link the program with studenti.cpp instead of with studentc.cpp. Listing 14.6 shows the program. Be sure to compile it along with studenti.cpp.

# Listing 14.6 use_stui.cpp

```
// use_stui.cpp -- using a class with private inheritance
// compile with studenti.cpp
#include <iostream>
#include "studenti.h"
using std::cin;
using std::cout;
using std::endl;

void set(Student & sa, int n);

const int pupils = 3;
const int quizzes = 5;

int main()
{
    Student ada[pupils] =
        {Student(quizzes), Student(quizzes), Student(quizzes)};

    int i;
    for (i = 0; i < pupils; i++)
        set(ada[i], quizzes);
    cout << "\nStudent List:\n";
    for (i = 0; i < pupils; ++i)
        cout << ada[i].Name() << endl;
    cout << "\nResults:";
    for (i = 0; i < pupils; i++)
    {
        cout << endl << ada[i];
        cout << "average: " << ada[i].Average() << endl;
    }
    cout << "Done.\n";
    return 0;
}
```