# Listing 8.33 Assigning a derived class object to a base class object and vice versa

```
A A1;
B B1;
A1=B1; //OK
B1=A1; //ERROR!
```

The set of data members of the derived class is, or is reckoned to be, a proper superset of the set of data members of its base class. Thus, in this mind, in Listing 8.33, 'B1' will have its own copies of not only data members that 'A1' but also some extra members of its own. If the second assignment in Listing 8.33 works, then the data members of 'B1' that are common in name with those of 'A1' will get initialized. However, the data members that are exclusively in 'B1' will remain unchanged and may no longer match with the rest of the data members of 'B1'. Keeping this in mind, the compiler prevents the second assignment.

However, the class designer, if/she so desires, may provide an assignment operator function to the derived class so that a base class object can be assigned to a derived class object. Listing 8.34

# Listing 8.34 Enabling a base class object to be assigned to a derived class object

```
/*Beginning of B.h*/
#include="A.h"
class B : public A {
public:
B& operator=(const A&); //to enable B1=A1;
/*
rest of the class B
*/
};
/*End of B.h*/
```

Statements to modify the values of the data members that are exclusive to the derived class can be provided in Listing 8.34.
npose there is no explicitly defined assignment operator-overloading function for the derived class that has a reference to the derived class object as a formal argument. Further, suppose there is an explicitly assignment operator-overloading function for the derived class that has a reference to the base class object as a formal argument. Even then the compiler would generate an assignment operator that has a reference to the derived class object as a formal argument. For suppressing the generation of the implicit default assignment, the formal argument of the explicit operator must be of the same type as the class itself.

# 8.2.6 Overloading Insertion and Extraction Operators

The syntax for overloading the insertion operator is given in Listing 8.35.

# Listing 8.35 Syntax for overloading the insertion operator

```
class A
{
```