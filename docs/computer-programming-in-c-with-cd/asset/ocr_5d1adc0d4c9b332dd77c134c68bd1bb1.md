```
```cpp
struct length
{
    int feet;
    int inch;
};

int main()
{
    length height;

    height.feet = 5;
    height.inch = 10;

    cout<<"Your height is : ";
    cout<<height.feet<<" feet ";
    cout<<height.inch<<" inch";

    return 0;
}
```
```

# Output:

Your height is : 5 feet 10 inch

In Listing 2, the structure length is declared that contains two integer elements that are feet and inch. Then, in the main() function a variable (height) of structure length is declared. This object is used to access the elements of structure length, by using the dot (.) operator.

# TEST YOUR KNOWLEDGE

**Q1.** Create a program using the structure that accepts Student ID and name of the student and displays them on the screen.

Ans.

```
```cpp
#include <iostream.h>

struct Student
{
    char name[20];
    int ID;
};

int main()
{
    cout<<"Enter the record of the student"<<"\n";
    cout<<"------------------------------"<<"\n";
    Student s;
    cout<<"Enter Name of the Student: ";
```
```