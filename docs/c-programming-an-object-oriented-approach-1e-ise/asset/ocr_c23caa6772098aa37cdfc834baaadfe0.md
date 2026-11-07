In Figure 11.9, the scope of the two classes shows that every name defined in the base class is also visible in the derived class, but the reverse is not true. This concept parallels block scope within a function.

How can the system distinguish which function we are calling? We must remember that we do not call member functions in a class just by name; we let the instance call the appropriate function. In other words, if person and student are two objects of the Person and Student classes, respectively, we use the following two statements:

| Using Person object | Using Student object |
|---|---|
| `person.set(11111111);`<br>`person.get();` | `student.set(3.7);`<br>`student.get();` |

Scope tells us how a compiler invokes a function based on the following rules:

+   a. The compiler tries to find a matching function (using names and parameters) that belongs to the class of the object that has invoked the function.
+   
+   b. If no matching function is found, the compiler looks at the functions inherited from the superclass.
+   
+   c. If no match is found, the search continues until the base class is reached.
+   
+   d. If no match is found in any class, a compilation error is issued.

# Delegation Of Duty

An overloaded or overridden member function in a derived class can delegate part of its operation to a member function in a class in a higher level by calling the corresponding member function. This is easily done with void member functions; it is more complicated with value-returning functions because two values must be returned, which requires a struct or a class object. We concentrate on the void member function in this case.

For example, the set member function in the Student class can be designed to set the data members of the Person class, identity, and the data member of its own class, gpa. However, as we said, the identity data member is hidden in the Student class and cannot be accessed by the set function in the Student class, but the set function in the Student class can call the set function of the Person class. In the same way, we can design a print function in the Person class that prints only the value of the identity data member. We can also design a print function in the Student class to call the print function in the Person class to do parts of its job. The following shows the definition of set function and print function with delegation.

| Using Person object | Using Student object |
|---|---|
| ```cpp
void Person :: set (long id)
{
    identity = id;
}

void Person :: print ()
{
    cout << name;
}
``` | ```cpp
void Student :: set (long id, double gp)
{
    Person :: set (id);  // Delegation
    gpa = gp;
}

void Student :: print ()
{
    Person :: print();  // Delegation
    cout << gpa;
}
``` |