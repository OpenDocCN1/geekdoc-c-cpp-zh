```
} return n*fact(n-1); //call by itself.
}
```

# Output

Enter an integer
5
Factorial of 5 is:120

In Program 2.40, the operation of the recursive fact() is somewhat complex, when fact() is called with an argument as 1 the function returns 1, otherwise it returns the value of n*fact(n-1). If value is 5, fact is called for the first time with 5 as an argument and second time it is called with an argument of 4 and third time with an argument 3 and so on until n is equal to 1. Each call of fact() stores the value of n while calling itself with another value of n.

When a function calls itself, a new set of local variables and arguments is allocated, and the function code executes with these variables. A recursive call does not create a new copy of function but a new a copy of values being operated are created. Every recursive function must be ended, otherwise it will call itself forever. The statement if(n==1) in the program does this, when the n value becomes 1 the program terminates.

The main advantage of the recursive function is that they can be used to implement several algorithms in the simplest way. The implementation of the quick sort is difficult using the iteration way. Thus, some may think that recursion is easier to iteration.

# SUMMARY

+   - Robustness, adaptability and reusability are goals of an object-oriented design.
+   - Abstraction, encapsulation and modularity are principles of an object-oriented design.
+   - Constructors are used for initializing objects. Destructors are used to destroy objects.
+   - Default constructors, parameterized constructors and copy constructors are the types of constructors.
+   - Constructor overloading is a technique of defining more than one constructor with the same name.
+   - Operator overloading changes the meaning of the predefined operators.
+   - Inheritance derives a new class from the already existing class. Access to base class members is controlled through public, private and protected access specifiers.
+   - The derived class will have the members of the base class based on the declaration type such as private, public or protected and the access specifier at the time of inheriting the base class.
+   - Single inheritance and multiple inheritance are the basic classifications of inheritance.
+   - Inheritance can be further divided into various types: hierarchical inheritance, single-level inheritance, multi-level inheritance, hybrid inheritance and multipath inheritance.
+   - When the access specifier of the base class is public, all the public members of the base class are accessible to the derived class.
+   - When the access specifier of the base class is private, then all the public, protected members of the base class become private members of the derived class.
+   - All the public and protected members of the base class become protected members of the derived class when the access specifier of the base class is protected. All the private members of the base class are not accessible by the derived class.
+   - Delegation is a mechanism in which the object of one class is used as a member of another class.
+   - Polymorphism defines one interface with many forms.