```
```cpp
cout << "\nThe names in the stack are:\n";

// pop names from the stack
while(!stack.empty())
{
    name = stack.front();  // retrieve the name
    stack.pop_front();     // pop name from the stack
    cout << name << endl;
}
return 0;
}
```
```

Following is a sample run of Program 13.3:

```
Enter as many names as you want, one per line
    To stop enter a single x
Enter a name (or x to stop): Jane Jones
Enter a name (or x to stop): Bill Smith
Enter a name (or x to stop): Jim Robinson
Enter a name (or x to stop): x

The names in the stack are:
Jim Robinson
Bill Smith
Jane Jones
```

# EXERCISES 13.3

+   1. **(Review)** State whether a stack is appropriate for each of the following tasks, and indicate why or why not:
+      a. A word-processing program must remember a line of up to 80 characters. Pressing the Backspace key deletes the previous character, and pressing Ctrl+Backspace deletes the entire line. Users must be able to undo deletion operations.
+      b. Customers must wait one to three months for delivery of their new cars. The dealer creates a list to determine the “fair” order in which customers should get their cars; the list is prepared in the order in which customers placed their requests for a new car.
+      c. You’re required to search downward in a pile of magazines to locate the issue for last January. Each magazine was placed on the pile as soon as it was received.
+      d. A programming team accepts jobs and prioritizes them on the basis of urgency.
+      e. A line forms at a bus stop.

+   2. **(Practice)** Enter and run Program 13.3.

+   3. **(Modify)** Modify Program 13.3 to implement a stack of integers rather than a stack of strings.