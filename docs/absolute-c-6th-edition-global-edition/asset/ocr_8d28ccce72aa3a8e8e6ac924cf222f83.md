# Chapter Summary

+   - A pointer is a memory address, so a pointer provides a way to indirectly name a variable by naming the address of the variable in the computer's memory.
+   - Dynamic variables (also called dynamically allocated variables) are variables that are created (and destroyed) while a program is running.
+   - NULL is a constant that is used to represent an empty pointer and is the number 0. nullptr is a newer constant introduced in C++11 to represent an empty pointer. nullptr is distinct from the number 0.
+   - Memory for dynamic variables is in a special portion of the computer's memory called the freestore manager. When a program is finished with a dynamic variable, the memory used by the dynamic variable can be returned to the freestore manager for reuse; this is done with a delete statement.
+   - A dynamically allocated array (also called simply a dynamic array) is an array whose size is determined when the program is running. A dynamic array is implemented as a dynamic variable of an array type.
+   - A destructor is a special kind of member function for a class. A destructor is called automatically when an object of the class passes out of scope. The main reason for destructors is to return memory to the freestore manager so the memory can be reused.
+   - A copy constructor is a constructor that has a single argument that is of the same type as the class. If you define a copy constructor, it will be called automatically whenever a function returns a value of the class type and whenever an argument is plugged in for a call-by-value parameter of the class type. Any class that uses pointers and the operator new should have a copy constructor.
+   - When overloading the assignment operator, it must be overloaded as a member operator. Be sure to check that your overloading works when the same variable is on both sides of the overloaded assignment operator.

# Answers to Self-Test Exercises

+   1. A pointer is the memory address of a variable.
+   2. int *p; // This declares a pointer to an int variable.
+      *p = 17; //Here, * is the dereferencing operator. This assigns //17 to the memory location pointed to by p.
+      void func(int* p); // Declares p to be a pointer value // parameter.
+   3. 10 20
+      20 20
+      30 30
+      If you replace *p1 = 30; with *p2 = 30;, the output would be the same.