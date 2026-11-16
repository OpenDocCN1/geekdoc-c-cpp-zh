```
std::cout << "*** Insufficient funds ***\n";
 acct_ptr->display();
}
```

Here, acct_ptr is a local variable, so it occupies space on the stack. It represents a simple address, essentially a number. The space for the acct_ptr variable is automatically deallocated when faulty_func completes. The problem is acct_ptr points to memory that was allocated with new, and this memory is not freed up within the function. The pointer acct_ptr is the only way to get to that memory, so when the function is finished, that memory is lost for the life of the program. The condition is known as a memory leak. If the program runs to completion quickly, the leak may go undetected. In a longer running program such as a web server, memory leaks can cause the program to crash after a period of time. The problem arises when code that leaks memory is executed repeatedly and eventually all of available memory becomes used up.

The corrected function would be written

```
void corrected_func() {
 Account *acct_ptr = new Account("Joe", 400, 1300.00);
 if (acct_ptr->withdraw(10.00))
 std::cout << "Withdrawal successful\n";
 else
 std::cout << "*** Insufficient funds ***\n";
 acct_ptr->display();
 delete acct_ptr;
}
```

If we step back and take an honest look at this corrected_func function, we will see that there really is no reason for using pointers and dynamic memory at all. This corrected_func offers no advantage over the following function.

```
void even_better_func() {
 Account acct("Joe", 400, 1300.00);
 if (acct.withdraw(10.00))
 std::cout << "Withdrawal successful\n";
 else
 std::cout << "*** Insufficient funds ***\n";
 acct.display();
}
```

So why consider pointers to objects at all? Programmers commonly use pointers to objects to build elaborate linked data structures. Section 18.3 describes one such data structure.

C++ supports vectors and arrays of objects, but they present special challenges. First, consider a simple situation. The Point class defines no constructor, so the following code is valid:

```
std::vector<Point> pts(100); // Okay
```

The compiler happily generates code that at run time will allocate enough space for 100 Point objects. No special initializations are needed since Point has no constructor. What if a class defines a constructor that accepts arguments and does not supply also a constructor that requires no arguments? Consider the Account class. The following statement is illegal:

```
std::vector<Account> acts(100); // Illegal, the Account class has // no default constructor
```