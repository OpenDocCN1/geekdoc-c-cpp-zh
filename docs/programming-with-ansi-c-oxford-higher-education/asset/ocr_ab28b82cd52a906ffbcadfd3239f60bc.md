```
case ASSIGNMENT:
for(i = 0; i < NoOfJobs; i++)
{
    AddAssignment();
}
break;

case PROJECT:
...
}
}
```

# Function to add information, AddJob()

The AddJob() function takes two arguments. The first is the enum value, which refers to what we are interested in inserting. We can pass ASSIGNMENT for adding an assignment to the Assignments array. Similarly, we can pass PROJECT for adding a project and REFERENCE for adding a reference in the corresponding arrays. The second argument is for multiple operations. It is not unusual to add multiple values of projects, assignments, and references together, thus calling the respective function that many times. In this example, we have added three assignments of Lara the first time and then have added two more assignments. Look at the calls made to AddJob() in the program.

```
Lara.AddJob(StudentJobs, 3);
Lara.AddJob(StudentJobs, 2);
```

Here, 3 and 2 are values passed to AddJob(), informing it that the first call needs to add three and second call needs to add two assignments. The StudentJobs value in both the cases is ASSIGNMENT, so in both the cases AddJob() adds to the Assignments array.

# Limitation of the solution

Now, the question is, what is the problem with this program? Suppose we need students to have a list of practicals completed. We should have a function such as AddPractical() that adds practicals. The AddJob() function needs to be modified to add one more case and the global enum also needs to be changed. Adding a function AddPractical() cannot be avoided, but is it possible to avoid changing AddJob() and the enum? It is possible if pointer to member functions are used. It solves the problem in such a way that adding one or more functions does not require a change in the AddJob() function and there is no further need for enum.

Program 4.16 is the same as Program 4.15 but uses a pointer to member function.

# PROGRAM 4.16 Solution using pointer to member function

```
// UsingPointerToMember.cpp
#include <iostream>
#include <string>
using namespace std;
// enum jobs {ASSIGNMENT, PROJECT, REFERENCE};
class Student
{
private:
    int RollNumber;
    string Name;
    string Address;
```