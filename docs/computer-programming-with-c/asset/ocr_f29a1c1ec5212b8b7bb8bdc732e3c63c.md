```
```cpp
/*pointer p and q point to dynamically allocated objects of
        Employee*/
p= new Employee;
q= new Employee;
/*Input the members of the Employee object pointed by the pointer
        p*/
cout<<"Enter the value of id , name and salary for object pointed
        by p"<<endl;
p->input();
/*Input the members of the Employee object pointed by the pointer
        q*/
cout<<"Enter the value of id , name and salary for object pointed
        by q"<<endl;
q->input();
/*Print the members of the Employee object pointed by the pointers
        p and q*/
cout<<"Employee Details are:"<<endl;
p->output();
q->output();
}
```
```

# **Output**

```
Enter the value of id, name and salary for object pointed by p
10 John 5000
Enter the value of id, name and salary for object pointed by q
20 Jack 3000
Employee Details are:
10   John   5000
20   Jack   3000
```

# 11.21  Linked List to Maintain Data about Employees

We have implemented linked list that can store integer data in Chapter 10, using dynamic memory allocation of structure objects. We have also specified the advantages of linked list over arrays in Chapter 10. Now that we understand dynamic memory allocation for class objects, we will upgrade our code in Section 11.12 that creates array of Employee objects by creating a linked list that can store data about employees instead of creating an array of objects. The full source code to store employee data by creating a linked list is given with following functions in class Node:

```
void insert(Employee x)
```

This function is used to insert the Employee object x into the linked list.

```
void traverse()
```