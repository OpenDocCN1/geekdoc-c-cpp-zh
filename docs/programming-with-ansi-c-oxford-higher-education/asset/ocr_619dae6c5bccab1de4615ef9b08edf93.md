Department is Exam
Designation is Informer

Details of employee number 7
Name is Kesar
Department is Exam
Designation is Coordinator

Details of employee number 8
Name is Michael
Department is Exam
Designation is Examiner

# How the Program Works

We have an array of employee objects in this program. The employee object contains employee number, name, department, and designation. It also contains two functions for reading and printing the employee object details. There is a function ListDeptWise(), which takes an array of employee objects as input and produces the list of employees for a given department. This function is defined after the definition of class employee. The ListDeptWise() function has been declared as a friend in the last line of the class definition with the following statement:

```
friend void ListDeptWise(employee[]);
```

This statement indicates that the non-member function ListDeptWise() is granted access to private class variables. The need for a friend function must be noted in this case. ListDeptWise() accesses private variables such as DeptName of employee class in the following statement:

```
(UniEmp[i].DeptName == TempDeptName);
```

If ListDeptWise() was a non-friend non-member function, it cannot access the private variables of employee such as DeptName and this statement will not be compiled.

# 4.11.1 Need for Friend Functions

Why do we require friend functions? Why not declare all functions as member functions? Consider making ListDeptWise() a member function. It actually operates on an array of employees and not on a singleton object. If we define ListDeptWise() as a member function, it will be called with a syntax such as UniEmployee[1].ListDeptWise(), which might mislead the reader of the program. ListDeptWise() need not be invoked by UniEmployee[1] alone. If we write UniEmployee[2].ListDeptWise(), the same result is obtained. In fact, even when a dummy employee object such as DummyEmp is defined and DummyEmp.ListDeptWise() is called, the same result will be obtained.

It should be noted that a reader might misinterpret that the object DummyEmp is executing a function and is being manipulated. Such functions should not be defined as members. Why is ListDeptWise() not a member? The reason is that the function under discussion is not the logical part of the object employee. It operates on a bunch of objects. Defining it as a member function will be wrong from the design point of view. Only those functions that describe logical operations from or to the object are to be defined as members (such as reading and printing operations). ListDeptWise() is better defined as a friend in such situations. We need such functions quite frequently,

> Only a function that is a logical part of the object should only be made a member.