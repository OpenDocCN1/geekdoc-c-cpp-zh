be negative. Line 31 of Fig. 12.9 invokes the object’s print member function to output the updated BasePlusCommissionEmployee’s information, and line 34 calls member function earnings to display the BasePlusCommissionEmployee’s earnings.

# *Exploring the Similarities Between Class BasePlusCommissionEmployee and Class CommissionEmployee*

Most of the code for class BasePlusCommissionEmployee (Figs. 12.7–12.8) is similar, if not identical, to the code for class CommissionEmployee (Figs. 12.4–12.5). For example, in class BasePlusCommissionEmployee, private data members firstName and lastName and member functions setFirstName, getFirstName, setLastName and getLastName are identical to those of class CommissionEmployee. Classes CommissionEmployee and BasePlusCommissionEmployee also both contain private data members socialSecurityNumber, commissionRate and grossSales, as well as get and set functions to manipulate these members. In addition, the BasePlusCommissionEmployee constructor is almost identical to that of class CommissionEmployee, except that BasePlusCommissionEmployee’s constructor also sets the baseSalary. The other additions to class BasePlusCommissionEmployee are private data member baseSalary and member functions setBaseSalary and getBaseSalary. Class BasePlusCommissionEmployee’s print member function is nearly identical to that of class CommissionEmployee, except that BasePlusCommissionEmployee’s print also outputs the value of data member baseSalary.

We literally copied code from class CommissionEmployee and pasted it into class BasePlusCommissionEmployee, then modified class BasePlusCommissionEmployee to include a base salary and member functions that manipulate the base salary. This “copy-and-paste” approach is error prone and time consuming. Worse yet, it can spread many physical copies of the same code throughout a system, creating a code-maintenance nightmare. Is there a way to “absorb” the data members and member functions of a class in a way that makes them part of another class without duplicating code? In the next several examples, we do exactly this, using inheritance.

![](bbox=[0.114, 0.482, 0.171, 0.525])

> **Software Engineering Observation 12.3**
> *Copying and pasting code from one class to another can spread errors across multiple source code files. To avoid duplicating code (and possibly errors), we inheritance, rather than the “copy-and-paste” approach, in situations where you want one class to “absorb” the data members and member functions of another class.*

![](bbox=[0.114, 0.573, 0.171, 0.616])

> **Software Engineering Observation 12.4**
> *With inheritance, the common data members and member functions of all the classes in the hierarchy are declared in a base class. When changes are required for these common features, you need to make the changes only in the base class—derived classes then inherit the changes. Without inheritance, changes would need to be made to all the source code files that contain a copy of the code in question.*

# ### 12.4.3 Creating a CommissionEmployee–BasePlusCommissionEmployee Inheritance Hierarchy

Now we create and test a new BasePlusCommissionEmployee class (Figs. 12.10–12.11) that derives from class CommissionEmployee (Figs. 12.4–12.5). In this example, a BasePlusCommissionEmployee object is a CommissionEmployee (because inheritance