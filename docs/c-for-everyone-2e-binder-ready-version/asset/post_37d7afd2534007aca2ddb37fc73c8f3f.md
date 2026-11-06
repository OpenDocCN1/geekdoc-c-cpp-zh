
## CHAPTER 9 CLASSES

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_416_0.png)

### CHAPTER GOALS

- To understand the concept of encapsulation
- To master the separation of interface and implementation
- To be able to implement your own classes
- To understand how constructors and member functions act on objects
- To discover appropriate classes for solving programming problems
- To distribute a program over multiple source files

### CHAPTER CONTENTS

- **9.1 OBJECT-ORIENTED PROGRAMMING** 390
- **9.2 SPECIFYING THE PUBLIC INTERFACE OF A CLASS** 392
  - *Syntax 9.1: Class Definition* 393
  - *Common Error 9.1: Forgetting a Semicolon* 395
- **9.3 DATA MEMBERS** 395
- **9.4 MEMBER FUNCTIONS** 397
  - *Syntax 9.2: Member Function Definition* 400
  - *Programming Tip 9.1: All Data Members Should Be Private; Most Member Functions Should Be Public* 402
  - *Programming Tip 9.2: const Correctness* 402
- **9.5 CONSTRUCTORS** 403
  - *Common Error 9.2: Trying to Call a Constructor* 405
  - *Special Topic 9.1: Initialized Lists* 405
  - *Special Topic 9.2: Overloading* 406
- **9.6 PROBLEM SOLVING: TRACING OBJECTS** 407
  - *How To 9.1: Implementing a Class* 409
  - *Worked Example 9.1: Implementing a Bank Account Class* 411
  - *Random Fact 9.1: Electronic Voting Machines* 412
- **9.7 PROBLEM SOLVING: DISCOVERING CLASSES** 414
  - *Programming Tip 9.3: Make Parallel Vectors into Vectors of Objects* 416
- **9.8 SEPARATE COMPILATION** 417
- **9.9 POINTERS TO OBJECTS** 422
  - *Special Topic 9.3: Destructors and Resource Management* 424
  - *Random Fact 9.2: Open Source and Free Software* 426

Here is the C++ syntax for the `CashRegister` class definition:

```cpp
class CashRegister
{
public:
   void clear();
   void add_item(double price);

   double get_total() const;
   int get_count() const;

private:
   data members—see Section 9.3
};
```

The member functions are declared in the *public section* of the class. Any part of the program can call the member functions. The data members are defined in the *private section* of the class. Only the member functions of the class can access those data members; they are hidden from the remainder of the program.

It is legal to declare the private members before the public section, but in this book, we place the public section first. After all, most programmers reading a class are class users, not implementers, and they are more interested in the public interface than in the private implementation.

The member function declarations look similar to the declarations of regular functions. These declarations do not provide any implementation. You will see in Section 9.4 how to implement the member functions.

There are two kinds of member functions, called **mutators** and **accessors**. A mutator is a function that modifies the data members of the object. The CashRegister class has two mutators: clear and add_item. After you call either of these functions, the total amount and item count are changed.

### Syntax 9.1 Class Definition

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_420_0.png)

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_421_0.png)

A mutator member function changes the object on which it operates.

An accessor member function does not change the object on which it operates. Use `const` with accessors.

Accessors just query the object for some information without changing it. The CashRegister class has two accessors: get_total and get_count. Applying either of these functions to a CashRegister object simply returns a value and does not modify the object. In C++, you should use the const reserved word to mark accessor functions (see Programming Tip 9.2 on page 402), like this:

```
    double get_total() const;
```

Member functions are invoked using the dot notation that you have already seen with string and stream functions:

```
    CashRegister register1; // Defines a CashRegister object
    register1.clear(); // Invokes a member function
```

Now we know what a CashRegister object can do, but not how it does it. Of course, to use CashRegister objects in our programs, we don't need to know. We simply use the public interface. Figure 1 shows the interface of the CashRegister class. The mutator functions are shown with arrows pointing inside the private data to indicate that they modify the data. The accessor functions are shown with arrows pointing the other way to indicate that they just read the data.

### SELF CHECK

- 5. What does the following code segment print?

```cpp
CashRegister reg;
reg.clear();
reg.add_item(0.95);
reg.add_item(0.95);
cout << reg.get_count() << " " << reg.get_total() << endl;
```

- 6. What is wrong with the following code segment?

```cpp
CashRegister reg;
reg.clear();
reg.add_item(0.95);
cout << reg.get_amount_due() << endl;
```

- 7. Declare a member function get_dollars of the CashRegister class that yields the dollar value of the total amount of the sale.
- 8. Name two accessor member functions of the string class.
- 9. Is the get member function of the ifstream class an accessor or a mutator?

### Practice It

Now you can try these exercises at the end of the chapter: R9.3, R9.7.

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_424_0.png)

*These clocks have common behavior, but each of them has a different state. Similarly, objects of a class can have their data members set to different values.*

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_424_1.png)

- 10. What is the value of `register1.item_count`, `register1.total_price`, `register2.item_count`, and `register2.total_price` after these statements?

```cpp
CashRegister register1;
register1.clear();
register1.add_item(0.90);
register1.add_item(0.95);
CashRegister register2;
register2.clear();
register2.add_item(1.90);
```

- 11. What is wrong with this code segment?

```cpp
CashRegister register2;
register2.clear();
register2.add_item(0.95);
cout << register2.total_price << endl;
```

- 12. Consider a class `Time` that represents a point in time, such as 9 A.M. or 3:30 P.M. Give two different sets of data members that can be used for implementing the `Time` class.
- 13. Suppose the implementer of the `Time` class changes from one implementation strategy to another, keeping the public interface unchanged. What do the programmers who use the `Time` class need to do?
- 14. Consider a class `Grade` that represents a letter grade, such as A+ or B. Give two different sets of data members that can be used for implementing the `Grade` class.

**Practice It** Now you can try these exercises at the end of the chapter: R9.16, R9.17, R9.18.

### 9.4 Member Functions

The definition of a class declares its member functions. Each member function is defined separately, after the class definition. The following sections show how to define member functions.

- 22. 

| key | file_count | i | arg |
| --- | --- | --- | --- |
| β | 0 | X | -d |
| -3 | 1 | Z | encrypt.txt |
|  |  | 3 |  |

Then the program prints the message
`Usage: caesar [-d] infile outfile`
and exits.

- 23. FDHVDU
- 24. It turns them into # characters. The ASCII code for a space is 32, and the # character has code 35.
- 25. It replaces the initial byte of a file with 0.
- 26. Change the process function to swap the values of the green and blue arguments. The remainder of the program stays unchanged.
- 27. You get the original image back.
- 28. We could have read the header values and pixel data sequentially, but to update the pixels, we had to move backwards.
- 29. We need 3 × 100 bytes for each scan line. There is no padding since this number is divisible by 4. The total size = 3 × 100 × 100 + 64 = 30,064 bytes.
