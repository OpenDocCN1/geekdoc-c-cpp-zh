
local variable parameter, so parameter.a is set equal to sample.a. But these are pointer variables, so during the function call parameter.a and sample.a point to the same dynamic array, as follows:

![](img/c76bba8c1d927f399768ffe2ab5f5bee_496_0.png)

When the function call ends, the destructor for PFArrayD is called to return the memory used by parameter to the freestore manager so it can be reused. The definition of the destructor contains the following statement:

```
delete [] a;
```

Since the destructor is called with the object parameter, this statement is equivalent to

```
delete [] parameter.a;
```

which changes the picture to the following:

![](img/c76bba8c1d927f399768ffe2ab5f5bee_496_1.png)

Since sample.a and parameter.a point to the same dynamic array, deleting parameter.a is the same as deleting sample.a. Thus, sample.a is undefined when the program reaches the statement

```
cout << "After call: " << sample[0] << endl;
```

so this cout statement is undefined. The cout statement may by chance give you the output you want, but sooner or later the fact that sample.a is undefined will produce problems. One major problem occurs when the object sample is a local variable in some function. In this case the destructor will be called with sample when the function call ends. That destructor call will be equivalent to

```
delete [] sample.a;
```

But, as we just saw, the dynamic array pointed to by sample.a has already been deleted once, and now the system is trying to delete it a second time. Calling delete twice to delete the same dynamic array (or any other variable created with new) can produce a serious system error that can cause your program to crash.

That was what would happen if there were no copy constructor. Fortunately, we included a copy constructor in our definition of the class PFArrayD, so the copy constructor is called automatically when the following function call is executed:

```
showPFArrayD(sample);
```

The copy constructor defines what it means to plug in the argument sample for the call-by-value parameter named parameter, so that now the picture is as follows:

![](img/c76bba8c1d927f399768ffe2ab5f5bee_497_0.png)

Thus, any change that is made to parameter.a has no effect on the argument sample, and there are no problems with the destructor. If the destructor is called for parameter and then called for sample, each call to the destructor deletes a different dynamic array.

returned value

When a function returns a value of a class type, the copy constructor is called automatically to copy the value specified by the return statement. If there is no copy constructor, problems similar to what we described for call-by-value parameters will occur.

when you need a copy constructor

If a class definition involves pointers and dynamically allocated memory using the new operator, you need to include a copy constructor. Classes that do not involve pointers or dynamically allocated memory do not need to define a copy constructor.

assignment statements

Contrary to what you might expect, the copy constructor is not called when you set one object equal to another using the assignment operator.6 However, if you do not like what the default assignment operator does, you can redefine the assignment operator as we have done in Displays 10.10 and 10.11.

## Copy Constructor

A copy constructor is a constructor that has one call-by-reference parameter that is of the same type as the class. The one parameter must be a call-by-reference parameter; normally, the parameter is also a constant parameter—that is, it is preceded by the const parameter modifier. The copy constructor for a class is called automatically whenever a function returns a value of the class type. The copy constructor is also called automatically whenever an argument is plugged in for a call-by-value parameter of the class type. A copy constructor can also be used in the same ways as other constructors.

Any class that uses pointers and the new operator should have a copy constructor.

## The Big Three

The copy constructor, the = assignment operator, and the destructor are called the big three because experts say that if you need any of them, you need all three. If any of these is missing, the compiler will create it, but the created item might not behave as you want. Thus, it pays to define them yourself. The copy constructor and overloaded = assignment operator that the compiler generates for you will work fine if all member variables are of predefined types such as int and double. For any class that uses pointers and the new operator, it is safest to define your own copy constructor, overloaded =, and a destructor.

## Self-Test Exercises

13. If a class is named MyClass and it has a constructor, what is the constructor named? If MyClass has a destructor what is the destructor named?

14. Suppose you change the definition of the destructor in Display 10.11 to the following. How would the sample dialogue in Display 10.12 change?

```
PFArrayD::~PFArrayD()
{
    cout << "\nGood-bye cruel world! The short life of\n" << "this dynamic array is about to end.\n";
    delete [] a;
}
```

15. The following is the first line of the copy constructor definition for the class PFArrayD. The identifier PFArrayD occurs three times and means something slightly different each time. What does it mean in each of the three cases?

```
PFArrayD::PFArrayD(const PFArrayD& pfaObject)
```

16. Answer these questions about destructors.

- a. What is a destructor and what must the name of a destructor be?
- b. When is a destructor called?
- c. What does a destructor actually do?
- d. What should a destructor do?

17. a. Explain carefully why no overloaded assignment operator is needed when the only data consists of built-in types.
b. Same as part a for a copy constructor.
c. Same as part a for a destructor.

## Chapter Summary

- A pointer is a memory address, so a pointer provides a way to indirectly name a variable by naming the address of the variable in the computer's memory.
- Dynamic variables (also called dynamically allocated variables) are variables that are created (and destroyed) while a program is running.
- NULL is a constant that is used to represent an empty pointer and is the number 0. nullptr is a newer constant introduced in C++11 to represent an empty pointer. nullptr is distinct from the number 0.
- Memory for dynamic variables is in a special portion of the computer's memory called the freestore manager. When a program is finished with a dynamic variable, the memory used by the dynamic variable can be returned to the freestore manager for reuse; this is done with a delete statement.
- A dynamically allocated array (also called simply a dynamic array) is an array whose size is determined when the program is running. A dynamic array is implemented as a dynamic variable of an array type.
- A destructor is a special kind of member function for a class. A destructor is called automatically when an object of the class passes out of scope. The main reason for destructors is to return memory to the freestore manager so the memory can be reused.
- A copy constructor is a constructor that has a single argument that is of the same type as the class. If you define a copy constructor, it will be called automatically whenever a function returns a value of the class type and whenever an argument is plugged in for a call-by-value parameter of the class type. Any class that uses pointers and the operator new should have a copy constructor.
- When overloading the assignment operator, it must be overloaded as a member operator. Be sure to check that your overloading works when the same variable is on both sides of the overloaded assignment operator.

## Answers to Self-Test Exercises

- 1. A pointer is the memory address of a variable.
- 2. int *p; // This declares a pointer to an int variable.
  *p = 17; //Here, * is the dereferencing operator. This assigns //17 to the memory location pointed to by p.
  void func(int* p); // Declares p to be a pointer value // parameter.
- 3. 10 20
  20 20
  30 30
  If you replace *p1 = 30; with *p2 = 30;, the output would be the same.
