A list can insert or delete an element just by rearranging the pointers, which is a constant time operation.

```
StudentIndex = find(ls.begin(), ls.end(), Maradona);
ls.insert(StudentIndex, Jaspal);
```

A new student Jaspal has been defined. The find() algorithm is used to get the iterator that points to Maradona. Next, Jaspal is inserted there using a member function insert() for list (ls.insert()). Here, the iterator is used like a file pointer for having seek-like operation. The insert() member function is available with all the containers.

Note List is the only container where insertion is a constant time operation irrespective of the location. A vector has constant time operation for insertion in the end and deque at the beginning and the end, but not at any location.

# 16.6.3 Deque

Deque, pronounced ‘deck’, is a useful container adapted into two other containers, namely, the stack and the queue. We are not going to discuss stacks and queues in this text, but they are as easy to work with as deques. Let us understand how a deque works with the help of Program 16.6.

# PROGRAM 16.6 Deques

```
//DeQueue.cpp
#include <deque>
#include <iostream>
#include <string>
using namespace std;
class Student
{
    int RollNumber;
    string Name;
public:
    Student(int TempRollNumber, string TempName)
    {
        RollNumber = TempRollNumber;
        Name = TempName;
    }
    bool operator < (Student AnotherStudent)
    {
        return(RollNumber < AnotherStudent.RollNumber);
    }
    friend ostream & operator <<(ostream & TempOut, Student & TempStud)
    {
        TempOut << "Roll number is: " << TempStud.RollNumber << endl;
        TempOut << "Name is: " << TempStud.Name << endl;
        return TempOut;
    }
};
int main()
{
    deque <Student> ds;
    Student Lara(1, "Brian Charles Lara");
    Student Beckham(2, "David Beckham");
    Student Steffi(3, "Steff Graf");
    Student Maradona(4, "Diego Maradona");
```