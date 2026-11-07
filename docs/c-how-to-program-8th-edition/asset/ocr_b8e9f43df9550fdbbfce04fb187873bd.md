**3.6** *(_Default Constructor_)* What’s a default constructor? How are an object’s data members initialized if a class has only an implicitly defined default constructor?

**3.7** *(_Data Members_)* Explain the purpose of a data member.

**3.8** *(_Header and Source-Code Files_)* What’s a header? What’s a source-code file? Discuss the purpose of each.

**3.9** *(_Using a Class Without a using Directive_)* Explain how a program could use class `string` without inserting a using directive.

**3.10** *(_Set and Get Functions_)* Explain why a class might provide a set function and a get function for a data member.

**3.11** *(_Modifying Class GradeBook_)* Modify class GradeBook (Figs. 3.11–3.12) as follows:

+   a) Include a second `string` data member that represents the course instructor’s name.  
+    b) Provide a set function to change the instructor’s name and a get function to retrieve it.  
+    c) Modify the constructor to specify course name and instructor name parameters.  
+    d) Modify function `displayMessage` to output the welcome message and course name, then the string `"This course is presented by: "` followed by the instructor’s name.

Use your modified class in a test program that demonstrates the class’s new capabilities.

**3.12** *(_Account Class_)* Create an Account class that a bank might use to represent customers’ bank accounts. Include a data member of type `int` to represent the account balance. [*Note:* In subsequent chapters, we’ll use numbers that contain decimal points (e.g., 2.75)—called floating-point values—to represent dollar amounts.] Provide a constructor that receives an initial balance and uses it to initialize the data member. The constructor should validate the initial balance to ensure that it’s greater than or equal to 0. If not, set the balance to 0 and display an error message indicating that the initial balance was invalid. Provide three member functions. Member function `credit` should add an amount to the current balance. Member function `debit` should withdraw money from the Account and ensure that the debit amount does not exceed the Account’s balance. If it does, the balance should be left unchanged and the function should print a message indicating "Debit amount exceeded account balance." Member function `getBalance` should return the current balance. Create a program that creates two Account objects and tests the member functions of class Account.

**3.13** *(_Invoice Class_)* Create a class called Invoice that a hardware store might use to represent an invoice for an item sold at the store. An Invoice should include four data members—a part number (type `string`), a part description (type `string`), a quantity of the item being purchased (type `int`) and a price per item (type `double`). [*Note:* In subsequent chapters, we’ll use numbers that contain decimal points (e.g., 2.75)—called floating-point values—to represent dollar amounts.] Your class should have a constructor that initializes the four data members. Provide a set and get function for each data member. In addition, provide a member function named `getInvoiceAmount` that calculates the invoice amount (i.e., multiplies the quantity by the price per item), then returns the amount as an `int` value. If the quantity is not positive, it should be set to 0. If the price per item is not positive, it should be set to 0. Write a test program that demonstrates class Invoice’s capabilities.

**3.14** *(_Employee Class_)* Create a class called Employee that includes three pieces of information as data members—a first name (type `string`), a last name (type `string`) and a monthly salary (type `int`). [*Note:* In subsequent chapters, we’ll use numbers that contain decimal points (e.g., 2.75)—called floating-point values—to represent dollar amounts.] Your class should have a constructor that initializes the three data members. Provide a set and a get function for each data member. If the monthly salary is not positive, set it to 0. Write a test program that demonstrates class Employee’s capabilities. Create two Employee objects and display each object’s yearly salary. Then give each Employee a 10 percent raise and display each Employee’s yearly salary again.