An important requirement for insertion in sorted associative container is that the object that is inserted must obey some form of ordering. This ordering can be achieved by overloading operator < () const for each of the objects that is to be inserted in these sorted associative containers.

The operator function must be defined as const. It is also important to note that these containers are also associative, and an element of the record can be used to access the entire record.

A sequence container element is accessed by the index or position of the element (similar to an array), whereas a sorted associative container element is accessed by a key value, which is a part of the element, similar to indexed sequential files. However, sorted associative container also allows sequential operation.

> Note Associative containers are named so because they help accessing elements in an associative manner rather than indexed manner. Associative search is quite usual in human processing system. It is common for us to hear a few bars of music associated with a specific song and recall that song rather than being provided with information such as the name of the movie and singer and then recalling it.

# 16.6.5 Maps

We are going to look at map first, which is a container that can have two items, namely, a key and a value stored in itself. It is automatically sorted on the key item at the time of insertion. As mentioned earlier, the key item must have some form of ordering. For user-defined objects, it is important to overload operator < as const to have the ordering.

Let us look at Program 16.7 first. There are two items; the first is a Student object, used as a key, and the second (the value) is an integer. As mentioned earlier, the Student object must observe some order. The order here is maintained on the basis of the total mark the student possesses. Thus, it is possible to have the merit list. The perception of ordering depends on the context. If one wants a roll-call to be programmed, maybe the roll number is the key in ordering, or if students list is to be printed namewise, the name of the student may form the key for ordering.

> Map is a container with a pair of items, namely, a key and a value stored in a sorted order of key.

# PROGRAM 16.7 Map

```
//Map.cpp
#include <map>
#include <string>
#include <iostream>
#include <algorithm>
using namespace std;
class Student
{
private:
    int RollNumber;
    float TotalMarks;

public:
    Student(){};
    Student(int TempRollNumber, float TempTotalMarks)
    {
        RollNumber = TempRollNumber;
        TotalMarks = TempTotalMarks;
    }

    bool operator < (Student TempStud) const
```