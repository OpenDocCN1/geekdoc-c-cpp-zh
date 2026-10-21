(c) throw int error1;
(d) int error1 throw;

7. The section where the exception is handled is called ______.
(a) try
(b) throw
(c) catch
(d) throws

8. Which function can be used to have our own unexpected() function instead of the built-in unexpected() function?
(a) set_unexpected
(b) user_unexpected
(c) new_unexpected
(d) It is not possible to do so

9. The code that we want to monitor for exceptions is kept in the ______ block.
(a) try
(b) throw
(c) catch
(d) throws

10. Which of the following is the correct syntax for a catch block?
(a) catch (int);
(b) catch (int intEx);
(c) Both
(d) None

# Conceptual Exercises

+   1. What are the different mechanisms of traditional error handling? What is the problem with them?
+   2. What is the need for a communication mechanism between the library designer and the library user? How does exception handling mechanism help?
+   3. What is the problem of destroying objects? How can exception handling help here?
+   4. What is the role of each of the components of the exception handling mechanism?
+   5. What is the role of the terminate() function in exception handling? Why does the exception handling mechanism not call abort() directly?
+   6. What is the difference between throwing exceptions inside and outside the function?
+   7. What is the importance of throwing objects rather than built-in type values?
+   8. When do we need multiple catch blocks for a single try block? Give an example.
+   9. What is the importance of catch all (catch (...))?
+   10. What are exception specifications? In which cases are they needed?

11. What is rethrow? What is its use?
12. What is the set_terminate() function? Why is it needed?
13. What is the unexpected() function? Give an example to explain the need of it.
14. What is uncaught_exception() function and why do we need it?
15. What are the disadvantages of the exception handling mechanism?

# Practical Exercises

+   1. Define the Time class described in Chapter 7. Provide checking for time and throw exception when an invalid time is input, either from the constructor or the user.
+   2. Define a stack class. The class should throw an exception when the stack underflow and overflow take place.
+   3. Use the Time class to provide an overloaded ‘-’. Here the time query is also to be recorded in a file. Use C text file to store the query. If a calling function provides expression Time1 – Time2, then operator ‘-’ function should throw an exception if Time2 is a later time than Time1. Before throwing the exception, though, the operator ‘-’ function should close the file.
+   4. Define a class TheException, which contains member functions for displaying messages regarding stack underflow and overflow. When overflow occurs, it asks for increasing the stack size. If the user says yes, it should respond by increasing the stack size. Use dynamically allocated array to implement stack.
+   5. Using Time class, throw an exception when invalid time is input. Write set_terminate() to provide your own terminate function, which takes care of this problem.
+   6. Use the stack class of Problem 2. Provide exception specification as throw() to push function and throw an exception when stack is overflow. Use set_unexpected() to set your own unexpected function to take care of this situation.
+   7. Write a normal stack class and also a stack class with exception handling and use them in two different programs. Use the classes a number of times in the respective programs. (You may write a loop, which creates and destroys the class). Compare the efficiency of both the programs when (a) exceptions are thrown (b) exceptions are not thrown In addition check the run-time as well as the resultant code size.