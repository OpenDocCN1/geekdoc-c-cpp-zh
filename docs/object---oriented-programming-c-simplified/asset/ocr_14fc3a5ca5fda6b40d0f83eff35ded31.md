EXPLANATION : For student's internal marks we have a class Internal and for student's external marks we have a class External. The internal marks must be between 0 to 60 and external marks must be between 0 to 40. These two classes are inherited by class total which finds the total marks and display all three marks :

+   (a) Internal
+   (b) External and
+   (c) Total

Note here that i_marks and e_marks are protected so that can be used inside the total class. They can be modified by the class total. So ideally i_marks and e_marks. Try to make use of this and create a new program yourself.

# → Resolving Ambiguity

In multiple inheritance when two base classes having same name for their functions and data, ambiguity arises when they are used in the derived class. For example, consider the two classes A and B having same function signature for function named show like void show (). Both the classes are inherited in the third class C. Now how class C can use show of A class and show of B class individually. Simply accessing show function in class C creates confusion as to which show we want to refer; show of class A or show of class B. In these situations we can use the scope resolution operator with class names to functions for accessing the function of individual class. Thus inside the member functions of class C we can access show of class A as A :: show() and show of class B as B :: show. If function show is also defined in the class C and all show are public then they can access in the main using an object of C class as :

+   C o1;
+   O1.A ::show( );      //calls show of A class
+   O1.B ::show( );      //calls show of B class
+   O1.show( );          // calls show of C class

See the example given below :

```
/*PROG 9.24 RESOLVING AMBIGUITY IN MULTIPLE INHERITANCE */

#include <iostream.h>
#include <conio.h>
class A
{
protected :
    int num;
public :
    void show()
    {
        cout<<"show of A\n";
        cout<<"num of A="<<num<<endl;
    }
};
```