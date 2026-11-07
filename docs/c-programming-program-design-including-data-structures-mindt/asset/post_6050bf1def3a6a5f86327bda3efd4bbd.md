
```cpp
for (int i = 1; i < 5; i++)
    myList[i] = i * myList[i - 1];

yourList = myList;
for (int i = 0; i < 5; i++)
    yourList[i] = 2 * myList[i];
```

- 30.
  - a. Write a statement that declares votes to be pointer of type `int`. (1)
  - b. Write a C++ code that dynamically creates a two-dimensional array of 50 rows and 10 columns and votes contains the base address of that array. (8)
  - c. Write a C++ code that outputs the data stored into the array votes one row per line. (8)
  - d. Write a C++ code that deallocates the memory space occupied by the two-dimensional array to which votes points. (8)

- 31. What is the purpose of a copy constructor? (12)

- 32. Name two situations when a copy constructor executes. (12)

- 33. Name three things that you should do for classes with pointer member variables. (12)

- 34. Suppose that you have the following classes, `small` and `notSmall`:

```cpp
class small
{
public:
    void print() const;
    int add() { return x + y; }
    small() {}
    small(int a, int b) { x = a; y = b; }

private:
    int x = 0;
    int y = 0;
};

void small::print() const
{
    cout << "small: -- " << endl
         << "x: " << x << ", y = " << y << endl;
}

class notSmall: public small
{
public:
    void print() const;
    int add();
    notSmall() {}
    notSmall(int a, int b, int c)
        : small(a, b) { z = c; }

private:
    int z;
};

void notSmall::print() const
{
    small::print();
    cout << "notSmall-- z: " << z << endl;
}

int notSmall::add()
{
    return z + small::add();
}
```

What is the output of the following function `main`? (4, 12)

```cpp
int main()
{
    small *ptrSmall;
    small objectSmall(2, 3);

    notSmall objectBig(3, 5, 9);

    ptrSmall = &objectSmall;
    cout << ptrSmall->add() << endl;
    ptrSmall->print();

    cout << "*-*-*-*-*-*-*-*-*-*-*" << endl << endl;

    ptrSmall = &objectBig;
    cout << ptrSmall->add() << endl;
    ptrSmall->print();

    return 0;
}
```

- 35. What is the output of the function `main` of Exercise 34, if the definition of `small` is replaced by the following definition: (13)

```cpp
class small
{
public:
    virtual void print() const;
    virtual int add() { return x + y; }
    small() {}
    small(int a, int b) { x = a; y = b; }

private:
    int x = 0;
    int y = 0;
};
```

- 36. What is the difference between compile-time binding and run-time binding? (12)

- 37. Is it legal to have an abstract class with all member functions pure virtual? (14)

integer of any number of digits. Add operations to add, subtract, multiply, and compare integers stored in two objects. Also add constructors to properly initialize objects and functions to set, retrieve, and print the values of objects.

- 5. Banks offer various types of accounts, such as savings, checking, certificates of deposit, and money market, to attract customers as well as meet their specific needs. Two of the most commonly used accounts are savings and checking. Each of these accounts has various options. For example, you may have a savings account that requires no minimum balance but has a lower interest rate. Similarly, you may have a checking account that limits the number of checks you may write. Another type of account that is used to save money for the long term is certificate of deposit (CD).

  In this programming exercise, you use abstract classes and pure virtual functions to design classes to manipulate various types of accounts. For simplicity, assume that the bank offers three types of accounts: savings, checking, and certificate of deposit, as described next.

  **Savings accounts:** Suppose that the bank offers two types of savings accounts: one that has no minimum balance and a lower interest rate and another that requires a minimum balance and has a higher interest rate.

  **Checking accounts:** Suppose that the bank offers three types of checking accounts: one with a monthly service charge, limited check writing, no minimum balance, and no interest; another with no monthly service charge, a minimum balance requirement, unlimited check writing, and lower interest; and a third with no monthly service charge, a higher minimum requirement, a higher interest rate, and unlimited check writing.

  **Certificate of deposit (CD):** In an account of this type, money is left for some time, and these accounts draw higher interest rates than savings or checking accounts. Suppose that you purchase a CD for six months. Then we say that the CD will mature in six months. The penalty for early withdrawal is stiff. Figure 12-25 shows the inheritance hierarchy of these bank accounts.

  ![](img/b217c421655b51e7494cf3b89bb5432d_953_0.png)

  **FIGURE 12-25** Inheritance hierarchy of banking accounts

  Note that the classes `bankAccount` and `checkingAccount` are abstract. That is, we cannot instantiate objects of these classes. The other classes in Figure 12-25 are not abstract.

  `bankAccount`: Every bank account has an account number, the name of the owner, and a balance. Therefore, instance variables such as `name`, `accountNumber`, and `balance` should be declared in the abstract class `bankAccount`. Some operations common to all types of accounts are retrieve account owner's name, account number, and account balance; make deposits; withdraw money; and create monthly statements. So include functions to implement these operations. Some of these functions will be pure virtual.

  `checkingAccount`: A checking account is a bank account. Therefore, it inherits all the properties of a bank account. Because one of the objectives of a checking account is to be able to write checks, include the pure virtual function `writeCheck` to write a check.

  `serviceChargeChecking`: A service charge checking account is a checking account. Therefore, it inherits all the properties of a checking account. For simplicity, assume that this type of account does not pay any interest, allows the account holder to write a limited number of checks each month, and does not require any minimum balance. Include appropriate named constants, instance variables, and functions in this class.

  `noServiceChargeChecking`: A checking account with no monthly service charge is a checking account. Therefore, it inherits all the properties of a checking account. Furthermore, this type of account pays interest, allows the account holder to write checks, and requires a minimum balance.

  `highInterestChecking`: A checking account with high interest is a checking account with no monthly service charge. Therefore, it inherits all the properties of a no service charge checking account. Furthermore, this type of account pays higher interest and requires a higher minimum balance than the no service charge checking account.

  `savingsAccount`: A savings account is a bank account. Therefore, it inherits all the properties of a bank account. Furthermore, a savings account also pays interest.

  `highInterestSavings`: A high-interest savings account is a savings account. Therefore, it inherits all the properties of a savings account. It also requires a minimum balance.

  `certificateOfDeposit`: A certificate of deposit account is a bank account. Therefore, it inherits all the properties of a bank account. In addition, it has instance variables to store the number of CD maturity months, interest rate, and the current CD month.

  Write the definitions of the classes described in this programming exercise and a program to test your classes.

- 6. The function `retrieveAt` of the class `arrayListType` is written as a `void` function. Rewrite this function so that it is written as a value returning function, returning the required item. If the location of the item to be returned is out of range, use the assert function to terminate the program. Also, write a program to test your function. Use the class `unorderedArrayListType` to test your function.

- 7. The function `removeAt` of the class `arrayListType` removes an element from the list by shifting the elements of the list. However, if the element to be
