
![](img/57c0d966bb33c67a5a188e6bf39e4e02_807_0.png)

Professor. The class AssistantProf also defines an additional member courseEnd which is of type Date. This member could represent the end date of the postgraduation course, which is currently pursued by the assistant Professor.

### 14.4.5 Hybrid inheritance

Combining different inheritance types into a single design is called as hybrid inheritance. The hierarchy in Figure 14.32 is the mixture of multi-level inheritance, multiple inheritance and hierarchical inheritance; this complete example when viewed together illustrates hybrid inheritance as shown in the Figure 14.32. The pattern represents that a Person can either be a Student or a Professor. And a Person who is both Student as well as Professor is called as an AssistantProf.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_807_1.png)

### How can I determine if two classes are to be related using Inheritance?

![](img/57c0d966bb33c67a5a188e6bf39e4e02_808_0.png)

Inheritance should be created whenever there is “IS-A” type of relationship between classes. As an example, let's say we are required to store data about two different types of accounts offered by a Bank:

- 1. Saving account
- 2. Current account

We can identify common attributes required by both the accounts and put it in a generic class named as Account. We can then apply IS-A relationship and define Saving and Current as two child classes of class Account. The parent class Account may define common members like accountId (Account identifier), customerName (name of the customer holding the account), balance (balance funds in the account) etc. because these attributes will be required in both the child classes. These are generic attributes because this information must be stored irrespective of the type of account.

While it is understood that treating inheritance makes sense only when there are common attributes required in multiple child classes, it is equally important to understand that different child classes must be created only if there is at least one attribute difference among each of the child classes. When we create two different classes Saving and Current to represent two different types of accounts, it is indeed very important that there exists some difference in between the two accounts. For instance, saving account pays interest on the balance money which current account does not; whereas current account imposes a rule to its customers to maintain a minimum balance of x dollars which saving account does not. Hence, clearly there is an attribute difference between the two classes, class Saving has a specialized member interest not present in class Current, whereas class Current has a specialized member minimum balance (to represent minimum balance required in account) which is not present in class Saving. Hence it makes complete sense to create two different child classes Saving and Current defining specialized members with a common parent class Account defining generalized members.

If there had been no difference between saving and current accounts, it would not have been possible to identify an attribute which is present in one class but not the other. In fact, if both the accounts are exactly the same, there would have been no need to create these child classes at all. We could have dumped all the attributes in class Account itself. In summary, creating inheritance makes sense only when:

- 1. There are some common attributes in multiple child classes (which can be declared in a generalized parent class)
- 2. There is at least one attribute difference among the child classes (per class). These specialized attributes specific to a child must be defined by the respective child class.

## 14.5 IS-A and HAS-A Relationship: An Example

To understand IS-A and HAS-A relationship between classes, let us create a C++ program to implement the hierarchy, which is defined in Figure 14.27. The hierarchy depicts that there are two types of Person objects, a Person can either be a Student or a Professor. There are some members such as name, gender, and date of birth, which are relevant for both Student as well as Professor, hence we define these members in a parent class Person and create Student and Professor as child classes of Person. This way we avoid duplication of code because the members defined in parent class will be inherited by each of the child classes. The members name, gender and date of birth will be available in the object memory of Student as well as Professor without a need to individually define them in these classes because they are defined at the parent level.

The child class Student defines only those members which are specific to a Student object such as roll_no and Marks. These members are not relevant to Professor and hence there is no point defining them at the parent level. Similarly, class Professor defines specialized members such as salary and prof_id which are not relevant to Student. The real world scenario for this is that every student has a roll number and obtains some marks in the examination he appears for. Whereas every professor has an identification number and gets a monthly salary for his work.

> **NOTES**
>
> **Inheritance** should be implemented between classes whenever there exists **IS-A** relationship in real world. For example, in this case, we could say **Student IS-A Person** or **Professor IS-A Person**. Hence inheritance is also called as **IS-A** relationship between classes.

Note that one of the members of class Person is used to represent 'date of birth' (dob) which in itself is a **composite attribute**. To store date of birth, we actually need to store three different members dd (day), mm (month), and yy (year). Hence, we create another class named as **Date** which contains the members dd, mm, and yy as shown in Figure 14.33. This concept is very similar as described in Chapter 9 where we have created a structure named as Date. In this case, we have created a **class Date** instead of a structure to encourage encapsulation and data hiding. Every object of class Date will represent one date in the real world. Every Person may it be a Student or a Professor has a date of birth, and hence we create an object of class Date in class Person to store the date of birth of any Person. So when you create an object of class Person or Student or Professor, it will have an object of class Date embedded in it. Such a relationship between classes is called as **composition**. By definition, when an object of one class is required to be part of the object memory of another class such that if the **whole part** is destroyed, then the **subpart** also gets destroyed, it is called composition between classes. For example, Figure 14.34 shows one object of class Student in memory. This object has an object of class Date embedded in it. For some reason, if a **Student** object goes out of scope (or gets destroyed), the **Date** object that is contained in it will also be destroyed, hence we say that there is a composition established between Student and Date classes.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_809_0.png)

**Figure 14.33:** IS-A and HAS-A relationship

Note that, this composition is established indirectly due to inheritance (in actuality, class Person contains an object of Date which is inherited by Student).

> **NOTES**
>
> **Composition** should be implemented between classes whenever there exists **HAS-A** relationship in real world. For example, in this case, we could say Person **HAS-A** date of birth OR Student **HAS-A** date of birth OR Professor **HAS-A** date of birth. Hence composition is also called as **HAS-A** relationship between classes.

The following is the full source code to implement the relationships between classes as shown in Figure 14.33.

```cpp
#include<iostream.h>
#include <Windows.h>
#include <stdio.h>
class Date
{
private:
    int dd;
    int mm;
    int yy;
public:
    void inputDate()
    {
        cout<<"Enter dd:"<<endl;
        cin>>dd;
        cout<<"Enter mm:"<<endl;
        cin>>mm;
        cout<<"Enter yyyy:"<<endl;
        cin>>yy;
    }
    void outputDate()
    {
        cout<<"dd:"<<dd<<"-"<<mm<<"-"<<yy<<endl;
    }
    void outputAge()
    {
        cout<<yy<<"years and "<<mm<<" months and "<<dd<<" days"<<endl;
    }
    static Date getCurrentDate()
    {
        SYSTEMTIME system;
        GetSystemTime(&system);
        Date today;
```
