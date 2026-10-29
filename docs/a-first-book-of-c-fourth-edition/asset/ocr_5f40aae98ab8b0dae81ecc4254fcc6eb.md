Enter a grade: 75
Enter a grade: 92

grade[0] is 85
grade[1] is 90
grade[2] is 78
grade[3] is 75
grade[4] is 92

In reviewing the output of Program 7.1, pay attention to the difference between the subscript value displayed and the numerical value stored in the corresponding array element. The subscript value refers to the element's location in the array, and the subscripted variable refers to the value stored in the designated location.

In addition to simply displaying the values stored in each array element, elements can also be processed by referencing the desired element. For example, in Program 7.2, the value of each element is accumulated in a total, which is displayed after all array elements have been displayed.

# Program 7.2

```
#include <iostream>
using namespace std;
int main()
{
    const int NUMELS = 5;
    int i, grade[NUMELS], total = 0;

    for (i = 0; i < NUMELS; i++)  // Enter the grades
    {
        cout << "Enter a grade: ";
        cin >> grade[i];
    }

    cout << "\nThe total of the grades";

    for (i = 0; i < NUMELS; i++)  // Display and total the grades
    {
        cout << " " << grade[i];
        total = total + grade[i];
    }

    cout << " is " << total << endl;

    return 0;
}
```