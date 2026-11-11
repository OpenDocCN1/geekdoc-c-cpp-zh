```
```cpp
}
};
void main()
{
Employee emp;                 /*Creating a class object*/
Employee *ptremp;             /*Creating a pointer object of a class type*/
ptremp=&emp;                  /*Initializing pointer object with the normal
                                object of the class*/
(*ptremp).x;                  /*Accessing the data member of the class*/
(*ptremp).employeeDetails(); /*Invoking the member function of the class*/
}
```
```

In the preceding code snippet, ptremp is declared as a pointer object of the Employee class. The ptremp object is initialized with the reference of the emp object of the Employee class. The Employee class has two public class members, the x variable and the employeeDetails() function. These class members are accessed by using the ptremp pointer object. The * symbol is used to get the actual data of the location pointed by the ptremp pointer object, and the . operator is used to access the members of the Employee class. Note that in this context, the * symbol is called as a de-referencing operator. The de-referencing operator is used to retrieve the object that a pointer points to.

Another way to initialize a pointer object of a class type is by using the new operator, as shown in the following code snippet:

```
```cpp
class Employee
{
public:
int x;
void employeeDetails()
{
...
}
};
void main()
{
Employee *ptremp;             /*Creating a pointer object of a class type*/
ptremp= new (Employee);       /*Initializing pointer object with the new
                                operator*/

ptremp->x;                    /*Accessing the data member of the class*/
ptremp->employeeDetails();    /*Invoking the member function of the class*/
delete ptremp;                /*releasing memory using the delete operator*/
}
```
```

In the preceding code snippet, ptremp is declared as a pointer object of the Employee class. The ptremp pointer object is initialized with the help of the new operator and is destroyed with the delete operator. In the case of pointers, class members are accessed by using the -> operator, instead of the . operator. However, both operators perform the same task, as they are only syntactically different.