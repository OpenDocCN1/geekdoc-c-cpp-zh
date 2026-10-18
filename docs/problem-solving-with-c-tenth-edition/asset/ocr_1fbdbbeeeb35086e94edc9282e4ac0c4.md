and call a function member through the pointer, discuss what determines which function is actually called—the base class member function or the derived-class function.

# CHAPTER SUMMARY

+   - Inheritance provides a tool for code reuse by deriving one class from another and by adding features to the derived class.
+   - Derived class objects inherit all the members of the base class and may add members.
+   - Late binding means that the decision of which version of a member function is appropriate is decided at run-time. Virtual functions are what C++ uses to achieve late binding. Polymorphism, late binding, and virtual functions are really all the same topic.
+   - A *protected* member in the base class is directly available to a publicly derived class’s member functions.

# Answers to Self-Test Exercises

+   1. Yes. You can plug in an object of a derived class for a parameter of the base class type. An HourlyEmployee is an Employee. A SalariedEmployee is an Employee.
+   
+   2.
+   ```cpp
+   class SmartBut : public Smart
+   {
+   public:
+       SmartBut();
+       SmartBut(int newA, int newB, bool newCrazy);
+       bool isCrazy() const;
+   private:
+       bool crazy;
+   };
+   ```
+   
+   3. It is legal because a and b are marked *protected* in the base class Smart and so they can be accessed by name in a derived class. If a and b had instead been marked *private*, then this would be illegal.
+   
+   4. The declaration for the function getName is not given in the definition of SalariedEmployee because it is not redefined in the class SalariedEmployee. It is inherited unchanged from the base class Employee.
+   
+   5.
+   ```cpp
+   #include <iostream>
+   #include "salariedemployee.h"
+   using namespace std;
+   namespace employeessavitch
+   ```