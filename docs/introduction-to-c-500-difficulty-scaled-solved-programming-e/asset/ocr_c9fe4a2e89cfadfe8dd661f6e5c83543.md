ascending order and another function to display the data of the students who got a better grade than
average grade of all students. The program should call those two functions.

```
#include <iostream>
#include <string>
using std::cout;
using std::cin;

const int SIZE = 100;

struct Student
{
    std::string name;
    int code;
    float grd;
};

void sort_by_grade(Student studs[], int num_studs);
void show_students(const Student studs[], int num_studs, float avg_grd);

int main() {
{
    int i;
    float sum_grd;
    Student studs[SIZE];

    sum_grd = 0;
    for(i = 0; i < SIZE; i++) {
        cout << "\nGrade [0-10]: ";
        cin >> studs[i].grd;
        if(studs[i].grd == -1)
            break;

        sum_grd += studs[i].grd;
        cin.get();
    }

    cout << " "Name: ";
    getline(cin, studs[i].name);

    cout << " "Code: ";
    cin >> studs[i].code;

    if(i == 0)
        return 0;
    sort_by_grade(studs, i); /* Sort the structures in grade ascending
order. The variable i specifies the number of students. */
    show_students(studs, i, sum_grd/i); /* The last argument is the
average grade of all students. */
    return 0;
}
```

```
void sort_by_grade(Student studs[], int num_studs)
{
    int i, j;
    Student s;
```