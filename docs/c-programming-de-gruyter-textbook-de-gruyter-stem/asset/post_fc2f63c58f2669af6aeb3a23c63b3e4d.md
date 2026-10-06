
## 7.6.4 Execution Result and Analysis

The result of the program is as follows.

```
The Line equation is: //equations
0.2368 0.2471 0.2568 1.2671 1.8471
0.1968 0.2071 1.2168 0.2271 1.7471
0.1581 1.1675 0.1768 0.1871 1.6471
1.1161 0.1254 0.1397 0.149 1.5471
The Result is: //solution
X[0]=1.04058
X[1]=0.987051
X[2]=0.93504
X[3]=0.881282
```

The equations that this example uses come from the book *C Programs of Common Algorithms* written by Mr Xu Shiliang. The calculation result here is exactly the same as in the book. The following equations are:

```
0.2368x0 + 0.2471x1 + 0.2568x2 + 1.2671x3 = 1.8471
0.1968x0 + 0.2071x1 + 1.2168x2 + 0.2271x3 = 1.7471
0.1581x0 + 1.1675x1 + 0.1768x2 + 0.1871x3 = 1.6471
1.1161x0 + 0.1254x1 + 0.1397x2 + 0.1490x3 = 1.5471 (7.8)
```

The matrix is stored in a one-dimensional array through dynamic memory allocation.

This is an example of solving practical problems through the derivation hierarchy of classes. The base class deals with the matrix. The publicly derived class Lineq is designed to deal with linear equations. In addition to the members inherited from the base class, new members are added to class Lineq according to actual needs. In this way, we detail and specialize the base class Matrix to describe and solve the problem more efficiently.

The access control is also designed according to actual needs. The matrix stored and maintained by the data members of the base class, which is the coefficient matrix in derived class, must take advantage of protected members, setting the access attributes of the base-class members to be protected. Thus the protected members inherited from the base class can be accessed in the publicly derived class Lineq, however are inaccessible by other modules outside the class. In this way, we find an appropriate balance between data sharing and data hiding.

New constructors and destructors should be added to the derived class to do the initialization and cleaning up within the derived class because the constructor and destructor of the base class cannot be inherited. The constructor of the derived class initializes the data inherited from the base class by calling the constructor of the base class. In this example, the constructor of the derived class Lineq calls the constructor of the base class Matrix and passes on the initialization arguments. The destructor of the derived class also calls the destructor of the base class to the cleaning up work.

## 7.7 Program Example: Personnel Information Management Program

In this section, we will take the personnel information management of a small corpora-as an example to further illustrate the procedure of derivation and the applications of virtual functions and base classes.

### 7.7.1 Problem Description

In Section 7.1.1, we analyzed the problem of the personnel information management system that had been discussed in Chapters 4.6. In Section 7.1.3 we proposed an improvement of the program. Here, we implement the salary calculating function mentioned in Section 7.1.1 using class inheritance and derivation. For example, we assume the salary calculating method to be: a manager's salary is 8,000 RMB; a part-time technician gets his salary by the hour and the hourly pay is 100 RMB; a part-time salesman's salary includes commissions, which are 4% of his sales; a sales manager takes his fixed salary of 5,000 RMB and sales commissions, which are 5% of his department's sales in a current month.

### 7.7.2 Class Design

According to the above needs, we design a base class employee, from which we derive the classes technician (part-time technician), manager (manager), and salesman (salesman). Because a sales manager is both a manager and a salesman, we design the class salesman derived from both class manager and salesman for this group of people.

In the base class employee, aside from the constructor and destructor, the operations on information on all kinds of people could be defined uniformly, to regulate the basic behaviors in all the derived classes of the class. Since the salary calculation methods for different kinds of people, they cannot be defined uniformly in the base class employee. Therefore, we can set the function body of salary calculating in the base class as empty, and implement specific functionalities in the homonymous functions in different derived classes according to the hiding rule. The class design is shown in Figure 7.10.

Since the two base classes of the class salesman have a common base class employee, we design the class employee as virtual to avoid ambiguity.
