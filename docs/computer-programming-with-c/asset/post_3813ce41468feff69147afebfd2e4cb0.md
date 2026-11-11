
## Chapter 14 | Inheritance

### 14.1 Overview

Inheritance is a relationship between classes wherein one class is derived from another class. The derived class is called child class, and the class from which it is derived is called parent class. Inheritance is also called as parent–child relationship between classes such that child class gives a specialized implementation of parent class. **Reusability** of the code is the key principle of inheritance because the properties defined in the parent class are borrowed by the child class. Inheritance is one of the most important features of object oriented programming, wherein the classes are organized in a **hierarchical** form. The class at the top of hierarchy is called **parent class**, whereas the class at the bottom of the hierarchy is called **child class**. Advantage of inheritance is that the **members** (variables and functions) defined by the parent class are also made available into the child class. This saves the programmers’ efforts to redevelop logic in child class, which is already implemented in parent class. Along with the properties defined in parent class, the child class can also have additional properties of its own as shown in Figure 14.1. Hence the parent class is also called **Base class/Super class/Generalized class** and the child class is also called **Derived class/Sub class/Specialized class**.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_786_0.png)

**Figure 14.1:** Principle of inheritance

As seen from Figure 14.1, the member1 and member2 are defined in the parent class, which are available by default, in the child class. Also, child class can define additional members such as member3 and member4. This means that if you create an object of parent class, it will contain only two members: member1 and member2; whereas, if you create an object of child class, it will contain four members: member1, member2, member3, and member4. Therefore, a parent class should define the common properties that are required by all the child classes, whereas each of child class should define the specialized properties applicable only for that child.

As an example, let’s assume that we need to store data about students and professors in a particular institute in computer memory. The requirement is that for every person (a student or a professor) we need to store name, date of birth, and gender. The only attribute difference is that professor has two additional attributes salary and prof_id which student does not, and student has additional attributes marks and roll_no, which professor does not. This means that for every student object, we need to store following information in computer memory:

- 1. Name
- 2. Date of Birth (dob)
- 3. Gender
- 4. Roll Number (roll_no)
- 5. Marks

Also, for every Professor object, we plan to store following information in computer memory:

- 1. Name
- 2. Date of Birth
- 3. Gender
- 4. Professor Identifier (prof_id)
- 5. Salary

Figure 14.2 shows the attributes of classes Student and Professor with the attribute differences highlighted in boldface.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_787_0.png)

Having members name, dob, and gender is a common requirement of Student and Professor classes. Instead of duplicating this code in both the classes, we can create a common parent class named as Person which defines the common members. We then create Student and Professor as child classes of class Person as shown in Figure 14.3.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_787_1.png)

As we have created a relationship of inheritance, all the child classes will by default borrow the members defined in the parent class. This means that we need not create the members name, gender, and dob separately in Student and Professor because they will be inherited from the parent class Person. The child classes Student and Professor should only define the specialized members required by them. This means that the only members to be defined in class Student are roll_no and marks, whereas those in class Professor should be prof_id and salary as shown in Figure 14.3. The notation of inheritance is an arrow head drawn from each child which points to the parent class as seen in Figure 14.3.

Similar to member variables, common member functions can also be defined at a parent level, thereby avoiding duplication of the code in each of the child classes.

> **Why is the notation of inheritance such that the arrow head points towards the parent class?**
>
> The arrow drawn from the child class indicates that we can access the members and member functions of the parent class using the object of child class. Note that, the direction of inheritance is always from ‘parent’ to ‘child’, however the arrow head represents the direction of ‘allowed access’ and hence the arrow head is from child to parent. This is a UML notation of inheritance. UML stands for Unified Modeling Language which is used for object-oriented analysis and design.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_789_0.png)

```cpp
class A
{
..........
..........
};
```

```cpp
class B : private A
{
..........
..........
};
```

**Figure 14.5:** Creating private inheritance

![](img/57c0d966bb33c67a5a188e6bf39e4e02_789_1.png)

**Figure 14.6:** Private inheritance

![](img/57c0d966bb33c67a5a188e6bf39e4e02_789_2.png)

```cpp
class A
{
..........
..........
};
```

```cpp
class B : protected A
{
..........
..........
};
```

**Figure 14.7:** Creating protected inheritance

In case of protected inheritance, the public/protected members of parent class A will be inherited as protected members in child class B. This means that if any member is defined as public or protected in a parent class A, then it will be inherited as a protected member in the child class B as shown in Figure 14.8. Again, the private members of the parent class A can never be accessed inside the child class B, although they are inherited and physically present in the object of B.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_790_0.png)

**Figure 14.8:** Protected inheritance

When the `<accessType>` is specified as public while creating the child class B, the inheritance is then called 'public inheritance' as shown in Figure 14.9.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_790_1.png)

**Figure 14.9:** Creating public inheritance

In case of public inheritance, the public members of parent class A will be inherited as public members in child class B. The protected members of parent class A will be inherited as protected members in child class B. As with other types of inheritance, the private members of the parent class A can never be accessed inside the child class B. Concept of public inheritance is shown in Figure 14.10.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_791_0.png)

> **How do I make a choice between private, public and protected inheritance?**
>
> Selecting between private, public or protected inheritance depends upon the requirements of data hiding to be implemented in the child class. It is recommended to use public inheritance since it preserves the access rules defined by the parent even in the child class. The choice to select appropriate access level for inheritance is still left to the programmer.

In this book, we will write all the inheritance programs using ‘public inheritance’ because it gives us maximum degree of reusability.

### 14.3 Access Specifiers in C++: Revisited

C++ supports the following three types of access specifiers:

#### Private access

A private member or a member function can only be accessed inside a class in which the member is defined. This means that when a member variable is defined as private, its value cannot be accessed from outside of the class; and when a member function is defined as private it cannot be invoked from any place outside of the class.

#### Public access

The public members/member functions of a class can be accessed from inside as well as outside the class. Hence, the public members can be accessed from any place in the C++ program.

#### Protected access

Protected members and member functions of a class can be accessed inside the class in which they are defined as well as in all the child classes of that class. The protected
