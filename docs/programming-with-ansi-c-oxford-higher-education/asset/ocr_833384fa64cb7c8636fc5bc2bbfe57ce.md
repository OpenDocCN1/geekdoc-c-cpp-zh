7. How can we define a function or a class in a namespace and use it outside?

8. How can we extend a namespace already defined? What is its advantage?

9. What is unnamed namespace? What is the use of unnamed namespace?

10. How can we define one namespace inside another? How can we use the objects defined in the inner namespace outside the outer namespace?

11. What are namespace aliases? What is their use?

12. What is std namespace? How is it different from other namespaces?

13. What is Koenig lookup? When is it applied?

# Practical Exercises

1. Write a program to define a namespace and define an employee class inside that. (Use any definition of employee class encountered so far). Define at least two member functions outside the namespace. Write a main() program and use the employee class objects there.

2. Get the definition of a student class from any of the previous chapters. Define the class in a namespace and define an employee class inside that. (Use any definition of employee class encountered so far). Define at least two member functions outside the namespace. Write a main() program and use the employee class objects there.

namespace Student. Define a function abs() in the class to indicate absence. Also use the function in the main program with abs() from the math library.

3. Get the definition of Time class from Chapter 6. Define a function DifferenceTime() as its member. Define the Time class inside the namespace. Define DifferenceTime() outside the namespace and use namespace alias to access that function in main().

4. Get the definition of a student class from any of the earlier chapters. Define a NewStudent class with a new data member MobileNumber indicating the mobile phone number of the student. Use namespace alias such that the main() function can use either of the student class.

5. Get the definition of any student class from earlier chapters. Overload << operator. Define the student class in a namespace and use it in the main program. Using using declaration for the student object in the main() and to see that it is available without specifying.