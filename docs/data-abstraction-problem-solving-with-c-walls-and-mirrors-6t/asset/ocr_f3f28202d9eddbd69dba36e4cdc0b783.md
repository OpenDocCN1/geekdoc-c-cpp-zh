```
if (toupper(userChoice) == 'A')
{
   bagPtr = new ArrayBag<string>();
   cout << "Testing the Array-Based Bag: " << endl;
}
else
{
   bagPtr = new LinkedBag<string>();
   cout << "Testing the Link-Based Bag: " << endl;
   // end if
}
cout << "The initial bag is empty. " << endl;
bagTester(bagPtr);
delete bagPtr;
bagPtr = nullptr;
cout << "All done!" << endl;
return 0;
} // end main
```

# Sample Output 1

Enter 'A' to test the array-based implementation
or 'L' to test the link-based implementation: A
Testing the Array-Based Bag:
The initial bag is empty.
isEmpty: returns 1; should be 1 (true)
Add 6 items to the bag:
The bag contains 6 items:
one two three four five one
isEmpty: returns 0; should be 0 (false)
getCurrentSize returns : 6; should be 6
Try to add another entry: add("extra") returns 0
All done!

# Sample Output 2

Enter 'A' to test the array-based implementation
or 'L' to test the link-based implementation: L
Testing the Link-Based Bag:
The initial bag is empty.
isEmpty: returns 1; should be 1 (true)
Add 6 items to the bag:
The bag contains 6 items:
one five four three two one
isEmpty: returns 0; should be 0 (false)
getCurrentSize returns : 6; should be 6
Try to add another entry: add("extra") returns 1
All done!

**Question 15** Revise the program in Listing 4-4 so that it tests first the array-based implementation and then the link-based implementation. Ensure that the program does not have a memory leak.