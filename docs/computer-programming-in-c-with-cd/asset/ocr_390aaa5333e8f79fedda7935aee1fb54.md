```
```cpp
}
}

void DisplayList()
{
for(int i=1;i<=N;i++)
cout<<Srec[i].Sname<<"  "<<Srec[i].Sid<<"  "<<Srec[i].Marks.Total<<endl;
}

};

void main()
{

MeritList Obj;
Obj.Input();
Obj.SortStudentRec();
Obj.DisplayList();

}
```
```

Q28: Develop a class for linked list operations and the class template is given below and expand all the member functions out side class. Also write a driver program (main program) (Mumbai University, December 2007)

# Ans:

```
```cpp
#include<iostream.h>
#include<conio.h>
#include<ctype.h>

class node
{

public:

int data;
node * link;
};

class List
{

node * Head;
```
```