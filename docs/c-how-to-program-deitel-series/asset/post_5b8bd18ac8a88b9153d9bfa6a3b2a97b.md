
## Section 9.13 *Using the this Pointer*

- Every object has access to its own address through the this pointer (p. 412).
- An object’s this pointer is not part of the object itself—i.e., the size of the memory occupied by the this pointer is not reflected in the result of a sizeof operation on the object.
- The this pointer is passed as an implicit argument to each non-static member function.
- Objects use the this pointer implicitly (as we’ve done to this point) or explicitly to reference their data members and member functions.
- The this pointer enables cascaded member-function calls (p. 414) in which multiple functions are invoked in the same statement.

## Section 9.14 *static Class Members*

- A static data member (p. 418) represents “class-wide” information (i.e., a property of the class shared by all instances, not a property of a specific object of the class).
- static data members have class scope and can be declared public, private or protected.
- A class’s static members exist even when no objects of that class exist.
- To access a public static class member when no objects of the class exist, simply prefix the class name and the scope resolution operator (::) to the name of the data member.
- The static keyword cannot be applied to a member definition that appears outside the class definition.
- A member function should be declared static (p. 419) if it does not access non-static data members or non-static member functions of the class. Unlike non-static member functions, a static member function does not have a this pointer, because static data members and static member functions exist independently of any objects of a class.

## Self-Review Exercises

- **9.1** Fill in the blanks in each of the following:

  a) Class members are accessed via the ______ operator in conjunction with the name of an object (or reference to an object) of the class or via the ______ operator in conjunction with a pointer to an object of the class.

  b) Class members specified as ______ are accessible only to member functions of the class and friends of the class.

  c) ______ class members are accessible anywhere an object of the class is in scope.

  d) ______ can be used to assign an object of a class to another object of the same class.

  e) A nonmember function must be declared as a(n) ______ of a class to have access to that class’s private data members.

  f) A constant object must be ______; it cannot be modified after it’s created.

  g) A(n) ______ data member represents class-wide information.

  h) An object’s non-static member functions have access to a “self pointer” to the object called the ______ pointer.

  i) Keyword ______ specifies that an object or variable is not modifiable.

  j) If a member initializer is not provided for a member object of a class, the object’s ______ is called.

  k) A member function should be static if it does not access ______ class members.

  l) Member objects are constructed ______ their enclosing class object.

- **9.2** Find the error(s) in each of the following and explain how to correct it (them):

  a) Assume the following prototype is declared in class Time:

  ```cpp
  void ~Time( int );
  ```

  b) Assume the following prototype is declared in class Employee:

  ```cpp
  int Employee(string, string);
  ```

  c) The following is a definition of class Example:

  ```cpp
  class Example
  {
  public:
      Example( int y = 10 )
          : data( y )
      {
          // empty body
      } // end Example constructor

      int getIncrementedData() const
      {
          return ++data;
      } // end function getIncrementedData

      static int getCount()
      {
          cout << "Data is " << data << endl;
          return count;
      } // end function getCount

  private:
      int data;
      static int count;
  }; // end class Example
  ```

## Answers to Self-Review Exercises

**9.1** a) dot (.), arrow (->). b) private. c) public. d) Default memberwise assignment (performed by the assignment operator). e) friend. f) initialized. g) static. h) this. i) const. j) default constructor. k) non-static. l) before.

**9.2**

a) *Error:* Destructors are not allowed to return values (or even specify a return type) or take arguments.

*Correction:* Remove the return type void and the parameter int from the declaration.

b) *Error:* Constructors are not allowed to return values.

*Correction:* Remove the return type int from the declaration.

c) *Error:* The class definition for Example has two errors. The first occurs in function getIncrementedData. The function is declared const, but it modifies the object.

*Correction:* To correct the first error, remove the const keyword from the definition of getIncrementedData. [*Note:* It would also be appropriate to remove this member function as get functions are typically const member functions.]

*Error:* The second error occurs in function getCount. This function is declared static, so it’s not allowed to access any non-static class member (i.e., data).

*Correction:* To correct the second error, remove the output line from the getCount definition.

## Exercises

- **9.3** *(Scope Resolution Operator)* What’s the purpose of the scope resolution operator?

- **9.4** *(Enhancing Class Time)* Provide a constructor that’s capable of using the current time from the time and localtime functions—declared in the C++ Standard Library header `<ctime>`—to initialize an object of the Time class.

- **9.5** *(Complex Class)* Create a class called `Complex` for performing arithmetic with complex numbers. Write a program to test your class. Complex numbers have the form

  `realPart + imaginaryPart * i`

  where *i* is

  `√−1`

  Use `double` variables to represent the private data of the class. Provide a constructor that enables an object of this class to be initialized when it’s declared. The constructor should contain default values in case no initializers are provided. Provide `public` member functions that perform the following tasks:

  a) Adding two `Complex` numbers: The real parts are added together and the imaginary parts are added together.

  b) Subtracting two `Complex` numbers: The real part of the right operand is subtracted from the real part of the left operand, and the imaginary part of the right operand is subtracted from the imaginary part of the left operand.

  c) Printing `Complex` numbers in the form (a, b), where a is the real part and b is the imaginary part.

- **9.6** *(Rational Class)* Create a class called `Rational` for performing arithmetic with fractions. Write a program to test your class. Use integer variables to represent the private data of the class—the numerator and the denominator. Provide a constructor that enables an object of this class to be initialized when it’s declared. The constructor should contain default values in case no initializers are provided and should store the fraction in reduced form. For example, the fraction

  $\frac{2}{4}$

  would be stored in the object as 1 in the numerator and 2 in the denominator. Provide `public` member functions that perform each of the following tasks:

  a) Adding two `Rational` numbers. The result should be stored in reduced form.

  b) Subtracting two `Rational` numbers. The result should be stored in reduced form.

  c) Multiplying two `Rational` numbers. The result should be stored in reduced form.

  d) Dividing two `Rational` numbers. The result should be stored in reduced form.

  e) Printing `Rational` numbers in the form a/b, where a is the numerator and b is the denominator.

  f) Printing `Rational` numbers in floating-point format.

- **9.7** *(Enhancing Class Time)* Modify the `Time` class of Figs. 9.4–9.5 to include a `tick` member function that increments the time stored in a `Time` object by one second. Write a program that tests the `tick` member function in a loop that prints the time in standard format during each iteration of the loop to illustrate that the `tick` member function works correctly. Be sure to test the following cases:

  a) Incrementing into the next minute.

  b) Incrementing into the next hour.

  c) Incrementing into the next day (i.e., 11:59:59 PM to 12:00:00 AM).

- **9.8** *(Enhancing Class Date)* Modify the `Date` class of Figs. 9.13–9.14 to perform error checking on the initializer values for data members `month`, `day`, and `year`. Also, provide a member function `nextDay` to increment the day by one. Write a program that tests function `nextDay` in a loop that prints the date during each iteration to illustrate that `nextDay` works correctly. Be sure to test the following cases:

  a) Incrementing into the next month.

  b) Incrementing into the next year.
