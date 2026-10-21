also come from some other program or by some communication channel. It is imperative that the order of the nodes in the list does not change. This operation is analogous to array indexing. Consider the statement

```
a[i] = NewValue;
```

The old value at the ith location in the array changes to NewValue. Though the value changes, the index does not change. A similar process is required in the linked list. The content of the node must be changed but not the position. Therefore, the programmer must ensure that when the node values are copied, the next pointer is found and copied as well. Thus, a statement of the kind

```
"Node at the ith position = NewValue"
```

should change the value of that node to NewValue without changing the position of that node. The way to do this is shown in the following example.

In Program 4.7, class StudentNode uses friend non-member function GenerateStudentNode() and also friend class StudentList. Thus, GenerateStudentNode() and StudentList can access the private members of StudentNode class. Friend functions are discussed in detail in Section 4.11.

# PROGRAM 4.7 Returning a reference to an object

```
// ObjRefReturn.cpp
#include <iostream>
#include <string>
using namespace std;

// The following class describes the node in the linked list
class StudentNode
{
    string Name;
    StudentNode *NextStud;
public:
    int RollNo;

    // Inserting roll no., name and setting NextStud value to null
    void SetStud(int TempRollNo, string TempName)
    {
        RollNo = TempRollNo;
        Name = TempName;
        NextStud = '\0';
    }

    void WriteStud()
    {
        cout << "Roll number is " << RollNo << "and the name is " << Name << endl;
    }

    StudentNode * GetNextPtr()
    // Get the next pointer pointing to the next item in the list
    {
        return NextStud;
    }

    void SetNextPtr(StudentNode * TempPointer)
    // Make the next pointer point to the value passed
```