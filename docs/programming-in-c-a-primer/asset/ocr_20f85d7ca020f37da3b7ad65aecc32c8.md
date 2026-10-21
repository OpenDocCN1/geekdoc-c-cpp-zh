# 13.2 Modify the program in Exercise 13.1 as follows:

+   - Implement Display in Cat class
+   - Implement Display in Dog class with the new modifier
+   - Modify the driver program such that base version as well as derived versions of Display are called. Run the program. Did you face any problem? Discuss.

# 13.3 Add the modifier new to the Display member of Cat in Exercise 13.2 and the run the program. Does it make any difference? Discuss.

# 13.4 Modify the program of Exercise 13.2 as follows:

+   - Add the modifier override to Display in Cat
+   - Change the modifier new to override in the declaration of Display of Dog
+   - Make the Display method in Animal class virtual
+   Execute the program and analyse the results.

# 13.5 Modify the program of Exercise 13.1 as follows:

+   - Add another method named Sound in the base class and make it abstract
+   - Implement the Sound method in derived classes
+   - Make the base class Animal abstract
+   Execute the program and analyse the results. What would be the result if the base class Animal is not made abstract?

# 13.6 Again consider the program of Exercise 13.1. Add the modifier sealed to the base class and run the program. Any changes! Comment.

# 13.7 Define a Person class with three data members: age, name and sex.

+   - Derive a class called Employee from Person that adds a data member code to store employee code
+   - Derive another class called Specialist from Employee
+   - Add a method to each derived class to display the information about what it is.
+   Write a driver program to generate an array of three ordinary employees and another array of three specialists and display information about them.
+   Also display the information of the specialists by calling the method inherited from Employee class.

# 13.8 Assume that a bank maintains two kinds of accounts for customers, one called savings account and the other current account. The savings account provides compound interest and withdrawal facilities but no cheque book facility. The current account provides cheque book facility but no interest. Current account holders should also maintain a minimum balance and if the balance falls below this level, a service charge is imposed.

Create a class Account that stores customer name, account number and type of account. From this derive the classes Cur-Acct and Sav-Acct to make them more specific to their requirements. Include the necessary member methods in order to accomplish the following tasks