# 7 Arrays 139

```
int num;
cin >> num;
vector<double> vec(num); // Create a vector of num doubles.
```

The following program reads a number of students, creates a vector object that contains their grades and a second one with their names. It, displays the names and the grades of the students with a grade greater than equal to the average grade.

```
#include <iostream> // Example 7.4
#include <string>
#include <vector>
using namespace std;
```

```
int main() {
    int i, num;
    float avg, sum;

    cout << "Enter number of students: ";
    cin >> num;

    vector<float> grd(num);
    vector<string> names(num);

    sum = 0;
    for(i = 0; i < num; i++) {
        cout << "Enter grade: ";
        cin >> grd[i];
        cin.get();

        cout << "Enter name: ";
        getline(cin, names[i]);
        sum += grd[i];
    }
    avg = sum/num;
    for(i = 0; i < num; i++)
        if(grd[i] >= avg)
            cout << names[i] << ": " << grd[i] << '\n';

    return 0;
}
```

We discuss the string class in Chapter 10. For now, consider that each name is stored in a string object. The vector contains elements of string type. We use the [] operator to access the elements, as we do with arrays. As we learn in Chapter 18, the vector class overloads the [] operator. Also, the vector class provides the at() function, which takes as an argument the index of the element.

```
for(i = 0; i < num; i++)
    cout << names.at(i) << ": " << grd.at(i) << '\n';
```

The difference with the [] operator is that at() checks for exceeding the bounds of the vector and in such a case it creates the out_of_range exception (we discuss exceptions in Chapter 22). Therefore, if you care about safety, use at() and check for exceptions. On the other hand, if you are sure that your code never exceeds the limits, use [] for greater speed.