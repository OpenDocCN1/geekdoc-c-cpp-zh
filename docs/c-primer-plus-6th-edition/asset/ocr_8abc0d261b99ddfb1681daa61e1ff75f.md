# Chapter 10 Objects and Classes

> Note\When you assign one object to another of the same class, by default C++ copies the contents of each data member of the source object to the corresponding data member of the target object.

You can use the constructor for more than initializing a new object. For example, the program has this statement in main():

```
stock1 = Stock("Nifty Foods", 10, 50.0);
```

The stock1 already exists. Therefore, instead of initializing stock1, this statement assigns new values to the object. It does so by having the constructor create a new, temporary object and then copying the contents of the new object to stock1. The program displays of the temporary object, invoking the destructor as it does so, as illustrated by the following annotated output:

```
Using a constructor to reset an object
Constructor using Nifty Foods could >> temporary object created
Bye, Nifty Foods! >> temporary object destroyed
Revised stock1:
Company: Nifty Foods Shares: 10 >> data now copied to stock1
Share Price: $50.00 Total Worth: $500.00
```

Some compilers might dispose of the temporary object later, delaying the destructor. Finally, at the end, the program displays this:

```
Done
Bye, NanoSmart!
Bye, Nifty Foods!
```

When the main() function terminates, its local variables (stock1 and stock2) pass from your plane of existence. Because such automatic variables go on the stack, the object created is the first deleted, and the first is the last deleted.(Recall that "NanoSmart" was originally in stock1 but was transferred to stock2, and stock1 was reset to "Nifty Foods\).

The output points out that there is a fundamental difference between the following two statements:

```
stock2 = Stock("Bofo Objects", 2, 2.0);
stock1 = Stock("Nifty Foods", 10, 50.0); // temporary object
```

The first of these statements invokes initialization; it creates an object with the indicated value, and it may or may not create a temporary object. The second statement invokes assignment. Using a constructor in an assignment statement in this fashion always causes the creation of a temporary object before assignment occurs.

> Tip
If you can set values either through initialization or by assignment, choose initialization. It is usually more efficient.